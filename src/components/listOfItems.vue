<template>
    <div class="list">
        <ul class="tasks" v-if="this.$props.isCompleted">
            <li
                v-for="(task, index) in completedItems"
                :class="{ complete: task.complete }"
                :key="Date.now() + index"
            >
                <label
                    for="userInput"
                    :class="[task.complete ? 'checked' : null]"
                >
                    <input
                        id="userInput"
                        type="checkbox"
                        v-model="task.complete"
                        class="task-input"
                        @click="itemId = index"
                    />
                    {{ task.name }}
                </label>
            </li>
        </ul>
        <ul class="tasks" v-if="!this.$props.isCompleted">
            <li
                v-for="(task, index) in pendingItems"
                :class="{ complete: task.complete }"
                :key="Date.now() + index"
            >
                <label
                    for="userInput"
                    :class="[task.complete ? 'checked' : null]"
                >
                    <input
                        id="userInput"
                        type="checkbox"
                        v-model="task.complete"
                        class="task-input"
                        @click="itemId = index"
                    />
                    {{ task.name }}
                </label>
            </li>
        </ul>
    </div>
</template>

<script lang="js">
export default {
    name:'listOfItems',
    props:['isCompleted'],
    data() {
        return {
            tasks: [
                { name: "create skeleton of todo", complete: true, pending: false },
                { name: "add ability to add tasks", complete: true, pending: false},
                {
                    name: 'clear task name after clicking "Add"',
                    complete: false, pending: true
                },
                {
                    name: 'put "Add" button in one line with input',
                    complete: false,  pending: true
                },
                {
                    name: 'add new task by hitting Enter instead of clicking "Add"',
                    complete: false, pending: true
                },
                {
                    name: "replace <input> with <ui-checkbox> in tasks list",
                    complete: false, pending: true
                },
                { name: "when task is complete cross it out", complete: false, pending: true },
                {
                    name: 'split tasks into "pending" and "complete" tabs using keen-ui component <ui-tabs>',
                    complete: false, pending: true
                },
                { name: "don't allow to add empty tasks", complete: false, pending: true },
                {
                    name: "make list of tasks scrollable, if there're are a lot of tasks",
                    complete: false, pending: true
                },
                {
                    name: "extract list item into a separate vue.js component",
                    complete: false, pending: true
                },
                {
                    name: "persist tasks list in a local storage",
                    complete: false, pending: true
                },
                { name: "add animation on task completion", complete: false, pending: true },
            ],
            itemId: 0
        };
    },
    mounted(){
       localStorage.setItem('tasks',  JSON.stringify(this.tasks));
       this.$emit('tasks', this.tasks);
    },
    computed:{
        completedItems(condition){
            return this.tasks.filter(el => el.complete === true);
        },
        pendingItems(condition){
            return this.tasks.filter(el => el.complete === false);
        }
    }

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
    .checked {
        text-decoration: line-through;
    }
}
</style>
