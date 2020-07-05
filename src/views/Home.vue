<template>
  <div class="home">
    <HelloWorld msg="HelloWorld msg" />

    <file-upload-component :configsFileUpload="fuconfigs">
      <!-- Default slot -->
      <template v-slot:default="{ file }">
        <div class="slot">
          Slot default ID: {{ file.id }}
          <br />
          Name: {{ file.name }}
          <br />
           <drop-area :configsDropArea="daconfigs">
               <template #footer>
                 Drop Area footer
               </template>
           </drop-area>
        </div>
      </template>
      <!-- Named slot  -->
      <template v-slot:dropareabottom>
        <div class="slot">This is slot bottom </div>
      </template>
      <!-- Named slot short hand -->
      <template #dropareabottom1>
        <div class="slot">This is slot bottom 1</div>
      </template>

      <!-- scoped slot  -->
      <template #dropareabottom2="scopedProps">
        <div class="slot">
          <div>This is slot bottom 2 </div>
          <div>Scoped props {{ scopedProps.number }}</div>
        </div>
      </template>

      <template #dropareabottom3="{double , square}">
        <div class="slot">
          <div>This is slot bottom 3</div>
          <div>Double {{ double }}</div>
          <div>Double {{ square }}</div>
        </div>
      </template>
    </file-upload-component>
   
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";
import DropArea from "@/components/DropArea.vue";
import FileUploadComponent from "@/components/FileUploadComponent.vue";

export default {
  name: "Home",
  components: {
    HelloWorld,
    FileUploadComponent,
    DropArea
  },
  data: function() {
    return {
      fuconfigs: { dropable: false },
      daconfigs: { droparea: "hide" }
    };
  }
};
</script>
<style lang="css" scoped>
.home {
  border: 1px solid black;
}
.slot {
  border: 1px dotted orangered;
}
</style>
