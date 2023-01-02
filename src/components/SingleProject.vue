<template>
  <div class="project" :class="{complete:project.complete}">
    <div class="col">
        <h3 @click="showDetail = !showDetail">{{project.title}}</h3>
        <div>
            <span class="material-icons" @click="deleteProject">
                delete
            </span>
            <router-link :to="{name:'editProject',params:{id:project.id}}">
                <span class="material-icons">
                    edit
                </span>
            </router-link>
            <span class="material-icons" @click="doneProject">
                done
            </span>
        </div>
    </div>
    <p v-if="showDetail">{{project.detail}}</p>
  </div>
</template>

<script>
export default {
    props:['project'],
    data() {
        return {
            showDetail : false,
            api : 'http://localhost:3000/projects/',
        }
    },
    methods: {
        deleteProject () {
            const deleteRoute = this.api + this.project.id;
           fetch(deleteRoute,{method:'DELETE'})
           .then(()=> {
            this.$emit('delete',this.project.id);
           })
           .catch((err)=> {
            console.log(err);
           });
        },
        doneProject () {
            const completeRoute = this.api + this.project.id;
            fetch(completeRoute,{
                method:'PATCH',
                headers:{
                    "Content-Type" : "application/json"
                },
                body: JSON.stringify(
                    {
                        complete : !this.project.complete
                    }
                )
            })
            .then(()=> {
                this.$emit('complete',this.project.id);
            })
            .catch((err)=> {
                console.log(err);
            })
            
        }
    }
}
</script>

<style scoped>
    .project {
        padding: 15px;
        margin: 10px;
        background: #f2f2f2;
        border-left: 4px solid red;
        border-radius: 5px;
    }
    .project h3 {
        color: indigo;
        cursor: pointer;
        padding: 5px;
    }
    .col {
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
    .col span {
        margin-left: 10px;
        padding: 4px;
        cursor: pointer;
    }
    .complete {
        border-left-color: green;
    }
</style>