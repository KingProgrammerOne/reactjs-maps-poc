# reactjs-maps-poc

React app

Axios

Restfull API(get marker data with LeftTop and RightBottom Lng/Lat from end point) 

GoogleMap API(Map, user Markers) 

complated project

![](./media/complet.png)
## Requirements

1. ReactJS SPA web application with the least number of artefacts in the project
1. Responsive and mobile browser friendl
1. Maps is to center on the current user geo location
1. Please note: currently, the data is availalbe in Southern Ontario, Canada only
1. Maps tab is to display geoHash overlay based on geoHash query to the end-point mapping the Avg(***value***) NOT Sum(***count***)
1. User can scroll the map with the overlay information updated automatically
1. User can zoom in and out with increased/decreased precision of the data plotted on the map
1. Map dynamically adjusts the data ploted based on the zoom level and the current map center, e.g.:
![](./media/sample-map.png)
1. Developer will address comments and issues reported
1. Developer will Walk thorugh the deliverables to explain the details and artefacts in the project

## Data End-Point

### geoHash Query

#### Request
```
{
	"timestampMs": {
		"from": 1514768401000,
		"to": 1577840401000
	},
	"boundary": {
		"topLeft": {
			"lat": 43.86056486018512,
			"lon": -79.48820762336254
		},
		"bottomRight": {
			"lat": 43.849911721297154,
			"lon": -79.47820767760277
		}
	},
	"precision": 8,
	"timeoutMs": 30000,
	"deviceId": "157929A2-3843-4F55-88FD-00EB3171ECE5",
	"connectionType": "cellular",
	"provider": "Rogers Wireless",
	"filterByProvider": false,
	"filterByDeviceId": true,
	"latencyRanges": {
		"good": 150,
		"poor": 250
	}
}
```



#### Response

```
{
    "region": {
        "value": 302.7456439625133,
        "valueRange": "poor"
    },
    "provider": {
        "value": 293.7247081860494,
        "valueRange": "poor"
    },
    "device": {
        "value": 300.35619598300724,
        "valueRange": "poor"
    },
    "latency": [
        {
            "location": {
                "lat": 43.85542795644142,
                "lon": -79.48320319410414
            },
            "geoPoint": "43.85542795644142,-79.48320319410414",
            "altitude": 225.96572542190552,
            "value": 290.3104166984558,
            "count": 96,
            "valueRange": "poor"
        },
        {
            "location": {
                "lat": 43.85527755606121,
                "lon": -79.48315945094717
            },
            "geoPoint": "43.85527755606121,-79.48315945094717",
            "altitude": 227.88265860421316,
            "value": 293.40285731724333,
            "count": 70,
            "valueRange": "poor"
        },
        {
            "location": {
                "lat": 43.858516342006624,
                "lon": -79.48659393936396
            },
            "geoPoint": "43.858516342006624,-79.48659393936396",
            "altitude": 228.74850781758627,
            "value": 72.54166666666667,
            "count": 48,
            "valueRange": "good"
        },
        {
            "location": {
                "lat": 43.859036933031994,
                "lon": -79.48281004891864
            },
            "geoPoint": "43.859036933031994,-79.48281004891864",
            "altitude": 228.00519670758928,
            "value": 2477.2714287894114,
            "count": 28,
            "valueRange": "poor"
        },
        {
            "location": {
                "lat": 43.859096266544206,
                "lon": -79.48181610626096
            },
            "geoPoint": "43.859096266544206,-79.48181610626096",
            "altitude": 228.13919947697565,
            "value": 622.976923429049,
            "count": 26,
            "valueRange": "poor"
        },
        {
            "location": {
                "lat": 43.85908182065647,
                "lon": -79.48247473042171
            },
            "geoPoint": "43.85908182065647,-79.48247473042171",
            "altitude": 229.10818774883563,
            "value": 1979.569230886606,
            "count": 26,
            "valueRange": "poor"
        }
```
## New requirement

1. Instead of circles
1. Use heatmap, where weight is the value returned by the end-point
1. Read initial map coordinates, precision, lat/lon delta from the query string to centre the map
1. Allow zoom-in/out and move of the map, fetch data based on the new map location
1. Formula to calculate the precision:
```
  const minPrecision = 4;
  const maxPrecision = 8;
  const maxLatitudeDelta = 1.5;
  const logBase = 1.91;
  const correctionFactor = 1.4;
  const precision = Math.max(
      minPrecision,
      Math.min(
        ((maxLatitudeDelta - Math.log(latitudeDelta)/Math.log(logBase)) * correctionFactor),
        maxPrecision
      )
    );

```

