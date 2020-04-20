<template>
  <div class="home">
    <div class="search">
      <van-row>
        <van-col span="19">
          <van-button class="date" @click="onShowSearchForDate">riqi</van-button>
        </van-col>
        <van-col span="5"><van-button type="primary" @click="showFilterEvent">筛选</van-button></van-col>
      </van-row>
    </div>
    <div class="schedule">
      <table  cellspacing="0">
        <thead>
          <tr>
            <th>团队</th>
            <th>姓名</th>
            <th>日期</th>
          </tr>
        </thead>
        <tbody>
          <tr @click="goDetail">
            <td>生产调度</td>
            <td>张三</td>
            <td>2020-4-10</td>
          </tr>
          <tr>
            <td>生产调度</td>
            <td>张三</td>
            <td>2020-4-10</td>
          </tr>
          <tr>
            <td>生产调度</td>
            <td>张三</td>
            <td>2020-4-10</td>
          </tr>
        </tbody>
      </table>
    </div>

    <SearchForDate ref="searchForDate" @filterData="filterDataEvent"></SearchForDate>
    <my-filter ref="filterComp"  @filterData="filterDataEvent"></my-filter>
    
  </div>
</template>
<style>
  .home {
    font-size: 0.4rem;
  }
  .home .search .van-button {
    width: 100%;
    height: 1rem;
    line-height: 1rem;
  }
  .home .search .date {
    text-align: left;
  }
  /* .search .schedule {} */
  .home .schedule table{
    width: 100%;
  }
  table th {
    line-height: 1rem;
    font-size: 0.4rem;
  }
  table td {
    line-height: 0.8rem;
  }
  table tr:nth-child(odd) td{
    background-color:#F5F5F5;
  }
</style>
<script>
// @ is an alias to /src
import { Button, Col, Row, Popup   } from 'vant';
import SearchForDate from "../components/SearchForDate";
import Filter from "../components/Filter";
export default {
  name: 'Home',
  components: {
    [Button.name]: Button,
    [Col.name]: Col,
    [Row.name]: Row,
    [Popup.name]: Popup,
    SearchForDate,
    MyFilter: Filter
  },
  data() {
    return {
      showSearch: false,
      showFilter: false
    }
  },
  methods:{
    onHideFilter() {
      this.showFilter = false;
    },
    showFilterEvent() {
      this.showFilter = true;
      this.$refs.filterComp.showFilter();
    },
    onShowSearchForDate() {
      this.$refs.searchForDate.showPopup();
    },
    filterDataEvent(obj) {
      console.log(obj)
    },
    goDetail() {
      this.$router.push("/detail")
    }
  }
}
</script>
