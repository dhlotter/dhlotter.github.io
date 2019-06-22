---
layout: single
permalink: /portfolio/
title: "Portfolio"
author_profile: true
---

To keep momentum and visualize my progress, I track my monthly nett worth and over the years my strategy has evolved to something fairly passive which doesn't require a lot of thinking anymore. Therefor, most of what I own is in ETF's and looks like this:

<html lang="en-US">
<body>
<div id="piechart"></div>
<script type="text/javascript" src="https://www.gstatic.com/charts/loader.js"></script>
<script type="text/javascript">
// Load google charts
google.charts.load('current', {'packages':['corechart']});
google.charts.setOnLoadCallback(drawChart);
// Draw the chart and set the chart values
function drawChart() {
  var data = google.visualization.arrayToDataTable([
  ['Fund', 'Percentage'],
  ['Emergency Fund', 2.19],
  ['Retirement', 37.14],
  ['TFSA', 4.94],
  ['Other',  55.73]
]);
  // Optional; add a title and set the width and height of the chart
  var options = {'title':'My Average Day', 'width':550, 'height':400};
  // Display the chart inside the <div> element with id="piechart"
  var chart = new google.visualization.PieChart(document.getElementById ('piechart'));
  chart.draw(data, options);
}
</script>
</body>
</html>


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


