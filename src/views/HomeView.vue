<template>
  <div class="home">
   <h1>home page</h1>
   <FilterNav @filterValue="current=$event" :current="current"></FilterNav>
   <div v-for="project in filterProjects" :key="project.id">
    <SingleProject :project="project" @delete="deleteProject" @complete="completeProject"/>
   </div>
  </div>
</template>

<script>

import FilterNav from '../components/FilterNav'
import SingleProject from '../components/SingleProject'
export default {
  components: {
    FilterNav, SingleProject 
  },
  name: 'HomeView',
  data() {
    return {
      projects:[],
      current:'all'
    }
  },
  methods: {
    deleteProject(id) {
      console.log(id);
      this.projects=this.projects.filter(project => {
        return project.id != id;
      });
      console.log(this.projects);
    },
    completeProject(id) {
      const completeProject = this.projects.find(project => {
        return project.id === id;
      })
      completeProject.complete = !completeProject.complete;
    }
  },
  computed:{
    filterProjects () {
      if(this.current === 'complete') {
        return this.projects.filter((p)=> {
            return p.complete
          })
      }else if(this.current === 'ongoing') {
        return this.projects.filter((p)=> {
            return !p.complete
          })
      }
      return this.projects
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
