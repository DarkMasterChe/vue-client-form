<template>
<div>
<div class="container">
	<div class="row">
	</div>
	<div class="row input-container">
		<h2>Паспортные данные</h2>
            <div>
                <span class="left"></span>
                <div class="selector">
                    <span class="left">Тип документа</span>
                    <div class="styled-input wide" :class="{ 'form-group--error': $v.document.$error }">
                        <select id="clientgroup" v-model.trim="document" @input="setDocument($event.target.value)" required>
                        <option value="ivanov">Паспорт</option>
                        <option value="zaharov">Свидетельство о рождении</option>
                        <option value="chernushova">Вод. удоставерение</option>
                        </select>
                    </div>
                </div>
                <div class="error" v-if="!$v.document.required">Поле не должно быть пустым.</div>
			</div>
            <div>
				<div class="styled-input wide" :class="{ 'form-group--error': $v.seria.$error }">
					<input type="text" v-model.trim="seria" @input="setSeria($event.target.value)" required />
					<label>Серия</label> 
                    <div class="error" v-if="!$v.seria.minLength">Серия должена содержать 4 цифр.</div>
                    <div class="error" v-if="!$v.seria.maxLength">Серия должена содержать 4 цифр.</div>
                    <div class="error" v-if="!$v.seria.numeric">Используйте цифры.</div>
				</div>
			</div>
			<div>
				<div class="styled-input wide" :class="{ 'form-group--error': $v.nomer.$error }">
					<input type="text" v-model.trim="nomer" @input="setNomer($event.target.value)" required />
					<label>Номер</label> 
                    <div class="error" v-if="!$v.nomer.minLength">Номер должен содержать 6 цифр.</div>
                    <div class="error" v-if="!$v.nomer.maxLength">Номер должен содержать 6 цифр.</div>
                    <div class="error" v-if="!$v.nomer.numeric">Используйте цифры.</div>
				</div>
			</div>
			<div>
				<div class="styled-input wide" :class="{ 'form-group--error': $v.issued.$error }">
					<input type="text" v-model.trim="issued" @input="setIssued($event.target.value)" required />
					<label>Кем выдан</label> 
                    <div class="error" v-if="!$v.issued.alpha">Используйте кирилицу.</div>
				</div>
			</div>
			<div>
				<div class="styled-input wide" :class="{ 'form-group--error': $v.date.$error }">
					<input type="text" v-model.trim="date" @input="setDate($event.target.value)" required />
					<label>Дата выдачи</label>
                    <div class="error" v-if="!$v.date.required">Поле не должно быть пустым.</div>
                    <div class="error" v-else-if="!$v.date.validDate">Дата должна быть в формате ДД.ММ.ГГГГ</div>
				</div>
			</div>
	</div>
</div>
</div>
</template>


<script>
import { required, minLength, maxLength, numeric, alpha } from 'vuelidate/lib/validators';
import moment from 'moment';
export default {
  name: 'app',
   data() {
    return {
      document: '',
      seria: '',
      nomer: '',
      issued: '',
      date: ''
    }
  },
   validations: {
    document: {
        required,
    },
    seria: {
        minLength: minLength(4),
        maxLength: maxLength(4),
        numeric,
    },
    nomer: {
        minLength: minLength(6),
        maxLength: maxLength(6),
        numeric,
    },
    issued: {
        alpha: value => /^[а-яё]*$/i.test(value),
    },
    date: {
      required,
      numeric,
      validDate: value => moment(value, 'DD.MM.YYYY', true).isValid(),
    }
  },
  methods: {
    setDocument(value) {
      this.document = value
      this.$v.document.$touch()
    },
    setSeria(value) {
      this.seria = value
      this.$v.seria.$touch()
    },
    setNomer(value) {
      this.nomer = value
      this.$v.nomer.$touch()
    },
    setIssued(value) {
      this.issued = value
      this.$v.issued.$touch()
    },
    setDate(value) {
      this.date = value
      this.$v.date.$touch()
    }
  }
}

</script>

<style lang="sass" scoped>

h2
  margin-left: 50px
  padding-top: 300px

.selector
  margin-top: -10px
  width: 450px
  height: 80px
  border: 2px solid #c5baba
  border-radius: 4px

select
  width: 150px
  padding: 5px 35px 5px 5px
  font-size: 14px
  width: 440px
  height: 50px
  background: #c5baba
  border-radius: 4px

input
  &:focus ~ label, &:valid ~ label
    margin-left: 12px
    font-size: 12px
    color: rgb(24, 23, 23)
    top: -5px

.styled-input
  float: left
  width: 100px
  margin: 5px
  position: relative
  border-radius: 4px

  label
    color: rgb(27, 26, 26)
    padding: 10px 10px 10px 10px
    position: absolute
    top: 10px
    left: 0
    transition: all 0.25s ease

  &.wide
    float: left
    width: 400px
    max-width: 100%

@media only screen and (max-width: 768px)
  .styled-input
    width: 100%

input
  padding: 20px
  border: 10px
  width: 100%
  font-size: 15px
  background-color: #c5baba
  color: rgb(32, 32, 32)
  border-radius: 4px

.input-container
  width: 400px
  max-width: 100%
  margin: 20px auto 25px auto
</style> 

