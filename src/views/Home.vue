<template>
    <div id="home">
        <div class="wrapper">
            <form>
                 <div class="search-wrap">
                    <input placeholder="Search API..." class="search" v-model="title" @input="getInput()"/>
                </div>
    
                <div class="select-wrap">
                    <select id="category" name="category" v-model="categories">
                        <option value="" disabled selected hidden>Filter by region</option>
                        <option value="">Cat</option>
                    </select>
                </div>
            </form>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
           title: '', 
           categories: '',
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

    .wrapper {
        padding: 1.5rem;
    }

    input, select {
        outline: none;
        border: none;
    }

    .search,
    select {
        height: 3rem;
        border-radius: 5px;
        border: 1px solid #e5e5e5;
    }

    .search {
        width: 100%;
        padding-left: 2rem;
    }

    .search::-webkit-input-placeholder { /* Edge */
        font-family: inherit;
    }

    .search:-ms-input-placeholder { /* Internet Explorer 10-11 */
        font-family: inherit;
    }

    .search::placeholder {
        font-family: inherit;
    }

    select {
        width: 60%;
        margin-top: 1.5rem;
    }
</style>