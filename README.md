<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Rocha Finance</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <script src="https://unpkg.com/@phosphor-icons/web"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f3f4f6; /* Gray-100 */
        }
        .hide-scrollbar::-webkit-scrollbar {
            display: none;
        }
        .hide-scrollbar {
            -ms-overflow-style: none;
            scrollbar-width: none;
        }
        .tab-content {
            display: none;
            animation: fadeIn 0.3s ease;
        }
        .tab-content.active {
            display: block;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(5px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        /* WhatsApp Chat Styles */
        .chat-bg {
            background-color: #efeae2;
            background-image: url('https://w0.peakpx.com/wallpaper/508/135/HD-wallpaper-whatsapp-background-solid-color.jpg');
            background-blend-mode: overlay;
        }
        .msg-bubble {
            max-width: 80%;
            word-wrap: break-word;
        }
    </style>
</head>
<body class="text-gray-800 h-screen flex flex-col md:flex-row overflow-hidden">

    <!-- Sidebar / Bottom Nav -->
    <nav class="bg-white shadow-lg z-20 md:w-64 md:flex-shrink-0 flex md:flex-col justify-between order-last md:order-first fixed bottom-0 w-full md:relative md:h-screen border-t md:border-r border-gray-200">
        <div class="hidden md:flex items-center justify-center h-20 border-b border-gray-100 px-6">
            <i class="ph-fill ph-wallet text-3xl text-emerald-600 mr-2"></i>
            <h1 class="text-xl font-bold text-gray-800 tracking-tight">Rocha Finance</h1>
        </div>
        
        <div class="flex md:flex-col w-full md:flex-1 px-2 md:px-4 py-2 md:py-6 justify-between md:justify-start gap-1 md:gap-2">
            <button onclick="switchTab('dashboard')" id="nav-dashboard" class="nav-btn flex-1 md:flex-none flex flex-col md:flex-row items-center md:justify-start p-2 md:p-3 rounded-xl hover:bg-gray-50 text-emerald-600 bg-emerald-50 transition-colors">
                <i class="ph ph-squares-four text-2xl md:mr-3"></i>
                <span class="text-xs md:text-sm font-medium mt-1 md:mt-0">Painel</span>
            </button>
            <button onclick="switchTab('transactions')" id="nav-transactions" class="nav-btn flex-1 md:flex-none flex flex-col md:flex-row items-center md:justify-start p-2 md:p-3 rounded-xl hover:bg-gray-50 text-gray-500 transition-colors">
                <i class="ph ph-list-dashes text-2xl md:mr-3"></i>
                <span class="text-xs md:text-sm font-medium mt-1 md:mt-0">Histórico</span>
            </button>
            <button onclick="switchTab('chat')" id="nav-chat" class="nav-btn flex-1 md:flex-none flex flex-col md:flex-row items-center md:justify-start p-2 md:p-3 rounded-xl hover:bg-gray-50 text-gray-500 transition-colors relative">
                <i class="ph ph-whatsapp-logo text-2xl md:mr-3 text-green-500"></i>
                <span class="text-xs md:text-sm font-medium mt-1 md:mt-0">WhatsApp</span>
                <span class="absolute top-2 right-2 md:right-4 w-2 h-2 bg-red-500 rounded-full animate-pulse"></span>
            </button>
            <button onclick="switchTab('budgets')" id="nav-budgets" class="nav-btn flex-1 md:flex-none flex flex-col md:flex-row items-center md:justify-start p-2 md:p-3 rounded-xl hover:bg-gray-50 text-gray-500 transition-colors">
                <i class="ph ph-target text-2xl md:mr-3"></i>
                <span class="text-xs md:text-sm font-medium mt-1 md:mt-0">Limites</span>
            </button>
            <button onclick="switchTab('categories')" id="nav-categories" class="nav-btn flex-1 md:flex-none flex flex-col md:flex-row items-center md:justify-start p-2 md:p-3 rounded-xl hover:bg-gray-50 text-gray-500 transition-colors">
                <i class="ph ph-tag text-2xl md:mr-3"></i>
                <span class="text-xs md:text-sm font-medium mt-1 md:mt-0">Categorias</span>
            </button>
        </div>
    </nav>

    <!-- Main Content Area -->
    <main class="flex-1 flex flex-col h-[calc(100vh-64px)] md:h-screen overflow-hidden bg-gray-50 relative">
        
        <!-- Header -->
        <header class="bg-white shadow-sm z-10 px-6 py-4 flex justify-between items-center flex-shrink-0">
            <div class="md:hidden flex items-center">
                <i class="ph-fill ph-wallet text-2xl text-emerald-600 mr-2"></i>
                <h1 class="text-lg font-bold text-gray-800">Rocha Finance</h1>
            </div>
            <div class="hidden md:block">
                <h2 class="text-xl font-semibold text-gray-800" id="current-view-title">Visão Geral</h2>
            </div>
            <div class="flex items-center space-x-4 bg-gray-100 rounded-lg p-1">
                <button onclick="changeMonth(-1)" class="p-2 text-gray-600 hover:text-emerald-600 transition"><i class="ph ph-caret-left font-bold"></i></button>
                <span id="current-month-display" class="font-medium text-sm md:text-base min-w-[100px] text-center capitalize">Maio 2026</span>
                <button onclick="changeMonth(1)" class="p-2 text-gray-600 hover:text-emerald-600 transition"><i class="ph ph-caret-right font-bold"></i></button>
            </div>
        </header>

        <!-- Scrollable Content -->
        <div class="flex-1 overflow-y-auto p-4 md:p-6 pb-24 md:pb-6 hide-scrollbar">
            
            <!-- TAB: Dashboard -->
            <div id="tab-dashboard" class="tab-content active max-w-5xl mx-auto">
                <!-- Summary Cards -->
                <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-8">
                    <div class="bg-white rounded-2xl p-5 shadow-sm border border-gray-100">
                        <p class="text-sm text-gray-500 font-medium mb-1">Saldo Total</p>
                        <h3 id="card-balance" class="text-3xl font-bold text-gray-800">R$ 0,00</h3>
                    </div>
                    <div class="bg-emerald-50 rounded-2xl p-5 shadow-sm border border-emerald-100">
                        <div class="flex justify-between items-center mb-1">
                            <p class="text-sm text-emerald-700 font-medium">Entradas</p>
                            <i class="ph ph-arrow-up-right text-emerald-600 bg-emerald-100 p-1 rounded-full"></i>
                        </div>
                        <h3 id="card-income" class="text-2xl font-bold text-emerald-700">R$ 0,00</h3>
                    </div>
                    <div class="bg-red-50 rounded-2xl p-5 shadow-sm border border-red-100">
                        <div class="flex justify-between items-center mb-1">
                            <p class="text-sm text-red-700 font-medium">Saídas</p>
                            <i class="ph ph-arrow-down-right text-red-600 bg-red-100 p-1 rounded-full"></i>
                        </div>
                        <h3 id="card-expense" class="text-2xl font-bold text-red-700">R$ 0,00</h3>
                    </div>
                </div>

                <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
                    <!-- Categories Chart -->
                    <div class="bg-white rounded-2xl p-6 shadow-sm border border-gray-100">
                        <h3 class="text-lg font-semibold text-gray-800 mb-4">Despesas por Categoria</h3>
                        <div class="relative h-64 w-full flex items-center justify-center">
                            <canvas id="expensesChart"></canvas>
                            <div id="no-chart-data" class="absolute inset-0 flex items-center justify-center text-gray-400 hidden">
                                Sem dados para este mês
                            </div>
                        </div>
                    </div>

                    <!-- Budget Progress -->
                    <div class="bg-white rounded-2xl p-6 shadow-sm border border-gray-100">
                        <h3 class="text-lg font-semibold text-gray-800 mb-4">Status dos Limites</h3>
                        <div id="dashboard-budgets" class="space-y-4">
                            <!-- Populated by JS -->
                        </div>
                    </div>
                </div>
            </div>

            <!-- TAB: Transactions -->
            <div id="tab-transactions" class="tab-content max-w-5xl mx-auto">
                <div class="flex justify-between items-center mb-6">
                    <h3 class="text-xl font-semibold text-gray-800">Histórico de Lançamentos</h3>
                    <button onclick="openTransactionModal()" class="bg-emerald-600 hover:bg-emerald-700 text-white px-4 py-2 rounded-lg font-medium transition shadow-sm flex items-center">
                        <i class="ph ph-plus font-bold mr-2"></i> Novo
                    </button>
                </div>
                
                <div class="bg-white rounded-2xl shadow-sm border border-gray-100 overflow-hidden">
                    <div class="overflow-x-auto">
                        <table class="w-full text-left border-collapse">
                            <thead>
                                <tr class="bg-gray-50 text-gray-500 text-xs uppercase tracking-wider">
                                    <th class="p-4 font-medium">Data</th>
                                    <th class="p-4 font-medium">Descrição</th>
                                    <th class="p-4 font-medium">Categoria</th>
                                    <th class="p-4 font-medium text-right">Valor</th>
                                    <th class="p-4 font-medium text-center">Ações</th>
                                </tr>
                            </thead>
                            <tbody id="transactions-list" class="divide-y divide-gray-100">
                                <!-- Populated by JS -->
                            </tbody>
                        </table>
                        <div id="empty-transactions" class="py-12 text-center text-gray-500 hidden">
                            <i class="ph ph-receipt text-4xl mb-2 text-gray-300"></i>
                            <p>Nenhuma transação neste mês.</p>
                        </div>
                    </div>
                </div>
            </div>

            <!-- TAB: WhatsApp Simulator -->
            <div id="tab-chat" class="tab-content max-w-2xl mx-auto h-[70vh] md:h-[80vh] flex flex-col">
                <div class="bg-[#075e54] text-white p-4 rounded-t-2xl flex items-center shadow-md">
                    <div class="w-10 h-10 bg-white rounded-full flex items-center justify-center mr-3">
                        <i class="ph-fill ph-robot text-[#075e54] text-2xl"></i>
                    </div>
                    <div>
                        <h3 class="font-semibold text-lg leading-tight">Bot Rocha Finance</h3>
                        <p class="text-xs text-green-100">Inteligência Artificial Ativa</p>
                    </div>
                </div>
                
                <div class="flex-1 chat-bg overflow-y-auto p-4 flex flex-col space-y-4" id="chat-messages">
                    <!-- Welcome Message -->
                    <div class="flex justify-start">
                        <div class="bg-white text-gray-800 p-3 rounded-xl rounded-tl-none msg-bubble shadow-sm text-sm">
                            Olá! Eu sou seu assistente financeiro. 🤖<br><br>
                            Você pode enviar mensagens como:<br>
                            👉 <i>"Gasolina 50"</i><br>
                            👉 <i>"Mercado R$ 150,00"</i><br>
                            👉 <i>"Salario 5000"</i><br><br>
                            Vou registrar automaticamente. Se eu errar a categoria, basta editar no histórico e eu <b>aprenderei para a próxima vez</b>!
                            <span class="block text-right text-[10px] text-gray-400 mt-1">Agora</span>
                        </div>
                    </div>
                </div>

                <div class="bg-gray-100 p-3 rounded-b-2xl flex items-center space-x-2">
                    <input type="text" id="chat-input" placeholder="Digite uma despesa..." class="flex-1 bg-white border-none rounded-full px-4 py-3 focus:outline-none focus:ring-2 focus:ring-emerald-500 shadow-sm" onkeypress="handleChatKeyPress(event)">
                    <button onclick="sendChatMessage()" class="bg-[#128c7e] hover:bg-[#075e54] text-white w-12 h-12 rounded-full flex items-center justify-center transition shadow-md flex-shrink-0">
                        <i class="ph-fill ph-paper-plane-right text-xl"></i>
                    </button>
                </div>
            </div>

            <!-- TAB: Budgets -->
            <div id="tab-budgets" class="tab-content max-w-3xl mx-auto">
                <div class="flex justify-between items-center mb-6">
                    <h3 class="text-xl font-semibold text-gray-800">Limites por Categoria (Orçamento)</h3>
                </div>
                <p class="text-gray-500 mb-6 text-sm">Defina um limite de gastos para cada categoria de despesa. Os valores salvos valem para todos os meses.</p>
                
                <div class="bg-white rounded-2xl shadow-sm border border-gray-100 p-6">
                    <div id="budget-list" class="space-y-4">
                        <!-- Populated by JS -->
                    </div>
                    <div class="mt-6 pt-4 border-t border-gray-100 flex justify-end">
                        <button onclick="saveBudgets()" class="bg-emerald-600 hover:bg-emerald-700 text-white px-6 py-2 rounded-lg font-medium transition shadow-sm">
                            Salvar Limites
                        </button>
                    </div>
                </div>
            </div>

            <!-- TAB: Categories -->
            <div id="tab-categories" class="tab-content max-w-3xl mx-auto">
                <div class="flex justify-between items-center mb-6">
                    <h3 class="text-xl font-semibold text-gray-800">Gerenciar Categorias</h3>
                    <button onclick="openCategoryModal()" class="bg-emerald-600 hover:bg-emerald-700 text-white px-4 py-2 rounded-lg font-medium transition shadow-sm flex items-center">
                        <i class="ph ph-plus font-bold mr-2"></i> Nova
                    </button>
                </div>
                
                <div class="grid grid-cols-1 md:grid-cols-2 gap-4" id="categories-grid">
                    <!-- Populated by JS -->
                </div>
            </div>

        </div>
    </main>

    <!-- Modal: Transaction -->
    <div id="modal-transaction" class="fixed inset-0 bg-black/50 z-50 hidden flex items-center justify-center backdrop-blur-sm p-4">
        <div class="bg-white rounded-2xl w-full max-w-md shadow-xl overflow-hidden flex flex-col max-h-[90vh]">
            <div class="px-6 py-4 border-b border-gray-100 flex justify-between items-center bg-gray-50">
                <h3 class="text-lg font-bold text-gray-800" id="modal-tx-title">Nova Transação</h3>
                <button onclick="closeModal('modal-transaction')" class="text-gray-400 hover:text-red-500 transition"><i class="ph ph-x text-xl"></i></button>
            </div>
            
            <div class="p-6 overflow-y-auto hide-scrollbar">
                <form id="form-transaction" class="space-y-4">
                    <input type="hidden" id="tx-id">
                    <input type="hidden" id="tx-source"> <!-- To track if it came from chat -->
                    
                    <div class="flex bg-gray-100 p-1 rounded-lg">
                        <button type="button" id="btn-type-expense" onclick="setTxType('expense')" class="flex-1 py-2 text-sm font-medium rounded-md bg-white shadow-sm text-red-600 transition">Saída</button>
                        <button type="button" id="btn-type-income" onclick="setTxType('income')" class="flex-1 py-2 text-sm font-medium rounded-md text-gray-500 hover:text-emerald-600 transition">Entrada</button>
                        <input type="hidden" id="tx-type" value="expense">
                    </div>

                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-1">Descrição</label>
                        <input type="text" id="tx-desc" required class="w-full border border-gray-300 rounded-lg px-3 py-2 focus:ring-2 focus:ring-emerald-500 focus:border-emerald-500 outline-none transition" placeholder="Ex: Conta de Luz">
                    </div>
                    
                    <div class="grid grid-cols-2 gap-4">
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-1">Valor (R$)</label>
                            <input type="number" step="0.01" id="tx-amount" required class="w-full border border-gray-300 rounded-lg px-3 py-2 focus:ring-2 focus:ring-emerald-500 focus:border-emerald-500 outline-none transition" placeholder="0.00">
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-1">Data</label>
                            <input type="date" id="tx-date" required class="w-full border border-gray-300 rounded-lg px-3 py-2 focus:ring-2 focus:ring-emerald-500 focus:border-emerald-500 outline-none transition">
                        </div>
                    </div>

                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-1">Categoria</label>
                        <select id="tx-category" required class="w-full border border-gray-300 rounded-lg px-3 py-2 focus:ring-2 focus:ring-emerald-500 focus:border-emerald-500 outline-none transition">
                            <!-- Populated JS -->
                        </select>
                    </div>

                    <div id="installments-container" class="pt-2 border-t border-gray-100 mt-4">
                        <label class="flex items-center space-x-2 cursor-pointer">
                            <input type="checkbox" id="tx-is-installment" onchange="toggleInstallments()" class="rounded text-emerald-600 focus:ring-emerald-500">
                            <span class="text-sm font-medium text-gray-700">Lançamento parcelado (meses)</span>
                        </label>
                        <div id="installments-opts" class="hidden mt-3 p-3 bg-gray-50 rounded-lg border border-gray-200">
                            <label class="block text-xs text-gray-500 mb-1">Número de parcelas</label>
                            <input type="number" id="tx-installments" min="2" max="60" value="2" class="w-full border border-gray-300 rounded-lg px-3 py-2 focus:ring-2 focus:ring-emerald-500 outline-none transition">
                            <p class="text-xs text-gray-500 mt-2"><i class="ph ph-info"></i> O valor total será dividido pelo número de parcelas informadas.</p>
                        </div>
                    </div>
                </form>
            </div>
            
            <div class="px-6 py-4 border-t border-gray-100 bg-gray-50 flex justify-end space-x-3 mt-auto">
                <button onclick="closeModal('modal-transaction')" class="px-4 py-2 text-gray-600 hover:bg-gray-200 rounded-lg font-medium transition">Cancelar</button>
                <button onclick="saveTransaction()" class="px-4 py-2 bg-emerald-600 hover:bg-emerald-700 text-white rounded-lg font-medium transition shadow-sm">Salvar</button>
            </div>
        </div>
    </div>

    <!-- Modal: Category -->
    <div id="modal-category" class="fixed inset-0 bg-black/50 z-50 hidden flex items-center justify-center backdrop-blur-sm p-4">
        <div class="bg-white rounded-2xl w-full max-w-sm shadow-xl overflow-hidden">
            <div class="px-6 py-4 border-b border-gray-100 flex justify-between items-center bg-gray-50">
                <h3 class="text-lg font-bold text-gray-800">Nova Categoria</h3>
                <button onclick="closeModal('modal-category')" class="text-gray-400 hover:text-red-500 transition"><i class="ph ph-x text-xl"></i></button>
            </div>
            <div class="p-6">
                <div class="space-y-4">
                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-1">Nome da Categoria</label>
                        <input type="text" id="cat-name" required class="w-full border border-gray-300 rounded-lg px-3 py-2 focus:ring-2 focus:ring-emerald-500 outline-none transition" placeholder="Ex: Viagens">
                    </div>
                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-1">Tipo Predominante</label>
                        <select id="cat-type" class="w-full border border-gray-300 rounded-lg px-3 py-2 focus:ring-2 focus:ring-emerald-500 outline-none transition">
                            <option value="expense">Saída (Despesa)</option>
                            <option value="income">Entrada (Receita)</option>
                        </select>
                    </div>
                </div>
            </div>
            <div class="px-6 py-4 border-t border-gray-100 bg-gray-50 flex justify-end space-x-3">
                <button onclick="closeModal('modal-category')" class="px-4 py-2 text-gray-600 hover:bg-gray-200 rounded-lg font-medium transition">Cancelar</button>
                <button onclick="saveCategory()" class="px-4 py-2 bg-emerald-600 hover:bg-emerald-700 text-white rounded-lg font-medium transition shadow-sm">Salvar</button>
            </div>
        </div>
    </div>

    <!-- Message Box Overlay (replaces alert) -->
    <div id="message-box" class="fixed inset-0 bg-black/40 z-[60] hidden flex items-center justify-center backdrop-blur-sm p-4">
        <div class="bg-white rounded-2xl p-6 w-full max-w-sm text-center shadow-2xl transform scale-95 transition-transform duration-200" id="msg-box-content">
            <div id="msg-icon" class="mx-auto flex items-center justify-center h-12 w-12 rounded-full bg-emerald-100 mb-4">
                <i class="ph ph-check text-2xl text-emerald-600"></i>
            </div>
            <h3 class="text-lg font-bold text-gray-900 mb-2" id="msg-title">Sucesso</h3>
            <p class="text-sm text-gray-500 mb-6" id="msg-text">Operação realizada.</p>
            <button onclick="closeMessageBox()" class="w-full inline-flex justify-center rounded-lg border border-transparent bg-emerald-600 px-4 py-2 text-base font-medium text-white shadow-sm hover:bg-emerald-700 focus:outline-none focus:ring-2 focus:ring-emerald-500 focus:ring-offset-2 sm:text-sm">
                OK
            </button>
        </div>
    </div>

    <!-- Confirm Box Overlay -->
    <div id="confirm-box" class="fixed inset-0 bg-black/40 z-[60] hidden flex items-center justify-center backdrop-blur-sm p-4">
        <div class="bg-white rounded-2xl p-6 w-full max-w-sm text-center shadow-2xl">
            <div class="mx-auto flex items-center justify-center h-12 w-12 rounded-full bg-red-100 mb-4">
                <i class="ph ph-warning text-2xl text-red-600"></i>
            </div>
            <h3 class="text-lg font-bold text-gray-900 mb-2">Confirmar Exclusão</h3>
            <p class="text-sm text-gray-500 mb-6">Tem certeza que deseja excluir este registro? Esta ação não pode ser desfeita.</p>
            <div class="flex justify-center space-x-3">
                <button onclick="closeConfirmBox()" class="px-4 py-2 text-gray-600 hover:bg-gray-100 rounded-lg font-medium transition">Cancelar</button>
                <button id="btn-confirm-action" class="px-4 py-2 bg-red-600 hover:bg-red-700 text-white rounded-lg font-medium transition shadow-sm">Excluir</button>
            </div>
        </div>
    </div>

    <script>
        // State Management
        let appState = {
            currentDate: new Date(2026, 4, 15), // May 2026 as per context
            transactions: [],
            categories: [
                { id: 'cat_1', name: 'Alimentação', type: 'expense', color: '#f59e0b', icon: 'ph-hamburger' },
                { id: 'cat_2', name: 'Transporte', type: 'expense', color: '#3b82f6', icon: 'ph-car' },
                { id: 'cat_3', name: 'Moradia', type: 'expense', color: '#8b5cf6', icon: 'ph-house' },
                { id: 'cat_4', name: 'Saúde', type: 'expense', color: '#ef4444', icon: 'ph-first-aid' },
                { id: 'cat_5', name: 'Lazer', type: 'expense', color: '#ec4899', icon: 'ph-popcorn' },
                { id: 'cat_6', name: 'Salário', type: 'income', color: '#10b981', icon: 'ph-money' },
                { id: 'cat_7', name: 'Outros', type: 'expense', color: '#6b7280', icon: 'ph-dots-three' }
            ],
            budgets: {}, // { categoryId: amount }
            keywordDict: {
                // Initial NLP learning dictionary for WhatsApp parsing
                'gasolina': 'cat_2', 'uber': 'cat_2', 'ônibus': 'cat_2', 'onibus': 'cat_2',
                'ifood': 'cat_1', 'mercado': 'cat_1', 'padaria': 'cat_1', 'restaurante': 'cat_1',
                'luz': 'cat_3', 'agua': 'cat_3', 'água': 'cat_3', 'aluguel': 'cat_3',
                'farmacia': 'cat_4', 'farmácia': 'cat_4', 'medico': 'cat_4',
                'cinema': 'cat_5', 'show': 'cat_5', 'bar': 'cat_5',
                'salario': 'cat_6', 'salário': 'cat_6', 'freela': 'cat_6'
            }
        };

        // Chart Instance
        let expensesChartInstance = null;

        // Utilities
        const generateId = () => '_' + Math.random().toString(36).substr(2, 9);
        
        const formatCurrency = (value) => {
            return new Intl.NumberFormat('pt-BR', { style: 'currency', currency: 'BRL' }).format(value);
        };

        const getMonthYearStr = (date) => {
            return `${date.getFullYear()}-${String(date.getMonth() + 1).padStart(2, '0')}`;
        };

        const getCategory = (id) => appState.categories.find(c => c.id === id) || appState.categories[appState.categories.length-1];

        // Custom Message Box
        function showMessage(title, text, type = 'success') {
            const box = document.getElementById('message-box');
            const icon = document.getElementById('msg-icon');
            document.getElementById('msg-title').innerText = title;
            document.getElementById('msg-text').innerText = text;
            
            if (type === 'error') {
                icon.className = 'mx-auto flex items-center justify-center h-12 w-12 rounded-full bg-red-100 mb-4';
                icon.innerHTML = '<i class="ph ph-x text-2xl text-red-600"></i>';
            } else {
                icon.className = 'mx-auto flex items-center justify-center h-12 w-12 rounded-full bg-emerald-100 mb-4';
                icon.innerHTML = '<i class="ph ph-check text-2xl text-emerald-600"></i>';
            }
            
            box.classList.remove('hidden');
        }
        function closeMessageBox() {
            document.getElementById('message-box').classList.add('hidden');
        }

        // Custom Confirm Box
        let confirmActionCb = null;
        function showConfirm(actionCb) {
            confirmActionCb = actionCb;
            document.getElementById('confirm-box').classList.remove('hidden');
        }
        function closeConfirmBox() {
            document.getElementById('confirm-box').classList.add('hidden');
            confirmActionCb = null;
        }
        document.getElementById('btn-confirm-action').addEventListener('click', () => {
            if(confirmActionCb) confirmActionCb();
            closeConfirmBox();
        });

        function initApp() {
            // Load dummy data just to not look empty initially if needed, but per prompt, let's start fresh or use local storage
            const stored = localStorage.getItem('rocha_finance_data');
            if (stored) {
                try {
                    let parsed = JSON.parse(stored);
                    appState.transactions = parsed.transactions || [];
                    if(parsed.categories && parsed.categories.length > 0) appState.categories = parsed.categories;
                    appState.budgets = parsed.budgets || {};
                    appState.keywordDict = parsed.keywordDict || appState.keywordDict;
                } catch(e) {}
            }

            updateView();
            populateCategorySelects();
            renderCategoriesTab();
            
            // Set initial chat greeting time
            document.querySelector('#chat-messages span').innerText = new Date().toLocaleTimeString('pt-BR', {hour: '2-digit', minute:'2-digit'});
        }

        function saveData() {
            localStorage.setItem('rocha_finance_data', JSON.stringify({
                transactions: appState.transactions,
                categories: appState.categories,
                budgets: appState.budgets,
                keywordDict: appState.keywordDict
            }));
            updateView();
        }

        function switchTab(tabId) {
            document.querySelectorAll('.tab-content').forEach(el => el.classList.remove('active'));
            document.getElementById(`tab-${tabId}`).classList.add('active');
            
            // Update Nav visual
            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.classList.remove('text-emerald-600', 'bg-emerald-50');
                btn.classList.add('text-gray-500');
            });
            const activeBtn = document.getElementById(`nav-${tabId}`);
            activeBtn.classList.remove('text-gray-500');
            activeBtn.classList.add('text-emerald-600', 'bg-emerald-50');

            // Update Title
            const titles = {
                'dashboard': 'Visão Geral',
                'transactions': 'Histórico',
                'chat': 'Assistente Inteligente',
                'budgets': 'Metas e Limites',
                'categories': 'Categorias'
            };
            document.getElementById('current-view-title').innerText = titles[tabId];

            if(tabId === 'dashboard') renderDashboard();
            if(tabId === 'transactions') renderTransactions();
            if(tabId === 'budgets') renderBudgets();
            if(tabId === 'chat') {
                // Scroll to bottom
                const chatArea = document.getElementById('chat-messages');
                chatArea.scrollTop = chatArea.scrollHeight;
            }
        }

        function changeMonth(delta) {
            appState.currentDate.setMonth(appState.currentDate.getMonth() + delta);
            updateView();
        }

        function updateView() {
            // Update Header Month
            const monthNames = ['Janeiro', 'Fevereiro', 'Março', 'Abril', 'Maio', 'Junho', 'Julho', 'Agosto', 'Setembro', 'Outubro', 'Novembro', 'Dezembro'];
            document.getElementById('current-month-display').innerText = `${monthNames[appState.currentDate.getMonth()]} ${appState.currentDate.getFullYear()}`;
            
            renderSummary();
            
            // Re-render active tab content
            const activeTab = document.querySelector('.tab-content.active').id.replace('tab-', '');
            if(activeTab === 'dashboard') renderDashboard();
            if(activeTab === 'transactions') renderTransactions();
            if(activeTab === 'budgets') renderBudgets();
        }

        function getFilteredTransactions() {
            const currentPrefix = getMonthYearStr(appState.currentDate);
            return appState.transactions.filter(tx => tx.date.startsWith(currentPrefix));
        }

        function renderSummary() {
            const txs = getFilteredTransactions();
            let income = 0;
            let expense = 0;

            txs.forEach(tx => {
                if(tx.type === 'income') income += tx.amount;
                else expense += tx.amount;
            });

            document.getElementById('card-income').innerText = formatCurrency(income);
            document.getElementById('card-expense').innerText = formatCurrency(expense);
            
            const balance = income - expense;
            const balanceEl = document.getElementById('card-balance');
            balanceEl.innerText = formatCurrency(balance);
            if (balance < 0) {
                balanceEl.classList.remove('text-gray-800');
                balanceEl.classList.add('text-red-600');
            } else {
                balanceEl.classList.add('text-gray-800');
                balanceEl.classList.remove('text-red-600');
            }
        }

        function renderDashboard() {
            const txs = getFilteredTransactions();
            const expenses = txs.filter(t => t.type === 'expense');
            
            // 1. Chart Data
            const catTotals = {};
            expenses.forEach(tx => {
                catTotals[tx.categoryId] = (catTotals[tx.categoryId] || 0) + tx.amount;
            });

            const labels = [];
            const data = [];
            const bgColors = [];

            Object.keys(catTotals).forEach(catId => {
                const cat = getCategory(catId);
                labels.push(cat.name);
                data.push(catTotals[catId]);
                bgColors.push(cat.color || '#9ca3af');
            });

            const canvas = document.getElementById('expensesChart');
            const noDataLabel = document.getElementById('no-chart-data');
            
            if (data.length === 0) {
                canvas.style.display = 'none';
                noDataLabel.classList.remove('hidden');
            } else {
                canvas.style.display = 'block';
                noDataLabel.classList.add('hidden');
                
                if (expensesChartInstance) {
                    expensesChartInstance.destroy();
                }
                
                expensesChartInstance = new Chart(canvas, {
                    type: 'doughnut',
                    data: {
                        labels: labels,
                        datasets: [{
                            data: data,
                            backgroundColor: bgColors,
                            borderWidth: 0,
                            hoverOffset: 4
                        }]
                    },
                    options: {
                        responsive: true,
                        maintainAspectRatio: false,
                        plugins: {
                            legend: { position: 'right', labels: { usePointStyle: true, font: { family: 'Inter' } } },
                            tooltip: {
                                callbacks: {
                                    label: function(context) {
                                        return ' ' + formatCurrency(context.raw);
                                    }
                                }
                            }
                        },
                        cutout: '70%'
                    }
                });
            }

            // 2. Budgets Dashboard
            const dashBudgets = document.getElementById('dashboard-budgets');
            dashBudgets.innerHTML = '';
            
            let hasBudgets = false;
            Object.keys(appState.budgets).forEach(catId => {
                const limit = appState.budgets[catId];
                if(limit <= 0) return;
                hasBudgets = true;
                
                const cat = getCategory(catId);
                const spent = catTotals[catId] || 0;
                const percent = Math.min(100, (spent / limit) * 100);
                
                let colorClass = 'bg-emerald-500';
                if (percent > 85) colorClass = 'bg-red-500';
                else if (percent > 60) colorClass = 'bg-yellow-500';

                dashBudgets.innerHTML += `
                    <div>
                        <div class="flex justify-between text-sm mb-1">
                            <span class="font-medium text-gray-700 flex items-center"><i class="ph ${cat.icon} mr-1" style="color: ${cat.color}"></i> ${cat.name}</span>
                            <span class="text-gray-500">${formatCurrency(spent)} / ${formatCurrency(limit)}</span>
                        </div>
                        <div class="w-full bg-gray-100 rounded-full h-2">
                            <div class="${colorClass} h-2 rounded-full transition-all duration-500" style="width: ${percent}%"></div>
                        </div>
                    </div>
                `;
            });

            if(!hasBudgets) {
                dashBudgets.innerHTML = '<p class="text-sm text-gray-400 italic">Nenhum limite de gastos definido. Vá na aba "Limites".</p>';
            }
        }

        function renderTransactions() {
            const list = document.getElementById('transactions-list');
            const empty = document.getElementById('empty-transactions');
            const txs = getFilteredTransactions();
            
            // Sort by date descending
            txs.sort((a,b) => new Date(b.date) - new Date(a.date));

            list.innerHTML = '';
            
            if (txs.length === 0) {
                empty.classList.remove('hidden');
            } else {
                empty.classList.add('hidden');
                txs.forEach(tx => {
                    const cat = getCategory(tx.categoryId);
                    const isInc = tx.type === 'income';
                    const dateArr = tx.date.split('-'); // YYYY-MM-DD
                    const dateFmt = `${dateArr[2]}/${dateArr[1]}`;
                    
                    const installmentBadge = tx.installmentInfo ? `<span class="ml-2 text-[10px] bg-gray-100 text-gray-500 px-2 py-0.5 rounded-full">${tx.installmentInfo}</span>` : '';
                    const nlpBadge = tx.source === 'chat' ? `<i class="ph-fill ph-robot text-emerald-500 ml-1 text-xs" title="Adicionado via Chat"></i>` : '';

                    list.innerHTML += `
                        <tr class="hover:bg-gray-50 transition group">
                            <td class="p-4 text-sm text-gray-600 whitespace-nowrap">${dateFmt}</td>
                            <td class="p-4 text-sm text-gray-800 font-medium">
                                <div class="flex items-center">
                                    ${tx.description} ${installmentBadge} ${nlpBadge}
                                </div>
                            </td>
                            <td class="p-4 text-sm">
                                <span class="inline-flex items-center px-2 py-1 rounded-md text-xs font-medium" style="background-color: ${cat.color}15; color: ${cat.color}">
                                    <i class="ph ${cat.icon} mr-1"></i> ${cat.name}
                                </span>
                            </td>
                            <td class="p-4 text-sm font-semibold text-right ${isInc ? 'text-emerald-600' : 'text-gray-800'}">
                                ${isInc ? '+' : '-'} ${formatCurrency(tx.amount)}
                            </td>
                            <td class="p-4 text-center">
                                <div class="flex items-center justify-center space-x-2 opacity-0 group-hover:opacity-100 transition-opacity">
                                    <button onclick="editTransaction('${tx.id}')" class="text-gray-400 hover:text-blue-500" title="Editar"><i class="ph ph-pencil-simple"></i></button>
                                    <button onclick="deleteTransaction('${tx.id}')" class="text-gray-400 hover:text-red-500" title="Excluir"><i class="ph ph-trash"></i></button>
                                </div>
                                <div class="md:hidden flex items-center justify-center space-x-2">
                                    <button onclick="editTransaction('${tx.id}')" class="text-blue-500 p-2"><i class="ph ph-pencil-simple"></i></button>
                                    <button onclick="deleteTransaction('${tx.id}')" class="text-red-500 p-2"><i class="ph ph-trash"></i></button>
                                </div>
                            </td>
                        </tr>
                    `;
                });
            }
        }

        function openTransactionModal() {
            document.getElementById('form-transaction').reset();
            document.getElementById('tx-id').value = '';
            document.getElementById('tx-source').value = 'manual';
            document.getElementById('modal-tx-title').innerText = 'Nova Transação';
            
            // Default date to today but inside current view month if possible
            const viewMonth = getMonthYearStr(appState.currentDate);
            const todayStr = new Date().toISOString().split('T')[0];
            document.getElementById('tx-date').value = todayStr.startsWith(viewMonth.substring(0,4)) ? todayStr : `${viewMonth}-01`;
            
            setTxType('expense');
            document.getElementById('installments-container').classList.remove('hidden');
            document.getElementById('installments-opts').classList.add('hidden');
            document.getElementById('modal-transaction').classList.remove('hidden');
        }

        function closeModal(id) {
            document.getElementById(id).classList.add('hidden');
        }

        function toggleInstallments() {
            const isChecked = document.getElementById('tx-is-installment').checked;
            const opts = document.getElementById('installments-opts');
            if(isChecked) opts.classList.remove('hidden');
            else opts.classList.add('hidden');
        }

        function setTxType(type) {
            document.getElementById('tx-type').value = type;
            const btnExp = document.getElementById('btn-type-expense');
            const btnInc = document.getElementById('btn-type-income');
            
            if(type === 'expense') {
                btnExp.className = 'flex-1 py-2 text-sm font-medium rounded-md bg-white shadow-sm text-red-600 transition';
                btnInc.className = 'flex-1 py-2 text-sm font-medium rounded-md text-gray-500 hover:text-emerald-600 transition';
            } else {
                btnInc.className = 'flex-1 py-2 text-sm font-medium rounded-md bg-white shadow-sm text-emerald-600 transition';
                btnExp.className = 'flex-1 py-2 text-sm font-medium rounded-md text-gray-500 hover:text-red-600 transition';
            }

            // Filter categories based on type
            populateCategorySelects(type);
        }

        function populateCategorySelects(typeFilter = null) {
            const select = document.getElementById('tx-category');
            select.innerHTML = '';
            
            appState.categories.forEach(cat => {
                if(typeFilter && cat.type !== typeFilter && cat.id !== 'cat_7') return; // Show others always as fallback
                select.innerHTML += `<option value="${cat.id}">${cat.name}</option>`;
            });
        }

        function addMonthsToDateStr(dateStr, monthsToAdd) {
            let [y, m, d] = dateStr.split('-');
            let date = new Date(y, parseInt(m)-1, d);
            date.setMonth(date.getMonth() + monthsToAdd);
            return date.toISOString().split('T')[0];
        }

        function saveTransaction() {
            const id = document.getElementById('tx-id').value;
            const desc = document.getElementById('tx-desc').value;
            let amount = parseFloat(document.getElementById('tx-amount').value);
            const date = document.getElementById('tx-date').value;
            const categoryId = document.getElementById('tx-category').value;
            const type = document.getElementById('tx-type').value;
            const source = document.getElementById('tx-source').value;

            if(!desc || !amount || !date || !categoryId) {
                showMessage('Atenção', 'Preencha todos os campos obrigatórios.', 'error');
                return;
            }

            const isInstallment = document.getElementById('tx-is-installment').checked;

            if (id) {
                // Edit existing
                const index = appState.transactions.findIndex(t => t.id === id);
                if(index > -1) {
                    let oldTx = appState.transactions[index];
                    
                    // NLP LEARNING CORE FEATURE:
                    // If this transaction was originally created by the chat bot,
                    // and the user is changing its category, the bot learns!
                    if (oldTx.source === 'chat' && oldTx.categoryId !== categoryId) {
                        learnFromCorrection(oldTx.description, categoryId, type);
                    }

                    appState.transactions[index] = {
                        ...oldTx, description: desc, amount, date, categoryId, type
                    };
                }
            } else {
                // Add new
                if (isInstallment) {
                    const parts = parseInt(document.getElementById('tx-installments').value);
                    if(parts > 1) {
                        const installmentAmount = amount / parts;
                        const groupId = generateId();
                        for(let i=0; i<parts; i++) {
                            const instDate = addMonthsToDateStr(date, i);
                            appState.transactions.push({
                                id: generateId(),
                                description: desc,
                                amount: installmentAmount,
                                date: instDate,
                                categoryId,
                                type,
                                source,
                                installmentInfo: `${i+1}/${parts}`,
                                groupId
                            });
                        }
                    } else {
                        appState.transactions.push({ id: generateId(), description: desc, amount, date, categoryId, type, source });
                    }
                } else {
                    appState.transactions.push({ id: generateId(), description: desc, amount, date, categoryId, type, source });
                }
            }

            saveData();
            closeModal('modal-transaction');
            showMessage('Sucesso', 'Transação salva com sucesso.');
        }

        function editTransaction(id) {
            const tx = appState.transactions.find(t => t.id === id);
            if(!tx) return;

            document.getElementById('tx-id').value = tx.id;
            document.getElementById('tx-source').value = tx.source || 'manual';
            document.getElementById('tx-desc').value = tx.description;
            document.getElementById('tx-amount').value = tx.amount;
            document.getElementById('tx-date').value = tx.date;
            
            setTxType(tx.type);
            document.getElementById('tx-category').value = tx.categoryId;
            
            document.getElementById('modal-tx-title').innerText = 'Editar Transação';
            document.getElementById('installments-container').classList.add('hidden'); // disable converting to installment on edit
            document.getElementById('modal-transaction').classList.remove('hidden');
        }

        function deleteTransaction(id) {
            showConfirm(() => {
                appState.transactions = appState.transactions.filter(t => t.id !== id);
                saveData();
            });
        }

        function renderCategoriesTab() {
            const grid = document.getElementById('categories-grid');
            grid.innerHTML = '';
            appState.categories.forEach(cat => {
                grid.innerHTML += `
                    <div class="bg-white p-4 rounded-xl border border-gray-100 flex items-center justify-between shadow-sm">
                        <div class="flex items-center">
                            <div class="w-10 h-10 rounded-full flex items-center justify-center text-xl mr-3" style="background-color: ${cat.color}20; color: ${cat.color}">
                                <i class="ph ${cat.icon}"></i>
                            </div>
                            <div>
                                <h4 class="font-medium text-gray-800">${cat.name}</h4>
                                <p class="text-xs text-gray-500">${cat.type === 'expense' ? 'Saída' : 'Entrada'}</p>
                            </div>
                        </div>
                    </div>
                `;
            });
        }

        function openCategoryModal() {
            document.getElementById('cat-name').value = '';
            document.getElementById('modal-category').classList.remove('hidden');
        }

        function saveCategory() {
            const name = document.getElementById('cat-name').value;
            const type = document.getElementById('cat-type').value;
            if(!name) return;

            const icons = ['ph-bag', 'ph-airplane', 'ph-book', 'ph-game-controller', 'ph-t-shirt', 'ph-wrench'];
            const colors = ['#f43f5e', '#a855f7', '#0ea5e9', '#84cc16', '#f97316', '#64748b'];
            
            const rnd = Math.floor(Math.random() * icons.length);

            appState.categories.push({
                id: generateId(),
                name,
                type,
                icon: icons[rnd],
                color: colors[rnd]
            });

            saveData();
            renderCategoriesTab();
            closeModal('modal-category');
            showMessage('Sucesso', 'Categoria adicionada.');
        }

        function renderBudgets() {
            const list = document.getElementById('budget-list');
            list.innerHTML = '';
            
            const expCategories = appState.categories.filter(c => c.type === 'expense');
            
            expCategories.forEach(cat => {
                const currentVal = appState.budgets[cat.id] || 0;
                list.innerHTML += `
                    <div class="flex items-center justify-between">
                        <div class="flex items-center w-1/2">
                            <i class="ph ${cat.icon} text-lg mr-2" style="color: ${cat.color}"></i>
                            <span class="text-sm font-medium text-gray-700">${cat.name}</span>
                        </div>
                        <div class="w-1/2 flex items-center bg-gray-50 rounded-lg px-3 border border-gray-200">
                            <span class="text-gray-500 text-sm mr-1">R$</span>
                            <input type="number" step="10" id="budget_input_${cat.id}" value="${currentVal}" class="w-full bg-transparent border-none py-2 text-right focus:ring-0 outline-none font-medium text-gray-800">
                        </div>
                    </div>
                `;
            });
        }

        function saveBudgets() {
            const expCategories = appState.categories.filter(c => c.type === 'expense');
            expCategories.forEach(cat => {
                const val = parseFloat(document.getElementById(`budget_input_${cat.id}`).value) || 0;
                appState.budgets[cat.id] = val;
            });
            saveData();
            showMessage('Limites Atualizados', 'Seus limites de orçamento foram salvos.');
        }

        // --------------------------------------------------------
        // NLP & Chatbot Logic
        // --------------------------------------------------------

        function handleChatKeyPress(e) {
            if(e.key === 'Enter') sendChatMessage();
        }

        function appendMessage(text, isUser) {
            const chatArea = document.getElementById('chat-messages');
            const time = new Date().toLocaleTimeString('pt-BR', {hour: '2-digit', minute:'2-digit'});
            
            if(isUser) {
                chatArea.innerHTML += `
                    <div class="flex justify-end mb-4">
                        <div class="bg-[#dcf8c6] text-gray-800 p-3 rounded-xl rounded-tr-none msg-bubble shadow-sm text-sm">
                            ${text}
                            <span class="block text-right text-[10px] text-gray-500 mt-1">${time}</span>
                        </div>
                    </div>
                `;
            } else {
                chatArea.innerHTML += `
                    <div class="flex justify-start mb-4">
                        <div class="bg-white text-gray-800 p-3 rounded-xl rounded-tl-none msg-bubble shadow-sm text-sm">
                            ${text}
                            <span class="block text-right text-[10px] text-gray-400 mt-1">${time}</span>
                        </div>
                    </div>
                `;
            }
            chatArea.scrollTop = chatArea.scrollHeight;
        }

        function processNLP(message) {
            const lowerMsg = message.toLowerCase();
            
            // 1. Extract Value
            // Matches numbers like 50, 50.00, 50,00, 1.500,00, R$ 50
            const valueMatch = lowerMsg.match(/(?:r\$)?\s?(\d+(?:\.\d{3})*(?:,\d{2})?|\d+(?:,\d{2})?|\d+(?:\.\d{2})?)/);
            
            if(!valueMatch) {
                return "Desculpe, não consegui identificar o valor. Tente digitar algo como 'Mercado 150' ou 'Conta de Luz R$ 80,50'.";
            }

            // Parse Value string to float
            let valStr = valueMatch[1].replace(/\./g, '').replace(',', '.');
            let amount = parseFloat(valStr);

            if(amount <= 0) return "O valor precisa ser maior que zero.";

            // 2. Extract Description (remove value part)
            let desc = message.replace(valueMatch[0], '').trim();
            if(desc.length === 0) desc = "Lançamento via Chat";

            // 3. Category Inference (The 'Learning' brain)
            let categoryId = null;
            
            // Sort keywords by length descending to match composite words first
            const keywords = Object.keys(appState.keywordDict).sort((a,b) => b.length - a.length);
            
            for(let kw of keywords) {
                if(lowerMsg.includes(kw)) {
                    categoryId = appState.keywordDict[kw];
                    break;
                }
            }

            // Fallbacks if no match
            let isIncome = lowerMsg.includes('recebi') || lowerMsg.includes('salario') || lowerMsg.includes('venda') || lowerMsg.includes('pagamento');
            let type = isIncome ? 'income' : 'expense';
            
            if(!categoryId) {
                if(isIncome) {
                    categoryId = appState.categories.find(c => c.type === 'income')?.id;
                } else {
                    categoryId = 'cat_7'; // Default to "Outros"
                }
            } else {
                // Get type from category
                type = getCategory(categoryId).type;
            }

            // 4. Save the transaction
            const todayStr = new Date().toISOString().split('T')[0]; // Using today's actual date for chat imports
            
            appState.transactions.push({
                id: generateId(),
                description: desc.charAt(0).toUpperCase() + desc.slice(1),
                amount: amount,
                date: todayStr,
                categoryId: categoryId,
                type: type,
                source: 'chat' // Flag to allow learning upon correction
            });

            saveData();
            
            const catObj = getCategory(categoryId);
            return `✅ Adicionado com sucesso!\n\n<b>${desc}</b>\nValor: R$ ${amount.toFixed(2).replace('.',',')}\nCategoria: ${catObj.name}\n\n<i>Se a categoria estiver incorreta, basta editar na aba Histórico que eu aprenderei para a próxima vez!</i>`;
        }

        function sendChatMessage() {
            const input = document.getElementById('chat-input');
            const text = input.value.trim();
            if(!text) return;

            // User message
            appendMessage(text, true);
            input.value = '';

            // Bot 'typing' simulation
            setTimeout(() => {
                const response = processNLP(text);
                appendMessage(response, false);
            }, 800);
        }

        function learnFromCorrection(description, newCategoryId, newType) {
            // Take the first main word of the description to map
            let words = description.toLowerCase().split(/\s+/).filter(w => w.length > 2);
            if(words.length > 0) {
                // Map the longest word or the first substantive
                let keyword = words[0]; 
                appState.keywordDict[keyword] = newCategoryId;
                console.log(`Bot learned: '${keyword}' is now mapped to ${newCategoryId}`);
                
                // Show a nice non-intrusive toast notification
                const toast = document.createElement('div');
                toast.className = 'fixed top-4 left-1/2 transform -translate-x-1/2 bg-gray-800 text-white px-4 py-2 rounded-full shadow-lg z-50 text-sm flex items-center animate-fade-in-down';
                toast.innerHTML = `<i class="ph-fill ph-robot text-emerald-400 mr-2 text-lg"></i> Aprendi que "${keyword}" é ${getCategory(newCategoryId).name}!`;
                document.body.appendChild(toast);
                setTimeout(() => {
                    toast.style.opacity = '0';
                    toast.style.transition = 'opacity 0.5s ease';
                    setTimeout(() => toast.remove(), 500);
                }, 4000);
            }
        }

        // Add small keyframe for toast
        const style = document.createElement('style');
        style.innerHTML = `
            @keyframes fadeInDown {
                0% { opacity: 0; transform: translate(-50%, -20px); }
                100% { opacity: 1; transform: translate(-50%, 0); }
            }
            .animate-fade-in-down { animation: fadeInDown 0.3s ease-out forwards; }
        `;
        document.head.appendChild(style);

        // Start App
        window.onload = initApp;

    </script>
</body>
</html>


