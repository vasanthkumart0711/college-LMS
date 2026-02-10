<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>College LMS</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
body{margin:0;font-family:Arial;background:#f2f2f2}


.header{
  background:#004080;
  color:#fff;
  padding:12px;
  text-align:center
}


.login{
  width:300px;
  margin:80px auto;
  background:#fff;
  padding:20px;
  border:1px solid #ccc
}
.login input{
  width:100%;
  padding:8px;
  margin-bottom:10px
}


.sidebar{
  width:200px;
  background:#333;
  color:#fff;
  min-height:100vh;
  float:left;
  padding:10px;
  display:none
}
.sidebar a{
  display:block;
  padding:10px;
  color:#fff;
  text-decoration:none;
  margin-bottom:5px;
  cursor:pointer
}
.sidebar a.active{background:#555}


.main{
  margin-left:200px;
  padding:20px;
  display:none
}
.section{display:none}
.section.active{display:block}

.box{
  background:#fff;
  padding:15px;
  margin-bottom:10px;
  border:1px solid #ccc
}

button{padding:6px 12px}

.alert{
  background:#d4edda;
  padding:10px;
  margin-bottom:10px;
  display:none
}
</style>
</head>
<body>


<div class="header">
  <h2>LMS College of Engineering</h2>
  <p>Learning Management System</p>
</div>


<div class="login" id="loginPage">
  <h3>Login</h3>
  <input type="text" id="username" placeholder="Username">
  <input type="password" id="password" placeholder="Password">
  <button onclick="login()">Login</button>
  <p id="loginError" style="color:red"></p>
</div>

<!-- Sidebar -->
<div class="sidebar" id="sidebar">
  <a class="nav active" data-page="dashboard">Dashboard</a>
  <a class="nav" data-page="courses">Courses</a>
  <a class="nav" data-page="assignments">Assignments</a>
  <a class="nav" data-page="profile">Profile</a>
</div>

<!-- Main -->
<div class="main" id="mainContent">

<div class="alert" id="alertBox"></div>

<!-- Dashboard -->
<div id="dashboard" class="section active">
  <h2>Dashboard</h2>
  <div class="box">Total Courses: 3</div>
  <div class="box">Assignments Pending: 2</div>
  <div class="box">Attendance: 90%</div>
  <div class="box">GPA: 8.2</div>
</div>

<!-- Courses -->
<div id="courses" class="section">
  <h2>Courses</h2>
  <div class="box">Web Development – Active</div>
  <div class="box">Java Programming – Active</div>
  <div class="box">Digital Electronics – Completed</div>
</div>

<!-- Assignments -->
<div id="assignments" class="section">
  <h2>Assignments</h2>

  <div class="box">
    HTML Assignment<br>
    Due Date: 15-02-2026<br>
    Result Time: 20-02-2026<br>
    Status: <span id="s1">Pending</span><br><br>
    <button onclick="submitAssignment('s1',this)">Submit</button>
  </div>

  <div class="box">
    JavaScript Assignment<br>
    Due Date: 18-02-2026<br>
    Result Time: 25-02-2026<br>
    Status: <span id="s2">Pending</span><br><br>
    <button onclick="submitAssignment('s2',this)">Submit</button>
  </div>
</div>

<!-- Profile -->
<div id="profile" class="section">
  <h2>Profile</h2>
  Name:<br>
  <input id="name" value="Vasanth Kumar" disabled><br><br>
  Department:<br>
  <input id="dept" value="Computer Science" disabled><br><br>
  <button onclick="editProfile()">Edit / Save</button>
</div>

</div>

<script>
/* Login */
function login(){
  const u=document.getElementById("username").value
  const p=document.getElementById("password").value

  if(u==="" || p===""){
    document.getElementById("loginError").innerText="Enter username and password"
  }else{
    document.getElementById("loginPage").style.display="none"
    document.getElementById("sidebar").style.display="block"
    document.getElementById("mainContent").style.display="block"
  }
}

/* Navigation */
document.querySelectorAll(".nav").forEach(link=>{
  link.onclick=()=>{
    document.querySelectorAll(".nav").forEach(n=>n.classList.remove("active"))
    link.classList.add("active")

    document.querySelectorAll(".section").forEach(s=>s.classList.remove("active"))
    document.getElementById(link.dataset.page).classList.add("active")
  }
})

/* Assignment Submit */
function submitAssignment(id,btn){
  document.getElementById(id).innerText="Submitted"
  btn.disabled=true
  showAlert("Assignment submitted")
}

/* Profile Edit */
let edit=false
function editProfile(){
  edit=!edit
  document.getElementById("name").disabled=!edit
  document.getElementById("dept").disabled=!edit
  if(!edit) showAlert("Profile updated")
}

/* Alert */
function showAlert(msg){
  const a=document.getElementById("alertBox")
  a.innerText=msg
  a.style.display="block"
  setTimeout(()=>a.style.display="none",2000)
}
</script>

</body>
</html>
