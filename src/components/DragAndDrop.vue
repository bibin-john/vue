<template>
  <div class="container">
    <div class="file-upload" @drop="drop" @dragover.prevent @dragenter.prevent>
      File Upload Component
    </div>
  </div>
</template>
<script>
export default {
  methods: {
    drop(e) {
      e.preventDefault();
      alert();
    }
  }
};
</script>
<style>
.container {
  margin: 10px;
  display: flex;
  justify-content: center;
  padding: 10px;
  border: 1px solid purple;
}

.file-upload {
  width: 300px;
  height: 100px;
  border: 1px solid #ccc;
  line-height: 100px;
}
</style>
