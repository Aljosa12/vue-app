<template>
<div>    

    <div class="modal-wrapper" tabindex="-1" role="dialog">
          <div id="myModal2" class="modal">

        <div class="modal-content modal-edit">
          <span id="close-edit" class="close">&times;</span>
          <div style="margin-top: 30px;">
            <form @submit="editTask">
            <input class="edit-input" type="text" name="topic" v-model="topic" placeholder="Add Task topic">
            <input class="edit-input" type="text" name="description" v-model="description" placeholder="Add description">
            <select v-model="assignee" class="edit-input"> 
                <option value="" disabled selected>Assignee username</option>
                <option style="color: white;" v-for="(data) in users" :value="data.id" :key="data.id" >
                    {{data.username}}
                </option>
            </select>
            <select v-model="reporter" class="edit-input"> 
                <option value="" disabled selected>Reporter username</option>
                <option style="color: white;" v-for="(data) in users" :value="data.id" :key="data.id" >
                    {{data.username}}
                </option>
            </select>
            <button id="btn-edit-task" >Edit Task</button>
            </form>
          </div>
          
        </div>

        </div>
    </div>

</div>
    
</template>

<script>

    export default {
        name: "Tasks",
        props: {
          tasks: []
        },
        data() {
        return {
          topic: '',
          description: '',
          assignee: Number,
          reporter: Number,
          users: JSON.parse(localStorage.getItem('users'))
        }
      },
      methods: { 
            editTask(){

                const editedTask = {
                topic: this.topic,
                description: this.description,
                assigneeID: this.assignee,
                reporterID: this.reporter
                }

                this.$emit('edit-task', editedTask);
            }
        }
    }

</script>

<style >
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


