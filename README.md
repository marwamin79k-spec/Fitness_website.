<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Fitness & Health | Made by Marwa Amin</title>

<style>
/* ===== GLOBAL ===== */
body{
  font-family: "Poppins", sans-serif;
  background: linear-gradient(135deg, #d4f1f4, #bde0fe, #caffbf);
  margin: 0;
  padding: 0;
  animation: fadeIn 1.2s ease;
}

@keyframes fadeIn{
  from{opacity:0;}
  to{opacity:1;}
}

/* ===== CONTAINER ===== */
.container{
  max-width: 850px;
  margin: 40px auto;
  padding: 25px;
  background: rgba(255,255,255,0.4);
  backdrop-filter: blur(15px);
  border-radius: 15px;
  box-shadow: 0 0 25px rgba(0,0,0,0.1);
  animation: slideUp 0.9s ease;
}

@keyframes slideUp{
  from{transform: translateY(40px); opacity:0;}
  to{transform: translateY(0); opacity:1;}
}

/* ===== HEADINGS ===== */
h1{
  text-align:center;
  color:#0b5345;
  font-size: 40px;
  margin-bottom: 5px;
  text-shadow: 1px 1px 3px #00000020;
}

h2{
  color:#145a32;
  margin-top: 25px;
  text-shadow: 1px 1px 3px #0000001a;
}

label{
  font-weight: 600;
  color:#053f2b;
}

/* ===== INPUTS ===== */
input, select{
  width:100%;
  padding:12px;
  margin:10px 0 18px 0;
  border-radius:10px;
  border:none;
  background: rgba(255,255,255,0.9);
  box-shadow: 0 0 8px #00000015 inset;
  font-size: 16px;
}

/* ===== BUTTON ===== */
button{
  width:100%;
  padding:14px;
  background: linear-gradient(135deg, #2ecc71, #27ae60);
  border:none;
  font-size:17px;
  color:white;
  border-radius:10px;
  cursor:pointer;
  letter-spacing: 1px;
  transition: 0.3s;
  box-shadow: 0 4px 12px #0000002a;
}

button:hover{
  background: linear-gradient(135deg, #27ae60, #1e8449);
  transform: scale(1.03);
}

/* ===== RESULT BOX ===== */
.result-box{
  margin-top:20px;
  padding:15px;
  background: rgba(255,255,255,0.7);
  border-radius:12px;
  font-weight:bold;
  color:#145a32;
  box-shadow: 0 0 10px #00000020 inset;
  animation: fadeIn 1s;
}

/* ===== FOOTER ===== */
.footer{
  text-align:center;
  margin-top:40px;
  padding:18px;
  background: rgba(0,0,0,0.1);
  color:#0b3d2e;
  border-radius: 0 0 12px 12px;
  font-size: 18px;
  font-weight: 600;
  letter-spacing: 1px;
}

</style>

</head>
<body>

<div class="container">

<h1>Fitness & Health Guide</h1>
<h2 style="text-align:center; color:#0e6655;">Created by: <span style="color:#0b3d2e; font-weight:700;">🌿 Marwa Amin</span></h2>

<!-- SECTION 1 -->
<h2>BMI Calculator</h2>

<label>Weight (kg):</label>
<input type="number" id="weight" placeholder="Enter your weight">

<label>Height (cm):</label>
<input type="number" id="height" placeholder="Enter your height">

<button onclick="calculateBMI()">Calculate BMI</button>

<div id="bmiResult" class="result-box"></div>

<hr>

<!-- SECTION 2 -->
<h2>Daily Calorie Calculator</h2>

<label>Weight (kg):</label>
<input type="number" id="cWeight">

<label>Height (cm):</label>
<input type="number" id="cHeight">

<label>Age:</label>
<input type="number" id="age">

<label>Gender:</label>
<select id="gender">
  <option value="male">Male</option>
  <option value="female">Female</option>
</select>

<label>Activity Level:</label>
<select id="activity">
  <option value="1.2">Sedentary</option>
  <option value="1.375">Light Active</option>
  <option value="1.55">Moderate</option>
  <option value="1.725">Very Active</option>
</select>

<button onclick="calculateCalories()">Calculate Calories</button>

<div id="calorieResult" class="result-box"></div>

<hr>

<!-- SECTION 3 -->
<h2>Meal Plan Generator</h2>

<label>Your Daily Calories:</label>
<input type="number" id="userCalories">

<label>Your Goal:</label>
<select id="goal">
  <option value="loss">Weight Loss</option>
  <option value="gain">Weight Gain</option>
</select>

<button onclick="generateMealPlan()">Generate Meal Plan</button>

<div id="mealResult" class="result-box"></div>

</div>

<div class="footer">
💚 Made by <strong>Marwa Amin</strong> – Pakistan’s Most Helpful Fitness Guide Website
</div>

<!-- JAVASCRIPT -->
<script>

/* BMI */
function calculateBMI(){
  let w=document.getElementById("weight").value;
  let h=document.getElementById("height").value;

  if(!w || !h){ alert("Enter both fields!"); return; }

  let m=h/100;
  let bmi=(w/(m*m)).toFixed(2);
  let type="";

  if(bmi<18.5) type="Underweight";
  else if(bmi<25) type="Normal";
  else if(bmi<30) type="Overweight";
  else type="Obese";

  document.getElementById("bmiResult").innerHTML =
    `Your BMI: <strong>${bmi}</strong> (${type})`;
}

/* CALORIES */
function calculateCalories(){
  let w=document.getElementById("cWeight").value;
  let h=document.getElementById("cHeight").value;
  let age=document.getElementById("age").value;
  let gen=document.getElementById("gender").value;
  let act=document.getElementById("activity").value;

  if(!w||!h||!age){ alert("Complete the details!"); return; }

  let bmr;
  if(gen==="male")
    bmr=10*w + 6.25*h - 5*age + 5;
  else
    bmr=10*w + 6.25*h - 5*age - 161;

  let total=Math.round(bmr * act);

  document.getElementById("calorieResult").innerHTML =
    `Your Daily Calories: <strong>${total}</strong>`;
}

/* MEAL PLAN */
function generateMealPlan(){
  let c=document.getElementById("userCalories").value;
  let g=document.getElementById("goal").value;

  if(!c){ alert("Enter calories!"); return; }

  c=Number(c);
  let b="",l="",d="",s="";

  if(g==="loss"){
    if(c<=1800){
      b="Oats + berries";
      l="Chicken salad";
      d="Veggies + rice";
      s="Apple";
    } else {
      b="Eggs + toast";
      l="Fish + quinoa";
      d="Veggie pasta";
      s="Yogurt";
    }
  }

  else{
    if(c<=2500){
      b="Omelette + smoothie";
      l="Chicken + rice";
      d="Pasta + chicken";
      s="Nuts + PB sandwich";
    } else {
      b="Eggs + avocado + oatmeal";
      l="Steak + sweet potato";
      d="Chicken + quinoa";
      s="Smoothie + nuts";
    }
  }

  document.getElementById("mealResult").innerHTML = `
    <strong>${g==="loss"?"Weight Loss":"Weight Gain"} Meal Plan:</strong><br><br>
    Breakfast: ${b}<br>
    Lunch: ${l}<br>
    Dinner: ${d}<br>
    Snacks: ${s}
  `;
}

</script>

</body>
</html>
