<template>
    <div>
        <div class="row">
            <div class="col s10 m11">
                <input class="form-controll" placeholder="Add your task!">
            </div>
            <div class="col s2 m1">
                <div class="btn-floating waves-effect waves-light red">
                    <i class="material-icons">add</i>
                </div>
            </div>
        </div>

        <!-- 未完了タスクのリスト表示 -->
        <div>
            <ul class="collection">
                <li v-for="task in tasks" v-if="!task.is_done" v-bind:id="'row_task_' + task.id" class="collection-item">
                    <label>
                        <input type="checkbox" v-bind:id="'task_' + task.id">
                        <span>{{ task.name }}</span>
                    </label>
                </li>
            </ul>
        </div>

        <!-- 完了済みタスクのリスト表示 -->
        <div class="btn" v-on:click="displayFinishedTasks">Display finished tasks</div>
        <div id="finished-tasks" class="display_none">
            <ul class="collection">
                <li v-for="task in tasks" v-if="task.is_done" v-bind:id="'row_task_' + task.id" class="collection-item">
                    <label>
                        <input type="checkbox" v-bind:id="'task_' + task.id" checked="checked">
                        <span class="line-through">{{ task.name }}</span>
                    </label>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
    import axios from 'axios'

    export default {
        data: function () {
            return {
                tasks: [],
                newTask: ''
            }
        },
        mounted: function () {
            this.fetchTasks();
        },
        methods: {
            fetchTasks: function () {
                axios.get('/api/tasks').then(
                    (response) => {
                        for (var i = 0; i < response.data.tasks.length; i++) {
                            this.tasks.push(response.data.tasks[i])
                        }
                    },
                    (error) => {
                        console.log(error)
                    }
                )
            },
            displayFinishedTasks: function() {
                document.querySelector('#finished-tasks').classList.toggle('display_none')
            }
        }
    }
</script>

<style scoped>
    [v-cloak] {
        display: none;
    }
    .display_none {
        display: none;
    }
    .line-through {
        text-decoration: line-through;
    }
</style>