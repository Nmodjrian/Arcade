# Combining Arcade and HTML for GIS pop ups

Street View for starting point 

 

// Write a script to return a value to show in the pop-up. 

// For example, get the average of 4 fields: 

// Average($feature.SalesQ1, $feature.SalesQ2, $feature.SalesQ3, $feature.SalesQ4) 

 

// Get the first point of the polyline feature 

var startPoint = Geometry($feature).paths[0][0]; 

 

// Get the longitude and latitude of the starting point 

var x = startPoint.x; 

var y = startPoint.y; 




 

var PathsGeometry = Geometry($feature); 

var ArcadeX = x; 

var ArcadeY = y; 

var ArcadeSr = PathsGeometry.spatialReference.wkid; 

var Latitude, Longitude; 

 

function AuxSphereToLatLon(x, y)  

{  Console("Converting..."); 

 

// Conversion based on http://dotnetfollower.com/wordpress/2011/07/javascript-how-to-convert-mercator-sphere-coordinates-to-latitude-and-longitude/  

 

var rMajor = 6378137; 

var shift = PI * rMajor; 

Longitude = x / shift * 180.0; 

Latitude = y / shift * 180.0; 

Latitude = 180 / PI * (2 * Atan(Exp(Latitude * PI / 180.0)) - PI / 2.0); 

} 

 

if (ArcadeSr == 4326) {  Console("4326 Spatial Reference - No Conversion Necessary");  Latitude = ArcadeY;  Longitude = ArcadeX;} else if (ArcadeSr == 102100) {  Console("102100 Spatial Reference - Conversion Necessary");  AuxSphereToLatLon(ArcadeX, ArcadeY);} else {  Console(ArcadeSr + " Spatial Reference is not supported - currently works with Web Maps where the basemap is in WGS84 (4326) or Web Mercator Auxiliary Sphere 102100");} 

var url = "http://www.google.com/maps/@?api=1&map_action=pano&viewpoint=" + text(Latitude) + "," + text(Longitude); 

return url; 

 

 

Street View for mid point 

// Get the number of paths in the polyline feature  

var numPaths = Count(Geometry($feature).paths);  

// Choose a random path index  

var pathIndex = Floor(numPaths/ 2.0);  

// Get the number of points in the chosen path  

var numPoints = Count(Geometry($feature).paths[pathIndex]);  

// Choose a random point index  

var pointIndex = Floor(numPoints / 2.0);  

// Get the chosen point  

var chosenPoint = Geometry($feature).paths[pathIndex][pointIndex];  

// Get the X and Y coordinates of the chosen point  

var x = chosenPoint.x;  

var y = chosenPoint.y;  

 

var PathsGeometry = Geometry($feature); 

var ArcadeX = x; 

var ArcadeY = y; 

var ArcadeSr = PathsGeometry.spatialReference.wkid; 

var Latitude, Longitude; 

 

function AuxSphereToLatLon(x, y)  

{  Console("Converting..."); 

 

// Conversion based on http://dotnetfollower.com/wordpress/2011/07/javascript-how-to-convert-mercator-sphere-coordinates-to-latitude-and-longitude/  

 

var rMajor = 6378137; 

var shift = PI * rMajor; 

Longitude = x / shift * 180.0; 

Latitude = y / shift * 180.0; 

Latitude = 180 / PI * (2 * Atan(Exp(Latitude * PI / 180.0)) - PI / 2.0); 

} 

 

if (ArcadeSr == 4326) {  Console("4326 Spatial Reference - No Conversion Necessary");  Latitude = ArcadeY;  Longitude = ArcadeX;} else if (ArcadeSr == 102100) {  Console("102100 Spatial Reference - Conversion Necessary");  AuxSphereToLatLon(ArcadeX, ArcadeY);} else {  Console(ArcadeSr + " Spatial Reference is not supported - currently works with Web Maps where the basemap is in WGS84 (4326) or Web Mercator Auxiliary Sphere 102100");} 

var url = "http://www.google.com/maps/@?api=1&map_action=pano&viewpoint=" + text(Latitude) + "," + text(Longitude); 

return url; 
