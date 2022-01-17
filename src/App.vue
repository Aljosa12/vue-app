<template>
   <div id="app">
     <div class="modal-wrapper" tabindex="-1" role="dialog">
          <div id="myModal2" class="modal">

        <div class="modal-content modal-edit">
          <span id="close-edit" class="close">&times;</span>
          <div style="margin-top: 30px;">
            <form>
            <input class="edit-input" type="text" name="topic" v-model="topic" placeholder="Add Task topic">
            <input class="edit-input" type="text" name="description" v-model="description" placeholder="Add description">
            <input class="edit-input" type="text" name="assignee" v-model="assignee" placeholder="Add assignee">
            <input class="edit-input" type="text" name="reporter" v-model="reporter" placeholder="Add reporter">
            <button id="btn-edit-task" >Edit Task</button>
            </form>
          </div>
          
        </div>

        </div>
    </div>
    <div>
        
    </div>
     
    <AddTask  v-on:add-task-event="addTask"/>
    <Tasks v-bind:tasks="tasks" v-on:del-task-event="deleteTask" v-on:sort="changeOrder" v-on:edit-task-event="editTask"/>
    <h1 style="color: white;">This are today's tasks</h1>
  </div>
</template>

<script>
import Tasks from './components/tasks/Tasks'
import AddTask from './components/tasks/AddTask'

export default {
  name: 'App',
  components: {
    Tasks,
    AddTask
  },
  data () {
    
    return {
      tasks: [],
      topic: '',
      description: '',
      assignee: '',
      reporter: '' 
    }
  },
  methods: {
    addTask(newTask){
      this.tasks = [...this.tasks, newTask]
    },
    deleteTask(id){
      this.tasks = this.tasks.filter(task => task.id !== id);
    },
    editTask(task) {
      const modal = document.getElementById("myModal2"),
       span = document.getElementById("close-edit"),
       btnEdit = document.getElementById("btn-edit-task");

      modal.style.display = "block";
      span.onclick = function() {
          modal.style.display = "none";
      }
      window.onclick = function(event) {

          if (event.target == modal) {
           modal.style.display = "none";
        }
      }

      btnEdit.addEventListener("click", ()=> {
        this.users = JSON.parse(localStorage.getItem('users'))
        let reporter = this.users.find(user => user.username === this.reporter);
        let assignee = this.users.find(user => user.username === this.assignee);

        task.description = this.description;
        task.topic = this.topic;
        task.assigneeID = assignee.id;
        task.reporterID = reporter.id;

      })  

    },
    changeOrder() {
            this.tasks = this.tasks.reverse();
    },
    editTaskData(e){
      console.log(e)
    },
    editBookItemEvent(task){
      //find the index of this id's object
      let objIndex = this.tasks.findIndex(obj => obj.id === task.id)
      //update the item
      this.tasks[objIndex].title = task.title;
    }
  },
  watch: {
    tasks: {
      handler() {
        localStorage.setItem('tasks',JSON.stringify(this.tasks))
        },
      deep: true
    },
    users: {
      handler() {
        // localStorage.setItem('users',JSON.stringify(this.users))
        },
      deep: true
    }
  },
  mounted() {
  if (localStorage.getItem("tasks")){
    this.tasks = JSON.parse(localStorage.getItem("tasks"))
  } else {
    let users = [
        {
          id: 0,
          name: 'Peter',
          lastname: 'Parker',
          username: 'Pete'
        },
        {
          id: 1,
          name: 'Mark',
          lastname: 'Martich',
          username: 'Marc'
        },
        {
          id: 2,
          name: 'Matt',
          lastname: 'Mason',
          username: 'Mason'
        },
        {
          id: 3,
          name: 'Ewan',
          lastname: 'Lynn',
          username: 'Ewan'
        },

      ]
   
    localStorage.setItem('users', JSON.stringify(users))
    const initialTasks = [
        {
          id: 0,
          topic: 'Go shopping',
          description: 'shopp',
          assigneeID: 2,
          reporterID: 3
        },
        {
          id: 1,
          topic: 'Go skydiving',
          description: 'Sky',
          assigneeID: 2,
          reporterID: 1
        },
        {
          id: 2,
          topic: 'Go shopping',
          description: 'shopp',
          assigneeID: 0,
          reporterID: 2
        },
        {
          id: 3,
          topic: 'Go skydiving',
          description: 'Sky',
          assigneeID: 1,
          reporterID: 2
        },
        {
          id: 4,
          topic: 'Go shopping',
          description: 'shopp',
          assigneeID: 2,
          reporterID: 3
        },
        {
          id: 5,
          topic: 'Go skydiving',
          description: 'Sky',
          assigneeID: 0,
          reporterID: 2
        },
        {
          id: 6,
          topic: 'Go shopping',
          description: 'shopp',
          assigneeID: 1,
          reporterID: 0
        },
        {
          id: 7,
          topic: 'Go skydiving',
          description: 'Sky',
          assigneeID: 3,
          reporterID: 1
        }
        ,
        {
          id: 8,
          topic: 'Go skydiving',
          description: 'Sky',
          assigneeID: 0,
          reporterID: 1
        }
      ]
   
    localStorage.setItem('tasks', JSON.stringify(initialTasks))
  }

}
}
</script>

<style >
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#btn-edit-task {
  display: block;
  margin: auto;
  width:320px;
  margin-top: 6px;
  margin-right: 15px;
  height: 33px;
  border: none;
}
.edit-input {
  width:320px;
  margin-top: 6px;
}
.modal-content {
  background-color: #6548ad;
}
</style>
