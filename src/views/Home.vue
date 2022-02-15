<template>
    <div id="home">
        <div class="wrapper">
            <form>
                <div class="flex-search">
                    <div class="search-wrap flex">
                        <input placeholder="Search API..." class="search" v-model="title"/>
                    </div>

                    <div class="select-wrap">
                        <div class="flex" style="padding-top: .7rem;" @click="showCategory = !showCategory">
                            <p>Categories</p>
                            <img src="./../assets/arrow-down.svg" alt=""/>
                        </div> 

                        <div class="categories" v-if="showCategory">
                           <div v-for="category in categories" :key="category.id">
                                <p class="category"> {{category}}</p>
                            </div>
                        </div>  
                    </div>
                </div> 
            </form>
            
            <!--DISPLAY WHEN PAGE IS STILL LOADING-->
            <p v-if="isLoading" class="loading">Loading...</p>

            <!--DISPLAY WHEN THERE'S A PROBLEM-->
            <div class="not-found" v-if="notFound">
                <h1>404</h1>
                <p>Sorry, no result found!</p>
            </div>

            <!--DISPLAY DATA WHEN API FETCH IS SUCCESSFUL-->
            <div class="container" v-if="!isLoading">
                <div v-for="list in searchAPI" :key="list.id" class="each-api">
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
           categories: [],
           apiList: [],
           showCategory: false,
           isLoading: false,
           notFound: false,
        }
    },
    methods: {
        getApi() {
            this.isLoading = true;
            fetch('https://api.publicapis.org/entries')
            .then( (res) => {
                if( res) {
                     res.json().then( (data) => {
                    this.isLoading = false;
                    this.apiList = data.entries;
                    console.log(this.apiList)

                    //DO NOT REPEAT CATEGORIES OF API
                    this.apiList.forEach( (api) => {
                        if(this.categories.indexOf(api.Category) !== -1){
                            return true
                        }
                        this.categories.push(api.Category)
                        //console.log(this.categories)
                    })
                })
                } else {
                    console.log('something is wrong')
                    this.notFound = !this.notFound;
                }
            })
        },     
    },

    computed: {
        searchAPI() {
            return this.apiList.filter(list => {
                return (
                list.API.toLowerCase().includes(this.title.toLowerCase()) 
                //|| avenge.quote.toLowerCase().includes(this.search.toLowerCase())
                );
            });
        },
        
    
    
    },

    mounted() {
        this.getApi()
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

    .search {
        padding-left: 2rem;
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

    .container {
        padding-top: 3rem;
    }

    .categories {
        border: 1px solid #e5e5e5;
        border-radius: 5px;
        margin-top: 2rem;
        z-index: 99;
        padding: 1.5rem 0;
        background-color: #fff;
        overflow-y: scroll;
        height: 60vh;
    }

    .category {
        padding-bottom: 12px;
        font-size: 17px;
        
    }

    .loading {
        /* Center vertically and horizontally */
        position: absolute;
        top: 60%;
        left: 50%;
        transform: translate(-50%, -50%);
        animation: load 1s alternate infinite ease-in;
    }

    @keyframes load {
        0%   {transform: scale(.9);}
        100% {transform: scale(1.4);}
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

    .not-found {
        /* Center vertically and horizontally */
        position: absolute;
        top: 65%;
        left: 50%;
        transform: translate(-50%, -50%);
    }

    .not-found p,
    .not-found h1{
        text-align: center;
    }

    h1 {
        font-size: 4.5rem;
    }

    @media screen and (min-width: 500px) {
        .search,
        .container {
            width: 70%;
            margin: auto;
        }

        .select-wrap {
            width: 40%;
        }

        .search {
            padding-left: unset;
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
            padding: 0 2rem;
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
            padding-top: 5rem;
        }

         .search-wrap {
            width: 30%;
        }

        .select-wrap {
            width: 20%;
        }

         .flex-search {
            padding: 0 2.5rem;
        }

        .not-found {
            top: 55%;
        }

        h1 {
            font-size: 6rem;
        } 

        .not-found p {
            font-size: 19px;
        }

    }

    @media screen and (min-width: 1200px) {
        .container {
            grid-template-columns: 25% 25% 25%;
        }

         .flex-search {
            padding: 0 6rem;
        }
    }

    @media screen and (min-width: 1400px) {
        #home {
            max-width: 1320px;
            margin: auto;
        }   
    }

</style>