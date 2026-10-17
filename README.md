<!DOCTYPE html>
<html lang="ru" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Суон Хилк — Веб-визитка</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts Inter -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                    }
                }
            }
        }
    </script>

    <style>
        /* Стиль стекла для светлой и темной темы */
        .glass {
            background: rgba(255, 255, 255, 0.85);
            backdrop-filter: blur(16px);
            -webkit-backdrop-filter: blur(16px);
            border: 1px solid rgba(0, 0, 0, 0.08);
        }
        
        .dark .glass {
            background: rgba(255, 255, 255, 0.05);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        .gradient-text {
            background: linear-gradient(135deg, #2563eb 0%, #7c3aed 50%, #db2777 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .dark .gradient-text {
            background: linear-gradient(135deg, #60a5fa 0%, #a855f7 50%, #ec4899 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .gradient-bg {
            background: linear-gradient(135deg, #2563eb 0%, #7c3aed 100%);
        }

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
    </style>
</head>
<body class="bg-slate-50 dark:bg-slate-950 text-slate-900 dark:text-slate-100 min-h-screen font-sans antialiased transition-colors duration-300 selection:bg-purple-500 selection:text-white flex flex-col justify-between">

    <!-- ФОНОВЫЕ ЭФФЕКТЫ -->
    <div class="fixed inset-0 pointer-events-none overflow-hidden z-0">
        <div class="absolute -top-40 -left-40 w-96 h-96 bg-blue-600/10 dark:bg-blue-600/20 rounded-full blur-3xl"></div>
        <div class="absolute top-1/3 -right-40 w-96 h-96 bg-purple-600/10 dark:bg-purple-600/20 rounded-full blur-3xl"></div>
        <div class="absolute -bottom-40 left-1/3 w-96 h-96 bg-pink-600/10 dark:bg-pink-600/20 rounded-full blur-3xl"></div>
    </div>

    <!-- ШАПКА / НАВИГАЦИЯ -->
    <header class="sticky top-0 z-40 w-full glass border-b border-slate-200 dark:border-slate-800/50">
        <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 h-20 flex items-center justify-between">
            
            <!-- Логотип и Имя -->
            <a href="#home" onclick="navigateTo('home')" class="flex items-center gap-3 group">
                <div class="w-10 h-10 rounded-xl gradient-bg flex items-center justify-center text-white font-bold text-xl shadow-lg shadow-blue-500/20 group-hover:scale-105 transition-transform">
                    AB
                </div>
                <div class="flex flex-col">
                    <span class="font-bold text-base tracking-tight leading-none text-slate-900 dark:text-slate-100 group-hover:text-blue-600 dark:group-hover:text-blue-400 transition-colors">Суон Хилк</span>
                    <span class="text-[11px] text-slate-500 dark:text-slate-400 font-medium mt-1">Практический Философ</span>
                </div>
            </a>

            <!-- Десктоп Меню -->
            <nav class="hidden md:flex items-center gap-1 bg-slate-200/80 dark:bg-slate-900/60 p-1.5 rounded-full border border-slate-300 dark:border-slate-800">
                <button onclick="navigateTo('home')" id="nav-home" class="nav-btn px-5 py-2 rounded-full text-sm font-medium transition-all text-blue-600 dark:text-blue-400 bg-white dark:bg-slate-800/80 shadow-sm">
                    <i class="fa-solid fa-house mr-2"></i>Главная
                </button>
                <button onclick="navigateTo('about')" id="nav-about" class="nav-btn px-5 py-2 rounded-full text-sm font-medium text-slate-600 dark:text-slate-400 hover:text-slate-900 dark:hover:text-slate-200 transition-all">
                    <i class="fa-solid fa-user mr-2"></i>О себе
                </button>
                <button onclick="navigateTo('projects')" id="nav-projects" class="nav-btn px-5 py-2 rounded-full text-sm font-medium text-slate-600 dark:text-slate-400 hover:text-slate-900 dark:hover:text-slate-200 transition-all">
                    <i class="fa-solid fa-briefcase mr-2"></i>Проекты
                </button>
                <button onclick="navigateTo('contact')" id="nav-contact" class="nav-btn px-5 py-2 rounded-full text-sm font-medium text-slate-600 dark:text-slate-400 hover:text-slate-900 dark:hover:text-slate-200 transition-all">
                    <i class="fa-solid fa-envelope mr-2"></i>Контакты
                </button>
            </nav>

            <!-- Кнопки темы и меню -->
            <div class="flex items-center gap-3">
                <button id="theme-toggle" class="w-10 h-10 rounded-xl glass flex items-center justify-center text-slate-700 dark:text-slate-300 hover:text-slate-900 dark:hover:text-white transition-all" title="Сменить тему">
                    <i class="fa-solid fa-moon text-lg" id="theme-icon"></i>
                </button>

                <button onclick="toggleMobileMenu()" class="md:hidden w-10 h-10 rounded-xl glass flex items-center justify-center text-slate-700 dark:text-slate-300">
                    <i class="fa-solid fa-bars text-xl" id="menu-icon"></i>
                </button>
            </div>
        </div>

        <!-- МОБИЛЬНОЕ МЕНЮ -->
        <div id="mobile-menu" class="hidden md:hidden border-b border-slate-200 dark:border-slate-800 bg-white/95 dark:bg-slate-950/95 backdrop-blur-xl px-4 py-4 space-y-2">
            <button onclick="navigateTo('home'); toggleMobileMenu();" class="mobile-nav-btn w-full text-left px-4 py-3 rounded-xl font-medium text-slate-900 dark:text-slate-200 flex items-center gap-3 bg-slate-100 dark:bg-slate-900">
                <i class="fa-solid fa-house w-5 text-blue-600 dark:text-blue-400"></i>Главная
            </button>
            <button onclick="navigateTo('about'); toggleMobileMenu();" class="mobile-nav-btn w-full text-left px-4 py-3 rounded-xl font-medium text-slate-600 dark:text-slate-400 flex items-center gap-3">
                <i class="fa-solid fa-user w-5 text-purple-600 dark:text-purple-400"></i>О себе & Навыки
            </button>
            <button onclick="navigateTo('projects'); toggleMobileMenu();" class="mobile-nav-btn w-full text-left px-4 py-3 rounded-xl font-medium text-slate-600 dark:text-slate-400 flex items-center gap-3">
                <i class="fa-solid fa-briefcase w-5 text-emerald-600 dark:text-emerald-400"></i>Проекты
            </button>
            <button onclick="navigateTo('contact'); toggleMobileMenu();" class="mobile-nav-btn w-full text-left px-4 py-3 rounded-xl font-medium text-slate-600 dark:text-slate-400 flex items-center gap-3">
                <i class="fa-solid fa-envelope w-5 text-pink-600 dark:text-pink-400"></i>Контакты
            </button>
        </div>
    </header>

    <!-- ОСНОВНОЙ КОНТЕНТ -->
    <main class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 py-12 relative z-10 flex-grow w-full">

        <!-- ================= СТРАНИЦА 1: ГЛАВНАЯ ================= -->
        <section id="page-home" class="page-section active space-y-8">
            <div class="space-y-6">
                <div class="inline-flex items-center gap-2 px-3.5 py-1.5 rounded-full glass border border-blue-500/30 text-blue-600 dark:text-blue-400 text-xs font-semibold tracking-wide">
                    <span class="w-2 h-2 rounded-full bg-emerald-500 animate-pulse"></span>
                    Наконец-то я разобрался как сделать этот дашборд
                </div>

                <h1 class="text-4xl sm:text-6xl font-extrabold tracking-tight leading-tight text-slate-900 dark:text-slate-100">
                    Работаю над этой <span class="gradient-text">веб-визиткой</span>
                </h1>

                <p class="text-slate-600 dark:text-slate-400 text-lg sm:text-xl leading-relaxed max-w-2xl font-light">
                    Привет! Я оператор ПК, Промо консультант и Практический Философ на пол ставки.
                </p>

                <!-- Увеличенные кнопки -->
                <div class="flex flex-wrap items-center gap-4 pt-2">
                    <button onclick="navigateTo('about')" class="px-8 py-4 text-base sm:text-lg rounded-2xl gradient-bg font-semibold text-white shadow-lg shadow-blue-500/25 hover:shadow-blue-500/40 hover:scale-105 transition-all flex items-center gap-2">
                        <span>Рабочая карьера</span>
                        <i class="fa-solid fa-arrow-right text-sm"></i>
                    </button>
                    <button onclick="navigateTo('projects')" class="px-8 py-4 text-base sm:text-lg rounded-2xl glass font-semibold text-slate-800 dark:text-slate-200 hover:bg-slate-200 dark:hover:bg-slate-800/80 transition-all">
                        Философские проекты
                    </button>
                </div>
            </div>

            <!-- Лёгкая горизонтальная линия -->
            <hr class="border-slate-200 dark:border-slate-800/80 my-8">

            <!-- 3 кнопки на одной строке -->
            <div class="flex flex-wrap items-center gap-3">
                <button onclick="navigateTo('projects')" class="px-5 py-2.5 rounded-xl glass text-sm font-medium text-slate-700 dark:text-slate-300 hover:bg-slate-200 dark:hover:bg-slate-800 transition-all">
                    Личные
                </button>
                <button onclick="navigateTo('projects')" class="px-5 py-2.5 rounded-xl glass text-sm font-medium text-slate-700 dark:text-slate-300 hover:bg-slate-200 dark:hover:bg-slate-800 transition-all">
                    Шуточные
                </button>
                <button onclick="navigateTo('projects')" class="px-5 py-2.5 rounded-xl glass text-sm font-medium text-slate-700 dark:text-slate-300 hover:bg-slate-200 dark:hover:bg-slate-800 transition-all">
                    Тестовые
                </button>
            </div>
        </section>

        <!-- ================= СТРАНИЦА 2: О СЕБЕ ================= -->
        <section id="page-about" class="page-section space-y-8">
            <div class="space-y-4">
                <h2 class="text-3xl font-extrabold text-slate-900 dark:text-slate-100">Обо мне & <span class="gradient-text">Навыки</span></h2>
                <p class="text-slate-600 dark:text-slate-400">Информация о моем пути и опыте работы.</p>
            </div>
            <div class="glass p-6 rounded-2xl space-y-4 border border-slate-200 dark:border-slate-800">
                <h3 class="text-xl font-bold text-slate-900 dark:text-slate-100">Кто я такой?</h3>
                <p class="text-slate-700 dark:text-slate-300 text-sm leading-relaxed">Оператор ПК, Промо консультант и Практический Философ. Занимаюсь веб-разработкой и решением интересных задач.</p>
            </div>
        </section>

        <!-- ================= СТРАНИЦА 3: ПРОЕКТЫ ================= -->
        <section id="page-projects" class="page-section space-y-8">
            <div class="space-y-4">
                <h2 class="text-3xl font-extrabold text-slate-900 dark:text-slate-100">Мои <span class="gradient-text">Проекты</span></h2>
                <p class="text-slate-600 dark:text-slate-400">Здесь собраны мои работы, личные и тестовые проекты.</p>
            </div>
        </section>

        <!-- ================= СТРАНИЦА 4: КОНТАКТЫ ================= -->
        <section id="page-contact" class="page-section space-y-8">
            <div class="space-y-4">
                <h2 class="text-3xl font-extrabold text-slate-900 dark:text-slate-100">Связаться со <span class="gradient-text">мной</span></h2>
                <p class="text-slate-600 dark:text-slate-400">Напишите мне в социальных сетях.</p>
            </div>
        </section>

    </main>

    <!-- ПОДВАЛ С СОЦСЕТЯМИ -->
    <footer class="w-full glass border-t border-slate-200 dark:border-slate-800/80 py-6 mt-12 relative z-10">
        <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 flex flex-col sm:flex-row items-center justify-between gap-4">
            <p class="text-xs text-slate-500 dark:text-slate-400">© 2026 Суон Хилк. Все права защищены.</p>
            <div class="flex items-center gap-4">
                <a href="https://t.me/soonhil" target="_blank" class="w-10 h-10 rounded-xl glass flex items-center justify-center text-slate-700 dark:text-slate-300 hover:text-blue-600 dark:hover:text-blue-400 hover:scale-110 transition-all" title="Telegram">
                    <i class="fa-brands fa-telegram text-lg"></i>
                </a>
                <a href="https://github.com/suonhilk" target="_blank" class="w-10 h-10 rounded-xl glass flex items-center justify-center text-slate-700 dark:text-slate-300 hover:text-purple-600 dark:hover:text-purple-400 hover:scale-110 transition-all" title="GitHub">
                    <i class="fa-brands fa-github text-lg"></i>
                </a>
                <a href="https://vk.com" target="_blank" class="w-10 h-10 rounded-xl glass flex items-center justify-center text-slate-700 dark:text-slate-300 hover:text-blue-600 dark:hover:text-blue-500 hover:scale-110 transition-all" title="VK">
                    <i class="fa-brands fa-vk text-lg"></i>
                </a>
            </div>
        </div>
    </footer>

    <!-- СКРИПТЫ НАВИГАЦИИ И ТЕМ -->
    <script>
        function navigateTo(pageId) {
            document.querySelectorAll('.page-section').forEach(section => {
                section.classList.remove('active');
            });
            const target = document.getElementById('page-' + pageId);
            if (target) {
                target.classList.add('active');
            }
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        function toggleMobileMenu() {
            const menu = document.getElementById('mobile-menu');
            menu.classList.toggle('hidden');
        }

        const themeToggle = document.getElementById('theme-toggle');
        const themeIcon = document.getElementById('theme-icon');
        const htmlElement = document.documentElement;

        themeToggle.addEventListener('click', () => {
            htmlElement.classList.toggle('dark');
            if (htmlElement.classList.contains('dark')) {
                themeIcon.className = "fa-solid fa-moon text-lg";
            } else {
                themeIcon.className = "fa-solid fa-sun text-lg text-amber-500";
            }
        });
    </script>
</body>
</html>
