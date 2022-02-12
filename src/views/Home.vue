<template>
    <div id="home">
        <div class="wrapper">
            <form>
                 <div class="search-wrap">
                    <input placeholder="Search API..." class="search" v-model="title" @input="getInput()"/>
                </div>
    
                <div class="select-wrap">
                    <select id="category" name="category" v-model="categories">
                        <option value="" disabled selected hidden>Filter by category</option>
                        <option value="">atarodo</option>
                    </select>
                </div>
            </form>

            <div v-for="list in apiList" :key="list.id" class="each-api">
                <div class="flex">
                    <p class="name">{{list.API}}</p> 
                    <a :href="list.Link"><img src="./../assets/link.svg" alt="visit-site"/></a>
                </div>
                <p class="desc">{{list.Description}}</p>
                <div class="flex details"> 
                    <div>
                        <p class="title">Category</p>
                        <p>{{list.Category}}</p>
                    </div> 
                    <div class="mid-div">
                        <p class="title">HTTPs</p>
                        <p >{{list.HTTPS}}</p>
                    </div>
                    <div>
                        <p class="title">Cors</p>
                        <p>{{list.Cors}}</p>
                    </div>    
                </div> 
            </div>
        </div>    
    </div>
</template>

<script>
export default {
    data() {
        return {
           title: '', 
           categories: '',
           apiList: [],
        }
    },
    methods: {
        getInput(){
            //this.title = title
           console.log(this.title) 
        },

        getApi() {
            fetch('https://api.publicapis.org/entries')
            .then( (res) => {
                res.json().then( (data) => {
                    this.apiList = data.entries;
                    console.log(this.apiList)
                })
            })
        }
    },
    created() {
        this.getApi()
    },
    updated() {
        console.log(this.apiList)
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

    .title {
        font-size: 13px;
        margin-bottom: 3px;
    }

    .each-api div.flex {
        display: flex;
        align-items: center;
    }

    .details {
        margin-top: 2rem;
    }

    .each-api {
        margin-bottom: 2rem;
        border: 1px solid #ccc;
        border-radius: 7px;
        padding: 1.5rem;
    }

    .desc {
        margin-top: .4rem;
    }

    .mid-div{
        margin: 0 2rem;
    }

    a {
        cursor: pointer;
    }

    img {
        height: 1.5rem;
        width: auto;
    }

    .name {
        font-size: 1.2rem;
        font-weight: bold;
        margin-right: 2rem;
    }
</style>