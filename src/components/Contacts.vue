<template>
  <div class="contacts-container">
    <h1 class="headings">Наши контакты</h1>

    <div class="row">
      <div class="info-section">
        <p><strong>Email:</strong><br> info@farengeit-online.ru</p>
        <p><strong>Телефон:</strong><br> +7 495 260-18-27</p>
        <p><strong>Адрес пункта выдачи:</strong><br> МО, г. Королев, ул. Полевая 43/12</p>
        <p><strong>Адрес склада:</strong><br> г. Москва, 43-й км МКАД, Логистический центр «Славянский мир» павильон 27,
          ворота 7</p>
        <p><strong>Режим работы:</strong><br> Пн. – Сб.: с 9:00 до 19:00 <br>Вс. - выходной</p>
      </div>
      <img alt="Карта" height="481" src="/src/assets/img/map.png" width="569"/>
    </div>

    <div class="form-section">
      <h2>Форма обратной связи</h2>
      <form @submit.prevent="submitForm">
        <div class="form-group">
          <label for="name">Имя:</label>
          <input id="name" v-model="form.name" required type="text"/>
        </div>
        <div class="form-group">
          <label for="email">Email:</label>
          <input id="email" v-model="form.email" required type="email"/>
        </div>
        <div class="form-group">
          <label for="message">Ваше сообщение:</label>
          <textarea id="message" v-model="form.msg" required rows="7"></textarea>
        </div>
        <button type="submit">Отправить</button>
      </form>
    </div>
  </div>
</template>

<script setup>
import {ref} from 'vue';
import {request} from "@/utils/fetch.js";

const form = ref({
  name: '',
  email: '',
  msg: '',
})

const submitForm = async () => {
  await request("/feedback", 'POST', form.value)
  // Reset form fields after submission
  form.value.name = '';
  form.value.email = '';
  form.value.msg = '';
};
</script>

<style scoped>
.contacts-container {
  padding: 0 50px 50px;
  //max-width: 800px; /* Limit the width */
  margin: auto; /* Center the container */
  //background-color: #f9f9f9; /* Light background */
  //border-radius: 8px; /* Rounded corners */
  //box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
}

h1 {
  text-align: center;
  margin-bottom: 20px;
}

.info-section {
  margin-bottom: 30px; /* Space between sections */
}

.form-section {
  background-color: #dfdfdf; /* White background for form section */
  width: 800px;
  padding: 20px 20px 40px;
  border-radius: 8px; /* Rounded corners */
  justify-self: center;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

.form-group {
  margin: 20px; /* Space between form groups */
}

label {
  display: block; /* Block display for labels */
  margin-bottom: 5px; /* Space below labels */
}

input, textarea {
  width: 100%; /* Full width */
  padding: 10px; /* Inner padding */
  border: 1px solid #ccc; /* Border color */
  border-radius: 4px; /* Rounded corners */
}

button {
  width: 100%; /* Full width */
  padding: 10px;
  background-color: #007bff; /* Button color */
  color: white; /* Text color */
  border: none;
  border-radius: 4px; /* Rounded corners */
  cursor: pointer; /* Pointer cursor */
}

button:hover {
  background-color: #0056b3; /* Darker shade on hover */
}
</style>