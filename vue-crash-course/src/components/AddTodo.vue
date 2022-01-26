<template>
    <form @submit.prevent="onSubmit">
        <input type="text" v-model="title">
        <button type="submit"></button>
    </form>
</template>

<script>
export default {
    methods: {
        onSubmit() {
            if (this.title.trim()) {
                const newTodo = {
                    id: Date.now(),
                    title: this.title,
                    comleted: false
                }
                console.log(newTodo)
                this.$emit('add-todo', newTodo);
                this.title = ''
            }

        }
    },
    data() {
        return {
            title: '',
        }
    }
}
</script>


<style scoped>
form {
    display: flex;
}

input {
    width: 400px
}
</style>