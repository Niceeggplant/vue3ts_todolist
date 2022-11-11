<template>
  <div class="todo-header">
    <el-input v-model="todoTitle" @change="add"  placeholder="请输入你的任务名称并按回车键确认" clearable />
  </div>
</template>

<script lang="ts" >
import {Todos} from "@/type";
import { ref ,defineComponent } from 'vue';
export default defineComponent ({
  name: "MyHead",
  props:{
    addTodo:{
      type:Function,
      required:true
    }
  },
  setup(props,context){
    const todoTitle = ref('')
    const  add = () =>{
      const text = todoTitle.value
      if(!text.trim()){
        return
      }
      const todo:Todos = {
        id:Date.now(),
        title:text.trim(),
        isDone:false
      }
      props.addTodo(todo)
      todoTitle.value = ''
    }
    return{
      todoTitle,
      add
    }
  }

})

</script>

<style scoped>

</style>