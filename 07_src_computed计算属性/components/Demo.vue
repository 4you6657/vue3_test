<template>
    <!-- Vue3组件中的模板结构可以没有根标签<div></div> -->
    <h1>一个人的信息</h1>
    姓：<input type="text" v-model="person.lastName">
    <br>
    名：<input type="text" v-model="person.firstName">
    <br>
    <span>全名：{{ person.fullName }}</span>
    <br>
    全名：<input type="text" v-model="person.fullName">
  </template>
  
  <script>
    import {reactive,computed} from 'vue'
    export default {
      name: 'Demo',
      /* computed:{
        fullName(){
          console.log(this)
          return this.person.lastName + '-' + this.person.firstName
        }
      }, */
      setup() {
        //数据
        let person = reactive({
          firstName:'三',
          lastName:'张'
        })
        
        //计算属性
        /* let fullName = computed(() => {
          return person.lastName + '-' + person.firstName
        }) */

        //计算属性的简写形式（没有考虑计算属性被修改的情况）
        /* person.fullName = computed(() => {
          return person.lastName + '-' + person.firstName
        }) */
        
        //计算属性的完整形式（考虑读和写）
        person.fullName = computed({
          get(){
            return person.lastName + '-' + person.firstName
          },
          set(value){
            const nameArr = value.split('-')
            person.lastName = nameArr[0]
            person.firstName = nameArr[1]
          }
        })

        // 返回一个对象（常用）
        return {
          person,
          // fullName   
        }
      },
    }
  </script>
  