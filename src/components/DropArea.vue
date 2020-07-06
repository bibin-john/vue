<template>
  <div
    class="droparea"
    :class="setClasses"
    @dragover.prevent="dragOver"
    @dragleave.prevent="dragLeave"
    @drop.prevent="drop($event)"
  >
    <div class="droparea-title">Drop the Files to upload</div>
    <div class="file-list-container">
      <div class="file-list-wrapper" v-for="file in fileList" :key="file.name">
        <span class="file-list-item"
          >{{ file.name }}
          <span class="close-icon" @click="removeItem(file.name)"></span
        ></span>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "DropArea",
  data() {
    return {
      isDragging: false,
      wrongFile: false,
      fileList: []
    };
  },
  computed: {
    setClasses() {
      return { isDragging: this.isDragging };
    }
  },
  props: {
    configsDropArea: {}
  },
  methods: {
    dragOver() {
      this.isDragging = true;
    },
    dragLeave() {
      this.isDragging = false;
    },
    async drop(e) {
      let dropedFiles = [...e.dataTransfer.files];
      let promises = [];
      dropedFiles.forEach(file => {
        promises.push(this.getFileDetails(file));
      });
      let dropedFileList = await Promise.all(promises);
      this.fileList = this.fileList.concat(dropedFileList);
      this.isDragging = false;
      this.uploadToServer();
    },
    getFileDetails(file) {
      const reader = new FileReader();
      return new Promise(resolve => {
        reader.onload = ev => {
          resolve({
            name: file.name,
            size: file.size,
            type: file.type,
            content: ev.target.result
          });
        };
        reader.readAsDataURL(file);
      });
    },
    removeItem(name) {
      this.fileList = this.fileList.filter(item => item.name !== name);
    },
    uploadToServer() {
      var formData = new FormData();
      this.fileList.forEach(file => {
        formData.append("uploads[]", file.content, file.name);
      });
      axios({
        method: "post",
        url: "http://localhost:8081/upload",
        data: formData,
        headers: { "Content-Type": "multipart/form-data" }
      })
        .then(function(response) {
          console.log(response);
        })
        .catch(function(response) {
          console.log(response);
        });
    }
  }
};
</script>
<style scoped>
.droparea {
  width: 100%;
  height: 100%;
  border: 2px dashed #ccc;
  border-radius: 10px;
  font-family: sans-serif;
  min-width: 100px;
  min-height: 100px;
}
.droparea-title {
  padding: 5px;
}
.isDragging {
  background-color: rgb(110, 110, 110);
  color: white;
}
.file-list-container {
  padding: 3px;
}
.file-list-wrapper {
  display: flex;
  align-items: center;
  justify-content: left;
  padding: 3px;
}
.file-list-item {
  padding: 3px 5px 3px 10px;
  background-color: #efecec;
  border-radius: 10px;
}
.close-icon {
  font-size: 15px;
  color: #f34545;
  margin-bottom: 11px;
  transition: color 0.2s ease-out;
  cursor: pointer;
}
.close-icon:after {
  content: "×";
}
</style>
