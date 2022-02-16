<template>
    <div>
        <button @click="addTodo">New To-Do</button>
    </div>
    <div>
        <div v-for="(todo, index) in todos" :key="todo">
            <TodoList :index="index" :todo="todos[index]" :removeTodo="removeTodo"></TodoList>
        </div>
    </div>
</template>

<script>
import TodoList from '../components/TodoList.vue'
import {ref} from 'vue'

export default {
    components: {TodoList},
    name: 'InteractiveBoard',
    setup(){
        const todos = ref([
            {
                id: Date.now(),
                title: 'To-Do #1',
                mode: true,
                list: [{task: 'First Task', status: false, id: Date.now()}]
            }
        ])
        
        const removeTodo = ((index) => {
            todos.value.splice(index, 1);
        })
        
        const addTodo = () => {
            const todo = {
                id: Date.now(),
                title: 'To-Do #' + (todos.value.length + 1),
                mode: true, 
                list:[]
            }
            todos.value.push(todo)
        }

        return {todos, removeTodo, addTodo}
    },

}
</script>

<style>
</style>