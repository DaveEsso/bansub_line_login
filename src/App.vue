<template>
    <div class="app">
      <line-login v-if="!loggedIn" @login-success="handleLoginSuccess" />
      <div v-else>
        <div class="user-profile">
          <img :src="userProfile.pictureUrl" :alt="userProfile.displayName" />
          <h2>{{ userProfile.displayName }}</h2>
          <p>{{ userProfile.userId }}</p>
        </div>
        <button @click="logout">Logout</button>
      </div>
    </div>
  </template>
  
  <script>
  import LineLogin from './LineLogin.vue';
  
  export default {
    components: {
      LineLogin
    },
    data() {
      return {
        loggedIn: false,
        userProfile: {}
      };
    },
    methods: {
      handleLoginSuccess() {
        // Retrieve user profile data after successful login
        window.liff.getProfile().then(profile => {
          this.userProfile = {
            userId: profile.userId,
            displayName: profile.displayName,
            pictureUrl: profile.pictureUrl
          };
          this.loggedIn = true;
        });
      },
      logout() {
        // Call the LINE Login SDK's logout method
        window.liff.logout();
        this.loggedIn = false;
        this.userProfile = {};
      }
    },
    mounted() {
      // Check the user's login status when the app loads
      window.addEventListener('load', () => {
        window.liff.init({ liffId: 'YOUR_LIFF_ID' }).then(() => {
          if (window.liff.isLoggedIn()) {
            this.handleLoginSuccess();
          }
        });
      });
    }
  };
  </script>
  
  <style>
  .app {
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  .user-profile {
    text-align: center;
  }
  </style>
  