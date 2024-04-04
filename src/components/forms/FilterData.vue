<script>
  export default {
    name: 'FilterData',
    props: {
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
        <input id="paymentDate" type="date" class="form-control">
      </div>
      <div className="col-2">
        <label for="paymentSource">Источник платежа</label>
        <select id="paymentSource" class="form-select" placeholder="Все источники">
          <option v-for="source in sources" :key="source.id" value="{{ source.id }}">{{ source.title }}</option>
        </select>
      </div>
    </div>
    <hr />
  </form>
</template>

<style>
</style>
