<template>
  <v-card flat>
    <div class="headline text-xs-center pa-5">
    </div>
    <v-bottom-nav
      :active.sync="bottomNav"
      :value="true"
      absolute
      color="transparent"
    >
      <v-btn
        color="teal"
        flat
        value="recent"
      >
        <span>Recent</span>
        <v-icon>history</v-icon>
      </v-btn>

      <v-btn
        color="teal"
        flat
        value="favorites"
      >
        <span>Favorites {{ starsCount }}</span>
        <v-icon>favorite</v-icon>
      </v-btn>

    </v-bottom-nav>
  </v-card>
</template>
<script>
  export default {
    props : ['stars-count'],
    data () {
      return {
        bottomNav: 'recent'
      }
    },
    watch : {
        bottomNav(){
           console.log("m hee");
           this.$emit('step',this.bottomNav);
        }
    }
  }
</script>