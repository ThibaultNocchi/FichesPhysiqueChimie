<template>
  <div>
    <h2>Fichiers</h2>
    <div class="row">
      <div
        v-for="(item, idx) in files"
        :key="idx"
        class="col-6 col-md-6 col-lg-4 col-xl-3 px-2 my-2"
      >
        <File :file="item"></File>
      </div>
    </div>
  </div>
</template>

<script>
import data from "@/assets/files.json";
import File from "@/components/File.vue";
export default {
  name: "FilesList",
  components: { File },
  data() {
    return {
      files: data
    };
  }
};
</script>
