<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" />

    <ul>
      <li v-for="paciente in pacientes" :key="paciente.id">
        {{ paciente.nombre }} {{ paciente.apellido }} - {{ paciente.edad }} |
         {{ paciente. }}
      </li>
    </ul>
  </div>
</template>

<script>
import Firebase from "firebase"
import HelloWorld from "@/components/HelloWorld.vue";

export default {
  name: "Home",
  components: {
    HelloWorld,
  },
  data: () => ({
    pacientes: []
  }),
  mounted() {
  //  Firebase.firestore()
  //  .collection("pacientes")
  //  .get()
  //  .then(collection => {
  //    collection.forEach((document) => {
  //      this.pacientes.push({ id: document.id, ...document.data() });
  //    });
  //  });
    Firebase.firestore()
    .collection("pacientes")
    .onSnapshot((querySnapshot) => {
      this.pacientes = [];
      querySnapshot.forEach(document => {
        this.pacientes.push({ id: document.id, ...document.data() });

      })
    })
  },
};
</script>
