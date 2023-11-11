<template>
    <div class="todo-container">
        <span v-if="!tache.isEditing" class="span-edit">{{ tache.name }}</span>
        <input v-else v-model="editedTaskName" @blur="finishEditing(tache)" :class="this.tache.isEditing ? 'tache-input-enable' : 'tache-input-disable'" type="text"/>
        <div class="buttons-container">
            <button @click="deleteTask()" class="delete-container">
                <img class="delete-icon" src="../assets/trash-icon.png">
            </button>
            <button @click="startEditing(this.tache)" class="edit-container">
                <img class="edit-icon" src="../assets/edit-icon.png">
            </button>
        </div>
    </div>
</template>

<script>
export default {
    name: "TodoComponent",
    data() {
        return {
            editedTaskName: "",
        }
    },
    props: {
        tache: Object,
        id: Number
    },
    methods: {
        deleteTask() {
            this.$emit('deleteTaskFromTasks', this.tache.id);
        },
        finishEditing(task) {
            task.isEditing = false;
            this.$emit('editTask', { id: this.tache.id, newName: this.editedTaskName });
            console.log("Fini: ", this.editedTaskName);
            console.log("EditTask TodoComponent: ", this.tache.id);
        },
        startEditing(task) {
            task.isEditing = true;
            this.editedTaskName = this.tache.name;
            console.log(this.editedTaskName);
        }
    }
}
</script>

<style>
    .todo-container {
        width: 100%;
        padding-top: 19px;
        padding-bottom: 21px;
        display: flex;
        align-items: center;
        border-top: 1px solid orange;
        justify-content: space-between;
    }

    .tache-input-disable {
        background-color: #1a202b;
        border: none;
        color: white;
        height: 20px;
        width: 80%;
        margin-left: 5px;
        font-weight: bold;
        font-size: 16px;
    }

    .tache-input-enable {
        background-color: #1a202b;
        font-size: 15px;
        border: none;
        width: 80%;
        margin-left: 5px;
        font-weight: bold;
        color: white;
    }

    .span-edit {
        margin-left: 6px;
        font-weight: bold;
    }

    .buttons-container {
        height: 100%;
        width: 70px;
        display: flex;
        justify-content: space-around;
    }

    .edit-icon, .delete-icon {
        width: 20px;
        height: 20px;
        object-fit: cover;
    }

    .delete-container, .edit-container {
        height: 30px;
        width: 30px;
        border-radius: 30px;
        background-color: #2c313c;
        display: flex;
        justify-content: center;
        align-items: center;
        border: none;
        cursor: pointer;
    }
</style>