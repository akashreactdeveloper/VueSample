<template>
    <div>
      <div v-if="showPrompt" id="fullscreen-overlay">
        <div id="prompt-box">
          <h2>Welcome to Our Website</h2>
          <p>For the best experience, click below to enter fullscreen mode.</p>
          <button @click="enterFullscreen">Enter Fullscreen</button>
        </div>
      </div>
      <div id="content">
        <h1>Website Content</h1>
        <p>Enjoy your immersive experience.</p>
        <button id="exit-button" v-if="isFullScreen" @click="exitFullscreen">
          Exit Fullscreen
        </button>
      </div>
      <div
        v-if="isFullScreen"
        id="top-blocker"
        @mousemove="preventTopAccess"
      ></div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        isFullScreen: false,
        showPrompt: true, // Show the fullscreen prompt on page load
      };
    },
    methods: {
      async enterFullscreen() {
        try {
          // Request fullscreen
          await document.documentElement.requestFullscreen();
  
          // Lock all keys, including Esc
          if ("keyboard" in navigator && "lock" in navigator.keyboard) {
            await navigator.keyboard.lock(); // Locks all keys
          }
  
          this.isFullScreen = true;
          this.showPrompt = false;
        } catch (error) {
          console.error("Error entering fullscreen:", error);
        }
      },
      async exitFullscreen() {
        try {
          if (document.fullscreenElement) {
            // Unlock keyboard before exiting fullscreen
            if ("keyboard" in navigator && "unlock" in navigator.keyboard) {
              navigator.keyboard.unlock();
            }
  
            await document.exitFullscreen();
          }
          this.isFullScreen = false;
        } catch (error) {
          console.error("Error exiting fullscreen:", error);
        }
      },
      preventTopAccess(event) {
        // Push the cursor down if it tries to reach the top
        if (event.clientY < 50) {
          window.scrollTo(0, 50);
        }
      },
    },
  };
  </script>
  
  <style scoped>
  #fullscreen-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    background: rgba(0, 0, 0, 0.8);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 1000;
    color: white;
  }
  #prompt-box {
    text-align: center;
    background: #282c34;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.5);
  }
  #prompt-box button {
    padding: 10px 20px;
    font-size: 16px;
    color: white;
    background-color: blue;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }
  #prompt-box button:hover {
    background-color: darkblue;
  }
  #content {
    padding: 20px;
    text-align: center;
  }
  #exit-button {
    position: fixed;
    top: 10px;
    right: 10px;
    padding: 10px 20px;
    background-color: red;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }
  #exit-button:hover {
    background-color: darkred;
  }
  #top-blocker {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 50px; /* Set height to limit top access */
    background-color: transparent;
    z-index: 1001;
    pointer-events: none;
  }
  </style>
  