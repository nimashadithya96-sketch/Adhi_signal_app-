<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ADHI Turbo Crash Signal App</title>
<style>
/* --- 1. GENERAL STYLES (Enhanced) --- */
body { 
    font-family: 'Inter', sans-serif; 
    margin:0; 
    padding:0; 
    display:flex; 
    flex-direction:column; 
    align-items:center; 
    min-height:100vh; 
    background: linear-gradient(135deg, #0f172a, #1e293b); /* Deeper, gradient background */
    color:#fff; 
    transition: background-color 0.3s; 
}
h1 { 
    color:#39ff14; 
    margin-bottom:18px; 
    text-align:center; 
    padding-top: 30px; 
    text-shadow: 0 0 15px rgba(57, 255, 20, 0.8), 0 0 5px rgba(57, 255, 20, 0.4); /* Stronger glow */
    letter-spacing: 1.5px;
}
h2 { color: #00bcd4; }
label { font-size:14px; color:#a0a0a0; margin-bottom:3px; }
button { 
    padding:12px 18px; 
    border-radius:12px; 
    border:0; 
    font-weight:800; 
    cursor:pointer; 
    transition: all 0.2s ease; 
    box-shadow: 0 6px 15px rgba(0,0,0,0.4); 
}
button:hover { 
    transform: translateY(-2px); 
    box-shadow: 0 8px 20px rgba(0,0,0,0.5); 
}

/* --- NEW: HACKER CODE CANVAS STYLES (Full Screen) --- */
#hackerCodeCanvas {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: -1; /* Place behind the content */
    display: none; /* Controlled by JS */
}
/* --- END HACKER BACKGROUND STYLES --- */


/* --- INPUT/FORM STYLES (Enhanced) --- */
input { 
    padding:14px; 
    border-radius:10px; 
    border: 2px solid #3a4257; 
    width:100%; 
    text-align:center; 
    font-size:16px;
    background-color: #1a2333; 
    color: #ffffff; 
    box-shadow: inset 0 2px 4px rgba(0,0,0,0.5);
    /* Make sure input inside password-wrapper doesn't stretch weirdly */
    box-sizing: border-box; 
}
/* Password Input specific padding for the icon */
.password-wrapper input {
    padding-right: 45px; 
}

/* --- Password Toggle Icon Styles --- */
.password-wrapper {
    position: relative;
    width: 100%;
}
.password-toggle {
    position: absolute;
    right: 12px;
    top: 50%;
    transform: translateY(-50%);
    cursor: pointer;
    color: #94a3b8; /* Icon color */
    transition: color 0.2s;
    padding: 5px; /* Increase touch target area */
    line-height: 0; /* Fix vertical alignment issue */
}
.password-toggle:hover {
    color: #fff;
}
.password-toggle svg {
    width: 20px;
    height: 20px;
    display: block;
}

/* --- 2. LAYOUT AND SPACING (Login/App Comfort) --- */
#appContent, #loginContainer, #registerContainer { 
    display:flex;
    flex-direction:column;
    align-items:center;
    width:90%;
    max-width:480px; 
    position:relative;
    padding: 40px; /* Increased padding for comfort */
    background: #1e293b; /* Slightly lighter inner background */
    border-radius: 25px; /* More rounded corners */
    /* Added green glow and strong shadow */
    box-shadow: 0 0 30px rgba(57, 255, 20, 0.1), 0 15px 40px rgba(0,0,0,0.9); 
    border: 3px solid #2d3b50; /* Thicker border */
    gap: 30px; /* Increased internal spacing */
    z-index: 10; /* Ensure content is above hacker background */
}
.input-group { 
    display:flex;
    flex-direction:column;
    gap: 5px; 
    width:100%;
}

/* --- NEW: REAL TIME CLOCK --- */
#realTimeClock {
    font-size: 32px;
    font-weight: 900;
    color: #39ff14; /* Neon Green */
    text-shadow: 0 0 10px rgba(57, 255, 20, 0.8), 0 0 5px rgba(57, 255, 20, 0.4);
    margin-bottom: 20px;
    text-align: center;
    width: 100%;
    padding: 10px;
    background-color: #0d121c;
    border-radius: 10px;
    border: 1px solid #39ff14;
}

/* --- 3. COMPONENT STYLES --- */
#generateBtn { /* Renamed to #generateBtn */
    width:100%; 
    background:linear-gradient(45deg, #ff0055, #ff6600); /* Hotter gradient */
    color:#fff; 
    font-size:22px; 
    text-transform: uppercase;
}
#generateBtn:active { background:linear-gradient(45deg, #dd0044, #ee5500); transform: translateY(0); }

/* Login/Register Button Comfort Styles */
#loginBtn, #registerBtn { 
    width:100%; 
    background:linear-gradient(45deg, #00bcd4, #0096a8); /* Blue gradient */
    color:#fff; 
    font-size:18px; 
    margin-top:15px; 
    box-shadow: 0 4px 10px rgba(0, 188, 212, 0.5);
}
#loginBtn:hover, #registerBtn:hover {
    background:linear-gradient(45deg, #0096a8, #00bcd4);
    box-shadow: 0 6px 15px rgba(0, 188, 212, 0.7);
}
#switchBtn { 
    background: #4f5a77; 
    color: #fff; 
    font-size: 16px; 
    text-transform: uppercase; /* Added for visual consistency */
    margin-top: 10px;
} 
/* REMOVED margin-top:20px; from #logoutBtn to unify spacing */
#logoutBtn { background:#ff6b6b; color:#fff; } 

/* History and How-to buttons that are now displayed directly */
#historyBtn, #howBtn { 
    background:#4f5a77; 
    color:#fff; 
    width:100%; 
    /* Removed margin-top from these, spacing is handled by the container */
}

/* --- Signal Output Area --- */
#signalOutput {
    width: 100%;
    text-align: center;
    margin-top: 25px;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 15px;
    border: 2px dashed #3a4257;
    border-radius: 15px;
    background-color: #1c2a44;
}

/* --- PRE-BET INSTRUCTION --- */
#preBetInstruction {
    background-color: #7b0000; /* Darker red background for warning */
    color: #fff;
    padding: 10px;
    border-radius: 8px;
    margin-bottom: 15px;
    font-weight: 700;
    text-align: center;
    border: 2px solid #ffaa00;
    line-height: 1.4;
    font-size: 15px;
}
#preBetInstruction strong {
    color: #ffaa00; /* Amber highlight for time/round */
    font-size: 16px;
}
/* --- END PRE-BET INSTRUCTION --- */

