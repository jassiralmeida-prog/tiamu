
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Mini Spotify</title>

<style>

body{
background:#121212;
display:flex;
justify-content:center;
align-items:center;
height:100vh;
font-family:Arial;
color:white;
}

.card{
width:260px;
background:#181818;
border-radius:12px;
padding:20px;
box-shadow:0 8px 20px rgba(0,0,0,0.5);
transition:0.3s;
}

.card:hover{
background:#282828;
transform:scale(1.05);
}

.cover{
width:100%;
height:160px;
background:url("https://lyrics.lyricfind.com/_next/image?url=%2Fimages%2Fv2%2Fcover_art%2Fcuration%2Foriginal%2F2%2F8%2F2%2Ff%2F6332-197d-421d-8c50-62f3359ac99a.jpg&w=3840&q=75");
background-size:cover;
border-radius:8px;
margin-bottom:15px;
}

.title{
font-size:17px;
font-weight:bold;
}

.artist{
color:#b3b3b3;
font-size:14px;
margin-bottom:15px;
}

.controls{
display:flex;
align-items:center;
justify-content:center;
margin-bottom:10px;
}

.play{
background:#1DB954;
border:none;
width:50px;
height:50px;
border-radius:50%;
font-size:18px;
cursor:pointer;
}

.progress{
width:100%;
height:5px;
background:#444;
border-radius:5px;
cursor:pointer;
margin-top:10px;
}

.progress-bar{
height:5px;
background:#1DB954;
width:0%;
border-radius:5px;
}

.time{
display:flex;
justify-content:space-between;
font-size:12px;
color:#b3b3b3;
margin-top:5px;
}

</style>
</head>

<body>

<div class="card">

<div class="cover"></div>

<div class="title">Svag</div>
<div class="artist">Victor Leksell</div>

<div class="controls">
<button class="play" onclick="toggleAudio()">▶</button>
</div>

<div class="progress" onclick="setProgress(event)">
<div class="progress-bar" id="progressBar"></div>
</div>

<div class="time">
<span id="current">0:00</span>
<span id="duration">0:00</span>
</div>

</div>

<audio id="audio" src="Victor Leksell - Svag.mp3"></audio>

<script>

const audio=document.getElementById("audio")
const playBtn=document.querySelector(".play")
const progressBar=document.getElementById("progressBar")
const current=document.getElementById("current")
const duration=document.getElementById("duration")

function toggleAudio(){

if(audio.paused){
audio.play()
playBtn.innerHTML="❚❚"
}else{
audio.pause()
playBtn.innerHTML="▶"
}

}

audio.addEventListener("timeupdate",()=>{

let progress=(audio.currentTime/audio.duration)*100
progressBar.style.width=progress+"%"

current.innerHTML=formatTime(audio.currentTime)

})

audio.addEventListener("loadedmetadata",()=>{

duration.innerHTML=formatTime(audio.duration)

})

function setProgress(e){

const width=e.currentTarget.clientWidth
const clickX=e.offsetX
const duration=audio.duration

audio.currentTime=(clickX/width)*duration

}

function formatTime(time){

let minutes=Math.floor(time/60)
let seconds=Math.floor(time%60)

if(seconds<10) seconds="0"+seconds

return minutes+":"+seconds

}

</script>

</body>
</html>
