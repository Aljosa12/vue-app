<template>
<div>
        <input id="search-box" type="text" v-model="search" placeholder="Assignee username...">
        <button id="btn-sort" @click="changeOrder()" type="button" >Sort <i class="arrow down"></i> <i class="arrow up"></i></button>
  <div class="container-wrapper">
        <div class="task" v-bind:key="task.id" v-for="task in tasksFilter">
          <Task v-bind:task="task" v-bind:users="users" v-on:del-task-item="deleteTask" v-on:show-task-info="showInfo" v-on:edit-task-item="editTask"></Task>
        </div>
    </div>


    
    <div class="modal-wrapper" tabindex="-1" role="dialog">
          <div id="myModal" class="modal">

        <div class="modal-content">
          <span id="close-details" class="close">&times;</span>
            
    <div id="data-info">
      
    </div>

        </div>

        </div>
    </div>

</div>
    
</template>

<script>
  import Task from "./TaskItem.vue"

    export default {
        name: "Tasks",
        props: {
          users: [], 
          tasks: []
        },
        components: {
          Task
        },
        data() {
        return {
          search: ''
        }
      },
        methods: {
           deleteTask(id) {
            this.$emit('del-task-event', id)
          },
          editTask(task) {
            this.$emit('edit-task-event', task)
          },
          findTasksForUser(e) {
          e.preventDefault();

          return this.tasks.filter(item => item.assignee === this.search)
        },
        changeOrder() {

          this.$emit('sort');
          },
          showInfo(task) {
              const modal = document.getElementById("myModal"),
               info = document.getElementById("data-info"),
               span = document.getElementById("close-details");

              modal.style.display = "block";

              let reporter = this.users.find(user => user.id === task.reporterID);
              let assignee = this.users.find(user => user.id === task.assigneeID);
              

              info.innerHTML = `<p>Topic</p><h3 class="task-info">${task.topic}</h3> <p>Assignee</p> <h3 class="task-info">${assignee.username}</h3><p>Description</p><h3 class="task-info">${task.description}</h3><p>Reporter</p><h3 class="task-info">${reporter.username}</h3>`;

              span.onclick = function() {
              modal.style.display = "none";
              }
              window.onclick = function(event) {

                if (event.target == modal) {
                  modal.style.display = "none";
                }
              }
            }
        },
        computed: {
      tasksFilter() {
            let assignee = this.users.find(user => user.username === this.search);
            if(assignee) {
              return this.tasks.filter(item => item.assigneeID === assignee.id)
              }
             return this.tasks
    }
}
    }

</script>

<style>

  .container-wrapper {
    width: max-content;
    margin: auto;
/* background-color: red; */
    /* border: 1px solid black; */
    display: grid;
    grid-template-columns: repeat(4, 200px);
    grid-auto-rows: 210px;
    row-gap: 5px;
    column-gap: 10px;
  }
  p {
    color: rgb(199, 199, 199);
    margin-bottom: 3px;
  }
  .task-info {
    margin-top: 4px;
    font-size: 16px;
    color: white;
    margin-bottom: 10px;
    font-weight: lighter;
  }
  .task-info::after {
    margin-top: 8px;
    content: '';
    width: 100%;
    height: 1px;
    left: 0;
    display: block;
    background-color: white;
}
  #search-box {
      margin-top: 20px;
      width: 330px;
    }
    #btn-sort {
      /* padding-left: 150px; */
       background-color: #3a6b35;
      color: white;
      border: none;
      padding: 7px;
      margin-left: 6px;
    }
  .container-wrapper:before {
    display: none;
  }

    .modal {
  display: none; /* Hidden by default */
  position: fixed; /* Stay in place */
  z-index: 1; /* Sit on top */
  left: 0;
  top: 0;
  width: 100%; /* Full width */
  height: 100%; /* Full height */
  overflow: auto; /* Enable scroll if needed */
  background-color: rgb(0,0,0); /* Fallback color */
  background-color: rgba(0,0,0,0.4); /* Black w/ opacity */
}

/* Modal Content/Box */
.modal-content {
  background-color: #fefefe;
  margin: 15% auto; /* 15% from the top and centered */
  padding: 20px;
  border: 1px solid #888;
  width: 400px; /* Could be more or less, depending on screen size */
  height: max-content; /* Could be more or less, depending on screen size */
}

/* The Close Button */
.close {
  color: #aaa;
  float: right;
  font-size: 28px;
  font-weight: bold;
}

.close:hover,
.close:focus {
  color: black;
  text-decoration: none;
  cursor: pointer;
}
.arrow {
  border: solid black;
  border-width: 0 3px 3px 0;
  display: inline-block;
  padding: 3px;
}

.up {
  margin-bottom: -2px;
  transform: rotate(-135deg);
  -webkit-transform: rotate(-135deg);
}

.down {
  margin-left: 5px;
  margin-bottom: 2px;
  transform: rotate(45deg);
  -webkit-transform: rotate(45deg);
}
</style>
