<template>
  <div>
    <section class="hero is-bold animated fadeIn bgcolor">
      <div class="hero-body">
          <div class="container">
            <h1 class="title textcolor">
                VALTRA
            </h1>
          </div>
      </div>
    </section>
    <div>
    <section class="hero is-bold animated slideInUp is-fullheight bodybgcolor">
      <!-- Hero head: will stick at the top -->
      <div class="hero-head">
        <nav class="navbar">
          <div class="container">
            <div class="navbar-brand">
            </div>
            <div class="navbar-menu">
              <div class="navbar">
                <a class="navbar"> <!-- is-active -->
                  <span class="navbar-item bgcolor">
                    <a class="button size" v-on:click="gotoHome">Home</a>
                  </span>
                </a>
                <a class="navbar">
                  <span class="navbar-item bgcolor">
                    <a class="button size">Broadcast</a>
                  </span>
                </a>
              </div>
              <div class="navbar-end">
                <span class="navbar-item bgcolor">
                  <button class="button" v-on:click="logout">Logout</button>
                </span>
              </div>
            </div>
          </div>
        </nav>
      </div>

      <!-- Hero content: will be in the middle -->
      <div class="hero-body" style="margin-top: -300px">
        <div class="container">
          <h1 class="title">
            Farmers
          </h1>
          <!-- <h2 class="subtitle">
            Subtitle
          </h2> -->
          <table class="table is-striped is-fullwidth">
          <thead>
              <tr>
                  <th class="has-text-center">Picture</th>
                  <th class="has-text-center">Name</th>
                  <th class="has-text-center">Location</th>
                  <th class="has-text-center">Status</th>
              </tr>
            </thead>
            <tbody>
                <tr v-for="(user, user_index) in users" :key="user_index">
                    <td class="center">
                      <img src="../assets/valtrasignature.png" style="width: 50px; height: 50px">
                    </td>
                    <td>{{user.Name}}</td>
                    <td><a @click="loadMap">{{user.Latitude}} / {{user.Longitude}}</a></td>
                    <td>{{user.Status}}</td>
                </tr>
            </tbody>
          </table>
        </div>
      </div>
    </section>
    </div>
  </div>
</template>

<script>

import firebase from 'firebase'

var config = {
  apiKey: "AIzaSyAn6m6RfMQFhhPe3hHIAqz4yMySBeuvMC8",
  authDomain: "valtra-5c843.firebaseapp.com",
  databaseURL: "https://valtra-5c843.firebaseio.com",
  projectId: "valtra-5c843",
  storageBucket: "valtra-5c843.appspot.com",
  messagingSenderId: "460566192298"
};    

firebase.initializeApp(config);

const database = firebase.database()

export default {
  name: 'Admin',
  data: function() {
    return {
      users: []
    }
  },
  mounted: function() {
    console.log("mounted")
    // database.ref('Users').on('child_added', snapshot => this.users.push({name: snapshot.val().Name, location= snapshot.val().Location, status: snapshot.val().Status}))
    database.ref('Users').on('child_added', snapshot => this.users.push(snapshot.val()))
  
  },
  methods: {
    logout: function() {
      firebase.auth().signOut().then(() => {
        this.$router.replace('login')
      })
    },
    // setUsers: function() {
    //   console.log("setUsers")
    //   this.users.push({Location: this.location, Name: this.name, Status: this.status})
    // },
    created: function() {  
      database.ref('Users').on('child_added', snapshot => this.users.push(snapshot.val()))
    },
    loadMap: function(){
      this.$router.replace('map')
    },
    gotoHome: function() {
        this.$router.replace('admin')
    }
  }
}
</script>

<style>
.bgcolor {
     background: #EF5451
 } 
.bodybgcolor {
  background: #E0E0E0
}
.textcolor {
    color: #FFFFFF
}
.size {
  height: 37px;
  width: 100px;
}
.center {
    text-align: center;
}
</style>