<template>
    <div>
        <form @submit="addTask">
            <input type="text" name="topic" v-model="topic" placeholder="Add Task topic">
            <input type="text" name="description" v-model="description" placeholder="Add description">
            <!-- <input type="text" name="assignee" v-model="assignee" placeholder="Assignee username"> -->
            <select v-model="assignee" > 
                <option value="" disabled selected>Assignee username</option>
                <option style="color: white;" v-for="(data) in users" :value="data.id" :key="data.id" >
                    {{data.username}}
                    {{data.username}}

                </option>
            </select>
            <select v-model="reporter" > 
                <option value="" disabled selected>Reporter username</option>
                <option style="color: white;" v-for="(data) in users" :value="data.id" :key="data.id" >
                    {{data.username}}
                </option>
            </select>
            <!-- <input type="text" name="reporter" v-model="reporter" placeholder="Reporter username"> -->
            <button class="add-task" type="submit">Add Task</button>
        </form>

        <div class="form-group">
            
            <!-- <option v-for="data in users" value="user.id"{{ user.username }}></option> -->
            
        </div>
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
                reporter: '',
                users: JSON.parse(localStorage.getItem('users'))
            }
        },
        methods: { 
            addTask(e){
                if(this.topic !== "") {
                    e.preventDefault();
                
                let idNum = 0;  

                this.tasks = JSON.parse(localStorage.getItem("tasks"))

                console.log(this.assignee, this.tasks)

                // Get last id from array and set id +1
                if (this.tasks.length !== 0) {
                    idNum = this.tasks[Object.keys(this.tasks)[Object.keys(this.tasks).length - 1]].id + 1
                }
            
                const newTask = {
                id: idNum,
                topic: this.topic,
                description: this.description,
                assigneeID: this.assignee,
                reporterID: this.reporter
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
  select {
      width: 200px;
      margin-left: 6px;
      background-color: #261b42;
      border: none;
      border-radius: 3px;
      padding: 8px;
      color: #68756D;
  }

  .add-task {
      background-color: #3a6b35;
      color: white;
      border: none;
      padding: 7px;
      margin-left: 6px;
  }
</style>
