<template>

    <div  id="tasks-container" class="tasks-container">
        <div style="margin-top: 16px;" class="tasks-wrapper">
            <span style="font-size: 22px;" class="float-right">
                <a class="link-description" @click="$emit('show-task-info', task)">
                    <p>topic:</p>
            <h3 class="topic">{{task.topic}}</h3>
                    <p>assignee:</p>
            <h3 class="assignee">{{user.username}}</h3>  </a>
            <button class="edit-task btn-task">
            <i  @click="$emit('edit-task-item', task)">edit</i>
            </button>
            <button class="delete-task btn-task">
            <i  @click="$emit('del-task-item', task.id)">delete</i>
            </button>
            <div class="container">

                <!-- <div style="display: none;" id="nets">A</div> -->
        </div>                
        </span>
    </div>
</div>

</template>

<script>

    export default {
        name: "Task",
        props: {
          users: [], 
          task: {}
        },
        data () {
            this.tasks = JSON.parse(localStorage.getItem("tasks"))

            return {    
                user: this.users.find(user => user.id === this.task.assigneeID)
            }
        }
    }
</script>

<style >
    .tasks-container {
        background-color: #3a6b35;
        width: 200px;
        height: 200px;
        cursor: pointer;
        box-shadow: rgba(100, 100, 111, 0.2) 0px 7px 29px 0px;
        transition: 0.2s all;
        border-radius: 5px;
    }
    .tasks-container:hover {
        background-color: #498343;
        width: 210px;
        height: 210px;
        margin-left: -5px;
        margin-top: -5px;
    }
    .tasks-wrapper {
        padding-top: 20px;
    }
    span {
        cursor: pointer;
        color: white;
    }
    p {
        font-size: 13px;
        color: white;
    }
    .link-description:hover {
        text-decoration: none;
    }
    .topic {
        font-size: 18px;
        color: white;
        margin-top: 0px;
    }
    .assignee {
        margin-top: 0px;
        font-size: 18px;
        color: white;
    }
    .btn-task {
        margin-top: 10px;
        border: none;
        font-size: 16px;
        padding: 3px 10px 3px 10px;
        border-radius: 3px;
    }
    .delete-task {
        margin-left: 5px;
        background-color: #e3b448;
    }
    .edit-task {
        background-color: #cbd18f;
        width: 60px;

    }
</style>
