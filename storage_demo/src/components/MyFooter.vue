<template>
  <div class="todo-footer">
    <el-checkbox v-model="isCheckAll">
      <span>
        已完成 {{count}} /全部 {{todos.length}}
      </span>
    </el-checkbox>
    <el-button size="mini" type="danger" plain @click="clearDone">清除已完成任务</el-button>
  </div>
</template>

<script lang="ts">
import {Todos} from "@/type";
import {defineComponent,computed,ComputedRef} from "vue";
export default defineComponent({
  name:"MyFooter",
  props:{
    todos:{
      type:Array as() =>Todos[],
      required:true
    },
    clearDone:{
      type:Function,
      required:true
    },
    checkAll: {
      type: Function,
      required: true
    }
  },
  setup(props){
    const  count = computed(()=>{
      return props.todos.reduce((pre:number,todo:Todos)=>
        pre + (todo.isDone?1:0),0)
    })

    const isCheckAll= computed({
      get(){
        return count.value>0 &&count.value === props.todos.length
      },
      set(val)
      {
        props.checkAll(val)
      }
    })
    return{
      count,isCheckAll
    }
  }

})
</script>

<style>
.todo-footer {
  display: flex;
  justify-content: space-between;
}
</style>