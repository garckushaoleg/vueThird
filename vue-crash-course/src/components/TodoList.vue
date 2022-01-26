<template>
    <div>
        <ul>
            <TodoItem 
              v-for="(todo, i) in todos" 
              :todo="todo" 
              @remove-todo="removeTodo"
              :index="i"
            />
        </ul>
    </div>
</template>

<script>
import TodoItem from '@/components/TodoItem'
export default {
    props: ['todos'],
    components: {
        TodoItem
    },
    methods: {
        removeTodo(id) {
            this.$emit('remove-todo', id)
        }
    },
    mounted() {
        console.log(this.todos)
    }
}
</script>

<style scoped>
ul {
    list-style: none;
    padding: 0;
    margin: 0;
}
</style>