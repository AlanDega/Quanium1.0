<template>
    
        <div>
<div>
    <h1>{{user.uid}}</h1>
    <div v-for="ref in randomRef">
      <div>
    <p>{{ref.id}}</p>
    </div>
</div>
 <div v-for="referee in unrandomReferees"  >
   <p>{{referee.uid}}</p>
   </div> 

<ul>
  <li>
      {{this.unrandomReferees}}
  </li>
</ul>
  </div>
                  <h2>{{user.email}}</h2>
                  <h2>{{this.playerCommTag}}</h2>
                 
              
                <v-col cols="12">


             <v-card
    class="mb-10"
    max-width="400"
  >
    <v-list-item>
      <v-list-item-avatar color="grey"></v-list-item-avatar>
      <v-list-item-content>
        <v-list-item-title class="headline"></v-list-item-title>
        <v-list-item-subtitle>by Kurt Wagner</v-list-item-subtitle>
      </v-list-item-content>
    </v-list-item>

    <v-divider></v-divider>
                 <v-card-actions>

            <v-btn @click="notify"  >Start Match</v-btn>
            <v-btn >End Match</v-btn>
            <v-btn  >add point</v-btn>
            <v-btn >reduce point</v-btn>

            <!-- one click media sharing distribution -->
            </v-card-actions>
            </v-card>
             

                  
 
           


      </v-col>
   
            </v-row>
 

   
  </div>
  </div>
</template>

<script>
  import firebase from "firebase";
import { CometChat } from '@cometchat-pro/chat'

  export default {
    name: '',
    components:{
    },
    data () {
      return {
     
        playerCommTag:'',
  
        RefereeId: '',
        success: (this.$route.params.success),
      email:'',
      user:'',
      gameMode: '',
       username: "",
      session_id: "",
      receiver_id: null,
      error: false,
      showSpinner: false,
      incomingCall: false,
      ongoingCall: false,
       Players: [],
        playerTag:'',
        refTag:'',
        refCommTag:'',
        user: '',
        unrandomPlayers:[],
        unrandomReferees:[],
        unrandomReferees:[],
        matchPlayer:[],
        randomReferee:'',
        randomRef: [],
        matchedReferee: false,
        ruid: ''

      
      }
      },

      created(){

      var messaging = firebase.messaging();

messaging.requestPermission()
    .then(() => {
        console.log("Have Permission");
        return messaging.getToken();
    })
    .then(token => {

        console.log("FCM Token:", token);
        this.refCommTag = token 
        //Do something with TOken like subscribe to topics

    })
    .catch(error => {
        if (error.code === "messaging/permission-blocked") {
            console.log("Please Unblock Notification Request Manually");
        } else {
            console.log("Error Occurred", error);
        }
    });
       firebase.auth().onAuthStateChanged(user => {
            if (user) {
                this.user = user;
            }
        });
      firebase
     .firestore().collection('users').get().then(snap => {
   this.size = snap.size;
   console.log( this.size);
     
     if( this.size >= 1) { 
       firebase
      .firestore()
      .collection('users').where( "available" , "==", true ).limit(1).get().then((querySnapshot) => {
        this.loading = false
        querySnapshot.forEach((doc) => {
          let data = {
            'id': doc.id,
           
          }
          this.randomRef.push(data);
          if( doc.id == this.user.uid){
          var FCM = require('fcm-push');

var serverKey = 'AIzaSyBKNZILuDHy1iOPwXrphOD05b8BVpG2Mwk';
var fcm = new FCM(serverKey);

var message = {
    to: this.refCommTag,
    data: {
        your_custom_data_key: 'your_custom_data_value'
    },
    notification: {
        title: 'you have been chosen',
        body: 'accept or reject'
    }
};
fcm.send(message)


    .then(function(response){
        console.log("Successfully sent with response: ", response);
    })
    .catch(function(err){
        console.log("Something has gone wrong!");
        console.error(err);
    })
    firebase.firestore().collection("users").doc(doc.id).delete().then(function() {
    console.log("Document successfully deleted!");
}).catch(function(error) {
    console.error("Error removing document: ", error);
});
    
        
  }
  
        

        })
      })
       
     
    .catch(function(error) {
        console.log("Error getting documents: ", error);
    });


//if (this.user.uid == this.randomReferee.uid[0] ){
   //  
       console.log('success');
       
     
      }
       })
     
     },
     mounted(){
       

     },
     
        
      
      
      methods: {
        notify(){
         
        }}}
      
</script>

<style lang="scss" scoped>

</style>