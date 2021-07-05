<script src="main.js"></script>
<template>
  <div id="app">
    <div class="todo-container">
      <div class="todo-wrap">
        <todo-header @addTask="addTask"></todo-header>
        <todo-list :list="list"></todo-list>
        <todo-footer :list="list"></todo-footer>
      </div>
    </div>
  </div>
</template>

<script>
import header from "components/todo-header"
import list from "components/todo-list"
import footer from "components/todo-footer"

export default {
  name: 'App',
  data(){
    return{
      list:[
        {id:0,name:'长白山滑雪',checked:true},
        {id:1,name:'爬玉龙雪山',checked:false},
        {id:2,name:'普吉岛冲浪',checked:false},
        {id:3,name:'三亚岛潜水',checked:false},
        {id:4,name:'港澳逛吃喝',checked:false},
        {id:5,name:'台湾环岛行',checked:false}
      ]
    }
  },
  components: {
    "todo-header":header,
    "todo-list":list,
    "todo-footer":footer
  },
  methods:{
    addTask(task){
      this.list.unshift(task)
    },
    checked(id,checked){
      this.list.forEach((item)=>{
          if(item.id === id){
            item.checked = checked
          }
      })
    },
    delTask(id){
      this.list = this.list.filter(item=>item.id !== id)
    },
    //全选功能
    checkAll(checked){
      this.list.forEach(item=>item.checked=checked)
    },
    //clear all the done task
    clear(id){
      this.list = this.list.filter(item => !item.checked)
    }

  },
  mounted() {
    //item上的列表选中功能
    this.$bus.$on("checked",this.checked)
    //item上的task删除功能
    this.$bus.$on("delTask",this.delTask)
    //footer的全选功能
    this.$bus.$on("checkAll",this.checkAll)
    //footer的清楚功能
    this.$bus.$on("clear",this.clear)
  },
  created() {
    //将存储中的数据读出来，赋值给list
    const list = JSON.parse(localStorage.getItem("todo-list-data"))
    this.list = list ? JSON.parse(list):[]

  },
  watch:{
    list:{
      handler(newList){
        //存到localStorage中（json字符串）
        localStorage.setItem("todo-list-data",JSON.stringify(newList))
      }
    },
    deep:true
  }
}
</script>

<style scoped>
  .todo-container {
    width: 600px;
    margin: 0 auto;
  }
  .todo-container .todo-wrap {
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
  }
</style>
