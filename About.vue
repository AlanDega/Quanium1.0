<template>
  <div>
    <input type="text" name="playerTag" id="player-tag" v-model="playerTag">
    <button @click="sendTag">save</button>
    <h1>{{user.uid}}</h1>
    <h2>{{matchPlayer}}</h2>
    <h2>{{matchReferee}}</h2>
   <button @click="randomize1">show random player</button>

 <div v-for="player in unrandomPlayers"  >
   <p>{{player.playerTag}}</p>
   </div> 

<ul>
  <li>
  </li>
</ul>
  </div>
</template>

<script>
import firebase, { firestore } from 'firebase'
import { log } from 'util';


  export default {
    data() {
      return {
        Players: [],
        playerTag:'',
        refTag:'',
        refCommTag:'',
        user: '',
        unrandomPlayers:[],
        unrandomReferees:[],
        matchPlayer:[],
        matchReferee:[],
        matchedPlayer: false,
        matchedReferee: false,
        size: ''

      }
    },
        

  
    beforeCreate(){
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
     .firestore().collection('availableReferees').get().then(snap => {
   this.size = snap.size;
   console.log( this.size)
   while( matchedPlayer === false){

   if( this.size >= 2) { 
      firebase
      .firestore()
      .collection('availableReferees').get().then((querySnapshot) => {
        querySnapshot.forEach((doc) => {
          let data = {
           
            'refTag': doc.data().refTag,
           
          }
          this.unrandomReferees.push(data)
        })
        
        if (this.refTag = this.matchReferee)
          {
    var FCM = require('fcm-push');

var serverKey = 'AIzaSyBKNZILuDHy1iOPwXrphOD05b8BVpG2Mwk';
var fcm = new FCM(serverKey);

var message = {
    to: this.refCommTag,
    data: {
        your_custom_data_key: 'your_custom_data_value'
    },
    notification: {
        title: 'Title of your push notification',
        body: 'Body of your push notification'
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
        var list1= this.unrandomReferees
var randomMatch1 = list1[Math.floor(Math.random() * list1.length)];
console.log(randomMatch1)
this.matchReferee = randomMatch1;
  }
      else {
        console.log('not enough players')
      }
   }
      )
   
}
  
   
   }
     })
     }

     

      
 ,
           
    
methods:{
 

        acceptChallenge () {

       this.matchedPlayer = true 
        
           
 .then(docRef => {
              console.log('Document written with ID: ', docRef.id)
            })
            .catch(function (error) {
              console.error('Error adding document: ', error)
            });
        }

     }  
  }  
               // you have one. Use User.getToken() instead
</script>

<style lang="scss" scoped>

</style>