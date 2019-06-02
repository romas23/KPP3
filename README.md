# Лабораторна 3: Розробка браузерної аплікації
## Мета: Розробити статичний браузерну аплікацію, що отримує дані з відкритого API, та відображає їх на мапі.

![terminal1](wea.jpg)
```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Weather in Vinnitsa</title>
        <style>
            #map{
                height:600px;
                width:100%;
            }
        </style>
    </head>
    <body>
        <div id="map"></div>
        <script>
            let map;
            function initMap(){
                var options = {
                    zoom:8,
                    center:{lat:49.233083,lng:28.468217}
                }
                map = new google.maps.Map(document.getElementById("map"), options);
            }
        </script>
        <script async defer
        src="https://maps.googleapis.com/maps/api/js?key=AIzaSyDpE2OU2Ry6FlFizeTMNxI6gbZEmLdwDCM&callback=initMap">
        </script>
        <script>
			let Cities = ['Vinnytsia','Kiev','Lviv','Zhytomyr','Khmelnytskyi','Rivne','Ivano-Frankivsk','Ternopil','Chernivtsi','Chernihiv','Sumy','Cherkasy','Poltava','Kharkiv','Dnipro','Kremenchuk','Zaporizhzhia','Mykolayiv','Kherson','Donetsk','Luhansk','Berdyansk','Sevastopol']
			
			for(let i=0;i<Cities.length;i++){
				fetch(`https://api.openweathermap.org/data/2.5/weather?q=${Cities[i]}&appid=cb0c137d96d8019f2f8daf82d349e41f`)
                .then(function(response) {
                    response.json().then(function(data) {
                        const icon = data['weather'][0]['icon'];
                        const iconUrl = `http://openweathermap.org/img/w/${icon}.png`;
                        let lon = data['coord']['lon'];
						let lat = data['coord']['lat'];
                        var marker = new google.maps.Marker({
                            position:{lat:lat,lng:lon},
                            map:map,
                            icon: iconUrl
                        });
					});
				});
			}
			
        </script>
    </body>
</html>
```
