<template>
  <button :class="colorClass" @click="modalOpen = true">{{ text }}</button>

  <Teleport to="body">
    <div class="create-account" v-if="modalOpen">
      <form action="POST">
        <div class="modal-header">
          <h2 class="title">Crie uma conta</h2>
          <button class="close-icon" @click="closeModal">
            <img src="../assets/close-icon.svg" alt="icone para cancelar" />
          </button>
        </div>
        <div class="fields">
          <div class="name-field">
            <label for="name">Nome</label>
            <input
              v-model.lazy="form.name"
              type="text"
              name="name"
              id="name-input"
              placeholder="Igor Halfeld"
            />
          </div>
          <div class="email-field">
            <label for="email">E-mail</label>
            <input
              v-model.lazy="form.email"
              type="email"
              name="email"
              id="email-input"
              placeholder="igor@exemplo.com"
            />
          </div>
          <div class="password-field">
            <label for="password">Senha</label>
            <input
              v-model.lazy="form.password"
              type="password"
              name="password"
              id="password-input"
              placeholder="****"
            />
          </div>
          <button @click.prevent="addNewPerson">Criar conta</button>
        </div>
      </form>
    </div>
  </Teleport>
</template>

<script setup>
import { reactive, ref } from "@vue/reactivity";
import { computed } from "@vue/runtime-core";
import useVuelidate from "@vuelidate/core";
import { required, email } from "@vuelidate/validators";

const modalOpen = ref(false);

// eslint-disable-next-line no-undef
defineProps(["text", "colorClass"]);

const form = reactive({
  name: "",
  email: "",
  password: "",
});

const rules = computed(() => {
  return {
    name: { required },
    email: { required, email },
    password: { required },
  };
});

const vuelidate = useVuelidate(rules);

function addNewPerson() {
  console.log(form);

  console.log(vuelidate.value.$error);
}

function cleanFields() {
  form.name = "";
  form.email = "";
  form.password = "";
}

function closeModal() {
  cleanFields();
  modalOpen.value = false;
}
</script>

<style scoped>
button {
  background: none;
  border: none;
  font-size: 18px;
}

.color-white {
  color: white;
  font-weight: 800;
  padding-right: 60px;
}

.color-pink {
  background-color: white;
  border-radius: 30px;
  color: #ef4983;
  font-weight: 800;
  padding: 10px 20px;
}

.create-account {
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: rgba(0, 0, 0, 0.2);
  position: fixed;
  top: 0;
}

.create-account form {
  background-color: white;
  border-radius: 2px;
  padding: 30px;
  width: 400px;
  height: 400px;
}

.modal-header {
  display: flex;
  justify-content: space-between;
  margin-bottom: 40px;
}

.modal-header button img {
  width: 15px;
}

.name-field,
.email-field,
.password-field {
  display: flex;
  flex-direction: column;
}

.name-field label,
.email-field label,
.password-field label {
  padding-bottom: 10px;
}

.name-field input,
.email-field input,
.password-field input {
  background-color: #f9f9f9;
  border: none;
  border-radius: 3px;
  padding: 8px 8px;
  margin-bottom: 20px;
  font-size: 20px;
}

form .fields button {
  background-color: #ef4983;
  border-radius: 30px;
  color: white;
  font-weight: 800;
  padding: 10px 20px;
  margin-top: 15px;
}
</style>
