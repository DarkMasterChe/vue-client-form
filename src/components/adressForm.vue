<template>
    <div class="adress-container">
  <h2>Адресс</h2>
  <div>
				<div class="styled-input-ad styled-input wide" :class="{ 'form-group--error': $v.index.$error }">
					<input type="text" v-model.trim="index" @input="setIndex($event.target.value)" required />
					<label>Индекс</label> 
                    <div>
                        <div class="error" v-if="!$v.index.minLength">Индекс должен содержать 6 цифр.</div>
                        <div class="error" v-if="!$v.index.maxLength">Индекс должен содержать 6 цифр.</div>
                        <div class="error" v-if="!$v.index.numeric">Используйте цифры.</div>
                    </div>
				</div>
			</div>
			<div class="right-row">
				<div class="styled-input-ad styled-input wide" :class="{ 'form-group--error': $v.country.$error }">
					<input type="text" v-model.trim="country" @input="setCountry($event.target.value)" required />
					<label>Страна</label> 
                    <div class="error" v-if="!$v.country.alpha">Используйте кирилицу.</div>
				</div>
			</div>
			<div>
				<div class="styled-input-ad styled-input wide" :class="{ 'form-group--error': $v.oblast.$error }">
					<input type="text" v-model.trim="oblast" @input="setOblast($event.target.value)" required />
					<label>Область</label> 
                    <div class="error" v-if="!$v.oblast.alpha">Используйте кирилицу.</div>
				</div>
        <div>
        <div class="styled-input-ad styled-input wide" :class="{ 'form-group--error': $v.city.$error }">
					<input type="text" v-model.trim="city" @input="setCity($event.target.value)" required />
					<label>Город</label> 
                    <div class="error" v-if="!$v.city.alpha">Используйте кирилицу.</div>
                    <div class="error" v-if="!$v.city.required">Поле не должно быть пустым.</div>
				</div>
                </div>
			</div>
			<div>
				<div class="styled-input-ad styled-input wide" :class="{ 'form-group--error': $v.street.$error }">
					<input type="text" v-model.trim="street" @input="setStreet($event.target.value)" required />
					<label>Улица</label> 
                    <div class="error" v-if="!$v.street.alpha">Используйте кирилицу.</div>
				</div>
			</div>
			<div>
				<div class="styled-input-ad styled-input wide" :class="{ 'form-group--error': $v.house.$error }">
					<input type="text" v-model.trim="house" @input="setHouse($event.target.value)" required />
					<label>Дом</label> 
                    <div class="error" v-if="!$v.house.alpha">Используйте цифры и кирилицу.</div>
				</div>
			</div>
</div>
</template>

<script>
import { required, minLength, maxLength, numeric, alpha } from 'vuelidate/lib/validators';
export default {
    name: 'AdressForm',
    data() {
    return {
      index: '',
      country: '',
      oblast: '',
      city: '',
      street: '',
      house: ''
    }
  },
   validations: {
    index: {
      minLength: minLength(6),
      maxLength: maxLength(6),
      numeric
    },
    country: {
      alpha: value => /^[а-яё]*$/i.test(value),
    },
    oblast: {
        alpha: value => /^[а-яё]*$/i.test(value),
    },
    city: {
        required,
        alpha: value => /^[а-яё]*$/i.test(value),
    },
    street: {
        alpha: value => /^[а-яё]*$/i.test(value),
    },
    house: {
        alpha: value => /^[а-яё0-9]*$/i.test(value),
    }

    
  },
  methods: {
    setIndex(value) {
      this.index = value
      this.$v.index.$touch()
    },
    setCountry(value) {
      this.country = value
      this.$v.country.$touch()
    },
    setOblast(value) {
      this.oblast = value
      this.$v.oblast.$touch()
    },
    setCity(value) {
      this.city = value
      this.$v.city.$touch()
    },
    setStreet(value) {
      this.street = value
      this.$v.street.$touch()
    },
    setHouse(value) {
      this.house = value
      this.$v.house.$touch()
    },
    showForm() {
        console.log("Form");
    }
  }
}
</script>


<style lang="sass" scoped>

h2
  margin-left: 50px

.adress-container
  width: 1000px
  max-width: 100%
  margin: 20px auto 25px auto

.styled-input-ad
  width: 220px
  margin: 5px
  position: relative
  border-radius: 4px
  float: left
  max-width: 100%
  margin-left: 70px

.wide
  float: left
  width: 400px
  max-width: 100%

.styled-input label
  color: rgb(27, 26, 26)
  padding: 10px 10px 10px 10px
  position: absolute
  top: 10px
  left: 0
  -webkit-transition: all 0.25s ease
  transition: all 0.25s ease
  pointer-events: none

input
  padding: 20px
  border: 10px
  width: 100%
  font-size: 15px
  background-color: #c5baba
  color: rgb(32, 32, 32)
  border-radius: 4px

  &:focus ~ label, &:valid ~ label
    margin-left: 12px
    font-size: 12px
    color: rgb(24, 23, 23)
    top: -5px
    transition: all 0.225s ease
</style>