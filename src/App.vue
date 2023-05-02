<template>
    <div id="app">
        <CalculatorRebuild />
    </div>
</template>

<script>
    import CalculatorRebuild from "./main/CalculatorRebuild";
export default {
    components: { CalculatorRebuild }
}
</script>

<style>
* {
    font-family: 'Courier New', Courier, monospace;
}

body {
    margin: 0;
}

#app {
    display: flex;
    flex-direction: column;
    height: 100vh;
    justify-content: center;
    align-items: center;
    text-align: center;

    color: #fff;
    background: rgb(238,174,202);
    background: radial-gradient(circle, rgba(238,174,202,1) 0%, rgba(148,187,233,1) 100%);
}
</style>