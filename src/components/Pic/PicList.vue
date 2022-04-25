<template>
  <ul class="pic__ls row">
    <li class="pic__item" :key="item.actid" v-for="item in data">
      <PicItem :item="item" v-bind="$attrs"/>
    </li>
  </ul>
</template>

<script>
import PicItem from '@/components/Pic/PicItem';

export default {
  inheritAttrs: false,
  name: 'PicList',
  props: {
    data: {
      type: Array,
      required: true,
    },
  },
  components: {
    PicItem,
  },
};
</script>


<style>

.pic__ls {
  padding-left: 0;
  margin-top: 0;
  list-style-type: none;
  display: flex;
  flex-wrap: wrap;
}

</style>
