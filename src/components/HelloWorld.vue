<template>
  <div class="hello">
 <div class="e1">
   <echart1/>
 <echart2/>
  <echart3/>
 </div>
<div class="e1">
    <echart4/>
 <echart5/>
  <echart6/>
</div>
<div class="e1">
    <echart7/>
 <echart8/>
  <echart9/>
</div>
  </div>
</template>

<script>
import echart1 from '@/components/echart1'
import echart2 from '@/components/echart2'
import echart3 from '@/components/echart3'
import echart4 from '@/components/echart4'
import echart5 from '@/components/echart5'
import echart6 from '@/components/echart6'
import echart7 from '@/components/echart7'
import echart8 from '@/components/echart8'
import echart9 from '@/components/echart9'
export default {
  name: 'HelloWorld',
  components:{
    echart1,
    echart2,
    echart3,
    echart4,
      echart5,
    echart6,
    echart7,
    echart8,
    echart9,
  },
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
 
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.hello{
  display: flex;
  flex-direction: column;
  flex-wrap: nowrap;
  justify-content: flex-start;
  align-items: center;
}
.e1{
   display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content: space-around;
  align-items: center;
}

</style>
