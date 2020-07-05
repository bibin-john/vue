<template>
  <div class="droparea">
    Drop Area Component <br>
     {{ configsDropArea.droparea }}
     <br>
    <slot name="footer" ></slot>
  </div>
</template>
<script>
export default {
  props: {
    configsDropArea: {}
  },
  methods: {}
};
</script>
<style scoped>
.droparea {
  border: orange 1px solid;
  height: 50px;
}
</style>
