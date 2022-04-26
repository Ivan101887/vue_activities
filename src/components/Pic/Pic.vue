<template>
  <div class="pic">
    <div class="pic__head">
      <h3>{{ parentTitle ? parentTitle : "全部" }}</h3>
    </div>
    <div class="pic__body">
      <PicList :data="sortData" :parent-is-show="parentTitle === ''" />
    </div>
  </div>
</template>

<script>
import PicList from '@/components/Pic/PicList';

export default {
  name: 'Pic',
  props: {
    data: {
      type: Array,
      required: true,
    },
    parentTitle: String,
    parentOrder: Number
  },
  components: {
    PicList,
  },
  computed: {
    sortData(){
      if(this.parentOrder === 0) {
        return this.data.sort( (a,b) => a.countDown - b.countDown );
      }
      return this.data.sort( (a,b) => b.countDown - a.countDown );
    }
  }
};
</script>


<style>
  .pic__head h3 {
    padding-left: 12px;
    margin-bottom: 12px;
    line-height: 1;
    font-size: 1.5rem;
    border-left: solid 5px rgb(204, 0, 0);
  }
</style>
