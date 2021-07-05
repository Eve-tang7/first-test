<template>
  <div class="todo-footer">
    <label>
      <input type="checkbox" v-model="checkAll" :disabled="disabled"/>
    </label>
    <span>
      <span>
        <strong>已完成</strong>
        <strong>{{doneNum}}</strong>
      </span>
      <span>/</span>
      <span>
        <strong>全部</strong>
        <strong>{{list.length}}</strong>
      </span>
    </span>
    <button class="btn btn-danger" @click="clear">清除已完成任务</button>
  </div>
</template>

<script>
export default {
  name: "todo-footer",
  props:{
    list:Array
  },
  methods:{
    clear(){
      this.$bus.$emit("clear")
    }
  },
  computed:{
    //已完成任务的数量
    doneNum(){
      /*let num = 0;
      this.list.forEach((item)=>{
        if(item.checked){
          num++
        }
      })
      return num;*/
      return this.list.reduce((adder,item)=>{
        return item.checked ? adder+1 : adder
      },0)
    },
    checkAll:{
      get(){
        //全选按钮选中逻辑：待办任务的数量 === 已完成的数量，且都不为0
        return ((this.list.length === this.doneNum)&&(this.list.length!==0 && this.doneNum!==0))
      },
      set(checked){
        //当前全选按钮的最新状态
        this.$bus.$emit("checkAll",checked)
      }
    },
    disabled(){
      return this.list.length ===0 && this.doneNum===0
    }
  }
}
</script>

<style scoped>
.todo-footer {
  height: 40px;
  line-height: 40px;
  padding-left: 6px;
  margin-top: 5px;
}

.todo-footer label {
  display: inline-block;
  margin-right: 20px;
  cursor: pointer;
}

.todo-footer label input {
  position: relative;
  top: -1px;
  vertical-align: middle;
  margin-right: 5px;
}

.todo-footer button {
  float: right;
  margin-top: 5px;
}
</style>
