<script setup>
import {ref} from "vue";

const passwordLength = ref(10);
const generatedPassword = ref('');
let result = ref('');
const uppercase_Checkbox = ref('');
const lowercase_Checkbox = ref('');
const numbers_Checkbox = ref('');
const symbols_Checkbox = ref('');

const generatePassword = () => {

  let characters = '';

  if (uppercase_Checkbox.value && uppercase_Checkbox.value.checked) {
    characters += 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
  }

  if (lowercase_Checkbox.value && lowercase_Checkbox.value.checked) {
    characters += 'abcdefghijklmnopqrstuvwxyz';
  }

  if (numbers_Checkbox.value && numbers_Checkbox.value.checked) {
    characters += '0123456789';
  }

  if (symbols_Checkbox.value && symbols_Checkbox.value.checked) {
    characters += '!@#$%^&*()-_=+/?';
  }

  let password = '';
  for (let i = 0; i < passwordLength.value; i++) {
    password += characters.charAt(Math.floor(Math.random() * characters.length));
  }
  generatedPassword.value = password;
  result.value.classList.remove('show');
}

const copyToClipboard = () => {
  navigator.clipboard.writeText(generatedPassword.value);
  result.value.classList.add('show');
}

</script>

<template>
  <div class="uk-container uk-container-small">
    <div class="card uk-card uk-card-default uk-card-body uk-width-1-2@m">
      <h3 class="title uk-card-title">Password Generator</h3>
      <div class="result-container">
        <span id="result" ref="result">{{ generatedPassword }}</span>
        <img @click="copyToClipboard" class="img" src="../assets/content_paste_black_24dp.svg" id="clipboard"
             alt="Copy">
      </div>

      <div class="settings">
        <div class="setting">
          <label>Password length</label>
          <input class="uk-input" type="number" v-model="passwordLength" min="0" max="20"/>
        </div>
        <p></p>

        <div class="setting">
          <label>Include uppercase letters</label>
          <input class="uk-checkbox" type="checkbox" ref="uppercase_Checkbox" checked/>
        </div>
        <div class="setting">
          <label>Include lowercase letters</label>
          <input class="uk-checkbox" type="checkbox" ref="lowercase_Checkbox" checked/>
        </div>
        <div class="setting">
          <label>Include numbers</label>
          <input class="uk-checkbox" type="checkbox" ref="numbers_Checkbox" checked/>
        </div>
        <div class="setting">
          <label>Include symbols</label>
          <input class="uk-checkbox" type="checkbox" ref="symbols_Checkbox" checked/>
        </div>
      </div>

      <button @click="generatePassword" class="button uk-button uk-button-default uk-width-1-1" id="generate">Generate
        Password
      </button>

    </div>
  </div>

</template>

<style scoped lang="scss">
.card {
  margin: 6rem auto;
  border-radius: 1rem;

  .title {
    text-align: center;
    color: #666;
  }


  .result-container {
    display: flex;
    align-items: center;
    position: relative;
    font-size: 18px;
    letter-spacing: 1px;
    padding: 12px 10px;
    height: 1.6rem;
    width: 100%;
    justify-content: space-between;
    border: 1px solid #e5e5e5;

    #result {
      word-wrap: break-word;
      max-width: calc(100% - 40px);
    }

    .img:hover {
      cursor: pointer;
    }

  }

  .settings {

    .setting {
      margin-top: 0.5rem;
      display: flex;
      align-items: center;
      justify-content: space-between;

      label {
        font-size: 1.3rem;
      }

      .uk-checkbox:checked {
        background-color: #666;
      }
    }
  }

  .button {
    margin-top: 0.5rem;
    color: #666;
  }

}

.show {
  background-color: #666;
  color: #fff;
}


</style>
