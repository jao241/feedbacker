/* eslint-disable @typescript-eslint/no-unused-vars */
<template>
  <button :class="colorClass" @click="modalOpen = true">{{ text }}</button>

  <Teleport to="body">
    <div class="create-account" v-if="modalOpen">
      <form>
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
              :class="{ errorField: errorNameField }"
              v-model.lazy="form.name"
              type="text"
              name="name"
              id="name-input"
              :placeholder="placeholder.name"
            />
            <span v-if="showNameErrorMessage">{{ errorMessage }}</span>
          </div>
          <div class="email-field">
            <label for="email">E-mail</label>
            <input
              :class="{ errorField: errorEmailField }"
              v-model.lazy="form.email"
              type="email"
              name="email"
              id="email-input"
              :placeholder="placeholder.email"
            />
            <span v-if="showEmailErrorMessage">{{ errorMessage }}</span>
          </div>
          <div class="password-field">
            <label for="password">Senha</label>
            <input
              :class="{ errorField: errorPasswordField }"
              v-model.lazy="form.password"
              type="password"
              name="password"
              id="password-input"
              :placeholder="placeholder.password"
            />
            <span v-if="showPasswordErrorMessage">{{ errorMessage }}</span>
          </div>
          <button
            @click.prevent="addNewPerson"
            :class="{
              loadingButton: showLoadIcon,
              activeButton: !showLoadIcon,
            }"
          >
            <p v-if="!showLoadIcon">Criar conta</p>
            <img
              v-if="showLoadIcon"
              id="loadImg"
              src="../assets/load-icon.svg"
              alt="icone de carregamento"
            />
          </button>
        </div>
      </form>
    </div>
  </Teleport>
</template>

<script setup>
import { ref } from "@vue/reactivity";

const modalOpen = ref(false);

// eslint-disable-next-line no-undef
defineProps(["text", "colorClass"]);

const placeholder = {
  name: "Igor Halfeld",
  email: "igor@exemplo.com",
  password: "****",
};

const form = ref({
  name: "",
  email: "",
  password: "",
});

const errorNameField = ref(false);
const errorEmailField = ref(false);
const errorPasswordField = ref(false);

const showNameErrorMessage = ref(false);
const showEmailErrorMessage = ref(false);
const showPasswordErrorMessage = ref(false);
const errorMessage = "* O campo é obrigatório";

const showLoadIcon = ref(true);

function validateFields() {
  if (!form.value.name) {
    showNameErrorMessage.value = true;
    errorNameField.value = true;
  }
  if (!form.value.email) {
    showEmailErrorMessage.value = true;
    errorEmailField.value = true;
  }
  if (!form.value.password) {
    showPasswordErrorMessage.value = true;
    errorPasswordField.value = true;
  }
}

function addNewPerson() {
  console.log(form.value);

  validateFields();
}

function cleanFields() {
  form.value.name = "";
  form.value.email = "";
  form.value.password = "";
}

function cleanErrorMessages() {
  errorNameField.value = false;
  errorEmailField.value = false;
  errorPasswordField.value = false;

  showNameErrorMessage.value = false;
  showEmailErrorMessage.value = false;
  showPasswordErrorMessage.value = false;
}

function closeModal() {
  cleanFields();
  cleanErrorMessages();
  modalOpen.value = false;
}
</script>

<style scoped>
button {
  background: none;
  border: none;
  font-size: 18px;
  cursor: pointer;
}

span {
  color: #f88676;
  font-size: 12px;
}

#loadImg {
  padding: 0 40px;
  width: 16px;
  animation: load 0.8s infinite;
}

.color-white {
  color: white;
  font-weight: 800;
  margin-right: 60px;
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
  padding-bottom: 10px;
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
  font-size: 20px;
  outline: none;
}

form .fields button {
  border-radius: 30px;
  color: white;
  font-weight: 800;
  padding: 10px 20px;
  margin-top: 15px;
}

.name-field .errorField,
.email-field .errorField,
.password-field .errorField {
  border: 3px solid #f88676;
}

.name-field .errorField::placeholder,
.email-field .errorField::placeholder,
.password-field .errorField::placeholder {
  color: #f88676;
}

.activeButton {
  background-color: #ef4983;
}

.loadingButton {
  background-color: rgba(239, 73, 131, 0.64);
}
@keyframes load {
  0% {
    transform: rotate(0deg);
  }

  100% {
    transform: rotate(180deg);
  }
}
</style>
