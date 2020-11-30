# Week 4.2 - Add functionality to your application


  - [Need to know](#need-to-know)
  - [Functions](#functions)
  - [Change forecast time](#change-forecast-time)
  - [Show outdoor areas on map](#show-outdoor-areas-on-map)
  - [Summary](#summary)
  

## Need to know

**Functions**: Are one of the fundamental building blocks in JavaScript. In JavaScript function is a block of code designed to perform a particular task and it is executed when "something" invokes it (calls it).  [Read more w3school JavaScript Functions](https://www.w3schools.com/js/js_functions.asp)

## Functions

To add functionality to an application, we need to use functions. Functions are blocks of code that perform a specific task. The basic syntax is
```html
function functionName (){
  //code
}
```
Let's say we want to have a button that you click and it prints a text to the page. First we need a page with a button and an element in which the text is printed, for example:
```html
    <button class="btn btn-info">Button</button> 
    <p id="someText"></p>
```
Then in the function we can use ```document.getElementById()``` to find the element we want to print text in and ```.innerHTML``` to put the text there.
So in the function we would have:

```html
<script>
    function myFunction() {
       document.getElementById("someText").innerHTML = "Hello you!";
    }
</script>
```
Since this is javascript inside an html document, we need to put the function inside script-tags.
The function won't be executed yet, because we haven't called it, so let's add a function call to the button:
```html
    <button class="btn btn-info" onclick="myFunction()">Button</button> 
    <p id="someText"></p>
```
Onclick is an event that executes a function once the button is clicked. The function name needs to be the same in the function call and the function inside script-tag, which in this case is "myFunction". Now we have a function that prints text to the page when it's clicked.  
Not clicked:    
<img src="/images/button_not_clicked.PNG" width="30%" height="50%">  
Clicked:  
<img src="/images/button_clicked.PNG" width="30%" height="50%">  

:bulb: Here is a full [example code](https://github.com/jenni-hautojarvi/cloud-rock-star-2020/blob/master/images/example_codes/button_click.html) of the previous

A function can also be given parameters inside parentheses (). So let's modify the code above to give the text printed on the page as a parameter instead.
```html
    <button class="btn btn-info" onclick="myFunction('Hello you!')">Button</button> 
    <p id="someText"></p>
```

```html
<script>
    function myFunction(text) {
       document.getElementById("someText").innerHTML = text;
    }
</script>
```
Note the use of ```' '``` when giving the desired text to myFunction in onclick. This code does the same thing as the previous code without a parameter. The benefit of parameters is, when we use the same function multiple times with different inputs, these inputs can be given as parameters. 

## Change forecast time

So far in the weather section we have fetched the current weather and weather forecast for two days at 12 o'clock. We can now try changing the time of the forecast by using functions. When we fetched forecast information, we looped through the information we got from weather api and used if statements to get the information we want. This was the code:  

```html
<script>
fetch("https://api.openweathermap.org/data/2.5/forecast?q=Helsinki&units=metric&&appid=YOURAPIKEY")
.then((response) => { 
	return response.json(); 
})
.then((weatherJson) => {
	console.log(weatherJson);
	var weatherArray = "";
	var count = 0;
	for(var i = 0; i < weatherJson.list.length; i++) { //Loop for going through the results for the forecast
		var time = weatherJson.list[i].dt_txt;	//eg. "2020-10-09 15:00:00"
		var hour = time.slice(11, 16);		//Separating the hour from time
		var date = time.slice(0, 10);		//Separating the date from time
		if(hour === "12:00"){			//If the hour is 12, data is stored to variables and then printed to console
			var description= weatherJson.list[i].weather[0].description;
			var temperature= weatherJson.list[i].main.temp;
			var icon = "https://openweathermap.org/img/wn/" + weatherJson.list[i].weather[0].icon + "@2x.png"; 
			console.log(date + " " + hour + " " + description + " " + temperature);
			weatherArray += "<div>Date: " + date + "<br>Hour: " +hour + "<br>Description: " + description + "<br>Temperature: " + temperature + "°C<br>" 
			+ "</div><div><img src=" + icon + "></img><br><br></div>";
			count++;
			if(count === 2){
				break;
			}
		}
	}
var futWeather = document.getElementById("futureWeather");
futWeather.innerHTML = weatherArray;
});
</script>
```
This code can be reused everytime we want to get weather information of different times. This is where functions are really useful. We don't have to write the same block of code over and over again, but use the same code everytime. So let's make the reusable part of previous code into a function: 

1. **Note! You can copy pase this after fetching Forecast. It will alert that function changeTime is not used. We will added it soon.**

```javascript

function changeTime(clock) {
    var weatherDiv = " ";
    var count = 0;

    //Going through a list that has weather forecast
    for(var i = 0; i< forecast.list.length; i++) {
        var time = forecast.list[i].dt_txt;
        var hour = time.slice(11, 16);
        var date = time.slice(0, 10);

        //If the hour from the button click matches the hour on the forecast list item, then that item is put to the variable that is shown on the page
        if(hour === clock){
            var icon = "https://openweathermap.org/img/wn/" + forecast.list[i].weather[0].icon + "@2x.png";
            weatherDiv += "<div class='col'>Date: " + date + "<br>Hour: " +hour +"<br>Description: " + forecast.list[i].weather[0].description + "<br>Temperature: " +    forecast.list[i].main.temp + "°C</div><div class='col'>" + "<img src=" + icon + "></img><br><br></div>";
            count++;
            if(count === 2){
                break;
            }
        }
    }
    document.getElementById("futureWeather").innerHTML = weatherDiv;
}
```
2. Now we have a function that takes time as a parameter and prints the output on the page accordingly. The fetch can be changed to use this function so that when we first go to the page it shows 12 O'clock weather forecast by default:

**Change your forecast fetcht to this. Remember to add your APIKEY. This needs to be before changeTime function**

```javascript
//Getting the weather forecast for Helsinki from the OpenWeatherMap api
var forecast;
fetch("https://api.openweathermap.org/data/2.5/forecast?q=Helsinki&units=metric&&appid=YOURAPIKEY")
.then((response) => {
	return response.json();
})
.then((myJson) => {
	forecast=myJson;
	changeTime("12:00");
}); 

```
There are a couple of things here to note. First there is a variable called forecast outside fetch and inside fetch we give forecast variable myJson as value. This is because we need to use data from myJson in the function we made and we can't use the data from inside fetch in another function, unless we pass it as a parameter. The reason we don't give it as a parameter is because we need to be able to use changeTime() function from the buttons. So as a solution we declare the variable outside fetch is that the changeTime() function can "see" it and therefore use it.   

Another thing to note is that we replaced all the code inside ```.then((myJson) => {}``` and called the function we made instead. 

Remember that since the function changeTime() searches for an element that has the id "futureWeather" and puts the content inside it, you need to have an element with that id in your HTML-code for things to show up in your page.

:bulb: At this point your code should be similar to [this](https://github.com/jenni-hautojarvi/cloud-rock-star/blob/master/images/example_codes/weatherwithfunction.html). 
Your application style can of course be whatever you want:).

Visually the change into function usage does not show, so the code in the link looks something like this:
<img src="/images/weather_current_and_forecast.png" width="75%">  

Now let's make buttons that use the function to change time of the weather forecast. For example we could make three buttons out of which one changes weather time to 12:00, one to 15:00 and 18:00.

3. Go to ```<div>``` part where you have your three buttons and add onclick events like below :blush:

```html
<button class="btn btn-info" onclick="changeTime('12:00')">12:00</button>
<button class="btn btn-info" onclick="changeTime('15:00')">15:00</button>
<button class="btn btn-info" onclick="changeTime('18:00')">18:00</button>
```

The button style used here comes from Bootstrap. In the onclick, we give the name of the function we made previously and use parameters to give the function the time we want to show. Using a function is as simple as that. To call it, just give the name of the function and required parameter(s).  

:bulb: [Here](https://github.com/jenni-hautojarvi/cloud-rock-star-2020/blob/master/images/example_codes/weatherwithfunctionandbuttons.html) is the code with the buttons.  
Click one of the buttons and the result: 
<img src="/images/weather_with_buttons.png" width="75%">

## Show outdoor areas on map

Now that we have the weather side of the application working, let's combine it with the Outdoor areas and add functionality to the map.
We already went through the fetch for outdoor areas and setting up the map in a previous week, so if you haven't already, add the following to your html page. Also, add the middle if loop and coor variable :blush:



```javascript
<script src="https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.6.0/leaflet.js" integrity="sha512-gZwIG9x3wUXg2hdXF6+rVkLF/0Vi9U8D2Ntg4Ga5I5BZpVkVxlJWbSQtXPSiUTtC0TjtGOmxa1AJPuV0CPthew==" crossorigin="anonymous"></script>
```
```javascript
	//Helsinki outdoor areas
        fetch("https://citynature.eu/api/wp/v2/places?cityid=5") // part 1 
	        .then((response) => { //part 2
	            return response.json(); //part 3
	        })
			    .then((natureJson) => { // 4
			        console.log(natureJson); // 5
	                var title = natureJson[0].title; //a
	                console.log("Title: " + title); //b
	                var coordinates = natureJson[0].routes.features[0].geometry.coordinates[0]; //c
	                console.log("Coordinates: " + coordinates);
	                var outdoor_list = "";
	                for (var i = 0; i < natureJson.length; i++) {
                    //ADD THIS IF LOOP!!
                    if (natureJson[i].routes !== null){
                        var coor = natureJson[i].routes.features[0].geometry.coordinates;
	                	
                    outdoor_list += '<li class="list-group-item list-group-item-action list-group-item-success"> \
                                <h5>Place name:</h5> \
                                <h4>' + natureJson[i].title +'</h4> \
                                <button type="button" class="btn btn-info">Homepage</button> \
                                <button type="button" class="btn btn-info" onclick="showMap( \'' + natureJson[i].title +  '\', \'' + JSON.stringify(coor) + '\');">Show  on map</button> \
                             </li>  <br>';
	                	}
	                	}
	                document.getElementById("list_outdoor").innerHTML = outdoor_list;
	            });

    
    //Map
	var mymap = L.map('mapid').setView([60.1699, 24.93], 13);

	L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
	       maxZoom: 19,
	       attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
	}).addTo(mymap);

    //ADD also this for showing areas in a map

	var layerGroup = L.layerGroup([]);
	layerGroup.addTo(mymap);

```
Note that for readibility, the html inside ```document.getElementById("list_outdoor").innerHTML += ``` has been indented like it would usually be indented in code. Because it is indented like this backslashes \ are required for the program to understand that the code continues on the next line.  
And also the required elements to show the Outdoor places on the page (remember to give the div with the map a height in css like we did in week 3.1):
```html
<div class="row" id="ulkoilu">
	<div class="col-sm-4">
	  <h3>Outdoor locations</h3>
	  <ul class="list-group" id="list_outdoor">Lista paikoista</ul>
	</div>
	<div class="col-sm-8"><h3>Helsinki map</h3>
		<div id="mapid">Map</div
	></div>
</div>
```
At this point we have a bunch of place names and a map. What we want is to combine these to show the outdoor areas on the map. The citynature API provides us with coordinates that we can use for this. We have already stored the coordinates in a variable in the fetch ```var coor = natureJson[i].routes.features[0].geometry.coordinates;```.  

Let's start by adding to a button an onclick event. In onclick we need to give the function name we want to use. We haven't made a function yet, so let's name it showMap(), for example. Because we need the cordinates in the showMap() function we need to pass them as a parameter to the function. 

Normally we would just say ```showMap(coor); ``` using the variable, we already have, but since the coordinates are in a JSON form, we will use JSON.stringify(coor). This will transform the coordinates into a string which is more lightweight when transporting data. So we use ```showMap(JSON.stringify(coor));``` instead. 

We also may want to show the name of the place on the map as well, so let's give that as a parameter too --> ```showMap(JSON.stringify(coor), natureJson[i].title);```  
As a whole the button is this:  
```html 
<button type="button" class="btn btn-info" onclick="showMap('JSON.stringify(coor)', 'natureJson[i].title);'">Show on map</button>
```

1. Let's add show on map function call to outdoor_list variable button 
```html
document.getElementById("list_outdoor").innerHTML += 
'<li class="list-group-item list-group-item-action list-group-item-success"> \
	<h5>Place name:</h5> \
	<h4>' + natureJson[i].title +'</h4> \
	 <button type="button" class="btn btn-info" onclick="showMap( \'' + natureJson[i].title +  '\', \'' + JSON.stringify(coor) + '\');">Show on map</button> \
</li>  <br>';

outdoor_list += '<li class="list-group-item list-group-item-action list-group-item-success"> \
    <h5>Place name:</h5> \
    <h4>' + natureJson[i].title +'</h4> \
    <button type="button" class="btn btn-info">Homepage</button> \
    <button type="button" class="btn btn-info" onclick="showMap( \'' + natureJson[i].title +  '\', \'' + JSON.stringify(coor) + '\');">Show on map</button></li>  <br>';
```
2. Now we'll add the actual function after map part in script section. So as before the basic syntax will be 
```javascript
function showMap() {
}
```
First let's take the parameters in and use JSON.parse to convert the coordinates back from string form.
```javascript
function showMap(coordinates, place_name) {
	var coor = JSON.parse(coordinates);
}
```
3. The coordinates from citynature come in the form longitude, latitude, but leaflet, which we use for the map, requires the coordinates to be the otherway around. This is why we need to reverse the coordinates. Let's make another function called reverseCoordinates() for this. This is a seperate function that we will call inside showMap() functions. As a parameter it requires the coordinates and we'll use forEach-loop to reverse the items in the array. 
```javascript
function reverseCoordinates(coor){
    var result = [];
    coor.forEach((item) => {
	result.push(item.reverse());
    })
    return result;
}
```
4. Let's continue with showMap() function and call the reverseCoordinates() function inside the function:  
```javascript
function showMap(coordinates, place_name) {
	var coor = JSON.parse(coordinates);
	var reversedCoor = reverseCoordinates(coor);
}
```
5. Now we will add marker to the map that points to the first coordinate point of the area and put the name of the place in a pop up:  
```javascript
function showMap(coordinates, place_name) {
	var coor = JSON.parse(coordinates);
	var reversedCoor = reverseCoordinates(coor);
    
    var marker = L.marker(reversedCoor[0]).addTo(mymap)
    .bindPopup(place_name)
    .openPopup();
      //function continues...                                     
    }
```
6. To be able the show actual area in the map, let's make a polygon and give it the coordinates  
```javascript
//functions continues...
var polygon = L.polygon(reversedCoor, {color: 'black', fillColor: '#f03', fillOpacity: 1}).addTo(mymap);
```
 7. And for the actual showing of the marker and area, we will add a layer:
```javascript
//functions continues...
layerGroup.addLayer(polygon, marker);
```
8. Now let's add one more thing to this. The marker and area will now show in the map but we want the map to also focus on the area that is being shown so let's add the following: 
```javascript
//functions continues...
mymap.panTo(reversedCoor[0]);

```
Now your function is ready to test! :blush:

10. People usually want's to have more information about the location they are about to visit. Let's add Homepage button to direct the user to the home page of the outdoor area. You have this button already. All you need to do is to add onclick part to the code like you did with the showMap() :sunglasses:

```html
<button type="button" class="btn btn-info" onclick="location.href=\''+ natureJson[i].url+';\'">Homepage</button>
```

Now we have all the functionality you need and you can customise the look of your app by styling it whatever way you want.  
:bulb: [Here](https://github.com/jenni-hautojarvi/cloud-rock-star-2020/blob/master/images/example_codes/final.html) is an example of the html of the application
	and [here](https://github.com/jenni-hautojarvi/cloud-rock-star/blob/master/images/example_codes/styles.css) some example css for the application.  
	
The final application with these looks like this:  
<img src="/images/complete.png" width="75%">

## Summary

Now your application is ready. Good job! You have now learn the basic of HTML and bootstrap. You also know how to use Fetch API and how to display JSON data on HTML page. You know how to build Javascript functions and how to call them to add functionality to your application. Now that you have learn the basics you can start desing your own ideas and make them real. 

Good luck in your journey and thank you for participating this challange. We hope this was helpfull for you :smile:
