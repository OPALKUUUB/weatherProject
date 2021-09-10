# weatherProject
<div style="display: flex;">
  <img src="https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black">&nbsp;
  <img src="https://img.shields.io/badge/Node.js-43853D?style=for-the-badge&logo=node.js&logoColor=white">&nbsp;
  <img src="https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white">&nbsp;
  <img src="https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white">&nbsp;
</div>
##### This is a first tuterial about Express. In this learning use https, body-parser. And I use data from api.openweathermap.org. (Thank you so much 🤟🤟🤟)
##### I through inside tag by use body-parser. Fetch data by use https. Link -> https://openweathermap.org/api

```js
const express = require("express");
const https = require("https")
const bodyParser = require("body-parser");
const app = express();
app.use(bodyParser.urlencoded({extended: true}));

app.get("/", function (req, res) {
    res.sendFile(__dirname + "/index.html")
})

app.post("/", function(req, res) {
    // console.log(req.body.cityName);
    const query = req.body.cityName;
    const apiKey = "Replace with your apikey";
    const unit = "metric";
    const url = "https://api.openweathermap.org/data/2.5/weather?q=" + query + "&units=" + unit + "&appid=" + apiKey;

    https.get(url, function (response) {
        console.log(response.statusCode);

        response.on("data", (data) => {
            const weatherData = JSON.parse(data);
            // console.log(weatherData);
            // const object = {
            //     name: "Opal",
            //     favouriteFood: "Salmon"
            // };
            // console.log(JSON.stringify(object));
            temp = weatherData.main.temp;
            console.log(temp);
            const weatherDescription = weatherData.weather[0].description;
            const icon = weatherData.weather[0].icon
            const imageURL = "http://openweathermap.org/img/wn/" + icon + "@2x.png";
            res.write("<p>The weather is curently " + weatherDescription + "</p>");
            res.write("<h1>The temperature in " + weatherData.name + " is " + temp + " degrees Celcius.</h1>")
            res.write("<img src=" + imageURL + ">");
            res.send();
        })
    });
})

app.listen("3000", function () {
    console.log("Server is running on port 3000!!!");
})
```
