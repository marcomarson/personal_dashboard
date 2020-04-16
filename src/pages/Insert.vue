<template>
    <q-dialog v-model="card" persistent >
      <q-card class="card">
          <q-card-section class="q-pt-none">
          <div class="text-subtitle1">
            Which manga do you want to add?
          </div>
        </q-card-section>

        <div class="logo-container">
            <img v-bind:src="this.form.image"  :key="this.form.image" class="logo" v-bind:alt="this.form.name" />
        </div>
        <q-card-section>

          <div class="row no-wrap items-center">
            <div class="col text-h6 ellipsis">
             {{this.form.name}}
            </div>
            <div class="col-auto text-grey text-caption q-pt-md row no-wrap items-center">
              
            </div>
          </div>

          <q-rating v-model="stars" :max="5" size="32px" />
        </q-card-section>

        <q-separator />
        <q-input outlined v-model="form.name" label="Name of the Manga" :dense="dense" />
        <q-input outlined v-model="form.image" label="Link of the Image" :dense="dense" />
        <q-input outlined v-model="form.last_episode" label="Last Episode (Number)" :dense="dense" />
        <q-input outlined v-model="form.link" label="Link of Manga" :dense="dense" />
        <q-card-actions align="center">
          <q-btn v-close-popup flat color="primary" label="Save" />
          <q-btn v-close-popup flat color="primary" @click="onSubmit" label="Cancel"  />
        </q-card-actions>
      </q-card>
    </q-dialog>
    <!-- <q-page padding class="full-width row  justify-center items-center">
        <div class="row">
            <div>
                <h6> Which manga do you want to add? </h6>
                     
                 <q-card-section class='col-sm-12'>
                    <img v-bind:src="this.form.image" :key="this.form.image"  class="solo">
                </q-card-section>
                <div class='col-sm-12'>
                 
                </div>   
            </div>
        </div>
    </q-page> -->
</template>

<script>
import solo from "assets/solo_leveling.jpg"

export default {
    data () {
        return {
            dense:true,
               card: true,
            stars:1,
            form: {
                name: '',
                image: '',
                last_episode: '',
                link: ''
            }
        }
    },
    methods: {
        onSubmit (evt) {
            console.log(this.name)
        }

    }
}
</script>

<style lang="scss">
.card{
    width: auto;
    height: auto;
    padding:0px 10px;
    .text-subtitle1{
        font-size: 18pt;
        text-align: center;
        // padding-bottom: 10px;
        padding:15px 0;
        color:#fff;
    }
    .q-placeholder{
        color:white;
    }
    .q-field__messages{
            color:white !important;
        }
    .q-field__label{
            color:white !important;
            
        }
        input{
            color:white;
            font-size: 10pt;
        }
        label{
            color:white !important;
            font-size: 13pt;
        }
        h6{
            color:white;
            margin-bottom: 10px;
            margin-top:10px;
            font-size: 13pt;
        }
        .button{
            margin-top:10px;
        }
    .logo-container{
        width: 250px;
        text-align: center;
        display: block;
        position: relative;
        margin:auto;

        .logo{
        
        
            // width: 50%;
            width: 100%;
            height: auto;
            position: relative;
        }

    }

}

</style>