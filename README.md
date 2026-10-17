
<!DOCTYPE html>
<html lang="pt">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>NEXORA AI | Tudo num só lugar</title>
<style>
*{box-sizing:border-box}
body{
 margin:0;background:#07111f;color:white;
 font-family:Arial,sans-serif
}
header{
 padding:22px;text-align:center;
 background:#101f35
}
h1{color:#35e0c0;margin:5px}
p{line-height:1.5;color:#c8d4e4}
main{max-width:850px;margin:auto;padding:18px}
.hero{text-align:center;padding:25px 5px}
.grid{
 display:grid;
 grid-template-columns:repeat(2,1fr);
 gap:12px
}
.card{
 background:#14243a;border:1px solid #28405a;
 border-radius:15px;padding:18px;
 cursor:pointer;color:white;text-align:left;
 font-size:16px
}
.card:hover{border-color:#35e0c0}
.card span{font-size:28px;display:block;margin-bottom:9px}
.panel{
 margin-top:22px;background:#14243a;
 padding:20px;border-radius:15px
}
textarea,input{
 width:100%;padding:13px;margin:8px 0;
 border:1px solid #38516b;border-radius:9px;
 background:#091827;color:white
}
button.action{
 background:#35e0c0;color:#07111f;
 border:0;border-radius:9px;padding:13px;
 font-weight:bold;cursor:pointer
}
#resposta{
 white-space:pre-wrap;line-height:1.6;
 margin-top:15px
}
small{color:#a7b7ca}
footer{text-align:center;padding:25px;color:#94a9c0}
</style>
</head>
<body>
<header>
<h1>NEXORA AI</h1>
<small>O teu universo inteligente</small>
</header>

<main>
<section class="hero">
<h2>Uma plataforma. Infinitas possibilidades.</h2>
<p>Aprende, organiza a tua vida, cuida de ti,
descobre serviços e desenvolve o teu futuro.</p>
</section>

<div class="grid">
<button class="card" onclick="abrir('Educação')">
<span>📚</span>Educação e estudos
</button>
<button class="card" onclick="abrir('Saúde')">
<span>🩺</span>Saúde física
</button>
<button class="card" onclick="abrir('Bem-estar')">
<span>🧠</span>Bem-estar mental
</button>
<button class="card" onclick="abrir('Fitness')">
<span>💪</span>Academia e exercícios
</button>
<button class="card" onclick="abrir('Negócios')">
<span>💼</span>Negócios e carreira
</button>
<button class="card" onclick="abrir('Serviços')">
<span>🛠️</span>Serviços e profissionais
</button>
<button class="card" onclick="abrir('Finanças')">
<span>💰</span>Finanças pessoais
</button>
<button class="card" onclick="abrir('Assistente')">
<span>🤖</span>Assistente NEXORA
</button>
</div>

<section class="panel">
<h2 id="titulo">Assistente NEXORA</h2>
<p id="descricao">
Escolhe uma área para começares.
</p>
<textarea id="pergunta" rows="4"
placeholder="Escreve aqui o que precisas..."></textarea>
<button class="action" onclick="responder()">
Continuar
</button>
<div id="resposta" aria-live="polite"></div>
</section>

<section class="panel">
<h2>Os meus objectivos</h2>
<input id="objectivo"
placeholder="Ex.: Estudar inglês 20 minutos por dia">
<button class="action" onclick="guardar()">
Adicionar objectivo
</button>
<div id="objectivos"></div>
</section>

<section class="panel">
<h2>NEXORA Premium</h2>
<p>Em breve: assistente com IA, planos
personalizados e ferramentas avançadas.</p>
<button class="action" onclick="interesse()">
Tenho interesse
</button>
<p id="premium"></p>
</section>
</main>

<footer>
NEXORA AI © 2026<br>
Tecnologia para uma vida melhor.
</footer>

<script>
let area="Assistente";

const descricoes={
"Educação":"Organiza os teus estudos e cria metas de aprendizagem.",
"Saúde":"Regista questões de saúde e prepara perguntas para profissionais.",
"Bem-estar":"Organiza hábitos de descanso e autocuidado.",
"Fitness":"Define objectivos de actividade física.",
"Negócios":"Planeia ideias e tarefas do teu negócio.",
"Serviços":"Descreve o serviço ou profissional que procuras.",
"Finanças":"Organiza metas financeiras pessoais.",
"Assistente":"Escreve uma ideia, dúvida ou objectivo."
};

function abrir(nome){
 area=nome;
 document.getElementById("titulo").textContent=nome;
 document.getElementById("descricao").textContent=
 descricoes[nome];
 document.getElementById("resposta").textContent="";
 document.getElementById("pergunta").focus();
}

function responder(){
 const pergunta=document.getElementById("pergunta").value.trim();
 const resposta=document.getElementById("resposta");
 if(!pergunta){
  resposta.textContent="Escreve primeiro o que precisas.";
  return;
 }
 const dados=JSON.parse(
  localStorage.getItem("nexoraPedidos")||"[]"
 );
 dados.push({
  area:area,
  pergunta:pergunta,
  data:new Date().toISOString()
 });
 localStorage.setItem("nexoraPedidos",JSON.stringify(dados));
 resposta.textContent=
 "Pedido registado na área "+area+
 ".\n\n"+pergunta+
 "\n\nA ligação ao motor de inteligência artificial"+
 " ainda está em desenvolvimento. Esta versão"+
 " guarda o pedido apenas neste dispositivo.";
}

function guardar(){
 const campo=document.getElementById("objectivo");
 const valor=campo.value.trim();
 if(!valor)return;
 const lista=JSON.parse(
  localStorage.getItem("nexoraMetas")||"[]"
 );
 lista.push(valor);
 localStorage.setItem("nexoraMetas",JSON.stringify(lista));
 campo.value="";
 mostrar();
}

function mostrar(){
 const lista=JSON.parse(
  localStorage.getItem("nexoraMetas")||"[]"
 );
 const div=document.getElementById("objectivos");
 div.replaceChildren();
 lista.forEach((meta,i)=>{
  const p=document.createElement("p");
  p.textContent=meta+" ";
  const botao=document.createElement("button");
  botao.textContent="Concluir";
  botao.onclick=()=>{
   lista.splice(i,1);
   localStorage.setItem("nexoraMetas",JSON.stringify(lista));
   mostrar();
  };
  p.appendChild(botao);
  div.appendChild(p);
 });
}

function interesse(){
 document.getElementById("premium").textContent=
 "Obrigado pelo interesse! As subscrições"+
 " ainda não estão disponíveis.";
}
mostrar();
</script>
</body>
</html>
