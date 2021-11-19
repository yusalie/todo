<template>
  <div class="container">
    <h2 class="text-center mt-5">Todo List</h2>
    <div class="d-flex">
      <input v-model="task" type="text" placeholder="Enter a task" class="form-control">
      <button @click="addTask" class="btn btn-primary rounded-0">Submit</button>
    </div>
    <table class="table table-bordered mt-5">
  <thead>
    <tr>
      <th scope="col">Task</th>
      <th scope="col" style="width: 120px">Status</th>
      <th scope="col" class="text-center">#</th>
      <th scope="col" class="text-center">#</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(task, index) in tasks" :key="index">
      <td><span :class="{'completed':task.status === 'finished'}">{{task.name}}</span></td>
      <td><span class="pointer" @click="changeStatus(index)">{{task.status}}</span></td>
      <td>
        <div class="text-center" @click="editTask(index)">
          <span class="fa fa-pen"></span>
        </div>
        </td>
      <td>
        <div class="text-center" @click="deleteTask(index)">
          <span class="fa fa-trash"></span>
        </div>
        </td>
    </tr>
  </tbody>
</table>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data(){
    return{
      task:'',
      editedTask:null,
      statuses: ["to-do", "in-progress", "finished"],
      tasks:[
        {
        name:'complete thavas deck',
        status:'in progress'
      },
      {
        name:'complete gavrail deck',
        status:'to-do'
      }
      ]
    }
  },
  methods:{
    addTask(){
      if(this.task.length ===0 ) return;
      if(this.editedTask == null){
          this.tasks.push({
        name:this.task,
        status:'to-do'
      });
      }else{
        this.tasks[this.editedTask].name = this.task;
      }
      
      this.task = ''
    },
    deleteTask(index){
      this.tasks.splice(index,1);
    },
    editTask(index){
      this.task = this.tasks[index].name;
      this.editedTask;
    },
    changeStatus(index){
      let newIndex = this.statuses.indexOf(this.tasks[index].status);
      if (++newIndex > 2) newIndex = 0;
      this.tasks[index].status = this.statuses[newIndex];
    }
  }
};
</script>

<style scoped>
.pointer{
  cursor:pointer;
}
.completed{
  text-decoration: line-through;
}
</style>