/* Signal Header Base Style (Will be overridden by JS for highlighting) */
#signalHeader {
    font-size: 14px; /* Reduced size for 'Next Signal Time:' line */
    font-weight: 500;
    color: #94a3b8; /* Lighter color for label */
    margin-bottom: 5px; /* Reduced gap to time */
    width: 100%;
    transition: all 0.3s; /* Smooth transition for color/size change */
}

/* NEW: Style for the actual time/highlighted text */
#signalTimeDisplay {
    font-size: 38px;
    font-weight: 900;
    color: #39ff14; /* Default green */
    text-shadow: 0 0 10px rgba(57, 255, 20, 0.6);
    margin-bottom: 15px;
    transition: all 0.3s;
    line-height: 1;
}

/* Signal Header and Time when it is a BET NOW state */
.bet-now-header #signalHeader {
    font-size: 20px;
    color: #FFDD66; 
    font-weight: 700;
    margin-bottom: 0px; 
}
.bet-now-header #signalTimeDisplay {
    color: #FFDD66; 
    font-size: 44px;
    text-shadow: 0 0 15px #FFDD66, 0 0 5px #FFDD66; 
}
.bet-now-highlight {
    padding: 10px;
    border-radius: 10px;
    background-color: rgba(255, 0, 0, 0.7); 
    border: 3px solid #FFDD66;
}
/* End BET NOW specific styles */


/* New style for the multi-line signal output */
.signal-round {
    display: flex;
    flex-direction: column; /* Stack multipliers vertically */
    gap: 8px; /* Space between each multiplier line */
    padding: 12px 15px;
    background-color: #24344d;
    border-radius: 8px;
    width: 100%;
    box-shadow: 0 2px 5px rgba(0,0,0,0.3);
    margin-bottom: 5px;
    text-align: left;
    font-size: 16px;
}
.multiplier-line {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 100%;
    font-weight: 600;
    padding-bottom: 5px;
    border-bottom: 1px dashed rgba(255, 255, 255, 0.1);
}
.multiplier-line:last-child {
    border-bottom: none;
    padding-bottom: 0;
}

.multiplier-name {
    color: #fff;
    font-weight: 400;
}
.multiplier-value {
    font-weight: 800;
    /* Styles handled inline in JS for colors (Green, Yellow, Red) */
    text-shadow: 0 0 5px rgba(255, 255, 255, 0.5);
}

#statusMessage {
    font-size: 14px;
    color: #00bcd4;
    font-weight: 600;
    margin-top: 15px;
}

/* --- PROMO CODE BOX --- */
#promoBox {
    background-color: #2c3a57;
    padding: 20px; 
    border-radius: 15px;
    width: 100%;
    text-align: center;
    border: 3px solid #ffaa00; 
    margin-top: 20px;
    box-shadow: 0 0 15px rgba(255, 170, 0, 0.5);
}
#promoCodeDisplay {
    font-size: 28px;
    font-weight: 900;
    color: #ffaa00; 
    text-shadow: 0 0 8px rgba(255, 170, 0, 0.8);
    margin: 10px 0;
}
#playNowBtn {
    background: linear-gradient(90deg, #ffaa00, #ff7700);
    color: #000; 
    font-size: 18px;
    width: 90%;
    margin-top: 15px;
}
#copyPromoBtn {
    background: #555;
    color: #fff;
    font-size: 14px;
    padding: 8px 15px;
    margin-top: 5px;
}
#motivationalMsg {
    color:#ffdd66; 
    font-size:15px; 
    font-weight:700; 
    margin-top:15px; 
    margin-bottom:10px;
    padding: 5px 0;
    border-top: 1px solid #4f5a77;
}

/* --- DISCLAIMER --- */
#disclaimer {
    color: #ff6b6b;
    font-weight: 600;
    text-align: center;
    margin-top: 20px;
    padding: 15px;
    border: 2px dashed #ff6b6b;
    border-radius: 10px;
    background-color: rgba(255, 107, 107, 0.08);
    font-size: 13px;
}

/* --- NEW: UNIFIED BOTTOM ACTION GROUP STYLES --- */
.bottom-actions {
    display: flex;
    flex-direction: column;
    width: 100%;
    gap: 12px; /* Uniform spacing between all three buttons */
    margin-top: 25px; /* Clear separation from Disclaimer */
}

/* --- Loading Screen Styles (NEW ANIMATION) --- */
#loading-screen {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: #0f172a; 
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    z-index: 9999;
    transition: opacity 0.5s ease-out; 
    overflow: hidden; /* Prevent rocket overflow from scrolling */
}

/* The Crash Game Rocket/Plane */
#crashRocket {
    font-size: 50px; 
    position: absolute;
    bottom: 30%; 
    left: 10%;
    transform: rotate(-45deg); 
    animation: flight-sequence 2s ease-in-out forwards;
    text-shadow: 0 0 10px #ff6600;
}

@keyframes flight-sequence {
    0% {
        transform: translate(0, 0) rotate(-45deg);
        opacity: 0.5;
    }
    50% {
        /* Move up and across */
        transform: translate(calc(60vw - 80px), -150px) rotate(-35deg);
        opacity: 1;
    }
    100% {
        /* Move far away and fade */
        transform: translate(calc(100vw - 80px), -250px) rotate(0deg);
        opacity: 0.1; 
    }
}

.loading-bar {
    width: 80%;
    max-width: 300px;
    height: 8px;
    background-color: #3a4257;
    border-radius: 4px;
    overflow: hidden;
    margin-top: 150px; /* Pushed down to clear the flight path */
}
.progress {
    height: 100%;
    width: 0%;
    background-color: #39ff14; 
    animation: progress-fill 2s forwards;
}
@keyframes progress-fill {
    0% { width: 0%; }
    100% { width: 100%; }
}
#loading-message {
    color: #00bcd4; 
    font-size: 18px;
    font-weight: bold;
    text-shadow: 0 0 5px rgba(0, 188, 212, 0.5);
}

