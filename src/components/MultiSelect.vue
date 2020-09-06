<template>
  <div style="border:1px solid #ccc;margin-top:20px">
    <div style="display:flex">
      <div>{{ titleSection.titleName }}</div>
      <div>All</div>
      <div>clear</div>
      <div>X</div>
    </div>
    <div style="display:flex">
      <div v-for="option in selectOptions" :key="option.name">
        <input
          type="checkbox"
          :checked="option.selected"
          v-model="option.selected"
        />
        {{ option.name }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "MultiSelect",
  props: {
    titleSection: {
      type: Object
    },
    selectOptions: {
      type: Array
    }
  }
};
</script>

<style scoped lang="scss"></style>
