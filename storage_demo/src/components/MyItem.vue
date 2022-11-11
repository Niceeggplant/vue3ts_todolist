<template>
<li class="todo-item">
  <el-checkbox v-model="isChecked" >
    {{todo.title}}
  </el-checkbox>
  <el-button
      size="mini"
      type="danger"
      @click="handleDelete(todo.id)"
      :icon="Delete"
      circle>
  </el-button>
</li>
</template>

<script lang="ts" >
import {Todos} from "@/type";
import {defineComponent, ref, inject, computed} from "vue";
import  {Delete} from "@element-plus/icons-vue"
export default  defineComponent({
  name: "MyItem",
  props:{
    todo:{
      type:Object as ()=> Todos,
      required:true
    },
    index:{
      type:Number
    }
  },
  setup(props,context){
    const checked1 = ref(false)
    const updateTodo=inject('updateTodo')
    const  delTodo = inject('delTodo')
    const handleDelete = (index:number)=>{
      if(window.confirm("确认删除吗？")) {
        if(typeof delTodo==='function')
          delTodo(index)
      }
    }
    const isChecked = computed({
      get(){
        return props.todo.isDone
      },
      set(val){
        if(typeof  updateTodo==='function')
          updateTodo(props.todo,val)
      }
    })

    return{
      isChecked,
      Delete,
      handleDelete
    }
  }

})
</script>

<style scoped>
.todo-item {
  border: 1px solid lightblue;
  list-style: none;
  width: 100%;
  padding: 5px;
  margin-left: -40px;
  border-radius: 5px;
  display: flex;
  justify-content: space-between;
}
</style>