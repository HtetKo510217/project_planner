<template>
  <div class="home">
   <h1>home page</h1>
   <div v-for="project in projects" :key="project.id">
      <div>
        <h3>{{project.title}}</h3>
        <p>{{project.detail}}</p>
      </div>
   </div>
  </div>
</template>

<script>

export default {
  name: 'HomeView',
  components: {
    
  },
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
