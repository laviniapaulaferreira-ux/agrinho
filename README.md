<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculadora de Adubação Rural</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>

    <div class="container">
        <h1>🌱 Calculadora de Adubação Rural</h1>

        <div class="card">
            <label for="cultura">Cultura:</label>
            <select id="cultura">
                <option value="Soja">Soja</option>
                <option value="Milho">Milho</option>
                <option value="Trigo">Trigo</option>
                <option value="Feijão">Feijão</option>
            </select>

            <label for="area">Área Plantada (ha):</label>
            <input type="number" id="area" placeholder="Ex: 50">

            <label for="adubo">Recomendação de Adubo (kg/ha):</label>
            <input type="number" id="adubo" placeholder="Ex: 350">

            <label for="preco">Preço do Adubo (R$/kg):</label>
            <input type="number" id="preco" step="0.01" placeholder="Ex: 2.80">

            <button onclick="calcularAdubo()">
                Calcular
            </button>

            <div id="resultado"></div>
        </div>
    </div>

    <script src="script.js"></script>

</body>
</html>
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
    font-family: Arial, Helvetica, sans-serif;
}

body{
    background: linear-gradient(135deg, #4CAF50, #2E7D32);
    min-height:100vh;
    display:flex;
    justify-content:center;
    align-items:center;
    padding:20px;
}

.container{
    width:100%;
    max-width:600px;
}

h1{
    text-align:center;
    color:white;
    margin-bottom:20px;
}

.card{
    background:white;
    padding:25px;
    border-radius:15px;
    box-shadow:0 4px 15px rgba(0,0,0,0.2);
}

label{
    display:block;
    margin-top:12px;
    margin-bottom:5px;
    font-weight:bold;
}

input, select{
    width:100%;
    padding:12px;
    border:1px solid #ccc;
    border-radius:8px;
    font-size:16px;
}

button{
    width:100%;
    margin-top:20px;
    padding:14px;
    border:none;
    border-radius:8px;
    background:#4CAF50;
    color:white;
    font-size:18px;
    cursor:pointer;
    transition:0.3s;
}

button:hover{
    background:#388E3C;
}

#resultado{
    margin-top:20px;
    padding:15px;
    background:#f5f5f5;
    border-radius:10px;
    font-size:17px;
    line-height:1.8;
}

@media(max-width:600px){

    h1{
        font-size:24px;
    }

    .card{
        padding:20px;
    }

    input,
    select,
    button{
        font-size:15px;
    }
}
function calcularAdubo() {

    const cultura = document.getElementById("cultura").value;
    const area = parseFloat(document.getElementById("area").value);
    const adubo = parseFloat(document.getElementById("adubo").value);
    const preco = parseFloat(document.getElementById("preco").value);

    const resultado = document.getElementById("resultado");

    if (isNaN(area) || isNaN(adubo) || area <= 0 || adubo <= 0) {
        resultado.innerHTML =
            "<span style='color:red'>Preencha os campos corretamente.</span>";
        return;
    }

    const quantidadeTotal = area * adubo;

    let html = `
        <h3>Resultado da Simulação</h3>
        <p><strong>Cultura:</strong> ${cultura}</p>
        <p><strong>Área:</strong> ${area} ha</p>
        <p><strong>Dose recomendada:</strong> ${adubo} kg/ha</p>
        <p><strong>Quantidade total necessária:</strong> ${quantidadeTotal.toLocaleString('pt-BR')} kg</p>
        <p><strong>Total em toneladas:</strong> ${(quantidadeTotal / 1000).toFixed(2)} t</p>
    `;

    if (!isNaN(preco) && preco > 0) {
        const custoTotal = quantidadeTotal * preco;

        html += `
            <p><strong>Preço por kg:</strong> R$ ${preco.toFixed(2)}</p>
            <p><strong>Custo estimado:</strong> R$ ${custoTotal.toLocaleString('pt-BR', {
                minimumFractionDigits: 2,
                maximumFractionDigits: 2
            })}</p>
        `;
    }

    resultado.innerHTML = html;
}
