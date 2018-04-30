<template>
    <div>
        <section class="hero is-bold animated slideInDown bgcolor">
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
                        <span class="navbar-burger burger" data-target="navbarMenuHeroA">
                            <span></span>
                            <span></span>
                            <span></span>
                        </span>
                        </div>
                        <div id="navbarMenuHeroA" class="navbar-menu">
                        <div class="navbar">
                            <a class="navbar"> <!-- is-active -->
                            <span class="navbar-item bgcolor">
                                <a class="button size" v-on:click="gotoHome">Home</a>
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
            </section>
        </div>
    </div>
</template>

<script>
import firebase from 'firebase'
export default {
  name: "Broadcast", 
  data() {
    return {
        
    };
  },

  methods:{

    logout: function() {
        firebase.auth().signOut().then(() => {
        this.$router.replace('login')
            })
    },
    gotoHome: function() {
        this.$router.replace('admin')
    }
  }
};
</script>

<style>
.bgcolor {
     background: #EF5451
 }
.textcolor {
    color: #FFFFFF
}
</style>
