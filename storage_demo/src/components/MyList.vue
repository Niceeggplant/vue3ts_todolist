<template>
 <ul>
   <my-item v-for="(todo,index) in todos" :key="todo.id" :index='index' :todo="todo"></my-item>
 </ul>
</template>

<script lang="ts">
import  {defineComponent} from "vue";
import MyItem from "@/components/MyItem.vue";

export default defineComponent({
  name: "MyList",
  components: {MyItem},
  props:['todos']

})
</script>

<style scoped>

</style>