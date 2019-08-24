<template>
<div>
    <h3>Let´s create your Profile </h3 >
<h1>{{user.uid}}</h1>
      

  <v-form v-model="valid" @submit.prevent="saveProfile">
    <v-container>
      <v-row>
        <v-col
          cols="12"
          md="4"
        >
          <v-text-field
            v-model="refTag"      
            label="choose your reftag"
            name="ref-tag"
            required
          ></v-text-field>
        </v-col>
        <v-col
          cols="12"
          md="4"
        >
          <v-text-field
            v-model="Name"
            label="Name"
            name="name"
            required
          ></v-text-field>
        </v-col>

       
          </v-col >
     
        
      <v-col>
        <v-btn  type="submit" >create profile</v-btn>
      </v-col>
    </v-row>
    </v-container>
  </v-form>

      

      
     
</div> 
</template>

<script>
import firebase from "firebase";
    export default {
      name: 'create-profile',
      data () {
        return {
          picker:'',
          selectedGame:'',
          platform: null,
          tournamentName: null,
          player1:"",
          player2:"",
          player3:"",
          player4:"",
          refTag:'',
          entryStake: null,
           valid: false,
           date: '',
           time: '',
      menu: false,
      modal: false,
      menu2: false,
         refCommTag:'',
         refTag:'',
         Name:'',
         user:''
      
      
      }
      },
      created() {
       firebase.auth().onAuthStateChanged(user => {
            if (user) {
                this.user = user;
            }
        });

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
      },
     
       

      
      
 
    methods: {

      
           saveProfile() {
          
          const fguid = this.generateUUID()
          firebase
          .firestore()
          .collection('availableReferees')
          .add({
            refCommTag: this.refCommTag,
            Name: this.Name,
            refTag:this.refTag,
            uid: this.user.uid
      //      platform: this.platform,
     //       entryStake: this.entryStake,
      
          })
            .then(docRef => {
              console.log('Document written with ID: ', docRef.id)
            })
            .catch(function (error) {
              console.error('Error adding document: ', error)
            })
        },
        generateUUID () {
          let d = new Date().getTime()
          let uuid = 'xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx'.replace(/[xy]/g, function (c) {
            let r = (d + Math.random() * 16) % 16 | 0
            d = Math.floor(d / 16)
            return (c === 'x' ? r : (r & 0x3 | 0x8)).toString(16)
          })
          return uuid
        }
      }
    }
      

    
</script>

<style scoped>
  section {
    height: 100vh;
  }
  h1 {
    font-size: 30px;
    margin: 30px 0;
  }
  .input {
    height: 40px;
  }
</style>