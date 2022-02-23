<template>
    <div class="todo">
        <h1 class="title">Checklist</h1>
        <div class="container-btns">
            <button
                class="pending-btn"
                icon="Pending"
                @click="isCompleted = false"
            >
                Pending
            </button>
            <button
                class="completed-btn"
                icon="Completed"
                @click="isCompleted = true"
            >
                Completed
            </button>
        </div>

        <listOfItems
            :isCompleted="isCompleted"
            @tasks="catchTasks"
            @update="updateLocalStorage"
        ></listOfItems>

        <div class="container">
            <ui-textbox
                placeholder="Add an item here..."
                v-model="newTaskName"
            ></ui-textbox>
            <button color="primary" @click="addTask" icon="add" class="add-btn">
                Add
            </button>
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
    mounted() {
      window.addEventListener('keyup', event => {
      if (event.key === 'Enter') {
        this.addTask();
      }});
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
            localStorage.setItem('tasks',  JSON.stringify(this.tasks));
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
    font: 18px/1.4 "RobotoDraft", sans-serif;

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
    .container,
    .container-btns {
        display: flex;
        justify-content: space-around;
        align-items: baseline;
    }
    .pending-btn,
    .add-btn,
    .completed-btn {
        border: none;
        border-radius: 15px;
        color: white;
        padding: 10px 32px;
        text-align: center;
        text-decoration: none;
        display: inline-block;
        font-size: 16px;
    }
    .pending-btn {
        background-color: #e7e7e7;
        color: black;
    }
    .add-btn {
        background-color: #008cba;
    }
    .completed-btn {
        background-color: #4caf50;
    }
    input[type="checkbox"] + label {
        position: relative;
        display: flex;
        margin: 0.6em 0;
        align-items: center;
        color: #9e9e9e;
        transition: color 250ms cubic-bezier(0.4, 0, 0.23, 1);
    }
}
</style>
