<template>
    <div id="app">
        <Header />
        <AddTodo v-on:add-todo="addTodo" />
        <Todos v-bind:todos="todos" v-on:del-todo="deleteToDo" />
    </div>
</template>

<script>
import Todos from './components/Todos.vue';
import Header from './components/layout/Header';
import AddTodo from './components/AddTodo';
import axios from 'axios';
export default {
    name: 'app',
    components: {
        Todos,
        Header,
        AddTodo
    },
    data() {
        return {
            todos: []
        };
    },
    created() {
        axios
            .get('http://jsonplaceholder.typicode.com/todos?_limit=5')
            .then(res => (this.todos = res.data))
            .catch(err => console.log(err));
    },
    methods: {
        deleteToDo(id) {
            axios
                .delete('http://jsonplaceholder.typicode.com/todos/' + id)
                .then(
                    res =>
                        (this.todos = this.todos.filter(todo => todo.id != id))
                )
                .catch(err => console.log(err));
        },
        addTodo(newTodo) {
            const { title, completed } = newTodo;
            axios
                .post('http://jsonplaceholder.typicode.com/todos', {
                    title,
                    completed
                })
                .then(res => (this.todos = [...this.todos, res.data]))
                .catch(err => console.log(err));
        }
    }
};
</script>

<style>
#app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}
* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}
body {
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
}
.btn {
    display: inline-block;
    border: none;
    background: #555;
    color: #fff;
    padding: 7px 20px;
    cursor: pointer;
}
.btn:hover {
    background: #666;
}
</style>
