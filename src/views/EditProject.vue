<template>
    <div>
        <h1>Edit Project</h1>
        <form @submit.prevent="handleUpdate">
          <label for="title" >Title :</label>
          <input type="text" name="title" id="title" required v-model="title">

          <label for="details">Details : </label>
          <textarea id="details" required v-model="details"></textarea>

          <button>Update Project</button>
      </form>
    </div>
</template>

<script>
export default {
    props : ['id'],
    data(){
        return {
            title : '',
            details : '',
            uri : 'http://localhost:3000/projects/'+ this.id
        }
    },
    mounted(){
        fetch(this.uri)
        .then(res => res.json())
        .then(data => {
            this.title = data.title
            this.details = data.details
        })
    },
    methods : {
        handleUpdate(){
            fetch(this.uri, 
            {
                method : 'PATCH',
                headers : {'Content-Type' : 'application/json'},
                body : JSON.stringify({
                    title : this.title,
                    details : this.details
                })
            })
            .then( ()=>{
                this.$router.push('/')
            })
            .catch(err => console.log(err))
        }
    }
}
</script>

<style scoped>
    h1{
        text-align: center;
        color: #888;
    }
</style>