<template>
  <div style="border:1px solid #ccc;margin-top:20px">
    <div style="display:flex">
      <div><i>@</i>{{ details.titleName }}</div>
      <div @click.prevent="checkAll">All</div>
      <div @click.prevent="clearAll">clear</div>
      <div @click.prevent="remove">X</div>
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
  name: "MultiOptionSelector",
  props: {
    details: {
      type: Object
    },
    selectOptions: {
      type: Array
    },
    removeItem: {
      type: Function
    }
  },
  methods: {
    checkAll() {
      this.selectOptions.forEach(element => {
        !element.selected ? (element.selected = true) : null;
      });
    },

    clearAll() {
      this.selectOptions.forEach(element => {
        element.selected ? (element.selected = false) : null;
      });
    },

    remove() {
      this.removeItem(this);
    }
  }
};
</script>

<style scoped lang="scss"></style>
