<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ADHI SIGNAL APP ✈️</title>
<style>
/* --- 1. GENERAL STYLES --- */
body { font-family: Arial, Helvetica, sans-serif; margin:0; padding:0; display:flex; flex-direction:column; align-items:center; min-height:100vh; background-color:#0f1724; color:#fff; }
h1 { color:#00ffd1; margin-bottom:18px; text-align:center; padding-top: 30px; }
label { font-size:14px; color:#00ffd1; margin-bottom:3px; }
button { padding:12px 18px; border-radius:10px; border:0; font-weight:700; cursor:pointer; transition: transform 0.1s ease; }
button:hover { transform: scale(1.05); }

/* --- INPUT FIELD FIX --- */
input { 
    padding:12px; 
    border-radius:10px; 
    border:0; 
    width:100%; 
    text-align:center; 
    font-size:16px;
    background-color: #1e293b; 
    color: #ffffff; 
}

/* --- 2. LAYOUT AND SPACING FIXES --- */
#appContent, #loginContainer, #registerContainer { 
    display:flex;
    flex-direction:column;
    gap: 15px; 
    align-items:center;
    width:90%;
    max-width:400px;
    position:relative;
}
.box { 
    display:flex;
    flex-direction:column;
    gap: 10px; 
    align-items:center; 
    width:100%;
    position:relative; 
    margin-bottom: 20px;
}
#appContent .box { 
    gap: 12px;
}


/* --- 3. COMPONENT STYLES --- */
#generateBtn { width:100%; background:#ff4444; color:#fff; font-size:16px; }
#togglePanelBtn { background:#ffaa00; color:#000; }
#modeBtn { position:absolute; top:-10px; right:-10px; background:#00ccff; color:#000; font-size:12px; padding:6px 10px; border-radius:20px; font-weight:700; }
#howBtn { background:#00cc88; color:#000; width:100%; font-size:14px; }
#logoutBtn { background:#ff5555; color:#fff; margin-top:10px; } 
#loginBtn, #registerBtn { width:100%; background:#00ccff; color:#000; font-size:16px; margin-top:10px; } 
#switchBtn { background: #333; color: #fff; font-size: 14px; } 

/* --- Loading Screen Styles (No change) --- */
#loading-screen {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: #0f1724; 
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    z-index: 9999;
    transition: opacity 0.5s ease-out; 
}
.spinner {
    border: 8px solid rgba(0, 255, 209, 0.3); 
    border-top: 8px solid #00ffd1; 
    border-radius: 50%;
    width: 60px;
    height: 60px;
    animation: spin 1.5s linear infinite;
    margin-bottom: 20px;
}
@keyframes spin {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
}
#loading-message {
    color: #ffaa00; 
    font-size: 18px;
    font-weight: bold;
    text-shadow: 0 0 5px rgba(255, 170, 0, 0.5);
}


#extraPanel { display:none; flex-direction:column; gap:8px; width:100%; margin-top:10px; }
#extraPanel.show { display:flex; }
#historyBtn { background:#00ff99; color:#000; }
#themeBtn { background:#8888ff; color:#fff; }

#out { margin-top:10px; color:#00ff99; font-size:18px; text-align:center; width:100%; }

#riskLabels { margin-top:6px; font-size:14px; text-align:center; display:none; }
#riskLabels span { margin:0 5px; font-weight:700; padding:2px 6px; border-radius:6px; }
#odd { background:#22ff22; color:#000; }
#risk { background:#ffcc00; color:#000; }
#veryRisk { background:#ff4444; color:#fff; }

/* --- MODALS (No change) --- */
#historyModal { display:none; position:fixed; top:0; left:0; width:100%; height:100%; background:rgba(0,0,0,0.8); justify-content:center; align-items:center; z-index:1000; }
#historyContent { background:#111; padding:20px; border-radius:12px; width:90%; max-width:400px; max-height:80%; overflow-y:auto; display:flex; flex-direction:column; gap:10px; }
#historyContent h2 { color:#00ffd1; margin-top:0; }
#historyContent p { color:#a0f4e0; padding:4px 6px; border-radius:6px; background:rgba(255,255,255,0.05); }
#closeHistory { background:#ff5555; color:#fff; margin-top:10px; }
#clearHistoryBtn { background:#ffaa00; color:#000; }

