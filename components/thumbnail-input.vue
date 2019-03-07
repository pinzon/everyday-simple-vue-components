<template>
  <div class="input-container">
    <!-- Input Image -->
    <input ref='input' v-if="thumbnailUrl" type="file">
    <div v-else class="thumbnail-container">
        <img :src="thumbnailUrl" />
        <div class="black-hover" @click="deleteImage()">
           <span class="delete-button">&times;</span> 
        </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    value: {
      type: Object
    }
  },

  data: {
    thumbnailUrl: this.value ? this.value.url || null : null,
    validMimeTypes: ['image/jpeg', 'image/jpg', 'image/png'],
  },

  methods: {
    fileSelection: function(e) {
      component = this;
      var files = e.target.files || e.dataTransfer.files;

      if (!files.length) {
        this.$emit("update:value", null);
        this.$emit("change");
        return;
      }

      file = files[0];

      if (!this.validMimeTypes.includes(file.type)) {
        e.target.value = "";
        return;
      }

      this.$emit("update:value", file);
      this.$emit("change");

      var fr = new FileReader();
      fr.onload = function() {
        component.thumbnailUrl = fr.result;
      };
      fr.readAsDataURL(file);
    },

    deleteImage: function() {
      this.thumbnailUrl = "";
      this.$refs.input.value = "";
      this.$emit("update:value", null);
      this.$emit("change");
    }
  }
};
</script>

<style>
    .thumbnail-container{
        position: relative;
        max-width: 300px;
        height: 200px;
    }
    .thumbnail-container img{
        width: 100%;
    }
    .thumbnail-container .black-hover{
        display: none;
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-color: rgba(0,0,0,0.5);
        cursor: pointer;
        align-items: center;
    }

    .thumbnail-container:hover .black-hover{
        display: block;
    }

    .thumbnail-container .black-hover .delete-button {
        font-size: 25px;
        color: #fff;
        font-weight: bold;
        align-self: center;
    }


</style>


