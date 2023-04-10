<template>
  <h2>当前求和为：{{ sum }}</h2>
  <button @click="sum++">点我+1</button>
  <hr>
  <h2>当前的信息为：{{ msg }}</h2>
  <button @click="msg+='！'">修改信息</button>
  <hr>
  <h2>姓名：{{ person.name }}</h2>
  <h2>年龄：{{ person.age }}</h2>
  <h2>薪资：{{ person.job.j1.salary }}K</h2>
  <button @click="person.name += '~'">修改姓名</button>
  <button @click="person.age++">增长年龄</button>
  <button @click="person.job.j1.salary++">张薪资</button>
</template>
  
  <script>
    import {ref,watch,reactive} from 'vue'
    export default {
      name: 'Demo',

      //Vue2里监视属性watch的写法
      //#region 
      //watch:{
        
        //简写形式
        /* sum(newValue,oldValue){
          console.log(`sum的值变化了！变化后是：${newValue}，变化前是：${oldValue}`)
        } */
        
        //完整写法（可以配置一些属性）
        /* sum:{
          immediate:true, //立即监听一下
          deep:true,//开启‘深度监视’，默认为浅度监视
          handler(newValue,oldValue){
            console.log(`sum的值变化了！变化后是：${newValue}，变化前是：${oldValue}`)
          }
        } */
      //},
      //#endregion
      
      setup() {
        //数据
        let sum = ref(0)
        let msg = ref('你好！')

        let person = reactive({
          name:'张三',
          age:18,
          job:{
            j1:{
              salary:20
            }
          }
        })

        //Vue3里的监视函数watch(要监视的参数,监视的回调函数,监视的配置项)
        //#region
        //情况一：监视ref所定义的一个响应式数据
        /* watch(sum,(newValue,oldValue)=>{
          console.log(`sum的值变化了！变化后是：${newValue}，变化前是：${oldValue}`)
        },{immediate:true}) */

        //情况二：监视ref所定义的多个响应式数据
        /* watch([sum,msg],(newValue,oldValue)=>{
          console.log(`sum/msg的值变化了！变化后是：${newValue}，变化前是：${oldValue}`)
        },{immediate:true})  */

        /**
         * 情况三：监视reactive所定义的一个响应式数据的全部属性
         * 注意：
         * 1、此处无法正确的获取oldValue
         * 2、强制开启了深度监视（deep配置无效）
         */
        /* watch(person,(newValue,oldValue)=>{
          console.log('person变化了！',newValue,oldValue)
        },{deep:false})//此处的deep配置无效 */

        //情况四：监视reactive所定义的一个响应式数据中的某个属性
        /* watch(()=>person.name,(newValue,oldValue)=>{
          console.log('person的name变化了！',newValue,oldValue)
        }) */

        //情况五：监视reactive所定义的一个响应式数据中的某些属性
        /* watch([()=>person.name,()=>person.age],(newValue,oldValue)=>{
          console.log('person的name/age变化了',newValue,oldValue)
        }) */

        //特殊情况
        /* watch(()=>person.job,(newValue,oldValue)=>{
          console.log('person的job变化了！',newValue,oldValue)
        },{deep:true}) //此处由于监视的是reactive所定义的对象中的某个属性，所以deep配置有效 */
        //#endregion
        
        // 返回一个对象（常用）
        return {
          sum,
          msg,
          person
        }
      },
    }
  </script>
  