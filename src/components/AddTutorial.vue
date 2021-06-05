<template>
  <div class="submit-form">
    <div v-if="!submitted">
      <div class="form-group">
        <label for="nom">nom</label>
        <input
          type="text"
          class="form-control"
          id="nom"
          required
          v-model="tutorial.nom"
          name="nom"
        />
      </div>

      <div class="form-group">
        <label for="prenom">prenom</label>
        <input
          class="form-control"
          id="prenom"
          required
          v-model="tutorial.prenom"
          name="prenom"
        />
      </div>

      <div class="form-group">
        <label for="adresse_mail">adresse_mail</label>
        <input
          class="form-control"
          id="adresse_mail"
          required
          v-model="tutorial.adresse_mail"
          name="adresse_mail"
        />
      </div>
            <div class="form-group">
        <label for="sex">sex</label>
        <input
          class="form-control"
          id="sex"
          required
          v-model="tutorial.sex"
          name="sex"
        />
      </div>
            <div class="form-group">
        <label for="adresse">adresse</label>
        <input
          class="form-control"
          id="adresse"
          required
          v-model="tutorial.adresse"
          name="adresse"
        />
      </div>
            <div class="form-group">
        <label for="prenom">age</label>
        <input
          class="form-control"
          id="age"
          required
          v-model="tutorial.age"
          name="age"
        />
      </div>
            <div class="form-group">
        <label for="activites">activites</label>
        <input
          class="form-control"
          id="activites"
          required
          v-model="tutorial.activites"
          name="activites"
        />
      </div>
      <button @click="saveTutorial" class="btn btn-success">Submit</button>
    </div>

    <div v-else>
      <h4>You submitted successfully!</h4>
      <button class="btn btn-success" @click="newTutorial">Add</button>
    </div>
  </div>
</template>

<script>
import TutorialDataService from "../services/TutorialDataService";

export default {
  name: "add-tutorial",
  data() {
    return {
      tutorial: {
        id: null,
        nom: "",
        prenom: "",
        adresse_mail: "",
        sex: "",
        adresse: "",
        travail: "",
        age: "",
        activites: "",

      },
      submitted: false
    };
  },
  methods: {
    saveTutorial() {
      var data = {
        nom: this.tutorial.nom,
        prenom: this.tutorial.prenom,
        adresse_mail: this.tutorial.adresse_mail,
        sex: this.tutorial.sex,
        adresse: this.tutorial.adresse,
        travail: this.tutorial.travail,
        age: this.tutorial.age,
        activites: this.tutorial.activites
      };

      TutorialDataService.create(data)
        .then(response => {
          this.tutorial.id = response.data.id;
          console.log(response.data);
          this.submitted = true;
        })
        .catch(e => {
          console.log(e);
        });
    },
    
    newTutorial() {
      this.submitted = false;
      this.tutorial = {};
    }
  }
};
</script>

<style>
.submit-form {
  max-width: 300px;
  margin: auto;
}
</style>
