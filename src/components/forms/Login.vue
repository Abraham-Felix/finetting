<style scoped>
.oneH {
width:100%;
display:grid;
}
.login {
  width: 200px !important;
  margin: auto;
}
.v-card {
    height: auto;
    max-width: 600px !important;
    -webkit-box-pack: center;
    width: 100% !important;
}

button {
    box-shadow: 0px 0px 3px -2px #b6bbc0;
    background: #b6bbc0;
    color: white;
    padding: .5vh;
    border-radius: 10px;
    margin: 2vh;
}

</style>

<template>
<v-form  class="contactForm">
        <div class="login pt-3">
            <h5 class="primary--text ">Log In</h5>
            <br>
            <div class="form-group">
                <v-text-field class="form-control" type="text" v-model="email" placeholder="Email">
                </v-text-field>
            </div>
            <v-text-field class="form-control" type="password" @keyup.enter="login" v-model="password" placeholder="Password">
            </v-text-field>
            <v-btn depressed small color="primary"  @click="login">Log in</v-btn>
            <div class="oneH">
            <div class="grid-50">
              <v-divider class="mb-5"/>
            <h5 class="primary--text">Other methods</h5>
            <v-btn @click.native="signInWithGoogle"><v-icon>mdi-google</v-icon></v-btn>
          </div>
          </div>
        </div>
</v-form>

</template>

<script>

import firebase from 'firebase';
import toastr from 'toastr';

export default {
    name: 'Login',
    data() {
        return {
            email: '',
            password: ''
        }
    },
    methods: {
        login: function() {
            firebase.auth().signInWithEmailAndPassword(this.email, this.password)
            .then(
                (user) => {
                    this.$router.go('fintechsocial' + user.message + this.created || true)
                    toastr.success('Bienvenido! es agradable tenerte cerca!')
                }
            )
            .catch (err =>
              toastr.error('Yikes! '+ err.message))
        },
        signInWithGoogle: function(){
          const provider = new firebase.auth.GoogleAuthProvider()
          firebase.auth().signInWithPopup(provider)
          .then(
          this.$router.go('fintechsocial'),
                  toastr.success('Bienvenido! es agradable tenerte cerca!')
  )
          .catch (err =>
            toastr.error('Yikes! '+ err.message))
        },
    },
    created () {
      firebase.auth().onAuthStateChanged(user => {
        this.authUser = user
      })
    }
}

</script>
