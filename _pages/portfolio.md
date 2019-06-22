---
layout: single
permalink: /portfolio/
title: "Portfolio"
author_profile: true
---

To keep momentum and visualize my progress, I track my monthly nett worth and over the years my strategy has evolved to something fairly passive which doesn't require a lot of thinking anymore. Therefor, most of what I own is in ETF's and looks like this:

**Emergency Fund** 
* 3 months living expenses

**Retirement** 
* Momentum - Investo Retirement Annuity
* Investec - iSelect Preservation Pension Plan
* Investec - iSelect Preservation Provident Fund

**Tax Free Savings Account** 
* Easy Equities - Sygnia Itrix MSCI World ETF

**Other**
* Binance - Crypto 
* Property - Cape Town 



<!-- Styles -->
<style>
#chartdiv {
  width: 100%;
  height: 500px;
}

</style>

<!-- Resources -->
<script src="https://www.amcharts.com/lib/4/core.js"></script>
<script src="https://www.amcharts.com/lib/4/charts.js"></script>
<script src="https://www.amcharts.com/lib/4/themes/animated.js"></script>

<!-- Chart code -->
<script>
am4core.ready(function() {

// Themes begin
am4core.useTheme(am4themes_animated);
// Themes end

// Create chart instance
var chart = am4core.create("chartdiv", am4charts.PieChart);

// Add data

chart.data = [ {
  "Category": "Emergency Fund",
  "Percentage": 2.19
}, {
  "Category": "Retirement",
  "Percentage": 37.14
}, {
  "Category": "TFSA",
  "Percentage": 4.94
}, {
  "Category": "Other",
  "Percentage": 55.73
} ];

// Add and configure Series
var pieSeries = chart.series.push(new am4charts.PieSeries());
pieSeries.dataFields.value = "Percentage";
pieSeries.dataFields.category = "Category";
pieSeries.slices.template.stroke = am4core.color("#FFFFFF");
pieSeries.slices.template.strokeWidth = 2;
pieSeries.slices.template.strokeOpacity = 1;

// This creates initial animation
pieSeries.hiddenState.properties.opacity = 1;
pieSeries.hiddenState.properties.endAngle = -90;
pieSeries.hiddenState.properties.startAngle = -90;

}); // end am4core.ready()
</script>

<!-- HTML -->
<div id="chartdiv"></div>


