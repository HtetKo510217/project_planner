<template>
  <div class="project" @click="showDetail = !showDetail">
    <h3>{{project.title}}</h3>
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
        cursor: pointer;
        background: #f2f2f2;

    }
    .project h3 {
        color: indigo;
        
    }
</style>