<template>
<div class="project" :class="{ complete : project.completed }">
    <div class="actions">
        <h4 @click="showDetail">{{ project.title }} </h4>
        <div class="icons">
            <router-link :to="{ name : 'EditProject' , params : { id : project.id} }">
                <span class="material-icons">edit</span>
            </router-link>
            <span class="material-icons" @click="deleteProject">delete</span>
            <span class="material-icons" @click="toggleComplete" :class="{ complete : project.completed }">done</span>
        </div>
    </div>
    <div class="details" v-if="isVisible">
        <small>{{ project.details }}</small>
    </div>
</div>
  
</template>

<script>
export default {
    props : ['project'],
    data(){
        return {
            isVisible : false,
            uri : 'http://localhost:3000/projects/'+ this.project.id
        }
    },
    methods : {
        showDetail(){
            this.isVisible = !this.isVisible
        },
        deleteProject(){
            fetch(this.uri, { method : 'DELETE' })
            .then( ()=> this.$emit('delete', this.project.id)) 
            .catch(err => console.log(err.message))
        },
        toggleComplete(){
            fetch(this.uri, {
                 method : 'PATCH',
                 headers : { 'Content-Type' : 'application/json' },
                 body : JSON.stringify({ completed : !this.project.completed })                 
            })
            .then( ()=> this.$emit('patch', this.project.id))
            .catch(err => console.log(err.message))
        }
    }
}
</script>

<style>
    .project{
        margin: 20px auto;
        background: white;
        padding: 10px 20px;
        border-radius: 5px;
        box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.6);
        border-left: 6px solid crimson;
    }
    h4{
        cursor: pointer;
    }
    .actions{
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
    .material-icons{
        font-size: 24px;
        margin-left: 10px;
        color: #bbb;
        cursor: pointer;
    }
    .material-icons:hover{
        color: #777;
    }
    .project.complete{
        border-left: 6px solid teal;
    }
    .material-icons.complete{
        color: teal;
    }
</style>