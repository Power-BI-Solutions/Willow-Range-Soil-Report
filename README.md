# Willow Branch Range - Soil Report <br><br/>

The Willow Range report uses a custom map. For each of the orchards I created a polygon by using Google Earth. The project from Google Earth outputs a kml file, which can't be read by Power BI.
The kml file had to be converted to topojson format in order to work within Power BI environment.
I will describe the whole process in the Creating Custom Map section.


### Dashboard
<p align="center">
<img width="650em" src="https://github.com/mBohunickaCharles/Willow-Range-Soil-Report/blob/master/images/Willow%20Branch%20Range.gif" align = "center"/>
</p>
<br><br/>

### Data Source
- [soil_data.xlsx](https://github.com/mBohunickaCharles/Willow-Range-Soil-Report/blob/master/soil_data.xlsx)
- [orchard_lookup.xlsx](https://github.com/mBohunickaCharles/Willow-Range-Soil-Report/blob/master/orchard_lookup.xlsx)
- [orchard_polygons.topojson](https://github.com/mBohunickaCharles/Willow-Range-Soil-Report/blob/master/custom_map/Orchard%2BPolygons.topojson)

Please note that data is all fictional and doesn't reflect real measurements. It was purely created for this exercise.
<br><br/>

### Creating Custom Map
To create custom map, I started with Google Earth. I created a new project and drew polygons for each of the fields. It doesn't matter what color you assighn to the fields, however it's important to name the field correctly. Names have to be exactly the same as you will be using in the report.

<p align="center">
<img width="700em" src="https://github.com/mBohunickaCharles/Willow-Range-Soil-Report/blob/master/images/orchard_polygons_earth.png" align = "center"/>
</p>

Clicking on 3 vertical dots (just next to bin) allowed me to save kml file locally. 
After I had my kml file saved, I needed to convert it to different format called topojson. For this task I used [MyGeodata Converter website.](https://mygeodata.cloud/converter/kml-to-json)
It's easy to navigate and provides an option to convert kml file to our desired convertion format. <br>

To be able to use custom maps in Power BI I had to use Shape Map. Mine wasn't available, and quick set up via options was needed:
- click on File => Options and Settings => Options
- a window will pop out => under GLOBAL click on Preview features
- activate Shape map visual

<p align="center">
<img width="700em" src="https://github.com/mBohunickaCharles/Willow-Range-Soil-Report/blob/master/images/preview_options.png" align = "center"/>
</p>

To be able to use Shape Map I had to close Power BI and reopen again. After restart I could see new visual icon added to my menu.
<br><br/>

### Custom Measures
To be able to switch between measures I have created custom measures. This allowed me to filter for various soil measurements within one dashboard. This is in my opinion more user friendly than having several dashboard for each of the soil measurement.

```dax
Chemical Measure Selection = 
SWITCH(
    VALUES(
        chemical_measures[chemical_measure]),
        "Total nitrogen stock (mg N/kg)", SUM(soil_data[Total nitrogen stock (mg N/kg)]),
        "N-supplying capacity (kg N/ha)", SUM(soil_data[N-supplying capacity (kg N/ha)]),
        "Total P-stock (mg P2O5/100g)", SUM(soil_data[Total P-stock (mg P2O5/100g)]),
        "K-soil stock (mmol+/kg)", SUM(soil_data[K-soil stock (mmol+/kg)]),
        "Total sulphur stock (mg S/kg)", SUM(soil_data[Total sulphur stock (mg S/kg)]),
        "S-supplying capacity (kg S/ha)", SUM(soil_data[S-supplying capacity (kg S/ha)]),
        "Ca-soil stock (mmol+/kg)", SUM(soil_data[Ca-soil stock (mmol+/kg)]),
        "Mg-soil stock (mmol+/kg)", SUM(soil_data[Mg-soil stock (mmol+/kg)]),
        "Ca-soil stock (kg Ca/ha)", SUM(soil_data[Ca-soil stock (kg Ca/ha)]),
        SUM(soil_data[Total nitrogen stock (mg N/kg)]
        )
)
```


```dax
Physical Measure Selection = 
SWITCH(
    VALUES(
        physical_measures[physical_measure]),
       "pH", SUM(soil_data[pH]),
        "C-organic SOC (%)", SUM(soil_data[C-organic SOC (%)]),
        "Bulk Density g/cm3", SUM(soil_data[Bulk Density g/cm3]),
        SUM(soil_data[pH]
        )
)
```

<br><br/>


### Model

<p align="center">
<img width="700em" src="https://github.com/mBohunickaCharles/Willow-Range-Soil-Report/blob/master/images/willow_range_data.png" align = "center"/>
</p>
<br><br/>

Author:
@mBohunickaCharles
