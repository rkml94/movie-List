<template>
  <div>    <v-app-bar
        app
        elevation="0"
    >
      <v-toolbar-title v-show="$vuetify.breakpoint.mdAndUp" v-bind:style="{cursor : 'pointer'}" @click="$router.push({path: `/`})">
        <img src="../../public/movie-svgrepo-com.svg" width="40px"/>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <SearchBox/>
      <v-spacer>
      <v-btn to="/">
            <v-icon>mdi-home</v-icon></v-btn>
      <v-btn to="/search">Custom Search</v-btn>
      <v-btn to="/w/">Categories</v-btn>
    </v-spacer>
    </v-app-bar>


  </div>
</template>
<script>
import SearchBox from "@/components/SearchBox";
import axios from "axios";

export default {
  components: { SearchBox},
  data: () => ({
    drawer: false,
    selectedItem: 0,
    items: [
      {text: 'Netflix', route: '/w/8', icon: require('@/assets/img/icon-netflix.png')},
      {text: 'Prime Videos', route: '/w/119', icon: require('@/assets/img/icon-amazon.png')},
      {text: 'Disney+', route: '/w/337', icon: require('@/assets/img/icon-disney.png')},
    ],
  }),
  watch: {
    group() {
      this.drawer = false
    },
  },
  methods: {
    getRandom() {
      let randomPage = Math.floor(Math.random() * 30)
      let randomItem = Math.floor(Math.random() * 19)
      axios.get('https://api.themoviedb.org/3/movie/top_rated', {
        params: {
          api_key: '98eac8fd7eda21192db847fa47bd4a13',
          page: randomPage
        }
      }).then((response) => {
        this.randomId = response.data.results[randomItem].id

        this.$router.push({path: `/m/${this.randomId}`})
      })

    }
  }
}
</script>
