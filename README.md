!DOCTYPE html>  
<html lang="ar" dir="rtl">  
<head>  
  <meta charset="UTF-8" />  
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>  
  <title>احسب معدلك</title>  
  
  <style>  
    *{  
      margin:0;  
      padding:0;  
      box-sizing:border-box;  
      font-family:Arial, sans-serif;  
    }  
  
    body{  
      background:#f3f4f6;  
      padding:20px;  
    }  
  
    .container{  
      max-width:900px;  
      margin:auto;  
      background:white;  
      padding:25px;  
      border-radius:15px;  
      box-shadow:0 0 15px rgba(0,0,0,0.1);  
    }  
  
    h1{  
      text-align:center;  
      margin-bottom:25px;  
      color:#2563eb;  
    }  
  
    table{  
      width:100%;  
      border-collapse:collapse;  
    }  
  
    th, td{  
      border:1px solid #ddd;  
      padding:10px;  
      text-align:center;  
    }  
  
    th{  
      background:#2563eb;  
      color:white;  
    }  
  
    input{  
      width:100%;  
      padding:8px;  
      text-align:center;  
      border:1px solid #ccc;  
      border-radius:6px;  
    }  
  
    button{  
      margin-top:20px;  
      width:100%;  
      padding:15px;  
      border:none;  
      border-radius:10px;  
      background:#2563eb;  
      color:white;  
      font-size:18px;  
      cursor:pointer;  
      transition:0.3s;  
    }  
  
    button:hover{  
      background:#1d4ed8;  
    }  
  
    .result{  
      margin-top:25px;  
      text-align:center;  
      font-size:24px;  
      font-weight:bold;  
      color:#111827;  
    }  
  
    .success{  
      color:green;  
    }  
  
    .fail{  
      color:red;  
    }  
  
    @media(max-width:700px){  
      table{  
        font-size:12px;  
      }  
  
      input{  
        padding:5px;  
      }  
    }  
  </style>  
</head>  
<body>  
  
<div class="container">  
  <h1>احسب معدلك</h1>  
  
  <table>  
    <thead>  
      <tr>  
        <th>المادة</th>  
        <th>المعامل</th>  
        <th>علامة الاختبار</th>  
        <th>علامة الفرض</th>  
        <th>معدل المادة</th>  
      </tr>  
    </thead>  
  
    <tbody id="subjectsTable"></tbody>  
  </table>  
  
  <button onclick="calculateAverage()">  
    احسب المعدل  
  </button>  
  
  <div class="result" id="result"></div>  
</div>  
  
<script>  
  
const subjects = [  
  {name:"اقتصاد جزئي 2", coef:2},  
  {name:"محاسبة التسيير", coef:2},  
  {name:"فرنسية", coef:1},  
  {name:"تحليل رياضي", coef:3},  
  {name:"ذكاء اصطناعي", coef:2},  
  {name:"احتمالات", coef:3},  
  {name:"انجليزية", coef:1},  
  {name:"جبر خطي", coef:3},  
  {name:"جغرافيا", coef:1},  
];  
  
const table = document.getElementById("subjectsTable");  
  
subjects.forEach((subject, index) => {  
  
  table.innerHTML += `  
    <tr>  
      <td>${subject.name}</td>  
      <td>${subject.coef}</td>  
  
      <td>  
        <input type="number" step="0.01" min="0" max="20"  
        id="exam-${index}">  
      </td>  
  
      <td>  
        <input type="number" step="0.01" min="0" max="20"  
        id="td-${index}">  
      </td>  
  
      <td id="module-${index}">  
        0  
      </td>  
    </tr>  
  `;  
});  
  
function calculateAverage(){  
  
  let total = 0;  
  let totalCoef = 0;  
  
  subjects.forEach((subject, index) => {  
  
    const exam =  
      parseFloat(document.getElementById(`exam-${index}`).value) || 0;  
  
    const td =  
      parseFloat(document.getElementById(`td-${index}`).value) || 0;  
  
    // حساب معدل المادة  
    const moduleAverage =  
      (exam * 0.6) + (td * 0.4);  
  
    document.getElementById(`module-${index}`).innerText =  
      moduleAverage.toFixed(2);  
  
    total += moduleAverage * subject.coef;  
  
    totalCoef += subject.coef;  
  });  
  
  const finalAverage = total / totalCoef;  
  
  const result = document.getElementById("result");  
  
  result.innerHTML =  
    `المعدل العام للسداسي الثاني : ${finalAverage.toFixed(2)}`;  
  
  if(finalAverage >= 10){  
    result.className = "result success";  
    result.innerHTML += "<br>✅ ناجح";  
  }  
  else{  
    result.className = "result fail";  
    result.innerHTML += "<br>❌ راسب";  
  }  
}  
  
</script>  
  
</body>  
</html>  
