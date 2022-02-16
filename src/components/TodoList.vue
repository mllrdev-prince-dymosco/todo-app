<template>
  <div>
    <div v-if="todo.mode">
      <div>{{todo.title}}</div>
      <div>
        <ul>
          <li v-for="(list, index) in todo.list" :key="list">
            <table>
              <tr>
                <td style="width: 20px"><input type="checkbox" v-model="todo.list[index].status" :id="list.id"/></td>
                <td><label :for="list.id">{{list.task}}</label></td>
                <td><button @click="removeTask(index)">Remove</button></td>
              </tr>
            </table>
          </li>
          <li><input v-model="newTask" @keyup.enter="addTask" placeholder="Enter a Task"/></li>
        </ul>
        <button @click="switchMode">Edit</button>
        <button @click="removeTodo(index)">Delete</button>
      </div>
    </div>

    <div v-else>
      <div>
        <input type="text" v-model="todo.title"/>
      </div>
      <div>
          <ul>
            <li v-for="(list, index) in todo.list" :key="list">
              <input type="text"  v-model="todo.list[index].task"/>
            </li>
          </ul>
          <button @click="switchMode">Save</button>
      </div>
    </div>
  </div>


</template>

<script>
  import {ref} from 'vue'
  export default {
    name: 'TodoList',
    props:["todo", "index", "removeTodo"],

    setup(props){

      const newTask = ref('')

      const addTask = () => {
        props.todo.list.push({task: newTask.value, status: false, id: Date.now()})
        newTask.value = ''
      }

      const switchMode = () => {
        props.todo.mode = !props.todo.mode
      }

      const removeTask = (index) => {
        props.todo.list.splice(index, 1)
      }

      return {newTask, addTask, switchMode, removeTask}

    }
  }
</script>

<style>

</style>
