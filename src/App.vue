<template>
    <Header />
    <input placeholder="Search API..." v-model="title" @input="getInput()"/>
    <label for="Category">Choose a Category</label>
    <select id="category" name="category">
        <option value="">Cat</option>
    </select>
</template>

<script>
import Header from './components/Header.vue'

export default {
    name: 'App',
    components: {
        Header
    },
    data() {
        return {
           title: '', 
        }
    },
    methods: {
        getInput(){
            //this.title = title
           console.log(this.title) 
        }
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
