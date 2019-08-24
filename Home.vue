<template>
  <section class="container">
    <div class="header">
  </div>
    <div class="columns">
      <div class="column is-8">
        <h1>Tournaments

        </h1>

        <div class="loader-section" v-if="loading">
          <div class="user-list">
            <div class="columns">
              <div class="column is-8">
                <p class="user-list__header animated-background__header"></p>
                <p class="user-list__sub animated-background__sub"></p>
                <p class="user-list__sub animated-background__sub"></p>
              </div>
              <div class="column is-4 right">
                <router-link class="button is-primary" to="/user">view profile </router-link>
              </div>
            </div>
          </div>

          <div class="user-list">
            <div class="columns">
              <div class="column is-8">
                <p class="user-list__header animated-background__header"></p>
                <p class="user-list__sub animated-background__sub"></p>
                <p class="user-list__sub animated-background__sub"></p>
              </div>
              <div class="column is-4 right">
                <router-link class="button is-primary" to="/user">view profile</router-link>
              </div>
            </div>
          </div>

          <div class="user-list">
            <div class="columns">
              <div class="column is-8">
                <p class="user-list__header animated-background__header"></p>
                <p class="user-list__sub animated-background__sub"></p>
                <p class="user-list__sub animated-background__sub"></p>
              </div>
              <div class="column is-4 right">
                <router-link class="button is-primary" to="/user">view profile</router-link>
              </div>
            </div>
          </div>

          <div class="user-list">
            <div class="columns">
              <div class="column is-8">
                <p class="user-list__header animated-background__header"></p>
                <p class="user-list__sub animated-background__sub"></p>
                <p class="user-list__sub animated-background__sub"></p>
              </div>
              <div class="column is-4 right">
                <router-link class="button is-primary" to="/user">view profile</router-link>
              </div>
            </div>
          </div>
        </div>

        <div class="user-list" v-for="tournament  in tournaments">
          <div class="columns">
            <div class="column is-8">
              <p>{{tournament.player1}} </p>
              <div class="inner">
                <div class="left">
                  <p class="user-list__sub"><strong> </strong>: {{tournament.id}}</p>
                </div>
                <div class="right">
                  <p class="user-list__sub"><strong></strong>: {{tournament.player3}}</p>
                </div>
                <div class="right">
<p>  {{tournament.player4}}
  </p>                
  </div>
                
              </div>
            </div>
            <div class="column is-4 right">
              <router-link class="button is-primary" v-bind:to="{ name: 'view-tournament', params: { tournament: tournament.fguid }}">
                view profile
                </router-link>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>

</template>

<script>
  import firebase from 'firebase'

  export default {
    name: 'home',
    data () {
      return {
        tournaments: [],
        loading: true,
        player1:'',
        player2:'',
        player3:'',
        player4:'',
      }
    },
    created () {

      firebase
      .firestore()
      .collection('tournaments').get().then((querySnapshot) => {
        this.loading = false
        querySnapshot.forEach((doc) => {
          let data = {
            'id': doc.id,
            'player1': doc.data().player1,
            'player2': doc.data().player2,
            'player3': doc.data().player3,
            'player4': doc.data().player4,
            'fguid': doc.data().fguid
          }
          this.tournaments.push(data)
        })
      })
    }
  }
</script>

<style lang="scss" scoped>
  
</style>

