<script>
  export default {
    name: 'FilterData',
    data () {
      return {
        date: '',
        id: '',
      }
    },
    props: {
      fetchPayments: {
        type: Function,
      },
      payments: {
        type: Array,
      },
      sources: {
        type: Array,
      }
    }
  }
</script>
<template>
  <form>
    <div className="mt-3 row">
      <div className="col-2">
        <label for="paymentDate">Дата платежа:</label>
        <input id="paymentDate" type="date" class="form-control" v-model="date" @input="fetchPayments(date, id)">
      </div>
      <div className="col-2">
        <label for="paymentSource">Источник платежа</label>
        <select id="paymentSource" class="form-select" v-model="id" :onSelect="fetchPayments(date, id)">
          <option selected>Все источники</option>
          <option v-for="source in sources" :key="source.id" :value="source.id">{{ source.title }}</option>
        </select>
      </div>
    </div>
    <hr />
  </form>
</template>

<style>
</style>
