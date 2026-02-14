

<html lang="en">
<head>
<meta charset="UTF-8">
<title>Student Applications at Dean of Student's Office</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<link href="https://fonts.googleapis.com/css2?family=Poppins&display=swap" rel="stylesheet">

<style>

/* =====================
   GLOBAL
===================== */

*{
box-sizing:border-box;
font-family:Poppins, sans-serif;
}

body{
margin:0;
background:#f4f6f8;
}

/* =====================
   NAVBAR
===================== */

nav{
background:#0b3c5d;
color:white;
padding:15px 25px;
display:flex;
justify-content:space-between;
align-items:center;
}

nav a{
color:white;
text-decoration:none;
margin-left:15px;
cursor:pointer;
}

/* =====================
   LOGO
===================== */

.nav-brand{
display:flex;
align-items:center;
gap:12px;
}

.logo{
height:45px;
width:auto;
}


/* =====================
   SECTIONS
===================== */

section{
display:none;
padding:40px 20px;
}

.active{
display:block;
}

/* =====================
   HERO
===================== */

header{
background:linear-gradient(to right,#0b3c5d,#328cc1);
color:white;
text-align:center;
padding:70px 20px;
}

/* =====================
   GRID
===================== */

.container{
max-width:1100px;
margin:auto;
display:grid;
grid-template-columns:repeat(auto-fit,minmax(250px,1fr));
gap:25px;
}

/* =====================
   CARD
===================== */

.card{
background:white;
padding:25px;
border-radius:15px;
box-shadow:0 5px 15px rgba(0,0,0,.1);
text-align:center;
transition:.3s;
}

.card:hover{
transform:translateY(-5px);
}

/* =====================
   BUTTON
===================== */

.btn{
display:inline-block;
background:#328cc1;
color:white;
padding:12px 20px;
border-radius:6px;
text-decoration:none;
margin-top:15px;
border:none;
cursor:pointer;
}

.btn:hover{
background:#1f6fa8;
}

/* =====================
   LOGIN
===================== */

.center{
display:flex;
justify-content:center;
align-items:center;
height:80vh;
}

.login-box{
background:white;
padding:40px;
width:320px;
border-radius:10px;
box-shadow:0 0 15px rgba(0,0,0,.1);
}

.login-box input{
width:100%;
padding:10px;
margin-top:15px;
}

/* =====================
   FOOTER
===================== */

footer{
background:#111;
color:#aaa;
text-align:center;
padding:20px;
margin-top:40px;
}

</style>
</head>

<body>

<!-- NAVBAR -->
<!-- NAVBAR -->
<nav>
  <div class="nav-brand">
    <img src="unnamed.png" alt="University of Eldoret Logo" class="logo">
    <strong>UNIVERSITY OF ELDORET DEAN OF STUDENT'S PORTAL</strong>
  </div>

  <div>
    <a onclick="showHome()">Home</a>
    <a onclick="showLogin()">Login</a>
    <a onclick="logout()">Logout</a>
  </div>
</nav>

<!-- HOME -->
<section id="home" class="active">
<header>
  <img src="unnamed.png" alt="University of Eldoret Logo" style="height:90px;margin-bottom:15px;">
  <h1>Student Applications Portal Dean Of Student's Office</h1>
  <p>Login to access applications</p>
</header>


<div style="text-align:center">
<button class="btn" onclick="showLogin()">Login to Continue</button>
</div>
</section>

<!-- LOGIN -->
<section id="login">
<div class="center">
<div class="login-box">
<h2>Student Login</h2>

<input type="text" id="user" placeholder="Student ADM NO.">
<input type="password" id="pass" placeholder="Password">

<button class="btn" onclick="login()">Login</button>

<p id="error" style="color:red;"></p>
</div>
</div>
</section>

<!-- DASHBOARD -->
<section id="dashboard">

<header>
<h1>Application Dashboard</h1>
<p>Select an application form</p>
</header>

<div class="container">

<!-- DEAN OF STUDENTS DEPARTMENT -->
<div class="card">
<h3>APPOINTMENT WITH DEAN OF STUDENT'S</h3>
<button class="btn btn-department" data-department="dean">Visit Dean's Department</button>
<div class="department-forms" id="dean-forms" style="display: none;">
  <div class="form-item">
    <p>Academic Appeal</p>
    <a class="btn btn-form" href="https://forms.gle/2BnvPARC8KKNNiie8" target="_blank">Open Form</a>
  </div>
  <div class="form-item">
    <p>Disciplinary Appeal</p>
    <a class="btn btn-form" href="https://forms.gle/2BnvPARC8KKNNiie8" target="_blank">Open Form</a>
  </div>
  <div class="form-item">
    <p>Student Grievance</p>
    <a class="btn btn-form" href="https://forms.gle/2BnvPARC8KKNNiie8" target="_blank">Open Form</a>
  </div>
  <div class="form-item">
    <p>Leave of Absence</p>
    <a class="btn btn-form" href="https://forms.gle/2BnvPARC8KKNNiie8" target="_blank">Open Form</a>
  </div>
  <div class="form-item">
    <p>Special Request</p>
    <a class="btn btn-form" href="https://forms.gle/2BnvPARC8KKNNiie8" target="_blank">Open Form</a>
  </div>
</div>
</div>

<!-- COUNSELLING DEPARTMENT -->
<div class="card">
<h3>Counselling Department</h3>
<button class="btn btn-department" data-department="counselling">Visit Counselling Department</button>
<div class="department-forms" id="counselling-forms" style="display: none;">
  <div class="form-item">
    <p>Mental Health Support</p>
    <a class="btn btn-form" href="https://forms.gle/3V3jqjwN2tgtki4m6" target="_blank">Open Form</a>
  </div>
  <div class="form-item">
    <p>Career Counselling</p>
    <a class="btn btn-form" href="https://forms.gle/3V3jqjwN2tgtki4m6" target="_blank">Open Form</a>
  </div>
  <div class="form-item">
    <p>Personal Development</p>
    <a class="btn btn-form" href="https://forms.gle/3V3jqjwN2tgtki4m6" target="_blank">Open Form</a>
  </div>
  <div class="form-item">
    <p>Academic Support</p>
    <a class="btn btn-form" href="https://forms.gle/3V3jqjwN2tgtki4m6" target="_blank">Open Form</a>
  </div>
  <div class="form-item">
    <p>Wellness Programs</p>
    <a class="btn btn-form" href="https://forms.gle/3V3jqjwN2tgtki4m6" target="_blank">Open Form</a>
  </div>
</div>
</div>

<!-- DEFERRAL AND WITHDRAWAL -->
<div class="card">
<h3>Deferral and Withdrawal from University</h3>
<button class="btn btn-department" data-department="deferral">Visit Deferral & Withdrawal Department</button>
<div class="department-forms" id="deferral-forms" style="display: none;">
  <div class="form-item">
    <p>Deferral Request</p>
    <a class="btn btn-form" href="https://forms.gle/eVfzWLFCxxkxAJkw7" target="_blank">Open Form</a>
  </div>
  <div class="form-item">
    <p>Semester Break</p>
    <a class="btn btn-form" href="https://forms.gle/eVfzWLFCxxkxAJkw7" target="_blank">Open Form</a>
  </div>
  <div class="form-item">
    <p>Withdrawal Request</p>
    <a class="btn btn-form" href="https://forms.gle/eVfzWLFCxxkxAJkw7" target="_blank">Open Form</a>
  </div>
  <div class="form-item">
    <p>Readmission Application</p>
    <a class="btn btn-form" href="https://forms.gle/eVfzWLFCxxkxAJkw7" target="_blank">Open Form</a>
  </div>
  <div class="form-item">
    <p>Documentation Request</p>
    <a class="btn btn-form" href="https://forms.gle/eVfzWLFCxxkxAJkw7" target="_blank">Open Form</a>
  </div>
</div>
</div>

<!-- BURSARY APPLICATION -->
<div class="card">
<h3>Bursary Application</h3>
<button class="btn btn-department" data-department="bursary">Visit Bursary Department</button>
<div class="department-forms" id="bursary-forms" style="display: none;">
  <div class="form-item">
    <p>Merit Bursary</p>
    <a class="btn btn-form" href="https://forms.gle/VQNL6YSK1nGjfjNR6" target="_blank">Open Form</a>
  </div>
  <div class="form-item">
    <p>Need-Based Bursary</p>
    <a class="btn btn-form" href="https://forms.gle/VQNL6YSK1nGjfjNR6" target="_blank">Open Form</a>
  </div>
  <div class="form-item">
    <p>Sports Bursary</p>
    <a class="btn btn-form" href="https://forms.gle/VQNL6YSK1nGjfjNR6" target="_blank">Open Form</a>
  </div>
  <div class="form-item">
    <p>Emergency Bursary</p>
    <a class="btn btn-form" href="https://forms.gle/VQNL6YSK1nGjfjNR6" target="_blank">Open Form</a>
  </div>
  <div class="form-item">
    <p>Appeal for Additional Support</p>
    <a class="btn btn-form" href="https://forms.gle/VQNL6YSK1nGjfjNR6" target="_blank">Open Form</a>
  </div>
</div>
</div>

<!-- WORK-STUDY PROGRAM -->
<div class="card">
<h3>Work-Study Program</h3>
<button class="btn btn-department" data-department="work-study">Visit Work-Study Department</button>
<div class="department-forms" id="work-study-forms" style="display: none;">
  <div class="form-item">
    <p>Program Application</p>
    <a class="btn btn-form" href="https://forms.gle/WZFE8HoBHUcJ3zoZ9" target="_blank">Open Form</a>
  </div>
  <div class="form-item">
    <p>Job Placement Request</p>
    <a class="btn btn-form" href="https://forms.gle/WZFE8HoBHUcJ3zoZ9" target="_blank">Open Form</a>
  </div>
  <div class="form-item">
    <p>Schedule Change</p>
    <a class="btn btn-form" href="https://forms.gle/WZFE8HoBHUcJ3zoZ9" target="_blank">Open Form</a>
  </div>
  <div class="form-item">
    <p>Performance Review</p>
    <a class="btn btn-form" href="https://forms.gle/WZFE8HoBHUcJ3zoZ9" target="_blank">Open Form</a>
  </div>
  <div class="form-item">
    <p>Internship Placement</p>
    <a class="btn btn-form" href="https://forms.gle/WZFE8HoBHUcJ3zoZ9" target="_blank">Open Form</a>
  </div>
</div>
</div>

<!-- EXAM CARDS -->
<div class="card">
<h3>Exam Cards</h3>
<button class="btn btn-department" data-department="exam">Visit Exam Department</button>
<div class="department-forms" id="exam-forms" style="display: none;">
  <div class="form-item">
    <p>Exam Card Request</p>
    <a class="btn btn-form" href="https://forms.gle/eVfzWLFCxxkxAJkw7" target="_blank">Open Form</a>
  </div>
  <div class="form-item">
    <p>Special Exam Arrangement</p>
    <a class="btn btn-form" href="https://forms.gle/eVfzWLFCxxkxAJkw7" target="_blank">Open Form</a>
  </div>
  <div class="form-item">
    <p>Exam Date Change Request</p>
    <a class="btn btn-form" href="https://forms.gle/eVfzWLFCxxkxAJkw7" target="_blank">Open Form</a>
  </div>
  <div class="form-item">
    <p>Exam Result Query</p>
    <a class="btn btn-form" href="https://forms.gle/eVfzWLFCxxkxAJkw7" target="_blank">Open Form</a>
  </div>
  <div class="form-item">
    <p>Supplementary Exam Application</p>
    <a class="btn btn-form" href="https://forms.gle/eVfzWLFCxxkxAJkw7" target="_blank">Open Form</a>
  </div>
</div>
</div>

<!-- RESEARCH GRANT -->
<div class="card">
<h3>Research Grant</h3>
<button class="btn btn-department" data-department="research">Visit Research Department</button>
<div class="department-forms" id="research-forms" style="display: none;">
  <div class="form-item">
    <p>Research Grant Application</p>
    <a class="btn btn-form" href="https://forms.gle/eVfzWLFCxxkxAJkw7" target="_blank">Open Form</a>
  </div>
  <div class="form-item">
    <p>Project Proposal</p>
    <a class="btn btn-form" href="https://forms.gle/eVfzWLFCxxkxAJkw7" target="_blank">Open Form</a>
  </div>
  <div class="form-item">
    <p>Budget Request</p>
    <a class="btn btn-form" href="https://forms.gle/eVfzWLFCxxkxAJkw7" target="_blank">Open Form</a>
  </div>
  <div class="form-item">
    <p>Progress Report</p>
    <a class="btn btn-form" href="https://forms.gle/eVfzWLFCxxkxAJkw7" target="_blank">Open Form</a>
  </div>
  <div class="form-item">
    <p>Final Report Submission</p>
    <a class="btn btn-form" href="https://forms.gle/eVfzWLFCxxkxAJkw7" target="_blank">Open Form</a>
  </div>
</div>
</div>

<!-- OTHER APPLICATIONS -->
<div class="card">
<h3>Other Applications</h3>
<button class="btn btn-department" data-department="other">Visit Other Applications</button>
<div class="department-forms" id="other-forms" style="display: none;">
  <div class="form-item">
    <p>Certificate Request</p>
    <a class="btn btn-form" href="https://forms.gle/eVfzWLFCxxkxAJkw7" target="_blank">Open Form</a>
  </div>
  <div class="form-item">
    <p>Transcript Request</p>
    <a class="btn btn-form" href="https://forms.gle/eVfzWLFCxxkxAJkw7" target="_blank">Open Form</a>
  </div>
  <div class="form-item">
    <p>General Inquiry</p>
    <a class="btn btn-form" href="https://forms.gle/eVfzWLFCxxkxAJkw7" target="_blank">Open Form</a>
  </div>
  <div class="form-item">
    <p>Alumni Registration</p>
    <a class="btn btn-form" href="https://forms.gle/eVfzWLFCxxkxAJkw7" target="_blank">Open Form</a>
  </div>
  <div class="form-item">
    <p>Special Permission Request</p>
    <a class="btn btn-form" href="https://forms.gle/eVfzWLFCxxkxAJkw7" target="_blank">Open Form</a>
  </div>
</div>
</div>

</div>
</section>

<!-- FOOTER -->
<footer>
© UNIVERSITY OF ELDORET ISO 9001:2015 CERTIFIED | Dean of Students’ Office
</footer>

<script>

/* =====================
   PAGE CONTROL
===================== */

function hideAll(){
["home","login","dashboard"].forEach(id=>{
document.getElementById(id).classList.remove("active");
});
}

function showHome(){
hideAll();
document.getElementById("home").classList.add("active");
}

function showLogin(){
hideAll();
document.getElementById("login").classList.add("active");
}

function showDashboard(){
hideAll();
document.getElementById("dashboard").classList.add("active");
}

/* =====================
   LOGIN LOGIC
===================== */

let loggedIn=false;

function login(){
let u=document.getElementById("user").value;
let p=document.getElementById("pass").value;

if(u==="PETERNYUTU" && p==="UOEINTERN"){
loggedIn=true;
document.getElementById("error").innerHTML="";
showDashboard();
}
else{
document.getElementById("error").innerHTML="Invalid Login Credentials";
}
}

function logout(){
loggedIn=false;
showHome();
}

</script>

</body>
</html>
