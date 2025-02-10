# wheader-api-mini-project
This is a little project about getting api from api.openweathermap.org

# ScreenShot
![screenshot](https://github.com/user-attachments/assets/c1fc0cff-4ed8-414d-ad42-096aa944b949)

### JS Code
```
"use srtict"

// let weatherApi = `https://api.openweathermap.org/data/2.5/weather?q=london&appid=5841ab891489da8876dae19b9a01b7ed`;

let searchBox = document.querySelector('.search-box');
let city = document.querySelector('.city');
let date = document.querySelector('.date');
let weather = document.querySelector('.weather');
let temp  = document.querySelector('.temp');
let hiLowTemp = document.querySelector('.hi-low');


let apiData = {
    url : "https://api.openweathermap.org/data/2.5/weather?q=",
    key : "5841ab891489da8876dae19b9a01b7ed"
}



function fetchingData(){
    let query = searchBox.value;

    fetch(`${apiData.url}${query}&appid=${apiData.key}`)
    .then(res => res.json())
    .then(data => {
        console.log(data)
        updateDom(data)
    })
}

function updateDom (data){
    city.innerHTML = `${data.name}`

    weather.innerHTML = `${data.weather[0].description}`

    temp.innerHTML = `${Math.floor(data.main.temp - 273.5)}°c `

    date.innerHTML = showTime();

    hiLowTemp.innerHTML = `${Math.floor(data.main.temp_min - 273.5)} °c/ ${Math.floor(data.main.temp_max - 273.5)}°c`

}


function showTime(){

    let days = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
    let months = ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'];

    let now = new Date()

    let dayStr = days[now.getDay()];
    let dayNum = now.getDate();
    let month = months[now.getMonth()];
    let year = now.getFullYear();

    return `${dayStr} ${dayNum} ${month} ${year}`;
    
}

searchBox.addEventListener('keyup', (event) => {
    if(event.keyCode === 13){
        fetchingData()
        
    }
    
})


```
