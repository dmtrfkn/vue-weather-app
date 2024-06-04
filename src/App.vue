<script>
import axios from 'axios';

export default {
  data() {
    return {
      city: '',
      error: '',
      info: null,
    };
  },
  computed: {
    cityName() {
      return this.city + 'e';
    },
    showTemp() {
      return 'Температура: ' + this.info.main.temp;
    },
    showFeelsLike() {
      return 'Ощущается как: ' + this.info.main.feels_like;
    },
    showMinTemp() {
      return 'Минимальная температура: ' + this.info.main.temp_min;
    },
    showMaxTemp() {
      return 'Максимальная температура: ' + this.info.main.temp_max;
    },
  },

  methods: {
    getWeather() {
      if (this.city.trim().length < 2) {
        this.error = 'Нужно больше, чем 1 символ';
        return false;
      }

      this.error = '';

      axios
        .get(
          `https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=3d9de74844d28377e81415151cbe6a66`,
        )
        .then((res) => (this.info = res.data));
    },
  },
};
</script>

<template>
  <!-- <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />
    </div>
  </header>
 -->
  <div class="wrapper">
    <h1>Погодное приложение</h1>
    <p>Узнать погоду в {{ city === '' ? 'вашем городе' : cityName }}</p>
    <input v-model="city" type="text" placeholder="Введите город" />
    <button @click="getWeather()" v-if="city !== ''">Получить погоду</button>
    <button v-else disabled>Введите название города</button>
    <p class="error">{{ error }}</p>

    <div v-if="info != null">
      <p>{{ showTemp }}</p>
      <p>{{ showFeelsLike }}</p>
      <p>{{ showMinTemp }}</p>
      <p>{{ showMaxTemp }}</p>
    </div>
  </div>
</template>

<style scoped>
.wrapper {
  width: 900px;
  height: 500px;
  padding: 20px;
  border-radius: 50px;
  text-align: center;
  background-color: #1f0f24;
}

.wrapper h1 {
  margin-top: 50px;
}

.wrapper p {
  margin-top: 20px;
}

.wrapper input {
  margin-top: 30px;
  background: transparent;
  border: 0;
  border-bottom: 2px solid #110813;
  color: #fcfcfc;
  font-size: 14px;
  padding: 5px 8px;
  outline: none;
}

.wrapper input:focus {
  border-bottom-color: #6e2d7d;
}

.wrapper button {
  background: #e3bc4b;
  color: #fff;
  border-radius: 10px;
  border: 2px solid口#b99935;
  padding: 10px 15px;
  margin-left: 20px;
  cursor: pointer;
  transition: transform 500ms ease;
}

.wrapper button:hover {
  transform: scale(1.1) translateY(-5px);
}

.wrapper button:disabled {
  background: #b99935;
  cursor: not-allowed;
}

.error {
  color: #d03939;
}
</style>

<!-- https://api.openweathermap.org/data/2.5/weather?q=Novosibirsk&units=metric&appid=3d9de74844d28377e81415151cbe6a66 -->
