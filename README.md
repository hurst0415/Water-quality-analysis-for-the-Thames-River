# Water quality analysis for the Thames River

## Introduction
In this project, we employ superstatistical methods and machine learning to analyze measured time series data of water quality indicators from the River Thames. Particular emphasis is placed on unraveling the complex underlying dynamics of water quality indicators.

## Requirements
* Python 3.9
* numpy==1.20.1
* pandas==1.2.3
* scikit-learn==1.4.2
* matplotlib==3.3.4
* seaborn==0.13.2
* tensorflow==2.11.0
* lightgbm==3.3.5
* xgboost==1.7.3
* torch==2.0.0

To install the required dependencies, use the following command:
```bash
pip install -r requirements.txt
```

## Data
Download real-time water quality measurements from the Meteor Data Cloud at "https://telemetry-data.com/viewer2," provided by the Environmental Agency out of their generous courtesy. Contact the agency directly to obtain the necessary access credentials. Choose the river, time span, and water quality indicators as needed. This project specifically focuses on data from the Thames River between December 1, 2017, and December 1, 2022, but the methodology can be extended to other rivers.

In our project, we use the following water quality indicators:

1. Dissolved oxygen (DO), measured in milligrams per liter (mg/L).
2. Temperature (Temp), measured in degrees Celsius (°C).
3. Electrical conductivity (COND), measured in microsiemens per centimeter (μS/cm).
4. pH (PH), ranging from 0 to 14.
5. Ammonium (AMMONIUM), measured in milligrams per liter (mg/L).
6. Turbidity (TURBIDITY), measured in nephelometric turbidity units (NTU).

For a geographical overview of our water quality monitoring sites as well as rainfall collection sites along the River Thames, run Map.ipynb to recreate the interactive HTML map. You can open Sites_map.html and hover over the map to check locations.[Uplo<!DOCTYPE html>
<html>
<head>
    
    <meta http-equiv="content-type" content="text/html; charset=UTF-8" />
    
        <script>
            L_NO_TOUCH = false;
            L_DISABLE_3D = false;
        </script>
    
    <style>html, body {width: 100%;height: 100%;margin: 0;padding: 0;}</style>
    <style>#map {position:absolute;top:0;bottom:0;right:0;left:0;}</style>
    <script src="https://cdn.jsdelivr.net/npm/leaflet@1.9.3/dist/leaflet.js"></script>
    <script src="https://code.jquery.com/jquery-1.12.4.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.2.2/dist/js/bootstrap.bundle.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/Leaflet.awesome-markers/2.0.2/leaflet.awesome-markers.js"></script>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/leaflet@1.9.3/dist/leaflet.css"/>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.2/dist/css/bootstrap.min.css"/>
    <link rel="stylesheet" href="https://netdna.bootstrapcdn.com/bootstrap/3.0.0/css/bootstrap.min.css"/>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@fortawesome/fontawesome-free@6.2.0/css/all.min.css"/>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/Leaflet.awesome-markers/2.0.2/leaflet.awesome-markers.css"/>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/python-visualization/folium/folium/templates/leaflet.awesome.rotate.min.css"/>
    
            <meta name="viewport" content="width=device-width,
                initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
            <style>
                #map_8a6d3947593db6f964f4af195e39415e {
                    position: relative;
                    width: 100.0%;
                    height: 100.0%;
                    left: 0.0%;
                    top: 0.0%;
                }
                .leaflet-container { font-size: 1rem; }
            </style>
        
</head>
<body>
    
    
            <div class="folium-map" id="map_8a6d3947593db6f964f4af195e39415e" ></div>
        
