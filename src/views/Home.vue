<template>
  <div class="home">
    <div v-if="projects.length">
      <FilterNav @filterChanged="catchError($event)" :current="current"/>
      <div v-for="project in filtered" :key="project.id">
        <SingleProject :project = "project" @delete = "handleDelete" @patch = "handlePatch" />
      </div>
    </div>
  </div>
</template>

<script>
import SingleProject from '../components/SingleProject.vue';
import FilterNav from '../components/FilterNav.vue';
export default {
  name: 'Home',
  data(){
    return {
      projects : [],
      current : 'all'
    }
  },
  components: { SingleProject , FilterNav },
  mounted(){
    fetch('http://localhost:3000/projects')
    .then( res => res.json())
    .then(data => this.projects = data)
    .catch(err => console.log(err.message))
  },
  methods : {
    handleDelete(id){
      this.projects = this.projects.filter( (project) => {
        return project.id !== id
      })
    },
    handlePatch(id){
      let p = this.projects.find(project =>{
        return project.id === id
      })
      p.completed = !p.completed
    },
    catchError(value){
      this.current = value
    }
  },
  computed : {
    filtered(){
      if(this.current === 'completed'){
        return this.projects.filter( (project) => project.completed)
      }
      if(this.current === 'ongoing'){
        return this.projects.filter( (project) => !project.completed)
      }
      return this.projects
    }
  }
}
</script>
