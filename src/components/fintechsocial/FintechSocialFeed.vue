
<style scoped>

.feed-card {
width:100% !important;
box-shadow: 0px 0px 4px -1px gray;
padding:7px !important;
}
</style>
<template>
    <div>
           <div
           v-for="post in allPosts.slice().reverse()"
           :key="post._key">
           <v-card class=" feed-card my-3">
           <v-row no-gutters>
           <v-col cols="1">
           <v-img
           class="align-center rounded-xl "
           width="30"
           :src="post.photoURL">
           </v-img>
           </v-col>
           <v-col cols="10">
             <p class="">{{post.postText}}</p>
             <p class="blue-grey--text ">{{post.displayName}}</p>
             <p class="mb-n1 mt-n5 d-flex flex-row-reverse"> {{post.date}} {{post.time}}</p>
             </v-col>
             </v-row>
       </v-card>
     </div>
   </div>
</template>
<script>
import firebase from '@/plugins/firebase'

let db = firebase.database();
//let usersRef = db.ref('users');
let postRef = db.ref('posts');
export default {
  name: 'FintechSocialFeed',
  data: () => ({
  authUser: null,
  allPosts: [] // initialise an array
}),
  methods: {
  },
  created: function() {
    data => console.log(data.user, data.credential.accessToken)
    firebase.auth().onAuthStateChanged(user => {
        if (user) {
          postRef.on('value', snapshot => {
            const val = snapshot.val()
            if (val) {
              this.allPosts = Object.values(val).flatMap(posts =>
              Object.entries(posts).map(([ _key, post ]) => ({ _key, ...post})))
            }
            console.log(snapshot.val())
          });
        }

     })
   }
}
</script>
