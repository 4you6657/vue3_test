<template>
  <!-- Vue3组件中的模板结构可以没有根标签<div></div> -->
  <h1>一个人的信息</h1>
  <h2>姓名：{{ person.name }}</h2>
  <h2>年龄：{{ person.age }}</h2>
  <h3>工作种类：{{ person.job.type }}</h3>
  <h3>工作薪资：{{ person.job.salary }}</h3>
  <h3>爱好：{{ person.hobby }}</h3>
  <h3>测试数据c：{{ person.job.a.b.c }}</h3>
  <button @click="changeInfo">修改信息</button>
  <button @click="addSex">添加一个sex属性</button>
  <button @click="deleteName">删除一个name属性</button>
</template>

<script>
  import {ref,reactive} from 'vue'
  export default {
    name: 'App',
    setup() {
      //数据
      /* let name = ref('张三')
      let age = ref(18)
      let job = reactive({
        type:'前端工程师',
        salary:'30K',
        a:{
          b:{
            c:666
          }
        }
      })
      let hobby = reactive(['抽烟','喝酒','烫头']) */

      let person = reactive({
        name:'张三',
        age:18,
        job:{
          type:'前端工程师',
          salary:'30K',
          a:{
            b:{
              c:666
            }
          }
        },
        hobby:['抽烟','喝酒','烫头']
      })

      //方法
      function changeInfo(){
        //ref函数定义
        person.name = '李四'
        person.age = 48 
        //reactive函数定义
        person.job.type = 'UI设计师'
        person.job.salary = '50K'
        person.job.a.b.c = 999
        person.hobby[0] = '学习'
      }
      
      // 返回一个对象（常用）
      return {
        /* name,
        age,
        job,
        hobby, */
        person,
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
