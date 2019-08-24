<template>
    <div>
<h2>gamemode</h2>
<v-btn @click="addUserData">referee</v-btn>
    </div>
</template>

<script>
import firebase from 'firebase'
    export default {
        data() {
            return {
            }
        },
        created(){
firebase.auth().onAuthStateChanged(user => {
            if (user) {
                this.user = user;
                console.log(this.user.uid)
            }

        });
        },
        methods:{
          addUserData(){  
firebase.firestore().collection("users").doc(this.user.uid).set({
    available: true
   
})
.then(function() {
    console.log("Document successfully written!");
})
.catch(function(error) {
    console.error("Error writing document: ", error);
});

        }
        }
    }
</script>

<style lang="scss" scoped>

</style>