<template>
  <div class="home">
    <div v-if="projects.length">
      <div v-for="project in projects" :key="project.id">
        <SingleProject :project = "project" @delete = "handleDelete" @patch = "handlePatch" />
      </div>
    </div>
  </div>
</template>

<script>
import SingleProject from '../components/SingleProject.vue';
export default {
  name: 'Home',
  data(){
    return {
      projects : []
    }
  },
  components: { SingleProject },
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
    }
  }
}
</script>
