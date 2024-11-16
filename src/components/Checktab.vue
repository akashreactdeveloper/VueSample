<template>
  <div>
    <h1>My Application</h1>
    <p>Stay on this tab or you'll get a warning!</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isAlertShown: false,  // Flag to prevent multiple alerts
      isUserAway: false,    // Tracks if user has been away for the required time
      awayTimeout: null,    // Timeout to delay alert
    };
  },
  mounted() {
    document.addEventListener("visibilitychange", this.handleVisibilityChange);
    window.addEventListener("blur", this.handleBlur);
    window.addEventListener("focus", this.handleFocus);
  },
  beforeDestroy() {
    document.removeEventListener("visibilitychange", this.handleVisibilityChange);
    window.removeEventListener("blur", this.handleBlur);
    window.removeEventListener("focus", this.handleFocus);
    clearTimeout(this.awayTimeout);
  },
  methods: {
    handleVisibilityChange() {
      if (document.hidden) {
        this.scheduleWarning();
      } else {
        this.resetWarning();
      }
    },
    handleBlur() {
      this.scheduleWarning();
      // create button components

    },
    handleFocus() {
      this.resetWarning();
    },
    scheduleWarning() {
      if (!this.isAlertShown) {
        // Delay alert to prevent it from triggering due to brief interactions
        this.awayTimeout = setTimeout(() => {
          this.isUserAway = true;
          this.showWarning();
        }, 1000); // Adjust delay as needed
      }
    },
    resetWarning() {
      clearTimeout(this.awayTimeout);
      this.isUserAway = false;
      this.isAlertShown = false; // Reset to allow alerts in future cases
    },
    showWarning() {
      if (this.isUserAway && !this.isAlertShown) {
        this.isAlertShown = true;
        
        // Schedule alert to close automatically after 1 second if it gets stuck
        setTimeout(() => this.isAlertShown = false, 1000);

        alert("Warning: You have switched tabs or clicked outside of this tab!");
        this.isAlertShown = false; // Reset the flag after alert is shown
      }
    },
  },
};
</script>

<style scoped>
/* Your styles here */
</style>
