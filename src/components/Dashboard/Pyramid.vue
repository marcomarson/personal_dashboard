<template>
  <div class="hello" ref="chartdiv">
  </div>
</template>

<script>
import * as am4core from "@amcharts/amcharts4/core";
import * as am4charts from "@amcharts/amcharts4/charts";
import am4themes_animated from "@amcharts/amcharts4/themes/animated";

am4core.useTheme(am4themes_animated);


export default {
  name: 'HelloWorld',
  async mounted() {
    let chart = am4core.create(this.$refs.chartdiv, am4charts.XYChart);

    chart.paddingRight = 20;

    let data = [];
    let visits = 10;

    var config = {
        headers: {'Access-Control-Allow-Origin': '*'}
    };
    let url='http://192.168.2.34:5000'

    var results =0
    await this.axios.get(url+'/exams_by_day',config).then((response) => {
        // console.log(response.data)
        results = response.data
        // console.log(results)
        let i =0
        for (let index in results) {
            // let this_data =  result.begintime.split("-")
            data.push({ date:new Date(results[index].begintime), name: "name" + i, value:results[index].code });
            i=i+1
        }
    });
    // console.log("DATA -> "+data)
    // console.log(data[0])

    // let i =0
    // for (result in results) {
    //   data.push({ date:results.begintime, name: "name" + i, value:result.code });
    //   i=i+1
    // }

    chart.data = data;

    let dateAxis = chart.xAxes.push(new am4charts.DateAxis());
    dateAxis.renderer.grid.template.location = 0;
    dateAxis.renderer.grid.template.stroke = am4core.color("#A0CA92");
    dateAxis.renderer.labels.template.fill = am4core.color("#FFFFFF");

    let valueAxis = chart.yAxes.push(new am4charts.ValueAxis());
    valueAxis.tooltip.disabled = true;
    valueAxis.renderer.minWidth = 35;
    valueAxis.renderer.labels.template.fill = am4core.color("#FFFFFF");
    valueAxis.renderer.grid.template.stroke = am4core.color("#A0CA92");

    let series = chart.series.push(new am4charts.LineSeries());
    series.dataFields.dateX = "date";
    series.dataFields.valueY = "value";
    series.tooltipText=
    "Qtde de Exames: {valueY.value}";

    // series.tooltipText = "{valueY.value}";
    chart.cursor = new am4charts.XYCursor();

    let scrollbarX = new am4charts.XYChartScrollbar();
    scrollbarX.series.push(series);
    chart.scrollbarX = scrollbarX;

    this.chart = chart;
  },

  beforeDestroy() {
    if (this.chart) {
      this.chart.dispose();
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.hello {
  width: 100%;
  height: 500px;
}
</style>