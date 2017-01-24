# README



## Usage

<html>
<head>
    <meta charset="utf-8">
    <link href="./build/nv.d3.css" rel="stylesheet" type="text/css">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/d3/3.5.2/d3.min.js" charset="utf-8"></script>
    <script src="./build/nv.d3.js"></script>

    <style>
        text {
            font: 12px sans-serif;
        }
        svg {
            display: block;
        }
        html, body, svg {
            margin: 0px;
            padding: 0px;
            height: 100%;
            width: 100%;
        }
    </style>
</head>
<body class='with-3d-shadow with-transitions'>
    <script>
        var expandLegend = function() {
            var exp = chart.legend.expanded();
            chart.legend.expanded(!exp);
            chart.update();
        }
    </script>
<svg id="chart1"></svg>

<script>

    var colors = d3.scale.category20();
    var chart;
    nv.addGraph(function() {
        // chart = nv.models.stackedAreaChart()
        chart = nv.models.multiBarChart()
            .useInteractiveGuideline(true)
            .x(function(d) { return d[0]; })
            .y(function(d) { return d[1]; })
            .duration(300);

        chart.xAxis.tickFormat(function(d) { return d3.time.format("%x")(new Date(d)); });
        chart.yAxis.tickFormat(d3.format("d"));
        chart.legend.vers("furious");

        d3.csv("./db/data.csv", function(csv_input) {

            // Extraction of CSV columns title
            var csv_col_title = Object.keys(csv_input[0]).splice(1, Object.keys(csv_input[0]).length);

            // Generation of an empty data structure : tags_obj
            var tags_obj = {};
            for (col_title of csv_col_title) {
                tags_obj[col_title] = {"values": [], "key": col_title}
            }

            // Fill tags_obj with CSV informations
            fill_tags_obj = csv_input.map(function(csv_input_line) {
                var date = new Date(csv_input_line["Date"]).getTime()
                for (col_title of csv_col_title) {
                    var data_obj = {"0": date, "1": parseInt(csv_input_line[col_title])}
                    tags_obj[col_title]["values"].push(data_obj)
                }
            })

            // Change tags_obj (object) to tags_array (array)
            var tags_array = Object.keys(tags_obj).map(function (key) { return tags_obj[key]; });

            // Chart creation
            d3.select("#chart1")
                .datum(tags_array)
                .transition().duration(1000)
                .call(chart)
                .each("start", function() {
                    setTimeout(function() {
                        d3.selectAll("#chart1 *").each(function() {
                            if(this.__transition__)
                                this.__transition__.duration = 1;
                        })
                    }, 0)
                });
            nv.utils.windowResize(chart.update);
            return chart;
        });
    })

</script>
</body>
</html>