<template>
    <div class ='manga col-md-auto col-xs-12 justify-center'>
        <div class="imagem">
            <img
            alt="Quasar logo"
            v-bind:src="manga.image"
            >
            <div class ='low-info'>
                <div class ='title'>
                    {{manga.title}}
                </div>
                <div class ='sub-title'>
                    {{manga.stars}}
                </div>
                <div class ='sub-title'>
                    {{manga.last_episode}}
                </div>
            </div>
        </div>
        <!-- </q-card> -->
    </div>
</template>

<script>
export default {
    name: 'PageIndex',
    props: ['manga']
}
</script>
<style lang='scss'>
.manga{
    // width: auto;
    position: relative;
    padding-left:5px;
    height: auto;
    text-align: center;
    margin-bottom: 15px;
    min-height: 200px !important;
    // min-width: 100px !important;
    // border:1px solid #ffffff80;
    box-shadow: 0 15px 35px rgba(50,50,93,.1), 0 5px 15px rgba(0,0,0,.07);
    .imagem{
        width: -webkit-fit-content;
        width: -moz-fit-content;
        .low-info{
        position: relative;
        color:#fff;
        background-color: #00000060;
        height: 50px;
        top:-14%;
    }

    }
    

    
    
}

</style>
