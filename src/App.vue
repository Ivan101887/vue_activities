<template>
  <div id="App">
    <div class="container mx-auto">
      <FilterBar
        :parent-data="cityArr"
        :parent-city="currentCity"
        @update="updateCity"
      />
      <Pic :data="selectData" :parent-title="currentCity" />
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
      activities: [],
    };
  },
  methods: {
    async getData() {
      try {
        const api = 'https://cloud.culture.tw/frontsite/trans/SearchShowAction.do?method=doFindFestivalTypeJ';
        const res = await this.$http.get(api).catch(err => console.log(err));
        const data = await res.data;
        this.activities = data;
      } catch (err) {
        console.log(err);
      }
    },
    updateCity(val) {
      this.currentCity = val;
    },
  },
  computed: {
    cityArr() {
      return [...new Set(this.activities.map((item) => item.cityName.substr(0,3)))];
    },
    selectData() {
      if(this.currentCity) {
        return this.activities.filter((item) => item.cityName.substr(0,3) === this.currentCity);
      }
      return this.activities;
    },
  },
  created() {
    this.getData();
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
