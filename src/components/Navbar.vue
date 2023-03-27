<template>
  <div id="nav">
    <router-link to="/">
      <img src="../assets/logo.png" alt="logo" id="logo" />
    </router-link> 
    <h1>Bem-vindo ao blog Lorem Ipsum!</h1>
    <a @click="confirmUser()"  id="user">Usuários do blog</a>
    
  </div>
</template>

<script>


export default {
 
  methods:{
    confirmUser() {
      var senha = "UserConfirm@123";
      var digitado =  prompt ("Digite a senha");
      if (digitado === senha) {
        this.$router.push('./user')
      }
      else{
        alert("Acesso negado")
    }
    },
  }
};
</script>

<style scoped>
#nav {
  background-color: black;
  border-bottom: 4px solid white;
  padding: 1rem 3rem;
  display: flex;
  align-items: center;
}

#nav h1 {
  text-align: center;
  color: aliceblue;
  font-size: large;
}

#logo {
  width: 30%;
}

@media (max-width: 576px) {
  #logo {
    width: 75%;
  }
}
@media (min-width: 1000px) {
  #logo {
    width: 40%;
  }
  #user{
    margin-left: 15rem ;  
  }
}
@media (min-width: 2500px) {
  #logo {
    width: 75%;
  }
  #user{
    margin-left: 40rem ;  
  }

}
#user{
    cursor: pointer;
    text-decoration: none;
    color: aliceblue;  
    
    text-align: center;                   
  }
</style>