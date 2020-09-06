<template>
  <div class="about">
    <h1>This is an about page</h1>
    <div style="margin:10px auto 10px auto;width:50%">
      <div v-for="file in episodicData" :key="file.id">
        <multi-option-selector
          :details="file.details"
          :selectOptions="file.selectOptions"
          :removeItem="removeCallback"
          ref="multiselect"
        >
        </multi-option-selector>
      </div>
      <a @click.prevent="getUserSelected()">get</a>
    </div>
  </div>
</template>
<script>
import MultiOptionSelector from "@/components/MultiOptionSelector";
export default {
  name: "about",
  components: { MultiOptionSelector },
  data: function() {
    return {
      episodicData: [
        {
          details: { id: 1, titleName: "music1.pdf" },
          selectOptions: [
            { name: "201", id: 1, selected: true },
            { name: "202", id: 2, selected: true },
            { name: "203", id: 3, selected: false },
            { name: "204", id: 4, selected: false }
          ]
        },
        {
          details: { id: 2, titleName: "music2.pdf" },
          selectOptions: [
            { name: "201", id: 1, selected: false },
            { name: "202", id: 2, selected: false },
            { name: "203", id: 3, selected: true },
            { name: "204", id: 4, selected: true }
          ]
        }
      ]
    };
  },
  methods: {
    getUserSelected() {
      let episodicDetails = [];
      this.$refs.multiselect.forEach(value => {
        let selected = [];
        value.selectOptions.forEach(value => {
          value.selected ? selected.push(value) : null;
        });
        if (selected.length > 0) {
          episodicDetails.push({
            fileDetails: value.details,
            episodicDetails: selected
          });
        }
      });

      console.log(episodicDetails);
    },

    removeCallback(item) {
      console.log(item.details.id);
      this.episodicData = this.episodicData.filter(
        data => data.details.id !== item.details.id
      );
    }
  }
};
</script>
