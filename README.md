
const courses=[
 {name:"Direito Constitucional",icon:"⚖",desc:"Constituição, direitos fundamentais e organização do Estado."},
 {name:"Direito Civil",icon:"§",desc:"Pessoas, obrigações, contratos, responsabilidade e família."},
 {name:"Direito Penal",icon:"◈",desc:"Princípios, crimes, penas e fundamentos da legislação penal."},
 {name:"Processo Civil",icon:"▤",desc:"Atos processuais, partes, recursos e procedimentos."},
 {name:"Direito Administrativo",icon:"◆",desc:"Administração pública, atos, agentes e serviços públicos."},
 {name:"Direito do Trabalho",icon:"✦",desc:"Relações trabalhistas, direitos e principais conceitos."},
 {name:"Direito Tributário",icon:"◇",desc:"Tributos, princípios e relações entre Estado e contribuinte."},
 {name:"Direitos Humanos",icon:"✧",desc:"Dignidade, liberdade, igualdade e proteção internacional."}
];
const materials=[
 {title:"Constitucional — Direitos Fundamentais",cat:"Direito Constitucional",desc:"Resumo introdutório com conceitos essenciais para revisão."},
 {title:"Civil — Teoria das Obrigações",cat:"Direito Civil",desc:"Material de apoio sobre obrigações, modalidades e efeitos."},
 {title:"Penal — Princípios do Direito Penal",cat:"Direito Penal",desc:"Guia rápido para entender os princípios fundamentais."},
 {title:"Processo Civil — Atos Processuais",cat:"Processo Civil",desc:"Mapa de conceitos para revisar atos e prazos processuais."},
 {title:"Administrativo — Atos Administrativos",cat:"Direito Administrativo",desc:"Resumo dos elementos, atributos e classificação."},
 {title:"Trabalho — Relação de Emprego",cat:"Direito do Trabalho",desc:"Conceitos básicos para iniciar seus estudos."},
 {title:"Tributário — Sistema Tributário",cat:"Direito Tributário",desc:"Introdução aos principais conceitos tributários."},
 {title:"Direitos Humanos — Dignidade",cat:"Direitos Humanos",desc:"Material de revisão sobre dignidade e direitos fundamentais."},
 {title:"Revisão Geral — 20 Questões",cat:"Direito Constitucional",desc:"Questões de revisão para testar seus conhecimentos."}
];

const courseGrid=document.querySelector("#courseGrid");
const materialGrid=document.querySelector("#materialGrid");
const filter=document.querySelector("#filter");
const search=document.querySelector("#search");
const empty=document.querySelector("#empty");
const modal=document.querySelector("#modal");
const modalContent=document.querySelector("#modalContent");

courses.forEach(c=>{
 courseGrid.innerHTML+=`<article class="course"><div class="icon">${c.icon}</div><h3>${c.name}</h3><p>${c.desc}</p></article>`;
});
[...new Set(materials.map(m=>m.cat))].forEach(c=>filter.innerHTML+=`<option>${c}</option>`);

function render(){
 const q=search.value.toLowerCase(), f=filter.value;
 const list=materials.filter(m=>(f==="all"||m.cat===f)&&(m.title.toLowerCase().includes(q)||m.cat.toLowerCase().includes(q)||m.desc.toLowerCase().includes(q)));
 materialGrid.innerHTML=list.map((m,i)=>`<article class="material"><span class="tag">${m.cat}</span><h3>${m.title}</h3><p>${m.desc}</p><button onclick="openMaterial(${materials.indexOf(m)})">Ver material</button></article>`).join("");
 empty.style.display=list.length?"none":"block";
}
function openMaterial(i){
 const m=materials[i];
 modalContent.innerHTML=`<span class="tag">${m.cat}</span><h2>${m.title}</h2><p>${m.desc}</p><p><strong>Área do aluno</strong><br>Este espaço está pronto para receber o PDF, vídeo ou material original da Sarah. Para disponibilizar arquivos reais, coloque os PDFs na pasta do projeto e altere o botão no código.</p><a class="download" href="#" onclick="event.preventDefault();alert('Adicione o arquivo PDF no projeto para ativar este download.')">Abrir material</a>`;
 modal.classList.add("open");modal.setAttribute("aria-hidden","false");
}
search.addEventListener("input",render);filter.addEventListener("change",render);
document.querySelector("#close").onclick=()=>{modal.classList.remove("open");modal.setAttribute("aria-hidden","true")};
modal.onclick=e=>{if(e.target===modal)document.querySelector("#close").click()};
document.querySelector(".menu").onclick=()=>{const nav=document.querySelector("nav");nav.style.display=nav.style.display==="flex"?"none":"flex";nav.style.position="absolute";nav.style.top="78px";nav.style.left="0";nav.style.right="0";nav.style.background="white";nav.style.padding="20px";nav.style.flexDirection="column"};
render();