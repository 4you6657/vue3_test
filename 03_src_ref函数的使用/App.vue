<template>
  <!-- Vue3组件中的模板结构可以没有根标签<div></div> -->
  <h1>一个人的信息</h1>
  <h2>姓名：{{ name }}</h2>
  <h2>年龄：{{ age }}</h2>
  <h3>工作种类：{{ job.type }}</h3>
  <h3>工作薪资：{{ job.salary }}</h3>
  <button @click="changeInfo">修改信息</button>
</template>

<script>
  import {ref} from 'vue'
  export default {
    name: 'App',
    setup() {
      //数据
      let name = ref('张三')
      let age = ref(18)
      let job = ref({
        type:'前端工程师',
        salary:'30K'
      })

      //方法
      function changeInfo(){
        // name.value = '李四'
        // age.value = 48 
        job.value.type = 'UI设计师'
        job.value.salary = '50K'
        // console.log(name,age)
      }
      
      // 返回一个对象（常用）
      return {
        name,
        age,
        job,
        changeInfo
      }
    },
  }
</script>

<style>
/* #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
} */
</style>
