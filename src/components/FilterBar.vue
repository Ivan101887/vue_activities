<template>
  <section class="filterBar">
    <div class="filter">
      <div class="filter__head">地區:</div>
      <ul class="filter__body">
        <li
          :class="['filter__item', { 'filter__item--active': !parentCity }]"
          @click="$emit('update:city', '')"
        >
          全部
        </li>
        <li
          :class="[
            'filter__item',
            { 'filter__item--active': parentCity === item }
          ]"
          @click="$emit('update:city', item)"
          v-for="item in parentData"
          :key="item"
        >
          {{ item }}
        </li>
      </ul>
    </div>
    <div class="filter">
      <div class="filter__head">排序:</div>
      <ul class="filter__body">
        <li
          :class="['filter__item', { 'filter__item--active': !parentOrderType }]"
          @click="$emit('update:order', 0)"
        >
          倒數時間由近到遠
        </li>
        <li
          :class="[
            'filter__item',
            { 'filter__item--active': parentOrderType === 1 }
          ]"
          @click="$emit('update:order', 1)"
        >
          倒數時間由遠到近
        </li>
      </ul>
    </div>
  </section>
</template>
<script>
export default {
  name: "filter-bar",
  props: {
    parentData: Array,
    parentCity: String,
    parentOrderType: Number,
  },
}
</script>
<style scoped>
  .filterBar {
    margin-top: 10px;
    padding: 15px;
    background-color: #fff;
  }
  .filter {
    display: flex;
    align-items: center;
  }
  .filter + .filter {
    margin-top: 15px;
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