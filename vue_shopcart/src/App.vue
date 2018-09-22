<template>
  <div>
    <Header/>
    <LessonList/>
  </div>
</template>


<script>
  import LessonList from './LessonList.vue';
  import Header from './Header.vue';
  export default {
    components:{
      Header,
      LessonList,
    },
  }
</script>

