<template>
  <div class="home">
   <h1>home page</h1>
   <div v-for="project in projects" :key="project.id">
    <SingleProject :project="project" @delete="deleteProject"/>
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
  methods: {
    deleteProject(id) {
      console.log(id);
      this.projects=this.projects.filter(project => {
        return project.id != id;
      });
      console.log(this.projects);
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
    .catch((err)=>{
      console.log(err);
    })
  }
}
</script>
