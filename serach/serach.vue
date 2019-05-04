<template>
   <div class="serach-wrapper">
      <div class="serach-bar">
         <span class="text">
            <img src="./serach.svg" class="serach-icon" width="20px" height="20px">
            <img src="./close.svg" class="close-icon" width="20px" height="20px" :class="{'hidden':!currentVal || !focusflag}" @click="cleanVal">
            <input type="text" class="input" @input="input" v-model="currentVal" @focus="focusvlue" @blur="blurvlue" ref="input" @keyup.enter="enterSure">
         </span>
         <span class="cancel" v-show="currentVal || focusflag" @click="cleanVal">
            取消
         </span>
      </div>
      <div class="result-list" v-if="filterValue && currentVal">
         <div class="list" v-for="item in filterValue" @click="changValue(item)" v-show="isShow">
            <img src="./order.svg" class="order-icon" width="20px" height="30px">
            <img src="./setion.svg" class="setion-icon" width="20px" height="30px">
            <section class="item">{{item}}</section> 
         </div>
      </div>
   </div>
</template>

<script>
   export default{
      props:{
         value:{
            type:String,
            default:''
         },
         result:{
            type:Array,
            default:[]
         }
      },
      data(){
         return{
            currentVal : this.value,
            focusflag:false,
            isShow:true
         }
      },
      computed:{
         filterValue(){
            return this.result.filter(item => new RegExp(this.currentVal,'i').test(item))
         }
      },
      methods:{
         input(){
            this.isShow = true
            this.$emit('update:value', this.currentVal)
         },
         focusvlue(){
            this.focusflag = true
         },
         blurvlue(){
            this.focusflag = false
         },
         cleanVal(){
            this.currentVal = ''
            this.$emit('update:value', this.currentVal)
            this.$refs.input.focus()
         },
         changValue(value){
            this.currentVal = value
            this.$emit('update:value', this.currentVal)
            this.isShow = false
         },
         enterSure(){
            this.isShow = false
         }
      }
   }
</script>
<style scoped lang='stylus' rel='stylesheet/stylus'>
.serach-wrapper
   position:relative
   .serach-bar
      display:flex
      .text,.cancel
         display:inline-block
      .text
         position:relative
         flex:1
         line-height:30px
         padding:0 30px
         border:1px solid #ccc
         border-radius:2px
         .serach-icon,.close-icon
            display:inline-block
         .serach-icon
            position:absolute
            top:0
            left:5px
            bottom:0
            right:0
            margin:auto 0
         .close-icon
            position:absolute
            top:0
            bottom:0
            right:5px
            margin:auto 0
            disable:disable
            &.hidden
               opacity:0
         .input
            border:none
            border-radius:2px
            height:30px
            width:100%
            padding-right:30px
            outline:none
      .cancel
         flex:0 0 50px
         color:#3190e8
         line-height:30px
         text-align:center
   .result-list
      position:absolute
      z-index:999
      background:white
      width:100%
      .list
         border-left:1px solid #ccc
         border-right:1px solid #ccc
         border-bottom:1px solid #ccc
         line-height:30px
         padding:10px 20px 10px 5px
         cursor:pointer
         .order-icon
            float:left
            margin-right:5px
         .setion-icon
            float:right
            color:#3190e8
         .item
            color:#666
</style>