/* --- MODAL STYLES (History & How-To) --- */
#historyModal, #howModal { display:none; position:fixed; top:0; left:0; width:100%; height:100%; background:rgba(0,0,0,0.9); justify-content:center; align-items:center; z-index:1000; }
#historyContent, #howContent { 
    background:#1e293b; 
    padding:25px; 
    border-radius:15px; 
    width:90%; 
    max-width:450px; 
    max-height:85%; 
    overflow-y:auto; 
    display:flex; 
    flex-direction:column; 
    gap:15px; 
    border: 2px solid #3a4257;
}
#historyContent h2, #howContent h2 { color:#39ff14; margin-top:0; text-align:center; }
#historyContent p { color:#a0f4e0; padding:8px; border-radius:6px; background:rgba(255,255,255,0.05); font-size:14px; }
#closeHistory, #closeHow, #clearHistoryBtn { background:#ff6b6b; color:#fff; margin-top:10px; }
#clearHistoryBtn { background:#ffaa00; color:#000; }

.special-instruction {
    background: #440000;
    padding: 15px;
    border-radius: 10px;
    border: 2px solid #ff6b6b;
    font-size: 15px;
    font-weight: 700;
    color: #ffdddd;
    line-height: 1.4;
}
.special-instruction strong {
    color: #ffaa00;
    font-size: 16px;
}

/* --- NEW: CUSTOM MESSAGE MODAL (Replacement for alert/confirm) --- */
#messageModal { 
    position:fixed; 
    top:0; 
    left:0; 
    width:100%; 
    height:100%; 
    background:rgba(0,0,0,0.7); 
    justify-content:center; 
    align-items:center; 
    z-index:10000; /* Highest z-index */
}
#messageContent { 
    background:#1e293b; 
    padding:30px; 
    border-radius:15px; 
    max-width:350px; 
    width:80%;
    text-align:center;
    box-shadow: 0 0 20px rgba(0, 188, 212, 0.5);
    border: 3px solid #00bcd4;
}
#messageText { 
    color:#fff; 
    font-size:18px; 
    margin-bottom:20px; 
    font-weight: 500;
}
#messageActions { 
    display:flex; 
    justify-content:center; 
    gap:15px; 
}
#alertOKBtn, #confirmOKBtn {
    background: linear-gradient(45deg, #39ff14, #00bcd4);
    color: #000;
    font-weight: 900;
}
#confirmCancelBtn {
    background: #ff6b6b;
    color: #fff;
    font-weight: 900;
}

</style>
</head>
<body>

<!-- NEW: HACKER CODE CANVAS ELEMENT (Full Screen Background) -->
<canvas id="hackerCodeCanvas"></canvas>

<!-- LOADING SCREEN -->
<div id="loading-screen">
    <!-- Crash Game Rocket/Plane Animation -->
    <div id="crashRocket">🚀</div> 
    
    <div class="loading-bar"><div class="progress"></div></div>
    <div id="loading-message">Loading ADHI Turbo Signal System...</div>
</div>

<!-- CUSTOM ALERT/CONFIRM MODAL -->
<div id="messageModal" style="display: none;">
    <div id="messageContent">
        <p id="messageText">පණිවිඩය මෙතැනින් පෙන්වයි.</p>
        <div id="messageActions">
            <button id="alertOKBtn" style="display:none;" onclick="closeMessageModal()">හරි (OK)</button>
            <button id="confirmCancelBtn" style="display:none;" onclick="handleConfirm(false)">නැත (Cancel)</button>
            <button id="confirmOKBtn" style="display:none;" onclick="handleConfirm(true)">ඔව් (Yes)</button>
        </div>
    </div>
</div>

<!-- MAIN APP INTERFACE -->
<h1>ADHI TURBO CRASH SIGNAL 🚀</h1>

<!-- LOGIN FORM -->
<div id="loginContainer" style="display: none;">
    <h2 style="color:#00bcd4;">පද්ධතියට පිවිසෙන්න</h2>
    <div class="input-group"><label for="loginUsernameInput">Username</label><input id="loginUsernameInput" type="text" placeholder="ඔබේ Username ඇතුළු කරන්න" required></div>
    
    <div class="input-group">
        <label for="loginPasswordInput">Password</label>
        <div class="password-wrapper">
            <input id="loginPasswordInput" type="password" placeholder="Password ඇතුළු කරන්න" required>
            <!-- Password Toggle Icon -->
            <span class="password-toggle" onclick="togglePasswordVisibility('loginPasswordInput', this)">
                <!-- Eye Icon (lucide-eye - initial state, password hidden) -->
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="lucide lucide-eye"><path d="M2 12s3-7 10-7 10 7 10 7-3 7-10 7-10-7-10-7Z"/><circle cx="12" cy="12" r="3"/></svg>
            </span>
        </div>
    </div>
    
    <!-- Changed button text -->
    <button id="loginBtn" onclick="loginUser()">LOGIN</button>
    <!-- Changed button text -->
    <button id="switchBtn" onclick="showRegister()">REGISTER NOW</button>
</div>

<!-- REGISTRATION FORM -->
<div id="registerContainer" style="display: none;">
    <h2 style="color:#ffaa00;">නව ගිණුමක් සාදන්න</h2>
    <div class="input-group"><label for="regUsernameInput">Username</label><input id="regUsernameInput" type="text" placeholder="Username (අවම අකුරු 4)" required></div>
    
    <div class="input-group">
        <label for="regPasswordInput">Password</label>
        <div class="password-wrapper">
            <input id="regPasswordInput" type="password" placeholder="Password (අවම අකුරු 6)" required>
            <!-- Password Toggle Icon -->
            <span class="password-toggle" onclick="togglePasswordVisibility('regPasswordInput', this)">
                 <!-- Eye Icon (lucide-eye - initial state, password hidden) -->
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="lucide lucide-eye-off"><path d="M9.88 9.88a3 3 0 1 0 4.24 4.24"/><path d="M10.73 5.08A10.43 10.43 0 0 1 12 5c2.1 0 4.1.84 5.8 2.37l1.44 1.44"/><path d="M2.5 12c.7-1.3 1.5-2.5 2.5-3.6 1-1.1 1.9-2.2 3.1-3.1"/><path d="M14.7 18.42A10.15 10.15 0 0 1 12 19c-2.1 0-4.1-.84-5.8-2.37l-1.44-1.44"/><path d="M19.5 12c-.7 1.3-1.5 2.5-2.5 3.6-1 1.1-1.9 2.2-3.1 3.1"/><line x1="2" x2="22" y1="2" y2="22"/></svg>
            </span>
        </div>
    </div>
    
    <button id="registerBtn" onclick="registerUser()">REGISTER ACCOUNT</button>
    <button id="switchBtn" onclick="showLogin()">Switch to Login</button>
