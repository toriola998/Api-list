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
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap');
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

#app {
    font-family: 'Inter', sans-serif;
}
</style>
