const ramos = [
  // PRIMER AÑO
  { id: "biologia", nombre: "BASES BIOLÓGICAS Y ANTROPOLÓGICAS DE LA VIDA", requisitos: [] },
  { id: "intro_med", nombre: "INTRODUCCIÓN AL ESTUDIO DE LA MEDICINA", requisitos: [] },

  // SEGUNDO AÑO
  { id: "anatomia", nombre: "ANATOMÍA NORMAL", requisitos: ["biologia"] },
  { id: "heg", nombre: "HEG", requisitos: ["biologia"] },
  { id: "aps", nombre: "APS", requisitos: ["intro_med"] },
  { id: "rcp", nombre: "RCP", requisitos: ["intro_med"] },
  { id: "informatica1", nombre: "INFORMÁTICA MÉDICA I", requisitos: [] },
  { id: "ingles1", nombre: "INGLÉS MÉDICO I", requisitos: [] },

  // TERCER AÑO
  { id: "fisiologia", nombre: "FISIOLOGÍA", requisitos: ["anatomia", "heg"] },
  { id: "bioquimica", nombre: "BIOQUÍMICA. INMUNOLOGÍA", requisitos: ["heg"] },
  { id: "salud_mental1", nombre: "SALUD MENTAL I", requisitos: ["aps"] },
  { id: "informatica2", nombre: "INFORMÁTICA MÉDICA II", requisitos: ["informatica1"] },
  { id: "ingles2", nombre: "INGLÉS MÉDICO II", requisitos: ["ingles1"] },

  // CUARTO AÑO
  { id: "patologia", nombre: "PATOLOGÍA GENERAL Y ESPECIAL", requisitos: ["fisiologia", "bioquimica"] },
  { id: "microbiologia", nombre: "MICROBIOLOGÍA", requisitos: ["bioquimica"] },
  { id: "semiologia", nombre: "SEMIOLOGÍA GENERAL", requisitos: ["fisiologia"] },
  { id: "farmacologia", nombre: "FARMACOLOGÍA GENERAL", requisitos: ["bioquimica"] },
  { id: "informatica3", nombre: "INFORMÁTICA MÉDICA III", requisitos: ["informatica2"] },
  { id: "ingles3", nombre: "INGLÉS MÉDICO III", requisitos: ["ingles2"] },

  // QUINTO, SEXTO, SÉPTIMO AÑOS (simplificado sem requisitos para exemplo)
  { id: "medicina_interna1", nombre: "MEDICINA INTERNA I", requisitos: ["semiologia", "patologia"] },
  { id: "clinica_emerg", nombre: "CLÍNICA MÉDICA Y EMERGENTOLOGÍA", requisitos: ["medicina_interna1"] },
];

const malla = document.getElementById("malla");

function createRamo(ramo) {
  const div = document.createElement("div");
  div.className = "ramo locked";
  div.id = ramo.id;
  div.textContent = ramo.nombre;
  div.onclick = () => approveRamo(ramo.id);
  malla.appendChild(div);
}

function approveRamo(id) {
  const ramo = document.getElementById(id);
  if (ramo.classList.contains("locked")) return;

  ramo.classList.add("approved");
  ramo.classList.remove("locked");
  ramo.onclick = null;

  updateDisponibles();
}

function updateDisponibles() {
  ramos.forEach(r => {
    if (document.getElementById(r.id).classList.contains("approved")) return;

    const requisitosAprobados = r.requisitos.every(reqId =>
      document.getElementById(reqId).classList.contains("approved")
    );

    if (requisitosAprobados) {
      const ramoDiv = document.getElementById(r.id);
      ramoDiv.classList.remove("locked");
    }
  });
}

// Inicializa toda a malha
ramos.forEach(createRamo);
updateDisponibles();
script.js
