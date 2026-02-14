<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Student Applications at Dean of Student's Office</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<link href="https://fonts.googleapis.com/css2?family=Poppins&display=swap" rel="stylesheet">

<style>
*{box-sizing:border-box;font-family:Poppins, sans-serif;margin:0;}
body{background:#f4f6f8;}
nav{background:#0b3c5d;color:white;padding:15px 25px;display:flex;justify-content:space-between;align-items:center;}
nav a{color:white;text-decoration:none;margin-left:15px;cursor:pointer;}
section{display:none;padding:40px 20px;}
.active{display:block;}
header{background:linear-gradient(to right,#0b3c5d,#328cc1);color:white;text-align:center;padding:70px 20px;}
.container{max-width:1100px;margin:auto;display:grid;grid-template-columns:repeat(auto-fit,minmax(250px,1fr));gap:25px;}
.card{background:white;padding:25px;border-radius:15px;box-shadow:0 5px 15px rgba(0,0,0,.1);text-align:center;transition:.3s;}
.card:hover{transform:translateY(-5px);}
.btn{display:inline-block;background:#328cc1;color:white;padding:12px 20px;border-radius:6px;text-decoration:none;margin-top:15px;border:none;cursor:pointer;}
.btn:hover{background:#1f6fa8;}
.center{display:flex;justify-content:center;align-items:center;height:80vh;}
.login-box{background:white;padding:40px;width:320px;border-radius:10px;box-shadow:0 0 15px rgba(0,0,0,.1);}
.login-box input, .login-box select, .login-box textarea{width:100%;padding:10px;margin-top:15px;}
table{border-collapse:collapse;width:100%;margin-top:20px;}
th, td{border:1px solid #333;padding:6px;text-align:left;}
textarea.commentBox{width:100%;height:50px;}
footer{background:#111;color:#aaa;text-align:center;padding:20px;margin-top:40px;}
</style>

<!-- Firebase SDKs -->
<script type="module">
import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-app.js";
import { getAuth, signInWithEmailAndPassword, signOut } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-auth.js";
import { getFirestore, collection, addDoc, getDocs, updateDoc, doc, query, where, orderBy, Timestamp } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-firestore.js";
import * as XLSX from "https://cdn.sheetjs.com/xlsx-latest/package/dist/xlsx.full.min.js";

// --- FIREBASE CONFIG ---
const firebaseConfig = {
  apiKey: "AIzaSyBZEjT6vbHYZf2aq4ZtaYcmJ37AbVXeclU",
  authDomain: "petercodingtests.firebaseapp.com",
  projectId: "petercodingtests",
  storageBucket: "petercodingtests.firebasestorage.app",
  messagingSenderId: "808823808882",
  appId: "1:808823808882:web:15c145a882086dea2fb3eb",
  measurementId: "G-X14XTMG5VS"
};

// Initialize Firebase
const app = initializeApp(firebaseConfig);
const auth = getAuth(app);
const db = getFirestore(app);

// --- GLOBALS ---
let currentUser = null;
let currentRole = null;

// --- PAGE CONTROL ---
function hideAll(){document.querySelectorAll("section").forEach(s=>s.classList.remove("active"));}
function showHome(){hideAll();home.classList.add("active");}
function showLogin(){hideAll();loginSection.classList.add("active");}
function showDashboard(){hideAll();dashboard.classList.add("active");}

// --- LOGIN ---
async function loginUser(){
  const email = document.getElementById("email").value;
  const password = document.getElementById("password").value;
  const role = document.getElementById("role").value;
  try{
    const userCredential = await signInWithEmailAndPassword(auth,email,password);
    currentUser = userCredential.user;
    currentRole = role;
    document.getElementById("welcome").innerText = role==="student"?"Welcome Student":"Dean Dashboard";
    studentSection.style.display = role==="student"?"block":"none";
    adminSection.style.display = role==="admin"?"block":"none";
    showDashboard();
    loadTables();
  }catch(e){
    document.getElementById("error").innerText = e.message;
  }
}

// --- LOGOUT ---
function logoutUser(){signOut(auth); showHome();}

// --- SUBMIT FORM ---
async function submitIssue(){
  let issue = issueSelect.value==="Other"?otherIssue.value:issueSelect.value;
  if(!admNo.value||!fullName.value||!issue){alert("Fill all fields");return;}
  await addDoc(collection(db,"submissions"),{
    admNo:admNo.value,
    fullName:fullName.value,
    contact:contact.value,
    year:year.value,
    department:department.value,
    issue:issue,
    status:"Pending",
    comment:"",
    createdAt:Timestamp.now(),
    studentEmail:currentUser.email
  });
  alert("Submitted successfully");
  loadTables();
}

// --- DECIDE (ADMIN) ---
async function decide(docId,decision,index){
  let comment = document.getElementById("comment_"+index).value;
  if(!comment.trim()){alert("Comment required"); return;}
  const submissionRef = doc(db,"submissions",docId);
  await updateDoc(submissionRef,{status:decision, comment:comment});
  loadTables();
}

// --- LOAD TABLES ---
async function loadTables(){
  studentTable.innerHTML="<tr><th>Admission</th><th>Name</th><th>Issue</th><th>Status</th><th>Admin Comment</th></tr>";
  const studentQuery = query(collection(db,"submissions"), where("studentEmail","==",currentUser.email), orderBy("createdAt","desc"));
  const snapshot = await getDocs(studentQuery);
  snapshot.forEach(docSnap=>{
    const s=docSnap.data();
    let row = studentTable.insertRow();
    row.insertCell(0).innerText=s.admNo;
    row.insertCell(1).innerText=s.fullName;
    row.insertCell(2).innerText=s.issue;
    row.insertCell(3).innerText=s.status;
    row.insertCell(4).innerText=s.comment||"-";
  });

  adminTable.innerHTML="<tr><th>Date</th><th>Admission</th><th>Name</th><th>Issue</th><th>Status</th><th>Decision & Comment</th></tr>";
  if(currentRole==="admin"){
    const today = new Date().toISOString().split("T")[0];
    const allSnap = await getDocs(collection(db,"submissions"));
    let index=0;
    allSnap.forEach(docSnap=>{
      const s=docSnap.data();
      const subDate=s.createdAt.toDate().toISOString().split("T")[0];
      if(subDate===today){
        let row = adminTable.insertRow();
        row.insertCell(0).innerText=subDate;
        row.insertCell(1).innerText=s.admNo;
        row.insertCell(2).innerText=s.fullName;
        row.insertCell(3).innerText=s.issue;
        row.insertCell(4).innerText=s.status;
        let cell=row.insertCell(5);
        if(s.status==="Pending"){
          cell.innerHTML=`<textarea class="commentBox" id="comment_${index}" placeholder="Decision Comment"></textarea>
          <button class="btn" onclick="decide('${docSnap.id}','Approved',${index})">Approve</button>
          <button class="btn" onclick="decide('${docSnap.id}','Rejected',${index})">Reject</button>`;
        }else{
          cell.innerHTML="<b>Comment:</b> "+s.comment;
        }
        index++;
      }
    });
  }
}

// --- EXPORT TODAY ---
async function exportToday(){
  const snapshot = await getDocs(collection(db,"submissions"));
  const today = new Date().toISOString().split("T")[0];
  let data=[];
  snapshot.forEach(docSnap=>{
    const s = docSnap.data();
    let subDate = s.createdAt.toDate().toISOString().split("T")[0];
    if(subDate===today){
      data.push({
        Date: subDate,
        Admission: s.admNo,
        Name: s.fullName,
        Issue: s.issue,
        Status: s.status,
        Comment: s.comment
      });
    }
  });
  if(data.length===0){alert("No submissions today"); return;}
  const ws=XLSX.utils.json_to_sheet(data);
  const wb=XLSX.utils.book_new();
  XLSX.utils.book_append_sheet(wb,ws,"Today_Report");
  XLSX.writeFile(wb,"Dean_End_of_Day_"+today+".xlsx");
}
</script>
</head>

<body>

<nav>
  <div class="nav-brand">
    <strong>UNIVERSITY OF ELDORET DEAN OF STUDENT'S PORTAL</strong>
  </div>
  <div>
    <a onclick="showHome()">Home</a>
    <a onclick="showLogin()">Login</a>
    <a onclick="logoutUser()">Logout</a>
  </div>
</nav>

<!-- HOME -->
<section id="home" class="active">
<header>
  <h1>Student Applications Portal</h1>
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
<h2>Login</h2>
<select id="role">
<option value="student">Student</option>
<option value="admin">Admin</option>
</select>
<input type="email" id="email" placeholder="Email">
<input type="password" id="password" placeholder="Password">
<button class="btn" onclick="loginUser()">Login</button>
<p id="error" style="color:red;"></p>
</div>
</div>
</section>

<!-- DASHBOARD -->
<section id="dashboard">
<h3 id="welcome"></h3>

<!-- STUDENT SECTION -->
<div id="studentSection" style="display:none">
<div class="center">
<div class="login-box">
<h3>Submit Application</h3>
<input type="text" id="admNo" placeholder="Admission Number">
<input type="text" id="fullName" placeholder="Full Name">
<input type="text" id="contact" placeholder="Email/Phone">
<input type="text" id="year" placeholder="Year of Study">
<select id="department">
<option>Dean of Students</option>
<option>Counselling</option>
<option>Deferral & Withdrawal</option>
<option>Bursary</option>
<option>Work-Study</option>
<option>Exam</option>
<option>Research</option>
<option>Other</option>
</select>
<select id="issueSelect" onchange="toggleOtherIssue()">
<option value="">Select Issue</option>
<option>Financial Hardship</option>
<option>Disciplinary Case</option>
<option>Accommodation Problem</option>
<option>Fee Clearance</option>
<option>Academic Appeal</option>
<option value="Other">Other</option>
</select>
<textarea id="otherIssue" placeholder="Describe Other Issue" style="display:none;"></textarea>
<button class="btn" onclick="submitIssue()">Submit</button>
</div>
</div>
<h4>Your Submissions</h4>
<table id="studentTable"></table>
</div>

<!-- ADMIN SECTION -->
<div id="adminSection" style="display:none">
<h3>All Submissions Today</h3>
<button class="btn" onclick="exportToday()">Export Excel</button>
<table id="adminTable"></table>
</div>

<footer>
© UNIVERSITY OF ELDORET | Dean of Students’ Office
</footer>

</body>
</html>
