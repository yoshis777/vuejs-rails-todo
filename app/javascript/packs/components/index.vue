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
                <li id="row_task_1" class="collection-item">
                    <label>
                        <input type="checkbox" id="task_1">
                        <span>Sample Task</span>
                    </label>
                </li>
            </ul>
        </div>

        <!-- 完了済みタスクのリスト表示 -->
        <div class="btn">Display finished tasks</div>
        <div>
            <ul class="collection">
                <li id="row_task_2" class="collection-item">
                    <label>
                        <input type="checkbox" id="task_2" checked="checked">
                        <span>Sample Task</span>
                    </label>
                </li>
            </ul>
        </div>
    </div>
</template>