</body>
<script>
    
    
            var map_8a6d3947593db6f964f4af195e39415e = L.map(
                "map_8a6d3947593db6f964f4af195e39415e",
                {
                    center: [51.5074, -0.1278],
                    crs: L.CRS.EPSG3857,
                    zoom: 13,
                    zoomControl: true,
                    preferCanvas: false,
                }
            );

            

        
    
            var tile_layer_51d788e964c4610df2d80816971eafb2 = L.tileLayer(
                "https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png",
                {"attribution": "Data by \u0026copy; \u003ca target=\"_blank\" href=\"http://openstreetmap.org\"\u003eOpenStreetMap\u003c/a\u003e, under \u003ca target=\"_blank\" href=\"http://www.openstreetmap.org/copyright\"\u003eODbL\u003c/a\u003e.", "detectRetina": false, "maxNativeZoom": 18, "maxZoom": 18, "minZoom": 0, "noWrap": false, "opacity": 1, "subdomains": "abc", "tms": false}
            ).addTo(map_8a6d3947593db6f964f4af195e39415e);
        
    
            var marker_980c9fe99403f98e3c46970722a13f5a = L.marker(
                [51.479811, -0.303104],
                {}
            ).addTo(map_8a6d3947593db6f964f4af195e39415e);
        
    
            var icon_96ea8704f391bc0931c8da08f05589f7 = L.AwesomeMarkers.icon(
                {"extraClasses": "fa-rotate-0", "icon": "info-sign", "iconColor": "white", "markerColor": "red", "prefix": "glyphicon"}
            );
            marker_980c9fe99403f98e3c46970722a13f5a.setIcon(icon_96ea8704f391bc0931c8da08f05589f7);
        
    
        var popup_bc64d8cf5c11badf642235be13efc678 = L.popup({"maxWidth": "100%"});

        
            
                var html_1187acbc3e22f8c9adc47d2867271c2b = $(`<div id="html_1187acbc3e22f8c9adc47d2867271c2b" style="width: 100.0%; height: 100.0%;">TBB</div>`)[0];
                popup_bc64d8cf5c11badf642235be13efc678.setContent(html_1187acbc3e22f8c9adc47d2867271c2b);
            
        

        marker_980c9fe99403f98e3c46970722a13f5a.bindPopup(popup_bc64d8cf5c11badf642235be13efc678)
        ;

        
    
    
            var marker_4a6113282278e15bba11f6292727c025 = L.marker(
                [51.485905, -0.282526],
                {}
            ).addTo(map_8a6d3947593db6f964f4af195e39415e);
        
    
            var icon_173fd90978a10aec0c4cee937dc77055 = L.AwesomeMarkers.icon(
                {"extraClasses": "fa-rotate-0", "icon": "info-sign", "iconColor": "white", "markerColor": "red", "prefix": "glyphicon"}
            );
            marker_4a6113282278e15bba11f6292727c025.setIcon(icon_173fd90978a10aec0c4cee937dc77055);
        
    
        var popup_ff3d07fd5d932b21db3c253d3e5631c8 = L.popup({"maxWidth": "100%"});

        
            
                var html_8df55463ec2777f8a049b643cccb5788 = $(`<div id="html_8df55463ec2777f8a049b643cccb5788" style="width: 100.0%; height: 100.0%;">TKB</div>`)[0];
                popup_ff3d07fd5d932b21db3c253d3e5631c8.setContent(html_8df55463ec2777f8a049b643cccb5788);
            
        

        marker_4a6113282278e15bba11f6292727c025.bindPopup(popup_ff3d07fd5d932b21db3c253d3e5631c8)
        ;

        
    
    
            var marker_5d47d103fa471d83ecb3d92d6613f493 = L.marker(
                [51.482289, -0.250819],
                {}
            ).addTo(map_8a6d3947593db6f964f4af195e39415e);
        
    
            var icon_402fb69b1ae4353101ba91df76f3be47 = L.AwesomeMarkers.icon(
                {"extraClasses": "fa-rotate-0", "icon": "info-sign", "iconColor": "white", "markerColor": "red", "prefix": "glyphicon"}
            );
            marker_5d47d103fa471d83ecb3d92d6613f493.setIcon(icon_402fb69b1ae4353101ba91df76f3be47);
        
    
        var popup_ac7e3d317e1e9b51fdc5f5a37d2911ca = L.popup({"maxWidth": "100%"});

        
            
                var html_3d8ec99d941a8c72c18f0e567bbc48f8 = $(`<div id="html_3d8ec99d941a8c72c18f0e567bbc48f8" style="width: 100.0%; height: 100.0%;">TChP</div>`)[0];
                popup_ac7e3d317e1e9b51fdc5f5a37d2911ca.setContent(html_3d8ec99d941a8c72c18f0e567bbc48f8);
            
        

        marker_5d47d103fa471d83ecb3d92d6613f493.bindPopup(popup_ac7e3d317e1e9b51fdc5f5a37d2911ca)
        ;

        
    
    
            var marker_59c2d1ef62ee099ea305e3f12d8a27c8 = L.marker(
                [51.489988, -0.234693],
                {}
            ).addTo(map_8a6d3947593db6f964f4af195e39415e);
        
    
            var icon_53bb1f5b5508995a91762f5e5f1026f2 = L.AwesomeMarkers.icon(
                {"extraClasses": "fa-rotate-0", "icon": "info-sign", "iconColor": "white", "markerColor": "red", "prefix": "glyphicon"}
            );
            marker_59c2d1ef62ee099ea305e3f12d8a27c8.setIcon(icon_53bb1f5b5508995a91762f5e5f1026f2);
        
    
        var popup_2c7568472154c268208f9451ef1fb4b0 = L.popup({"maxWidth": "100%"});

        
            
                var html_80ec027d749a02505f434a29a4af6600 = $(`<div id="html_80ec027d749a02505f434a29a4af6600" style="width: 100.0%; height: 100.0%;">TH</div>`)[0];
                popup_2c7568472154c268208f9451ef1fb4b0.setContent(html_80ec027d749a02505f434a29a4af6600);
            
        

        marker_59c2d1ef62ee099ea305e3f12d8a27c8.bindPopup(popup_2c7568472154c268208f9451ef1fb4b0)
        ;

        
    
    
            var marker_108efe233a3e31908f84d9a5a53342b6 = L.marker(
                [51.467322, -0.215383],
                {}
            ).addTo(map_8a6d3947593db6f964f4af195e39415e);
        
    
            var icon_6f49e10e8ce438e6e2ed9857f881e112 = L.AwesomeMarkers.icon(
                {"extraClasses": "fa-rotate-0", "icon": "info-sign", "iconColor": "white", "markerColor": "red", "prefix": "glyphicon"}
            );
            marker_108efe233a3e31908f84d9a5a53342b6.setIcon(icon_6f49e10e8ce438e6e2ed9857f881e112);
        
    
        var popup_81eaeefa2bca1631d898bad016955691 = L.popup({"maxWidth": "100%"});

        
            
                var html_085c273636944a87334f79661a3b9bd0 = $(`<div id="html_085c273636944a87334f79661a3b9bd0" style="width: 100.0%; height: 100.0%;">TPut</div>`)[0];
                popup_81eaeefa2bca1631d898bad016955691.setContent(html_085c273636944a87334f79661a3b9bd0);
            
        

        marker_108efe233a3e31908f84d9a5a53342b6.bindPopup(popup_81eaeefa2bca1631d898bad016955691)
        ;

        
    
    
            var marker_aee72310be36d1d5067822e494f04b15 = L.marker(
                [51.483087, -0.165929],
                {}
            ).addTo(map_8a6d3947593db6f964f4af195e39415e);
        
    
            var icon_a0b87bd2fa11a562231b986d04a1cd9e = L.AwesomeMarkers.icon(
                {"extraClasses": "fa-rotate-0", "icon": "info-sign", "iconColor": "white", "markerColor": "red", "prefix": "glyphicon"}
            );
            marker_aee72310be36d1d5067822e494f04b15.setIcon(icon_a0b87bd2fa11a562231b986d04a1cd9e);
        
    
        var popup_1236d7b8798f44b7e06f581d42447e92 = L.popup({"maxWidth": "100%"});

        
            
                var html_9001e11bb60138a854d00cd31e15c6c2 = $(`<div id="html_9001e11bb60138a854d00cd31e15c6c2" style="width: 100.0%; height: 100.0%;">TCaP</div>`)[0];
                popup_1236d7b8798f44b7e06f581d42447e92.setContent(html_9001e11bb60138a854d00cd31e15c6c2);
            
        

        marker_aee72310be36d1d5067822e494f04b15.bindPopup(popup_1236d7b8798f44b7e06f581d42447e92)
        ;

        
    
    
            var marker_1b47da51ad2a99ebff68332c27f665eb = L.marker(
                [51.495672, 0.041657],
                {}
            ).addTo(map_8a6d3947593db6f964f4af195e39415e);
        
    
            var icon_08d23060cb594d62424985ac8c312806 = L.AwesomeMarkers.icon(
                {"extraClasses": "fa-rotate-0", "icon": "info-sign", "iconColor": "white", "markerColor": "red", "prefix": "glyphicon"}
            );
            marker_1b47da51ad2a99ebff68332c27f665eb.setIcon(icon_08d23060cb594d62424985ac8c312806);
        
    
        var popup_2a70eb07f93795cb3354b29cadf84227 = L.popup({"maxWidth": "100%"});

        
            
                var html_812bdbcbe415a855e82d13c874323163 = $(`<div id="html_812bdbcbe415a855e82d13c874323163" style="width: 100.0%; height: 100.0%;">TBGP</div>`)[0];
                popup_2a70eb07f93795cb3354b29cadf84227.setContent(html_812bdbcbe415a855e82d13c874323163);
            
        

        marker_1b47da51ad2a99ebff68332c27f665eb.bindPopup(popup_2a70eb07f93795cb3354b29cadf84227)
        ;

        
    
    
            var marker_d26bf43e9eb60e733c6516ce8b5646cc = L.marker(
                [51.504281, 0.167781],
                {}
            ).addTo(map_8a6d3947593db6f964f4af195e39415e);
        
    
            var icon_0cb6e9693067e1c87bb27b105a018522 = L.AwesomeMarkers.icon(
                {"extraClasses": "fa-rotate-0", "icon": "info-sign", "iconColor": "white", "markerColor": "red", "prefix": "glyphicon"}
            );
            marker_d26bf43e9eb60e733c6516ce8b5646cc.setIcon(icon_0cb6e9693067e1c87bb27b105a018522);
        
    
        var popup_f721d51c0f5e0789a48a7042eee13568 = L.popup({"maxWidth": "100%"});

        
            
                var html_e1c465b23a9b424338ea00e30f55db9f = $(`<div id="html_e1c465b23a9b424338ea00e30f55db9f" style="width: 100.0%; height: 100.0%;">TEB</div>`)[0];
                popup_f721d51c0f5e0789a48a7042eee13568.setContent(html_e1c465b23a9b424338ea00e30f55db9f);
            
        

        marker_d26bf43e9eb60e733c6516ce8b5646cc.bindPopup(popup_f721d51c0f5e0789a48a7042eee13568)
        ;

        
    
    
            var marker_2f39220b8b8eab0e0a6df630c73d077f = L.marker(
                [51.470424, 0.250742],
                {}
            ).addTo(map_8a6d3947593db6f964f4af195e39415e);
        
    
            var icon_dae89a59b278e9954ff4d0964fc0ddd6 = L.AwesomeMarkers.icon(
                {"extraClasses": "fa-rotate-0", "icon": "info-sign", "iconColor": "white", "markerColor": "red", "prefix": "glyphicon"}
            );
            marker_2f39220b8b8eab0e0a6df630c73d077f.setIcon(icon_dae89a59b278e9954ff4d0964fc0ddd6);
        
    
        var popup_fffb403754c255fc8ce7b136e2aefde7 = L.popup({"maxWidth": "100%"});

        
            
                var html_461f38531bcafc03b995b4c3b77d757d = $(`<div id="html_461f38531bcafc03b995b4c3b77d757d" style="width: 100.0%; height: 100.0%;">TPur</div>`)[0];
                popup_fffb403754c255fc8ce7b136e2aefde7.setContent(html_461f38531bcafc03b995b4c3b77d757d);
            
        

        marker_2f39220b8b8eab0e0a6df630c73d077f.bindPopup(popup_fffb403754c255fc8ce7b136e2aefde7)
        ;

        
    
    
            var marker_3c40c9115fce64ece0f06a54901aa95b = L.marker(
                [51.479811, -0.303104],
                {}
            ).addTo(map_8a6d3947593db6f964f4af195e39415e);
        
    
            var icon_2d21bf3ddf01fc9b495902cf559ece7e = L.AwesomeMarkers.icon(
                {"extraClasses": "fa-rotate-0", "icon": "info-sign", "iconColor": "white", "markerColor": "red", "prefix": "glyphicon"}
            );
            marker_3c40c9115fce64ece0f06a54901aa95b.setIcon(icon_2d21bf3ddf01fc9b495902cf559ece7e);
        
    
        var popup_5321a47af1dc613c28819cbfaf795218 = L.popup({"maxWidth": "100%", "permanent": true});

        
            
                var html_4fcd5398234393dcbb9a5535c2802301 = $(`<div id="html_4fcd5398234393dcbb9a5535c2802301" style="width: 100.0%; height: 100.0%;">TBB</div>`)[0];
                popup_5321a47af1dc613c28819cbfaf795218.setContent(html_4fcd5398234393dcbb9a5535c2802301);
            
        

        marker_3c40c9115fce64ece0f06a54901aa95b.bindPopup(popup_5321a47af1dc613c28819cbfaf795218)
        ;

        
    
    
            var marker_540540ab7579f13264b01b2e1c3f2694 = L.marker(
                [51.479811, -0.303104],
                {}
            ).addTo(map_8a6d3947593db6f964f4af195e39415e);
        
    
            var div_icon_c75db25f7fb3854a003daa412b68a800 = L.divIcon({"className": "empty", "html": "\u003cdiv style=\u0027font-size: 16px; color: blue; font-weight: bold;\u0027\u003eTBB\u003c/div\u003e", "iconAnchor": [10, 0], "iconSize": [150, 36]});
            marker_540540ab7579f13264b01b2e1c3f2694.setIcon(div_icon_c75db25f7fb3854a003daa412b68a800);
        
    
            var marker_e626a1bca6dce14e87f40caa97d0319d = L.marker(
                [51.485905, -0.282526],
                {}
            ).addTo(map_8a6d3947593db6f964f4af195e39415e);
        
    
            var icon_0292927423f93849079d47b40c018221 = L.AwesomeMarkers.icon(
                {"extraClasses": "fa-rotate-0", "icon": "info-sign", "iconColor": "white", "markerColor": "red", "prefix": "glyphicon"}
            );
            marker_e626a1bca6dce14e87f40caa97d0319d.setIcon(icon_0292927423f93849079d47b40c018221);
        
    
        var popup_74cfbb7f63d54395065ef41721300e86 = L.popup({"maxWidth": "100%", "permanent": true});

        
            
                var html_c0af9c0e87b8b975f1e27cb36ca75e47 = $(`<div id="html_c0af9c0e87b8b975f1e27cb36ca75e47" style="width: 100.0%; height: 100.0%;">TKB</div>`)[0];
                popup_74cfbb7f63d54395065ef41721300e86.setContent(html_c0af9c0e87b8b975f1e27cb36ca75e47);
            
        

        marker_e626a1bca6dce14e87f40caa97d0319d.bindPopup(popup_74cfbb7f63d54395065ef41721300e86)
        ;

        
    
    
            var marker_2899854bb28865839c255eebfe4bd491 = L.marker(
                [51.485905, -0.282526],
                {}
            ).addTo(map_8a6d3947593db6f964f4af195e39415e);
        
    
            var div_icon_513893dc13670250825094e942caaa01 = L.divIcon({"className": "empty", "html": "\u003cdiv style=\u0027font-size: 16px; color: blue; font-weight: bold;\u0027\u003eTKB\u003c/div\u003e", "iconAnchor": [10, 0], "iconSize": [150, 36]});
            marker_2899854bb28865839c255eebfe4bd491.setIcon(div_icon_513893dc13670250825094e942caaa01);
        
    
            var marker_8e343461f78a8803f754949f0b83271d = L.marker(
                [51.482289, -0.250819],
                {}
            ).addTo(map_8a6d3947593db6f964f4af195e39415e);
        
    
            var icon_b8d3fbdc616f4a1dbc5fc98165705914 = L.AwesomeMarkers.icon(
                {"extraClasses": "fa-rotate-0", "icon": "info-sign", "iconColor": "white", "markerColor": "red", "prefix": "glyphicon"}
            );
            marker_8e343461f78a8803f754949f0b83271d.setIcon(icon_b8d3fbdc616f4a1dbc5fc98165705914);
        
    
        var popup_03555efecb32f669a27d38631cf2cafb = L.popup({"maxWidth": "100%", "permanent": true});

        
            
                var html_17f687c5d2092c78bbbe5f8394f13f30 = $(`<div id="html_17f687c5d2092c78bbbe5f8394f13f30" style="width: 100.0%; height: 100.0%;">TChP</div>`)[0];
                popup_03555efecb32f669a27d38631cf2cafb.setContent(html_17f687c5d2092c78bbbe5f8394f13f30);
            
        

        marker_8e343461f78a8803f754949f0b83271d.bindPopup(popup_03555efecb32f669a27d38631cf2cafb)
        ;

        
    
    
            var marker_c366c19d1ccd45d3209ce2f9362e7645 = L.marker(
                [51.482289, -0.250819],
                {}
            ).addTo(map_8a6d3947593db6f964f4af195e39415e);
        
    
            var div_icon_3f134532b7c372f441d231d1f3cba5a2 = L.divIcon({"className": "empty", "html": "\u003cdiv style=\u0027font-size: 16px; color: blue; font-weight: bold;\u0027\u003eTChP\u003c/div\u003e", "iconAnchor": [10, 0], "iconSize": [150, 36]});
            marker_c366c19d1ccd45d3209ce2f9362e7645.setIcon(div_icon_3f134532b7c372f441d231d1f3cba5a2);
        
    
            var marker_9efc5f110f791edc1446cadecc316f45 = L.marker(
                [51.489988, -0.234693],
                {}
            ).addTo(map_8a6d3947593db6f964f4af195e39415e);
        
    
            var icon_20caf2dbdc423150331f75bf55371779 = L.AwesomeMarkers.icon(
                {"extraClasses": "fa-rotate-0", "icon": "info-sign", "iconColor": "white", "markerColor": "red", "prefix": "glyphicon"}
            );
            marker_9efc5f110f791edc1446cadecc316f45.setIcon(icon_20caf2dbdc423150331f75bf55371779);
        
    
        var popup_f985636280921141fb23e280429c1dcb = L.popup({"maxWidth": "100%", "permanent": true});

        
            
                var html_f2975ff548c0019a984dc53068113003 = $(`<div id="html_f2975ff548c0019a984dc53068113003" style="width: 100.0%; height: 100.0%;">TH</div>`)[0];
                popup_f985636280921141fb23e280429c1dcb.setContent(html_f2975ff548c0019a984dc53068113003);
            
        

        marker_9efc5f110f791edc1446cadecc316f45.bindPopup(popup_f985636280921141fb23e280429c1dcb)
        ;

        
    
    
            var marker_362aa351cf9636c2f53e1bd93ddd617a = L.marker(
                [51.489988, -0.234693],
                {}
            ).addTo(map_8a6d3947593db6f964f4af195e39415e);
        
    
            var div_icon_0573a9fd85b6ebbf498a275b3d9b29e9 = L.divIcon({"className": "empty", "html": "\u003cdiv style=\u0027font-size: 16px; color: blue; font-weight: bold;\u0027\u003eTH\u003c/div\u003e", "iconAnchor": [10, 0], "iconSize": [150, 36]});
            marker_362aa351cf9636c2f53e1bd93ddd617a.setIcon(div_icon_0573a9fd85b6ebbf498a275b3d9b29e9);
        
    
            var marker_e2cfb197952f0411d52e162dd653062d = L.marker(
                [51.467322, -0.215383],
                {}
            ).addTo(map_8a6d3947593db6f964f4af195e39415e);
        
    
            var icon_efc8b103ffb9cedc24cf5c21b056f854 = L.AwesomeMarkers.icon(
                {"extraClasses": "fa-rotate-0", "icon": "info-sign", "iconColor": "white", "markerColor": "red", "prefix": "glyphicon"}
            );
            marker_e2cfb197952f0411d52e162dd653062d.setIcon(icon_efc8b103ffb9cedc24cf5c21b056f854);
        
    
        var popup_427bf742d3640a68199d3b419d62159f = L.popup({"maxWidth": "100%", "permanent": true});

        
            
                var html_8233ca9d0eb0ad80e011d1744d3f3c36 = $(`<div id="html_8233ca9d0eb0ad80e011d1744d3f3c36" style="width: 100.0%; height: 100.0%;">TPut</div>`)[0];
                popup_427bf742d3640a68199d3b419d62159f.setContent(html_8233ca9d0eb0ad80e011d1744d3f3c36);
            
        

        marker_e2cfb197952f0411d52e162dd653062d.bindPopup(popup_427bf742d3640a68199d3b419d62159f)
        ;

        
    
    
            var marker_b257eee7f56af104afa9dd9d700f5067 = L.marker(
                [51.467322, -0.215383],
                {}
            ).addTo(map_8a6d3947593db6f964f4af195e39415e);
        
    
            var div_icon_f944fcbc78268c29ed964e0d30d51f70 = L.divIcon({"className": "empty", "html": "\u003cdiv style=\u0027font-size: 16px; color: blue; font-weight: bold;\u0027\u003eTPut\u003c/div\u003e", "iconAnchor": [10, 0], "iconSize": [150, 36]});
            marker_b257eee7f56af104afa9dd9d700f5067.setIcon(div_icon_f944fcbc78268c29ed964e0d30d51f70);
        
    
            var marker_453c43a6d3af01cd533a3d14bd1ce3fc = L.marker(
                [51.483087, -0.165929],
                {}
            ).addTo(map_8a6d3947593db6f964f4af195e39415e);
        
    
            var icon_9861992054a238abd2517320f6c2387a = L.AwesomeMarkers.icon(
                {"extraClasses": "fa-rotate-0", "icon": "info-sign", "iconColor": "white", "markerColor": "red", "prefix": "glyphicon"}
            );
            marker_453c43a6d3af01cd533a3d14bd1ce3fc.setIcon(icon_9861992054a238abd2517320f6c2387a);
        
    
        var popup_df5715035b7b2b41603e74545f587aef = L.popup({"maxWidth": "100%", "permanent": true});

        
            
                var html_f20225804cf0265a19bc63f8c07e12eb = $(`<div id="html_f20225804cf0265a19bc63f8c07e12eb" style="width: 100.0%; height: 100.0%;">TCaP</div>`)[0];
                popup_df5715035b7b2b41603e74545f587aef.setContent(html_f20225804cf0265a19bc63f8c07e12eb);
            
        

        marker_453c43a6d3af01cd533a3d14bd1ce3fc.bindPopup(popup_df5715035b7b2b41603e74545f587aef)
        ;

        
    
    
            var marker_84459058edb040bc9e0939daa9247788 = L.marker(
                [51.483087, -0.165929],
                {}
            ).addTo(map_8a6d3947593db6f964f4af195e39415e);
        
    
            var div_icon_f6b54c0023aac187e226754a008465ad = L.divIcon({"className": "empty", "html": "\u003cdiv style=\u0027font-size: 16px; color: blue; font-weight: bold;\u0027\u003eTCaP\u003c/div\u003e", "iconAnchor": [10, 0], "iconSize": [150, 36]});
            marker_84459058edb040bc9e0939daa9247788.setIcon(div_icon_f6b54c0023aac187e226754a008465ad);
        
    
            var marker_f0e6587cbd603a7c31a2a7df3a382879 = L.marker(
                [51.495672, 0.041657],
                {}
            ).addTo(map_8a6d3947593db6f964f4af195e39415e);
        
    
            var icon_11cbdd6bf521ecf8f0a69da264d09d8b = L.AwesomeMarkers.icon(
                {"extraClasses": "fa-rotate-0", "icon": "info-sign", "iconColor": "white", "markerColor": "red", "prefix": "glyphicon"}
            );
            marker_f0e6587cbd603a7c31a2a7df3a382879.setIcon(icon_11cbdd6bf521ecf8f0a69da264d09d8b);
        
    
        var popup_747503e78e68f8aa5518245d461326bb = L.popup({"maxWidth": "100%", "permanent": true});

        
            
                var html_f7682e3770cf4c9468689ceb280d24f5 = $(`<div id="html_f7682e3770cf4c9468689ceb280d24f5" style="width: 100.0%; height: 100.0%;">TBGP</div>`)[0];
                popup_747503e78e68f8aa5518245d461326bb.setContent(html_f7682e3770cf4c9468689ceb280d24f5);
            
        

        marker_f0e6587cbd603a7c31a2a7df3a382879.bindPopup(popup_747503e78e68f8aa5518245d461326bb)
        ;

        
    
    
            var marker_1527e0b628c01691593c3aec8c699d1e = L.marker(
                [51.495672, 0.041657],
                {}
            ).addTo(map_8a6d3947593db6f964f4af195e39415e);
        
    
            var div_icon_8b53c1b063fb18c66f365f35a84bf9f9 = L.divIcon({"className": "empty", "html": "\u003cdiv style=\u0027font-size: 16px; color: blue; font-weight: bold;\u0027\u003eTBGP\u003c/div\u003e", "iconAnchor": [10, 0], "iconSize": [150, 36]});
            marker_1527e0b628c01691593c3aec8c699d1e.setIcon(div_icon_8b53c1b063fb18c66f365f35a84bf9f9);
        
    
            var marker_541dbc401e9caaa1ddbe62e1a0068c5a = L.marker(
                [51.504281, 0.167781],
                {}
            ).addTo(map_8a6d3947593db6f964f4af195e39415e);
        
    
            var icon_26d2dd2410e9d2c78c5c815fbae7e478 = L.AwesomeMarkers.icon(
                {"extraClasses": "fa-rotate-0", "icon": "info-sign", "iconColor": "white", "markerColor": "red", "prefix": "glyphicon"}
            );
            marker_541dbc401e9caaa1ddbe62e1a0068c5a.setIcon(icon_26d2dd2410e9d2c78c5c815fbae7e478);
        
    
        var popup_4f6e2c5b06728408ce5de15b756fb8b5 = L.popup({"maxWidth": "100%", "permanent": true});

        
            
                var html_d6a2295e6d079e2af89ef0dd439f110f = $(`<div id="html_d6a2295e6d079e2af89ef0dd439f110f" style="width: 100.0%; height: 100.0%;">TEB</div>`)[0];
                popup_4f6e2c5b06728408ce5de15b756fb8b5.setContent(html_d6a2295e6d079e2af89ef0dd439f110f);
            
        

        marker_541dbc401e9caaa1ddbe62e1a0068c5a.bindPopup(popup_4f6e2c5b06728408ce5de15b756fb8b5)
        ;

        
    
    
            var marker_2bf02caa119b28d3f25a2b937c043be0 = L.marker(
                [51.504281, 0.167781],
                {}
            ).addTo(map_8a6d3947593db6f964f4af195e39415e);
        
    
            var div_icon_e35f637925bb1a29200bd6e06dc0409c = L.divIcon({"className": "empty", "html": "\u003cdiv style=\u0027font-size: 16px; color: blue; font-weight: bold;\u0027\u003eTEB\u003c/div\u003e", "iconAnchor": [10, 0], "iconSize": [150, 36]});
            marker_2bf02caa119b28d3f25a2b937c043be0.setIcon(div_icon_e35f637925bb1a29200bd6e06dc0409c);
        
    
            var marker_a51550a4a35b919d8ff38236b06b06a5 = L.marker(
                [51.470424, 0.250742],
                {}
            ).addTo(map_8a6d3947593db6f964f4af195e39415e);
        
    
            var icon_be55944b06e55bbee2bfb76e66ce3ab0 = L.AwesomeMarkers.icon(
                {"extraClasses": "fa-rotate-0", "icon": "info-sign", "iconColor": "white", "markerColor": "red", "prefix": "glyphicon"}
            );
            marker_a51550a4a35b919d8ff38236b06b06a5.setIcon(icon_be55944b06e55bbee2bfb76e66ce3ab0);
        
    
        var popup_97d655b2366ce1600845fe0d83050b1e = L.popup({"maxWidth": "100%", "permanent": true});

        
            
                var html_cbb852c3429292aa9dafd558ba0fdec2 = $(`<div id="html_cbb852c3429292aa9dafd558ba0fdec2" style="width: 100.0%; height: 100.0%;">TPur</div>`)[0];
                popup_97d655b2366ce1600845fe0d83050b1e.setContent(html_cbb852c3429292aa9dafd558ba0fdec2);
            
        

        marker_a51550a4a35b919d8ff38236b06b06a5.bindPopup(popup_97d655b2366ce1600845fe0d83050b1e)
        ;

        
    
    
            var marker_37fba254c1b606303f2b132bf62b6305 = L.marker(
                [51.470424, 0.250742],
                {}
            ).addTo(map_8a6d3947593db6f964f4af195e39415e);
        
    
            var div_icon_8e4b3cc7232c97aa10143cd14f0f92d5 = L.divIcon({"className": "empty", "html": "\u003cdiv style=\u0027font-size: 16px; color: blue; font-weight: bold;\u0027\u003eTPur\u003c/div\u003e", "iconAnchor": [10, 0], "iconSize": [150, 36]});
            marker_37fba254c1b606303f2b132bf62b6305.setIcon(div_icon_8e4b3cc7232c97aa10143cd14f0f92d5);
        
