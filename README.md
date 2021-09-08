<!DOCTYPE html>
<html lang="en">
<head>
<script>
let text=document.querySelector("input");
let btn=document.getElementById("btn");
let weather=document.getElementById("weather");
let loc=document.getElementById("location");
let speed=document.getElementById("speed");
let temp=document.getElementById("temp");
let minmax=document.getElementById("minmax");
let time=document.getElementById("time");
start();
function start(){
    getweather("london")
}
btn.addEventListener("click",(e)=>{
    e.preventDefault();
    let input=text.value;
    getweather(input);
    text.value="";
});
function getweather(input){
    fetch(`https://api.openweathermap.org/data/2.5/weather?q=${input}&appid=cc7b365cdf72c6b1736b020dc6c87432`)
    .then((result)=>{
        return result.json()
    })
    .then((data)=>{
        let txt=data.weather[0].description;
        weather.innerHTML=txt;
        txt=data.sys.country;
        loc.innerHTML=input.toUpperCase()+','+txt;
        txt=data.wind.speed;
        speed.innerHTML=txt+" kms";
        txt=parseInt(data.main.temp-273);
        temp.innerHTML=txt+"*C";
        txt=parseInt(data.main.temp_min-273);
        let txt2=parseInt(data.main.temp_max-273);
        minmax.innerHTML=txt+"*C(min) / "+txt2+"*C(max)";
        txt=new Date(data.dt).toDateString();
        time.innerHTML=txt;
    })
    .catch((err)=>{
        alert("Enter Valid Name");
        console.log(err.message);
    });
}

</script>

    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weather App</title>
    </head>
<style>
body{
    height:100vh;
    font-family:helvetica;
    background-image: url("https://images.unsplash.com/photo-1592210454359-9043f067919b?ixid=MnwxMjA3fDB8MHxzZWFyY2h8Mnx8d2VhdGhlcnxlbnwwfHwwfHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=600&q=60");
    background-repeat: no-repeat;
    background-size:cover;
    display:flex;
    justify-content: space space-evenly;
    align-items: center;
}
p{
    margin: 5px;
    color:blue;
}
#od{
    background:rgba(256,256,256,.5);
    width:300px;
    text-align:center;
    border-radius:30px;
}
#id{
    width:200px;
    text-align:center;
    background:rgba(256,256,256,.6);
    border-radius:30px;
}
div{
    margin:10px auto;
}
input{
    opacity: ;
    border:none;
    margin:10px auto;
    width:200px;
    height:30px;
    text-align:center;
    font-size:25px;
    padding:5px;
    background-color:lightgreen;
    border-radius:10px;
}
button{
    color:blue;
    border:none;
    margin:auto;
    width:215px;
    height:40px;
    text-align:center;
    font-size:25px;
    padding:5px;
    border-radius:10px;
}
button:hover{
    background-color:rgb(209, 141, 38);
}
#location{
    font-size:20px;
}
#time{
    font-size:20px;
}
#temp{
    font-size:30px;
}
#minmax{
    font-size:15px;
}
#weather{
    font-size:20px;
}
#speed{
    font-size:20px;
}
</style>

<body>
    <div id="od">
        <input type="text"><br>
        <button id="btn" type="submit">Get Weather</button>
        <div id="id">
            <p id="location"></p>
            <p id="time"></p>
            <p id="temp"></p>
            <p id="minmax"></p>
            <p id="speed"></p>
            <p id="weather"></p>
        </div>
    </div>

</body>
</html>
