<template>
  <section class="hero is-primary">
    <div class="hero-body">
      <p class="title">
        Lancer Resources
      </p>
      <p class="subtitle">
        Primary subtitle
      </p>
    </div>
  </section>
  <section class="section">
    <div class="container">
      
    </div>
  </section>
</template>

<script>
export default {
  setup() {
    const getResources = useGetResults()
    const productSearch = useSearch()
    const resultSorting = useSorting({})
    return { getResources, productSearch, resultSorting }
  }
}
function getResults(){
  fetch()
}
function useSearch(getResults) { 
}
function useSorting({ input, options }) { 
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.container{
  display:flex;
  flex-direction: column;
  flex-wrap: wrap;
  column-gap: 1em;
  align-items: flex-start;
}


</style>
