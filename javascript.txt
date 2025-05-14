document.getElementById("form-diario").addEventListener("submit", function (e) {
  e.preventDefault();
  const fecha = document.getElementById("fecha").value;
  const cuenta = document.getElementById("cuenta").value;
  const debe = parseFloat(document.getElementById("debe").value) || 0;
  const haber = parseFloat(document.getElementById("haber").value) || 0;

  const tablaDiario = document.getElementById("tabla-diario").getElementsByTagName("tbody")[0];
  const row = tablaDiario.insertRow();
  row.innerHTML = `
    <td>${fecha}</td>
    <td>${cuenta}</td>
    <td>${debe.toFixed(2)}</td>
    <td>${haber.toFixed(2)}</td>
  `;

  formDiario.reset();
  agregarAlMayor(cuenta, debe, haber);
  agregarABalanza(cuenta, debe, haber);
});

function agregarAlMayor(cuenta, debe, haber) {
  const tabla = document.getElementById("tabla-mayor").getElementsByTagName("tbody")[0];
  const row = tabla.insertRow();
  row.innerHTML = `<td>${cuenta}</td><td>${debe.toFixed(2)}</td><td>${haber.toFixed(2)}</td>`;
}

function agregarABalanza(cuenta, debe, haber) {
  const tabla = document.getElementById("tabla-balanza").getElementsByTagName("tbody")[0];
  const row = tabla.insertRow();
  row.innerHTML = `<td>${cuenta}</td><td>${debe.toFixed(2)}</td><td>${haber.toFixed(2)}</td>`;
}

// Calculadora científica
let calcInput = "";

function appendCalc(value) {
  calcInput += value;
  document.getElementById("calc-input").value = calcInput;
}

function clearCalc() {
  calcInput = "";
  document.getElementById("calc-input").value = "";
}

function calculate() {
  try {
    const result = eval(calcInput);
    document.getElementById("calc-input").value = result;
    calcInput = "" + result;
  } catch {
    document.getElementById("calc-input").value = "Error";
    calcInput = "";
  }
}
