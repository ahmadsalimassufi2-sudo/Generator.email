<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>AI Chat GitHub Pages</title>
<style>
:root {
  --bg-light:#e5ddd5; --chat-bg-light:#fff; --user-light:#dcf8c6; --ai-light:#f1f0f0;
  --bg-dark:#121212; --chat-bg-dark:#1e1e1e; --user-dark:#2a7f2a; --ai-dark:#333;
}
body{font-family:Arial; background:var(--bg-light); display:flex; flex-direction:column; align-items:center; padding:10px; margin:0; transition:0.3s;}
h2{margin-bottom:10px;}
.chat-container{width:100%; max-width:500px; background:var(--chat-bg-light); border-radius:10px; padding:10px; display:flex; flex-direction:column; height:60vh; overflow-y:auto; box-shadow:0 0 10px rgba(0,0,0,0.1); transition:0.3s;}
.message{max-width:70%; margin:5px 0; padding:10px; border-radius:10px; word-wrap:break-word; line-height:1.4; font-size:16px; cursor:pointer;}
.user{align-self:flex-end; background:var(--user-light); transition:0.3s;}
.ai{align-self:flex-start; background:var(--ai-light); transition:0.3s;}
input{width:100%; max-width:500px; padding:10px; margin-top:10px; border-radius:20px; border:1px solid #ccc; font-size:16px;}
button{margin-top:5px; padding:8px 15px; background:#ff69b4; color:white; border:none; border-radius:5px; cursor:pointer;}
button:hover{background:#ff85c1;}
.controls{display:flex; gap:10px; margin-bottom:5px; flex-wrap:wrap; justify-content:center;}
</style>
</head>
<body>
<h2>AI Chat GitHub Pages</h2>
<div class="controls">
<button onclick="toggleTheme()">Ganti Tema 🌙/☀️</button>
<button onclick="resetChat()">Reset Chat 🔄</button>
<select id="topicSelect">
<option value="">Pilih Topik AI (opsional)</option>
<option value="teknologi">Teknologi</option>
<option value="sejarah">Sejarah</option>
<option value="sains">Sains</option>
<option value="hiburan">Hiburan</option>
</select>
<input type="text" id="usernameInput" placeholder="Masukkan nama kamu" style="width:100%; max-width:500px; margin-top:5px;">
</div>
<div class="chat-container" id="chat"></div>
<input type="text" id="userInput" placeholder="Tulis pesanmu..." onkeydown="if(event.key==='Enter'){sendMessage()}">

<script>
const OPENAI_API_KEY = "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"; // Sudah diganti
let darkMode=false;
const chatContainer=document.getElementById('chat');
const topicSelect=document.getElementById('topicSelect');
const usernameInput=document.getElementById('usernameInput');

// Load history
let chatHistory = JSON.parse(localStorage.getItem('chatHistory')) || [];
chatHistory.forEach(msg => appendMessage(msg.text, msg.sender, false));

function toggleTheme(){
  darkMode=!darkMode;
  document.body.style.background=darkMode?'var(--bg-dark)':'var(--bg-light)';
  chatContainer.style.background=darkMode?'var(--chat-bg-dark)':'var(--chat-bg-light)';
  document.querySelectorAll('.user').forEach(e=>e.style.background=darkMode?'var(--user-dark)':'var(--user-light)');
  document.querySelectorAll('.ai').forEach(e=>e.style.background=darkMode?'var(--ai-dark)':'var(--ai-light)');
}

function resetChat(){chatContainer.innerHTML=''; chatHistory=[]; localStorage.removeItem('chatHistory');}

function appendMessage(text,sender,save=true){
  const msg=document.createElement('div');
  msg.className=`message ${sender}`;
  msg.textContent=text;
  chatContainer.appendChild(msg);
  chatContainer.scroll({top:chatContainer.scrollHeight, behavior:'smooth'});
  msg.onclick=()=>{navigator.clipboard.writeText(text); alert('Teks disalin!');};
  if(save){chatHistory.push({text,sender}); localStorage.setItem('chatHistory',JSON.stringify(chatHistory));}
}

async function sendMessage(){
  const username=usernameInput.value.trim()||"Anon";
  let text=document.getElementById('userInput').value.trim();
  if(!text) return;
  document.getElementById('userInput').value='';

  const emojis=['🙂','😃','🤔','😎','😉'];
  appendMessage(username+": "+text+' '+emojis[Math.floor(Math.random()*emojis.length)],'user');

  const aiMsg=document.createElement('div');
  aiMsg.className='message ai';
  aiMsg.textContent='Mengetik...';
  chatContainer.appendChild(aiMsg);
  chatContainer.scroll({top:chatContainer.scrollHeight, behavior:'smooth'});

  try{
    const topic=topicSelect.value;
    const prompt=(topic?'Topik: '+topic+'\n':'')+text;

    const res = await fetch('https://api.openai.com/v1/chat/completions',{
      method:'POST',
      headers:{
        'Content-Type':'application/json',
        'Authorization':'Bearer '+OPENAI_API_KEY
      },
      body: JSON.stringify({
        model:"gpt-3.5-turbo",
        messages:[{role:"user", content:prompt}],
        max_tokens:300
      })
    });

    const data=await res.json();
    const answer=data.choices[0].message.content;
    const aiEmojis=['🤖','💡','🎯','✨','🧠'];
    const answerWithEmoji=answer+' '+aiEmojis[Math.floor(Math.random()*aiEmojis.length)];

    aiMsg.textContent='';
    let i=0;
    const typingInterval=setInterval(()=>{
      aiMsg.textContent+=answerWithEmoji[i];
      i++;
      chatContainer.scroll({top:chatContainer.scrollHeight, behavior:'smooth'});
      if(i>=answerWithEmoji.length) clearInterval(typingInterval);
    },30);

    const utterance=new SpeechSynthesisUtterance(answer);
    speechSynthesis.speak(utterance);

    setTimeout(()=>{chatHistory.push({text:answerWithEmoji,sender:'ai'}); localStorage.setItem('chatHistory',JSON.stringify(chatHistory));},answerWithEmoji.length*30+50);

  }catch(err){
    aiMsg.textContent="Terjadi kesalahan: "+err.message;
  }
}
</script>
</body>
</html>
