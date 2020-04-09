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
    let chart = am4core.create(this.$refs.chartdiv, am4charts.PieChart);
    // Add and configure Series
    var pieSeries = chart.series.push(new am4charts.PieSeries());
    pieSeries.dataFields.value = "value";
    pieSeries.dataFields.category = "type";

    // Let's cut a hole in our Pie chart the size of 30% the radius
    chart.innerRadius = am4core.percent(30);

    // Put a thick white border around each Slice
    pieSeries.slices.template.stroke = am4core.color("#fff");
    pieSeries.slices.template.strokeWidth = 1;
    pieSeries.slices.template.strokeOpacity = 1;
    pieSeries.slices.template
    // change the cursor on hover to make it apparent the object can be interacted with
    .cursorOverStyle = [
        {
        "property": "cursor",
        "value": "pointer"
        }
    ];

    pieSeries.alignLabels = false;
    pieSeries.labels.template.bent = true;
    pieSeries.labels.template.radius = 3;
    pieSeries.labels.template.padding(0,0,0,0);
    pieSeries.labels.template.fill = am4core.color("#ffffff");


    pieSeries.ticks.template.disabled = true;

    // Create a base filter effect (as if it's not there) for the hover to return to
    var shadow = pieSeries.slices.template.filters.push(new am4core.DropShadowFilter);
    shadow.opacity = 0;

    // Create hover state
    var hoverState = pieSeries.slices.template.states.getKey("hover"); // normally we have to create the hover state, in this case it already exists

    // Slightly shift the shadow and make it more prominent on hover
    var hoverShadow = hoverState.filters.push(new am4core.DropShadowFilter);
    hoverShadow.opacity = 0.7;
    hoverShadow.blur = 5;

    // Add a legend
    chart.legend = new am4charts.Legend();
     chart.legend.labels.template.fill = am4core.color("#fff");
    chart.legend.valueLabels.template.fill = am4core.color("#fff"); 
    chart.data=[];
    var config = {
            headers: {'Access-Control-Allow-Origin': '*'}
        };
        let url='http://192.168.2.34:5000'

        var results =0
        await this.axios.get(url+'/symptoms_pie',config).then((response) => {
            // console.log(response.data)
            results = response.data
            chart.data=results 
        });

        // chart.data = [{
        // "type": "Possui sintomas",
        // "value": 750
        // },{
        // "type": "Não possui sintomas",
        // "value": 150
        // }];
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