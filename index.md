<!DOCTYPE html>
<html>

<head>

<meta charset="utf-8">



<style>


    body {

        font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;

        width: 960px;

        height: 500px;

        position: relative;

    }


    svg {

        width: 100%;

        height: 100%;

        position: center;

    }
    
    b {
        color: #00c8ff;
        stroke: #00efff;
    }
    



    .toolTip {

        font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;

        position: absolute;

        display: none;

        width: auto;

        height: auto;

        background: none repeat scroll 0 0 white;

        border: 0 none;

        border-radius: 8px 8px 8px 8px;

        box-shadow: -3px 3px 15px #888888;

        color: black;

        font: 12px sans-serif;

        padding: 5px;

        text-align: center;

    }



    



</style>


</head>



<body>

<b>105年 交通事故發生件數</b>


<script src="http://d3js.org/d3.v3.min.js"></script>

<script>


    data = [
                       { label: "1月", value: 26398 },

                       { label: "2月", value: 21555 },

                       { label: "3月", value: 25242 },

                       { label: "4月", value: 23685 },

                       { label: "5月", value: 24149 },

                       { label: "6月", value: 23489 },

                       { label: "7月", value: 24294 },

                       { label: "8月", value: 23753 },

                       { label: "9月", value: 22106 },

                       { label: "10月", value: 22323 },

                       { label: "11月", value: 23544 },

                       { label: "12月", value: 24838 },
                   ];



    var div = d3.select("body").append("div").attr("class", "toolTip");



    var svg_height = 500;
    var svg_width = 960;


    //scale need it
    var max = d3.max(data, function (d) { return d.value; });



    svg = d3.select('body')

                      .append("svg")

                      .attr("width", svg_width)

                      .attr("height", svg_height);




    bar = svg.selectAll("g")

                      .data(data)

                      .enter()

                      .append("g");











    bar.append("rect")

                     .attr("x", function (d, i) {
                         return 10 + i * 50;
                     })
                     .attr("y", function (d) {
                         return 480- (d.value-20000)/70*4;
                     })
                     .attr("width", 40)
                     .attr("height", function(d){
                         return (d.value-20000)/70*4 ;

                     })
                     .attr("fill", function (d) {

                         return "rgb(" + Math.round((d.value - 20000) / 100 * 5) + ",0 ,0 )";

                     })
                     .attr("stroke","rgba(0,0,0,0.5)");
                     











    // little box
    bar

          .on("mousemove", function (d) {

              div.style("left", d3.event.pageX + 10 + "px");

              div.style("top", d3.event.pageY - 25 + "px");

              div.style("display", "inline-block");

              div.html((d.label) + "<br>" + (d.value) + "件");

          });

    bar

          .on("mouseout", function (d) {

              div.style("display", "none");

          });





    var scaleY = d3.scale.linear()
         .range([400, 0])
         .domain([20000, 27000]);



    var axisY = d3.svg.axis()
         .scale(scaleY)
         .orient("right")
         .ticks(10)
         .tickSize(-600,0);




    var s = svg.append("g");

    s
   .call(axisY)
   .attr({
    'fill':'none',
    'stroke':'rgba(0,0,0,0.2)',
    'transform':'translate(600,80)'
   }).selectAll('text')
   .attr({
    'fill':'#000',
    'stroke':'none',
   }).style({
    'font-size':'10px'
   });


    bar.append("text")
                       .text(function (d) {

                           return d.label;

                       })

                       .attr("text-anchor", "middle")

                       .attr("x", function (d, i) {

                           return 30 + i * 50;

                       })

                       .attr("y", 450)

                       .attr("font-family", "sans-serif")

                       .attr("font-size", "15px")

                       .attr("fill", "white")

                       .attr("stroke", "white");

   

</script>
    資料來源  <a href="https://www.moi.gov.tw/stat/">內政部 統計處</a>

</body>


</html>
