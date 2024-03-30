<template>
    <div id="top-banner">
        <h1>Tic Tac Toe w/ </h1>
        <img src="../assets/logo.png">
    </div>
</template>

<script>
export default{
    name: 'TopBanner',
    compontents:{},
}
</script>

<style>
h1{
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    font-family: sans-serif;
    font-weight: 700;
    font-size: 6rem;
}
img {
    display: inline;
    height: 90%;
}
#top-banner{
    height: 100px;
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 20px;
    padding: 20px;
    /* border: 1px solid black; */
}
</style>