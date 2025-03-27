<template>
    <h1>Single todo</h1>

    <input type="text" v-model="title" placeholder="Title"> <br>
    <button @click="updateTodo">Update</button>
    <button @click="DeleteTodo">Delete</button>
</template>

<script>
export default {
    data() {
        return {
            title: "",
        }
    },

    created() {
        const id = this.$route.params.id

        fetch('http://localhost:27836/api/ToDo/' + id)
            .then(data => data.json())
            .then(todo => {
                this.title = todo.title
            })
    },

    methods: {
        updateTodo() {
            const todo = {
                title: this.title,
            }

            const id = this.$route.params.id

            fetch('http://localhost:27836/api/ToDo/' + id, {
                method: 'PUT',
                headers: { 'content-type': 'application/json' },
                body: JSON.stringify(todo)
            })
                .then(() => {
                    this.$router.push('/todo')
                })

        },
        DeleteTodo() {
            const id = this.$route.params.id

            fetch('http://localhost:27836/api/ToDo/' + id, {
                method: 'DELETE',
            })
                .then(() => {
                    this.$router.push('/todo')
                })
        }
    }
}
</script>