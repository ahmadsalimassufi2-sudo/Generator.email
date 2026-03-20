<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<title>Ucapan Lebaran 💖</title>

<style>
body {
    margin: 0;
    overflow: hidden;
    font-family: Arial, sans-serif;
    background: linear-gradient(to top, #ff9a9e, #fad0c4);
    color: white;
}

/* BINGKAI ATAS & BAWAH */
.top-border, .bottom-border {
    position: fixed;
    width: 100%;
    text-align: center;
    font-size: 22px;
    z-index: 10;
    animation: geser 6s infinite alternate ease-in-out;
}

.top-border { top: 0; }
.bottom-border { bottom: 0; }

@keyframes geser {
    from {transform: translateX(-30px);}
    to {transform: translateX(30px);}
}

/* BINGKAI KIRI & KANAN */
.side-border {
    position: fixed;
    top: 0;
    height: 100%;
    width: 30px;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    align-items: center;
    font-size: 22px;
    z-index: 10;
}

.left-border { left: 0; }
.right-border { right: 0; }

/* CONTAINER */
.container {
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    text-align: center;
    padding: 40px;
    box-sizing: border-box;
}

h1 {
    font-size: 28px;
}

/* BUTTON */
button {
    padding: 15px 30px;
    font-size: 18px;
    border: none;
    border-radius: 20px;
    background: #ff4d6d;
    color: white;
    cursor: pointer;
    margin-top: 20px;
    box-shadow: 0 0 15px rgba(255,255,255,0.7);
}

button:hover {
    transform: scale(1.1);
}

/* PESAN */
#pesan {
    display: none;
    margin-top: 20px;
    font-size: 18px;
    padding: 20px;
    background: rgba(255,255,255,0.2);
    border-radius: 20px;
    animation: fadeIn 1s ease;
}

@keyframes fadeIn {
    from {opacity: 0; transform: scale(0.8);}
    to {opacity: 1; transform: scale(1);}
}

/* LOVE HUJAN */
.love {
    position: absolute;
    top: -50px;
    animation: jatuh linear infinite;
}

@keyframes jatuh {
    to {
        transform: translateY(110vh);
    }
}
</style>
</head>

<body>

<!-- ATAS -->
<div class="top-border">
💖🌸💗✨💕🌸💖✨💗💕🌸💖✨💗💕🌸💖✨💗💕🌸💖
</div>

<!-- BAWAH -->
<div class="bottom-border">
💖🌸💗✨💕🌸💖✨💗💕🌸💖✨💗💕🌸💖✨💗💕🌸💖
</div>

<!-- KIRI -->
<div class="side-border left-border">
🌸 💖 🌸 💕 🌸 💗 🌸 💖 🌸 💕 🌸 💗
</div>

<!-- KANAN -->
<div class="side-border right-border">
💗 🌸 💕 🌸 💖 🌸 💗 🌸 💕 🌸 💖 🌸
</div>

<!-- ISI -->
<div class="container">
    <h1>🌙 Selamat Hari Raya 💖</h1>

    <button id="tombol" onclick="tampilkanPesan()">💌 Tekan disini ya 💌</button>

    <div id="pesan">
        <p>
            Assalamu'alaikum Laura 🥺💖🌸<br><br>
            Di hari yang suci ini, aku ingin memohon maaf sebesar-besarnya
            atas semua kesalahan aku ya 🙏🥺💕<br><br>
            Semoga kita selalu diberi kebahagiaan, kesehatan,
            dan hubungan yang makin baik 💗✨🌸<br><br>
            Selamat Hari Raya Idul Fitri 🌙💖<br>
            Mohon Maaf Lahir dan Batin 🤍🥰
        </p>
    </div>
</div>

<script>
function tampilkanPesan() {
    document.getElementById("pesan").style.display = "block";
    document.getElementById("tombol").style.display = "none";
}

/* HUJAN LOVE */
function createLove() {
    const love = document.createElement("div");
    love.classList.add("love");
    love.innerHTML = ["💖","💕","💗","🌸"][Math.floor(Math.random()*4)];

    love.style.left = Math.random() * window.innerWidth + "px";
    love.style.animationDuration = (Math.random() * 3 + 2) + "s";
    love.style.fontSize = (Math.random() * 20 + 15) + "px";

    document.body.appendChild(love);

    setTimeout(() => {
        love.remove();
    }, 5000);
}

setInterval(createLove, 200);
</script>

</body>
</html>
