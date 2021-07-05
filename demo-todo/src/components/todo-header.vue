<template>
  <div class="todo-header">
    <input type="text" placeholder="请输入你的任务名称，按回车键确认"
    v-model="name" @keydown.13="addTask"/>
  </div>
</template>

<script>
export default {
  name:'todo-header',
  data(){
    let id = localStorage.getItem('todo-list-id')
    return{
      name:'',
      id
    }
  },
  methods:{
    addTask() {
      let name = this.name;
      let task={
        id:this.id++,
        name,
        checked:false,
      }
      this.$emit('addTask',task)
      this.name = ''
      //id存储
      localStorage.setItem('todo-list-id',JSON.stringify(this.id))
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.todo-header input {
  width: 560px;
  height: 28px;
  font-size: 14px;
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 4px 7px;
}

.todo-header input:focus {
  outline: none;
  border-color: rgba(82, 168, 236, 0.8);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 8px rgba(82, 168, 236, 0.6);
}
</style>
