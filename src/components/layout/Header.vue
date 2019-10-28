<template>
    <header>
        <h1>TodoList</h1>
        <div id="nav">
            <router-link to="/">Home</router-link>|
            <router-link to="/about">About</router-link>
        </div>
    </header>
</template>

<script lang="ts">
// import Vue from 'vue'
export default {
    name: 'Header'
};
</script>

<style scoped>
.header {
    background: rgb(0, 0, 0);
    color: #fff;
    text-align: center;
    padding: 10px;
}

.header a {
    color: #fff;
    padding-right: 5px;
}
</style>