<template>
  <div class="container">
    <div class="file-upload">
      File Upload Component
      <br />
      Dropable: {{ configsFileUpload.dropable }}

      <slot :file="fileObj"></slot>

      <slot name="dropareabottom"></slot>
      <slot name="dropareabottom1"></slot>
      <slot name="dropareabottom2" v-bind:number="3"></slot>
      <slot
        name="dropareabottom3"
        v-bind:double="5 + 5"
        v-bind:square="5 * 5"
      ></slot>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    configsFileUpload: {}
  },
  methods: {},
  data() {
    return {
      fileObj: { id: 1, name: "file1" }
    };
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
  height:300px;
  border: 1px solid #ccc;
}
</style>
