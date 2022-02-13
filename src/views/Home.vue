<template>
    <div id="home">
        <div class="wrapper">
            <form>
                <div class="flex-search">
                    <div class="search-wrap flex">
                        <input placeholder="Search API..." class="search" v-model="title" @input="getInput()"/>
                    </div>

                    <div class="select-wrap flex">
                        <p>Categories <img src="./../assets/arrow-down.svg" alt=""/></p>
                    </div>
                </div>
                 
            </form>
            
            <div class="container">
                <div v-for="list in apiList" :key="list.id" class="each-api">
                    <div class="flex">
                        <p class="name">{{list.API}}</p> 
                        <a :href="list.Link" target="_blank"><img src="./../assets/link.svg" alt="visit-site"/></a>
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
        //this.getApi()
    }
}
</script>

<style scoped>
    #home {
        background-color: #fff;
        height: 100vh;
        width: 100vw;
    }

    .flex {
        display: flex;
        align-items: center;
    }

    .wrapper {
        padding: 1.5rem;
    }

    input{
        outline: none;
        border: none;
    }

    .search-wrap,
    .select-wrap {
        height: 3rem;
        border-radius: 5px;
        border: 1px solid #e5e5e5;
    }

     .select-wrap {
        width: 60%;
        margin-top: 1.5rem;
        cursor: pointer;
    }

    .select-wrap p {
        font-size: 14px;
        padding-left: 2rem;
    }

    .search-wrap {
        width: 100%;
    
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

    @media screen and (min-width: 500px) {
        .search,
        .container {
            width: 70%;
            margin: auto;
        }
    }

     @media screen and (min-width: 700px) {
        .container {
            width: unset;
            display: grid;
            grid-template-columns: 40% 40%;
            justify-content: center;
            margin: auto;
            gap: 20px;
        }

        .flex-search {
            display: flex;
            justify-content: space-between;
            padding: 0 3rem;
        }

        .search-wrap {
            width: 45%;
        }

        .select-wrap {
            margin-top: unset;
            width: 30%;
        }
    }

    @media screen and (min-width: 1000px) {
        .container {
            grid-template-columns: 30% 30% 30%;
        }

         .search-wrap {
            width: 30%;
        }

        .select-wrap {
            width: 20%;
        }

         .flex-search {
            padding: 0 4rem;
        }
    }

    @media screen and (min-width: 1200px) {
        .container {
            grid-template-columns: 25% 25% 25%;
        }
    }

</style>