<template>
  <div id="app" class="container mt-4">
    <div class="card">
      <div class="card-body">
        <h5 class="card-title">
          Épinglé
        </h5>

        <h6 class="card-title mt-4">Autres</h6>
        <a
          :href="public_path + 'hard_coded_files/' + el"
          target="_blank"
          class="card-link"
          v-for="(el, idx) in hard_coded"
          :key="idx"
          >{{ get_filename(el) }}</a
        >

        <h6 class="card-title mt-4">Programme prépa</h6>
        <a
          :href="public_path + 'hard_coded_files/Prepa/' + el"
          target="_blank"
          class="card-link"
          v-for="(el, idx) in prepa"
          :key="idx"
          >{{ get_filename(el) }}</a
        >

        <h6 class="card-title mt-4">Liens</h6>
        <a
          :href="el.link"
          target="_blank"
          class="card-link"
          v-for="(el, idx) in links"
          :key="idx"
          >{{ el.name }}</a
        >
      </div>
    </div>

    <div class="form-inline my-4">
      <div class="form-group">
        <input
          type="text"
          id="search_query"
          class="form-control"
          placeholder="Recherche"
          v-model="search_query"
        />
      </div>

      <div class="form-check form-check-inline ml-4">
        <input
          class="form-check-input"
          type="checkbox"
          id="physic"
          v-model="physic"
        />
        <label class="form-check-label" for="physic">Physique</label>
      </div>
      <div class="form-check form-check-inline">
        <input
          class="form-check-input"
          type="checkbox"
          id="chemistry"
          v-model="chemistry"
        />
        <label class="form-check-label" for="chemistry">Chimie</label>
      </div>

      <button class="btn btn-danger ml-2" @click="clear">
        Effacer
      </button>
    </div>

    <FilesList
      :search_query="search_query"
      :physic="physic"
      :chemistry="chemistry"
    ></FilesList>
  </div>
</template>

<script>
import FilesList from "@/components/FilesList.vue";
export default {
  name: "App",
  components: { FilesList },
  methods: {
    clear() {
      this.search_query = "";
      (this.physic = false), (this.chemistry = false);
    },
    get_filename(path) {
      let splitted = path.split("/");
      return splitted[splitted.length - 1];
    }
  },
  data() {
    return {
      search_query: "",
      physic: false,
      chemistry: false,
      hard_coded: [
        "LPQ_en_30_minutes.pdf",
        "Notes LP43.pdf",
        "Evolution d'équilibre NO2 N2O4.pdf"
      ],
      prepa: [
        "Électricité Électronique Conversion de puissance.pdf",
        "Électromagnétisme.pdf",
        "Mécanique des fluides.pdf",
        "Mécanique.pdf",
        "Ondes.pdf",
        "Optique.pdf",
        "Oscillateurs _ Traitement de signal _ Relativité.pdf",
        "Quantique.pdf",
        "Thermodynamique.pdf"
      ],
      links: [
        {
          name: "Exemples plans",
          link: "https://fiches-agreg-physique.fr/pdf/Fiches_agreg.pdf"
        },
        {
          name: "Programmes Python",
          link:
            "http://cdrom2016.agregation-physique.org/index.php/programmes-informatiques/programme-python"
        },
        {
          name: "Ressources prépa Montrouge",
          link: "http://ressources.agreg.phys.ens.fr/ressources/"
        },
        {
          name: "Ressources Paul",
          link: "http://agreg-remigereau.e-monsite.com/"
        },
        {
          name: "Ressources prépa Rennes",
          link:
            "https://ged.univ-rennes1.fr/nuxeo/nxpath/default/default-domain/sections/ufr/UFR%20SPM.1548773351600/Internet/Agregation%20de%20Physique/Programmes%20Python@view_documents?tabIds=%3A&conversationId=0NXMAIN1"
        }
      ],
      public_path: process.env.BASE_URL
    };
  }
};
</script>

<style lang="scss">
@import "../node_modules/bootstrap/scss/bootstrap";
</style>
