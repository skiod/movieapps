<template>

    <div>
      <v-layout>
        <v-flex xs12 sm6 offset-sm3>
          <v-card>
            <img src="@/assets/popcorn.png"/>
            <v-card-title class="justify-center" primary-title>
                <h3 class="headline mb-0 text-md-center">Movies</h3>
            </v-card-title>
            <v-card-text>
                <Main @push-stars="getStars" v-if="recent == 'recent'"></Main>
                <Favorite :items="stars" v-if="recent == 'favorites' "></Favorite>
            </v-card-text>
            <Footer @step="step" :stars-count="stars.length"></Footer>
          </v-card>
        </v-flex>
    </v-layout>
    </div>
</template>

<script>
  import Footer from "./Footer";
  import Main   from './Main';
  import Favorite from './Favorite';
  export default {
    components: {Footer,Main,Favorite},
    data(){
        return {
            recent : 'recent',
            stars : [],
        }
    },
    methods : {
        step(value){
           this.recent = value;
        },
        getStars(stars){
            this.stars = stars;
            console.log("x",stars);
        }
    }
  }
</script>
