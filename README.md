# planefinder

it is plane parametrs imitate application, you can gat them by http://localhost:7634/aircraft

for communicating application you need to chekout apropriate tag


reponse example below
<pre>
<code>
[
   {
      "id":1,
      "callsign":"SAL001",
      "squawk":"sqwk",
      "reg":"N12345",
      "flightno":"SAL001",
      "route":"route",
      "type":"LJ",
      "category":"ct",
      "altitude":30000,
      "heading":280,
      "speed":440,
      "lat":39.2979849,
      "lon":-94.71921,
      "barometer":0.0,
      "vert_rate":0,
      "selected_altitude":0,
      "polar_distance":0.0,
      "polar_bearing":0.0,
      "is_adsb":false,
      "is_on_ground":true,
      "last_seen_time":"2022-11-16T15:00:12.751883789Z",
      "pos_update_time":"2022-11-16T15:00:12.751884830Z",
      "bds40_seen_time":"2022-11-16T15:00:12.751885053Z"
   },
   {
      "id":2,
      "callsign":"SAL002",
      "squawk":"sqwk",
      "reg":"N54321",
      "flightno":"SAL002",
      "route":"route",
      "type":"LJ",
      "category":"ct",
      "altitude":40000,
      "heading":65,
      "speed":440,
      "lat":39.8560963,
      "lon":-104.6759263,
      "barometer":0.0,
      "vert_rate":0,
      "selected_altitude":0,
      "polar_distance":0.0,
      "polar_bearing":0.0,
      "is_adsb":false,
      "is_on_ground":true,
      "last_seen_time":"2022-11-16T15:00:12.751901354Z",
      "pos_update_time":"2022-11-16T15:00:12.751901684Z",
      "bds40_seen_time":"2022-11-16T15:00:12.751901893Z"
   },
   {
      "id":3,
      "callsign":"SAL002",
      "squawk":"sqwk",
      "reg":"N54321",
      "flightno":"SAL002",
      "route":"route",
      "type":"LJ",
      "category":"ct",
      "altitude":40000,
      "heading":65,
      "speed":440,
      "lat":39.8412964,
      "lon":-105.0048267,
      "barometer":0.0,
      "vert_rate":0,
      "selected_altitude":0,
      "polar_distance":0.0,
      "polar_bearing":0.0,
      "is_adsb":false,
      "is_on_ground":true,
      "last_seen_time":"2022-11-16T15:00:12.751903317Z",
      "pos_update_time":"2022-11-16T15:00:12.751903532Z",
      "bds40_seen_time":"2022-11-16T15:00:12.751903721Z"
   }
]</code></pre>

it uses lomback lib for Aircraft domen\
@Data - annotation equivalent methods equals(), hashcode(), toString(), getters and setters\
@NoArgsConstructor, @AllArgsConstructor, equivalent constructor without argument and constructor with all arguments\

@JsonIgnoreProperties(ignoreUnknown = true) - it's a jackson annotation it is ignoring unknown values, for which thare are no propertis
if we used RedisTamplate without repository, we need to to create some set and get methods for converting time data to string.


### claud concept (after "without_cloud" tag, we went to cloud concept)
this app concept is - Supplier -> consumer(planefinder ->rabbit->aircraft-positions) concept\
before this aircraft-positions(webflux_redis,webflux_jpa_RDBAndNoSql) requested to planefinder(tag:claud_strategy_without_kafka) for data, but naw planfinder is sending data to RabbitMQ and aircraft-positions pull from rabbit \
it is sanding data by his Supplier> reportPositions() method every second(without @scheduler), which annotated @bean\
and in application.properties we set the direction where are sanding we data (appropriate the aircraft-positions getting data process)\

chapter 6
