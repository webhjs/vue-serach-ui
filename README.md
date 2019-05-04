# vue-serach-ui
this is vue-server-ui components
# 父组件调用 
## js：```import Serach from '@/components/serach/serach```
## html： ```<Serach :value.sync="value" :result="result"></Serach>```
***.sync 在2.3中作为语法糖写法***
>作用是在子组件vue-server-ui中用this.$emit('update:value', newVal)触发父组件value的更新
---
### 依赖两个值 value 是用于跟踪input框中的值 result用于显示自定义的历史记录
