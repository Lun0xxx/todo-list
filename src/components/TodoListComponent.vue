<template>
    <div class="todo-list-container">
        <div class="todo-list">
            <TodoComponent v-for="task in tasks" :key="task.id" :id="task.id" :tache="task" @deleteTaskFromTasks="deleteTaskFromTasks" @editTask="editTask"/>
        </div>
    </div>
    <button @click="resetList()" class="reset-button">Reset</button>
</template>

<script>
import TodoComponent from './TodoComponent.vue'

export default {
    name: "TodoListComponent",
    components: {
        TodoComponent
    },
    props: {
        tasks: Array
    },
    emits: ['deleteTaskFromTasks', 'resetList', 'editTask'],
    methods: {
        resetList() {
            this.$emit('resetList');
        },
        deleteTaskFromTasks(taskId) {
            console.log("Id depuis TodoListComponent.vue: ", taskId);
            this.$emit("deleteTaskFromTasks", taskId);
        },
        editTask(taskObject) {
            console.log("EditTask TodoListComponent: ", taskObject.id);
            this.$emit('editTask', taskObject);
        }
    }
}
</script>

<style>
    .todo-list-container {
        border: 2px solid orange;
        margin-top: 2%;
        width: 40%;
        border-radius: 5px;
        min-height: 50px;
        max-height: 495px; /* Ajustez cette hauteur maximale en fonction de vos besoins */
    /* Activer la barre de défilement si nécessaire */
        display: flex;
        align-items: center;
        justify-content: center;
        flex-direction: column;
    }
  
    .todo-list {
        display: flex;
        flex-direction: column;
        height: 100%;
        width: 95%;
        overflow: scroll;
    }

    .todo-list-container .todo-list > .todo-container:first-child {
        border: none;
    }

    .reset-button {
        width: 60px;
        height: 40px;
        background-color: orange;
        color: white;
        border-radius: 5px;
        border: none;
        font-weight: bold;
        cursor: pointer;
        margin-top: 10px;
    }
</style>