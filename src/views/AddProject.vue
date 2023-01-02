<template>
  <h1>Add Project</h1>
  <form @submit.prevent="addProject">
    <div class="from-group">
        <label>Project Title</label>
        <input type="text" v-model="title">
    </div>
    <div class="from-group">
        <label>Project Detail</label>
        <textarea  cols="30" rows="10" v-model="detail"></textarea>
    </div>
    <button>Add Project</button>
  </form>
</template>

<script>
import router from '@/router'
export default {
    data(){
        return {
            title:'',
            detail:'',
        }
    },
    methods: {
        addProject() {
           fetch("http://localhost:3000/projects",{
            method:"POST",
            headers: {
                "Content-Type" : "application/json"
            },
            body:JSON.stringify(
                {
                    title:this.title,
                    detail:this.detail,
                    complete:false
                }
            )
           })
           .then(()=> {
                this.$router.push('/')
            })
            .catch((err)=> {
                console.log(err);
            })
        }
    }
}
</script>

<style>
    h1 {
        color: darkred;
        margin-bottom: 50px;
    }
    .from-group label {
        display: block;
        padding-bottom: 10px;
        text-align: left;
        font-size: 16px;
        font-weight: bold;
    }
    .from-group input,
    .from-group textarea {
        width: 100%;
        box-sizing: border-box;
        padding: 10px;
        resize: none;
        margin-bottom: 10px;
        outline: none;
        font-size: 16px;
    }
    button {
        padding: 10px;
        cursor: pointer;
    }
</style>