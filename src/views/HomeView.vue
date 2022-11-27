<template>
  <div class="home">
   <h1>home page</h1>
   <div v-for="project in projects" :key="project.id">
    <SingleProject :project="project" />
   </div>
  </div>
</template>

<script>

import SingleProject from '../components/SingleProject'
export default {
  components: { SingleProject },
  name: 'HomeView',
  data() {
    return {
      projects:[],
    }
  },
  mounted () {
    fetch('http://localhost:3000/projects')
    .then((response)=>{
      return response.json()
    })
    .then((datas)=> {
      this.projects = datas
    })
    .catch(()=>{

    })
  }
}
</script>
