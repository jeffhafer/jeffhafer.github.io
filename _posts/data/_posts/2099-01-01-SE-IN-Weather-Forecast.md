---
categories: ['data']
layout: post
title: SE IN Weather Forecast
published: true
---
<html lang="en" xml:lang="en" xmlns="http://www.w3.org/1999/xhtml">
	<head>
		<title>Weather</title>
	    	<meta charset="utf-8"/>
		<link rel="icon" href="http://hafer.net/favicons/weather.ico" type="image/x-icon"> 
		<script src='https://ajax.googleapis.com/ajax/libs/jquery/1.7.1/jquery.min.js'></script>
		<style>
			.b{font-weight: bold;}
			body{}
			.inv{
				display: none;
			}
			#div_maps img{
				width: 100%;
			}
			#div_maps table{
				width: 100%;
			}
			#div_maps td{
				text-align: center;
				width: 50%;
			}
			.div_temp{
				visibility: hidden;
			}
			#tbl_hourly td{
				border: 1px solid lightgrey;
			    text-align: center;
				width: 5.88%;
			}
			#tbl_out, #tbl_hourly{
				border: 1px solid black;
				text-align: center;
				width: 100%;
			}
			#tbl_out img, #tbl_hourly img{
				width: 50px;
			}
			#tbl_out td{
				border: 1px solid lightgrey;
			    text-align: center;
				width: 9.09%;
			}
		</style>
	</head>
	<body>
		<div id='div_out'></div>
		<br>
		<div id='div_hourly'></div>
		<p></p>
		<div id='div_maps'></div>
		<div class='div_temp' id='t0'></div>
		<div class='div_temp' id='t1'></div>
		<div class='div_temp' id='t2'></div>
		<div class='div_temp' id='t3'></div>
		<div class='div_temp' id='t4'></div>
		<div class='div_temp' id='t5'></div>
		<div class='div_temp' id='t6'></div>
		<div class='div_temp' id='t7'></div>
		<div class='div_temp' id='t8'></div>
		<div class='div_temp' id='t9'></div>
	</body>
	<script>
		$(document).ready(function(){
			//Create the grids 
			var h = "";
			h += "<table id='tbl_out' cellpadding=0 cellspacing=0>";
			h += "<tr><td>Date</td>		<td><span id='date0'></span></td>	<td><span id='date1'></span></td>	<td><span id='date2'></span></td>	<td><span id='date3'></span></td>	<td><span id='date4'></span></td>	<td><span id='date5'></span></td>	<td><span id='date6'></span></td>	<td><span id='date7'></span></td>	<td><span id='date8'></span></td>	<td><span id='date9'></span></td></tr>";
			h += "<tr><td>&nbsp;</td>	<td><span id='day0'></span></td>	<td><span id='day1'></span></td>	<td><span id='day2'></span></td>	<td><span id='day3'></span></td>	<td><span id='day4'></span></td>	<td><span id='day5'></span></td>	<td><span id='day6'></span></td>	<td><span id='day7'></span></td>	<td><span id='day8'></span></td>	<td><span id='day9'></span></td></tr>";
			h += "<tr><td>&nbsp;</td>	<td><span id='img0'></span></td>	<td><span id='img1'></span></td>	<td><span id='img2'></span></td>	<td><span id='img3'></span></td>	<td><span id='img4'></span></td>	<td><span id='img5'></span></td>	<td><span id='img6'></span></td>	<td><span id='img7'></span></td>	<td><span id='img8'></span></td>	<td><span id='img9'></span></td></tr>";
			h += "<tr><td>High</td>		<td><span id='high0'></span></td>	<td><span id='high1'></span></td>	<td><span id='high2'></span></td>	<td><span id='high3'></span></td>	<td><span id='high4'></span></td>	<td><span id='high5'></span></td>	<td><span id='high6'></span></td>	<td><span id='high7'></span></td>	<td><span id='high8'></span></td>	<td><span id='high9'></span></td></tr>";
			h += "<tr><td>Low</td>		<td><span id='low0'></span></td>	<td><span id='low1'></span></td>	<td><span id='low2'></span></td>	<td><span id='low3'></span></td>	<td><span id='low4'></span></td>	<td><span id='low5'></span></td>	<td><span id='low6'></span></td>	<td><span id='low7'></span></td>	<td><span id='low8'></span></td>	<td><span id='low9'></span></td></tr>";
			h += "<tr><td>Precip%</td>	<td><span id='prec0'></span></td>	<td><span id='prec1'></span></td>	<td><span id='prec2'></span></td>	<td><span id='prec3'></span></td>	<td><span id='prec4'></span></td>	<td><span id='prec5'></span></td>	<td><span id='prec6'></span></td>	<td><span id='prec7'></span></td>	<td><span id='prec8'></span></td>	<td><span id='prec9'></span></td></tr>";
			h += "<tr><td>Humid</td>	<td><span id='hum0'></span></td>	<td><span id='hum1'></span></td>	<td><span id='hum2'></span></td>	<td><span id='hum3'></span></td>	<td><span id='hum4'></span></td>	<td><span id='hum5'></span></td>	<td><span id='hum6'></span></td>	<td><span id='hum7'></span></td>	<td><span id='hum8'></span></td>	<td><span id='hum9'></span></td></tr>";
			h += "<tr><td>Wind</td>		<td><span id='wind0'></span></td>	<td><span id='wind1'></span></td>	<td><span id='wind2'></span></td>	<td><span id='wind3'></span></td>	<td><span id='wind4'></span></td>	<td><span id='wind5'></span></td>	<td><span id='wind6'></span></td>	<td><span id='wind7'></span></td>	<td><span id='wind8'></span></td>	<td><span id='wind9'></span></td></tr>";
			h += "<tr><td>Avg H</td>	<td><span id='avgh0'></span></td>	<td><span id='avgh1'></span></td>	<td><span id='avgh2'></span></td>	<td><span id='avgh3'></span></td>	<td><span id='avgh4'></span></td>	<td><span id='avgh5'></span></td>	<td><span id='avgh6'></span></td>	<td><span id='avgh7'></span></td>	<td><span id='avgh8'></span></td>	<td><span id='avgh9'></span></td></tr>";
			h += "<tr><td>Avg L</td>	<td><span id='avgl0'></span></td>	<td><span id='avgl1'></span></td>	<td><span id='avgl2'></span></td>	<td><span id='avgl3'></span></td>	<td><span id='avgl4'></span></td>	<td><span id='avgl5'></span></td>	<td><span id='avgl6'></span></td>	<td><span id='avgl7'></span></td>	<td><span id='avgl8'></span></td>	<td><span id='avgl9'></span></td></tr>";
			h += "<tr><td>Rec H</td>	<td><span id='rech0'></span></td>	<td><span id='rech1'></span></td>	<td><span id='rech2'></span></td>	<td><span id='rech3'></span></td>	<td><span id='rech4'></span></td>	<td><span id='rech5'></span></td>	<td><span id='rech6'></span></td>	<td><span id='rech7'></span></td>	<td><span id='rech8'></span></td>	<td><span id='rech9'></span></td></tr>";
			h += "<tr><td>Rec L</td>	<td><span id='recl0'></span></td>	<td><span id='recl1'></span></td>	<td><span id='recl2'></span></td>	<td><span id='recl3'></span></td>	<td><span id='recl4'></span></td>	<td><span id='recl5'></span></td>	<td><span id='recl6'></span></td>	<td><span id='recl7'></span></td>	<td><span id='recl8'></span></td>	<td><span id='recl9'></span></td></tr>";
			h += "</table>";
			$("#div_out").html(h);
            var h = "";
			h += "<table id='tbl_hourly' cellpadding=0 cellspacing=0>";
			h += "<tr><td>Time</td>		<td><span id='time0'></span></td>	<td><span id='time1'></span></td>	<td><span id='time2'></span></td>	<td><span id='time3'></span></td>	<td><span id='time4'></span></td>	<td><span id='time5'></span></td>	<td><span id='time6'></span></td>	<td><span id='time7'></span></td>	<td><span id='time8'></span></td>	<td><span id='time9'></span></td>   <td><span id='time10'></span></td>   <td><span id='time11'></span></td>   <td><span id='time12'></span></td>    <td><span id='time13'></span></td>  <td><span id='time14'></span></td>  <td><span id='time15'></span></td></tr>";
			h += "<tr><td>Temp</td>	    <td><span id='temp0'></span></td>	<td><span id='temp1'></span></td>	<td><span id='temp2'></span></td>	<td><span id='temp3'></span></td>	<td><span id='temp4'></span></td>	<td><span id='temp5'></span></td>	<td><span id='temp6'></span></td>	<td><span id='temp7'></span></td>	<td><span id='temp8'></span></td>	<td><span id='temp9'></span></td>   <td><span id='temp10'></span></td>   <td><span id='temp11'></span></td>   <td><span id='temp12'></span></td>   <td><span id='temp13'></span></td>   <td><span id='temp14'></span></td>   <td><span id='temp15'></span></td></tr>";
			h += "<tr><td>&nbsp;</td>	<td><span id='img20'></span></td>	<td><span id='img21'></span></td>	<td><span id='img22'></span></td>	<td><span id='img23'></span></td>	<td><span id='img24'></span></td>	<td><span id='img25'></span></td>	<td><span id='img26'></span></td>	<td><span id='img27'></span></td>	<td><span id='img28'></span></td>	<td><span id='img29'></span></td>   <td><span id='img210'></span></td>   <td><span id='img211'></span></td>   <td><span id='img212'></span></td>   <td><span id='img213'></span></td>   <td><span id='img214'></span></td>   <td><span id='img215'></span></td></tr>";
			h += "<tr><td>Humid</td>	<td><span id='hum20'></span></td>	<td><span id='hum21'></span></td>	<td><span id='hum22'></span></td>	<td><span id='hum23'></span></td>	<td><span id='hum24'></span></td>	<td><span id='hum25'></span></td>	<td><span id='hum26'></span></td>	<td><span id='hum27'></span></td>	<td><span id='hum28'></span></td>	<td><span id='hum29'></span></td>   <td><span id='hum210'></span></td>   <td><span id='hum211'></span></td>   <td><span id='hum212'></span></td>   <td><span id='hum213'></span></td>   <td><span id='hum214'></span></td>   <td><span id='hum215'></span></td></tr>";
			h += "<tr><td>Precip%</td>	<td><span id='pop20'></span></td>	<td><span id='pop21'></span></td>	<td><span id='pop22'></span></td>	<td><span id='pop23'></span></td>	<td><span id='pop24'></span></td>	<td><span id='pop25'></span></td>	<td><span id='pop26'></span></td>	<td><span id='pop27'></span></td>	<td><span id='pop28'></span></td>	<td><span id='pop29'></span></td>   <td><span id='pop210'></span></td>   <td><span id='pop211'></span></td>   <td><span id='pop212'></span></td>   <td><span id='pop213'></span></td>   <td><span id='pop214'></span></td>   <td><span id='pop215'></span></td></tr>";
			h += "<tr><td>Rain</td>	    <td><span id='rain0'></span></td>	<td><span id='rain1'></span></td>	<td><span id='rain2'></span></td>	<td><span id='rain3'></span></td>	<td><span id='rain4'></span></td>	<td><span id='rain5'></span></td>	<td><span id='rain6'></span></td>	<td><span id='rain7'></span></td>	<td><span id='rain8'></span></td>	<td><span id='rain9'></span></td>   <td><span id='rain10'></span></td>   <td><span id='rain11'></span></td>   <td><span id='rain12'></span></td>   <td><span id='rain13'></span></td>   <td><span id='rain14'></span></td>   <td><span id='rain15'></span></td></tr>";
			h += "<tr><td>Snow</td>	    <td><span id='snow0'></span></td>	<td><span id='snow1'></span></td>	<td><span id='snow2'></span></td>	<td><span id='snow3'></span></td>	<td><span id='snow4'></span></td>	<td><span id='snow5'></span></td>	<td><span id='snow6'></span></td>	<td><span id='snow7'></span></td>	<td><span id='snow8'></span></td>	<td><span id='snow9'></span></td>   <td><span id='snow10'></span></td>   <td><span id='snow11'></span></td>   <td><span id='snow12'></span></td>   <td><span id='snow13'></span></td>   <td><span id='snow14'></span></td>   <td><span id='snow15'></span></td></tr>";
			h += "<tr><td>Wind</td>	    <td><span id='wind20'></span></td>	<td><span id='wind21'></span></td>	<td><span id='wind22'></span></td>	<td><span id='wind23'></span></td>	<td><span id='wind24'></span></td>	<td><span id='wind25'></span></td>	<td><span id='wind26'></span></td>	<td><span id='wind27'></span></td>	<td><span id='wind28'></span></td>	<td><span id='wind29'></span></td>  <td><span id='wind210'></span></td>  <td><span id='wind211'></span></td>  <td><span id='wind212'></span></td>  <td><span id='wind213'></span></td>  <td><span id='wind214'></span></td>  <td><span id='wind215'></span></td></tr>";
			h += "<tr><td>WChill</td>	<td><span id='wc0'></span></td>	    <td><span id='wc1'></span></td>	    <td><span id='wc2'></span></td>	    <td><span id='wc3'></span></td>	    <td><span id='wc4'></span></td>	    <td><span id='wc5'></span></td>	    <td><span id='wc6'></span></td>	    <td><span id='wc7'></span></td>	    <td><span id='wc8'></span></td>	    <td><span id='wc9'></span></td>     <td><span id='wc10'></span></td>     <td><span id='wc11'></span></td>     <td><span id='wc12'></span></td>     <td><span id='wc13'></span></td>     <td><span id='wc14'></span></td>     <td><span id='wc15'></span></td></tr>";			
			h += "</table>";
			$("#div_hourly").html(h);
			var url = [];
			$.getJSON( "https://api-ak.wunderground.com/api/c991975b7f4186c0/forecast10day/hourly10day/labels/astronomy10day/lang:EN/units:english/v:2.0/bestfct:1/q/zmw:47006.1.99999.json?ttl=300", function( jd ) {
				$.each(jd.forecast.days, function(i,day){
					$("#date" + i).html(day.summary.date.month + "/" + day.summary.date.day);
					$("#day" + i).html(day.summary.date.weekday_short);
					$("#high" + i).html(day.summary.high);
					$("#low" + i).html(day.summary.low);
					$("#img" + i).html("<img src='http:" + day.summary.icon_url + "'>");
					$("#prec" + i).html(day.summary.pop + '%');
					$("#hum" + i).html(day.summary.humidity_max + "-" + day.summary.humidity_min);
					$("#wind" + i).html(day.summary.wind_max_speed + ' ' + day.summary.wind_max_dir);
				});
				for (var ii=0; ii<10; ii++){
                    var today = new Date(Date.now() + 24 * 60 * 60 * 1000 * (ii+1) );
                    var d = today.getDate();
                    var mon = today.getMonth()+1;
                    if (d<10){ d = '0' + d; }
                    if (mon<10){ mon = '0' + mon; }
				    var url = "https://api-ak.wunderground.com/api/d8585d80376a429e/history_2012" + mon + d + "/lang:EN/units:english/bestfct:1/v:2.0/q/KCVG.json?showObs=0&ttl=120";
				    var c = 0;
					$.getJSON(url, function(json){
				        var max_temp =        json.history.days[0].summary.max_temperature_record;
				        var max_temp_normal = json.history.days[0].summary.max_temperature_normal;
				        var max_temp_year =   json.history.days[0].summary.max_temperature_record_year;
				        var min_temp =        json.history.days[0].summary.min_temperature_record;
				        var min_temp_normal = json.history.days[0].summary.min_temperature_normal;
				        var min_temp_year =   json.history.days[0].summary.min_temperature_record_year;
				        $("#avgh" + c).html( max_temp_normal );
				        $("#avgl" + c).html( min_temp_normal );
				        $("#rech" + c).html( max_temp + " (" + max_temp_year + ")" );
				        $("#recl" + c).html( min_temp + " (" + min_temp_year + ")" );
				        c++;
					});
				}
          		$.each(jd.forecast.days[0].hours, function(i,hour){
          		    var hr = hour.date.iso8601.split("T");
          		    var hr = hr[1].split(":");
          		    var hr = hr[0];
                    $("#time" + i).html(hr + ":00");
                    $("#temp" + i).html(hour.temperature);
                    $("#wc" + i).html(hour.windchill);
                    $("#img2" + i).html("<img src='http:" + hour.icon_url + "'>");
                    $("#hum2" + i).html(hour.humidity + "-" + hour.humidity);
                    $("#pop2" + i).html(hour.pop + '%');
                    $("#rain" + i).html(hour.liquid_precip);
                    $("#snow" + i).html(hour.snow);
                    $("#wind2" + i).html(hour.wind_speed + ' ' + hour.wind_dir);
          		});
          		//If necessary, use the hourly forecast from days[1] to complete the data in the hourly table
          		var time0 = parseInt($("#time0").html());
          		if (time0 > 8){
          		    var count = 1;
          		    //Fill in the appropriate info from day1
          		    $.each(jd.forecast.days[1].hours, function(i,hour){
          		        var hr = hour.date.iso8601.split("T");
          		        var hr = hr[1].split(":");
          		        var hr = hr[0];
                        var offset = (23 - time0) + count;
                        $("#time" + offset).html(hr + ":00");
                        $("#temp" + offset).html(hour.temperature);
                        $("#wc" + offset).html(hour.windchill);
                        $("#img2" + offset).html("<img src='https:" + hour.icon_url + "'>");
                        $("#hum2" + offset).html(hour.humidity + "-" + hour.humidity);
                        $("#pop2" + offset).html(hour.pop + '%');
                        $("#rain" + offset).html(hour.liquid_precip);
                        $("#snow" + offset).html(hour.snow);
                        $("#wind2" + offset).html(hour.wind_speed + ' ' + hour.wind_dir);
                        count++;
          		    });
          		}
			});
		});
		//Add the map table
		var h = "";
		h += "<table border=0 cellpadding=0 cellspacing=1 width=100%>";
		h += "	  <tr>";
		h += "		<td width=50%><img src='http://radblast-aws.wunderground.com/cgi-bin/radar/WUNIDS_map?station=IND&brand=wui&num=10&delay=15&type=N0R&frame=0&scale=1.000&noclutter=0&t=1368730983&lat=0&lon=0&label=you&showstorms=0&map.x=400&map.y=240&centerx=400&centery=240&transx=0&transy=0&showlabels=1&severe=0&rainsnow=0&lightning=0&smooth=0' alt='map' /></td>";
		h += "		<td width=50%><img src='http://services.intellicast.com/200904-01/576347879/Image/Radar/Radar2009.13L/Loop/SectorName/usa' alt='map' /></td>";
		h += "</tr><tr>";
		h += "		<td valign=top width=50%><center><img src='http://images.intellicast.com/WxImages/CustomGraphic/wg30t.gif' alt='map' /></center></td>";
		h += "<td valign=top width=50%><center><img src='https://s.w-x.co/staticmaps/WEB_48hour_rain_snow_1280x720.jpg' alt='map'/></center></td>";
		h += "</tr><tr>";
		h += "<td valign=top width=50%><center><img src='https://s.w-x.co/staticmaps/CPC_30_DAY_PRECIP_1280x720.jpg' alt='map'/></center></td>";
		h += "<td valign=top width=50%><center><img src='https://s.w-x.co/staticmaps/CPC_90_DAY_PRECIP_1280x720.jpg' alt='map'/></center></td>";
		h += "</tr><tr>";
		h += "<td valign=top width=50%><center><img src='https://s.w-x.co/staticmaps/acttemp_1280x720.jpg' alt='map'/></center></td>";
		h += "<td valign=top width=50%><center><img src='https://s.w-x.co/staticmaps/us_wxlo1_1280x720.jpg' alt='map'/></center></td>";
		h += "</tr>";
		h += "</table>";
		$("#div_maps").html(h);
	</script>
</html>
<!--
	2018.11.08
		+ Migrated to a fully client-sdie app. No need for a proxy.
	2018.01.02 - 2018.01.03
		+ Add section showing hourly forecast out 16hrs
		+ Add Avg temps, Record temps and years to 10 day forecast
-->
