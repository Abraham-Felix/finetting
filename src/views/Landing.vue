<template>
<div id="app">
<!-- cloud transitions -->
  <CloudTransitions/>
  <v-container mt-15>
  <transition appear name="fade">
   <div class="mt-15">
      <h5>
        <span
        class="get primary--text pulsate-css"
        transition="scroll-y-transition">
        Welcome to Finetting
        </span>

              <div class="landing-intro text-sm-body-2 center mt-15">
                <h3 class="f-p  font-weight-medium align-justify text--secondary">

                  A place to be social and talk about financial technology.
                </h3>
              </div>
        <h4
        v-if="user.loggedIn"
        class="pt-5"
        >
        <router-link
        to="tutorials"
        >
        Be social in Finetting, it can lighten your mood and make you feel happier. </router-link> </h4>
      </h5>
       <v-divider class="mb-5" />
       <v-btn
       dark
       to="fintechsocial"
       v-if="user.loggedIn">
       Dashboard
       </v-btn>
     <div class="center nav-col-mid d-flex justify-center align-center">
       <v-dialog
         transition="dialog-bottom-transition"
         max-width="600"
       >
         <template v-slot:activator="{ on, attrs }">
           <v-btn
             v-if="!user.loggedIn"
             class="mx-10 nav-btns"
             dark
             small
             title="login"
             color="primary"
             v-bind="attrs"
             v-on="on"
           >
           <span class="web-nav-btns"> login </span>
           <span class="mobile-icons mdi mdi-account-key"></span></v-btn>
         </template>
         <template v-slot:default="dialog">
           <v-card class="my-0">
             <v-card-actions class="justify-end">
               <v-btn
                 text
                 @click="dialog.value = false"
               ><v-icon>mdi-close</v-icon></v-btn>
             </v-card-actions>
             <v-card-text>
<!-- Login Component  -->
             <Login/>
             </v-card-text>
           </v-card>
         </template>
       </v-dialog>
       <v-dialog
         transition="dialog-bottom-transition"
         max-width="600"
       >
         <template v-slot:activator="{ on, attrs }">
           <v-btn
           v-if="!user.loggedIn"
           class="mx-10 nav-btns"
           dark
           small
           title="sign up"
           color="primary"
           v-bind="attrs"
           v-on="on"
           >
           <span class="mobile-icons mdi mdi-account-edit"></span>
           <span class="web-nav-btns" title="create an account"> sign up</span>
         </v-btn>
         </template>
         <template v-slot:default="dialog">
           <v-card class="my-0">
            <v-card-actions class="justify-end">
              <v-btn
                text
                @click="dialog.value = false"
              ><v-icon>mdi-close</v-icon>
              </v-btn>
            </v-card-actions>
              <SignUp/>
           </v-card>
         </template>
       </v-dialog>
     </div>
<!-- Ape animation -->
<ApeSignAnimation/>
         <!-- Mockup Slider -->
      <div class=" pb-md-16 slide-card">
        <MockupSlider class="mb-16" />
      </div>
   </div>
  </transition>
 </v-container>
<!-- TechStackIcons Slider -->
 <TechStackIcons/>
</div>
</template>

<script>
import firebase from 'firebase';
import toastr from 'toastr';
import { mapGetters } from "vuex";
import Login from "@/components/forms/Login.vue";
import SignUp from "@/components/forms/SignUp.vue";
// import ApeSignAnimation from "@/components/animations/ApeSignAnimation.vue"
// import MockupSlider from "@/components/animations/MockupSlider.vue";
// import TechStackIcons from '../components/animations/TechStackIcons.vue'
// import CloudTransitions from "@/components/animations/CloudTransitions.vue"

export default {
  name: 'Landing',
  components: {
    Login,
    SignUp,
    // MockupSlider,
    // TechStackIcons,
    // CloudTransitions,
    // ApeSignAnimation
  },
  computed: {
    // map `this.user` to `this.$store.getters.user`
    ...mapGetters({
      user: "user",
    })
  },
  methods: {
  logout: function() {
    firebase.auth().signOut()
    .then(() => {
      this.$router.go('landing')
    })
    .catch (err =>
      toastr.error('Yikes! '+ err.message))
    .catch (
      toastr.success('You have logged out, Thanks for using Mexdev app, see ya!'))
  },
}
}
</script>

<style >

#app {
  overflow: hidden !important;
}
#body {
  overflow: hidden !important;
}
p {
  font-size: 12px !important;
}
h1 {
   font-size: min(3rem, 200%, 20vw) ;
}
h4 {
  text-align: revert !important;
}
.landing-intro {
  max-width: 900px;
}
.get {
  font-size: min(3rem, 200%, 20vw);
  color: #5388E6;
}
.on {
  font-size: 25px ;
  font-family: poppins ;
}
.slide-card {
    margin: 20px auto !important;
    max-width: 900px !important;
    min-width: auto !important;
    transition: 1s;
    display: block;
}
.h-des {
  font-size: 16px ;
  font-family: monospace;
  line-height: 1.8;
  max-width:85%;
  margin:auto;
  text-align: justify;
  transition: 1s;
}
//media queries
@media screen and (max-width:900px) {
  .h-des {
    font-size: 0.8em !important;
  }
  .f-p {
      font-size: 0.6em !important;
      width:80%;
      transition: 1s;
    }
}

</style>