</script>
</html>ading Sites_map.html…]()


## The data processing
Process the data: Import the raw data into the Jupyter Notebook file named *dataframe.ipynb*. Apply robust filtering techniques to remove any faulty or inaccurate measurements. 
The data sets retrieved contain several problems. Below are some of the main issues and the ways in which we rectify them:
1. DO and DO-MGL parameters not considered, instead use the DOO-MGL parameter measured with an optical optode for more reliable data. 'DOO-MGL' is equivalent to the commonly known 'DO' in this project.
1. DO measurements exceeding 25mg/L are deemed faulty and discarded, as achieving a concentration as high as 25mg/L is generally unlikely under standard conditions.
2. Remove non-positive measurements for ’COND’, ’PH’, ’AMMONIUM’, ’Turbidity’ and ’DO’ indicators.
3. Remove large spikes and sudden dropouts due to probe faults or human activities, such as the
oxygen pumped into the river from a boat in August 2022.
4. COND measurements in ms/cm unit, change to us/cm.
5. Remove data outages, which were caused by sonde changes.

Save the cleaned data in your folder for further analysis.


## Superstatistical analysis
### Statistical Anlysis
Run the "Statistical_analysis.ipynb" notebook to visualize the trajectories and probability density functions (PDFs) of the time series data from the measured sites.

