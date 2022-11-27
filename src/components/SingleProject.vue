<template>
  <div class="project">
    <div class="col">
        <h3 @click="showDetail = !showDetail">{{project.title}}</h3>
        <div>
            <span class="material-icons">
                delete
            </span>
            <span class="material-icons">
                edit
            </span>
            <span class="material-icons">
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
            showDetail : false
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
</style>