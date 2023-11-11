<template>
    <div id="todo-creator">
      <h2>Todo List</h2>
      <div class="todo-input-container">
        <input class="new-task-input" v-model="newTask" type="text" placeholder="Enter your task">
        <button @click="addTask(newTask)" class="add-button">Add</button>
      </div>
      <TodoListComponent @deleteTaskFromTasks="deleteTaskFromTasks" @resetList="resetList()" @editTask="editTask" :tasks="tasks"></TodoListComponent>
    </div>
</template>

<script>
import TodoListComponent from './TodoListComponent.vue'

export default {
    name: "TodoCreator",
    data() {
        return {
            tasks: [],
            taskId: -1,
            newTask: ""
        }
    },
    components: {
        TodoListComponent
    },
    methods: {
        showTask() {
            this.tasks.forEach(objet => {
                console.log("Id: ", objet.id, " Nom: ", objet.name);
            });
        },
        addTask(task) {
            console.log(task);
            if (task.trim() !== "") {
                this.taskId++;
                this.tasks.push({ id: this.taskId, name: task, isEditing: false });
                this.saveTasks();
                this.newTask = "";
                this.showTask(); 
            }
        },
        saveTasks() {
            localStorage.setItem('tasks', JSON.stringify(this.tasks));
            localStorage.setItem('taskId', this.taskId);
        },
        deleteTaskFromTasks(id) {
            this.tasks = this.tasks.filter((tache) => tache.id !== id);
            this.tasks.forEach(task => {
                console.log("Tâche: ", task.name, " - Id: ", task.id);
            })
            this.saveTasks();
        },
        resetList() {
            this.tasks = [];
            this.taskId = -1;
            this.saveTasks();
        },
        editTask(taskObject) {
            console.log("EditTask TodoCreator : ", taskObject.id);
            console.log("Before: ");
            this.tasks.forEach((task) => {
                console.log("Id: ", task.id, " Name: ", task.name);
            })
            const task = this.tasks.find(task => task.id === taskObject.id);

            if (task) {
                task.name = taskObject.newName;
                this.saveTasks();
            }
        }
    },
    created() {
        const data = localStorage.getItem("tasks");
        const id = localStorage.getItem('taskId');
        
        this.tasks = data ? this.tasks = JSON.parse(data) : this.tasks = [];
        this.taskId = id ? this.taskId = id : -1;
    }
}
</script>
  
<style>
    #todo-creator {
        width: 100%;
        display: flex;
        align-items: center;
        flex-direction: column;
    }
    
    h2 {
        color: orange;
    }
    
    .todo-input-container {
        width: 250px;
        height: 5%;
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
    
    .new-task-input {
        width: 70%;
        background-color: #232933;
        border: none;
        height: 100%;
        border-radius: 5px;
        font-weight: bold;
        padding-left: 10px;
        color: white;
        outline: none;
    }
    
    .add-button {
        width: 20%;
        height: 100%;
        background-color: orange;
        color: white;
        border-radius: 5px;
        border: none;
        font-weight: bold;
        cursor: pointer;
    }
</style>
  