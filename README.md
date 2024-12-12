//index.html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KISHKINDA UNIVERSITY virtual assistant</title>
  <link rel="shortcut icon" href="logo.jpg" type="image/x-icon">
  <link rel="stylesheet" href="style.css">
</head>
<body>
    <img src="logo.jpg" alt="logo" id="logo">
    <h1>I'm <span id="name">KISHKINDA UNIVERSITY</span>,Your <span id="va">Virtual Assistant</span></h1>
    <img src="voice.gif" alt="voice" id="voice">
    <button id="btn"><img src="mic.svg" alt="mic"><span id="content"> Click here for talk to me</span> </button>

    <script src="script.js"></script>
</body>
</html>

//script.js
let btn=document.querySelector("#btn")
let content=document.querySelector("#content")
let voice=document.querySelector("#voice")

function speak(text){
    let text_speak=new SpeechSynthesisUtterance(text)
    text_speak.rate=1
    text_speak.pitch=1
    text_speak.volume=1
    text_speak.lang="hi-GB"
    window.speechSynthesis.speak(text_speak)
}

function wishMe(){
    let day=new Date()
    let hours=day.getHours()
    if(hours>=0 && hours<12){
        speak("Good Morning Sir")
    }
    else if(hours>=12 && hours <16){
        speak("Good afternoon Sir")
    }else{
        speak("Good Evening Sir")
    }
}
// window.addEventListener('load',()=>{
//     wishMe()
// })
let speechRecognition= window.SpeechRecognition || window.webkitSpeechRecognition 
let recognition =new speechRecognition()
recognition.onresult=(event)=>{
    let currentIndex=event.resultIndex
    let transcript=event.results[currentIndex][0].transcript
    content.innerText=transcript
   takeCommand(transcript.toLowerCase())
}

btn.addEventListener("click",()=>{
    recognition.start()
    voice.style.display="block"
    btn.style.display="none"
})
function takeCommand(message){
   voice.style.display="none"
    btn.style.display="flex"
    if(message.includes("hello")||message.includes("hey")){
        speak("hello sir,what can i help you?")
    }
    else if(message.includes("who are you")){
        speak("i am virtual assistant ,created by Ayush Sir")
    }else if(message.includes("open youtube")){
        speak("opening youtube...")
        window.open("https://youtube.com/","_blank")
    }
    else if(message.includes("open google")){
        speak("opening google...")
        window.open("https://google.com/","_blank")
    }
    else if(message.includes("open facebook")){
        speak("opening facebook...")
        window.open("https://facebook.com/","_blank")
    }
    else if(message.includes("open instagram")){
        speak("opening instagram...")
        window.open("https://instagram.com/","_blank")
    }
    else if(message.includes("open calculator")){
        speak("opening calculator..")
        window.open("calculator://")
    }
    else if(message.includes("open whatsapp")){
        speak("opening whatsapp..")
        window.open("whatsapp://")
    }
    else if(message.includes("time")){
      let time=new Date().toLocaleString(undefined,{hour:"numeric",minute:"numeric"})
      speak(time)
    }
    else if(message.includes("date")){
        let date=new Date().toLocaleString(undefined,{day:"numeric",month:"short"})
        speak(date)
      }
    else{
        let finalText="this is what i found on internet regarding" + message.replace("shipra","") || message.replace("shifra","")
        speak(finalText)
        window.open(`https://www.google.com/search?q=${message.replace("shipra","")}`,"_blank")
    }
}


//style.css
@import url('https://fonts.googleapis.com/css2?family=Protest+Guerrilla&display=swap');
*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
body{
    width: 100%;
    height: 100%;
    background-color: black;
    display: flex;
    align-items: center;
    justify-content: center;
    gap:30px;
    flex-direction: column;
}
#logo{
    width: 20vw;
}
h1{
    color: aliceblue;
    font-family: "Protest Guerrilla", sans-serif;
}
#name{
    color:rgb(212, 43, 122);
    font-size: 45px;
}
#va{
    color:rgb(43, 206, 212);
    font-size: 45px; 
}
#voice{
    width: 100px;
    display: none;
   
}
#btn{
width: 30%;
background: linear-gradient(to right,rgb(21, 145, 207),rgb(201, 41, 116));
padding: 10px;
display: flex;
align-items: center;
justify-content: center;
gap: 10px;
font-size: 20px;
border-radius: 20px;
color: white;
box-shadow: 2px 2px 10px rgb(21, 145, 207),2px 2px 10px rgb(201, 41, 116);
border: none;
transition: all 0.5s;
cursor: pointer;
}
#btn:hover{
    box-shadow: 2px 2px 20px rgb(21, 145, 207),2px 2px 20px rgb(201, 41, 116);
    letter-spacing: 2px;
}
