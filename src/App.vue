<template>
  <div id="app">
    <ClientForm />
    <AdressForm />
    <PassportForm />
  </div>
</template>

<script>
import ClientForm from '@/components/clientForm.vue';
import AdressForm from '@/components/adressForm.vue';
import PassportForm from '@/components/passportForm.vue';

export default {
  name: 'App',
  components: {
    ClientForm,
    AdressForm,
    PassportForm
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
