<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KAISHI - Belajar Bilangan</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700&display=swap');
        
        body {
            font-family: 'Poppins', sans-serif;
            background: linear-gradient(135deg, #4f46e5, #7e22ce, #c026d3);
            min-height: 100vh;
            color: #333;
        }
        .draggable {
            cursor: grab;
            transition: transform 0.2s, box-shadow 0.2s;
            background: linear-gradient(to bottom right, #ffffff, #f3f4f6);
        }
        .draggable:active {
            cursor: grabbing;
            transform: scale(1.05);
        }
        .draggable.dragging {
            opacity: 0.8;
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.3);
        }
        .basket {
            transition: all 0.3s;
            min-height: 150px;
            border-width: 2px;
            border-style: dashed;
        }
        .basket.drag-over {
            transform: scale(1.03);
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.2);
        }
        .item-container {
            min-height: 100px;
        }
        @keyframes celebrate {
            0% { transform: scale(1); }
            50% { transform: scale(1.2); }
            100% { transform: scale(1); }
        }
        .celebrate {
            animation: celebrate 0.5s ease;
        }
        .progress-bar {
            transition: width 0.5s ease;
        }
        .game-container {
            background: linear-gradient(to bottom, #ffffff, #f9fafb);
            box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25);
        }
        .header-gradient {
            background: linear-gradient(135deg, #3b82f6, #6366f1, #8b5cf6);
        }
        .difficulty-btn {
            transition: all 0.3s ease;
        }
        .difficulty-btn.active {
            transform: scale(1.05);
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.2);
        }
        .decimal-basket {
            background: linear-gradient(145deg, #e0f2fe, #bae6fd);
            border-color: #38bdf8;
        }
        .integer-basket {
            background: linear-gradient(145deg, #dcfce7, #bbf7d0);
            border-color: #22c55e;
        }
        .fraction-basket {
            background: linear-gradient(145deg, #f3e8ff, #e9d5ff);
            border-color: #a855f7;
        }
        .btn-primary {
            background: linear-gradient(to right, #3b82f6, #6366f1);
            transition: all 0.3s ease;
        }
        .btn-primary:hover {
            background: linear-gradient(to right, #2563eb, #4f46e5);
            transform: translateY(-2px);
            box-shadow: 0 10px 15px -3px rgba(59, 130, 246, 0.3);
        }
        .btn-secondary {
            background: linear-gradient(to right, #64748b, #475569);
            transition: all 0.3s ease;
        }
        .btn-secondary:hover {
            background: linear-gradient(to right, #475569, #334155);
            transform: translateY(-2px);
            box-shadow: 0 10px 15px -3px rgba(71, 85, 105, 0.3);
        }
        .logo {
            font-weight: 800;
            background: linear-gradient(to right, #f9fafb, #ffffff);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            letter-spacing: 2px;
        }
        .info-card {
            background: linear-gradient(to bottom right, rgba(255, 255, 255, 0.9), rgba(249, 250, 251, 0.9));
            backdrop-filter: blur(10px);
            border-radius: 12px;
            box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.1);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }
        .info-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.2);
        }
        .footer {
            background: linear-gradient(to right, rgba(30, 41, 59, 0.95), rgba(15, 23, 42, 0.95));
            backdrop-filter: blur(10px);
        }
        .tab-active {
            background: linear-gradient(to right, #3b82f6, #6366f1);
            color: white;
        }
    </style>
</head>
<body class="p-4 md:p-8">
    <!-- Main Header -->
    <header class="max-w-6xl mx-auto mb-8 text-white">
        <div class="flex flex-col md:flex-row justify-between items-center p-6 rounded-xl header-gradient shadow-lg">
            <div class="mb-4 md:mb-0">
                <h1 class="text-4xl md:text-5xl logo">KAISHI</h1>
                <p class="text-blue-100 mt-1">Platform Belajar Matematika Interaktif</p>
            </div>
            <div class="text-center md:text-right">
                <h2 class="text-xl md:text-2xl font-semibold">Selamat Datang!</h2>
                <p class="text-blue-100">Mari Belajar Bilangan Desimal & Pecahan</p>
            </div>
        </div>
    </header>

    <!-- Info Tabs -->
    <div class="max-w-6xl mx-auto mb-8">
        <div class="bg-white bg-opacity-90 rounded-xl shadow-lg overflow-hidden">
            <div class="flex border-b">
                <button id="info-tab" class="flex-1 py-3 px-4 text-center font-medium tab-active">Informasi Bilangan</button>
                <button id="game-tab" class="flex-1 py-3 px-4 text-center font-medium text-gray-700 hover:bg-gray-100 transition-colors">Game Pengelompokan</button>
            </div>
            
            <!-- Info Content -->
            <div id="info-content" class="p-6">
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <!-- Bilangan Desimal -->
                    <div class="info-card p-5">
                        <div class="flex items-center mb-4">
                            <div class="w-12 h-12 rounded-full flex items-center justify-center mr-4" style="background: linear-gradient(135deg, #38bdf8, #0ea5e9);">
                                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 20l4-16m2 16l4-16M6 9h14M4 15h14" />
                                </svg>
                            </div>
                            <h3 class="text-xl font-bold text-blue-600">Bilangan Desimal</h3>
                        </div>
                        <p class="text-gray-700 mb-3">
                            Bilangan desimal adalah bilangan yang memiliki bagian pecahan yang ditandai dengan tanda koma (,) atau titik (.) sebagai pemisah.
                        </p>
                        <p class="text-gray-700 mb-3">
                            Contoh bilangan desimal: 0,5 (nol koma lima), 3,14 (tiga koma satu empat), 2,718 (dua koma tujuh satu delapan).
                        </p>
                        <p class="text-gray-700">
                            Bilangan desimal digunakan untuk mewakili nilai yang tidak dapat dinyatakan sebagai bilangan bulat, seperti hasil pengukuran atau perhitungan yang memerlukan ketelitian.
                        </p>
                    </div>
                    
                    <!-- Bilangan Pecahan -->
                    <div class="info-card p-5">
                        <div class="flex items-center mb-4">
                            <div class="w-12 h-12 rounded-full flex items-center justify-center mr-4" style="background: linear-gradient(135deg, #a855f7, #8b5cf6);">
                                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 15l7-7 7 7" />
                                </svg>
                            </div>
                            <h3 class="text-xl font-bold text-purple-600">Bilangan Pecahan</h3>
                        </div>
                        <p class="text-gray-700 mb-3">
                            Bilangan pecahan adalah bilangan yang terdiri dari pembilang dan penyebut yang dipisahkan oleh garis pecahan.
                        </p>
                        <p class="text-gray-700 mb-3">
                            Contoh bilangan pecahan: 1/2 (satu per dua), 3/4 (tiga per empat), 5/8 (lima per delapan).
                        </p>
                        <p class="text-gray-700">
                            Bilangan pecahan menyatakan bagian dari keseluruhan. Pembilang menunjukkan berapa bagian yang diambil, sedangkan penyebut menunjukkan keseluruhan bagian.
                        </p>
                    </div>
                    
                    <!-- Bilangan Bulat -->
                    <div class="info-card p-5">
                        <div class="flex items-center mb-4">
                            <div class="w-12 h-12 rounded-full flex items-center justify-center mr-4" style="background: linear-gradient(135deg, #22c55e, #16a34a);">
                                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 7h6m0 10v-3m-3 3h.01M9 17h.01M9 14h.01M12 14h.01M15 11h.01M12 11h.01M9 11h.01M7 21h10a2 2 0 002-2V5a2 2 0 00-2-2H7a2 2 0 00-2 2v14a2 2 0 002 2z" />
                                </svg>
                            </div>
                            <h3 class="text-xl font-bold text-green-600">Bilangan Bulat</h3>
                        </div>
                        <p class="text-gray-700 mb-3">
                            Bilangan bulat adalah bilangan tanpa bagian pecahan atau desimal, termasuk bilangan negatif, nol, dan positif.
                        </p>
                        <p class="text-gray-700 mb-3">
                            Contoh bilangan bulat: -5, 0, 42, 100, -273.
                        </p>
                        <p class="text-gray-700">
                            Bilangan bulat digunakan untuk menyatakan kuantitas utuh, seperti jumlah benda, urutan, atau posisi relatif terhadap titik referensi.
                        </p>
                    </div>
                    
                    <!-- Hubungan Antar Bilangan -->
                    <div class="info-card p-5">
                        <div class="flex items-center mb-4">
                            <div class="w-12 h-12 rounded-full flex items-center justify-center mr-4" style="background: linear-gradient(135deg, #f97316, #ea580c);">
                                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7h12m0 0l-4-4m4 4l-4 4m0 6H4m0 0l4 4m-4-4l4-4" />
                                </svg>
                            </div>
                            <h3 class="text-xl font-bold text-orange-600">Hubungan Antar Bilangan</h3>
                        </div>
                        <p class="text-gray-700 mb-3">
                            Bilangan pecahan dapat diubah menjadi bilangan desimal dengan cara membagi pembilang dengan penyebut.
                        </p>
                        <p class="text-gray-700 mb-3">
                            Contoh: 1/2 = 0,5 | 3/4 = 0,75 | 2/5 = 0,4
                        </p>
                        <p class="text-gray-700">
                            Sebaliknya, bilangan desimal dapat diubah menjadi pecahan dengan menentukan pembilang dan penyebut yang sesuai, lalu disederhanakan jika memungkinkan.
                        </p>
                    </div>
                </div>
                
                <div class="mt-6 text-center">
                    <button id="start-game-btn" class="btn-primary px-8 py-3 text-white font-medium rounded-lg text-lg">
                        Mulai Game Pengelompokan
                    </button>
                </div>
            </div>
            
            <!-- Game Content -->
            <div id="game-content" class="hidden">
                <!-- Game Area -->
                <div class="game-container">
                    <!-- Difficulty Selection -->
                    <div class="p-4 bg-gradient-to-r from-indigo-50 to-purple-50">
                        <h2 class="text-center font-semibold text-gray-700 mb-3">Pilih Tingkat Kesulitan:</h2>
                        <div class="flex justify-center gap-3">
                            <button class="difficulty-btn px-5 py-2 rounded-full text-white font-medium active" data-level="easy" 
                                style="background: linear-gradient(to right, #4ade80, #22c55e);">
                                Mudah
                            </button>
                            <button class="difficulty-btn px-5 py-2 rounded-full text-white font-medium" data-level="medium"
                                style="background: linear-gradient(to right, #fb923c, #f97316);">
                                Sedang
                            </button>
                            <button class="difficulty-btn px-5 py-2 rounded-full text-white font-medium" data-level="hard"
                                style="background: linear-gradient(to right, #f87171, #ef4444);">
                                Sulit
                            </button>
                        </div>
                    </div>

                    <!-- Progress Bar -->
                    <div class="px-6 pt-4">
                        <div class="flex items-center justify-between mb-2">
                            <span class="text-sm font-medium text-gray-700">Progres:</span>
                            <span id="progress-text" class="text-sm font-medium text-gray-700">0%</span>
                        </div>
                        <div class="w-full bg-gray-200 rounded-full h-2.5">
                            <div id="progress-bar" class="progress-bar bg-gradient-to-r from-blue-400 via-purple-500 to-pink-500 h-2.5 rounded-full" style="width: 0%"></div>
                        </div>
                    </div>

                    <!-- Game Area -->
                    <div class="p-6">
                        <!-- Items to sort -->
                        <div class="item-container p-4 bg-gradient-to-r from-gray-100 to-gray-50 rounded-lg mb-6 flex flex-wrap justify-center gap-3" id="items-container">
                            <!-- Items will be generated here -->
                        </div>

                        <!-- Baskets -->
                        <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                            <div class="basket decimal-basket p-4 rounded-lg" data-type="decimal">
                                <h2 class="text-center font-bold text-blue-700 mb-3">Bilangan Desimal</h2>
                                <div class="min-h-[100px] flex flex-wrap gap-2 justify-center items-start" id="decimal-basket"></div>
                            </div>
                            <div class="basket integer-basket p-4 rounded-lg" data-type="integer">
                                <h2 class="text-center font-bold text-green-700 mb-3">Bilangan Bulat</h2>
                                <div class="min-h-[100px] flex flex-wrap gap-2 justify-center items-start" id="integer-basket"></div>
                            </div>
                            <div class="basket fraction-basket p-4 rounded-lg" data-type="fraction">
                                <h2 class="text-center font-bold text-purple-700 mb-3">Bilangan Pecahan</h2>
                                <div class="min-h-[100px] flex flex-wrap gap-2 justify-center items-start" id="fraction-basket"></div>
                            </div>
                        </div>
                    </div>

                    <!-- Feedback Area -->
                    <div id="feedback" class="p-4 text-center hidden"></div>

                    <!-- Controls -->
                    <div class="p-6 bg-gradient-to-b from-gray-50 to-gray-100 flex justify-center gap-4">
                        <button id="check-btn" class="btn-primary px-6 py-2 text-white font-medium rounded-lg">
                            Periksa Jawaban
                        </button>
                        <button id="reset-btn" class="btn-secondary px-6 py-2 text-white font-medium rounded-lg">
                            Mulai Ulang
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Footer -->
    <footer class="footer max-w-6xl mx-auto rounded-xl overflow-hidden text-white">
        <div class="p-6">
            <h2 class="text-xl font-bold mb-4 text-center">Tim Pengembang</h2>
            <div class="grid grid-cols-1 md:grid-cols-3 gap-4 text-center">
                <div class="p-3">
                    <h3 class="font-medium text-lg">Muhammad Shidqi Al Ghiffari</h3>
                    <p class="text-gray-300">Pengembang</p>
                </div>
                <div class="p-3">
                    <h3 class="font-medium text-lg">Muhammad Azka Hammam</h3>
                    <p class="text-gray-300">Pengembang</p>
                </div>
                <div class="p-3">
                    <h3 class="font-medium text-lg">Muhammad Akhlis Faidlul Ulum</h3>
                    <p class="text-gray-300">Pengembang</p>
                </div>
            </div>
            <div class="mt-6 text-center text-gray-400 text-sm">
                <p>© 2025 KAISHI - Platform Belajar Matematika Interaktif</p>
            </div>
        </div>
    </footer>

    <!-- Result Modal -->
    <div id="result-modal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 hidden">
        <div class="bg-gradient-to-b from-white to-gray-50 rounded-xl p-8 max-w-md w-full mx-4 shadow-2xl">
            <div id="result-icon" class="text-6xl text-center mb-4">🎉</div>
            <h2 id="result-title" class="text-2xl font-bold text-center mb-4 bg-clip-text text-transparent bg-gradient-to-r from-blue-600 to-purple-600">Selamat!</h2>
            <p id="result-message" class="text-center mb-6">Kamu berhasil mengelompokkan semua bilangan dengan benar!</p>
            <div class="flex justify-center">
                <button id="play-again-btn" class="btn-primary px-6 py-2 text-white font-medium rounded-lg">
                    Main Lagi
                </button>
            </div>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // Tab switching
            const infoTab = document.getElementById('info-tab');
            const gameTab = document.getElementById('game-tab');
            const infoContent = document.getElementById('info-content');
            const gameContent = document.getElementById('game-content');
            const startGameBtn = document.getElementById('start-game-btn');
            
            infoTab.addEventListener('click', function() {
                infoTab.classList.add('tab-active');
                gameTab.classList.remove('tab-active');
                gameTab.classList.add('text-gray-700', 'hover:bg-gray-100');
                infoContent.classList.remove('hidden');
                gameContent.classList.add('hidden');
            });
            
            gameTab.addEventListener('click', function() {
                gameTab.classList.add('tab-active');
                gameTab.classList.remove('text-gray-700', 'hover:bg-gray-100');
                infoTab.classList.remove('tab-active');
                infoContent.classList.add('hidden');
                gameContent.classList.remove('hidden');
                initGame(); // Initialize game when switching to game tab
            });
            
            startGameBtn.addEventListener('click', function() {
                gameTab.click();
            });
            
            // Game data for different difficulty levels
            const gameLevels = {
                easy: [
                    { id: 1, value: "0.5", type: "decimal", display: "0,5" },
                    { id: 2, value: "1.75", type: "decimal", display: "1,75" },
                    { id: 3, value: "2.25", type: "decimal", display: "2,25" },
                    { id: 4, value: "5", type: "integer", display: "5" },
                    { id: 5, value: "10", type: "integer", display: "10" },
                    { id: 6, value: "0", type: "integer", display: "0" },
                    { id: 7, value: "1/2", type: "fraction", display: "1/2" },
                    { id: 8, value: "3/4", type: "fraction", display: "3/4" },
                    { id: 9, value: "1/4", type: "fraction", display: "1/4" }
                ],
                medium: [
                    { id: 1, value: "0.75", type: "decimal", display: "0,75" },
                    { id: 2, value: "1.25", type: "decimal", display: "1,25" },
                    { id: 3, value: "3.14", type: "decimal", display: "3,14" },
                    { id: 4, value: "-5", type: "integer", display: "-5" },
                    { id: 5, value: "42", type: "integer", display: "42" },
                    { id: 6, value: "-12", type: "integer", display: "-12" },
                    { id: 7, value: "5/8", type: "fraction", display: "5/8" },
                    { id: 8, value: "7/10", type: "fraction", display: "7/10" },
                    { id: 9, value: "2/3", type: "fraction", display: "2/3" },
                    { id: 10, value: "0.333", type: "decimal", display: "0,333" },
                    { id: 11, value: "100", type: "integer", display: "100" },
                    { id: 12, value: "3/5", type: "fraction", display: "3/5" }
                ],
                hard: [
                    { id: 1, value: "0.125", type: "decimal", display: "0,125" },
                    { id: 2, value: "2.718", type: "decimal", display: "2,718" },
                    { id: 3, value: "0.333...", type: "decimal", display: "0,333..." },
                    { id: 4, value: "-42", type: "integer", display: "-42" },
                    { id: 5, value: "1000", type: "integer", display: "1000" },
                    { id: 6, value: "-273", type: "integer", display: "-273" },
                    { id: 7, value: "11/12", type: "fraction", display: "11/12" },
                    { id: 8, value: "5/16", type: "fraction", display: "5/16" },
                    { id: 9, value: "7/9", type: "fraction", display: "7/9" },
                    { id: 10, value: "0.0625", type: "decimal", display: "0,0625" },
                    { id: 11, value: "-1000", type: "integer", display: "-1000" },
                    { id: 12, value: "13/15", type: "fraction", display: "13/15" },
                    { id: 13, value: "0.001", type: "decimal", display: "0,001" },
                    { id: 14, value: "999", type: "integer", display: "999" },
                    { id: 15, value: "3/17", type: "fraction", display: "3/17" }
                ]
            };

            let currentLevel = 'easy';
            let currentItems = [...gameLevels[currentLevel]];
            let correctPlacements = 0;
            let totalItems = currentItems.length;
            
            // DOM elements
            const itemsContainer = document.getElementById('items-container');
            const baskets = document.querySelectorAll('.basket');
            const checkBtn = document.getElementById('check-btn');
            const resetBtn = document.getElementById('reset-btn');
            const feedback = document.getElementById('feedback');
            const progressBar = document.getElementById('progress-bar');
            const progressText = document.getElementById('progress-text');
            const resultModal = document.getElementById('result-modal');
            const resultTitle = document.getElementById('result-title');
            const resultMessage = document.getElementById('result-message');
            const resultIcon = document.getElementById('result-icon');
            const playAgainBtn = document.getElementById('play-again-btn');
            const difficultyBtns = document.querySelectorAll('.difficulty-btn');

            // Difficulty selection
            difficultyBtns.forEach(btn => {
                btn.addEventListener('click', function() {
                    // Update active button
                    difficultyBtns.forEach(b => b.classList.remove('active'));
                    this.classList.add('active');
                    
                    // Set new difficulty level
                    currentLevel = this.getAttribute('data-level');
                    initGame();
                });
            });

            // Initialize game
            function initGame() {
                // Clear containers
                itemsContainer.innerHTML = '';
                document.getElementById('decimal-basket').innerHTML = '';
                document.getElementById('integer-basket').innerHTML = '';
                document.getElementById('fraction-basket').innerHTML = '';
                
                // Reset progress
                correctPlacements = 0;
                currentItems = [...gameLevels[currentLevel]];
                totalItems = currentItems.length;
                updateProgress();
                
                // Shuffle items
                currentItems.sort(() => Math.random() - 0.5);
                
                // Create draggable items
                currentItems.forEach(item => {
                    const itemElement = document.createElement('div');
                    itemElement.className = 'draggable px-4 py-2 rounded-lg shadow-md border border-gray-200 font-medium text-gray-800';
                    itemElement.setAttribute('draggable', 'true');
                    itemElement.setAttribute('data-id', item.id);
                    itemElement.setAttribute('data-type', item.type);
                    itemElement.textContent = item.display;
                    
                    // Add drag events
                    itemElement.addEventListener('dragstart', dragStart);
                    itemElement.addEventListener('dragend', dragEnd);
                    
                    itemsContainer.appendChild(itemElement);
                });
                
                // Hide feedback
                feedback.classList.add('hidden');
            }
            
            // Drag and drop functionality
            function dragStart(e) {
                this.classList.add('dragging');
                e.dataTransfer.setData('text/plain', this.getAttribute('data-id'));
            }
            
            function dragEnd() {
                this.classList.remove('dragging');
            }
            
            baskets.forEach(basket => {
                basket.addEventListener('dragover', e => {
                    e.preventDefault();
                    basket.classList.add('drag-over');
                });
                
                basket.addEventListener('dragleave', () => {
                    basket.classList.remove('drag-over');
                });
                
                basket.addEventListener('drop', e => {
                    e.preventDefault();
                    basket.classList.remove('drag-over');
                    
                    const itemId = e.dataTransfer.getData('text/plain');
                    const draggedItem = document.querySelector(`[data-id="${itemId}"]`);
                    
                    if (draggedItem) {
                        const basketType = basket.getAttribute('data-type');
                        const itemContainer = basket.querySelector('div');
                        
                        // Move item to basket
                        itemContainer.appendChild(draggedItem);
                        
                        // Check if correct placement
                        const itemType = draggedItem.getAttribute('data-type');
                        if (itemType === basketType) {
                            draggedItem.classList.add('bg-gradient-to-r', 'from-green-100', 'to-green-50', 'border-green-300');
                            correctPlacements++;
                            updateProgress();
                        } else {
                            draggedItem.classList.add('bg-gradient-to-r', 'from-red-100', 'to-red-50', 'border-red-300');
                        }
                    }
                });
            });
            
            // Update progress bar
            function updateProgress() {
                const percentage = Math.round((correctPlacements / totalItems) * 100);
                progressBar.style.width = `${percentage}%`;
                progressText.textContent = `${percentage}%`;
            }
            
            // Check answers
            checkBtn.addEventListener('click', () => {
                let allCorrect = true;
                let wrongPlacements = 0;
                
                baskets.forEach(basket => {
                    const basketType = basket.getAttribute('data-type');
                    const items = basket.querySelectorAll('.draggable');
                    
                    items.forEach(item => {
                        const itemType = item.getAttribute('data-type');
                        
                        if (itemType === basketType) {
                            item.classList.remove('bg-gradient-to-r', 'from-red-100', 'to-red-50', 'border-red-300');
                            item.classList.add('bg-gradient-to-r', 'from-green-100', 'to-green-50', 'border-green-300', 'celebrate');
                        } else {
                            item.classList.remove('bg-gradient-to-r', 'from-green-100', 'to-green-50', 'border-green-300');
                            item.classList.add('bg-gradient-to-r', 'from-red-100', 'to-red-50', 'border-red-300');
                            allCorrect = false;
                            wrongPlacements++;
                        }
                    });
                });
                
                // Show feedback
                feedback.classList.remove('hidden');
                
                if (allCorrect && document.querySelectorAll('.basket .draggable').length === totalItems) {
                    feedback.className = 'p-4 text-center text-green-700 bg-gradient-to-r from-green-100 to-green-50 rounded-lg';
                    feedback.textContent = 'Hebat! Semua bilangan sudah dikelompokkan dengan benar!';
                    
                    // Show success modal
                    resultTitle.textContent = 'Selamat!';
                    resultMessage.textContent = `Kamu berhasil menyelesaikan level ${getLevelName(currentLevel)}!`;
                    resultIcon.textContent = getLevelEmoji(currentLevel);
                    resultModal.classList.remove('hidden');
                } else {
                    // Calculate how many items are placed
                    const placedItems = document.querySelectorAll('.basket .draggable').length;
                    
                    if (placedItems < totalItems) {
                        feedback.className = 'p-4 text-center text-yellow-700 bg-gradient-to-r from-yellow-100 to-yellow-50 rounded-lg';
                        feedback.textContent = `Masih ada ${totalItems - placedItems} bilangan yang belum dikelompokkan.`;
                    } else {
                        feedback.className = 'p-4 text-center text-red-700 bg-gradient-to-r from-red-100 to-red-50 rounded-lg';
                        feedback.textContent = `Ada ${wrongPlacements} bilangan yang salah penempatan. Coba periksa lagi!`;
                    }
                }
            });
            
            function getLevelName(level) {
                switch(level) {
                    case 'easy': return 'Mudah';
                    case 'medium': return 'Sedang';
                    case 'hard': return 'Sulit';
                    default: return 'Mudah';
                }
            }
            
            function getLevelEmoji(level) {
                switch(level) {
                    case 'easy': return '🎉';
                    case 'medium': return '🏆';
                    case 'hard': return '🌟';
                    default: return '🎉';
                }
            }
            
            // Reset game
            resetBtn.addEventListener('click', initGame);
            
            // Play again
            playAgainBtn.addEventListener('click', () => {
                resultModal.classList.add('hidden');
                initGame();
            });
            
            // Initialize game on load
            initGame();
        });
    </script>
</body>
</html>