</div>

<!-- APP CONTENT -->
<div id="appContent" style="display: none;">
  <div class="box" style="gap: 30px; width: 100%;"> 
    
    <!-- REAL TIME CLOCK -->
    <div id="realTimeClock">--:--:--</div>

    <!-- Button renamed to GENERATE SIGNAL -->
    <button id="generateBtn" onclick="displayCurrentSignal()">GENERATE SIGNAL</button>
    
    <!-- SIGNAL OUTPUT AREA -->
    <div id="signalOutput">
        
        <!-- PRE-BET INSTRUCTION SLOT -->
        <div id="preBetInstruction" style="display: none;"></div>
        
        <!-- Updated structure for time display -->
        <div id="timeDisplayContainer">
            <div id="signalHeader">Signal සඳහා සූදානම්...</div>
            <div id="signalTimeDisplay">--:--</div>
        </div>
        <!-- End Updated structure -->

        <div id="signalRounds" style="width: 100%;">
            <!-- Initial Signal Output Structure -->
            <div class="signal-round">
                <div class="multiplier-line"><span class="multiplier-name">2x:</span><span class="multiplier-value" style="color:#39ff14;">✅</span></div>
                <div class="multiplier-line"><span class="multiplier-name">3x:</span><span class="multiplier-value" style="color:#ffaa00;">⚠️️</span></div>
                <div class="multiplier-line"><span class="multiplier-name">5x - 10x:</span><span class="multiplier-value" style="color:#ff6b6b;">☠️⚠️️</span></div>
            </div>
        </div>
        <div id="statusMessage">GENERATE SIGNAL බොත්තම ඔබා වර්තමාන Signal කාලය දැන ගන්න.</div>
    </div>
    
    <!-- PROMO CODE & PLAY NOW -->
    <div id="promoBox">
        <p style="color:#fff; font-size:14px; font-weight:600; margin-bottom:5px;">ඔබගේ විශේෂ ප්‍රවර්ධන කේතය (Bonus Code):</p>
        <div id="promoCodeDisplay">1x_3660569</div>
        <button id="copyPromoBtn" onclick="copyPromoCode()">Copy Code</button>
        
        <!-- MOTIVATIONAL MESSAGE -->
        <p id="motivationalMsg">
            ඔබ තවමත් lost නම්, **ඉක්මනින් Promo Code එක යොදා නව ගිණුමක් සාදා** play කර ජයග්‍රහණය කරන්න!
        </p>
        
        <button id="playNowBtn" onclick="open1xBet()">Play Now & Register 🚀</button>
    </div>

    <div id="disclaimer">
        ⚠️ **අවවාදයයි:** මෙය ගණිතමය සිමියුලේෂන් එකක් පමණි. කිසිදු ජයග්‍රහණයක් සහතික කළ නොහැක. ඔබගේ වගකීම මත පමණක් භාවිතා කරන්න.
    </div>
    
    <!-- START: UNIFIED BOTTOM ACTION GROUP (For Balance) -->
    <div class="bottom-actions">
      <button id="historyBtn" onclick="openHistory()">Signal History</button>
      <button id="howBtn" onclick="openHow()">භාවිතයට උපදෙස්</button>
      <button id="logoutBtn" onclick="logoutUser()">Log Out</button>
    </div>
    <!-- END: UNIFIED BOTTOM ACTION GROUP -->

  </div>
</div>

<!-- MODALS -->
<div id="historyModal">
  <div id="historyContent">
    <h2>Signal History</h2>
    <div id="historyBox"></div>
    <button id="clearHistoryBtn" onclick="clearHistory()">Clear History</button>
    <button id="closeHistory" onclick="closeHistory()">Close</button>
  </div>
</div>

<div id="howModal">
  <div id="howContent">
    <h2>භාවිතයට උපදෙස්</h2>
    <p>මෙම App එක **Crash Game** එකක ප්‍රතිඵලය ගණිතමය වශයෙන් අනුරූපණය (Simulate) කිරීම සඳහා නිර්මාණය කර ඇත.</p>
    
    <!-- SPECIAL INSTRUCTION SECTION (Promo Code Requirement) -->
    <h3 style="color:#ffaa00; margin-top:5px;">✅ විශේෂයෙන් මෙය අනුගමනය කරන්න:</h3>
    <div class="special-instruction">
        <p>මෙහි **win** කිරීමට නම්,</p>
        <ol style="padding-left: 18px; margin: 10px 0;">
            <li style="margin-bottom: 8px;">අනිවාර්යයෙන්ම 1xBet හි **නව ගිණුමක්** විය යුතුමයි..!</li>
            <li style="margin-bottom: 8px;">එහි **<strong id="promoCodeInModal">1x_3660569</strong>** යන promo code එක භාවිතයෙන් සාදන ලද account එකක් විය යුතුමයි.</li>
        </ol>
        <p style="margin-top: 15px;">එයට හේතුව: **මේ Promo Code එකෙන් සාදන Account සියල්ලටම Run වෙන්නේ එකම Algorithm පද්ධතිය නිසා. 💥**</p>
        <p style="margin-top: 15px;">**⚠️ අවමය:** ගිණුමෙහි අවම වශයෙන් **2000LKR** පමණ රඳවා ගන්න.</p>
    </div>
    
    <h3 style="font-weight:700; color:#39ff14;">භාවිතා කරන ආකාරය:</h3>
    <p>මෙම පද්ධතිය **පෙර ගණනය කරන ලද කාලසටහනකට** අනුව ක්‍රියාත්මක වේ.</p>
    <ol style="margin-top:0;">
        <li><span style="font-weight:bold;">GENERATE SIGNAL</span> බොත්තම ඔබන්න.</li>
        <li>පද්ධතිය, **වර්තමාන වේලාවට** අදාළ හෝ ඊළඟට එන Signal කාලසටහන පෙන්වනු ඇත.</li>
        <li>**🚨 අති විශේෂ උපදෙස්:** ඔබ Signal වේලාවට **කලින් විනාඩියේ** ඇති Round 3 හි ප්‍රතිඵල බලා, ඊළඟට (Signal වේලාවේ) එන **ඊලගට ආරම්භ වන round එක BET කළ යුතුය.**</li>
        <li>Signal එක සඳහා **1.00x - 30.00x** අතර ආරක්ෂිත Multiplier අගයන් නිර්දේශ කර ඇත.</li>
    </ol>
    <p style="font-style:italic;">**Play Now** බොත්තම මඟින් ඔබගේ ගිණුම සාදා ගැනීමට යොමු වේ.</p>
    <p style="color:#ff6b6b; font-weight:bold;">⚠️ මතක තබා ගන්න: මෙය අහඹු ක්‍රීඩාවකි. මෙම App එකේ Signal කිසිදු ජයග්‍රහණයක් **සහතික නොකරයි**.</p>
    <button id="closeHow" onclick="closeHow()">Close</button>
  </div>