#howModal { display:none; position:fixed; top:0; left:0; width:100%; height:100%; background:rgba(0,0,0,0.9); justify-content:center; align-items:center; z-index:2000; }
#howContent { background:#111; padding:20px; border-radius:12px; width:90%; max-width:400px; max-height:80%; overflow-y:auto; color:#fff; }
#howContent h2 { color:#00ffd1; margin-top:0; text-align:center; }
#howContent p { margin-bottom:10px; line-height:1.4; }
#howContent .highlight { color:#ffdd00; font-weight:700; }
#howContent .start { color:#00bfff; font-weight:700; }
#howContent .end { color:#ff77ff; font-weight:700; }
#howContent .underline { text-decoration:underline; }
#howContent .warning { color:red; background:white; font-weight:bold; padding:4px; border-radius:4px; }
#howContent button { background:#ff5555; color:#fff; margin-top:10px; padding:10px 15px; border-radius:8px; border:0; font-weight:700; }
</style>
</head>
<body>

<div id="loading-screen">
    <div class="spinner"></div>
    <div id="loading-message">Loading ADHI Signal System...</div>
</div>

<h1>ADHI SIGNAL APP ✈️</h1>

<div id="loginContainer" style="display: none;">
    <h2 style="color:#00ccff;">පද්ධතියට පිවිසෙන්න</h2>
    <label for="loginUsernameInput">Username</label>
    <input id="loginUsernameInput" type="text" placeholder="ඔබේ Username ඇතුළු කරන්න" required>
    <label for="loginPasswordInput">Password</label>
    <input id="loginPasswordInput" type="password" placeholder="Password ඇතුළු කරන්න" required>
    <button id="loginBtn" onclick="loginUser()">Login</button>
    <button id="switchBtn" onclick="showRegister()">Switch to Register</button>
</div>

<div id="registerContainer" style="display: none;">
    <h2 style="color:#ffaa00;">නව ගිණුමක් සාදන්න</h2>
    <label for="regUsernameInput">Username</label>
    <input id="regUsernameInput" type="text" placeholder="Username (අවම අකුරු 4)" required>
    <label for="regPasswordInput">Password</label>
    <input id="regPasswordInput" type="password" placeholder="Password (අවම අකුරු 6)" required>
    <button id="registerBtn" onclick="registerUser()">Register</button>
    <button id="switchBtn" onclick="showLogin()">Switch to Login</button>
</div>

<div id="appContent" style="display: none;">
  <div class="box">
    <button id="modeBtn" onclick="toggleInputMode()">Mode: Picker</button>
    <label for="t1">Start Time</label>
    <input id="t1" type="time" step="1" placeholder="Start time">
    <label for="t2">End Time</label>
    <input id="t2" type="time" step="1" placeholder="End time">

    <button id="generateBtn" onclick="calc()">Generate</button>
    <button id="howBtn" onclick="openHow()">භාවිතයට උපදෙස්</button>
    <button id="togglePanelBtn" onclick="toggleExtraPanel()">Show Options</button>
    
    <button id="logoutBtn" onclick="logoutUser()">Log Out</button>

    <div id="extraPanel">
      <button id="historyBtn" onclick="openHistory()">History</button>
      <button id="themeBtn" onclick="switchTheme()">Switch Theme</button>
    </div>

    <div id="out"></div>
    <div id="riskLabels">
      <span id="odd">ODD -: 2x ✅</span>
      <span id="risk">5x risk ⚠️</span>
      <span id="veryRisk">10x very risky ⚠️️</span>
    </div>
  </div>
</div>

<div id="historyModal">
  <div id="historyContent">
    <h2>History</h2>
    <div id="historyBox"></div>
    <button id="clearHistoryBtn" onclick="clearHistory()">Clear History</button>
    <button id="closeHistory" onclick="closeHistory()">Close</button>
  </div>
</div>

<div id="howModal">
  <div id="howContent">
    <h2>භාවිතයට උපදෙස්</h2>
    <p>උදාහරණයක් ලෙස: <span class="start">දම්පාට Start ODD එක</span> (2:00x - 9:99x) / අවසන් වී <span class="start">නිල් පැහැති ODD</span> (1:00x - 1:99x) තුනක් (3 or 3+) හෝ ඊට වැඩියෙන් ගොස් පටන් ගන්නා <span class="start">දම් / රෝස පැහැති ODD</span> එක App එකේ <span class="end">End</span> යට තීරුවෙහි නිවැරදිව යොදන්න。</p>
    <p class="underline">කෙටි හදුන්වා දීම:</p>
    <p>නිල්පාට ODD යන්න කලින් පටන් ගත් <span class="start">දම් පාට</span> ODD එකේ වේලාව තප්පර සමග <strong>Start ODD</strong> හි යොදන්න. ඉන් පසු නිල් ODD ගිහින් අවසන් නම් එහි ඇති දම් හෝ රෝස ODD එකේ වේලාව App එකේ <strong>End Time</strong> යටතේ යොදන්න。</p>
    <p class="warning">මෙය ගණිතමය ක්‍රමයක් බව කරුණාවෙන් සලකන්න..!!</p>
    <button onclick="closeHow()">Close</button>
  </div>
