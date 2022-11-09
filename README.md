# 차트 라이브러리 3가지
-------------------------------
* chartjs
```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/2.9.4/Chart.js"></script>

<body>
<h1>2022 삼성전자 주가</h1>
<canvas id="Chart1" style="width:100%;max-width:600px"></canvas>


<script>
var xValues = [1,2,3,4,5,6,7,8,9,10,11];
var yValues = [78600, 73300, 71700, 69100, 67300, 66700, 56200, 61300, 58400, 55200, 60000];

new Chart("Chart1", {
  type: "line",
  data: {
    labels: xValues,
    datasets: [{
      fill: true,
      lineTension: 0,
      backgroundColor: "rgba(0,0,255,1.0)",
      borderColor: "rgba(0,0,255,0.1)",
      data: yValues
    }]
  },
  options: {
    legend: {display: false},
    scales: {
      yAxes: [{ticks: {min: 10000, max:90000}}],
    }
  }
});
</script>


</body>
```

* echart
```html
<script src="https://cdn.jsdelivr.net/npm/echarts@5.4.0/dist/echarts.min.js"></script>
</head>
<body>
<!-- 높이와 너비가 지정된 Dom 을 생성합니다 -->
<div id="main" style="width: 600px;height:400px;"></div>
    <script type="text/javascript">
        // DOM을 준비하고 echart 객체를 만듭니다.
        var myChart = echarts.init(document.getElementById('main'));

        // 차트 속성과 데이터를 지정합니다.
        var option = {
            title: {
            	text: '2022 삼성전자 주가'
            },
            tooltip: {},
            legend: {
            	data:['Stock']
            },
            xAxis: {
            	data: ["1월","2월","3월","4월","5월","6월","7월","8월","9월","10월","11월",]
            },
            yAxis: {},
            series: [{
                name: 'Stock',
                type: 'bar',
                data: [78600, 73300, 71700, 69100, 67300, 66700, 56200, 61300, 58400, 55200, 60000]
            }]
        };

        // 위에서 설정한 속성을 차트에 반영합니다.
        myChart.setOption(option);
    </script>
    </body>
```
  
  
  
  
  
  
* D3
```html
<script src="https://d3js.org/d3.v4.min.js"></script>
<body>
<svg width="600" height="500"></svg>
<script>

    var svg = d3.select("svg"),
        margin = 200,
        width = svg.attr("width") - margin,
        height = svg.attr("height") - margin

    svg.append("text")
       .attr("transform", "translate(100,0)")
       .attr("x", 50)
       .attr("y", 50)
       .attr("font-size", "24px")
       .text("2022 삼성전자 주가")

    var xScale = d3.scaleBand().range([0, width]).padding(0.4),
        yScale = d3.scaleLinear().range([height, 0]);

    var g = svg.append("g")
               .attr("transform", "translate(" + 100 + "," + 100 + ")");

    d3.csv("XYZ.csv", function(error, data) {
        if (error) {
            throw error;
        }

        xScale.domain(data.map(function(d) { return d.month; }));
        yScale.domain([0, d3.max(data, function(d) { return d.value; })]);

        g.append("g")
         .attr("transform", "translate(0," + height + ")")
         .call(d3.axisBottom(xScale))
         .append("text")
         .attr("y", height - 250)
         .attr("x", width - 100)
         .attr("text-anchor", "end")
         .attr("stroke", "black")
         .text("month");

        g.append("g")
         .call(d3.axisLeft(yScale).tickFormat(function(d){
             return "₩" + d;
         })
         .ticks(10))
         .append("text")
         .attr("transform", "rotate(-90)")
         .attr("y", 6)
         .attr("dy", "-5.1em")
         .attr("text-anchor", "end")
         .attr("stroke", "black")
         .text("Stock Price");

        g.selectAll(".bar")
         .data(data)
         .enter().append("rect")
         .attr("class", "bar")
         .attr("x", function(d) { return xScale(d.month); })
         .attr("y", function(d) { return yScale(d.value); })
         .attr("width", xScale.bandwidth())
         .attr("height", function(d) { return height - yScale(d.value); });
    });
</script>
</body>
```

* github.io: <https://aestura.github.io/Aestura1.gitnub.io/>

