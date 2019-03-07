<template>
  <div id="app">
    <h3>Action Checkbox</h3>Status:
    <action-checkbox v-model="checkboxStatus" @click="checkboxAction"></action-checkbox>
    {{checkboxStatus ? 'True' : false}}

    <h3>CountDown</h3>Time left:
    <countdown :active="checkboxStatus" :seconds.sync="secondsLeft"></countdown>

    <h3>File List Input</h3>
    <div style="width: 100%">
      <filelist-input v-model="fileList"></filelist-input>
    </div>

    <h3>Modal</h3>
    <button type="button" @click="showModal = true">Show Modal</button>
    <modal v-if="showModal"> 
      This is a modal <br>
      <button @click="showModal =  false"><i class="fa fa-times"></i> Close</button>
    </modal>

    <h3>Paginator</h3>
    <paginator :pages="10" :current.sync="currentPage" ></paginator>

     <h3>Thumbnail Input</h3>
     <div style="width: 100%">
      <thumbnail-input v-model="profileImage" ></thumbnail-input>
    </div>
    

  </div>
</template>

<script>
import ActionCheckbox from "./components/ActionCheckbox.vue";
import Countdown from "./components/Countdown.vue";
import FilelistInput from "./components/FilelistInput.vue";
import Modal from "./components/Modal.vue";
import Paginator from "./components/Paginator.vue";
import ThumbnailInput from "./components/ThumbnailInput.vue";

export default {
  name: "app",
  components: {
    ActionCheckbox,
    Countdown,
    FilelistInput,
    Modal,
    Paginator,
    ThumbnailInput
  },

  data: function() {
    return {
      checkboxStatus: true,
      secondsLeft: 10000,
      fileList: null,
      showModal:false,
      currentPage: 0,
      profileImage: null
    };
  },

  methods: {
    checkboxAction: function(e) {
      console.log("action for checkbox", e);
    }
  }
};
</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

</style>
