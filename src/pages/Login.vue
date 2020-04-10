<template>
    <q-page padding class="full-width row  justify-center items-center">
        <q-card  class="login">
           <h6> Login</h6>
            <q-form action="https://some-url.com" method="post" @submit="onSubmit">
                <q-input   v-model="email" filled type="email" hint="Email" />
                <q-input color="white"   v-model="password" filled :type="isPwd ? 'password' : 'text'" hint="Password">
                    
                    <template v-slot:append>
                        <q-icon
                            :name="isPwd ? 'visibility_off' : 'visibility'"
                            class="cursor-pointer"
                            @click="isPwd = !isPwd"
                        />
                    </template>
                </q-input >
                <q-btn class="button" label="Submit" type="submit" color="primary"/>

               
            </q-form>
           
        </q-card>
    </q-page>
</template>

<script>

export default {
    data () {
        return {
            form: {
                password: '',
                isPwd: true,

                email: ''
            }
        }
    },
    methods: {
        onSubmit () {
            if (this.accept !== true) {
                this.$q.notify({
                color: 'red-5',
                textColor: 'white',
                icon: 'warning',
                message: 'You need to accept the license and terms first'
                })
            }
            else {
                this.$q.notify({
                color: 'green-4',
                textColor: 'white',
                icon: 'cloud_done',
                message: 'Submitted'
                })
            }
        }

    }
}
</script>

<style  lang="scss">
.login{
    text-align: center;
    position: relative;
    padding:10px;
    width:350px;
    color:white;
    font-size: 10pt;
    .q-field__messages{
        color:white !important;
    }
    input{
        color:white;
         font-size: 10pt;
    }
    label{
        color:white;
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
}
</style>