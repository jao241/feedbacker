<template>
  <div class="home">
    <main v-if="false">
      <div class="main">
        <header>
          <img
            src="../assets/logo_white.svg"
            alt="logo feedbacker"
            class="logo"
          />
          <div class="header-buttons">
            <button class="color-white">Crie uma conta</button>
            <button>Entrar</button>
          </div>
        </header>
        <section class="main-content">
          <div class="description">
            <h2>Tenha um feedback.</h2>
            <h2>E faça seus clientes mais felizes!</h2>
            <p>
              Receba ideias, reclamações e feeedbacks com um simples widget na
              página.
            </p>
            <button @click="showCreateAccountModal">
              Crie uma conta grátis
            </button>
          </div>
          <div class="main-image">
            <img src="../assets/blue-ballons.svg" alt="foto de balões azuis" />
          </div>
        </section>
      </div>
      <section class="questions">
        <h2>Alguma dúvida?</h2>
        <p>Quer saber melhor como funciona e quais são os preços?</p>
        <button>Nos mande um e-mail</button>
      </section>
      <footer><p>feedbacker &copy; 2020</p></footer>
    </main>
  </div>
  <div class="create-account">
    <form>
      <div class="modal-header">
        <h2 class="title">Crie uma conta</h2>
        <button class="close-icon">X</button>
      </div>
      <div class="fields">
        <div class="name-field">
          <label for="name">Nome</label>
          <input type="text" name="name" id="name-input" />
        </div>
        <div class="email-field">
          <label for="email">E-mail</label>
          <input type="text" name="email" id="email-input" />
        </div>
        <div class="password-field">
          <label for="password">Senha</label>
          <input type="text" name="password" id="password-input" />
        </div>
        <button>Criar conta</button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  setup() {
    function showCreateAccountModal() {
      console.log("click");
    }

    return {
      showCreateAccountModal,
    };
  },
};
</script>

<style scoped>
button {
  background: none;
  border: none;
  font-size: 18px;
}

footer {
  align-items: center;
  background-color: #f4f4f4;
  bottom: 0;
  display: flex;
  justify-content: center;
  padding: 38px;
  position: relative;
  bottom: 0;
}

footer p {
  font-size: 18px;
}

.main {
  background-color: #ef4983;
}

.color-white {
  color: white;
}

header {
  align-items: center;
  display: flex;
  justify-content: space-between;
  padding: 30px;
}

.logo {
  padding-left: 80px;
}

.header-buttons {
  padding-right: 80px;
}

.header-buttons button {
  padding: 8px;
}

.header-buttons button:first-child {
  font-weight: 800;
  margin-right: 40px;
}

.header-buttons button:last-child {
  background-color: white;
  border-radius: 30px;
  color: #ef4983;
  font-weight: 800;
  padding: 10px 20px;
}

.main-content {
  display: flex;
  justify-content: space-around;
}

.description {
  color: white;
  padding-left: 200px;
  padding-top: 100px;
  width: 37%;
}

.description h2 {
  font-size: 48px;
}

.description p {
  font-size: 24px;
  margin: 10px auto 20px;
}

.description button {
  background-color: white;
  border-radius: 30px;
  color: #ef4983;
  font-weight: 800;
  padding: 10px 20px;
}

.main-image img {
  width: 450px;
}

.questions {
  align-items: center;
  display: flex;
  flex-direction: column;
  height: 30vh;
}

.questions h2 {
  color: #444444;
  font-size: 36px;
  padding-top: 40px;
}

.questions p {
  color: #444444;
  font-size: 18px;
  padding-bottom: 40px;
}

.questions button {
  background-color: #ef4983;
  border-radius: 30px;
  color: white;
  font-weight: 800;
  padding: 10px 20px;
}

.create-account {
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: lightblue;
}

.create-account form {
  background-color: lightcoral;
  padding: 30px;
  width: 300px;
}

.modal-header {
  display: flex;
  justify-content: space-between;
  margin-bottom: 40px;
}

.name-field {
  display: flex;
  flex-direction: column;
}

.name-field input {
  width: 90%;
}
</style>