</div>

<script>
// --- CUSTOM MESSAGE MODAL LOGIC (Replaces alert/confirm) ---
let confirmCallback = null;

function closeMessageModal() {
    document.getElementById('messageModal').style.display = 'none';
}

function handleConfirm(result) {
    closeMessageModal();
    if (confirmCallback) {
        confirmCallback(result);
        confirmCallback = null;
    }
}

function customAlert(message) {
    document.getElementById('messageText').innerText = message;
    document.getElementById('alertOKBtn').style.display = 'block';
    document.getElementById('confirmCancelBtn').style.display = 'none';
    document.getElementById('confirmOKBtn').style.display = 'none';
    document.getElementById('messageModal').style.display = 'flex';
}

function customConfirm(message, callback) {
    confirmCallback = callback;
    document.getElementById('messageText').innerText = message;
    document.getElementById('alertOKBtn').style.display = 'none';
    document.getElementById('confirmCancelBtn').style.display = 'block';
    document.getElementById('confirmOKBtn').style.display = 'block';
    document.getElementById('messageModal').style.display = 'flex';
}
// --- END CUSTOM MESSAGE MODAL LOGIC ---


// --- CONFIGURATION ---
const PARTNER_PROMO_CODE = "1x_3660569";
// --- THIS LINK IS NOW UPDATED ---
const PARTNER_URL = "https://refpa58144.com/L?tag=d_4844655m_1236c_adhi_crash_app&site=4844655&ad=1236"; 

// --- SECURITY CONSTANTS ---
const LOGIN_KEY = "isLoggedIn"; 
const USERS_KEY = "adhiUsers"; 
const DEVICE_KEY = "Adhi_Device_UUID"; 

// --- APP VARIABLES ---
let historyArr = [];
let signalSchedule = {}; 

// --- HACKER CODE RAIN VARIABLES ---
let matrixInterval = null;
const hackerTextFont = 'monospace';
const fontSize = 16;
let drops = [];
let canvas, ctx;
let columns;
let targetText = '';

// New Multiplier Structure
const MULTIPLIER_DATA = [
    { name: "2x", value: "✅", color: "#39ff14" }, // Green: Safe/Guaranteed
    { name: "3x", value: "⚠️️", color: "#ffaa00" }, // Amber: Caution
    { name: "5x - 10x", value: "☠️⚠️️", color: "#ff6b6b" } // Red: High Risk/High Reward
];


// --- HACKER CODE RAIN LOGIC (Full Screen Canvas) ---
function initializeHackerCanvas() {
    canvas = document.getElementById('hackerCodeCanvas');
    ctx = canvas.getContext('2d');
    
    resizeHackerCanvas();
    window.addEventListener('resize', resizeHackerCanvas);
}

function resizeHackerCanvas() {
    if (!canvas) return;
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
    
    // Calculate columns based on the font size
    columns = Math.floor(canvas.width / fontSize);
    
    // Initialize drops array for the new number of columns
    drops = [];
    for (let x = 0; x < columns; x++) {
        drops[x] = 1; // Start y coordinate for each column
    }
}

function drawHackerRain() {
    if (!ctx) return;
    
    // 1. Draw a semi-transparent background for the fading trail effect
    // Color: #0f172a background with slight transparency (0.05)
    ctx.fillStyle = 'rgba(15, 23, 42, 0.05)'; 
    ctx.fillRect(0, 0, canvas.width, canvas.height);

    // 2. Set the text style for the code rain
    ctx.fillStyle = '#39ff14'; // Neon Green
    ctx.font = `${fontSize}px ${hackerTextFont}`;

    // 3. Draw the characters for each drop
    for (let i = 0; i < drops.length; i++) {
        // Generate a random character (mix of numbers, letters, and symbols)
        const text = String.fromCharCode(33 + Math.random() * 94);
        
        // Draw the character
        ctx.fillText(text, i * fontSize, drops[i] * fontSize);

        // Send the drop back to the top randomly after reaching the bottom
        if (drops[i] * fontSize > canvas.height && Math.random() > 0.975) {
            drops[i] = 0;
        }

        // Increment the y-coordinate for the next frame
        drops[i]++;
    }
    
    // 4. Draw the central target text (LOGIN / REGISTER NOW)
    if (targetText) {
        ctx.fillStyle = 'rgba(57, 255, 20, 0.9)'; // Brighter green for central text
        ctx.font = `bold 48px 'Inter', sans-serif`;
        ctx.textAlign = 'center';
        ctx.textBaseline = 'middle';
        ctx.shadowColor = '#39ff14';
        ctx.shadowBlur = 15;
        
        ctx.fillText(targetText, canvas.width / 2, canvas.height / 2);
        ctx.shadowBlur = 0; // Reset shadow
    }
}

function updateHackerBackground(text, isVisible) {
    const canvas = document.getElementById('hackerCodeCanvas');
    targetText = text.toUpperCase();

    if (isVisible) {
        if (!canvas) return;
        canvas.style.display = 'block';
        
        if (!matrixInterval) {
            // Start the animation loop if it's not running
            matrixInterval = setInterval(drawHackerRain, 50); // ~20 FPS
        }
    } else {
        if (!canvas) return;
        canvas.style.display = 'none';
        
        if (matrixInterval) {
            clearInterval(matrixInterval);
            matrixInterval = null;
        }
    }
}
// --- END HACKER CODE RAIN LOGIC ---


