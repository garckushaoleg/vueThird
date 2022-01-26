<template>
    <li>
        <span v-bind:class="{ done: todo.completed}">
            <input type="checkbox" @change="todo.completed = !todo.completed">
            <strong>{{ index + 1 }}</strong>
            {{ titleOfTodo }}
        </span>
        <button class="rm" @click="$emit('remove-todo', todo.id)">&times;</button>
    </li>
</template>

<script>
export default {
    props: {
        todo: {
            type: Object,
            required: true
        },
        index: Number
    },
    computed: {
        titleOfTodo: {
            get: function() {
                return this.todo.title.toUpperCase()
            }
        }
    }
}
</script>

<style scoped>
li {
    borser: 1px solid #ccc;
    display: flex;
    justify-content: center;
    padding: .5rem 3 rem;
    margin-bottom: 1rem;
}

.rm {
    background: red;
    color: #fff;
    border-radius: 50%;
    font-weight: bold;
}

.done {
    text-decoration: line-through;
}
</style>
