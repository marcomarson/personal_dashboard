<template>
  <div>
    <div class="row">
      <div class="col-12">
        <card type="chart">
          <template slot="header">
            <div class="row">
              <div class="col-sm-6" :class="isRTL ? 'text-right' : 'text-left'">
                <h5 class="card-category">{{$t('dashboard.totalShipments')}}</h5>
                <h2 class="card-title">{{$t('dashboard.performance')}}</h2>
              </div>
              <div class="col-sm-6">
                <div class="btn-group btn-group-toggle"
                     :class="isRTL ? 'float-left' : 'float-right'"
                     data-toggle="buttons">
                  <label v-for="(option, index) in bigLineChartCategories"
                         :key="option"
                         class="btn btn-sm btn-primary btn-simple"
                         :class="{active: bigLineChart.activeIndex === index}"
                         :id="index">
                    <input type="radio"
                           @click="initBigChart(index)"
                           name="options" autocomplete="off"
                           :checked="bigLineChart.activeIndex === index">
                    {{option}}
                  </label>
                </div>
              </div>
            </div>
          </template>
          <div class="chart-area">
            <line-chart style="height: 100%"
                        ref="bigChart"
                        chart-id="big-line-chart"
                        :key="update"
                        :chart-data="bigLineChart.chartData"
                        :gradient-colors="bigLineChart.gradientColors"
                        :gradient-stops="bigLineChart.gradientStops"
                        :extra-options="bigLineChart.extraOptions">
            </line-chart>
          </div>
        </card>
      </div>
    </div>
    <div class="row">
      <div class="col-lg-4 col-md-12">
        <card class="card" :header-classes="{'text-right': isRTL}">
          <h4 slot="header" class="card-title"></h4>
         <div class="chart-area">
            <Pie></Pie>
          </div>
        </card>
      </div>
      
      <div class="col-lg-8 col-md-12">
        <card class="card" :header-classes="{'text-right': isRTL}">
          <h4 slot="header" class="card-title"></h4>
         <div class="chart-area">
            <Stacked></Stacked>
          </div>
        </card>
      </div>
      
    </div>
    <div class="row">
      <div class="col-lg-12 col-md-12">
        <card class="card" :header-classes="{'text-right': isRTL}">
          <h4 slot="header" class="card-title">{{$t('dashboard.simpleTable')}}</h4>
          <div class="table-responsive">
            <user-table :values="tableValues"></user-table>
          </div>
        </card>
      </div>
    </div>
    <div class="row">
      <div class="col-lg-12 col-md-12">
        <card class="card" :header-classes="{'text-right': isRTL}">
          <h4 slot="header" class="card-title"></h4>
         <div class="chart-area">
            <Pyramid></Pyramid>
          </div>
        </card>
      </div>
    </div>
    <div class="row">
      <div class="col-lg-4" :class="{'text-right': isRTL}">
        <card type="chart">
          <template slot="header">
            <h5 class="card-category">{{$t('dashboard.dailySales')}}</h5>
            <h3 class="card-title"> Média da Idade <i class="tim-icons icon-double-right text-info "></i>{{this.blueBarChart.avg}}</h3>
          </template>
          <div class="chart-area">
            <bar-chart style="height: 100%"
                       chart-id="blue-bar-chart"
                       :key="blueBarChart.update"
                       :chart-data="blueBarChart.chartData"
                       :gradient-stops="blueBarChart.gradientStops"
                       :extra-options="blueBarChart.extraOptions">
            </bar-chart>
          </div>
        </card>
      </div>
    </div>
  </div>
