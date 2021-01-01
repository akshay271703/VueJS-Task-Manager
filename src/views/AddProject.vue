<template>
  <div>
      <form @submit.prevent="handleAdd">
          <label for="title" >Title :</label>
          <input type="text" name="title" id="title" required v-model="title">

          <label for="details">Details : </label>
          <textarea id="details" required v-model="details"></textarea>

          <button>Add New Project</button>
      </form>
  </div>
</template>

<script>
export default {
    data(){
        return {
            title : '',
            details : ''
        }
    },
    methods : {
        handleAdd(){
            let addProject = {
                title : this.title,
                details : this.details,
                completed : false
            }
            fetch('http://localhost:3000/projects', { 
                method : 'POST' ,
                headers : { 'Content-Type' : 'application/json' },
                body : JSON.stringify(addProject)
                })
            .then( ()=> this.$router.push('/'))
        }
    }
}
</script>

<style>
    form{
        background: white;
        padding: 20px;
        border-radius: 10px;
    }
    label{
        display: block;
        color: #bbb;
        text-transform: uppercase;
        font-size: 15px;
        font-weight: bold;
        letter-spacing: 1px;
        margin: 20px 0 10px 0;
    }
    input{
        padding: 10px;
        border: 0;
        border-bottom: 1px solid #ddd ;
        width: 100%;
        box-sizing: border-box;
    }
    textarea{
        border: 0;
        border-bottom: 1px solid #ddd;
        padding: 10px;
        width: 100%;
        box-sizing: border-box;
        height: 100px;
        outline: none;
    }
    form button{
        display: block;
        margin: 20px auto 0;
        background: #00ce89;
        color: white;
        padding: 10px;
        border: 0;
        border-radius: 6px;
        font-size: 16px;
        cursor: pointer;
    }
</style>