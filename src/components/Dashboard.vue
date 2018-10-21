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
                <Main v-if="recent == 'recent'"></Main>
            </v-card-text>
            <Footer @step="step"></Footer>
          </v-card>
        </v-flex>
    </v-layout>
    </div>
</template>

<script>
  import Footer from "./Footer";
  import Main   from './Main';
  export default {
    components: {Footer,Main},
    data(){
        return {recent : 'recent'}
    },
    methods : {
        step(value){
           this.recent = value;
        }
    }
  }
</script>
