<style scoop>
form.v-form.mb-10.px-10 {
padding: 0 !important;
}
.main-content {
margin:auto;
}
.post-image {
max-width:100px;
}
</style>

<template>
<!-- form here :D -->
<v-form
class="mb-10 px-10"
v-model="valid"
v-on:submit.prevent="addPost"
>
  <v-card class=" d-flex align-self-start flex-column"  cols="auto">
    <v-row no-gutters>
      <v-col  class="s-div "  cols="1">
        <v-img
        class="align-center post-image"
        :src="authUser.photoURL">
        </v-img>
      </v-col>
      <v-col  class="s-div d-flex" cols="11">
      <v-textarea
      v-model="newPost.postText"
      :rules="postRules"
      :counter="155"
      rows="2"
      class="pt-5"
      label="Share your thoughts! 😎"
      required>
    </v-textarea>
    <v-btn
    class="ml-3 m-tb-20 align-self-end"
    @click="markcompleted();"
    type="submit"
    small color="primary"
    dark
    >
      {{ displayText }}
    </v-btn>
      </v-col>
    </v-row>
  </v-card>
  </v-form>
</template>
  <script>

  import firebase from '@/plugins/firebase'
  import toastr from 'toastr';
  let db = firebase.database();
  let messagesRef = db.ref('posts');

  export default {
  name: 'FeedForm',
  data: () => ({
  authUser: '',
  displayName: '',
  displayText: 'send',
  newPost: {
      postText: '',
      displayName: '',
      photoURL: '',
  },

  postRules: [
      v => !!v || 'Content is required amigo!'
  ]

  }),

  methods: {
      addPost: function() {
          messagesRef.child(this.authUser.uid).push(this.newPost);
          this.newPost.postText = '';
          this.authUser.displayName = '';
          this.authUser.photoURL = '';
          toastr.success('Horray! message sent successfully');
          this.displayText = 'Nice job!'
          this.postRules = true;
      },
      markcompleted: function() {
          this.displayText = 'something is strange';
      }
  },
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
                this.newPost.displayName = user.displayName
                this.newPost.photoURL = user.photoURL
                }
              })
        }

  }
  </script>
