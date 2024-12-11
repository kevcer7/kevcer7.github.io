<!DOCTYPE html>
<html>
<head>
  <title>Vega-Lite Map</title>
  <script src="https://cdn.jsdelivr.net/npm/vega@5"></script>
  <script src="https://cdn.jsdelivr.net/npm/vega-lite@5"></script>
  <script src="https://cdn.jsdelivr.net/npm/vega-embed@6"></script>
</head>
<body>
  <div id="vis"></div>

  <script type="text/javascript">
    var yourVlSpec = {
      $schema: 'https://vega.github.io/schema/vega-lite/v5.json',
      description: 'A map of buildings in Chicago by sector.',
      data: {
        url: 'assets/json/chicagocover.json',
        format: {
          type: 'json',
          property: 'features' // Use this if your JSON is geoJSON, otherwise adjust accordingly
        }
      },
      transform: [
        {
          calculate: "datum['Latitude'] + ', ' + datum['Longitude']",
          as: 'geo'
        }
      ],
      mark: 'circle',
      encoding: {
        longitude: {
          field: 'Longitude',
          type: 'quantitative'
        },
        latitude: {
          field: 'Latitude',
          type: 'quantitative'
        },
        size: {value: 10},
        color: {
          field: 'Cohort - Sector',
          type: 'nominal',
          legend: {title: 'Sector'}
        },
        tooltip: [
          {field: 'Address', type: 'nominal'}
        ]
      }
    };

    vegaEmbed('#vis', yourVlSpec, {actions: false});
  </script>
</body>
</html>
