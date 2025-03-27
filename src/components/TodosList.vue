<template>
    <h2>Todos</h2>

    <p v-for="todo in todos" :key="todo.id">

        <router-link :to="'/todo/' + todo.id">{{ todo.title }} </router-link>
        <input type="checkbox" v-model="todo.completed" />
        <span :class="{ completed: todo.completed }">{{ todo.completed ? 'Completed' : 'Not Completed' }}</span>    
    
    </p>
</template>

<script>
    export default{
        name: 'todosList',

        data(){
            return{
                todos:[]
            }
        },

        created(){
            fetch('http://localhost:27836/api/ToDo')
            .then(data => data.json())
            .then(todos => {
                this.todos = todos
            })
        }
    }
</script>

<style>
.completed {
  text-decoration: line-through;
}
</style>