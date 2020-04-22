<template>
  <q-page class="main">
    <div class='row'>
      <div class=' col-6 col-xs-12'>
        <div>
            <img
              alt="Profile image"
              src="~assets/profile.jpg"
            >
            <div class='name'>
              <h1><b>Marco Marson</b> </h1>
          </div>
         
        </div>
      </div>
      <div class='col-6 col-xs-12 second-part'>
        <div class='main-title'>
          <about> </about>
        </div>

      </div>
      
    </div>
  </q-page>
</template>

<script>
import About from 'components/About'
export default {
  name: 'PageIndex',
  components:{
    About
  }
}
</script>
<style lang='scss'>
.main{
  img{
    // height: auto;
    // width:100vw;
    height:100vw;
  }
  .name{
    font-size: 26pt;
    position: absolute;
    width:100vw;
    margin-top:-180px;
    text-align: center;
  }
  


}
</style>