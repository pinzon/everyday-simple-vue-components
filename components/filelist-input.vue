<template>
  <div v-if="filesArray.length" class="file-list">
    <div
      v-for="(file,index) in filesArray"
      :key="index"
      class="file-clickable"
      @click="deleteFromSelection(index)"
    >
      <span v-text="file.name" class="text"></span>
      <span class="delete">&times;</span>
    </div>
  </div>

  <input v-else class="form-control-file" ref="input" @change="fileSelection" type="file" multiple>
</template>
<script>
export default {
  props: ["files"], //Object variable where to save the list of files

  data: function() {
    return {
      filesArray: []
    };
  },

  computed: {},

  mounted: function() {},

  methods: {
    fileSelection: function(e) {
      this.filesArray = Array.from(e.target.files || e.dataTransfer.files);
      this.$emit("update:files", e.target.files || e.dataTransfer.files);
    },

    deleteFromSelection: function(indexToDelete) {
      this.filesArray = this.filesArray.filter(
        (e, index) => index != indexToDelete
      );
      var dTransfer = new DataTransfer();

      this.filesArray.forEach(element => {
        dTransfer.items.add(element);
      });

      this.$emit("update:files", dTransfer.files);
    }
  }
};
</script>
<style scoped>
.file-list {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  align-items: flex-start;
  width: 100%;
}

.file-clickable {
  color: white;
  background-color: rgba(50, 50, 50, 0.5);
  border-radius: 5px;
  padding: 5px;
  cursor: pointer;
  position: relative;
}

.file-clickable .delete {
  display: none;
  position: absolute;
  left: 45%;
  top: 10%;
  font-size: 20px;
  font-weight: bold;
}

.file-clickable:hover {
  background-color: rgba(0, 0, 0, 0.5);
}

.file-clickable:hover .text {
  visibility: hidden;
}
.file-clickable:hover .delete {
  display: block;
}
</style>


