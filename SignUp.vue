<template>
  <v-form>
    <v-container>
      <v-row>

        <v-col cols="12" sm="4">
          <v-text-field
            v-model="first"
            label="First Name"
            outlined
          ></v-text-field>
        </v-col>

        <v-col cols="12" sm="4">
          <v-text-field
            v-model="last"
            label="Last Name"
            outlined
          ></v-text-field>
        </v-col>
        <v-col cols="12" sm="4">
          <v-text-field
            v-model="refTag"
            label="refTag"
            outlined
          ></v-text-field>
        </v-col>

      </v-row>
      <v-btn @click="signUp">sign up</v-btn>
    </v-container>
  </v-form>
</template>
<script>
import firebase from 'firebase';
  export default {
    data: () => ({
      first: 'John',
      last: 'Doe',
      refTag: '',
    }),
    methods:{
    signUp(){
    
    firebase.auth().createUserWithEmailAndPassword(this.email, this.password).catch(function(error) {
  // Handle Errors here.
  var errorCode = error.code;
  var errorMessage = error.message;
  // ...
});
  }
  } 
  }
</script>