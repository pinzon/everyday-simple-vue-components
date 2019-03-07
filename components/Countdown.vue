<template>
  <span>{{ stopwatch }}</span>
</template>

<script>
export default {
  props: [
    "active", // Bool condition to set if the countdown is running 
    "seconds" // Countdown time in seconds
    ],

  data: function() {
    return {
      stopwatch: '',
      interval: null // Old code for firefox
    };
  },

  beforeMount(){
    this.stopwatch = this.hhmmss(this.$props.seconds);
  },

  mounted() {
    // console.log('mounted')
    this.interval = setInterval(this.updateTimer, 1000);
    
  },

  beforeDestroy() {
    // console.log('destroyed')
    clearInterval(this.interval);
  },

  watch: {},

  methods: {
    updateTimer: function() {
      console.log('updating')
      if (this.$props.active && this.$props.seconds > 0) {
        this.$emit("update:seconds", this.$props.seconds - 1);
      }
      this.stopwatch = this.hhmmss(this.$props.seconds);
    },

    hhmmss: function(secs) {
        var minutes = Math.floor(secs / 60);
        secs = secs % 60;
        var hours = Math.floor(minutes / 60);
        minutes = minutes % 60;
        return `${this.pad(hours)}:${this.pad(minutes)}:${this.pad(secs)}`;
    },

    pad: function (num) {
      return ("0"+num).slice(-2);
    }
  }
};
</script>

<style>
</style>