</template>
<script>
  import LineChart from '@/components/Charts/LineChart';
  import BarChart from '@/components/Charts/BarChart';
  import * as chartConfigs from '@/components/Charts/config';
  import TaskList from './Dashboard/TaskList';
  import UserTable from './Dashboard/UserTable';
  import Pyramid from './Dashboard/Pyramid';
  import Pie from './Dashboard/Pie';
  import Stacked from './Dashboard/Stacked';
  import config from '@/config';
  export default {
    components: {
      LineChart,
      BarChart,
      TaskList,
      UserTable,
      Loading,
      Pyramid,
      Pie,
      Stacked
    },
    data() {
      return {
        tableValues:[],
        isLoading:true,
        fullPage:true,
        bigLineChart: {
            allData: [
            [7, 12, 11, 5, 3],
            [80, 120, 105, 110, 95, 105, 90, 100, 80, 95, 70, 120],
            [60, 80, 65, 130, 80, 105, 90, 130, 70, 115, 60, 130]
          ],
           labels_name: [
            [7, 12, 11, 5, 3],
            [80, 120, 105, 110, 95, 105, 90, 100, 80, 95, 70, 120],
            [60, 80, 65, 130, 80, 105, 90, 130, 70, 115, 60, 130]
          ],
          activeIndex: 0,
          chartData: null,
          extraOptions: chartConfigs.purpleChartOptions,
          gradientColors: config.colors.primaryGradient,
          gradientStops: [1, 0.4, 0],
          categories: []
        },
        purpleLineChart: {
          extraOptions: chartConfigs.purpleChartOptions,
          chartData: {
            labels: ['JUL', 'AUG', 'SEP', 'OCT', 'NOV', 'DEC'],
            datasets: [{
              label: "Data",
              fill: true,
              borderColor: config.colors.danger,
              borderWidth: 2,
              borderDash: [],
              borderDashOffset: 0.0,
              pointBackgroundColor: config.colors.danger,
              pointBorderColor: 'rgba(255,255,255,0)',
              pointHoverBackgroundColor: config.colors.danger,
              pointBorderWidth: 20,
              pointHoverRadius: 4,
              pointHoverBorderWidth: 15,
              pointRadius: 4,
              data: [80, 100, 70, 80, 120, 80],
            }]
          },
          gradientColors: config.colors.primaryGradient,
          gradientStops: [1, 0.2, 0],
        },
        greenLineChart: {
          extraOptions: chartConfigs.greenChartOptions,
          chartData: {
            labels: ['JUL', 'AUG', 'SEP', 'OCT', 'NOV'],
            datasets: [{
              label: "My First dataset",
              fill: true,
              borderColor: config.colors.danger,
              borderWidth: 2,
              borderDash: [],
              borderDashOffset: 0.0,
              pointBackgroundColor: config.colors.danger,
              pointBorderColor: 'rgba(255,255,255,0)',
              pointHoverBackgroundColor: config.colors.danger,
              pointBorderWidth: 20,
              pointHoverRadius: 4,
              pointHoverBorderWidth: 15,
              pointRadius: 4,
              data: [90, 27, 60, 12, 80],
            }]
          },
          gradientColors: ['rgba(66,134,121,0.15)', 'rgba(66,134,121,0.0)', 'rgba(66,134,121,0)'],
          gradientStops: [1, 0.4, 0],
        },
        blueBarChart: {
          extraOptions: chartConfigs.barChartOptions,
          chartData: {
            labels: ['0-9', '20-29', '30-39', '40-49', '50-59', '70-79'],
            datasets: [{
              label: "Quantidade de Exames",
              fill: true,
              borderColor: config.colors.info,
              borderWidth: 2,
              borderDash: [],
              borderDashOffset: 0.0,
              data: [0, 0, 0, 0, 0, 0],
            }]
          },
          gradientColors: config.colors.primaryGradient,
          gradientStops: [1, 0.4, 0],
          avg:0,
          update:false
        },
        update: false
      }
    },
    computed: {
      enableRTL() {
        return this.$route.query.enableRTL;
      },
      isRTL() {
        return this.$rtl.isRTL;
      },
      bigLineChartCategories() {
        return this.$t('dashboard.chartCategories');
      }
    },
    methods: {
      onCancel() {
        console.log('User cancelled the loader.')
      },  
      initBigChart(index) {
        console.log(this.bigLineChart)
        this.bigLineChart.activeIndex=index;
        let chartData = {
          datasets: [{
            fill: true,
            borderColor: config.colors.primary,
            borderWidth: 2,
            borderDash: [],
            borderDashOffset: 0.0,
            pointBackgroundColor: config.colors.primary,
            pointBorderColor: 'rgba(255,255,255,0)',
            pointHoverBackgroundColor: config.colors.primary,
            pointBorderWidth: 20,
            pointHoverRadius: 4,
            pointHoverBorderWidth: 15,
            pointRadius: 4,
            data: this.bigLineChart.allData[index],
            label:"Quantidade de Exames"
          }],
          labels: this.bigLineChart.labels_name[index]
        }
        this.bigLineChart.chartData=chartData;
        
        this.$refs.bigChart.updateGradients(this.bigLineChart.chartData);
      },
      getDataBigChart(){
        var config = {
          headers: {'Access-Control-Allow-Origin': '*'}
        };
        let url='http://192.168.2.34:5000'
        this.axios.get(url+'/exams_by_date',config).then((response) => {
          let result = response.data;
          let ajuste=false;
          
          if (  JSON.stringify(this.bigLineChart.allData[0]) !== JSON.stringify(result['by_day'].code)){
             this.bigLineChart.allData[0]=result['by_day'].code;
            this.bigLineChart.labels_name[0]=result['by_day'].day;
            ajuste=true;    
          }
           if (  JSON.stringify(this.bigLineChart.allData[1]) !== JSON.stringify(result['by_week'].code)){
            this.bigLineChart.allData[1]=result['by_week'].code;
            this.bigLineChart.labels_name[1]=result['by_week'].week_of_month;

            ajuste=true;    
          }
           if (  JSON.stringify(this.bigLineChart.allData[2]) !== JSON.stringify(result['by_month'].code)){
            this.bigLineChart.allData[2]=result['by_month'].code; 
            this.bigLineChart.labels_name[2]=result['by_month'].month;
   
            ajuste=true;
          }
          if(ajuste==true){
           this.updatePlot()
           this.isLoading = false;
          }
          
        });
        
      },
      getDataAgeCategory(){
        var config = {
          headers: {'Access-Control-Allow-Origin': '*'}
        };
        let url='http://192.168.2.34:5000'
        this.axios.get(url+'/exams_by_age_category',config).then((response) => {
          let result = response.data
          if (JSON.stringify(this.blueBarChart.chartData.datasets[0].data) !== JSON.stringify(result.count)){
            this.blueBarChart.chartData.labels = result.age_category;
            this.blueBarChart.chartData.datasets[0].data = result.count;
            this.blueBarChart.avg = result.avg;
             this.blueBarChart.update = !this.blueBarChart.update
          } 
        });       
      },
    getTable(){
        var config = {
          headers: {'Access-Control-Allow-Origin': '*'}
        };
        let url='http://192.168.2.34:5000'
        this.axios.get(url+'/table1',config).then((response) => {
          let result = response.data
          this.tableValues=response.data;
          
        });       
      },
    updatePlot(){
      let chartData = {
          datasets: [{
            fill: true,
            borderColor: config.colors.primary,
            borderWidth: 2,
            borderDash: [],
            borderDashOffset: 0.0,
            pointBackgroundColor: config.colors.primary,
            pointBorderColor: 'rgba(255,255,255,0)',
            pointHoverBackgroundColor: config.colors.primary,
            pointBorderWidth: 20,
            pointHoverRadius: 4,
            pointHoverBorderWidth: 15,
            pointRadius: 4,
            data: this.bigLineChart.allData[this.bigLineChart.activeIndex],
            label:"Quantidade de Exames"
          }],
          labels: this.bigLineChart.labels_name[this.bigLineChart.activeIndex]
        }
        this.bigLineChart.chartData=chartData;
      this.update = !this.update
     
    }
    },
    beforeCreate(){
      this.isLoading = true;
      this.interval = setInterval(() => this.getDataBigChart(), 1000000);
       this.interval2 = setInterval(() => this.getDataAgeCategory(), 500000);
       
    },
    mounted() {
      this.i18n = this.$i18n;
      if (this.enableRTL) {
        this.i18n.locale = 'en';
        this.$rtl.enableRTL();
      }
      this.initBigChart(0);
      this.getDataAgeCategory();
      this.getTable();

      this.getDataBigChart();
      },
    beforeDestroy() {
      if (this.$rtl.isRTL) {
        this.i18n.locale = 'en';
        this.$rtl.disableRTL();
      }
    }
  };
</script>
<style>
</style>