</div>

<script>
// --- SECURITY CONSTANTS ---
const LOGIN_KEY = "isLoggedIn"; 
const USERS_KEY = "adhiUsers"; 
const DEVICE_KEY = "Adhi_Device_UUID"; // New key for the unique device ID

// --- APP VARIABLES ---
let historyArr = [];
let timePickerMode = true;
let themeMode = 0;
let riskTimeout;

// --- DEVICE ID GENERATION & INITIALIZATION ---

function generateUUID() {
    // Simple, non-standard UUID generation for local security purposes
    return 'xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx'.replace(/[xy]/g, function(c) {
        var r = Math.random() * 16 | 0, v = c == 'x' ? r : (r & 0x3 | 0x8);
        return v.toString(16);
    });
}

function getDeviceID() {
    let deviceID = localStorage.getItem(DEVICE_KEY);
    if (!deviceID) {
        deviceID = generateUUID();
        localStorage.setItem(DEVICE_KEY, deviceID);
        console.log("New Device ID Registered:", deviceID); // For debugging
    }
    return deviceID;
}

// --- LOADING SCREEN ---
function hideLoadingScreen() {
    const loadingScreen = document.getElementById('loading-screen');
    loadingScreen.style.opacity = '0'; 
    setTimeout(() => {
        loadingScreen.style.display = 'none';
        checkLoginStatus(); 
    }, 500); 
}

// --- DISPLAY FUNCTIONS ---
function showLogin() {
    document.getElementById('registerContainer').style.display = 'none';
    document.getElementById('loginContainer').style.display = 'flex';
}

function showRegister() {
    document.getElementById('loginContainer').style.display = 'none';
    document.getElementById('registerContainer').style.display = 'flex';
}

// --- LOGIN/REGISTER FUNCTIONS ---

function getStoredUsers() {
    const usersJson = localStorage.getItem(USERS_KEY);
    return usersJson ? JSON.parse(usersJson) : {};
}

function registerUser() {
    const username = document.getElementById('regUsernameInput').value.trim();
    const password = document.getElementById('regPasswordInput').value;
    const currentDeviceID = getDeviceID(); // Get this device's unique ID

    if (username.length < 4 || password.length < 6) {
        alert('Username අවම අකුරු 4 ක් සහ Password අවම අකුරු 6 ක් විය යුතුය.');
        return;
    }

    const users = getStoredUsers();
    if (users[username]) {
        alert('මෙම Username එක දැනටමත් භාවිතයේ ඇත. වෙනත් නමක් තෝරන්න.');
        return;
    }

    // Save user details with the Device ID
    users[username] = {
        password: password,
        deviceID: currentDeviceID // THIS IS THE SECURITY KEY
    };
    localStorage.setItem(USERS_KEY, JSON.stringify(users));
    
    alert('ලියාපදිංචිය සාර්ථකයි! දැන් ඔබට පිවිසිය හැක.');
    showLogin();
    
    // Clear registration fields
    document.getElementById('regUsernameInput').value = '';
    document.getElementById('regPasswordInput').value = '';
}

function loginUser() {
    const username = document.getElementById('loginUsernameInput').value.trim();
    const password = document.getElementById('loginPasswordInput').value;
    const currentDeviceID = getDeviceID(); // Get this device's unique ID
    
    if (!username || !password) {
        alert('කරුණාකර Username සහ Password ඇතුළු කරන්න.');
        return;
    }

    const users = getStoredUsers();
    const userData = users[username];

    if (!userData) {
        alert('වැරදි Username එකක්. නැවත උත්සාහ කරන්න.');
        return;
    }
    
    // 1. Password Check
    if (userData.password !== password) {
        alert('වැරදි Password එකක්. නැවත උත්සාහ කරන්න.');
        return;
    }

    // 2. DEVICE ID CHECK (THE SECURITY LAYER)
    if (userData.deviceID !== currentDeviceID) {
        alert('⚠️ Login අසාර්ථකයි. මෙම ගිණුම වෙනත් උපාංගයක (Device) ලියාපදිංචි කර ඇත.');
        return;
    }

    // Success
    localStorage.setItem(LOGIN_KEY, 'true');
    localStorage.setItem('currentUsername', username); 
    alert('පිවිසීම සාර්ථකයි! ඔබ දැන් App එක භාවිත කළ හැක.');
    checkLoginStatus();
}

function logoutUser() {
    if (confirm('ඔබට ඉවත් වීමට (Log Out) අවශ්‍ය බව ස්ථිරද?')) {
        localStorage.removeItem(LOGIN_KEY);
        localStorage.removeItem('currentUsername');
        alert('ඔබ සාර්ථකව ඉවත් විය.');
        checkLoginStatus();
    }
}

