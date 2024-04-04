<script>
  import axios from 'axios'
  export default {
    name: 'PaymentList',
    data () {
      return {
        sources: null,
        types: null,
        statuses: null,
      }
    },
    props: {
      payments: {
        type: Array,
      },
    },
    methods: {
      findTitle (arr, id) {
        const item = arr.find((i) => i.id === id);
        return item.title;
      },
      getStatusTitleClass (id) {
        const backgrounds = {
          1: 'bg-danger',
          2: 'bg-warning',
          3: 'bg-success',
        };
        return `badge ${backgrounds[id]}`;
      }
    },
    created () {
      axios.get('https://tests.szapi.ru/ts16/public_html/form_tss')
        .then((res) => {
          this.sources = res.data.sources;
          this.types = res.data.types;
          this.statuses = res.data.statuses;
        })
    }
  }
</script>

<template>
  <table class="table table-hover">
    <thead>
      <tr>
        <th scope="col">Клиент</th>
        <th scope="col">Договор</th>
        <th scope="col">Тип платежа</th>
        <th scope="col">Дата</th>
        <th scope="col">Сумма (руб.)</th>
        <th scope="col">Источник платежа</th>
        <th scope="col">Статус</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(payment, index) in payments" :key="index">
        <td>{{ payment.client }}</td>
        <td>{{ payment.contract }}</td>
        <td>{{ findTitle(types, payment.type_id) }}</td>
        <td>{{ payment.date }}</td>
        <td>{{ payment.summ }}</td>
        <td>{{ findTitle(sources, payment.source_id) }}</td>
        <td><span className="badge" :class="getStatusTitleClass(payment.status_id)">{{ findTitle(statuses, payment.status_id) }}</span></td>
      </tr>
    </tbody>
  </table>
</template>