<script>
  import axios from 'axios'
  import FilterData from './components/forms/FilterData.vue'
  import PaymentList from './components/PaymentList.vue'

  export default {
    components: { FilterData, PaymentList },
    data () {
      return {
        payments: null,
        sources: null
      }
    },
    methods: {
      fetchPayments (date = '', id = '') {
        const source_id = id === 'Все источники' ? '' : id;
        const searchParams = new URLSearchParams({
          source_id,
          date: date
        });
        axios.get(`https://tests.szapi.ru/ts16/public_html/payments?${searchParams}`)
          .then((res) => this.payments = res.data)
      },
      fetchSources () {
        axios.get('https://tests.szapi.ru/ts16/public_html/sources')
          .then((res) => this.sources = res.data)
      }
    },
    created() {
      this.fetchPayments();
      this.fetchSources();
    }
  }
</script>

<template>
  <div className="container-lg">
    <h3>Cписок платежей</h3>
    <button className="btn btn-primary">Добавить платеж</button>
    <FilterData v-bind:fetchPayments="fetchPayments" v-bind:payments="payments" v-bind:sources = "sources" />
    <PaymentList v-bind:payments="payments" />
  </div>
</template>

<style>
</style>
