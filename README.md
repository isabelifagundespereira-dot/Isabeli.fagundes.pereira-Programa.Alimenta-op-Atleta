<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Controle de Alimentação do Atleta</title>
  <style>
    :root {
      --bg-color: #121212;
      --card-bg: #1e1e1e;
      --text-color: #e0e0e0;
      --primary-color: #00e676;
      --secondary-color: #333333;
      --danger-color: #ff5252;
      --border-color: #333;
    }

    body {
      font-family: Arial, sans-serif;
      background-color: var(--bg-color);
      color: var(--text-color);
      margin: 0;
      padding: 20px;
    }

    header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 20px;
    }

    .card {
      background-color: var(--card-bg);
      border-radius: 8px;
      padding: 20px;
      margin-bottom: 20px;
      border: 1px solid var(--border-color);
    }

    .dashboard {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
      gap: 15px;
      margin-bottom: 20px;
    }

    .indicador {
      background-color: var(--card-bg);
      padding: 15px;
      border-radius: 8px;
      text-align: center;
      border: 1px solid var(--border-color);
    }

    .indicador span {
      font-size: 1.5rem;
      display: block;
    }

    .indicador strong {
      font-size: 1.2rem;
      display: block;
      margin-top: 5px;
    }

    .grid-perfil, .form-grid, .rotina-grid, .filtros {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      gap: 15px;
    }

    .campo {
      display: flex;
      flex-direction: column;
    }

    .campo.grande {
      grid-column: span 2;
    }

    label {
      margin-bottom: 5px;
      font-size: 0.9rem;
    }

    input, select, textarea {
      padding: 10px;
      background-color: #2b2b2b;
      border: 1px solid var(--border-color);
      color: #fff;
      border-radius: 4px;
    }

    textarea {
      resize: vertical;
      min-height: 60px;
    }

    .botoes, .agua-acoes, .acoes {
      margin-top: 15px;
      display: flex;
      gap: 10px;
    }

    .btn {
      padding: 10px 15px;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      font-weight: bold;
    }

    .btn-primary { background-color: var(--primary-color); color: #000; }
    .btn-secondary { background-color: var(--secondary-color); color: #fff; }
    .btn-danger { background-color: var(--danger-color); color: #fff; }
    .btn-agua { background-color: #0022ff; color: #fff; }

    .tabela-container {
      overflow-x: auto;
      margin-top: 15px;
    }

    table {
      width: 100%;
      border-collapse: collapse;
      text-align: left;
    }

    th, td {
      padding: 12px;
      border-bottom: 1px solid var(--border-color);
    }

    th {
      background-color: #252525;
    }

    .sem-registros {
      text-align: center;
      padding: 20px;
      color: #888;
    }

    @media (max-width: 600px) {
      .campo.grande {
        grid-column: span 1;
      }
    }
  </style>
</head>
<body>

  <header>
    <h1>🏃 AtletaControl</h1>
    <span>Tema escuro</span>
  </header>

  <!-- PERFIL DO ATLETA -->
  <section class="card">
    <div class="titulo">
      <h2>👤 Perfil do atleta</h2>
    </div>
    <p>Informações para organização dos registros.</p>
    <div class="grid-perfil">
      <div class="campo">
        <label for="atletaNome">Nome</label>
        <input type="text" id="atletaNome" placeholder="Nome do atleta">
      </div>
      <div class="campo">
        <label for="modalidade">Modalidade</label>
        <input type="text" id="modalidade" placeholder="Ex.: Futebol">
      </div>
      <div class="campo">
        <label for="equipe">Equipe / Clube</label>
        <input type="text" id="equipe" placeholder="Nome da equipe">
      </div>
      <div class="campo">
        <label for="dataRegistro">Data</label>
        <input type="date" id="dataRegistro">
      </div>
    </div>
  </section>

  <!-- RESUMO / DASHBOARD -->
  <section class="dashboard">
    <div class="indicador">
      <span>🥤</span>
      <small>Refeições registradas</small>
      <strong id="totalRefeicoes">0</strong>
    </div>
    <div class="indicador agua">
      <span>💧</span>
      <small>Água registrada</small>
      <strong id="aguaTotal">0 L</strong>
    </div>
    <div class="indicador sono">
      <span>🌙</span>
      <small>Sono</small>
      <strong id="sonoTotal">-</strong>
    </div>
    <div class="indicador energia">
      <span>⚡</span>
      <small>Energia percebida</small>
      <strong id="energiaTotal">-</strong>
    </div>
  </section>

  <!-- REGISTRO DE REFEIÇÃO -->
  <section class="card">
    <div class="titulo">
      <h2>🍲 Registrar refeição</h2>
    </div>
    <p>Registre o que foi consumido e como você se sentiu.</p>
    <form id="formRefeicao">
      <input type="hidden" id="refeicaoId">
      <div class="form-grid">
        <div class="campo">
          <label for="tipoRefeicao">Tipo de refeição *</label>
          <select id="tipoRefeicao" required>
            <option value="">Selecione</option>
            <option>Café da manhã</option>
            <option>Lanche da manhã</option>
            <option>Almoço</option>
            <option>Lanche da tarde</option>
            <option>Jantar</option>
            <option>Lanche noturno</option>
            <option>Refeição pré-treino</option>
            <option>Refeição pós-treino</option>
          </select>
        </div>
        <div class="campo">
          <label for="horario">Horário *</label>
          <input type="time" id="horario" required>
        </div>
        <div class="campo grande">
          <label for="alimentos">Alimentos consumidos *</label>
          <textarea id="alimentos" placeholder="Ex.: arroz, feijão, legumes..." required></textarea>
        </div>
        <div class="campo">
          <label for="porcao">Porção / quantidade</label>
          <input type="text" id="porcao" placeholder="Ex.: 1 prato">
        </div>
        <div class="campo">
          <label for="relacaoTreino">Antes ou depois do treino?</label>
          <select id="relacaoTreino">
            <option value="Não informado">Não informado</option>
            <option value="Antes do treino">Antes do treino</option>
            <option value="Depois do treino">Depois do treino</option>
            <option value="Sem relação">Sem relação</option>
          </select>
        </div>
        <div class="campo grande">
          <label for="observacoes">Observações</label>
          <textarea id="observacoes" placeholder="Como se sentiu após a refeição?"></textarea>
        </div>
      </div>
      <div class="botoes">
        <button type="submit" class="btn btn-primary" id="btnSalvar">➕ Registrar refeição</button>
        <button type="button" class="btn btn-secondary" id="btnCancelar" hidden>Cancelar</button>
      </div>
    </form>
  </section>

  <!-- HIDRATAÇÃO -->
  <section class="card">
    <div class="titulo">
      <h2>💧 Controle de hidratação</h2>
    </div>
    <p>Registre a ingestão de líquidos ao longo do dia.</p>
    <div class="hidratacao">
      <div class="agua-contador">
        <div class="agua-visual">
          <span>🥛</span>
          <strong id="aguaExibida">0 ml</strong>
        </div>
      </div>
      <div class="agua-acoes">
        <button class="btn btn-agua" onclick="adicionarAgua(200)">+ 200 ml</button>
        <button class="btn btn-agua" onclick="adicionarAgua(300)">+ 300 ml</button>
        <button class="btn btn-agua" onclick="adicionarAgua(500)">+ 500 ml</button>
        <button class="btn btn-secondary" id="btnZerarAgua" onclick="zerarAgua()">Zerar</button>
      </div>
    </div>
  </section>

  <!-- ROTINA DIÁRIA -->
  <section class="card">
    <div class="titulo">
      <h2>🌙 Rotina diária</h2>
    </div>
    <p>Registre informações subjetivas da rotina.</p>
    <div class="rotina-grid">
      <div class="campo">
        <label for="sono">Horas de sono</label>
        <input type="number" id="sono" min="0" max="24" step="0.5" placeholder="Ex.: 8">
      </div>
      <div class="campo">
        <label for="energia">Energia percebida</label>
        <select id="energia">
          <option value="">Selecione</option>
          <option value="Muito baixa">Muito baixa</option>
          <option value="Baixa">Baixa</option>
          <option value="Moderada">Moderada</option>
          <option value="Boa">Boa</option>
          <option value="Muito boa">Muito boa</option>
        </select>
      </div>
      <div class="campo grande">
        <label for="observacaoDia">Observações sobre o dia</label>
        <textarea id="observacaoDia" placeholder="Ex.: disposição, recuperação, rotina..."></textarea>
      </div>
    </div>
    <div class="botoes">
      <button type="button" class="btn btn-primary" id="btnSalvarRotina" onclick="salvarRotina()">💾 Salvar rotina</button>
    </div>
  </section>

  <!-- HISTÓRICO E FILTROS -->
  <section class="card">
    <div class="cabecalho">
      <h2>📋 Histórico alimentar</h2>
    </div>
    <p>Consulte os registros realizados.</p>
    <div class="tabela-container">
      <table>
        <thead>
          <tr>
            <th>Horário</th>
            <th>Tipo</th>
            <th>Alimentos</th>
            <th>Porção</th>
            <th>Relação Treino</th>
            <th>Ações</th>
          </tr>
        </thead>
        <tbody id="tabelaRefeicoes"></tbody>
      </table>
    </div>
    <div class="sem-registros" id="semRegistros">
      <h3>Nenhuma refeição registrada</h3>
      <p>Utilize o formulário acima para começar.</p>
    </div>
  </section>

  <script>
    let consumoAguaMl = 0;
    let refeicoes = [];

    document.getElementById('dataRegistro').valueAsDate = new Date();

    function adicionarAgua(quantidade) {
      consumoAguaMl += quantidade;
      atualizarHidratacao();
    }

    function zerarAgua() {
      consumoAguaMl = 0;
      atualizarHidratacao();
    }

    function atualizarHidratacao() {
      document.getElementById('aguaExibida').innerText = `${consumoAguaMl} ml`;
      document.getElementById('aguaTotal').innerText = `${(consumoAguaMl / 1000).toFixed(1)} L`;
    }

    function salvarRotina() {
      const sono = document.getElementById('sono').value;
      const energia = document.getElementById('energia').value;

      document.getElementById('sonoTotal').innerText = sono ? `${sono} h` : '-';
      document.getElementById('energiaTotal').innerText = energia || '-';
      alert('Rotina salva com sucesso!');
    }

    document.getElementById('formRefeicao').addEventListener('submit', function(e) {
      e.preventDefault();

      const tipo = document.getElementById('tipoRefeicao').value;
      const horario = document.getElementById('horario').value;
      const alimentos = document.getElementById('alimentos').value;
      const porcao = document.getElementById('porcao').value || '-';
      const relacaoTreino = document.getElementById('relacaoTreino').value;

      const novaRefeicao = { tipo, horario, alimentos, porcao, relacaoTreino };
      refeicoes.push(novaRefeicao);

      document.getElementById('formRefeicao').reset();
      atualizarTabela();
    });

    function atualizarTabela() {
      const tbody = document.getElementById('tabelaRefeicoes');
      const semRegistros = document.getElementById('semRegistros');
      tbody.innerHTML = '';

      if (refeicoes.length === 0) {
        semRegistros.style.display = 'block';
      } else {
        semRegistros.style.display = 'none';
        refeicoes.forEach((ref, index) => {
          const tr = document.createElement('tr');
          tr.innerHTML = `
            <td>${ref.horario}</td>
            <td>${ref.tipo}</td>
            <td>${ref.alimentos}</td>
            <td>${ref.porcao}</td>
            <td>${ref.relacaoTreino}</td>
            <td><button class="btn btn-danger" onclick="removerRefeicao(${index})">Excluir</button></td>
          `;
          tbody.appendChild(tr);
        });
      }

      document.getElementById('totalRefeicoes').innerText = refeicoes.length;
    }

    function removerRefeicao(index) {
      refeicoes.splice(index, 1);
      atualizarTabela();
    }
  </script>
</body>
</html>
