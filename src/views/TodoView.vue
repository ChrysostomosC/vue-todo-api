<template>
    <h1>Todo list</h1>

    <TodosList :key="todosKey" />

    <p>
        <input type="text" placeholder="Title" v-model="title"> <br>    
        <button @click="SaveTodo">Save</button>
    </p>
</template>

<script>
    import TodosList from '@/components/TodosList.vue';

    export default{
        components: {
            TodosList
        },

        data(){
            return{
                title:"",
                todosKey:0
            }
        },

        methods:{
            SaveTodo(){
                const todo = {
                    title: this.title
                }

                fetch('http://localhost:27836/api/ToDo', {
                    method: 'POST',
                    body: JSON.stringify(todo),
                    headers: { 'content-type': 'application/json' }
                })

                .then(() => {
                    this.todosKey++
                })
                
            }
        }
    }
</script>
