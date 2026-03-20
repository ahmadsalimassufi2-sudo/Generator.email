<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<title>Ahmad ❤️ Putri</title>

<!-- Font Lucu -->
<link href="https://fonts.googleapis.com/css2?family=Pacifico&family=Chewy&family=Baloo+2:wght@600&display=swap" rel="stylesheet">

<style>
body {
    margin: 0;
    height: 100vh;
    background: linear-gradient(270deg, #ffd1dc, #ffe6f0, #ffc1dd);
    background-size: 600% 600%;
    animation: bgMove 10s ease infinite;
    display: flex;
    justify-content: center;
    align-items: center;
    overflow: hidden;
}

@keyframes bgMove {
    0% {background-position: 0% 50%;}
    50% {background-position: 100% 50%;}
    100% {background-position: 0% 50%;}
}

/* Love jatuh */
.love {
    position: absolute;
    font-size: 30px;
    animation: fall linear infinite;
    opacity: 0.8;
}

@keyframes fall {
    0% {transform: translateY(-10vh) rotate(0deg);}
    100% {transform: translateY(110vh) rotate(360deg);}
}

/* Bubble hati */
.bubble {
    position: absolute;
    font-size: 25px;
    animation: floatUp 8s ease-in-out infinite;
    opacity: 0.4;
}

@keyframes floatUp {
    0% {transform: translateY(100vh);}
    100% {transform: translateY(-120vh);}
}

.container {
    text-align: center;
    z-index: 10;
}

button {
    padding: 16px 40px;
    font-size: 22px;
    font-family: 'Chewy', cursive;
    background: #ff5fa2;
    color: white;
    border: none;
    border-radius: 45px;
    cursor: pointer;
    box-shadow: 0 15px 30px rgba(0,0,0,0.3);
    transition: transform 0.3s;
}

button:hover {
    transform: scale(1.2);
}

.love-box {
    display: none;
    animation: pop 1s ease forwards;
}

@keyframes pop {
    from {transform: scale(0) rotate(-10deg); opacity: 0;}
    to {transform: scale(1) rotate(0deg); opacity: 1;}
}

.name {
    font-family: 'Pacifico', cursive;
    font-size: 44px;
    color: #ff2f92;
    text-shadow: 0 0 10px #fff;
    animation: wiggle 2s infinite;
}

@keyframes wiggle {
    0% {transform: rotate(0deg);}
    25% {transform: rotate(2deg);}
    50% {transform: rotate(-2deg);}
    75% {transform: rotate(2deg);}
    100% {transform: rotate(0deg);}
}

.heart {
    font-size: 80px;
    margin: 15px 0;
    animation: beat 0.9s infinite;
}

@keyframes beat {
    0%,100% {transform: scale(1);}
    50% {transform: scale(1.5);}
}

.subtitle {
    font-family: 'Baloo 2', cursive;
    font-size: 22px;
    color: #ff4fa0;
}

.footer {
    margin-top: 10px;
    font-size: 16px;
    color: #ff7bbf;
}
</style>
</head>

<body>

<!-- Love jatuh -->
<script>
for(let i=0;i<25;i++){
    document.write(`<div class="love" style="
        left:${Math.random()*100}%;
        animation-duration:${3+Math.random()*5}s;
    ">💖</div>`);
}
for(let i=0;i<20;i++){
    document.write(`<div class="bubble" style="
        left:${Math.random()*100}%;
        animation-duration:${5+Math.random()*6}s;
    ">💗</div>`);
}
</script>

<div class="container">
    <button onclick="showLove()">tekan disini yaa sayanggg 💕</button>

    <div class="love-box" id="loveBox">
        <div class="name">Ahmad Salim Assufi</div>
        <div class="heart">💞</div>
        <div class="name">Putri Bunga Lestari</div>

        <div class="subtitle">
            Satu Hati • Satu Cinta • Selamanya
        </div>

        <div class="footer">
            Setia itu pilihan, dan aku memilihmu 💖
        </div>
    </div>
</div>

<script>
function showLove(){
    document.querySelector("button").style.display="none";
    document.getElementById("loveBox").style.display="block";
}
</script>

</body>
</html>
