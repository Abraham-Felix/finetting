<style scoped>
  .s-div{
    box-shadow: 0px 0px 4px -1px gray;
    padding:7px !important;
  }
  

  .feed-wall {
  overflow-y: auto;
  height:520px;
  }

</style>
<!-- full scoped style to be revised -->
<style>
.top-r {
 text-align: -webkit-right;
}
main {
      position: initial !important;
}
.v-navigation-drawer--absolute {
    position: fixed;
    margin-top: 65px;
}
.v-application--wrap {
  min-height: 0;
}
</style>
<template>
<div class="ml-12" >

  <!-- Fintech Social container layout -->

    <v-container  fluid>
    <div class="main-content">
    <!-- form here :D -->
   <FeedForm/>

<!-- feed wall -->
<v-divider/>
          <div class="feed-wall">
            <FintechSocialFeed/>
          </div>
    </div>

      <!-- View/edit profile -->
        <v-dialog
          class="mb-16"
          v-model="dialog"
          max-width="1250px"
          >
        <div class=" top-r">
            <v-btn
            class="form-close-btn mr-3 mt-3"
            width="10px"
            @click="dialog = false"
            >
                <v-icon> mdi-close </v-icon>
            </v-btn>
          </div>
          <FintechSocialProfile/>
            <v-card-actions>
                <v-spacer></v-spacer>
            </v-card-actions>
        </v-dialog>
    </v-container>

    <v-navigation-drawer class="fill" v-model="drawer" :mini-variant.sync="mini" permanent absolute>
        <!-- user avatar -->
        <v-list-item class="px-2">
            <v-list-item-avatar>
                <v-img :src="authUser.photoURL"></v-img>
            </v-list-item-avatar>

            <v-list-item-title>
                {{displayName}}
            </v-list-item-title>

            <v-btn icon @click.stop="mini = !mini">
                <v-icon>mdi-chevron-left</v-icon>
            </v-btn>
        </v-list-item>
        <v-list nav dense>
            <v-list-item-group v-model="group" style="text-align:left" active-class="text--accent-4">
      <!-- add gigs side nav button -->
                <v-list-item>
                    <v-list-item-title @click.stop="dialog = true">
                    <v-list-item-icon>
                        <v-icon title="Profile"> mdi-account </v-icon>
                    </v-list-item-icon>
                     Profile
                    </v-list-item-title>
                </v-list-item>

            </v-list-item-group>
        </v-list>
    </v-navigation-drawer>
</div>

</template>

<script>


import firebase from '@/plugins/firebase'
import FintechSocialProfile from '@/components/fintechsocial/FintechSocialProfile.vue'
import FintechSocialFeed from '@/components/fintechsocial/FintechSocialFeed.vue'
import FeedForm from '@/components/fintechsocial/FeedForm.vue'

export default {
    name: 'FintechSocial',
    components: {
      FintechSocialProfile,
      FintechSocialFeed,
      FeedForm
    },
    data: () => ({
        menu: false,
        drawer: true,
        mini: true,
        dialog: false,
        authUser: '',
        displayName: '',
        viewgigdialog: false,
        tutorialdialog: false,
      }),
      created: function() {
          // functions
          var user = firebase.auth().currentUser;
          var uid;
          if (user != null) {
            uid = user.uid; // The user's ID, unique to the Firebase project. Do NOT use
                             // this value to authenticate with your backend server, if
                             // you have one. Use User.getToken() instead.
          }
            this.userID= uid;
          //data => console.log(data.user, data.credential.accessToken)
          firebase.auth().onAuthStateChanged(user => {
              this.authUser = user
              if (user) {
                  this.displayName = user.displayName
                  this.photoURL = user.photoURL
                  }
                })
          }

      }
</script>