### Detrending
Our approach focuses on describing fluctuations around the mean rather than modeling the complete distribution. Execute the notebooks "Detrending-additive.ipynb" and "Detrending-multiplicative.ipynb" for additive and multiplicative detrending methods, respectively.

### Superstatistical Results
The fluctuations deduced from the detrending methods can be well modeled by q-Gaussian distributions, as demonstrated by the results in "Detrending-additive.ipynb" and "Detrending-multiplicative.ipynb". Save the log-likelihood results and parameters for the best-fitting q-Gaussians, then run "Superstatistical results.ipynb". This notebook compares the robustness of different detrending methods and displays the spatial plot of parameters.


## Regression analysis

In this section, we compare the LGBM regression model to the XGBoost and linear regression baselines, in both SMAPE and the SHAP values of each of the features. Each model has its own notebook file: LGBM_basic.ipynb for LGBM regression, XGBoost_baseline.ipynb for XGBoost, and Linear_Regression_baseline.ipynb for linear regression. For each method, set the path to your local path to the site data being tested and uncomment the appropriate features.



## Sequential forecasting 

In this section, we compare numerous effective existing forecast models with the recently developed transformer, namely Informer, which is the state-of-the-art machine learning techniques. This techinques are based on [Time series forecasting](https://github.com/tensorflow/docs/blob/master/site/en/tutorials/structured_data/time_series.ipynb) and [Informer2020](https://github.com/zhouhaoyi/Informer2020). Modifications were made to suit the water quality time series.

1. Choose a specific dataset from one site and import it into another Jupyter Notebook file named time_series_forecasting.ipynb. Execute the notebook ten times and calculate the average of the mean absolute error (MAE) to evaluate model performance.
   
2. Finnaly,import the data to *Informer2020* folder, and run the *informer.ipynb*, where you can set the input, label and prediction lengths. The performance evaluation will be saved in the *metrics.npy* in the *results* folder.

3. Compare the MAE from all models and deduce the model with the best predictive capability.

