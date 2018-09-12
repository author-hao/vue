# vue
个人笔记


vue  组件 中使用的时间过滤器


filters: { // 组建中的时间过滤器
    timer: val => {
      const timeFormatArr = [0, 60, 3600, 86400, 2592000, 946080000, Number.MAX_VALUE]
      const timeUnit = ['刚刚', '分钟前', '小时前', '天前', '月前', '年前']
      let dateTime = new Date(val).getTime()
      let now = new Date().getTime()
      let time = (now - dateTime) / 1000
      let index = timeFormatArr.findIndex((item, index) => {
        return item <= time && timeFormatArr[index + 1] > time
      })
      if (index === 0) {
        return timeUnit[0]
      }
      time = time / timeFormatArr[index] | 0
      // console.log(time + timeUnit[index])
      return time + timeUnit[index]
    }
  }
  
  
   全局的时间过滤器
   
   创建一个js文件
   
   import Vue from 'vue'

//   全局时间过滤器

export default Vue.filter('FilterTime', value => {
  const timeFormatArr = [0, 60, 3600, 86400, 2592000, 946080000, Number.MAX_VALUE]
  const timeUnit = ['刚刚', '分钟前', '小时前', '天前', '月前', '年前']
  let dateTime = new Date(value).getTime()
  let now = new Date().getTime()
  let time = (now - dateTime) / 1000
  let index = timeFormatArr.findIndex((item, index) => {
    return item <= time && timeFormatArr[index + 1] > time
  })
  if (index === 0) {
    return timeUnit[0]
  }
  time = time / timeFormatArr[index] | 0
  // console.log(time + timeUnit[index])
  return time + timeUnit[index]
})


在main.js中

import * as custom from './filters/filter-Date'

Object.keys(custom).forEach(key => {
  Vue.filter(key, custom[key])
})

  就可以了   使用{{    这里是时间 | FilterTime }  }  // | 管道 过滤
  
	得到 这个样    5小时前。。。根据现在时间减去创建时间得到的
