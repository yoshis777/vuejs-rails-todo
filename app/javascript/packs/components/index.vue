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
        <div class="btn">Display finished tasks</div>
        <div>
            <ul class="collection">
                <li v-for="task in tasks" v-if="task.is_done" v-bind:id="'row_task_' + task.id" class="collection-item">
                    <label>
                        <input type="checkbox" v-bind:id="'task_' + task.id" checked="checked">
                        <span>{{ task.name }}</span>
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
            }
        }
    }
</script>