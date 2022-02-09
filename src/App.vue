<template>
    <div id="app">
        <Header />
        <Home />
    </div>
</template>

<script>
import Header from './components/Header.vue'
import Home from './views/Home.vue'

export default {
    name: 'App',
    components: {
        Header,
        Home,
    }  
}
</script>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
</style>
