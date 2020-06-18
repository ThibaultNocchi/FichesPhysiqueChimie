<template>
  <div class="card">
    <div class="card-body">
      <h5 class="card-title">{{ file.name }}</h5>
      <h6 class="card-subtitle mb-2 text-muted">{{ subtitle }}</h6>
      <p class="card-text">{{ tags_joined }}</p>
      <a
        :href="public_path + 'pdfs/' + file.name"
        class="card-link"
        target="_blank"
        >Lien</a
      >
    </div>
  </div>
</template>

<script>
export default {
  props: { file: { required: true } },
  data() {
    return {
      public_path: process.env.BASE_URL
    };
  },
  name: "File",
  computed: {
    tags_joined() {
      return this.file.tags.map(el => '"' + el + '"').join(" ");
    },
    subtitle() {
      return this.file.physic ? "Physique" : "Chimie";
    }
  }
};
</script>
