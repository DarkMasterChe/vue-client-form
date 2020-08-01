<template>
<div>
<div class="container">
	<div class="row">
			<h2 style="text-align:center">Создание нового клиента</h2>
	</div>
	<div class="row input-container">
			<div>
				<div class="styled-input wide" :class="{ 'form-group--error': $v.secondname.$error }">
					<input type="text" v-model.trim="secondname" @input="setSecondname($event.target.value)"  required />
					<label>Фамилия</label> 
				</div>
        <div class="error" v-if="!$v.secondname.required">Поле не должно быть пустым.</div>
        <div class="error" v-else-if="!$v.secondname.alpha">Используйте кирилицу.</div>
			</div>
			<div>
				<div class="styled-input wide " :class="{ 'form-group--error': $v.name.$error }">
					<input type="text" v-model.trim="name" @input="setName($event.target.value)" required />
					<label>Имя</label> 
				</div>
         <div class="error" v-if="!$v.name.required">Поле не должно быть пустым.</div>
        <div class="error" v-else-if="!$v.name.alpha">Используйте кирилицу.</div>
			</div>
			<div>
				<div class="styled-input wide" :class="{ 'form-group--error': $v.thirdname.$error }">
					<input type="text" v-model.trim="thirdname" @input="setThirdname($event.target.value)" required />
					<label>Отчество</label> 
          <div class="error" v-if="!$v.thirdname.alpha">Используйте кирилицу.</div>
				</div>
			</div>
			<div>
				<div class="styled-input wide " :class="{ 'form-group--error': $v.date.$error }">
					<input type="text" :value="date" @input="setDate($event.target.value)" required>
          <label>Дата рождения</label> 
				</div>
          <div class="error" v-if="!$v.date.required">Поле не должно быть пустым.</div>
          <div class="error" v-else-if="!$v.date.validDate">Дата должна быть в формате ДД.ММ.ГГГГ</div>
			</div>
      <div>
				<div class="styled-input wide" :class="{ 'form-group--error': $v.phone.$error }">
					<input type="text" :value="phone" @input="setPhone($event.target.value)" required />
					<label>Номер телефона</label>
				</div>
          <div class="error" v-if="!$v.phone.minLength">Номер должен содержать 11 цифр.</div>
          <div class="error" v-if="!$v.phone.maxLength">Номер должен содержать 11 цифр.</div>
          <div class="error" v-if="!$v.phone.numeric">Используйте цифры.</div>
          <div class="error" v-else-if="!$v.phone.mustBePhone">Номер должен начинаться с 7.</div>
			</div>
      <div>
				<div class="styled-input wide" :class="{ 'form-group--error': $v.pol.$error }">
					<input type="text"  v-model.trim="pol" @input="setPol($event.target.value)" required/>
					<label>Пол</label>
				</div>
        <div class="error" v-if="!$v.pol.alpha">Используйте кирилицу.</div>
			</div>
      <div>
        <span class="left"></span>
          <div class="selector">
            <span class="left">Группа клиентов</span>
            <div class="styled-input wide" :class="{ 'form-group--error': $v.clients.$error }">
                <select id="clientgroup" v-model.trim="clients" @input="setClients($event.target.value)" required>  
                  <option value="VIP">VIP</option>
                  <option value="P">Проблемные</option>
                  <option value="OMS">ОМС</option>
                </select>
            </div>
          </div>
          <div class="error" v-if="!$v.clients.required">Поле не должно быть пустым.</div>
			</div>
      <div>
        <span class="left"></span>
          <div class="selector">
            <span class="left">Лечащий врач</span>
            <div class="styled-input wide">
                <select id="clientgroup" value="group">
                  <option value="ivanov">Иванов</option>
                  <option value="zaharov">Захаров</option>
                  <option value="chernushova">Чернышева</option>
                </select>
            </div>
          </div>
			</div>
      <div class="checkbox">
        <label>
          Не отправлять СМС
        </label>
        <input type="checkbox" value="true">
      </div>
			
	</div>
</div>
</div>
</template>

<script>
import { required, minLength, maxLength, numeric, alpha } from 'vuelidate/lib/validators';
import moment from 'moment';
const mustBePhone = (value) => value.indexOf('7') == 0;

export default {
  name: 'ClientForm',
   data() {
    return {
      name: '',
      secondname: '',
      thirdname: '',
      date: '',
      phone: '',
      pol: '',
      clients: ''
    }
  },
   validations: {
    name: {
      required,
      minLength: minLength(4),
      alpha: value => /^[а-яё]*$/i.test(value),
    },
    secondname: {
      required,
      minLength: minLength(4),
      alpha: value => /^[а-яё]*$/i.test(value),
    },
    thirdname: {
      minLength: minLength(4),
      alpha: value => /^[а-яё]*$/i.test(value),
    },
    phone: {
      required,
      minLength: minLength(11),
      maxLength: maxLength(11),
      numeric,
      mustBePhone
    },
    date: {
      required,
      numeric,
      validDate: value => moment(value, 'DD.MM.YYYY', true).isValid(),
    },
    pol: {
      alpha: value => /^[а-яё]*$/i.test(value),
    },
    clients: {
      required
    }
  },
  methods: {
    setName(value) {
      this.name = value
      this.$v.name.$touch()
    },
    setSecondname(value) {
      this.secondname = value
      this.$v.secondname.$touch()
    },
    setThirdname(value) {
      this.thirdname = value
      this.$v.thirdname.$touch()
    },
    setPhone(value) {
      this.phone = value
      this.$v.phone.$touch()
    },
   setDate(value) {
      this.date = value
      this.$v.date.$touch()
    },
    setPol(value) {
      this.pol = value
      this.$v.pol.$touch()
    },
    setClients(value) {
      this.clients = value
      this.$v.clients.$touch()
    }
  }
}
</script>

<style lang="sass" scoped>

.checkbox
  margin-top: 8px
  width: 450px
  height: 40px
  border: 2px solid #c5baba
  border-radius: 4px

.left
  margin-right: 320px

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

@media screen and (min-width: 0\0 )
  select
    background: none\9
    padding: 5px\9

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

