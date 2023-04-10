<template>
  <input type="text" v-model="keyWord">
  <h3>{{ keyWord }}</h3>
</template>

<script>
  import {ref,customRef} from 'vue'
  export default {
    name: 'App',
    setup(){
      //自定义ref：myRef
      function myRef(value,delay){
        let timer
        // console.log('---myRef---',value)
        return customRef((track,trigger)=>{
          return{
            get:function(){
              console.log(`有人从myRef容器中读取数据了！我把${value}给他了！`)
              track()//通知Vue追踪一下value的改变（提前跟get商量一下让它认为value是有用的）
              return value
            },
            set:function(newValue){
              console.log(`有人把myRef容器中数据修改为：${newValue}！`)
              clearTimeout(timer)
              timer = setTimeout(() => {
                value = newValue
                trigger() //通知Vue重新去解析模板
              }, delay);
            },
          }
        })

      }
      // let keyWord = ref('hello')//使用Vue提供的ref
      let keyWord = myRef('hello',500)//使用程序员自定义ref
      return{
        keyWord
      }
    }
  }
</script>
