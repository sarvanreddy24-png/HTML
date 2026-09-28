# 
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Attendance Advisor</title>

<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

<style>
* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
    font-family: Arial, sans-serif;
}

body {        
    background: #f4f7fc;
    color: #172b4d;
}

/* Header */
.header {
    height: 75px;
    background: linear-gradient(90deg, #173b70, #315b9b);
    color: white;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0 30px;
}

.logo {
    display: flex;
    align-items: center;
    gap: 15px;
}

.logo-icon {
    font-size: 38px;
}

.logo h1 {
    font-size: 24px;
}

.logo p {
    font-size: 13px;
    opacity: 0.9;
}

.profile {
    display: flex;
    align-items: center;
    gap: 12px;
}

.profile-icon {
    width: 42px;
    height: 42px;
    background: white;
    color: #315b9b;
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;
}

/* Layout */
.container {
    display: flex;
    min-height: calc(100vh - 75px);
}

/* Sidebar */
.sidebar {
    width: 200px;
    background: white;
    padding: 20px 12px;
    border-right: 1px solid #ddd;
}

.sidebar a {
    display: block;
    padding: 15px;
    margin-bottom: 8px;
    text-decoration: none;
    color: #344b70;
    border-radius: 10px;
    cursor: pointer;
}

.sidebar a:hover,
.sidebar a.active {
    background: #e5efff;
    color: #1764df;
}

/* Main */
.main {
    flex: 1;
    padding: 28px;
}

.welcome {
    margin-bottom: 20px;
}

.welcome h2 {
    font-size: 26px;
}

.welcome p {
    color: #66758f;
    margin-top: 5px;
}

/* Cards */
.cards {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 20px;
}

.card {
    background: white;
    border-radius: 14px;
    padding: 20px;
    box-shadow: 0 3px 15px rgba(0,0,0,0.05);
}

.card h3 {
    margin-bottom: 18px;
}

/* Attendance */
.attendance-box {
    display: flex;
    align-items: center;
    gap: 30px;
}

.circle {
    width: 135px;
    height: 135px;
    border-radius: 50%;
    background: conic-gradient(#12b886 78%, #dcefe8 0);
    display: flex;
    align-items: center;
    justify-content: center;
}

.circle-inner {
    width: 105px;
    height: 105px;
    background: white;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 25px;
    font-weight: bold;
}

.stats p {
    margin: 10px 0;
}

.status {
    background: #dff8ec;
    color: #16855d;
    padding: 8px 15px;
    border-radius: 8px;
    display: inline-block;
}

/* Subjects */
.subject {
    margin-bottom: 18px;
}

.subject-title {
    display: flex;
    justify-content: space-between;
    margin-bottom: 7px;
}

.progress {
    height: 10px;
    background: #e8edf5;
    border-radius: 10px;
    overflow: hidden;
}

.progress-bar {
    height: 100%;
    border-radius: 10px;
}

.blue { background: #2878e8; }
.purple { background: #7950f2; }
.orange { background: #f59f00; }
.green { background: #12b886; }

/* Quick Actions */
.actions {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 12px;
}

.action {
    padding: 18px;
    border-radius: 12px;
    background: #eef5ff;
    cursor: pointer;
    transition: 0.2s;
}

.action:hover {
    transform: translateY(-2px);
    background: #e1edff;
}

.action span {
    font-size: 24px;
}

.action h4 {
    margin-top: 8px;
}

/* Chart */
.chart-card {
    min-height: 300px;
}

/* Leave suggestion */
.suggestion {
    margin-top: 20px;
    background: #e7faf3;
    border: 1px solid #b8ead7;
    border-radius: 14px;
    padding: 20px;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.btn {
    border: none;
    padding: 12px 22px;
    background: #13a873;
    color: white;
    border-radius: 8px;
    cursor: pointer;
    font-weight: bold;
}

.btn:hover {
    background: #0c8e61;
}

/* Chatbot */
.chatbot {
    width: 350px;
    background: white;
    border-left: 1px solid #ddd;
    display: flex;
    flex-direction: column;
}

.chat-header {
    padding: 20px;
    border-bottom: 1px solid #eee;
}

.chat-header h3 {
    margin-bottom: 5px;
}

.chat-header p {
    color: #69778f;
    font-size: 13px;
}

.messages {
    flex: 1;
    padding: 20px;
    overflow-y: auto;
}

.message {
    padding: 13px;
    border-radius: 12px;
    margin-bottom: 12px;
    max-width: 90%;
    line-height: 1.5;
}

.bot {
    background: #f0f4fa;
}

.user {
    background: #dceaff;
    margin-left: auto;
}

.chat-input {
    display: flex;
    padding: 15px;
    border-top: 1px solid #eee;
    gap: 8px;
}

.chat-input input {
    flex: 1;
    border: 1px solid #ccd5e2;
    border-radius: 20px;
    padding: 12px 15px;
    outline: none;
}

.send {
    width: 45px;
    border: none;
    background: #2878e8;
    color: white;
    border-radius: 50%;
    cursor: pointer;
}

/* OD Simulator */
.modal {
    display: none;
    position: fixed;
    inset: 0;
    background: rgba(0,0,0,0.45);
    align-items: center;
    justify-content: center;
    z-index: 10;
}

.modal-box {
    width: 420px;
    background: white;
    padding: 25px;
    border-radius: 15px;
}

.modal-box h2 {
    margin-bottom: 20px;
}

.form-group {
    margin-bottom: 15px;
}

.form-group label {
    display: block;
    margin-bottom: 7px;
    font-weight: bold;
}

.form-group input,
.form-group select {
    width: 100%;
    padding: 11px;
    border: 1px solid #ccd5e2;
    border-radius: 8px;
}

.result {
    margin-top: 15px;
    background: #eef5ff;
    padding: 15px;
    border-radius: 10px;
}

.close {
    float: right;
    cursor: pointer;
    font-size: 20px;
}

/* Responsive */
@media(max-width: 1000px) {
    .chatbot {
        display: none;
    }
}

@media(max-width: 700px) {
    .sidebar {
        display: none;
    }

    .cards {
        grid-template-columns: 1fr;
    }

    .main {
        padding: 15px;
    }

    .header {
        padding: 0 15px;
    }

    .profile {
        display: none;
    }
}
</style>
</head>

<body>

<!-- HEADER -->
<header class="header">

    <div class="logo">
        <div class="logo-icon">🎓</div>

        <div>
            <h1>Attendance Advisor</h1>
            <p>Know Your Attendance • Plan Your Leaves • Stay on Track</p>
        </div>
    </div>

    <div class="profile">
        <div class="profile-icon">👨‍🎓</div>

        <div>
            <b>Hello, Jaswanth</b>
            <br>
            <small>ECE - 2nd Year</small>
        </div>
    </div>

</header>


<div class="container">

<!-- SIDEBAR -->

<nav class="sidebar">

    <a class="active">🏠 Dashboard</a>

    <a>📅 Attendance</a>

    <a onclick="openOD()">📨 Leave Request</a>

    <a onclick="focusChat()">💬 Chatbot</a>

    <a>⚙️ Settings</a>

</nav>


<!-- MAIN CONTENT -->

<main class="main">

    <div class="welcome">
        <h2>Welcome Back, Jaswanth!</h2>
        <p>Here's your attendance overview and quick actions.</p>
    </div>


    <div class="cards">

        <!-- OVERALL ATTENDANCE -->

        <div class="card">

            <h3>Overall Attendance</h3>

            <div class="attendance-box">

                <div class="circle">

                    <div class="circle-inner">
                        78%
                    </div>

                </div>

                <div class="stats">

                    <p>
                        <b>Present Days</b><br>
                        39
                    </p>

                    <p>
                        <b>Total Working Days</b><br>
                        50
                    </p>

                    <span class="status">
                        ✓ On Track
                    </span>

                </div>

            </div>

        </div>


        <!-- SUBJECT ATTENDANCE -->

        <div class="card">

            <h3>Subject-wise Attendance</h3>

            <div class="subject">

                <div class="subject-title">
                    <span>Electronics</span>
                    <b>82%</b>
                </div>

                <div class="progress">
                    <div class="progress-bar blue"
                         style="width:82%"></div>
                </div>

            </div>


            <div class="subject">

                <div class="subject-title">
                    <span>Networks</span>
                    <b>76%</b>
                </div>

                <div class="progress">
                    <div class="progress-bar purple"
                         style="width:76%"></div>
                </div>

            </div>


            <div class="subject">

                <div class="subject-title">
                    <span>DSP</span>
                    <b>70%</b>
                </div>

                <div class="progress">
                    <div class="progress-bar orange"
                         style="width:70%"></div>
                </div>

            </div>


            <div class="subject">

                <div class="subject-title">
                    <span>EMFT</span>
                    <b>85%</b>
                </div>

                <div class="progress">
                    <div class="progress-bar green"
                         style="width:85%"></div>
                </div>

            </div>

        </div>


        <!-- QUICK ACTIONS -->

        <div class="card">

            <h3>Quick Actions</h3>

            <div class="actions">

                <div class="action">
                    <span>📅</span>
                    <h4>View Attendance</h4>
                </div>

                <div class="action"
                     onclick="openOD()">

                    <span>📨</span>
                    <h4>Apply for Leave</h4>

                </div>

                <div class="action">

                    <span>📊</span>
                    <h4>Check Requirement</h4>

                </div>

                <div class="action"
                     onclick="focusChat()">

                    <span>💬</span>
                    <h4>Chat with Advisor</h4>

                </div>

            </div>

        </div>


        <!-- ATTENDANCE CHART -->

        <div class="card chart-card">

            <h3>Attendance Trend</h3>

            <canvas id="attendanceChart"></canvas>

        </div>

    </div>


    <!-- LEAVE SUGGESTION -->

    <div class="suggestion">

        <div>

            <h3>💡 Leave Suggestion</h3>

            <p>
                You have 2 days of leave allowance.
                You can check your projected attendance
                before applying.
            </p>

        </div>

        <button class="btn"
                onclick="openOD()">

            Apply Leave

        </button>

    </div>

</main>


<!-- CHATBOT -->

<section class="chatbot" id="chatbot">

    <div class="chat-header">

        <h3>🤖 Attendance Advisor</h3>

        <p>
            Ask me anything about your attendance,
            leaves, or requirements!
        </p>

    </div>


    <div class="messages" id="messages">

        <div class="message bot">

            Hi Jaswanth! 👋

            <br><br>

            I'm your Attendance Advisor.

            <br><br>

            You can ask:
            <br>
            • What is my attendance?
            <br>
            • Can I take leave tomorrow?
            <br>
            • How much attendance do I need?

        </div>


        <div class="message user">

            What is my current attendance?

        </div>


        <div class="message bot">

            Your overall attendance is <b>78%</b>.

            <br><br>

            You have attended 39 out of 50
            working days.

            <br><br>

            ✓ You are currently on track.

        </div>

    </div>


    <div class="chat-input">

        <input
            id="chatInput"
            placeholder="Type your message..."
            onkeydown="if(event.key==='Enter') sendMessage()"
        >

        <button class="send"
                onclick="sendMessage()">

            ➤

        </button>

    </div>

</section>

</div>


<!-- OD MODAL -->

<div class="modal" id="odModal">

    <div class="modal-box">

        <span class="close"
              onclick="closeOD()">✕</span>

        <h2>📨 OD / Leave Simulator</h2>

        <div class="form-group">

            <label>Leave Type</label>

            <select id="leaveType">

                <option value="od">
                    On-Duty (OD)
                </option>

                <option value="medical">
                    Medical Leave
                </option>

                <option value="leave">
                    Normal Leave
                </option>

            </select>

        </div>


        <div class="form-group">

            <label>Number of Days</label>

            <input
                type="number"
                id="leaveDays"
                value="1"
                min="1"
                max="30"
            >

        </div>


        <button class="btn"
                onclick="calculateAttendance()">

            Calculate

        </button>


        <div class="result"
             id="result">

            Enter your leave days to calculate
            projected attendance.

        </div>

    </div>

</div>


<script>

/* Attendance Chart */

const ctx =
document.getElementById('attendanceChart');

new Chart(ctx, {

    type: 'line',

    data: {

        labels:
        ['Mon','Tue','Wed','Thu','Fri','Sat','Sun'],

        datasets: [{

            label: 'Attendance %',

            data:
            [74, 79, 73, 77, 74, 79, 78],

            borderWidth: 3,

            tension: 0.4,

            fill: false

        }]

    },

    options: {

        responsive: true,

        scales: {

            y: {

                min: 0,

                max: 100

            }

        }

    }

});


/* OD Modal */

function openOD() {

    document.getElementById("odModal")
        .style.display = "flex";

}


function closeOD() {

    document.getElementById("odModal")
        .style.display = "none";

}


/* Calculate projected attendance */

function calculateAttendance() {

    let days =
        parseInt(
            document.getElementById("leaveDays").value
        );

    let currentPresent = 39;

    let currentTotal = 50;

    /*
       OD and approved medical leave
       are treated as attended days
       in this prototype.
    */

    let type =
        document.getElementById("leaveType").value;

    let projected;

    if(type === "od" || type === "medical") {

        projected =
            ((currentPresent + days) /
            (currentTotal + days)) * 100;

    } else {

        projected =
            (currentPresent /
            (currentTotal + days)) * 100;

    }

    document.getElementById("result").innerHTML =

        "<b>Projected Attendance</b><br><br>" +

        "Current: 78%<br>" +

        "After " + days + " day(s): " +

        "<b>" + projected.toFixed(2) + "%</b><br><br>" +

        (projected >= 75
        ? "✓ Attendance remains at or above 75%."
        : "⚠ Attendance may fall below 75%.");

}


/* Chatbot */

function focusChat() {

    document.getElementById("chatInput").focus();

}


function sendMessage() {

    let input =
        document.getElementById("chatInput");

    let text =
        input.value.trim();

    if(text === "") return;


    let messages =
        document.getElementById("messages");


    let userMessage =
        document.createElement("div");

    userMessage.className =
        "message user";

    userMessage.innerText =
        text;

    messages.appendChild(userMessage);


    input.value = "";


    setTimeout(() => {

        let reply =
            document.createElement("div");

        reply.className =
            "message bot";


        let lower =
            text.toLowerCase();


        if(lower.includes("attendance")) {

            reply.innerHTML =
                "Your current overall attendance is <b>78%</b>. You have attended 39 out of 50 working days.";

        }

        else if(
            lower.includes("leave") ||
            lower.includes("od")
        ) {

            reply.innerHTML =
                "You can use the Leave Simulator to check how OD, medical leave, or normal leave may affect your attendance.";

        }

        else if(
            lower.includes("75")
        ) {

            reply.innerHTML =
                "Your current attendance is 78%, which is 3 percentage points above 75%.";

        }

        else {

            reply.innerHTML =
                "I can help you with attendance percentage, OD/leave calculations, and attendance requirements.";

        }


        messages.appendChild(reply);

        messages.scrollTop =
            messages.scrollHeight;

    }, 500);

}

</script>

</body>
</html>
