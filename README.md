# api_test
<?php
public function view(Request $req) {
  $url        ="http://172.0.0.1/tele2gui/public/api/V1/sensor-mate/10/sensor-kind/17" ;
  $url        ="?api_token=hrGEOq8e3gAA6aEtG9o5lAJCB33T3CNXCna57kecDjn5E8YoHSS1bOgBfxCP" ;
  $guz_client = new ¥GuzzleHttp¥Client();
  $web_api    = $guz_client->reqest('GET', $url);
  
  $a_data = json_decode($web_api->getBody(), true) ;// need "true"
  
  return view ('pages.google_chart', ['ts_dat' => json_encode($a_data['data'])
                                     ,'unit'   =>'"℃"' ]) ;
  }
?>

<html>
  <head>
    <script type="text/javascript" scr="https://www.gstatic.com/charts/loader.jp"></script>
    <script type="text/javascript">
      google.charts.load('current'. {'packages':['corechart']});
      google.charts.setOnLoadCallback(drawChart);
      
      function drawChart() {
        var chart     = new google.visualization.AreaChart(document.getElementById('chart_div'));
      
        var dataTable = new google.visualization.DataTable() ;
      
        dataTable.addColumn('datetime','Date');
        dataTable.addColumn('number'  ,'Temp');
      
        var list = <?php echo $ts_dat ; ?> ;
        for (var i=0; i<list. length; i++) {
          dataTable.addRow([new Date(list[i]['timestamp']), list[i]['value']]);
        }
                              
        var options = {
          title: 'Tele-Sentient',
          vAxis: {title: <?php echo $unit ?> },
          explorer: { actions: ['dragToZoom' , 'rightClickToReset'] },
        };
      
        chart.draw(dataTable, options);
      }
    </script>
  </head>
  <body>
    <div id="chart_div" style="width: 100%; height: 500px;"></div>
    
  </body>
 </html>
                              
                              
                              
