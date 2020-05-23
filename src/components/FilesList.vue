<template>
  <h2>PDF</h2>
</template>

<script>
import data from "@/assets/files.json";
export default {
  name: "FilesList",
  data() {
    return {
      files: data
    };
  }
};
</script>
