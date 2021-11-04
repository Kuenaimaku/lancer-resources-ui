<template>
  <section class="hero is-dark">
    <div class="hero-body">
      <p class="title">
        Pilot NET LANCER Resources
      </p>
      <p class="subtitle">
        (*/ω＼*)
      </p>
    </div>
  </section>
  <section class="section container">
    <Searchbar :search="search" :options="options" @tagSelected="searchTagSelected"/>
  </section>
  <section class="section flexContainer">
    <Resource v-for="item in filter" :key="item.resourceId" :resource="item"/>
  </section>
</template>

<script>
import Searchbar from './components/Searchbar.vue'
import Resource from './components/Resource.vue'

export default {
  components: {
    Searchbar,
    Resource
  },

  data() {
    return {
      "resources":[],
      "search":{
        "title": "",
        "tags": [],
        "allTags": true
      },
      "options":{
        "tags": [],
      }
    }
  },

  async created() {
    await this.loadResources()
    await this.loadTags()
  },

  computed: {
    filter(){
      let filtered = this.resources;
      if(this.search.tags.length != 0){
          filtered = filtered.filter( el => this.search.tags.every( x => el.tags.includes(x) ));
      }
      
      if(this.search.title !== ""){
        filtered = filtered.filter(el => el.title.toLowerCase().includes(this.search.title.toLowerCase()));
      }
      
      return filtered;
    }
  },
  methods: {
    async loadResources() {
      await fetch(`${import.meta.env.VITE_BACKEND_URL}/Resources`)
        .then(response => response.json())
        .then(data => this.resources = data)
    },
    async loadTags() {
      await fetch(`${import.meta.env.VITE_BACKEND_URL}/Resources/tags`)
        .then(response => response.json())
        .then(data => this.options.tags = data.sort())
    },
    searchTagSelected(event){
      if(this.search.tags.includes(event.tag)){
        this.search.tags.pop(event.tag)
      }
      else{
        this.search.tags.push(event.tag)
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background:#2a2a2a;
}

.section {
  background:#a2a2a2;
}

.flexContainer {
  display:flex;
  flex-direction: row;
  flex-wrap: wrap;
  column-gap: 1em;
  align-items: flex-start;
}


</style>