function checkLoginStatus() {
    // Ensure Device ID is generated before checking status
    getDeviceID(); 
    
    const isLoggedIn = localStorage.getItem(LOGIN_KEY);
    const loginContainer = document.getElementById('loginContainer');
    const registerContainer = document.getElementById('registerContainer');
    const appContent = document.getElementById('appContent');
    
    if (isLoggedIn === 'true') {
        loginContainer.style.display = 'none';
        registerContainer.style.display = 'none';
        appContent.style.display = 'flex';
        toggleInputMode();
    } else {
        appContent.style.display = 'none';
        registerContainer.style.display = 'none';
        loginContainer.style.display = 'flex';
        
        document.getElementById('loginUsernameInput').value = ''; 
        document.getElementById('loginPasswordInput').value = '';
        document.getElementById('regUsernameInput').value = '';
        document.getElementById('regPasswordInput').value = '';
    }
}

// --- EXISTING APP FUNCTIONS ---

function toggleInputMode(){
  timePickerMode = !timePickerMode;
  const t1=document.getElementById('t1');
  const t2=document.getElementById('t2');
  const modeBtn=document.getElementById('modeBtn');
  if(timePickerMode){
    t1.type='time'; t2.type='time'; t1.placeholder='Start time'; t2.placeholder='End time';
    t1.removeAttribute('inputmode'); t2.removeAttribute('pattern'); modeBtn.innerText='Mode: Picker';
  } else {
    t1.type='text'; t2.type='text'; t1.placeholder='HH:MM:SS'; t2.placeholder='HH:MM:SS';
    t1.setAttribute('inputmode','numeric'); t2.setAttribute('inputmode','numeric');
    t1.setAttribute('pattern','[0-9:]*'); t2.setAttribute('pattern','[0-9:]*');
    modeBtn.innerText='Mode: Text';
  }
}

function calc(){
  const t1=document.getElementById('t1').value;
  const t2=document.getElementById('t2').value;
  if(!t1||!t2){alert('Enter both times'); return;}
  let h1,m1,s1,h2,m2,s2;
  if(timePickerMode){
    [h1,m1,s1]=t1.split(':').map(Number);
    [h2,m2,s2]=t2.split(':').map(Number);
  } else {
    const arr1=t1.split(':').map(Number);
    const arr2=t2.split(':').map(Number);
    h1=arr1[0]; m1=arr1[1]; s1=arr1[2]||0;
    h2=arr2[0]; m2=arr2[1]; s2=arr2[2]||0;
  }
  const now=new Date();
  const d1=new Date(now.getFullYear(),now.getMonth(),now.getDate(),h1,m1,s1);
  const d2=new Date(now.getFullYear(),now.getMonth(),now.getDate(),h2,m2,s2);
  let diff=d2-d1; if(diff<0) diff+=24*60*60*1000;
  const next=new Date(d2.getTime()+diff);
  const hh=String(next.getHours()).padStart(2,'0');
  const mm=String(next.getMinutes()).padStart(2,'0');
  const ss=String(next.getSeconds()).padStart(2,'0');
  const resultText='Next time: '+hh+':'+mm+':'+ss;
  document.getElementById('out').innerText=resultText;

  const riskLabels = document.getElementById('riskLabels');
  riskLabels.style.display = 'block';
  if(riskTimeout) clearTimeout(riskTimeout);
  riskTimeout = setTimeout(()=>{ riskLabels.style.display='none'; }, 180000);

  historyArr.unshift(`Start: ${t1} | End: ${t2} → ${resultText}`);
  if(historyArr.length>50) historyArr.pop();
}

function toggleExtraPanel(){ document.getElementById('extraPanel').classList.toggle('show'); }
function openHistory(){ document.getElementById('historyModal').style.display='flex'; renderHistory(); }
function closeHistory(){ document.getElementById('historyModal').style.display='none'; }
function renderHistory(){ 
    document.getElementById('historyBox').innerHTML = historyArr.map(h=>`<p>${h}</p>`).join(''); 
}
function clearHistory(){ if(confirm('Clear all history?')){ historyArr=[]; renderHistory(); } }
function openHow(){ document.getElementById('howModal').style.display='flex'; }
function closeHow(){ document.getElementById('howModal').style.display='none'; }

function switchTheme(){
  themeMode=(themeMode+1)%2;
  if(themeMode===0) document.body.style.background='#0f1724';
  else document.body.style.background='#222244';
}

// Initialize Device ID and hide loading screen
document.addEventListener('DOMContentLoaded', () => {
    // Initialize Device ID immediately
    getDeviceID(); 
    // Hide loading screen after 1.5 seconds
    setTimeout(hideLoadingScreen, 1500); 
});
</script>
</body>
</html>
