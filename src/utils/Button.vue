<script lang="ts">
    export default{
        name: "Button",
        props:{
            txt: String,
            click: Function,
            color: String,
        }
    }
</script>

<template>
    <button class="btn" :style="{backgroundColor: color}" @click="click">{{txt}}</button>
</template>

<style scoped>
    .btn{
        max-width: max-content;
        padding: 0.7rem 2rem;
        margin: 1rem;
        border-radius: 5px;
        border: 2px solid #eee;
        background-color: crimson;
        color: whitesmoke;
        font-weight: 700;
        font-size: 1rem;
        cursor: pointer;
    }
</style>