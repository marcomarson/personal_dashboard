<template>
  <q-page class="main">
    <div class='row'>
      <div class=' col-md-6 col-xs-12'>
        <div>
            <img
              alt="Quasar logo"
              src="~assets/profile.jpg"
            >
            <div class='name'>
              <h1><b>Marco Marson</b> </h1>
          </div>
         
        </div>
      </div>
      <div class='col-6 second-part'>
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
  overflow:hidden;
  width: auto;
  img{
    height: 100vh;
    // width:100vh;
  }
  .name{
    font-size: 26pt;
    position: absolute;
    width: auto;
    margin-top:-200px;
    // margin-top:70vh;
    // left:25%;
    // margin-right:15%;
    text-align: center;
    h1{
      font-size: 26pt;
    }
  }
  


}
</style>