<template>

    <!-- <ul class="news__list">
    <li v-for:="article in articles" 
    class="news__item"> <img :src= article.urlToImage> {{ article.title }}
    {{ article.description }}
    </li>
    </ul> -->
    <form @submit.prevent="searchNews" class="d-flex flexcolumn justify-content-center">
        <div class="input-group mx-sm-3 mb-2">
            <label class="visually-hidden" for="search">Search</label>
            <input type="search" name="search" v-model="searchTerm" key=""
                id="search" class="form-control mb-2 mr-sm-2" placeholder="Enter search term here" />
            <button class="btn btn-primary mb-2">Search</button>
        </div>
        <p>You are searching for {{ searchTerm }}</p>
    </form>

    <div class= "grid">
        <div class="card" style="width: 18rem;" v-for:="article in articles">
                <img :src= article.urlToImage class="card-img-top" alt="">
                    <div class="card-body">
                        <h5 class="card-title">{{ article.title }}</h5>
                        <p class="card-text">{{article.description}}</p>
                    </div>
            
        </div>
    </div>
    
    
</template>

<script>
export default {
    data() {
        return {
            articles: [], 
            searchTerm: ''
        }
    },
    methods: {
        searchNews() {
            let self = this;
            fetch('https://newsapi.org/v2/everything?q='+ self.searchTerm + '&language=en', {
        headers: {
            'Authorization': `Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}`,
            }
        })
            .then(function(response) {
            return response.json();
            })
            .then(function(data) {
            console.log(data);
            self.articles = data.articles;
            });
        }
    }
}
</script>

<style>
.grid{
  display: grid;
  grid-template-columns: auto auto auto;
  
}

.card{
    margin-bottom: 10px;
}

.card-text, .card-title{
    text-align: left;
}
</style>