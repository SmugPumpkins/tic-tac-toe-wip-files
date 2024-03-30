<template>
    <div class="board center_flex" ref="board" :style="maxStyle">
        <div class="board_grid" ref="board_grid" :style="gridStyle">
            <TicTacSpace v-for="(value, index) in flattenSquares" :key="index" :value="value" class="space"
                @click="makeMove(index)" />
        </div>
    </div>
</template>

<script>
import TicTacSpace from './Tic-Tac-Space.vue'
export default {
    name: 'TicTacBoard',
    components: {
        TicTacSpace,
    },
    mounted() {
        this.$nextTick(() => {
            this.updateBoardMaxHeight();
        });

        // Define and attach the resize event listener
        this.resizeHandler = () => {
            this.updateBoardMaxHeight();
        };
        window.addEventListener('resize', this.resizeHandler);
    },
    beforeDestroy() {
        // Make sure to remove the event listener when the component is destroyed
        window.removeEventListener('resize', this.resizeHandler);
    },
    data() {
        return {
            rules: {
                rowToWin: true,
                nInALine: 3,
                alternateXO: true,
                chooseXO: false,
                rows: 3,
                columns: 3,
            },
            squares: this.setGrid(3,3),
            currentPlayer: 'X',
            boardHeight: 0,
            boardWidth: 0,
            maxHeight: window.innerHeight,
            
        }
    },
    computed: {
        flattenSquares() {
            return this.squares.flat(); // Use the JavaScript Array .flat() method
        },
        maxStyle() {
            console.log("max height: " + this.maxHeight);
            return {
                'max-height': `${this.maxHeight}px`,
                'height': `${this.maxHeight}px` // Use maxHeight for max-height style
            };
        },
        gridStyle() {
            const rows = this.squares.length;
            const cols = this.squares[0].length;
            const h = this.boardHeight;
            const w = this.boardWidth;
            const containerRatio = w / h;
            const gridRatio = cols / rows;
            const colGap = (cols + 1) * 2;
            const rowGap = (rows + 1) * 2;
            const columnsByWidth = (100 - colGap) / cols;
            const columnsByHeight = (100 - colGap) * ((gridRatio / containerRatio) / cols);
            const rowsByWidth = (100 - rowGap) * (((rows / cols) / (h / w)) / rows);
            const rowsByHeight = (100 - rowGap) / rows;

            //console.log("h: " + this.boardHeight + " w: " + this.boardWidth);
            console.log("h: " + this.boardHeight + " w:" + this.boardWidth);
            if (gridRatio < containerRatio) {
                console.log("value returned")
                return {
                    'grid-template-columns': `repeat(${cols}, ${columnsByHeight}%)`,
                    'grid-template-rows': `repeat(${rows}, ${rowsByHeight}%)`,
                }
            } else {
                console.log("value returned")
                return {
                    'grid-template-columns': `repeat(${cols}, ${columnsByWidth}%)`,
                    'grid-template-rows': `repeat(${rows}, ${rowsByWidth}%)`,
                }
            }
        },
    },
    methods: {
        switchPlayer() {
            this.currentPlayer = this.currentPlayer === 'X' ? 'O' : 'X';
        },
        makeMove(flatIndex) {
            const rows = this.squares.length;
            const columns = this.squares[0].length;
            const row = Math.floor(flatIndex / columns);
            const col = flatIndex % columns;
            if (this.squares[row][col] === null) {
                if (this.rules.alternateXO) {
                    this.squares[row][col] = this.currentPlayer;
                    this.switchPlayer();
                }
            }
        },
        setGrid(columns, rows) {
            let grid = []; // Initialize the grid array
            for (let i = 0; i < rows; i++) { // Outer loop for each row
                let row = []; // Initialize the row array
                for (let j = 0; j < columns; j++) { // Inner loop for each column in a row
                    row.push(null); // Add a null for each column in the current row
                }
                grid.push(row); // Add the completed row to the grid
            }
            return grid; // Return the constructed grid
        },
        updateBoardSize() {
            const board = this.$refs.board_grid;
            if (board) {
                this.boardHeight = board.offsetHeight;
                this.boardWidth = board.offsetWidth;
                console.log("h: " + this.boardHeight + " w:" + this.boardWidth);
            }
        },
        updateBoardMaxHeight() {
            const board = this.$refs.board;
            if (board) {
                const rect = board.getBoundingClientRect();
                this.maxHeight = (window.innerHeight - (rect.top)) * 0.99; // Calculate max height
                console.log(this.maxHeight, rect.top, window.innerHeight);
            }
            this.$nextTick(() => {
                this.updateBoardSize();
            });
        },
        checkGameState(){
            for (let i = 0; i < this.r; i++){

            }
        },
    }
}
</script>

<style>
.board {
    width: 60%;
    margin: auto;
    overflow: hidden;
}

.board_grid {
    width: 100%;
    height: 90%;
    display: grid;
    gap: 2%;
    padding: 2%;
    align-items: center;
    justify-content: center;
}

.space {
    border: 8px solid black;
    border-radius: 25px;
    display: flex;
    justify-content: center;
    align-items: center;
    aspect-ratio: 1/1;
}
</style>