// --- DEVICE ID GENERATION & INITIALIZATION ---
function generateUUID() {
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
    }
    return deviceID;
}

// --- UTILITY FUNCTIONS ---
function copyToClipboard(text) {
    const textarea = document.createElement('textarea');
    textarea.value = text;
    document.body.appendChild(textarea);
    textarea.select();
    try {
        const successful = document.execCommand('copy');
        if (successful) {
            // Using customAlert instead of native alert()
            customAlert('Promo Code එක Copy කර ඇත!');
        } else {
            customAlert('Copy කිරීමට අසමත් විය. කරුණාකර Code එක අතින් Copy කරන්න: ' + text);
        }
    } catch (err) {
        customAlert('Copy කිරීමට අසමත් විය. කරුණාකර Code එක අතින් Copy කරන්න: ' + text);
    }
    document.body.removeChild(textarea);
}

// Helper to get the previous minute from HH:MM string
function getPreviousMinute(timeStr) {
    const [h, m] = timeStr.split(':').map(Number);
    let totalMinutes = h * 60 + m;
    totalMinutes = (totalMinutes - 1 + 1440) % 1440; // Subtract 1 minute and wrap around 24 hours (1440 min)

    const prevH = Math.floor(totalMinutes / 60);
    const prevM = totalMinutes % 60;
    
    return `${String(prevH).padStart(2, '0')}:${String(prevM).padStart(2, '0')}`;
}

// --- PASSWORD TOGGLE FUNCTION ---
function togglePasswordVisibility(inputId, iconElement) {
    const input = document.getElementById(inputId);
    if (input.type === 'password') {
        input.type = 'text';
        // Change icon to 'eye-off' (password is now visible)
        iconElement.innerHTML = `<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="lucide lucide-eye-off"><path d="M9.88 9.88a3 3 0 1 0 4.24 4.24"/><path d="M10.73 5.08A10.43 10.43 0 0 1 12 5c2.1 0 4.1.84 5.8 2.37l1.44 1.44"/><path d="M2.5 12c.7-1.3 1.5-2.5 2.5-3.6 1-1.1 1.9-2.2 3.1-3.1"/><path d="M14.7 18.42A10.15 10.15 0 0 1 12 19c-2.1 0-4.1-.84-5.8-2.37l-1.44-1.44"/><path d="M19.5 12c-.7 1.3-1.5 2.5-2.5 3.6-1 1.1-1.9 2.2-3.1 3.1"/><line x1="2" x2="22" y1="2" y2="22"/></svg>`;
    } else {
        input.type = 'password';
        // Change icon to 'eye' (password is now hidden)
        iconElement.innerHTML = `<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="lucide lucide-eye"><path d="M2 12s3-7 10-7 10 7 10 7-3 7-10 7-10-7-10-7Z"/><circle cx="12" cy="12" r="3"/></svg>`;
    }
}
// --- END: PASSWORD TOGGLE FUNCTION ---

// --- CORE: REAL TIME CLOCK ---
function updateClock() {
    const now = new Date();
    const h = String(now.getHours()).padStart(2, '0');
    const m = String(now.getMinutes()).padStart(2, '0');
    const s = String(now.getSeconds()).padStart(2, '0');
    const clockElement = document.getElementById('realTimeClock');
    if (clockElement) {
        clockElement.innerText = `${h}:${m}:${s}`;
    }
}

// --- CORE: SCHEDULE GENERATION LOGIC ---
function generateFullSchedule() {
    const schedule = {};
    let currentHour = 0;
    let currentMinute = 2; // Start time: 00:02
    let intervalIndex = 0;
    // Alternating 3 mins, 2 mins intervals (as requested)
    const intervals = [3, 2]; 

    // Loop through 24 hours (1440 minutes)
    while (currentHour < 24) {
        // Stop condition: 23:57 PM (11:57 PM) is the last signal
        if (currentHour === 23 && currentMinute > 57) {
            break; 
        }

        const timeString = `${String(currentHour).padStart(2, '0')}:${String(currentMinute).padStart(2, '0')}`;
        
        // Signal definition: Store the Multiplier Data directly
        schedule[timeString] = MULTIPLIER_DATA;

        // Calculate next time
        const interval = intervals[intervalIndex % 2];
        currentMinute += interval;

        if (currentMinute >= 60) {
            currentHour += Math.floor(currentMinute / 60);
            currentMinute = currentMinute % 60;
        }

        intervalIndex++;
        
        if (currentHour >= 24) {
             break;
        }
    }
    return schedule;
}


// Finds the *next* signal time (T) that is >= current time
function findNearestSignalSlot(schedule) {
    const now = new Date();
    const currentHour = now.getHours();
    const currentMinute = now.getMinutes();
    const nowInMinutes = currentHour * 60 + currentMinute;

    const times = Object.keys(schedule).sort();
    let nextSignalTime = null;

    // 1. Look for an upcoming signal today
    for (const timeStr of times) {
        const [h, m] = timeStr.split(':').map(Number);
        const scheduledInMinutes = h * 60 + m;

        // Find the first scheduled time that is >= current time
        if (scheduledInMinutes >= nowInMinutes) {
            nextSignalTime = timeStr;
            break;
        }
    }

    // 2. If no signal found today, use the first signal of the next day (00:02)
    if (!nextSignalTime) {
        nextSignalTime = times[0]; 
        return {
            time: nextSignalTime,
            signal: schedule[nextSignalTime],
            isTomorrow: true
        };
    }
    
    return {
        time: nextSignalTime,
        signal: schedule[nextSignalTime],
        isTomorrow: false
    };
}


