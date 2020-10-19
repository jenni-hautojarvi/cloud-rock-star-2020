# Week 2.1 - Add Helsinki Outdoor route API 

In this lab we fetch a JSON file accross the network and print it to the JS console.

  - [Need to know](#need-to-know)
  - [Create your first app](#create-your-first-app)
  - [Summary](#summary)
  

## Need to know

**Javascript**: JavaScript is a programming language that allows you to implement complex features on web pages and it is the world's most popular web programming language. It's also free to use and already running in browser on computers, tablets and smart-phones. If you are intered to learn more click this: [w3schools](https://www.w3schools.com/js/DEFAULT.asp).

**Fetch API**: provides a JavaScript interface for accessing and manipulating parts of the HTTP pipeline, such as requests and responses. More information: [Here](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)

**Helsinki outdoor data**: Citynature.eu offers an open REST API interface (licence CC BY 4.0) that can be used by application developers to utilise the information from both Helsinki and Tallinn available on the site. More information: [Citynature.eu](https://citynature.eu/en/to-the-developers/)

## Add your first Javascript code

You can modify your application code from git or Web IDE. Instructions are for Web IDE.

1. Open Web IDe from your application tool chain.

<img src="/images/toolchain-ready.png" width="80%" height="80%">

2. Click **public** folder and after that click ``index.html``


3. First let's modify the **index.html**: 
- Add script tags for Javasript

```html
<!DOCTYPE html>
<html>

  <head>
    <title>NodeJS Starter Application</title>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" href="stylesheets/style.css">
  </head>

  <body>
    <table>
      <tr>
        <td style= "width:30%;">
          <img class = "newappIcon" src="images/newapp-icon.png">
        </td>
        <td>
          <h1 id="message">Hello World!</h1>
          <p class='description'></p> Thanks for creating a <span class = "blue">NodeJS Starter Application</span>.
        </td>
      </tr>
    </table>
    <!-- add script tags for Javascript Note: This is how to comment html code-->
    <script>
    </script>
  </body>

</html>
```

4. Add your first Javascript Fetch API. 

Add the Fetch API function to collect JSON file from Helsinki Outdoor nature webpage inside the ``script`` tags. Using fetch we request the data every time we load the application page. **NOTE:** We don't store the data in database.

In the code:
1. This is the url where we fetch data. **Note: If your application is https:// you can't fetch data from http:// because of Web Security**
2. The response is HTTP response, not the actual JSON file. 
3. We extract the JSON body content from the response using **json()** method
4. After JSON is extracted data is restored in variable natureJson
5. Print JSON data to Javascript console

```html
<script>
    //Helsinki outdoor areas
    fetch("https://citynature.eu/api/wp/v2/places?cityid=5") // part 1 
        .then((response) => { //part 2
            return response.json(); //part 3
        })
		    .then((natureJson) => { // 4
		        console.log(natureJson); // 5
            });
</script>
```

After you have updated ``script`` part remember to **commit** and **push** the changes to Git or you can't see the changes in your application.

5. Open your application and find your browser JS console
- Safari: Develop -> Show JavaScript console
- Firefox: Tools -> Web Developer -> Web console
- Chrome: Three dots right upper corner -> More Tools -> Developer tools -> Console

- Chrome: 
<img src="/images/Chrome-js-console.png" width="80%" height="80%">

- From **Elements** you can see your source code and **Styles** your CSS

<img src="/images/chrome-elements.png" width="80%" height="80%">

- Go to **Console**

**Congratulations, you have fecth data to your application on IBM Cloud™!** :clap:

<img src="/images/chrome-console-data.png" width="100%" height="100%">

## How to select spefic detail from JSON data

JSON data contains object and list of object. Word JSON comes from **J**ava**S**cript **O**bject **N**otation.

- Here you can see that our outdoor data is in a list [] that has object {}. It can also contain objects inside object. In our data list we have 11 objects.

<img src="/images/Console-outdoor-data.png" width="100%" height="100%">

6. Let's print only the first object title and first coordinate values.

- a) Set variable title and sign to it natureJSON (our data) first object and it's title. Counting starts from 0 in Javascript.
- b) If you want print also string (text) with the variable you need to add "" around your text and add + mark between string and variable.
- c) Our coordinates are inside a list in our object. To access coordinates first call the data list first object and after this you call the list name and its first object. Inside **routes** object the list is called **features**. Let's call the first object in here also. Inside the first object is object called **geometry** and inside that object is our list of **coordinates**.

```html
<script>
    //Helsinki outdoor areas (Note: This is how to comment JS code)
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
            	});
</script>
```

**Congratulations, you have fecth data to your application on IBM Cloud™!** :clap:

<img src="/images/chrome-json-data-points.png" width="100%" height="100%">

If you have error or you can't see the print in console. Your ``index.html`` should now look something like this. See: [index.html](https://github.com/jenni-hautojarvi/cloud-rock-star/blob/master/images/example_codes/new_index.html) 

## Summary

Fantastic! Week 2.1 is complete! :smile:

At this point you have added data to your first Node.js application on IBM Cloud using Cloud Foundry public environment.

Now that you have outrood routes data it's time to fecth weather data. Go to [
Week 2.2 - Add Weather API](https://github.com/jenni-hautojarvi/cloud-rock-star/tree/master/Week%202.2%20-%20Add%20Weather%20API). 
