<template>
  <h4>{{person}}</h4>
  <h2>姓名：{{ name }}</h2>
  <h2>年龄：{{ age }}</h2>
  <h2>薪资：{{ job.j1.salary }}K</h2>
  <button @click="name += '~'">修改姓名</button>
  <button @click="age++">增长年龄</button>
  <button @click="job.j1.salary++">张薪资</button>
</template>
  
  <script>
    import {reactive,toRef,toRefs} from 'vue'
    export default {
      name: 'Demo',   
      setup() {
        //数据
        let person = reactive({
          name:'张三',
          age:18,
          job:{
            j1:{
              salary:20
            }
          }
        }) 
        
        const x = toRefs(person)
        console.log('@@@',x)
        // 返回一个对象（常用）
        return {
          person,
          // toRef(要操作的对象,要操作的对象的属性)
          //应用：要将响应式对象中的某个属性单独提供给外部使用时。
          // name:toRef(person,'name'),
          // age:toRef(person,'age'),
          // salary:toRef(person.job.j1,'salary'),

          //toRefs与toRef功能一致，但可以批量创建多个ref对象。
          ...toRefs(person)
        }
      },
    }
  </script>
  