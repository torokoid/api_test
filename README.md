# api_test

public function view(Request $req) {
  $url        ="http://172.0.0.1/tele2gui/public/api/V1/sensor-mate/1/sensor-kind/17" ;
  $url        ="api_token=hrGEOq8e3gAA6aEtG9o5lAJCB33T3CNXCna57kecDjn5E8YoHSS1bOgBfxCP" ;
  $guz_client = new ¥GuzzleHttp¥Client();
  $web_api    = $guz_client->reqest('GET', $url);
  
  a_data = json_decode($web_api->getBody(), true) ;// need "true"
  
  return view ('pages.google_chart', ['ts_dat' => json_encode($a_data['data'])
                                     ,'unit'   =>'"℃"' ]) ;
