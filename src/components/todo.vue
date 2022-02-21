<template>
    <div class="todo">
        <h1 class="title">Checklist</h1>
        <div class="container-btns">
            <ui-button
                color="primary"
                icon="Pending"
                @click="isCompleted = false"
                >Pending</ui-button
            >
            <ui-button
                color="primary"
                icon="Completed"
                @click="isCompleted = true"
                >Completed</ui-button
            >
        </div>

        <listOfItems
            :isCompleted="isCompleted"
            @tasks="catchTasks"
        ></listOfItems>

        <div class="container">
            <ui-textbox
                placeholder="e.g. 'read vue.js guide'"
                v-model="newTaskName"
            ></ui-textbox>
            <ui-button
                color="primary"
                @keypress.enter="addTask"
                icon="add"
                @click="addTask"
                >Add</ui-button
            >
        </div>
    </div>
</template>

<script lang="js">
import listOfItems from './listOfItems';

export default {
    data() {
        return {
            newTaskName: "",
            tasks:[],
            isCompleted: false,
        };
    },
    components:{
        listOfItems
    },
    methods: {
        addTask() {
            if(this.newTaskName.length === 0) return;
            this.tasks.push({ name: this.newTaskName, complete: false });
            this.newTaskName = "";
            this.updateLocalStorage();
        },
        catchTasks(tasks){
            this.tasks = tasks;
        },
        updateLocalStorage(){
            if(localStorage.getItem('tasks')) {
                localStorage.removeItem('tasks');
                localStorage.setItem('tasks',  JSON.stringify(this.tasks));
            }
        }
    },

};
</script>

<style scoped lang="scss">
.todo {
    margin: auto;
    background: #fff;
    padding: 20px;
    border-radius: 5px;
    box-shadow: rgba(0, 0, 0, 0.3) 3px 3px 15px;

    .title {
        margin-top: 0;
    }

    .tasks {
        list-style: none;
        width: 400px;
        height: 200px;
        padding: 0;
        overflow: auto;
    }
    .container {
        display: flex;
        justify-content: space-around;
        align-items: baseline;
    }
}
</style>
