<!DOCTYPE html>
<html lang="pt-br">
<head>
<meta charset="UTF-8">
<title>Follow Up CRM</title>

<style>

body{
font-family:Arial;
background:#f1f3f6;
padding:15px;
}

.card{

background:white;
padding:15px;
border-radius:10px;
box-shadow:0px 3px 10px rgba(0,0,0,0.15);
max-width:420px;
margin:auto;

}

h2{

text-align:center;
margin-top:0;

}

button{

width:100%;
margin-top:8px;
padding:12px;
border:none;
border-radius:8px;
font-weight:bold;
cursor:pointer;

}

.follow{background:#3498db;}
.neg{background:#f39c12;}
.conv{background:#27ae60;}
.lost{background:#e74c3c;}

textarea{

width:100%;
margin-top:12px;
padding:10px;
border-radius:8px;
border:1px solid #ccc;

}

.history{

margin-top:15px;
max-height:200px;
overflow:auto;
background:#fafafa;
padding:10px;
border-radius:8px;
font-size:13px;

}

.item{

border-bottom:1px solid #ddd;
padding:5px;

}

</style>

</head>

<body>

<div class="card">

<h2>Follow Up Atendimento</h2>

<button class="follow"
onclick="registrar('Follow Up Agendado')">
📞 Follow Up Agendado
</button>

<button class="neg"
onclick="registrar('Em Negociação')">
🤝 Em Negociação
</button>

<button class="conv"
onclick="registrar('Convertido')">
✅ Convertido
</button>

<button class="lost"
onclick="registrar('Lead Perdido')">
❌ Lead Perdido
</button>

<textarea id="obs"
placeholder="Observação do atendimento..."
rows="3"></textarea>

<div class="history" id="history">

Histórico vazio

</div>

</div>


<script>

const chave="historicoFollowUp";

function carregar(){

let dados=JSON.parse(localStorage.getItem(chave)) || [];

mostrar(dados);

}

function registrar(status){

let obs=document.getElementById("obs").value;

let agora=new Date();

let registro={

status:status,

obs:obs,

data:agora.toLocaleString()

};

let dados=JSON.parse(localStorage.getItem(chave)) || [];

dados.unshift(registro);

localStorage.setItem(chave,JSON.stringify(dados));

document.getElementById("obs").value="";

mostrar(dados);


/* ENVIO PARA API OU WEBHOOK

fetch("URL_DA_API",{

method:"POST",

headers:{

"Content-Type":"application/json"

},

body:JSON.stringify(registro)

})

*/

}

function mostrar(lista){

let div=document.getElementById("history");

if(lista.length==0){

div.innerHTML="Histórico vazio";

return;

}

div.innerHTML="";

lista.forEach(item=>{

div.innerHTML+=`

<div class="item">

<b>${item.status}</b><br>

${item.data}<br>

Obs: ${item.obs || "-"}

</div>

`;

});

}

carregar();

</script>

</body>
</html>
