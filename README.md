<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Bài tập nối cột</title>

<style>

body{
font-family:Arial, sans-serif;
text-align:center;
background:transparent;
margin:0;
padding:20px;
}

h2{
margin-bottom:25px;
}

.container{
max-width:900px;
margin:auto;
display:flex;
flex-wrap:wrap;
gap:30px;
justify-content:center;
}

.column{
flex:1 1 350px;
}

p{
font-weight:bold;
}

.box{
border:2px dashed #777;
border-radius:10px;
padding:10px;
margin:10px;
min-height:55px;
background:rgba(255,255,255,0.2);
transition:0.2s;
}

.box:hover{
border-color:#333;
}

.bank{
padding:10px;
}

.item{
border-radius:10px;
padding:10px;
margin:10px;
background:rgba(200,220,255,0.8);
cursor:grab;
transition:0.2s;
box-shadow:0 2px 5px rgba(0,0,0,0.15);
}

.item:hover{
transform:scale(1.05);
background:#dce7ff;
}

button{
margin-top:20px;
padding:10px 20px;
font-size:16px;
border:none;
border-radius:8px;
background:#4CAF50;
color:white;
cursor:pointer;
}

button:hover{
background:#3d9140;
}

.correct{
background:rgba(0,255,0,0.25);
}

.wrong{
background:rgba(255,0,0,0.25);
}

#score{
margin-top:15px;
font-size:18px;
font-weight:bold;
}

</style>
</head>

<body>

<h2>Nối cột A với cột B</h2>

<div class="container">

<div class="column">

<p>1. Phương pháp điện phân nóng chảy</p>
<div class="box" data-answer="D"></div>

<p>2. Phương pháp nhiệt luyện</p>
<div class="box" data-answer="E"></div>

<p>3. Phương pháp thủy luyện</p>
<div class="box" data-answer="A"></div>

<p>4. Tái chế kim loại</p>
<div class="box" data-answer="C"></div>

<p>5. Quặng kim loại</p>
<div class="box" data-answer="B"></div>

</div>

<div class="column bank" id="bank">

<div class="item" draggable="true" data-id="A">
A. Hòa tan kim loại rồi thu hồi
</div>

<div class="item" draggable="true" data-id="B">
B. Hợp chất tự nhiên chứa kim loại
</div>

<div class="item" draggable="true" data-id="C">
C. Thu hồi kim loại từ phế liệu
</div>

<div class="item" draggable="true" data-id="D">
D. Dùng dòng điện tách kim loại
</div>

<div class="item" draggable="true" data-id="E">
E. Dùng chất khử ở nhiệt độ cao
</div>

</div>

</div>

<button onclick="check()">Kiểm tra</button>

<div id="score"></div>

<script>

let items=document.querySelectorAll(".item")
let boxes=document.querySelectorAll(".box")
let bank=document.getElementById("bank")

items.forEach(item=>{
item.addEventListener("dragstart",e=>{
e.dataTransfer.setData("text",item.dataset.id)
})
})

boxes.forEach(box=>{

box.addEventListener("dragover",e=>e.preventDefault())

box.addEventListener("drop",e=>{
e.preventDefault()

let id=e.dataTransfer.getData("text")
let el=document.querySelector('[data-id="'+id+'"]')

if(box.children.length>0){
bank.appendChild(box.children[0])
}

box.appendChild(el)

})

})

bank.addEventListener("dragover",e=>e.preventDefault())

bank.addEventListener("drop",e=>{
e.preventDefault()

let id=e.dataTransfer.getData("text")
let el=document.querySelector('[data-id="'+id+'"]')

bank.appendChild(el)

})

function check(){

let score=0

boxes.forEach(box=>{

box.classList.remove("correct","wrong")

let item=box.querySelector(".item")

if(!item)return

if(item.dataset.id===box.dataset.answer){
box.classList.add("correct")
score++
}
else{
box.classList.add("wrong")
}

})

document.getElementById("score").innerHTML="Điểm: "+score+"/5"

}

</script>

</body>
</html>
