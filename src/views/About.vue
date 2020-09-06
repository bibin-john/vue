<template>
  <div class="about">
    <h1>This is an about page</h1>
    <div style="margin:10px auto 10px auto;width:50%">
      <div v-for="file in episodicData" :key="file.id">
        <multi-select
          :titleSection="file.titleSection"
          :selectOptions="file.selectOptions"
          ref="multiselect"
        >
        </multi-select>
      </div>
      <a @click.prevent="getUserSelected()">get</a>
    </div>
  </div>
</template>
<script>
import MultiSelect from "@/components/MultiSelect";
export default {
  name: "about",
  components: { MultiSelect },
  data: function() {
    return {
      episodicData: [
        {
          id: 1,
          titleSection: { titleName: "music1.pdf" },
          selectOptions: [
            { name: "201", id:1, selected: true },
            { name: "202", id:2, selected: true },
            { name: "203", id:3, selected: false },
            { name: "204", id:4, selected: false }
          ]
        },
        {
          id: 2,
          titleSection: { titleName: "music2.pdf" },
          selectOptions: [
            { name: "201", id:1, selected: false },
            { name: "202", id:2, selected: false },
            { name: "203", id:3, selected: true },
            { name: "204", id:4, selected: true }
          ]
        }
      ]
    };
  },
  methods: {
    getUserSelected() {
      
      let episodicDetails = []
      this.$refs.multiselect.forEach(value => {
        let selected = [];
        value.selectOptions.forEach(value => {
          value.selected?selected.push(value):null;
        });

          episodicDetails.push({fileDetails:value.titleSection ,episodicDetails:selected});
      });
        
      console.log(episodicDetails);
    }
  }
};
</script>
