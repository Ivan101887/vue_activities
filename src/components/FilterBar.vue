<template>
  <section class="filter">
    <div class="filter__head">地區:</div>
    <ul class="filter__body">
      <li
        :class="['filter__item', { 'filter__item--active': !parentCity }]"
        @click="$emit('update', '')"
      >
        全部
      </li>
      <li
        :class="[
          'filter__item',
          { 'filter__item--active': parentCity === item }
        ]"
        @click="$emit('update', item)"
        v-for="item in parentData"
        :key="item"
      >
        {{ item }}
      </li>
    </ul>
  </section>
</template>
<script>
export default {
  name: "filter-bar",
  props: {
    parentData: Array,
    parentCity: String,
  },
}
</script>
<style scoped>
  .filter {
    display: flex;
    margin-top: 10px;
    padding: 15px;
    background-color: #fff;
  }
  .filter__head {
    white-space: nowrap;
    padding: 25px 20px;
    border-right: 3px solid #ddd;
  }
  .filter__body {
    padding-left: 10px;
    margin-top: 0;
    margin-bottom: 0;
    display: flex;
    flex-wrap: wrap;
  }
  .filter__item {
    list-style: none;
    margin-left: 10px;
    margin-right: 10px;
    margin: 5px 10px;
    cursor: pointer;
  }
  .filter__item--active {
    color: #cc0000;
  }
</style>