<script>
export default {
  data() {
    return {
      fullscreen: false
    };
  },
  methods: {
    toggleFullscreen() {
      document.querySelector(".v-app-bar").style.display = "none";
      let el = document.documentElement; // makes whole app fullscreen
      // let el = document.querySelector(".app-view"); // makes view fullscreen
      if (!this.fullscreen) {
        document.querySelector(".v-app-bar").style.display = "none";
        this.fullscreen = true;
        el.style.padding = "0px";
        if (el.requestFullscreen) {
          el.requestFullscreen();
        } else if (el.msRequestFullscreen) {
          el.msRequestFullscreen();
        } else if (el.mozRequestFullScreen) {
          el.mozRequestFullScreen();
        } else if (el.webkitRequestFullscreen) {
          el.webkitRequestFullscreen();
        }
      } else {
        location.reload();
        document.querySelector(".v-app-bar").style.display = "block";
        this.fullscreen = false;
        el.style.padding = "24px 96px";
        if (document.exitFullscreen) {
          document.exitFullscreen();
        } else if (document.webkitExitFullscreen) {
          document.webkitExitFullscreen();
        } else if (document.mozCancelFullScreen) {
          document.mozCancelFullScreen();
        } else if (document.msExitFullscreen) {
          document.msExitFullscreen();
        } else {
          console.log("Fullscreen API is not supported.");
        }
      }
    },
    setFullscreenEscapeListeners() {
      document.addEventListener(
        "fullscreenchange",
        this.fullscreenEscapedHandler,
        false
      );
      document.addEventListener(
        "mozfullscreenchange",
        this.fullscreenEscapedHandler,
        false
      );
      document.addEventListener(
        "webkitfullscreenchange",
        this.fullscreenEscapedHandler,
        false
      );
    },
    removeFullscreenEscapeListeners() {
      document.removeEventListener(
        "fullscreenchange",
        this.fullscreenEscapedHandler
      );
      document.removeEventListener(
        "mozfullscreenchange",
        this.fullscreenEscapedHandler
      );
      document.removeEventListener(
        "webkitfullscreenchange",
        this.fullscreenEscapedHandler
      );
    },
    fullscreenEscapedHandler() {
      // Required to handle when fullscreen is exited with ESC key
      const fullscreenElement =
        document.fullscreenElement ||
        document.mozFullScreenElement ||
        document.webkitFullscreenElement;
      this.fullscreen = fullscreenElement ? true : false;
      this.$forceUpdate(); // Required so that toolbar re-renders
      console.log(
        `${
          this.fullscreen
            ? "Entered fullscreen (Press ESC to exit)"
            : "Exited fullscreen"
        }`
      );
    }
  }
};
</script>
