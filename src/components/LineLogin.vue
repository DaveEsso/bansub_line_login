<template>
    <div class="line-login">
      <button @click="lineLogin">Login with LINE</button>
    </div>
  </template>
  
  <script>
  export default {
    mounted() {
      // Load the LINE Login SDK
      if (!window.liff) {
        const script = document.createElement('script');
        script.src = 'https://static.line-scdn.net/liff/edge/2/sdk.js';
        document.head.appendChild(script);
        script.onload = () => this.initializeLineLogin();
      } else {
        this.initializeLineLogin();
      }
    },
    methods: {
      initializeLineLogin() {
        // Initialize the LINE Login SDK
        window.liff.init({ liffId: 'YOUR_LIFF_ID' });
      },
      lineLogin() {
        // Open the LINE Login popup
        window.liff.login();
      }
    }
  };
  </script>
  
  <style scoped>
  .line-login {
    text-align: center;
  }
  </style>
  