<template>
  <div class="hello" ref="chartdiv">
  </div>
</template>

<script>
import * as am4core from "@amcharts/amcharts4/core";
import * as am4charts from "@amcharts/amcharts4/charts";
import am4themes_dataviz from "@amcharts/amcharts4/themes/dataviz";
import am4themes_animated from "@amcharts/amcharts4/themes/animated";

// am4core.useTheme(am4themes_dataviz);
am4core.useTheme(am4themes_animated);


export default {
  name: 'HelloWorld',
  async mounted() {
    let chart = am4core.create(this.$refs.chartdiv, am4charts.XYChart);
    chart.hiddenState.properties.opacity = 0; // this creates initial fade-in

    let url='http://192.168.2.34:5000'
     var config = {
        headers: {'Access-Control-Allow-Origin': '*'}
    };

    var results =0
    await this.axios.get(url+'/by_sex',config).then((response) => {
            // console.log(response.data)
            results = response.data
            console.log(results)
            let i =0
            chart.data = results
        });

    // chart.data = [
    // {
    //     category: "One",
    //     value1: 1,
    //     value2: 5,
    //     value3: 3
    // },
    // {
    //     category: "Two",
    //     value1: 2,
    //     value2: 5,
    //     value3: 3
    // },
    // {
    //     category: "Three",
    //     value1: 3,
    //     value2: 5,
    //     value3: 4
    // },
    // {
    //     category: "Four",
    //     value1: 4,
    //     value2: 5,
    //     value3: 6
    // },
    // {
    //     category: "Five",
    //     value1: 3,
    //     value2: 5,
    //     value3: 4
    // },
    // {
    //     category: "Six",
    //     value1: 2,
    //     value2: 13,
    //     value3: 1
    // }
    // ];


    chart.colors.step = 2;
    chart.padding(30, 30, 10, 30);
    chart.legend = new am4charts.Legend();

    var categoryAxis = chart.xAxes.push(new am4charts.CategoryAxis());
    categoryAxis.dataFields.category = "age";
    categoryAxis.renderer.grid.template.location = 0;
    categoryAxis.renderer.labels.template.fill = am4core.color("#FFFFFF");
    categoryAxis.renderer.labels.template.wrap = true;
    categoryAxis.renderer.labels.template.truncate = true;
    categoryAxis.renderer.labels.template.maxWidth = 120;
    categoryAxis.renderer.minGridDistance=30;
    categoryAxis.renderer.labels.template.tooltipText = "Idade entre: {category}";



    var valueAxis = chart.yAxes.push(new am4charts.ValueAxis());
    valueAxis.min = 0;
    valueAxis.max = 100;
    valueAxis.strictMinMax = true;
    valueAxis.calculateTotals = true;
    valueAxis.renderer.minWidth = 50;
    valueAxis.renderer.labels.template.fill = am4core.color("#FFFFFF");


    var series1 = chart.series.push(new am4charts.ColumnSeries());
    series1.columns.template.width = am4core.percent(80);
    series1.columns.template.tooltipText =
    "{name}: {valueY.totalPercent.formatNumber('#.0')}% \n \
    Qtde de Exames: {valueY.value}";
    series1.name = "Mulher";
    series1.dataFields.categoryX = "age";
    series1.dataFields.valueY = "female";
    series1.dataFields.valueYShow = "totalPercent";
    series1.dataItems.template.locations.categoryX = 0.5;
    series1.stacked = true;
    series1.tooltip.pointerOrientation = "vertical";

    var bullet1 = series1.bullets.push(new am4charts.LabelBullet());
    bullet1.interactionsEnabled = false;
    bullet1.label.text = "{valueY.totalPercent.formatNumber('#.0')}%";
    bullet1.label.fill = am4core.color("#ffffff");
    bullet1.locationY = 0.5;

    var series2 = chart.series.push(new am4charts.ColumnSeries());
    series2.columns.template.width = am4core.percent(80);
    // series2.columns.template.tooltipText =
    // "{name}: {valueY.totalPercent.formatNumber('#.0')}%";
    series2.columns.template.tooltipText =
    "{name}: {valueY.totalPercent.formatNumber('#.0')}% \n \
    Qtde de Exames: {valueY.value}";
    series2.name = "Homem";
    series2.dataFields.categoryX = "age";
    series2.dataFields.valueY = "male";
    series2.dataFields.valueYShow = "totalPercent";
    series2.dataItems.template.locations.categoryX = 0.5;
    series2.stacked = true;
    series2.tooltip.pointerOrientation = "vertical";

    var bullet2 = series2.bullets.push(new am4charts.LabelBullet());
    bullet2.interactionsEnabled = false;
    bullet2.label.text = "{valueY.totalPercent.formatNumber('#.0')}%";
    bullet2.locationY = 0.5;
    bullet2.label.fill = am4core.color("#ffffff");


    chart.scrollbarX = new am4core.Scrollbar();
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