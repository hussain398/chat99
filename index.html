
<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<title>المقسّم الذكي المتكامل</title>

<style>
body{
    margin:0;
    font-family: Arial;
    background: linear-gradient(135deg,#1e3c72,#2a5298);
    display:flex;
    justify-content:center;
    align-items:center;
    min-height:100vh;
}

.app{
    width:420px;
    background:white;
    border-radius:20px;
    padding:20px;
    box-shadow:0 10px 30px rgba(0,0,0,0.3);
}

h2{
    text-align:center;
    color:#2a5298;
}

label{
    font-size:14px;
    font-weight:bold;
}

input,select{
    width:100%;
    padding:10px;
    margin:8px 0 12px 0;
    border-radius:10px;
    border:1px solid #ccc;
}

.section{
    background:#f4f6f8;
    padding:10px;
    border-radius:10px;
    margin-bottom:15px;
}

button{
    width:100%;
    padding:12px;
    background:#2a5298;
    color:white;
    border:none;
    border-radius:12px;
    font-size:16px;
    cursor:pointer;
}

.result{
    margin-top:15px;
    background:#f9fafc;
    padding:12px;
    border-radius:12px;
    font-size:14px;
    line-height:1.6;
}
</style>
</head>

<body>

<div class="app">

<h2>💰 المقسّم الذكي الكامل</h2>

<label>المبلغ</label>
<input type="number" id="money" value="0">

<label>نوع الدخل</label>
<select id="type">
<option value="daily">يومي</option>
<option value="monthly">شهري</option>
<option value="yearly">سنوي</option>
</select>

<h3>🛒 تقسيم المصروف (نسب)</h3>
<div class="section">
<label>🍔 الأكل (% من المال)</label>
<input type="number" id="foodPercent" value="50">

<label>🥤 الشرب (% من المال)</label>
<input type="number" id="drinkPercent" value="30">

<label>💰 الادخار (% من المال)</label>
<input type="number" id="savePercent" value="20">
</div>

<h3>🍳 وجبات مجانية</h3>
<div class="section">
<label><input type="checkbox" id="breakfast"> فطور مجاني</label><br>
<label><input type="checkbox" id="lunch"> غداء مجاني</label><br>
<label><input type="checkbox" id="dinner"> عشاء مجاني</label>
</div>

<h3>📅 أيام الصرف</h3>
<div class="section">
<label><input type="checkbox" class="day"> السبت</label><br>
<label><input type="checkbox" class="day"> الأحد</label><br>
<label><input type="checkbox" class="day"> الاثنين</label><br>
<label><input type="checkbox" class="day"> الثلاثاء</label><br>
<label><input type="checkbox" class="day"> الأربعاء</label><br>
<label><input type="checkbox" class="day"> الخميس</label><br>
<label><input type="checkbox" class="day"> الجمعة</label>
</div>

<button onclick="calc()">احسب</button>

<div class="result" id="result">📊 النتيجة ستظهر هنا</div>

</div>

<script>
function calc(){

let money = parseFloat(document.getElementById("money").value);
let type = document.getElementById("type").value;

// تحويل إلى يومي
if(type==="monthly") money/=30;
if(type==="yearly") money/=365;

// النسب
let foodP = parseFloat(document.getElementById("foodPercent").value)/100;
let drinkP = parseFloat(document.getElementById("drinkPercent").value)/100;
let saveP = parseFloat(document.getElementById("savePercent").value)/100;

// الوجبات المجانية
let free=0;
if(document.getElementById("breakfast").checked) free++;
if(document.getElementById("lunch").checked) free++;
if(document.getElementById("dinner").checked) free++;

// تعديل بسيط حسب الوجبات المجانية
saveP += free*0.05;
foodP -= free*0.05;

if(foodP < 0.2) foodP = 0.2;

// أيام الصرف
let days = document.querySelectorAll(".day:checked").length;
if(days === 0){
document.getElementById("result").innerHTML="⚠️ اختر أيام الصرف";
return;
}

// الحساب
let food = money * foodP;
let drink = money * drinkP;
let save = money * saveP;

// الأيام بدون صرف = ادخار إضافي
let extraSave = (7 - days) * money;
save += extraSave;

// التوقعات
let month = save * 30;
let year = save * 365;

// العرض
document.getElementById("result").innerHTML =
"📊 الدخل اليومي: " + money.toFixed(2) + "<br><br>" +
"🍔 الأكل: " + food.toFixed(2) + "<br>" +
"🥤 الشرب: " + drink.toFixed(2) + "<br>" +
"💰 الادخار: " + save.toFixed(2) + "<br><br>" +
"📈 التوقع:<br>" +
"📅 بعد شهر: " + month.toFixed(2) + "<br>" +
"📆 بعد سنة: " + year.toFixed(2);

}
</script>

</body>
</html>
