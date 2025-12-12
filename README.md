# SandCreekNDVI
NDVI of 2015,2020,2023 of sand creek
// 2015
// Create your point (change coordinates)
var point = ee.Geometry.Point(-104.71, 38.88);
// 1000 meter radius
var area1000 = point.buffer(1000);
// Load Landsat 7
var l7 = ee.ImageCollection("LANDSAT/LE07/C02/T1_L2")
  .filterDate('2015-01-01', '2015-12-31')
  .filterBounds(area1000)         // <- Use only this
  .map(function(img){
    img = img.multiply(100).add(-0.2);
    return img.copyProperties(img, img.propertyNames());
  });

// Compute NDVI
var addNDVI = l7.map(function(img){
  var ndvi = img.normalizedDifference(['SR_B4', 'SR_B3']).rename('NDVI');
  return img.addBands(ndvi);
});

// Composite
var ndviComposite = addNDVI.select('NDVI').median();

// NDVI visualization
var ndviVis = {
  min: 0,
  max: 1,
  palette: ['white', 'darkgreen', 'blue', 'brown', 'green']
};

//2020
// Create your point (change coordinates)
var point = ee.Geometry.Point(-104.71, 38.88);
// 1000 meter radius
var area1000 = point.buffer(1000);
// Load Landsat 7
var l7 = ee.ImageCollection("LANDSAT/LE07/C02/T1_L2")
  .filterDate('2020-01-01', '2020-12-31')
  .filterBounds(area1000)         // <- Use only this
  .map(function(img){
    img = img.multiply(100).add(-0.2);
    return img.copyProperties(img, img.propertyNames());
  });

// Compute NDVI
var addNDVI = l7.map(function(img){
  var ndvi = img.normalizedDifference(['SR_B4', 'SR_B3']).rename('NDVI');
  return img.addBands(ndvi);
});

// Composite
var ndviComposite = addNDVI.select('NDVI').median();

// NDVI visualization
var ndviVis = {
  min: 0,
  max: 1,
  palette: ['white', 'darkgreen', 'blue', 'brown', 'green']
};


// Add NDVI first
Map.addLayer(ndviComposite, ndviVis, 'NDVI Vegetation');

// Add boundary after so it draws on top
Map.addLayer(area1000, {color: 'grey'}, '1000m Radius');

// Add NDVI first
Map.addLayer(ndviComposite, ndviVis, 'NDVI Vegetation');

//2023
// Create your point (change coordinates)
var point = ee.Geometry.Point(-104.71, 38.88);
// 1000 meter radius
var area1000 = point.buffer(1000);
// Load Landsat 7
var l7 = ee.ImageCollection("LANDSAT/LE07/C02/T1_L2")
  .filterDate('2023-01-01', '2023-12-31')
  .filterBounds(area1000)         // <- Use only this
  .map(function(img){
    img = img.multiply(100).add(-0.2);
    return img.copyProperties(img, img.propertyNames());
  });

// Compute NDVI
var addNDVI = l7.map(function(img){
  var ndvi = img.normalizedDifference(['SR_B4', 'SR_B3']).rename('NDVI');
  return img.addBands(ndvi);
});

// Composite
var ndviComposite = addNDVI.select('NDVI').median();

// NDVI visualization
var ndviVis = {
  min: 0,
  max: 1,
  palette: ['white', 'darkgreen', 'blue', 'brown', 'green']
};

// Add NDVI first
Map.addLayer(ndviComposite, ndviVis, 'NDVI Vegetation');

// Add boundary after so it draws on top
Map.addLayer(area1000, {color: 'grey'}, '1000m Radius');

