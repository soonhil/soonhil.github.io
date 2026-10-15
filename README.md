
<html lang="ru" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Веб-визитка</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts Inter -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    
    <script>
        // Конфигурация Tailwind для кастомных градиентов и тёмной темы
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                    },
                    colors: {
                        brand: {
                            50: '#f0f7ff',
                            500: '#3b82f6',
                            600: '#2563eb',
                            700: '#1d4ed8',
                        }
                    }
                }
            }
        }
    </script>

    <style>
        /* Дополнительные пользовательские стили и анимации */
        .glass {
            background: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(16px);
            -webkit-backdrop-filter: blur(16px);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .light .glass {
            background: rgba(255, 255, 255, 0.7);
            border: 1px solid rgba(0, 0, 0, 0.08);
        }

        .gradient-text {
            background: linear-gradient(135deg, #60a5fa 0%, #a855f7 50%, #ec4899 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .gradient-bg {
            background: linear-gradient(135deg, #2563eb 0%, #7c3aed 100%);
        }

        /* Плавные переходы страниц */
        .page-section {
            display: none;
            opacity: 0;
            transform: translateY(12px);
            transition: opacity 0.3s ease, transform 0.3s ease;
        }

        .page-section.active {
            display: block;
            opacity: 1;
            transform: translateY(0);
        }

        /* Кастомный скроллбар */
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: rgba(15, 23, 42, 0.6);
        }
        ::-webkit-scrollbar-thumb {
            background: #334155;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #475569;
        }
    </style>
</head>
<body class="bg-slate-950 text-slate-100 min-h-screen font-sans antialiased transition-colors duration-300 light:bg-slate-50 light:text-slate-900 selection:bg-purple-500 selection:text-white flex flex-col justify-between">

    <!-- ФОНОВЫЕ ЭФФЕКТЫ (Вайб свечение) -->
    <div class="fixed inset-0 pointer-events-none overflow-hidden z-0">
        <div class="absolute -top-40 -left-40 w-96 h-96 bg-blue-600/20 rounded-full blur-3xl"></div>
        <div class="absolute top-1/3 -right-40 w-96 h-96 bg-purple-600/20 rounded-full blur-3xl"></div>
        <div class="absolute -bottom-40 left-1/3 w-96 h-96 bg-pink-600/20 rounded-full blur-3xl"></div>
    </div>

    <!-- ШАПКА / НАВИГАЦИЯ -->
    <header class="sticky top-0 z-40 w-full glass border-b border-slate-800/50 light:border-slate-200/80">
        <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 h-20 flex items-center justify-between">
            
            <!-- Логотип -->
            <a href="#home" onclick="navigateTo('home')" class="flex items-center gap-3 group">
                <div class="w-10 h-10 rounded-xl gradient-bg flex items-center justify-center text-white font-bold text-xl shadow-lg shadow-blue-500/20 group-hover:scale-105 transition-transform">
                    АВ
                </div>
                <div class="flex flex-col">
                    <span class="font-bold text-lg tracking-tight leading-none group-hover:text-blue-400 transition-colors">Суон Хилк</span>
                    <span class="text-xs text-slate-400 font-medium mt-1">Практический Философ</span>
                </div>
            </a>

            <!-- Десктоп Меню -->
            <nav class="hidden md:flex items-center gap-1 bg-slate-900/60 light:bg-slate-200/60 p-1.5 rounded-full border border-slate-800 light:border-slate-300">
                <button onclick="navigateTo('home')" id="nav-home" class="nav-btn px-5 py-2 rounded-full text-sm font-medium transition-all text-blue-400 bg-slate-800/80 light:bg-white light:shadow-sm">
                    <i class="fa-solid fa-house mr-2"></i>Главная
                </button>
                <button onclick="navigateTo('about')" id="nav-about" class="nav-btn px-5 py-2 rounded-full text-sm font-medium text-slate-400 hover:text-slate-200 transition-all">
                    <i class="fa-solid fa-user mr-2"></i>О себе
                </button>
                <button onclick="navigateTo('projects')" id="nav-projects" class="nav-btn px-5 py-2 rounded-full text-sm font-medium text-slate-400 hover:text-slate-200 transition-all">
                    <i class="fa-solid fa-briefcase mr-2"></i>Проекты
                </button>
                <button onclick="navigateTo('contact')" id="nav-contact" class="nav-btn px-5 py-2 rounded-full text-sm font-medium text-slate-400 hover:text-slate-200 transition-all">
                    <i class="fa-solid fa-envelope mr-2"></i>Контакты
                </button>
            </nav>

            <!-- Действия справа -->
            <div class="flex items-center gap-3">
                <!-- Переключатель темы -->
                <button id="theme-toggle" class="w-10 h-10 rounded-xl glass flex items-center justify-center text-slate-300 hover:text-white hover:border-slate-700 transition-all" title="Сменить тему">
                    <i class="fa-solid fa-moon text-lg" id="theme-icon"></i>
                </button>

                <!-- Кнопка Инспектора кода -->
                <button onclick="openInspectorModal()" class="hidden sm:flex items-center gap-2 px-3.5 py-2 rounded-xl text-xs font-mono bg-purple-950/40 text-purple-300 border border-purple-800/50 hover:bg-purple-900/50 transition-all">
                    <i class="fa-solid fa-code"></i>
                    <span>Код страницы</span>
                </button>

                <!-- Мобильная кнопка меню -->
                <button onclick="toggleMobileMenu()" class="md:hidden w-10 h-10 rounded-xl glass flex items-center justify-center text-slate-300">
                    <i class="fa-solid fa-bars text-xl" id="menu-icon"></i>
                </button>
            </div>
        </div>

        <!-- МОБИЛЬНОЕ ВЫПИСНОЕ МЕНЮ -->
        <div id="mobile-menu" class="hidden md:hidden border-b border-slate-800 bg-slate-950/95 backdrop-blur-xl px-4 py-4 space-y-2">
            <button onclick="navigateTo('home'); toggleMobileMenu();" class="mobile-nav-btn w-full text-left px-4 py-3 rounded-xl font-medium text-slate-200 flex items-center gap-3 bg-slate-900">
                <i class="fa-solid fa-house w-5 text-blue-400"></i>Главная
            </button>
            <button onclick="navigateTo('about'); toggleMobileMenu();" class="mobile-nav-btn w-full text-left px-4 py-3 rounded-xl font-medium text-slate-400 flex items-center gap-3">
                <i class="fa-solid fa-user w-5 text-purple-400"></i>О себе & Навыки
            </button>
            <button onclick="navigateTo('projects'); toggleMobileMenu();" class="mobile-nav-btn w-full text-left px-4 py-3 rounded-xl font-medium text-slate-400 flex items-center gap-3">
                <i class="fa-solid fa-briefcase w-5 text-emerald-400"></i>Проекты
            </button>
            <button onclick="navigateTo('contact'); toggleMobileMenu();" class="mobile-nav-btn w-full text-left px-4 py-3 rounded-xl font-medium text-slate-400 flex items-center gap-3">
                <i class="fa-solid fa-envelope w-5 text-pink-400"></i>Контакты
            </button>
            <div class="pt-2">
                <button onclick="openInspectorModal(); toggleMobileMenu();" class="w-full flex items-center justify-center gap-2 px-4 py-2.5 rounded-xl text-xs font-mono bg-purple-950/50 text-purple-300 border border-purple-800/50">
                    <i class="fa-solid fa-code"></i>
                    <span>Как это устроено (Код)</span>
                </button>
            </div>
        </div>
    </header>

    <!-- ОСНОВНОЙ КОНТЕНТ (СТРАНИЦЫ) -->
    <main class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 py-10 relative z-10 flex-grow w-full">

        <!-- ================= СТРАНИЦА 1: ГЛАВНАЯ ================= -->
        <section id="page-home" class="page-section active">
            <div class="grid grid-cols-1 lg:grid-cols-12 gap-12 items-center min-h-[70vh]">
                
                <!-- Левый блок - Текст -->
                <div class="lg:col-span-7 space-y-6">
                    <div class="inline-flex items-center gap-2 px-3.5 py-1.5 rounded-full glass border border-blue-500/30 text-blue-400 text-xs font-semibold tracking-wide">
                        <span class="w-2 h-2 rounded-full bg-emerald-400 animate-pulse"></span>
                        Наконец-то я разобрался как сделать этот дашборд
                    </div>

                    <h1 class="text-4xl sm:text-6xl font-extrabold tracking-tight leading-tight">
                        Работаю над этой <span class="gradient-text">веб-визиткой</span>
                    </h1>

                    <p class="text-slate-400 text-lg sm:text-xl leading-relaxed max-w-2xl font-light">
                        Привет! Я оператор ПК, Промо консультантант и Практический Философ на пол ставки.
                    </p>

                    <!-- Кнопки действий -->
                    <div class="flex flex-wrap items-center gap-4 pt-2">
                        <button onclick="navigateTo('projects')" class="px-7 py-3.5 rounded-2xl gradient-bg font-semibold text-white shadow-lg shadow-blue-500/25 hover:shadow-blue-500/40 hover:scale-105 transition-all flex items-center gap-2">
                            <span>Смотреть работы</span>
                            <i class="fa-solid fa-arrow-right text-sm"></i>
                        </button>
                        <button onclick="navigateTo('contact')" class="px-7 py-3.5 rounded-2xl glass font-semibold text-slate-200 hover:bg-slate-800/80 hover:border-slate-600 transition-all">
                            Связаться со мной
                        </button>
                    </div>

                    <!-- Быстрая статистика -->
                    <div class="grid grid-cols-3 gap-4 pt-8 border-t border-slate-800/80">
                        <div>
                            <p class="text-3xl font-extrabold text-slate-100">15+</p>
                            <p class="text-xs text-slate-400 mt-1">Философских проектов</p>
                        </div>
                        <div>
                            <p class="text-3xl font-extrabold text-slate-100">2+ года</p>
                            <p class="text-xs text-slate-400 mt-1">Опыта в накрутка опыта</p>
                        </div>
                        <div>
                            <p class="text-3xl font-extrabold text-slate-100">100%</p>
                            <p class="text-xs text-slate-400 mt-1">Адаптивность</p>
                        </div>
                    </div>
                </div>

                <!-- Правый блок - Аватар / Карточка -->
                <div class="lg:col-span-5 flex justify-center">
                    <div class="relative w-full max-w-sm">
                        <div class="absolute inset-0 gradient-bg rounded-3xl blur-2xl opacity-40 animate-pulse"></div>
                        <div class="relative glass p-6 rounded-3xl border border-slate-700/50 space-y-6">
                            <div class="relative h-72 rounded-2xl overflow-hidden group">
                                <img src="https://images.лллcom/photo-1534528741775-53994a69daeb?auto=format&fit=crop&w=800&q=80" 
                                     alt="Суон Хилк" 
                                     class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-500"
                                     onerror="this.src='https://placehold.co/600x600/1e293b/ffffff?text=Аватар'">
                                <div class="absolute inset-0 bg-gradient-to-t from-slate-950 via-transparent to-transparent opacity-80"></div>
                                <div class="absolute bottom-4 left-4 right-4">
                                    <p class="text-lg font-bold text-white">Нищий Софист</p>
                                    <p class="text-xs text-slate-300">Амбициозный парень</p>
                                </div>
                            </div>

                            <!-- Быстрые соцсети -->
                            <div class="flex items-center justify-between pt-2">
                                <span class="text-xs text-slate-400 uppercase tracking-wider font-semibold">Быстрая связь:</span>
                                <div class="flex items-center gap-3">
                                    <a href="https://t.me/soonhil" target="_blank" class="w-9 h-9 rounded-xl glass flex items-center justify-center text-slate-300 hover:text-blue-400 hover:scale-110 transition-all">
                                        <i class="fa-brands fa-telegram"></i>
                                    </a>
                                    <a href="https://github.com/suonhilk" target="_blank" class="w-9 h-9 rounded-xl glass flex items-center justify-center text-slate-300 hover:text-purple-400 hover:scale-110 transition-all">
                                        <i class="fa-brands fa-github"></i>
                                    </a>
                                    <a href="https://vk.com" target="_blank" class="w-9 h-9 rounded-xl glass flex items-center justify-center text-slate-300 hover:text-blue-500 hover:scale-110 transition-all">
                                        <i class="fa-brands fa-vk"></i>
                                    </a>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

            </div>
        </section>

        <!-- ================= СТРАНИЦА 2: О СЕБЕ И НАВЫКИ ================= -->
        <section id="page-about" class="page-section space-y-12">
            <div class="text-center max-w-2xl mx-auto space-y-3">
                <h2 class="text-3xl sm:text-4xl font-extrabold">Обо мне & <span class="gradient-text">Навыки</span></h2>
                <p class="text-slate-400">бла была бла</p>
            </div>

            <!-- Биография и история -->
            <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
                <div class="glass p-8 rounded-3xl space-y-4 border border-slate-800">
                    <div class="w-12 h-12 rounded-2xl bg-blue-500/10 text-blue-400 flex items-center justify-center text-2xl font-bold">
                        <i class="fa-solid fa-user-astronaut"></i>
                    </div>
                    <h3 class="text-xl font-bold">Кто я такой?</h3>
                    <p class="text-slate-300 leading-relaxed text-sm">
                        бла бла бла что-то там про философию
                    </p>
                    <p class="text-slate-400 leading-relaxed text-sm">
                        что-то там это и что-то, что-то это
                    </p>
                </div>

                <div class="glass p-8 rounded-3xl space-y-6 border border-slate-800">
                    <h3 class="text-xl font-bold flex items-center gap-2">
                        <i class="fa-solid fa-graduation-cap text-purple-400"></i>
                        Мой путь
                    </h3>

                    <div class="space-y-6 relative border-l border-slate-800 pl-6">
                        <div class="relative">
                            <span class="absolute -left-[31px] top-1 w-3.5 h-3.5 rounded-full bg-blue-500 ring-4 ring-slate-950"></span>
                            <span class="text-xs font-mono text-blue-400">2024 — Настоящее время</span>
                            <h4 class="font-semibold text-slate-200">Freelance & Web Development</h4>
                            <p class="text-xs text-slate-400 mt-1">Лидогенерация, Оперирование ПК, Ведение дебатов</p>
                        </div>
                        <div class="relative">
                            <span class="absolute -left-[31px] top-1 w-3.5 h-3.5 rounded-full bg-purple-500 ring-4 ring-slate-950"></span>
                            <span class="text-xs font-mono text-purple-400">2023 — 2024</span>
                            <h4 class="font-semibold text-slate-200">что-то там номер 3</h4>
                            <p class="text-xs text-slate-400 mt-1">Что-то про навыки</p>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Блок Навыков -->
            <div class="glass p-8 rounded-3xl border border-slate-800 space-y-6">
                <h3 class="text-2xl font-bold">Всё технологично</h3>

                <div class="grid grid-cols-1 sm:grid-cols-2 gap-6">
                    <!-- Навык 1 -->
                    <div class="space-y-2">
                        <div class="flex justify-between text-sm font-medium">
                            <span class="flex items-center gap-2"><i class="fa-brands fa-html5 text-orange-500"></i> HTML5 & Семантика</span>
                            <span class="text-blue-400 font-mono">95%</span>
                        </div>
                        <div class="w-full bg-slate-800 h-2.5 rounded-full overflow-hidden">
                            <div class="bg-gradient-to-r from-orange-500 to-amber-400 h-full rounded-full" style="width: 95%"></div>
                        </div>
                    </div>

                    <!-- Навык 2 -->
                    <div class="space-y-2">
                        <div class="flex justify-between text-sm font-medium">
                            <span class="flex items-center gap-2"><i class="fa-brands fa-css3-alt text-blue-500"></i> CSS3 & Tailwind CSS</span>
                            <span class="text-blue-400 font-mono">90%</span>
                        </div>
                        <div class="w-full bg-slate-800 h-2.5 rounded-full overflow-hidden">
                            <div class="bg-gradient-to-r from-blue-500 to-cyan-400 h-full rounded-full" style="width: 90%"></div>
                        </div>
                    </div>

                    <!-- Навык 3 -->
                    <div class="space-y-2">
                        <div class="flex justify-between text-sm font-medium">
                            <span class="flex items-center gap-2"><i class="fa-brands fa-js text-yellow-400"></i> JavaScript (ES6+)</span>
                            <span class="text-blue-400 font-mono">80%</span>
                        </div>
                        <div class="w-full bg-slate-800 h-2.5 rounded-full overflow-hidden">
                            <div class="bg-gradient-to-r from-yellow-400 to-ambe# me
