<template>
  <li>
    <label>
      <input type="checkbox" v-model="checked"/>
      <span>{{ item.name }}</span>
    </label>
    <button class="btn btn-danger" @click="delTask(item.id)">删除</button>
  </li>
</template>

<script>
export default {
  name: "todo-item",
  props:{
    item:Object
  },
  methods:{
    delTask(id){
      this.$bus.$emit("delTask",id)
    }
  },
  computed:{
    checked:{
      get(){
        return this.item.checked
      },
      set(checked){
        this.$bus.$emit('checked',this.item.id,checked)
        //console.log(checked)
      }
    }
  }
}
</script>

<style scoped>
.todo-empty {
  height: 40px;
  line-height: 40px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding-left: 5px;
  margin-top: 10px;
}
/*item*/
li {
  list-style: none;
  height: 36px;
  line-height: 36px;
  padding: 0 5px;
  border-bottom: 1px solid #ddd;
}

li label {
  float: left;
  cursor: pointer;
}

li label li input {
  vertical-align: middle;
  margin-right: 6px;
  position: relative;
  top: -1px;
}

li button {
  float: right;
  display: none;
  margin-top: 3px;
}
li:hover button{
  display: block;
}

li:before {
  content: initial;
}

li:last-child {
  border-bottom: none;
}

</style>
