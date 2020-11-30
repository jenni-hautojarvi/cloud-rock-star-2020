# Week 3.1 - Print data to your application 

In this part you will print data to you web application. You will learn how to do For and If loop by using Javascript and printing map with information.

  - [Need to know](#need-to-know)
  - [For loop](#for-loop)
  - [Print data to your application page](#print-data-to-your-application-page)
  - [Weather data](#weather-data)
  - [Outdoor places list](#outdoor-places-list)
  - [Map](#map)
  - [Summary](#summary)
  

## Need to know

**getElementById() method:** This is a HTML DOM method and it returns elment that has the ID attribute with the spesicied value. [Visit s3chool](https://www.w3schools.com/jsref/met_document_getelementbyid.asp)

**Leaflet**: Is open-source Javascript library for mobile-friendly interactive maps. [Leaflet](https://leafletjs.com)

## For loop

Using **For loop** we can run the same code as many time we need by using each time different values.

Let's make example:

We want to print every item from a list called list_item = ["a", "b", "c"]. String needs to be inside "Hello Wordl" and integers with out example  number_list = [2, 3, 4].

1. Go to you `index.html`file.

2. Add to inside ``<script>`` tags

```html
<script>
 var list_item = ["a", "b", "c"]; // in Javascript you need to use var to initialize the variable
 var i; //We don't always have to insert value to the variable
    //We can see that in the list there is 3 variable so let's do the loop run 3 times
    //Set i=0 because we want to start at the beginning of list and list first index is 0.
    // Second statement defines condition how many times we run the loop. In our case we run it as loong as variable i value is lower than 3.
    // i++ add +1 to the i variable. This is executed after the code block has been executed.
    for(i= 0; i < 3; i++){
        //let's firt print everything to the console
        console.log(list_item[i]); // call your list and by using [i] we are calling the index of the list item
    };
</script>
```
**With loops if we initialize variable inside loop we can't used it outside of the loop**


3. Remember ``Commit`` and ``Push`` to **Git**

4. See result from your browser console log

<img src="/images/for_loop_result.png" alt="for_loop_result" width="50%" height="50%">

**More information:** [Visit w3schools.com](https://www.w3schools.com/js/js_loop_for.asp)

## Print data to your application page

5. Open to ``index.html`` and modify your ``<body>`` part

```html
<body>
    <div id="data"></div>
    
```

6. Add in ``<script>`` part HTML DOM getElementByid() method


```html
<script>
 var list_item = ["a", "b", "c"]; 
 var i; 
 var text = ""; //initialize the variable to string
    for(i= 0; i < list_item.length; i++){ //We don't always know how much data we have in our list so it's better to use length property
        //you can keep this if you want
        console.log(list_item[i]);
        text += list_item[i] + "<br>"; //We add to text variable list item and row changes
    };
    document.getElementById("data").innerHTML = text; //We call HTML element that has id name data and insert (innerHTML) text variable data to it
</script>
```

:bulb: Your code should looks like this at this point [See example index.html](https://github.com/jenni-hautojarvi/cloud-rock-star-2020/blob/master/images/example_codes/for_loop.html)

7. Remember to ``Commit``and ``Push`` to **Git** :smile:


**Congratulations, you have now connected Javascript code to print information to your application page** :clap:

<img src="/images/for_loop_div.png" width="20%" height="20%">

**Note:** Your printed data in your application is next to left side because we don't have style for this ``<div>`` tag or for it's **id** and everything start from left upper corner in HTML :smile:

## Weather data

Let's update current weather and forecast at the sametime :smile:

8. Open your ``index.html``

- We are going to add:
    - 2 ``<div>`` in ``<body>`` element like we added in the ``for`` loop exercices
    - modify printing part to ``<script>``element

9. Add two ``<div>`` with ids called **currentWeather** and **futureWeather**

10. Go where you fetch and print current weather data

- add after you print weather data variables to the console log next code. Replace **?** marks with correct variable names :smile:

- ``<img>`` tag is for printing image to your web page. You need to add into src="path_to_your_image". **More information**: Visit [w3school](https://www.w3schools.com/html/html_images.asp)

```html
<script>
    //Here we get the image of current weather and save it to icon variable
    var weather_icon = "https://openweathermap.org/img/wn/" + icon + "@2x.png";
		  
    //Here is different way to use getElementById() method. First we save the document element in variable and after this we add data and other elements to it. Like in For loop we added <br>
    var currWeather = document.getElementById("currentWeather");
    currWeather.innerHTML = "<div>City: " + ? + "<br>Description: <br>" + ? + "<br>Temperature: <br>" + ? +"°C <br>" + "</div><div><img src=" + ? + "></img></div>";
</script>
```

11. Go where you fetch and print forecast data

- Set variable ``weatherArray`` like we did with ``text`` in For loop excercise :blush: 
    - **Hint:** It's in same place in current weather :wink:

- Add same image variable initaliationg that we used in current weather and add it where you set other variables like temperature. 
    - We can use same variable names inside fetch and functions if we initialized thouse inside the method that we are using because thouse variables stays stage variables and can't be call outside of the method.

- Next we need to add state where we save forecast data into weatherArray variable. This needs to be inside ``if(hour==="12:00")`` loop after you initialized variables but before state ``count++``. And same exercise in here, replace ``?`` marks with variables names :blush:

```html
<script>
weatherArray += "<div>Date: " + ? + "<br>Hour: " + ? + "<br>Description: " + ? + "<br>Temperature: " + ? + "°C<br>" + "</div><div><img src=" + ? + "></img><br><br></div>";
</script>
```

**Congratulations, you have now printed weather data to your application page** :+1:

<img src="/images/weather.png" width="20%" height="20%">

:bulb: Your code should look like [this](https://github.com/jenni-hautojarvi/cloud-rock-star-2020/blob/master/images/example_codes/weather.html)

## Outdoor places list

Now we make a list of outdoor places. Let's do the same as we did with weather data.

12. Open ``index.html`` and add in ``<body>`` new ``<div>``with id called **list_outdoor**

13. Go where you fetch ourdoor data and add next code after you printed coordinates in console log :blush:
- Here we print list using ``<li>`` tag. **Read more:** [List w3shcool](https://www.w3schools.com/html/html_lists.asp)

```html
<script>
    
    var outdoor_list = "";
    for (var i = 0; i < natureJson.length; i++) { 	
        outdoor_list += '<li> <h5>Place name:</h5><h4>' 
        title +'</h4> </li>  <br>';
    }
    document.getElementById("list_outdoor").innerHTML = outdoor_list;

</script>
```
**You did it! We have now list of places!** :clap:

<img src="/images/list_places.png" width="10%" height="10%">

## Map

Now let's print map to your application. We are going to use Leaflet.

13. Open your ``index.html``. Add ``div``with id called **mapid**. After this add this (**FULL**) code after div. We need it show that we can print the map :smile:
- Do not add anything inside this ``<script>``element!


```html

    <script src="https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.6.0/leaflet.js" integrity="sha512-gZwIG9x3wUXg2hdXF6+rVkLF/0Vi9U8D2Ntg4Ga5I5BZpVkVxlJWbSQtXPSiUTtC0TjtGOmxa1AJPuV0CPthew==" crossorigin="anonymous"></script>

```
14. Add in ``<script>`` part next code. **Do not add this into the part we just added!**
- You can added in the end or at the beginning :blush:



```html
<script>
    var mymap = L.map('mapid').setView([60.1699, 24.93], 13); //here we set view point in Helsinki

    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', { //we create tilelayer from your map
	       maxZoom: 19,
	       attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
    }).addTo(mymap); //we add it to your map

</script>
```
15. Add to ``<header>`` element next link. This collects metadata for printing map.

```html

<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.6.0/leaflet.css" integrity="sha512-xwE/Az9zrjBIphAcBb3F6JVqxf46+CDLwfLMHloNu6KEQCAWi6HcDUbeOfBIptF7tcCzusKFjFw2yuvEpDL9wQ==" crossorigin="anonymous" />

```
16. So that we can see our map we need to make area for it. We can do it by modifying style sheet :blush:
- Open ``style.css``. You can find it inside ``stylesheets`` and next code 

```css

#mapid { 
    height: 500px; 
        }

```

**Congratulations, you have now printed not just list of outdoor places but also a map!** :clap:

<img src="/images/map_list.png" width="100%" height="100%">

:bulb: Your code should looks like [this](https://github.com/jenni-hautojarvi/cloud-rock-star-2020/blob/master/images/example_codes/map.html)

## Summary

Fantastic! Week 3.1 is complete! :blush:

You now know how loops works and how to initialize variable. You also now know how to connect and print data to your html page using JavaScript. Nice job! :+1:

Next lets check how to change layout and you can start designing your application layout [Week 3.2 - Set application layout](https://github.com/jenni-hautojarvi/cloud-rock-star-2020/tree/master/Week%203.2%20-%20Set%20application%20layout)
 
