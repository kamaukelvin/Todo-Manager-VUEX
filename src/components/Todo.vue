<template>
<div>
  <h1>My Todo List</h1>
  <div class="todos">
      <!-- for loop with "item in items" but items in our scenarios is the getter allTodos that has access to the todos array -->

      <div v-for="todo in allTodos" v-bind:key="todo.id" class="todo">

        <!-- after looping through the array in the allTodos getter we get a single todo that we can display -->
      
      {{todo.title}}
      <i @click="deleteTodo(todo.id)" class="fas fa-trash-alt"></i>
      </div>
  </div>
</div>
</template>

<script>
// initializing getters from the store into this component
// mapActions calls the actions from our modules

import {mapGetters, mapActions} from 'vuex'

export default {
    name: "Todo",

    // our actions are called in the methods object

    // syntax for one method only

        // methods:mapAction(['getTodos'])

        // For multiple methods
    methods:{
        ...mapActions(['getTodos', 'deleteTodo'])
    },

    // defining which getters we want to use by computed and adding them as an array
    // more getters in the todo.js in store can be added in the array to utilize them here
    computed: mapGetters(['allTodos']),

    // calling the method getTodos when the component is mounted
    created(){
        this.getTodos();
    }

    

}
</script>

<style scoped>
.todos{
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-gap:1rem;
}
.todo{
    border: 1px solid #ccc;
    background: #41b883;
    padding: 1rem;
    border-radius: 5px;
    text-align:center;
    position: relative;
    cursor: pointer;

}
i{
    position: absolute;
    bottom:10px;
    right:10px;
    color: #fff;
    cursor: pointer;
}

</style>