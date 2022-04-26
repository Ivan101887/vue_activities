<template>
    <div class="filter">
      <div class="filter__head">{{parentTitle}}:</div>
      <ul class="filter__body">
        <li
          :class="[
            'filter__item',
            { 'filter__item--active': parentIndex === index}
          ]"
          v-for="(item,index) in parentData"
          :key="item"
          @click="$emit('update', index)"
        >
          {{ item }}
        </li>
      </ul>
    </div>
</template>
<script>
export default {
  inheritAttrs: false,
  name: "filter-bar",
  props: {
    parentTitle: String,
    parentData: Array,
    parentIndex: Number,
    parentOrderType: Number,
  },
}
</script>
<style scoped>
  
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