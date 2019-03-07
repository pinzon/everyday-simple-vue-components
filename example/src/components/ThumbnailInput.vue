<template>
  <div class="input-container">
    <!-- Input Image -->
    <input ref="input" v-if="!thumbnailUrl" @change="fileSelection" type="file">
    <div v-else class="thumbnail-container" @click="deleteImage()">
      <img :src="thumbnailUrl">
      <span class="delete-button">&times;</span>
      
    </div>
  </div>
</template>
<script>
export default {
  props:['value'],

  model:{
    prop: 'value',
    event: 'change'
  },

  data: function () {
    return {
      thumbnailUrl: '',
      validMimeTypes: ['image/jpeg', 'image/jpg', 'image/png'],
    }
  },

  methods: {
    fileSelection: function(e) {
      var component = this;
      var files = e.target.files || e.dataTransfer.files;

      if (!files.length) {
        this.$emit("change", null);
        return;
      }

      var file = files[0];

      if (!this.validMimeTypes.includes(file.type)) {
        e.target.value = "";
        return;
      }

      this.$emit("change", file);

      var fr = new FileReader();
      fr.onload = function() {
        component.thumbnailUrl = fr.result;
      };
      fr.readAsDataURL(file);
    },

    deleteImage: function() {
      this.thumbnailUrl = "";
      // this.$refs.input.value = "";
      this.$emit("update:value", null);
      this.$emit("change");
    }
  }
};
</script>

<style>
.thumbnail-container {
  position: relative;
  max-width: 300px;
  max-height: 200px;
  overflow: hidden;
  cursor: pointer;
}
.thumbnail-container img {
  max-width: 100%;
  max-height: 100%;
  position: relative;
}

.thumbnail-container:hover img {
  mask: linear-gradient(rgba(0, 0, 0, 1.0), #fff);
}

.thumbnail-container:hover .delete-button{
  display: block;
}

.thumbnail-container .delete-button {
  display: none;
  font-size: 30px;
  color: #000;
  font-weight: bold;
  align-self: center;
  position: absolute;
  top: 45%;
  left: 45%;
}
</style>


