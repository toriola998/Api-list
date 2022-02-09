<template>
    <div id="home">
        <div class="search">
            <input placeholder="Search API..." v-model="title" @input="getInput()"/>
        </div>
    
        <div>
            <label for="Category">Choose a Category</label>
            <select id="category" name="category">
                <option value="">Cat</option>
            </select>
        </div>
    </div>
</template>

<script>
export default {
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

<style scoped>
    #home {
    background-color: #fff;
    height: 100vh;
    width: 100%;
}
</style>