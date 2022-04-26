<template>
  <div id="App">
    <div class="container mx-auto">
      <FilterBar
        :parent-data="cityArr"
        :parent-city="currentCity"
        :parent-order-type="orderType"
        @update:city="updateCity"
        @update:order="updateOrder"
      />
      <Pic
        :data="activities"
        :parent-order="orderType"
        :parent-title="currentCity"
      />
    </div>
  </div>
</template>

<script>
import Pic from '@/components/Pic/Pic';
import FilterBar from './components/FilterBar.vue';

export default {
  name: 'App',
  components: {
    Pic,
    FilterBar,
  },
  data() {
    return {
      currentCity: '',
      orderType: 0,
      activities: [],
    };
  },
  async created() {
    await this.getData();
  },
  methods: {
    async getData() {
      try {
        const api = 'https://cloud.culture.tw/frontsite/trans/SearchShowAction.do?method=doFindFestivalTypeJ';
        const res = await this.$http.get(api).catch(err => console.log(err));
        const data = await res.data;
        this.activities = data;
        this.defineNewData();
      } catch (err) {
        console.log(err);
      }
    },
    updateCity(val) {
      this.currentCity = val;
    },
    updateOrder(val) {
      this.orderType = val;
    },
    setCountDown(e_date){
      const targetTime = Date.parse(e_date);
      const now = Date.parse(new Date());
      return Math.ceil( (targetTime - now) / 86400000) ;
    },
    setPlace(){
      return [...new Set(this.activities.map((item) => item.cityName.split('  ')))]
    },
    defineNewData(){
      this.activities.forEach((item,index) => {
        item.countDown = this.setCountDown(item.endTime);
        item.place = this.setPlace()[index];
      });
    }
  },
  computed: {
    cityArr() {
      return [...new Set(this.activities.map((item) => item.place[0]))];
    },
    selectData() {
      if(this.currentCity) {
        return this.activities.filter((item) => item.place[0] === this.currentCity);
      }
      return this.activities;
    },
  },
  
};
</script>

<style>
  body {
    font-family: Arial, Helvetica, "微軟正黑體", sans-serif;
    background-color: #f0ede5;
  }

  body,
  button {
    font-size: 100%;
  }

  .row {
    margin-left: -12px;
    margin-right: -12px;
  }

  .container {
    max-width: 1200px;
  }

  .mx-auto {
    margin-left: auto;
    margin-right: auto;
  }

  .img-resp {
    max-width: 100%;
    height: auto;
    vertical-align: bottom;
  }
</style>
