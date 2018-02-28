<template>
  <div>
    <div v-if="!$store.getters.token">
    </div>
    <div v-else>
      <h1 align="center">News Today</h1>            
          <v-layout>
            <v-flex>
              <v-card>
                <v-container fluid grid-list-md>
                  <v-layout row wrap>
                    <v-flex xs12 md6 lg3 v-for="head in news" :key="head.id">
                      <v-card flat tile>
                        <v-card-media :src=head.urlToImage height="200px">
                        </v-card-media>
                        <br>
                        <v-card-media primary-title>
                          <div>
                            <h3 class="headline mb-0">{{head.title}}</h3>
                            <div>{{head.description}}..</div>
                          </div>
                          </v-card-media>
                        <v-card-actions>
                          <v-btn flat color="orange">Share</v-btn>
                          <v-btn flat color="purple" :href=head.url target="_blank"> Explore</v-btn>
                        </v-card-actions>                        
                      </v-card>
                    </v-flex>                    
                  </v-layout>
                </v-container>
              </v-card>
            </v-flex>
          </v-layout>  
    </div>
  </div>
</template>

<script>
  import axios from "axios";
  export default {
    data() {
      return {
        news: "",
        show: false
      };
    },
    created() {
      axios
        .get(
          `https://newsapi.org/v2/top-headlines?country=id&apiKey=3de8c4841f374df1948cc06d7b299022`
        )
        .then(response => {
          // JSON responses are automatically parsed.
          this.news = response.data.articles;
        })
        .catch(e => {
          this.errors.push(e);
        });
    }
  };

</script>

<style scoped>


</style>