function displayCurrentSignal() {
    // Ensure schedule is generated
    if (Object.keys(signalSchedule).length === 0) {
        signalSchedule = generateFullSchedule();
    }
    
    const timeDisplayContainer = document.getElementById('timeDisplayContainer');
    const headerDiv = document.getElementById('signalHeader');
    const timeDiv = document.getElementById('signalTimeDisplay');
    const roundsDiv = document.getElementById('signalRounds');
    const statusDiv = document.getElementById('statusMessage');
    const preBetDiv = document.getElementById('preBetInstruction');
    
    const now = new Date();
    const nowH = String(now.getHours()).padStart(2, '0');
    const nowM = String(now.getMinutes()).padStart(2, '0');
    const nowTimeStr = `${nowH}:${nowM}`;

    let isBetTime = false;
    let targetSignalTime = null;
    let targetSignalData = null;
    let isTomorrow = false;

    // 1. Check if the current minute is a scheduled signal time (NOW BET TIME)
    if (signalSchedule[nowTimeStr]) {
        isBetTime = true;
        targetSignalTime = nowTimeStr;
        targetSignalData = signalSchedule[nowTimeStr];
    } else {
        // 2. If not, find the next signal slot (NEXT SIGNAL)
        const nearestSlot = findNearestSignalSlot(signalSchedule); 
        targetSignalTime = nearestSlot.time;
        targetSignalData = nearestSlot.signal;
        isTomorrow = nearestSlot.isTomorrow;
    }
    
    const timeDisplay = targetSignalTime;
    const timeBefore = getPreviousMinute(timeDisplay);
    
    // --- RESET STYLES ---
    timeDisplayContainer.classList.remove('bet-now-highlight');
    timeDisplayContainer.classList.remove('bet-now-header');
    headerDiv.innerHTML = 'Next Signal Time:'; // Default label
    timeDiv.style.color = '#39ff14'; // Default time color
    timeDiv.style.fontSize = '38px';
    timeDiv.style.textShadow = '0 0 10px rgba(57, 255, 20, 0.6)';

    preBetDiv.style.display = 'block'; 
    preBetDiv.style.backgroundColor = '#7b0000';
    preBetDiv.style.borderColor = '#ffaa00';
    // --- END RESET ---


    if (isBetTime) {
        // Scenario A: NOW BET TIME (HIGHLY HIGHLIGHTED)
        timeDisplayContainer.classList.add('bet-now-highlight', 'bet-now-header');
        headerDiv.innerHTML = `🚨 NOW BET TIME! 🚀`; // Override label
        
        statusDiv.innerText = "ඔබගේ ගිණුමට පිවිස වහාම BET කරන්න! 🤑";
        
        preBetDiv.innerHTML = `
            🛑 **දැන්ම BET කරන්න!** (Signal වේලාව: ${timeDisplay}). Multiplier: **2x✅ | 3x⚠️️ | 5x-10x☠️⚠️️**
        `;
        preBetDiv.style.backgroundColor = '#AA0000'; // Darker red for urgency
        preBetDiv.style.borderColor = '#FFDD66';


    } else {
        // Scenario B: NEXT SIGNAL (Wait Time)
        // Header and Time are set to default 'Next Signal Time:' and green time.
        
        if (isTomorrow) {
            statusDiv.innerText = "දැනට Signal කාලසටහන අවසන්. හෙට 00:02 AM න් පසු නැවත උත්සාහ කරන්න.";
            preBetDiv.style.display = 'none';
        } else {
            statusDiv.innerText = "Signal එක ලැබෙන තෙක් රැඳී සිටින්න. මෙම Multiplier අගයන් 1xBet හි ප්‍රවර්ධන කේතය සහිත ගිණුම් සඳහා පමණි.";
            
            preBetDiv.innerHTML = `
                🛑 **Signal එක ලැබීමට ආසන්නයි.** ${timeBefore} විනාඩියේ Round 3 බලා, ඊලගට එන **${timeDisplay}** Round එක BET කරන්න.
            `;
        }
    }
    
    // Set the time display
    timeDiv.innerText = timeDisplay;

    // Render the signal data (New Multiplier Structure)
    roundsDiv.innerHTML = '';
    
    const roundElement = document.createElement('div');
    roundElement.className = 'signal-round';

    let historyLog = `${timeDisplay} | `;

    targetSignalData.forEach(item => {
        const line = document.createElement('div');
        line.className = 'multiplier-line';
        line.innerHTML = `
            <span class="multiplier-name">${item.name}:</span>
            <span class="multiplier-value" style="color:${item.color};">${item.value}</span>
        `;
        roundElement.appendChild(line);
        historyLog += `${item.name}${item.value} `;
    });

    roundsDiv.appendChild(roundElement);
        
    // Save to History
    historyArr.unshift(`${historyLog.trim()} (${isBetTime ? 'BET NOW' : 'NEXT'})`);
    if(historyArr.length > 50) historyArr.pop();
}

// --- PROMO FUNCTIONS ---
function copyPromoCode() {
    copyToClipboard(PARTNER_PROMO_CODE);
}

function open1xBet() {
    window.open(PARTNER_URL, '_blank');
}


// --- LOADING SCREEN ---
function hideLoadingScreen() {
    const loadingScreen = document.getElementById('loading-screen');
    // Ensure the animation has completed before fade out starts
    setTimeout(() => {
        loadingScreen.style.opacity = '0'; 
        // Also set pointer-events to none during the fade to ensure nothing blocks clicks
        loadingScreen.style.pointerEvents = 'none'; 
        setTimeout(() => {
            loadingScreen.style.display = 'none';
            checkLoginStatus(); 
        }, 500); 
    }, 2000); // 2000ms is the duration of the flight-sequence/progress-fill animations
}

// --- DISPLAY/AUTH FUNCTIONS ---
function showLogin() {
    document.getElementById('registerContainer').style.display = 'none';
    document.getElementById('loginContainer').style.display = 'flex';
    updateHackerBackground('LOGIN', true); // Updated to use canvas logic
}

function showRegister() {
    document.getElementById('loginContainer').style.display = 'none';
    document.getElementById('registerContainer').style.display = 'flex';
    updateHackerBackground('REGISTER NOW', true); // Updated to use canvas logic
}

function getStoredUsers() {
    const usersJson = localStorage.getItem(USERS_KEY);
    return usersJson ? JSON.parse(usersJson) : {};
}

