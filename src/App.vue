<template>
    <Header />
</template>

<script>
import Header from './components/Header.vue'


export default {
    name: 'App',
    components: {
        Header
        }
}
</script>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
#app {
    background-color: #fff;
    height: 100vh;
    width: 100%;
}
</style>
