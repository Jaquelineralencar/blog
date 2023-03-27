<template>
  <div id="accordionUsers">
  <div class="accordion" id="accordionExample" v-for="user in users" :key="user.id">
  <div class="accordion-item">
    <h2 class="accordion-header" >
      <button class="accordion-button" type="button" data-bs-toggle="collapse" :data-bs-target="'#' + user.id" aria-expanded="false" :aria-controls="user.id">
        {{user.username}}
      </button>
    </h2>
    <div :id="user.id" class="accordion-collapse collapse show" data-bs-parent="#accordionExample"> 
        <p>ID de identificação: {{ user.id }}</p>
       <p>Nome: {{ user.name }}</p>
       <p> Nome de usuário: {{ user.username }}</p>
       <p> E-mail: {{ user.email}}</p>
       <p> website: {{ user.website }}</p>
       <p>Informações pessoais: </p>
       <p> Endereço:</p>
       <p> Rua/Avenida: {{ user.address.street }}</p>
       <p> Número:  {{ user.address.suite }}</p>
       <p> Cidade: {{ user.address.city }}</p>
       <p> CEP: {{ user.address.zipcode }}</p>
       <p> Telefone: {{ user.phone }}</p>
       <p> Empresa: {{ user.company.name }}</p>
       <p> Slogan: {{ user.company.catchPhrase }}</p>
       <p> Ramo: {{ user.company.bs }}</p>   
    </div>
  </div>
</div>
</div>
</template>

<script>
import axios from "axios";
export default {
  name: "Users",
  props: {
    users: Array,
  },
  data() {
    return {
      users: [],
    };
  },
  mounted() {
    this.getUsers();
  },
  methods: {
    async getUsers() {
      const response = await axios.get(
        "https://jsonplaceholder.typicode.com/users"
      );
      if (response.status == 200) {
        this.users = response.data;
      } else {
        console.error("Erro");
      }
    },
  },
  idUser() {
    localStorage.setItem("idUser", user.id);
  },
};
</script>


<style scoped>
#accordionUsers {
  margin: 1rem;
  border: 1px solid black;

  margin: 3rem 1rem 1rem 8rem;
  text-align: center;

  width: 80%;
}

</style>