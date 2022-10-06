<script lang="ts">
export default{
    name: "Input",
    props:{
        input: String,
    }
}
</script>

<template>
  <textarea v-model="input" class="inptBox"></textarea>
</template>

<style scoped>
    .inptBox{
        margin: 2rem auto;
        width: 100%;
        min-height: 300px;
        border-radius: 10px;
        border: 2px solid #eee; 
        padding: 10px;
        font-size: 1.2rem;  
        outline: none;  
        background-color: orange;
        resize: vertical;
    }
</style>
