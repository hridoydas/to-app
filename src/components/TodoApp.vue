<template>
  <div class="container">
   <h2 class="text-center mt-5">Todo App</h2>
   <div class="d-flex">
     <input v-model="task" type="text" placeholder="Enter task" class="form-control rounded-0" required>
     <button @click="submitTask" class="btn btn-warning rounded-0" >SUBMIT</button>
   </div>

   <table class="table table-bordered mt-4">
  <thead>
    <tr>
      <th scope="col">Task</th>
      <th scope="col">Status</th>
      <th class="text-center" scope="col">Edit</th>
      <th class="text-center" scope="col">Delete</th>
    </tr>
  </thead>
  <tbody>
    <tr  v-for="(task, index) in tasks" :key="index">
      <td>
        <span :class="{'finished': task.status==='to-do'}">
          {{task.name}}
        </span>
      </td>
      <td style="width:120px">
        <span  @click="changeStatus(index)" class="pointer"
        :class="{'text-danger': task.status==='to-do',
                      'text-warning': task.status==='in-progress',
                      'text-info': task.status==='finished'
                      }">
          {{task.status}}
        </span>
      </td>
      <td>
        <div class="text-center"  @click="editTask(index)">
          <span class="fa fa-pen pointer"></span>
        </div>
      </td>
      <td>
          <div class="text-center" @click="deleteTask(index)">
          <span class="fa fa-trash pointer">
            
          </span>
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
      editedTask: null,
      avaialableStatus: ['to-do','in-progress','finished'],

      tasks:[
        {
          name: "Steal banana from longest tree",
          status: 'to-do'
        },
        {
          name: "Sell the previous banana",
          status: 'in-progress'
        },
        {
          name: "Sell the previous bananas",
          status: 'finished'
        }
      ]
    }
  },
  methods:{
    submitTask(){
      // console.log(this.task);
      if(this.task.length===0){
        return;
      }
      // else if (this.task===" "){
      //   alert("cannot keep empty task")
      // }
      if(this.editedTask===null){
        this.tasks.push({
        name: this.task,
        status: "to-do"
      });
      }else{
        this.tasks[this.editedTask].name=this.task;
        this.editedTask=null;
      }

      this.task='';            
    },
    deleteTask(index){
      this.tasks.splice(index, 1)
    },

    editTask(index){
      this.task = this.tasks[index].name;
      this.editedTask = index;
    },
    changeStatus(index){
      let newIndex = this.avaialableStatus.indexOf[this.tasks[index].status];
      if(++newIndex > 2) newIndex = 0;
      this.tasks[index].status = this.avaialableStatus[newIndex];
    },

    // firstCharUpper(str){
    //   return str[0].toUpperCase() + str.substring(1);
    // }
  }
}
</script>

<style  scoped>
.pointer{
  cursor: pointer;
}
.finished{
  text-decoration: line-through;
}
</style>