function registerUser() {
    const username = document.getElementById('regUsernameInput').value.trim();
    const password = document.getElementById('regPasswordInput').value;
    const currentDeviceID = getDeviceID(); 

    if (username.length < 4 || password.length < 6) {
        // Replaced alert with customAlert
        customAlert('Username අවම අකුරු 4 ක් සහ Password අවම අකුරු 6 ක් විය යුතුය.'); 
        return;
    }

    const users = getStoredUsers();
    if (users[username]) {
        customAlert('මෙම Username එක දැනටමත් භාවිතයේ ඇත. වෙනත් නමක් තෝරන්න.');
        return;
    }

    users[username] = {
        password: password,
        deviceID: currentDeviceID 
    };
    localStorage.setItem(USERS_KEY, JSON.stringify(users));
    
    customAlert('ලියාපදිංචිය සාර්ථකයි! දැන් ඔබට පිවිසිය හැක.');
    showLogin();
    
    document.getElementById('regUsernameInput').value = '';
    document.getElementById('regPasswordInput').value = '';
}

function loginUser() {
    const username = document.getElementById('loginUsernameInput').value.trim();
    const password = document.getElementById('loginPasswordInput').value;
    const currentDeviceID = getDeviceID(); 
    
    if (!username || !password) {
        customAlert('කරුණාකර Username සහ Password ඇතුළු කරන්න.');
        return;
    }

    const users = getStoredUsers();
    const userData = users[username];

    if (!userData) {
        customAlert('වැරදි Username එකක්. නැවත උත්සාහ කරන්න.');
        return;
    }
    
    if (userData.password !== password) {
        customAlert('වැරදි Password එකක්. නැවත උත්සාහ කරන්න.');
        return;
    }

    if (userData.deviceID !== currentDeviceID) {
        customAlert('⚠️ Login අසාර්ථකයි. මෙම ගිණුම වෙනත් උපාංගයක (Device) ලියාපදිංචි කර ඇත.');
        return;
    }

    // Success
    localStorage.setItem(LOGIN_KEY, 'true');
    localStorage.setItem('currentUsername', username); 
    customAlert('පිවිසීම සාර්ථකයි! ඔබ දැන් App එක භාවිත කළ හැක.');
    checkLoginStatus();
}

function logoutUser() {
    // Replaced window.confirm() with customConfirm()
    customConfirm('ඔබට ඉවත් වීමට (Log Out) අවශ්‍ය බව ස්ථිරද?', (result) => {
        if (result) {
            localStorage.removeItem(LOGIN_KEY);
            localStorage.removeItem('currentUsername');
            customAlert('ඔබ සාර්ථකව ඉවත් විය.');
            checkLoginStatus();
        }
    });
}

function checkLoginStatus() {
    getDeviceID(); 
    
    const isLoggedIn = localStorage.getItem(LOGIN_KEY);
    const loginContainer = document.getElementById('loginContainer');
    const registerContainer = document.getElementById('registerContainer');
    const appContent = document.getElementById('appContent');
    const timeDisplayContainer = document.getElementById('timeDisplayContainer');
    
    if (isLoggedIn === 'true') {
        loginContainer.style.display = 'none';
        registerContainer.style.display = 'none';
        appContent.style.display = 'flex';
        
        // --- HACKER BG HIDE ---
        updateHackerBackground('', false); 
        
        // Reset output on login
        document.getElementById('signalHeader').innerText = 'Signal සඳහා සූදානම්...';
        document.getElementById('signalTimeDisplay').innerText = '--:--';
        timeDisplayContainer.classList.remove('bet-now-highlight', 'bet-now-header');
        
        // Updated innerHTML to reflect the new structure on reset
        document.getElementById('signalRounds').innerHTML = `
            <div class="signal-round">
                <div class="multiplier-line"><span class="multiplier-name">2x:</span><span class="multiplier-value" style="color:#39ff14;">✅</span></div>
                <div class="multiplier-line"><span class="multiplier-name">3x:</span><span class="multiplier-value" style="color:#ffaa00;">⚠️️</span></div>
                <div class="multiplier-line"><span class="multiplier-name">5x - 10x:</span><span class="multiplier-value" style="color:#ff6b6b;">☠️⚠️️</span></div>
            </div>
        `;
        document.getElementById('statusMessage').innerText = 'GENERATE SIGNAL බොත්තම ඔබා වර්තමාන Signal කාලය දැන ගන්න.';
        document.getElementById('preBetInstruction').style.display = 'none'; // Hide instruction on login

    } else {
        appContent.style.display = 'none';
        registerContainer.style.display = 'none';
        loginContainer.style.display = 'flex';
        
        // --- HACKER BG SHOW (Default: LOGIN) ---
        updateHackerBackground('LOGIN', true); 
        
        document.getElementById('loginUsernameInput').value = ''; 
        document.getElementById('loginPasswordInput').value = '';
        document.getElementById('regUsernameInput').value = '';
        document.getElementById('regPasswordInput').value = '';
    }
}

// --- APP FUNCTIONS ---
function openHistory(){ document.getElementById('historyModal').style.display='flex'; renderHistory(); }
function closeHistory(){ document.getElementById('historyModal').style.display='none'; }
function renderHistory(){ 
    const box = document.getElementById('historyBox');
    box.innerHTML = historyArr.length > 0 
        ? historyArr.map(h=>`<p>${h}</p>`).join('') 
        : '<p style="text-align:center; color:#ffaa00;">No history yet.</p>'; 
}
function clearHistory(){ 
    // Replaced window.confirm() with customConfirm()
    customConfirm('සියලු History ඉවත් කිරීමට අවශ්‍ය බව ස්ථිරද?', (result) => { 
        if(result){ 
            historyArr=[]; 
            renderHistory(); 
        } 
    });
}
function openHow(){ 
    document.getElementById('promoCodeInModal').innerText = PARTNER_PROMO_CODE;
    document.getElementById('howModal').style.display='flex'; 
}
function closeHow(){ document.getElementById('howModal').style.display='none'; }


// Initialize Device ID, generate schedule, and hide loading screen
document.addEventListener('DOMContentLoaded', () => {
    // 1. Initialize Canvas for Hacker Rain
    initializeHackerCanvas();

    // 2. Generate the full 24-hour schedule on load
    signalSchedule = generateFullSchedule();
    
    // 3. Set the promo code display
    document.getElementById('promoCodeDisplay').innerText = PARTNER_PROMO_CODE;
    
    getDeviceID(); 
    
    // 4. Start the real-time clock
    updateClock();
    setInterval(updateClock, 1000); 
    
    // 5. Wait for animations before hiding
    hideLoadingScreen(); 
});
</script>
</body>
</html>
