<!DOCTYPE html><html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>WebForge ULTRA PRO EDITOR</title>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;800&display=swap" rel="stylesheet"><style>
*{margin:0;padding:0;box-sizing:border-box;font-family:'Poppins',sans-serif}
body{background:#020617;color:white}

nav{padding:15px;background:#020617;display:flex;justify-content:space-between;align-items:center}
nav h2{color:#38bdf8}

.container{display:flex;height:92vh}

.sidebar{
width:200px;
background:#020617;
padding:10px;
border-right:1px solid #1e293b;
}

.sidebar button{
width:100%;margin:5px 0
}

.editor{
width:40%;
padding:15px;
display:flex;
flex-direction:column;
}

.preview{
width:40%;
background:white;
display:flex;
flex-direction:column;
}

iframe{flex:1;border:none}

.console{height:150px;background:black;color:#00ff88;padding:10px;overflow:auto}

textarea{
width:100%;
height:100%;
background:#0f172a;
color:#38bdf8;
border:none;
padding:20px;
border-radius:12px;
margin-top:10px;
font-size:18px;
line-height:1.6;
letter-spacing:0.5px;
}

.tabs{display:flex}
.tabs button{flex:1;background:#0f172a;color:white}

.controls{display:flex;flex-wrap:wrap}
button{padding:10px;margin:5px;border:none;border-radius:8px;background:#38bdf8;cursor:pointer}

.footer{text-align:center;padding:10px;color:#94a3b8}

</style></head><body><nav>
<h2>WebForge ULTRA PRO</h2>
<div>
<button onclick="downloadSite()">⬇ Export</button>
<button onclick="toggleTheme()">🌗 Theme</button>
</div>
</nav><div class="container"><div class="sidebar">
<button onclick="newFile()">📄 New</button>
<button onclick="saveCode()">💾 Save</button>
<button onclick="loadCode()">📂 Load</button>
<button onclick="clearCode()">🗑 Clear</button>
<button onclick="runCode()">▶ Run</button>
</div><div class="editor"><div class="tabs">
<button onclick="switchTab('html')">HTML</button>
<button onclick="switchTab('css')">CSS</button>
<button onclick="switchTab('js')">JS</button>
</div><textarea id="htmlCode"><h1>WebForge PRO</h1><p>Next level editor 🚀</p></textarea><textarea id="cssCode" style="display:none;">body{background:black;color:white;text-align:center}</textarea><textarea id="jsCode" style="display:none;">console.log('Ready')</textarea><div class="controls">
<button onclick="toggleAutoRun()">⚡ Auto</button>
<button onclick="searchText()">🔍 Search</button>
<button onclick="duplicateCode()">📄 Duplicate</button>
</div></div><div class="preview">
<iframe id="preview"></iframe>
<div class="console" id="console"></div>
</div></div><div class="footer">WebForge ULTRA — Build Your Website, Build Your Future</div><script>
let currentTab='html';
let autoRun=false;
let dark=true;

function switchTab(tab){
['html','css','js'].forEach(t=>document.getElementById(t+'Code').style.display='none');
document.getElementById(tab+'Code').style.display='block';
currentTab=tab;
}

function runCode(){
let html=htmlCode.value;
let css="<style>"+cssCode.value+"</style>";let js="<script>try{"+jsCode.value+"}catch(e){parent.logError(e)}</script>"; preview.srcdoc=html+css+js; log("✅ Running..."); }

function log(msg){console.innerHTML+=msg+"<br>"} function logError(e){log("❌ "+e.message)}

function saveCode(){ localStorage.setItem('html',htmlCode.value); localStorage.setItem('css',cssCode.value); localStorage.setItem('js',jsCode.value); log('💾 Saved'); }

function loadCode(){ htmlCode.value=localStorage.getItem('html')||''; cssCode.value=localStorage.getItem('css')||''; jsCode.value=localStorage.getItem('js')||''; log('📂 Loaded'); }

function clearCode(){htmlCode.value='';cssCode.value='';jsCode.value='';log('🗑 Cleared')} function newFile(){clearCode();log('📄 New file')}

function toggleAutoRun(){autoRun=!autoRun;log('⚡ Auto '+(autoRun?'ON':'OFF'))} setInterval(()=>{if(autoRun)runCode()},1500);

function downloadSite(){ let file=new Blob([htmlCode.value+"<style>"+cssCode.value+"</style><script>"+jsCode.value+"</script>"],{type:'text/html'}); let a=document.createElement('a'); a.href=URL.createObjectURL(file); a.download='webforge.html';a.click(); }

function toggleTheme(){ dark=!dark; document.body.style.background=dark?'#020617':'white'; document.body.style.color=dark?'white':'black'; }

function searchText(){ let text=prompt('Search:'); if(!text)return; if(htmlCode.value.includes(text)) log('Found in HTML'); if(cssCode.value.includes(text)) log('Found in CSS'); if(jsCode.value.includes(text)) log('Found in JS'); }

function duplicateCode(){ htmlCode.value+=htmlCode.value; cssCode.value+=cssCode.value; jsCode.value+=jsCode.value; log('📄 Duplicated'); } </script>

</body>
</html>
