<template>
  <div class="lesson">
    <div 
      class="cover"
      :style="coverStyle"
    >
    </div>
    <span class="title">{{lesson.title}}</span>
    <span class="price">{{lesson.price}}</span>
    <span class="teachers">{{teacher}}</span>
    <div 
      :class="btnClass" 
      @click="addToCart(lesson)"
    >
      {{btnlable}}
    </div>
  </div>
</template>

<script>
import {mapMutations, mapGetters} from 'vuex';
  export default {
    props:['lesson'],
    computed:{
      ...mapGetters(['isLessonInCart']),
      btnClass(){
        return {
          buy: true,
          bought: this.isLessonInCart(this.lesson),
        };
      },
      btnlable(){
        return (
          this.isLessonInCart(this.lesson) ? '已加入購物車' : '加入購物車'
        )
      },
      teacher(){
        return this.lesson.teachers
        .map(t => t.username)
        .join(', ');
      },
      coverStyle(){
        return {
          backgroundImage: `url('${this.lesson.cover}')`,
        };
      },
    },
    methods:{
      ...mapMutations(['addToCart']),
    },
  }
</script>

<style scoped>
  .lesson{
    display: inline-block;
    width: 200px;
    border-radius: 6px;
    overflow: hidden;
    margin: 10px;
    box-shadow: 2px 2px 15px #999;
    margin: 10px;
    vertical-align: top;
  }
  .cover{
    width: 100%;
    height: 120px;
    background: center center;
    background-size: cover;
  }
  span{
    display: block;
    padding: 6px;
  }
  .title{
  font-size: .9em;
  height: 30px;
  color: #333;
  text-align: left;
}
.price{
  display: block;
  font-size: .85em;
  color: #178fac;
}
.price:before{
  content: '$';
}
.teachers{
  font-size: .7em;
  line-height: 1.7em;
  color: #178fac;
}
.buy{
  clear: both;
  text-align: center;
  padding: 6px;
  font-size: .7em;
  background-color: #dee;
  cursor: pointer;
}
.buy:hover{
  background-color: #cee;
}
.buy.bought{
  background-color: #ccc;
}
</style>