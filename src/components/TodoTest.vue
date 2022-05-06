<template>
  <div class="container shadow-lg px-5 py-5 rounded-3">
    <h1 class="mb-5">Penluk To Do List</h1>
    
    <div class="d-flex mb-5">
      <input
        v-model="newTodo"
        type="text"
        placeholder="Enter To Do"
        class="form-control form-input me-3"
      />
      <button type="submit" class="submit-btn px-3 py-2" @click="addTodo()">
        +
      </button>
    </div>

    <div
      class="row todo-list shadow px-3 pt-3 pb-2 align-items-center mb-4"
      v-for="(todo, index) in todos"
      :key="index"
    >
    <div class="col-6 text-start"  @click="editTodo(index)" >
      <div class="form-check">
        <div @click="changeStatus(index)">
        <input class="form-check-input" type="checkbox" value="" id="flexCheckDefault" >
        <label class="form-check-label" for="flexCheckDefault">
          <h5 :class="{ 'todo-finished': todo.status === 'finished' }">  
           {{ todo.name }}   
          </h5>

        </label>
      </div>
      </div>
    </div>
      <div class="col-3">
        <div class="d-flex justify-content-start align-items-center">
           <div
            class="status-indicator mb-1 me-2"
            :class="{
              'status-indicator-todo': todo.status === 'to-do',
              'status-indicator-finished': todo.status === 'finished',
            }"
          ></div>   
          <div
            class="status-text"
            @click="changeStatus(index)"
            :class="{
              'status-text-todo': todo.status === 'to-do',
              'status-text-finished': todo.status === 'finished',
            }"
          >
            <h5>{{ todo.status }}</h5>
          </div>
        </div>
      </div>
      <div class="col-3" text-end action-btn >
        <div class="d-flex justify-content-start align-items-center">
       

         
           <div class="material-symbols-outlined edittodo-btn px-3 py-2"  @click="editTodo(index)">
          edit
          </div>
          <div class="me-3"></div>
           <!-- <button type="submit" class="delete-btn px-3 py-2" @click="removeTodo(todo)">
            X
           </button> -->
           <div class="material-symbols-outlined delete-btn px-3 py-2"  @click="removeTodo(todo)">
          delete
          </div>

        </div>
      </div>

    </div>
  </div>  

</template>

<script>
export default {
  name: "ToDo",
  data() {
    return {
      newTodo: "",
      indexEditTodo: null,
      tempNameTodo: "",
      tempStatusTodo: "",
      todoStatus: ["to-do", "finished"],
      todos: [
        {
          name: "Belajar ",
          status: "to-do",
        },
        {
          name: "thesis",
          status: "to-do",
        },
      ],
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo.length === 0) return;
      if (this.indexEditTodo === null) {
        this.todos.push({
          name: this.newTodo,
          status: "to-do",
        });
      } else {
        this.todos[this.indexEditTodo].name = this.newTodo;
        this.indexEditTodo = null;
      }
      this.newTodo = "";
    },
     changeStatus(index) {
      let statusIndex = this.todoStatus.indexOf(this.todos[index].status);
      if (++statusIndex > 1) statusIndex = 0;
      this.todos[index].status = this.todoStatus[statusIndex];
    },
    editTodo(index) {
      this.newTodo = this.todos[index].name;
      this.indexEditTodo = index;
    },
     removeTodo(todo) {
      this.todos.splice(this.todos.indexOf(todo), 1)
    },
    
    
    
  },
};
</script>

<style scoped>
.form-input {
  border: 1px solid rgb(243, 48, 123);
  border-radius: 50px;
}
.form-control:focus {
  box-shadow: none;

}
.submit-btn {
  background-color: rgb(30, 181, 241);
  border-radius: 50%;
  border: none;
  font-size: 20px;
  font-weight: 800;
  color: #fff;
}
.delete-btn {
  border-radius: 50%;
  border: none;
  font-size: 20px;
  font-weight: 800;
  color: rgb(255, 0, 0);
}
.edittodo-btn{

  border-radius: 10%;
  border: none;
  font-size: 20px;
  font-weight: 800;
  color: rgb(0, 255, 0);
  transition-duration: 0.4s;
}
.edittodo-btn:hover{
  background-color: #18be1e;
  color: white;
}
.todo-list {
  border-radius: 50px;
}
.todo-finished {
  font-style: italic;
  text-decoration: line-through;

}
.status-text-finished {
  color: green;
}

.status-text-todo {
  color: red;
}

</style>
