<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Dean of Students Portal Demo</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<link href="https://fonts.googleapis.com/css2?family=Poppins&display=swap" rel="stylesheet">
<style>
*{box-sizing:border-box;font-family:Poppins,sans-serif;margin:0;}
body{background:#f4f6f8;}
nav{background:#0b3c5d;color:white;padding:15px 25px;display:flex;justify-content:space-between;align-items:center;}
nav a{color:white;text-decoration:none;margin-left:15px;cursor:pointer;}
section{display:none;padding:40px 20px;}
.active{display:block;}
header{background:linear-gradient(to right,#0b3c5d,#328cc1);color:white;text-align:center;padding:40px 20px;}
.container{max-width:1100px;margin:auto;display:grid;grid-template-columns:repeat(auto-fit,minmax(250px,1fr));gap:25px;}
.card{background:white;padding:25px;border-radius:15px;box-shadow:0 5px 15px rgba(0,0,0,.1);text-align:center;transition:.3s;}
.card:hover{transform:translateY(-5px);}
.btn{display:inline-block;background:#328cc1;color:white;padding:8px 14px;border-radius:6px;text-decoration:none;margin:5px;border:none;cursor:pointer;}
.btn:hover{background:#1f6fa8;}
.center{display:flex;justify-content:center;align-items:center;height:auto;margin:30px 0;}
.login-box{background:white;padding:30px;width:400px;border-radius:10px;box-shadow:0 0 15px rgba(0,0,0,.1);}
.login-box input, .login-box select, .login-box textarea{width:100%;padding:10px;margin-top:12px;}
table{border-collapse:collapse;width:100%;margin-top:15px;font-size:14px;}
th, td{border:1px solid #333;padding:8px;text-align:left;}
footer{background:#111;color:#aaa;text-align:center;padding:20px;margin-top:40px;}
</style>
</head>
<body>

<!-- NAVBAR -->
<nav>
<strong>UNIVERSITY OF ELDORET - Dean of Students Portal</strong>
<div>
<a onclick="showHome()">Home</a>
<a onclick="showLogin()">Login</a>
<a onclick="logout()">Logout</a>
</div>
</nav>

<!-- HOME -->
<section id="home" class="active">
<header>
<h1>Welcome to the Dean of Students Demo Portal</h1>
<p>Login to access applications</p>
</header>
<div style="text-align:center;margin-top:30px;">
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
<p>Submit applications and track status</p>
</header>

<div class="center">
<div class="login-box">
<h3>Submit New Form</h3>

<input type="text" id="admNo" placeholder="Admission Number">
<input type="text" id="fullName" placeholder="Full Name">
<input type="text" id="contact" placeholder="Email or Phone Number">
<input type="text" id="year" placeholder="Year of Study (e.g Year 1, Year 2)">
<input type="text" id="formName" placeholder="Form Name">

<select id="department">
<option>Dean of Students</option>
<option>Academic Affairs</option>
<option>Hostel & Accommodation</option>
<option>Finance Office</option>
<option>Registrar</option>
<option>Student Welfare</option>
</select>

<textarea id="details" rows="4" placeholder="Describe Your Issue"></textarea>

<button class="btn" onclick="submitForm()">Submit</button>
</div>
</div>

<h3>Your Submissions</h3>
<table id="studentTable">
<tr>
<th>Admission No</th>
<th>Full Name</th>
<th>Contact</th>
<th>Year</th>
<th>Form</th>
<th>Department</th>
<th>Issue</th>
<th>Status</th>
</tr>
</table>

<h3>Dean Dashboard (Approver View)</h3>
<table id="deanTable">
<tr>
<th>Admission No</th>
<th>Full Name</th>
<th>Contact</th>
<th>Year</th>
<th>Form</th>
<th>Department</th>
<th>Issue</th>
<th>Status</th>
<th>Action</th>
</tr>
</table>

</section>

<footer>
© UNIVERSITY OF ELDORET | Dean of Students’ Office
</footer>

<script>
let loggedIn=false;
let studentName="";
let submissions=[];

function hideAll(){
["home","login","dashboard"].forEach(id=>{
document.getElementById(id).classList.remove("active");
});
}

function showHome(){hideAll();document.getElementById("home").classList.add("active");}
function showLogin(){hideAll();document.getElementById("login").classList.add("active");}
function showDashboard(){hideAll();document.getElementById("dashboard").classList.add("active");}

function login(){
let u=document.getElementById("user").value;
let p=document.getElementById("pass").value;

if(u==="uoe" && p==="uoe"){
loggedIn=true;
studentName=u;
document.getElementById("error").innerHTML="";
showDashboard();
}else{
document.getElementById("error").innerHTML="Invalid Login Credentials";
}
}

function logout(){
loggedIn=false;
showHome();
}

function submitForm(){

let admNo=document.getElementById("admNo").value;
let fullName=document.getElementById("fullName").value;
let contact=document.getElementById("contact").value;
let year=document.getElementById("year").value;
let formName=document.getElementById("formName").value;
let department=document.getElementById("department").value;
let details=document.getElementById("details").value;

if(!admNo || !fullName || !contact || !year || !formName || !details){
alert("Please fill all fields");
return;
}

let sub={
id:submissions.length+1,
student:studentName,
admNo:admNo,
fullName:fullName,
contact:contact,
year:year,
form:formName,
department:department,
details:details,
status:"Pending"
};

submissions.push(sub);
updateTables();

document.getElementById("admNo").value="";
document.getElementById("fullName").value="";
document.getElementById("contact").value="";
document.getElementById("year").value="";
document.getElementById("formName").value="";
document.getElementById("details").value="";
}

function approve(id){
let s=submissions.find(s=>s.id===id);
s.status="Approved";
updateTables();
}

function reject(id){
let s=submissions.find(s=>s.id===id);
s.status="Rejected";
updateTables();
}

function updateTables(){

let studentTable=document.getElementById("studentTable");
studentTable.innerHTML=`<tr>
<th>Admission No</th>
<th>Full Name</th>
<th>Contact</th>
<th>Year</th>
<th>Form</th>
<th>Department</th>
<th>Issue</th>
<th>Status</th>
</tr>`;

submissions.filter(s=>s.student===studentName).forEach(s=>{
let row=studentTable.insertRow();
row.insertCell(0).innerText=s.admNo;
row.insertCell(1).innerText=s.fullName;
row.insertCell(2).innerText=s.contact;
row.insertCell(3).innerText=s.year;
row.insertCell(4).innerText=s.form;
row.insertCell(5).innerText=s.department;
row.insertCell(6).innerText=s.details;
row.insertCell(7).innerText=s.status;
});

let deanTable=document.getElementById("deanTable");
deanTable.innerHTML=`<tr>
<th>Admission No</th>
<th>Full Name</th>
<th>Contact</th>
<th>Year</th>
<th>Form</th>
<th>Department</th>
<th>Issue</th>
<th>Status</th>
<th>Action</th>
</tr>`;

submissions.forEach(s=>{
let row=deanTable.insertRow();
row.insertCell(0).innerText=s.admNo;
row.insertCell(1).innerText=s.fullName;
row.insertCell(2).innerText=s.contact;
row.insertCell(3).innerText=s.year;
row.insertCell(4).innerText=s.form;
row.insertCell(5).innerText=s.department;
row.insertCell(6).innerText=s.details;
row.insertCell(7).innerText=s.status;

let actionCell=row.insertCell(8);

if(s.status==="Pending"){
let approveBtn=document.createElement("button");
approveBtn.innerText="Approve";
approveBtn.className="btn";
approveBtn.onclick=()=>approve(s.id);

let rejectBtn=document.createElement("button");
rejectBtn.innerText="Reject";
rejectBtn.className="btn";
rejectBtn.onclick=()=>reject(s.id);

actionCell.appendChild(approveBtn);
actionCell.appendChild(rejectBtn);
}
});
}
</script>

</body>
</html>
