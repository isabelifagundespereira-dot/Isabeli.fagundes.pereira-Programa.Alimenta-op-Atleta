# Isabeli.fagundes.pereira-Programa.Alimenta-op-Atleta
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Controle de Alimentação do Atleta</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <header class="topo">
        <div class="marca">
            <div class="icone-marca">🏃</div>
            <div>
                <h1>AtletaControl</h1>
                <p>Controle de alimentação e rotina esportiva</p>
            </div>
        </div>
        <button id="btnTema" class="btn btn-tema">
            🌙 Tema escuro
        </button>
    </header>

    <main class="container">
        <!-- PERFIL -->
        <section class="card">
            <div class="titulo">
                <h2>👤 Perfil do atleta</h2>
                <p>Informações para organização dos registros.</p>
            </div>
            <div class="grid-perfil">
                <div class="campo">
                    <label>Nome</label>
                    <input type="text" id="atletaNome" placeholder="Nome do atleta">
                </div>
                <div class="campo">
                    <label>Modalidade</label>
                    <input type="text" id="modalidade" placeholder="Ex.: futebol">
                </div>
                <div class="campo">
                    <label>Equipe / Clube</label>
                    <input type="text" id="equipe" placeholder="Nome da equipe">
                </div>
                <div class="campo">
                    <label>Data</label>
                    <input type="date" id="dataRegistro">
                </div>
            </div>
        </section>

        <!-- RESUMO -->
        <section class="dashboard">
            <div class="indicador">
                <span>🍽️</span>
                <div>
                    <small>Refeições registradas</small>
                    <strong id="totalRefeicoes">0</strong>
                </div>
            </div>
            <div class="indicador agua">
                <span>💧</span>
                <div>
                    <small>Água registrada</small>
                    <strong id="aguaTotal">0 L</strong>
                </div>
            </div>
            <div class="indicador sono">
                <span>🌙</span>
                <div>
                    <small>Sono</small>
                    <strong id="sonoTotal">--</strong>
                </div>
            </div>
            <div class="indicador energia">
                <span>⚡</span>
                <div>
                    <small>Energia percebida</small>
                    <strong id="energiaTotal">--</strong>
                </div>
            </div>
        </section>

        <!-- REGISTRO DE REFEIÇÃO -->
        <section class="card">
            <div class="titulo">
                <h2>🥗 Registrar refeição</h2>
                <p>Registre o que foi consumido e como você se sentiu.</p>
            </div>
            <form id="formRefeicao">
                <input type="hidden" id="refeicaoId">
                <div class="form-grid">
                    <div class="campo">
                        <label>Tipo de refeição *</label>
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
                        <label>Horário *</label>
                        <input type="time" id="horario" required>
                    </div>
                    <div class="campo grande">
                        <label>Alimentos consumidos *</label>
                        <input type="text" id="alimentos" placeholder="Ex.: arroz, feijão, legumes..." required>
                    </div>
                    <div class="campo">
                        <label>Porção / quantidade</label>
                        <input type="text" id="portcao" placeholder="Ex.: 1 prato">
                    </div>
                    <div class="campo">
                        <label>Antes ou depois do treino?</label>
                        <select id="relacaoTreino">
                            <option value="Não informado">Não informado</option>
                            <option value="Antes do treino">Antes do treino</option>
                            <option value="Depois do treino">Depois do treino</option>
                            <option value="Sem relação">Sem relação</option>
                        </select>
                    </div>
                    <div class="campo grande">
                        <label>Observações</label>
                        <textarea id="observacoes" placeholder="Como se sentiu após a refeição?"></textarea>
                    </div>
                </div>
                <div class="botoes">
                    <button type="submit" class="btn btn-primary" id="btnSalvar">
                        + Registrar refeição
                    </button>
                    <button type="button" class="btn btn-secondary" id="btnCancelar" hidden>
                        Cancelar
                    </button>
                </div>
            </form>
        </section>

        <!-- HIDRATAÇÃO -->
        <section class="card">
            <div class="titulo">
                <h2>💧 Controle de hidratação</h2>
                <p>Registre a ingestão de líquidos ao longo do dia.</p>
            </div>
            <div class="hidratacao">
                <div class="agua-contador">
                    <div class="agua-visual">
                        <span>💧</span>
                        <strong id="aguaExibida">0 ml</strong>
                    </div>
                </div>
                <div class="agua-acoes">
                    <button class="btn btn-agua" data-agua="200">
                        + 200 ml
                    </button>
                    <button class="btn btn-agua" data-agua="300">
                        + 300 ml
                    </button>
                    <button class="btn btn-agua" data-agua="500">
                        + 500 ml
                    </button>
                    <button class="btn btn-secondary" id="btnZerarAgua">
                        Zerar
                    </button>
                </div>
            </div>
        </section>

        <!-- ROTINA -->
        <section class="card">
            <div class="titulo">
                <h2>🌙 Rotina diária</h2>
                <p>Registre informações subjetivas da rotina.</p>
            </div>
            <div class="rotina-grid">
                <div class="campo">
                    <label>Horas de sono</label>
                    <input type="number" id="sono" min="0" max="24" step="0.5" placeholder="Ex.: 8">
                </div>
                <div class="campo">
                    <label>Energia percebida</label>
                    <select id="energia">
                        <option value="">Selecione</option>
                        <option value="Muito baixa">Muito baixa</option>
                        <option value="Baixa">Baixa</option>
                        <option value="Moderada">Moderada</option>
                        <option value="Boa">Boa</option>
                        <option value="Muito boa">Muito boa</option>
                    </select>
                </div>
                <div class="campo campo-grande">
                    <label>Observações sobre o dia</label>
                    <textarea id="observacaoDia" placeholder="Ex.: disposição, recuperação, rotina..."></textarea>
                </div>
            </div>
            <button id="btnSalvarRotina" class="btn btn-primary">
                💾 Salvar rotina
            </button>
        </section>

        <!-- FILTROS -->
        <section class="card">
            <div class="cabecalho">
                <div>
                    <h2>📊 Histórico alimentar</h2>
                    <p>Consulte os registros realizados.</p>
                </div>
                <div class="acoes">
                    <button id="btnExportar" class="btn btn-success">
                        📥 Exportar CSV
                    </button>
                    <button id="btnImprimir" class="btn btn-secondary">
                        🖨️ Imprimir
                    </button>
                    <button id="btnLimpar" class="btn btn-danger">
                        🗑️ Limpar
                    </button>
                </div>
            </div>
            <div class="filtros">
                <div class="campo">
                    <label>Pesquisar</label>
                    <input type="search" id="pesquisa" placeholder="🔍 Alimento ou refeição">
                </div>
                <div class="campo">
                    <label>Tipo</label>
                    <select id="filtroTipo">
                        <option value="todos">Todos</option>
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
            </div>
            <div class="tabela-container">
                <table>
                    <thead>
                        <tr>
                            <th>Data</th>
                            <th>Horário</th>
                            <th>Refeição</th>
                            <th>Alimentos</th>
                            <th>Porção</th>
                            <th>Treino</th>
                            <th>Ações</th>
                        </tr>
                    </thead>
                    <tbody id="tabelaRefeicoes"></tbody>
                </table>
                <div id="semRegistros" class="vazio">
                    <span>🍽️</span>
                    <h3>Nenhuma refeição registrada</h3>
                    <p>Utilize o formulário acima para começar.</p>
                </div>
            </div>
        </section>
    </main>

    <!-- MODAL -->
    <div id="modal" class="modal" hidden>
        <div class="modal-conteudo">
            <div class="modal-icone">
                ⚠️
            </div>
            <h2>Confirmação</h2>
            <p id="modalTexto">Deseja continuar?</p>
            <div class="modal-botoes">
                <button id="modalCancelar" class="btn btn-secondary">
                    Cancelar
                </button>
                <button id="modalConfirmar" class="btn btn-danger">
                    Confirmar
                </button>
            </div>
        </div>
    </div>

    <!-- TOAST -->
    <div id="toast" class="toast">
        <span id="toastIcon">✅</span>
        <span id="toastTexto">Operação realizada</span>
    </div>

    <footer>
        <strong>AtletaControl</strong>
        <p>Sistema de organização alimentar e rotina esportiva.</p>
    </footer>

    <script src="script.js"></script>
</body>
</html>
