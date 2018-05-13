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
                    <div class="brdcast">
                    <p style="white-space: pre-line;">{{ message }}</p>
                    <br>
                    <textarea id="message" v-model="message" placeholder="Message to broadcast"></textarea>
                    <br>
                    <button class="sendButton" v-on:click="sendMessage">Send</button>
                    </div>
                </div>
            </section>
        </div>
    </div>
</template>

<script>
import firebase from 'firebase'

const database = firebase.database()
export default {
  name: "Broadcast", 
  data() {
    return {
        
    };
  },

  methods:{
    sendMessage: function() {
       var msg = document.getElementById("message").value
       document.getElementById("message").value = "";
       msg = msg.trim()
       if(msg.length > 0){
<<<<<<< HEAD
           database.ref('Broadcast/Message').push('msg');
            //alert(msg);
                    this.$toast.open({
                    duration: 3000,    
                    message: 'Message sent !',
                    type: 'is-success'
                })
             }
        else{
            this.$toast.open({
                duration: 2000,
                message: 'Oops. cannot broadcast empty message !',
                type: 'is-danger'
            })
        }     
=======
           database.ref('Broadcast/Message').push(msg);
           database.ref('Broadcast/Message/Current').set(msg);
           database.ref('Broadcast/Message/Check').set("true");
            alert(msg); }
>>>>>>> 4d521b9e7b00a315349f507f99e5b33ea8a6aef5
        
    },
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

.brdcast {
height: 500px
}

textarea {
  width: 80%;
  height:30%;
  border-radius: 5px;
}

.sendButton {
    color: #fff;
    background-color: #5cb85c;
    border-color: #4cae4c;
    border: 1px solid transparent;
    border-radius: 4px;
    padding: 7px 14px;
    margin-left: -76%
}
</style>
