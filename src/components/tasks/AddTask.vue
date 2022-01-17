<template>
    <div>
        <form @submit="addTask">
            <input type="text" name="topic" v-model="topic" placeholder="Add Task topic">
            <input type="text" name="description" v-model="description" placeholder="Add description">
            <input type="text" name="assignee" v-model="assignee" placeholder="Add assignee">
            <input type="text" name="reporter" v-model="reporter" placeholder="Add reporter">
            <button class="add-task" type="submit">Add Task</button>
        </form>
    </div>
</template>

<script>
    export default {
        
        name: "Task",
        data () {
            return {
                topic: '',
                description: '',
                assignee: '',
                reporter: ''
            }
        },
        methods: {  
            addTask(e){
                if(this.topic !== "") {
                    e.preventDefault();
                
                let idNum = 0;  

                this.tasks = JSON.parse(localStorage.getItem("tasks"))
                this.users = JSON.parse(localStorage.getItem('users'))

                console.log(this.users)

                let reporter = this.users.find(user => user.username === this.reporter);
                let assignee = this.users.find(user => user.username === this.assignee);


                // Get last id from array and set id +1
                if (this.tasks.length !== 0) {
                    console.log('555')
                    idNum = this.tasks[Object.keys(this.tasks)[Object.keys(this.tasks).length - 1]].id + 1
                }
            
                const newTask = {
                id: idNum,
                topic: this.topic,
                description: this.description,
                assigneeID: assignee.id,
                reporterID: reporter.id
                }

                
    
                this.$emit('add-task-event', newTask);
            
                this.topic = ''
                this.description = ''
            }
        }
    }
  }
</script>
<style >
  input {
      width: 200px;
      margin-left: 6px;
      background-color: #261b42;
      border: none;
      border-radius: 3px;
      padding: 8px;
      color: white;
  }
  .add-task {
      background-color: #3a6b35;
      color: white;
      border: none;
      padding: 7px;
      margin-left: 6px;
  }
</style>
