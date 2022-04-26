<template>
  <div id="App">
    <div class="container mx-auto">
      <section class="filterBar">
        <FilterBar
          parent-title="地區"
          :parent-data="cityArr"
          :parent-index="index.city"
          @update="updateCity"
        />
        <FilterBar
          parent-title="排序"
          :parent-data="['倒數時間由近到遠', '倒數時間由遠到近']"
          :parent-index="index.order"
          @update="updateOrder"
        />
      </section>

      <Pic
        :data="selectData"
        :parent-order="index.order"
        :parent-title="cityArr[index.city]"
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
      index: {
        city: 0,
        order: 0,
      },
      currentCity: '全部',
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
      this.index.city = val;
      this.currentCity = this.cityArr[val];
    },
    updateOrder(val) {
      this.index.order = val;
    },
    setCountDown(e_date){
      const targetTime = Date.parse(e_date);
      const now = Date.parse(new Date());
      return Math.ceil( (targetTime - now) / 86400000) ;
    },
    setPlace(){
      return [...new Set(this.activities.map((item) => item.cityName.split(/\s+/g)))]
    },
    defineNewData(){
      this.activities.forEach((item,index) => {
        item.countDown = this.setCountDown(item.endTime);
        item.place = this.setPlace()[index];
      });
    },
    sortData(arr){
      if(this.index.order === 0) {
        return arr.sort( (a,b) => a.countDown - b.countDown );
      }
      return arr.sort( (a,b) => b.countDown - a.countDown );
    }
  },
  computed: {
    cityArr() {
      const arr = [...new Set(this.activities.map((item) => item.place[0]))];
      arr.unshift('全部')
      return arr;
    },
    selectData() {
      let arr = [];
      this.currentCity === '全部'
        ?arr = this.activities
        :arr = this.activities.filter((item) => item.place[0] === this.currentCity);
      return this.sortData(arr)
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

  .filterBar {
    margin-top: 10px;
    padding: 15px;
    background-color: #fff;
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
