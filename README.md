<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sweet Dreams - Каталог тортов</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700&family=Montserrat:wght@300;400;600&display=swap');
        
        body {
            font-family: 'Montserrat', sans-serif;
            background-color: #fff9f9;
        }
        
        .title-font {
            font-family: 'Playfair Display', serif;
        }
        
        .cake-card {
            transition: all 0.3s ease;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
        }
        
        .cake-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 15px rgba(0, 0, 0, 0.1);
        }
        
        .modal-enter {
            opacity: 0;
            transform: scale(0.9);
        }
        
        .modal-enter-active {
            opacity: 1;
            transform: translateX(0);
            transition: opacity 300ms, transform 300ms;
        }
        
        .modal-exit {
            opacity: 1;
        }
        
        .modal-exit-active {
            opacity: 0;
            transform: scale(0.9);
            transition: opacity 300ms, transform 300ms;
        }
        
        .filter-btn.active {
            background-color: #f472b6;
            color: white;
        }
        
        /* Animation for cart icon */
        @keyframes bounce {
            0%, 20%, 50%, 80%, 100% {transform: translateY(0);}
            40% {transform: translateY(-10px);}
            60% {transform: translateY(-5px);}
        }
        
        .bounce {
            animation: bounce 1s;
        }
        
        /* Page transition */
        .page {
            display: none;
        }
        
        .page.active {
            display: block;
            animation: fadeIn 0.5s;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        
        /* Cart sidebar */
        .cart-sidebar {
            transform: translateX(100%);
            transition: transform 0.3s ease-out;
        }
        
        .cart-sidebar.open {
            transform: translateX(0);
        }
    </style>
</head>
<body class="text-gray-800">
    <!-- Header -->
    <header class="bg-pink-50 py-6 shadow-sm sticky top-0 z-40">
        <div class="container mx-auto px-4">
            <div class="flex flex-col md:flex-row justify-between items-center">
                <div class="flex items-center mb-4 md:mb-0">
                    <i class="fas fa-birthday-cake text-3xl text-pink-500 mr-3"></i>
                    <h1 class="title-font text-3xl font-bold text-pink-600 cursor-pointer" id="home-link">Sweet Dreams</h1>
                </div>
                <div class="flex items-center space-x-6">
                    <a href="#" class="nav-link text-pink-600 hover:text-pink-800 font-medium" data-page="home">Главная</a>
                    <a href="#" class="nav-link text-gray-600 hover:text-pink-600 font-medium" data-page="about">О нас</a>
                    <a href="#" class="nav-link text-gray-600 hover:text-pink-600 font-medium" data-page="delivery">Доставка</a>
                    <a href="#" class="nav-link text-gray-600 hover:text-pink-600 font-medium" data-page="contacts">Контакты</a>
                    <button id="cart-button" class="relative bg-pink-500 hover:bg-pink-600 text-white px-4 py-2 rounded-full flex items-center">
                        <i class="fas fa-shopping-cart mr-2"></i>
                        Корзина
                        <span id="cart-count" class="ml-2 bg-white text-pink-600 rounded-full w-6 h-6 flex items-center justify-center text-sm">0</span>
                    </button>
                </div>
            </div>
        </div>
    </header>

    <!-- Cart Sidebar -->
    <div id="cart-sidebar" class="cart-sidebar fixed top-0 right-0 w-full md:w-1/3 h-full bg-white shadow-xl z-50 overflow-y-auto">
        <div class="p-6">
            <div class="flex justify-between items-center mb-6">
                <h2 class="title-font text-2xl font-bold text-pink-700">Ваша корзина</h2>
                <button id="close-cart" class="text-gray-500 hover:text-gray-700">
                    <i class="fas fa-times text-xl"></i>
                </button>
            </div>
            
            <div id="cart-items" class="mb-6">
                <!-- Cart items will be loaded here -->
                <p id="empty-cart-message" class="text-gray-500 text-center py-8">Ваша корзина пуста</p>
            </div>
            
            <div class="border-t border-gray-200 pt-4">
                <div class="flex justify-between mb-2">
                    <span class="font-medium">Итого:</span>
                    <span id="cart-total" class="font-bold text-pink-600">0 ₽</span>
                </div>
                <button class="w-full bg-pink-500 hover:bg-pink-600 text-white py-3 rounded-full font-medium">
                    Оформить заказ
                </button>
            </div>
        </div>
    </div>

    <!-- Home Page -->
    <div id="home-page" class="page active">
        <!-- Hero Section -->
        <section class="bg-gradient-to-r from-pink-100 to-purple-100 py-16">
            <div class="container mx-auto px-4 text-center">
                <h2 class="title-font text-4xl md:text-5xl font-bold text-pink-700 mb-6">Наши восхитительные торты</h2>
                <p class="text-xl text-gray-600 max-w-2xl mx-auto mb-8">Каждый торт - произведение искусства, созданное с любовью и вниманием к деталям</p>
                <div class="relative max-w-md mx-auto">
                    <input type="text" placeholder="Найти торт..." class="w-full py-3 px-6 rounded-full border-0 shadow-md focus:ring-2 focus:ring-pink-300">
                    <button class="absolute right-2 top-1/2 transform -translate-y-1/2 bg-pink-500 text-white p-2 rounded-full hover:bg-pink-600">
                        <i class="fas fa-search"></i>
                    </button>
                </div>
            </div>
        </section>

        <!-- Filters -->
        <section class="py-8 bg-white">
            <div class="container mx-auto px-4">
                <div class="flex flex-wrap justify-center gap-3">
                    <button class="filter-btn active px-4 py-2 rounded-full border border-pink-300 hover:bg-pink-100 transition" data-category="all">
                        Все торты
                    </button>
                    <button class="filter-btn px-4 py-2 rounded-full border border-pink-300 hover:bg-pink-100 transition" data-category="classic">
                        Классические
                    </button>
                    <button class="filter-btn px-4 py-2 rounded-full border border-pink-300 hover:bg-pink-100 transition" data-category="wedding">
                        Свадебные
                    </button>
                    <button class="filter-btn px-4 py-2 rounded-full border border-pink-300 hover:bg-pink-100 transition" data-category="kids">
                        Детские
                    </button>
                    <button class="filter-btn px-4 py-2 rounded-full border border-pink-300 hover:bg-pink-100 transition" data-category="cheesecake">
                        Чизкейки
                    </button>
                    <button class="filter-btn px-4 py-2 rounded-full border border-pink-300 hover:bg-pink-100 transition" data-category="vegan">
                        Веганские
                    </button>
                </div>
            </div>
        </section>

        <!-- Cakes Catalog -->
        <section class="py-12">
            <div class="container mx-auto px-4">
                <h3 class="title-font text-3xl font-bold text-center mb-12 text-pink-700">Наш каталог</h3>
                
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-8" id="cakes-container">
                    <!-- Cakes will be loaded here by JavaScript -->
                </div>
            </div>
        </section>

        <!-- Testimonials -->
        <section class="py-16 bg-pink-50">
            <div class="container mx-auto px-4">
                <h3 class="title-font text-3xl font-bold text-center mb-12 text-pink-700">Отзывы наших клиентов</h3>
                
                <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
                    <div class="bg-white p-6 rounded-xl shadow-md">
                        <div class="flex items-center mb-4">
                            <div class="w-12 h-12 rounded-full bg-pink-200 flex items-center justify-center text-pink-600 font-bold mr-4">АС</div>
                            <div>
                                <h4 class="font-bold">Анна Смирнова</h4>
                                <div class="flex">
                                    <i class="fas fa-star text-yellow-400"></i>
                                    <i class="fas fa-star text-yellow-400"></i>
                                    <i class="fas fa-star text-yellow-400"></i>
                                    <i class="fas fa-star text-yellow-400"></i>
                                    <i class="fas fa-star text-yellow-400"></i>
                                </div>
                            </div>
                        </div>
                        <p class="text-gray-600">"Заказала торт на юбилей мужа. Все были в восторге! Вкус просто потрясающий, а оформление даже лучше, чем на фото. Обязательно закажу еще!"</p>
                    </div>
                    
                    <div class="bg-white p-6 rounded-xl shadow-md">
                        <div class="flex items-center mb-4">
                            <div class="w-12 h-12 rounded-full bg-pink-200 flex items-center justify-center text-pink-600 font-bold mr-4">МК</div>
                            <div>
                                <h4 class="font-bold">Мария Ковалева</h4>
                                <div class="flex">
                                    <i class="fas fa-star text-yellow-400"></i>
                                    <i class="fas fa-star text-yellow-400"></i>
                                    <i class="fas fa-star text-yellow-400"></i>
                                    <i class="fas fa-star text-yellow-400"></i>
                                    <i class="fas fa-star text-yellow-400"></i>
                                </div>
                            </div>
                        </div>
                        <p class="text-gray-600">"Свадебный торт был просто сказочным! Все гости спрашивали, где мы его заказывали. Очень внимательные кондитеры, учли все наши пожелания."</p>
                    </div>
                    
                    <div class="bg-white p-6 rounded-xl shadow-md">
                        <div class="flex items-center mb-4">
                            <div class="w-12 h-12 rounded-full bg-pink-200 flex items-center justify-center text-pink-600 font-bold mr-4">ДП</div>
                            <div>
                                <h4 class="font-bold">Дмитрий Петров</h4>
                                <div class="flex">
                                    <i class="fas fa-star text-yellow-400"></i>
                                    <i class="fas fa-star text-yellow-400"></i>
                                    <i class="fas fa-star text-yellow-400"></i>
                                    <i class="fas fa-star text-yellow-400"></i>
                                    <i class="fas fa-star-half-alt text-yellow-400"></i>
                                </div>
                            </div>
                        </div>
                        <p class="text-gray-600">"Заказал торт на день рождения дочери. Ребенок был в полном восторге от дизайна с единорогами! Вкус тоже отличный, хотя мог бы быть чуть менее сладким."</p>
                    </div>
                </div>
            </div>
        </section>
    </div>

    <!-- About Page -->
    <div id="about-page" class="page">
        <section class="py-16 bg-white">
            <div class="container mx-auto px-4">
                <div class="flex flex-col md:flex-row items-center">
                    <div class="md:w-1/2 mb-8 md:mb-0 md:pr-8">
                        <img src="https://images.unsplash.com/photo-1556911220-bff31c812dba?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1080&q=80" alt="Наша кондитерская" class="rounded-xl shadow-lg w-full">
                    </div>
                    <div class="md:w-1/2">
                        <h2 class="title-font text-3xl font-bold text-pink-700 mb-6">О нашей кондитерской</h2>
                        <p class="text-gray-600 mb-4">Sweet Dreams - это семейная кондитерская, основанная в 2010 году. Наша миссия - создавать не просто десерты, а настоящие произведения искусства, которые приносят радость и оставляют незабываемые впечатления.</p>
                        <p class="text-gray-600 mb-4">Мы используем только натуральные ингредиенты высшего качества: свежие фермерские яйца, натуральное сливочное масло, отборную муку и свежие фрукты. Никаких искусственных красителей и консервантов!</p>
                        <p class="text-gray-600 mb-6">Наша команда состоит из профессиональных кондитеров с многолетним опытом работы в лучших ресторанах и кондитерских Европы. Каждый торт мы создаем с любовью и вниманием к деталям.</p>
                        
                        <div class="bg-pink-50 p-6 rounded-xl">
                            <h3 class="title-font text-xl font-bold text-pink-700 mb-3">Наши преимущества</h3>
                            <ul class="space-y-2">
                                <li class="flex items-center">
                                    <i class="fas fa-check-circle text-pink-500 mr-2"></i>
                                    <span>100% натуральные ингредиенты</span>
                                </li>
                                <li class="flex items-center">
                                    <i class="fas fa-check-circle text-pink-500 mr-2"></i>
                                    <span>Индивидуальный подход к каждому клиенту</span>
                                </li>
                                <li class="flex items-center">
                                    <i class="fas fa-check-circle text-pink-500 mr-2"></i>
                                    <span>Бесплатная доставка по городу</span>
                                </li>
                                <li class="flex items-center">
                                    <i class="fas fa-check-circle text-pink-500 mr-2"></i>
                                    <span>Гарантия свежести и качества</span>
                                </li>
                            </ul>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <section class="py-16 bg-pink-50">
            <div class="container mx-auto px-4">
                <h2 class="title-font text-3xl font-bold text-center text-pink-700 mb-12">Наша команда</h2>
                
                <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
                    <div class="bg-white p-6 rounded-xl shadow-md text-center">
                        <img src="https://images.unsplash.com/photo-1580489944761-15a19d654956?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1080&q=80" alt="Анна" class="w-32 h-32 rounded-full mx-auto mb-4 object-cover">
                        <h3 class="title-font text-xl font-bold text-pink-700 mb-1">Анна Иванова</h3>
                        <p class="text-gray-500 mb-3">Главный кондитер</p>
                        <p class="text-gray-600">"Кондитерское искусство - это моя страсть. Каждый торт - это маленькая история, которую я создаю с любовью."</p>
                    </div>
                    
                    <div class="bg-white p-6 rounded-xl shadow-md text-center">
                        <img src="https://cs4.pikabu.ru/post_img/big/2015/07/16/6/1437033968_1045898135.png" alt="Михаил" class="w-32 h-32 rounded-full mx-auto mb-4 object-cover">
                        <h3 class="title-font text-xl font-bold text-pink-700 mb-1">Михаил Петров</h3>
                        <p class="text-gray-500 mb-3">Шеф-кондитер</p>
                        <p class="text-gray-600">"Я работаю с десертами более 15 лет. Для меня важно не только вкус, но и эстетика каждого изделия."</p>
                    </div>
                    
                    <div class="bg-white p-6 rounded-xl shadow-md text-center">
                        <img src="https://images.unsplash.com/photo-1573496359142-b8d87734a5a2?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1080&q=80" alt="Елена" class="w-32 h-32 rounded-full mx-auto mb-4 object-cover">
                        <h3 class="title-font text-xl font-bold text-pink-700 mb-1">Елена Соколова</h3>
                        <p class="text-gray-500 mb-3">Дизайнер тортов</p>
                        <p class="text-gray-600">"Моя задача - превратить ваши мечты в реальность. Я создаю уникальные дизайны, которые впечатляют и восхищают."</p>
                    </div>
                </div>
            </div>
        </section>
    </div>

    <!-- Delivery Page -->
    <div id="delivery-page" class="page">
        <section class="py-16 bg-white">
            <div class="container mx-auto px-4">
                <h2 class="title-font text-3xl font-bold text-center text-pink-700 mb-12">Условия доставки</h2>
                
                <div class="grid grid-cols-1 md:grid-cols-2 gap-8 mb-12">
                    <div class="bg-pink-50 p-8 rounded-xl">
                        <div class="flex items-center mb-4">
                            <div class="bg-pink-500 text-white rounded-full w-12 h-12 flex items-center justify-center mr-4">
                                <i class="fas fa-truck text-xl"></i>
                            </div>
                            <h3 class="title-font text-xl font-bold text-pink-700">Доставка по городу</h3>
                        </div>
                        <p class="text-gray-600 mb-4">Мы осуществляем бесплатную доставку по всему городу при заказе от 3000 рублей. Доставка осуществляется с 9:00 до 21:00.</p>
                        <p class="text-gray-600">Время доставки согласовывается с менеджером после оформления заказа. Среднее время доставки - 2 часа.</p>
                    </div>
                    
                    <div class="bg-pink-50 p-8 rounded-xl">
                        <div class="flex items-center mb-4">
                            <div class="bg-pink-500 text-white rounded-full w-12 h-12 flex items-center justify-center mr-4">
                                <i class="fas fa-store text-xl"></i>
                            </div>
                            <h3 class="title-font text-xl font-bold text-pink-700">Самовывоз</h3>
                        </div>
                        <p class="text-gray-600 mb-4">Вы можете забрать заказ самостоятельно из нашей кондитерской по адресу: г. Москва, ул. Кондитерская, 15.</p>
                        <p class="text-gray-600">Часы работы: ежедневно с 9:00 до 21:00. Пожалуйста, сообщите нам время вашего визита, чтобы мы подготовили ваш заказ.</p>
                    </div>
                </div>
                
                <div class="bg-white border border-pink-200 rounded-xl p-6 shadow-sm">
                    <h3 class="title-font text-xl font-bold text-pink-700 mb-4">Как сделать заказ?</h3>
                    <ol class="space-y-4">
                        <li class="flex items-start">
                            <span class="bg-pink-500 text-white rounded-full w-6 h-6 flex items-center justify-center mr-3 mt-1 flex-shrink-0">1</span>
                            <p class="text-gray-600">Выберите понравившийся торт в нашем каталоге или оставьте заявку на индивидуальный дизайн.</p>
                        </li>
                        <li class="flex items-start">
                            <span class="bg-pink-500 text-white rounded-full w-6 h-6 flex items-center justify-center mr-3 mt-1 flex-shrink-0">2</span>
                            <p class="text-gray-600">Добавьте торт в корзину и перейдите к оформлению заказа.</p>
                        </li>
                        <li class="flex items-start">
                            <span class="bg-pink-500 text-white rounded-full w-6 h-6 flex items-center justify-center mr-3 mt-1 flex-shrink-0">3</span>
                            <p class="text-gray-600">Укажите дату и время доставки, а также адрес (если требуется доставка).</p>
                        </li>
                        <li class="flex items-start">
                            <span class="bg-pink-500 text-white rounded-full w-6 h-6 flex items-center justify-center mr-3 mt-1 flex-shrink-0">4</span>
                            <p class="text-gray-600">Оплатите заказ удобным для вас способом (онлайн или при получении).</p>
                        </li>
                        <li class="flex items-start">
                            <span class="bg-pink-500 text-white rounded-full w-6 h-6 flex items-center justify-center mr-3 mt-1 flex-shrink-0">5</span>
                            <p class="text-gray-600">Получите ваш идеальный торт в назначенное время и наслаждайтесь!</p>
                        </li>
                    </ol>
                </div>
            </div>
        </section>
        
        <section class="py-16 bg-pink-50">
            <div class="container mx-auto px-4">
                <h2 class="title-font text-3xl font-bold text-center text-pink-700 mb-12">Часто задаваемые вопросы</h2>
                
                <div class="max-w-3xl mx-auto space-y-4">
                    <div class="bg-white p-6 rounded-xl shadow-sm">
                        <h3 class="title-font text-lg font-bold text-pink-700 mb-2">Как далеко заранее нужно заказывать торт?</h3>
                        <p class="text-gray-600">Мы рекомендуем делать заказ минимум за 3 дня до нужной даты. Для сложных дизайнов и свадебных тортов - за 2 недели.</p>
                    </div>
                    
                    <div class="bg-white p-6 rounded-xl shadow-sm">
                        <h3 class="title-font text-lg font-bold text-pink-700 mb-2">Можно ли изменить дизайн торта после оформления заказа?</h3>
                        <p class="text-gray-600">Да, изменения возможны за 48 часов до даты доставки. После этого времени мы начинаем приготовление торта.</p>
                    </div>
                    
                    <div class="bg-white p-6 rounded-xl shadow-sm">
                        <h3 class="title-font text-lg font-bold text-pink-700 mb-2">Как хранить торт после получения?</h3>
                        <p class="text-gray-600">Большинство наших тортов нужно хранить в холодильнике. Перед подачей рекомендуем вынуть торт за 30 минут до употребления.</p>
                    </div>
                    
                    <div class="bg-white p-6 rounded-xl shadow-sm">
                        <h3 class="title-font text-lg font-bold text-pink-700 mb-2">Есть ли у вас торты без сахара?</h3>
                        <p class="text-gray-600">Да, мы предлагаем торты с сахарозаменителями. Пожалуйста, укажите это при оформлении заказа.</p>
                    </div>
                </div>
            </div>
        </section>
    </div>

    <!-- Contacts Page -->
    <div id="contacts-page" class="page">
        <section class="py-16 bg-white">
            <div class="container mx-auto px-4">
                <h2 class="title-font text-3xl font-bold text-center text-pink-700 mb-12">Наши контакты</h2>
                
                <div class="flex flex-col md:flex-row gap-8">
                    <div class="md:w-1/2">
                        <div class="bg-pink-50 p-8 rounded-xl h-full">
                            <h3 class="title-font text-xl font-bold text-pink-700 mb-6">Как нас найти</h3>
                            
                            <div class="space-y-6">
                                <div class="flex items-start">
                                    <div class="bg-pink-500 text-white rounded-full w-10 h-10 flex items-center justify-center mr-4 mt-1 flex-shrink-0">
                                        <i class="fas fa-map-marker-alt"></i>
                                    </div>
                                    <div>
                                        <h4 class="font-bold text-gray-800 mb-1">Адрес</h4>
                                        <p class="text-gray-600">г. Москва, ул. Кондитерская, 15</p>
                                    </div>
                                </div>
                                
                                <div class="flex items-start">
                                    <div class="bg-pink-500 text-white rounded-full w-10 h-10 flex items-center justify-center mr-4 mt-1 flex-shrink-0">
                                        <i class="fas fa-phone-alt"></i>
                                    </div>
                                    <div>
                                        <h4 class="font-bold text-gray-800 mb-1">Телефон</h4>
                                        <p class="text-gray-600">+7 (999) 123-45-67</p>
                                        <p class="text-gray-600">+7 (495) 123-45-67</p>
                                    </div>
                                </div>
                                
                                <div class="flex items-start">
                                    <div class="bg-pink-500 text-white rounded-full w-10 h-10 flex items-center justify-center mr-4 mt-1 flex-shrink-0">
                                        <i class="fas fa-envelope"></i>
                                    </div>
                                    <div>
                                        <h4 class="font-bold text-gray-800 mb-1">Email</h4>
                                        <p class="text-gray-600">info@sweetdreams.ru</p>
                                        <p class="text-gray-600">orders@sweetdreams.ru</p>
                                    </div>
                                </div>
                                
                                <div class="flex items-start">
                                    <div class="bg-pink-500 text-white rounded-full w-10 h-10 flex items-center justify-center mr-4 mt-1 flex-shrink-0">
                                        <i class="fas fa-clock"></i>
                                    </div>
                                    <div>
                                        <h4 class="font-bold text-gray-800 mb-1">Часы работы</h4>
                                        <p class="text-gray-600">Пн-Пт: 9:00 - 21:00</p>
                                        <p class="text-gray-600">Сб-Вс: 10:00 - 20:00</p>
                                    </div>
                                </div>
                            </div>
                            
                            <div class="mt-8">
                                <h4 class="font-bold text-gray-800 mb-3">Мы в социальных сетях</h4>
                                <div class="flex space-x-4">
                                    <a href="#" class="bg-pink-500 text-white rounded-full w-10 h-10 flex items-center justify-center hover:bg-pink-600">
                                        <i class="fab fa-instagram"></i>
                                    </a>
                                    <a href="#" class="bg-pink-500 text-white rounded-full w-10 h-10 flex items-center justify-center hover:bg-pink-600">
                                        <i class="fab fa-facebook-f"></i>
                                    </a>
                                    <a href="#" class="bg-pink-500 text-white rounded-full w-10 h-10 flex items-center justify-center hover:bg-pink-600">
                                        <i class="fab fa-vk"></i>
                                    </a>
                                    <a href="#" class="bg-pink-500 text-white rounded-full w-10 h-10 flex items-center justify-center hover:bg-pink-600">
                                        <i class="fab fa-telegram-plane"></i>
                                    </a>
                                </div>
                            </div>
                        </div>
                    </div>
                    
                    <div class="md:w-1/2">
                        <div class="bg-white border border-pink-200 rounded-xl p-8 shadow-sm h-full">
                            <h3 class="title-font text-xl font-bold text-pink-700 mb-6">Напишите нам</h3>
                            
                            <form>
                                <div class="mb-4">
                                    <label for="name" class="block text-gray-700 font-medium mb-2">Ваше имя</label>
                                    <input type="text" id="name" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-pink-300 focus:border-pink-300">
                                </div>
                                
                                <div class="mb-4">
                                    <label for="email" class="block text-gray-700 font-medium mb-2">Email</label>
                                    <input type="email" id="email" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-pink-300 focus:border-pink-300">
                                </div>
                                
                                <div class="mb-4">
                                    <label for="phone" class="block text-gray-700 font-medium mb-2">Телефон</label>
                                    <input type="tel" id="phone" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-pink-300 focus:border-pink-300">
                                </div>
                                
                                <div class="mb-4">
                                    <label for="message" class="block text-gray-700 font-medium mb-2">Сообщение</label>
                                    <textarea id="message" rows="4" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-pink-300 focus:border-pink-300"></textarea>
                                </div>
                                
                                <button type="submit" class="w-full bg-pink-500 hover:bg-pink-600 text-white py-3 rounded-full font-medium">
                                    Отправить сообщение
                                </button>
                            </form>
                        </div>
                    </div>
                </div>
            </div>
        </section>
        
        <section class="py-8 bg-pink-50">
            <div class="container mx-auto px-4">
                <div class="rounded-xl overflow-hidden h-96">
                    <iframe src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d2245.373789919745!2d37.61531071593096!3d55.75202398055315!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x46b54a5a738fa419%3A0x7c347d506f52311b!2sRed%20Square!5e0!3m2!1sen!2sru!4v1623750000000!5m2!1sen!2sru" width="100%" height="100%" style="border:0;" allowfullscreen="" loading="lazy"></iframe>
                </div>
            </div>
        </section>
    </div>

    <!-- Cake Modal -->
    <div id="cake-modal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 hidden">
        <div class="bg-white rounded-xl max-w-4xl w-full mx-4 overflow-hidden shadow-2xl transform transition-all">
            <div class="flex flex-col md:flex-row">
                <div class="md:w-1/2">
                    <img id="modal-image" src="" alt="" class="w-full h-full object-cover">
                </div>
                <div class="md:w-1/2 p-6">
                    <div class="flex justify-between items-start">
                        <div>
                            <h3 id="modal-title" class="title-font text-2xl font-bold text-pink-700"></h3>
                            <p id="modal-category" class="text-sm text-gray-500 mt-1"></p>
                        </div>
                        <button id="close-modal" class="text-gray-400 hover:text-gray-600">
                            <i class="fas fa-times text-xl"></i>
                        </button>
                    </div>
                    
                    <div class="my-4">
                        <div class="flex items-center mb-2">
                            <i class="fas fa-star text-yellow-400 mr-1"></i>
                            <span id="modal-rating" class="font-medium"></span>
                            <span class="text-gray-500 ml-2" id="modal-reviews"></span>
                        </div>
                        <p id="modal-description" class="text-gray-600"></p>
                    </div>
                    
                    <div class="border-t border-b border-gray-200 py-4 my-4">
                        <div class="flex justify-between items-center mb-2">
                            <span class="font-medium">Вес:</span>
                            <span id="modal-weight" class="text-gray-600"></span>
                        </div>
                        <div class="flex justify-between items-center mb-2">
                            <span class="font-medium">Количество порций:</span>
                            <span id="modal-servings" class="text-gray-600"></span>
                        </div>
                        <div class="flex justify-between items-center">
                            <span class="font-medium">Состав:</span>
                            <span id="modal-ingredients" class="text-gray-600 text-right"></span>
                        </div>
                    </div>
                    
                    <div class="flex justify-between items-center mt-6">
                        <div>
                            <span class="text-2xl font-bold text-pink-600" id="modal-price"></span>
                        </div>
                        <div class="flex items-center">
                            <button class="quantity-minus bg-gray-200 hover:bg-gray-300 text-gray-800 w-8 h-8 rounded-full flex items-center justify-center">
                                <i class="fas fa-minus"></i>
                            </button>
                            <span class="mx-4 text-lg font-medium" id="modal-quantity">1</span>
                            <button class="quantity-plus bg-gray-200 hover:bg-gray-300 text-gray-800 w-8 h-8 rounded-full flex items-center justify-center">
                                <i class="fas fa-plus"></i>
                            </button>
                        </div>
                    </div>
                    
                    <button id="add-to-cart" class="w-full bg-pink-500 hover:bg-pink-600 text-white py-3 rounded-full mt-6 font-medium flex items-center justify-center">
                        <i class="fas fa-shopping-cart mr-2"></i>
                        Добавить в корзину
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- Footer -->
    <footer class="bg-pink-800 text-white py-12">
        <div class="container mx-auto px-4">
            <div class="grid grid-cols-1 md:grid-cols-4 gap-8">
                <div>
                    <h4 class="title-font text-xl font-bold mb-4">Sweet Dreams</h4>
                    <p class="mb-4">Кондитерская, где каждый торт создается с любовью и вниманием к деталям.</p>
                    <div class="flex space-x-4">
                        <a href="#" class="hover:text-pink-200"><i class="fab fa-instagram text-xl"></i></a>
                        <a href="#" class="hover:text-pink-200"><i class="fab fa-facebook text-xl"></i></a>
                        <a href="#" class="hover:text-pink-200"><i class="fab fa-vk text-xl"></i></a>
                    </div>
                </div>
                
                <div>
                    <h4 class="title-font text-xl font-bold mb-4">Меню</h4>
                    <ul class="space-y-2">
                        <li><a href="#" class="nav-link hover:text-pink-200" data-page="home">Главная</a></li>
                        <li><a href="#" class="nav-link hover:text-pink-200" data-page="about">О нас</a></li>
                        <li><a href="#" class="nav-link hover:text-pink-200" data-page="delivery">Доставка</a></li>
                        <li><a href="#" class="nav-link hover:text-pink-200" data-page="contacts">Контакты</a></li>
                    </ul>
                </div>
                
                <div>
                    <h4 class="title-font text-xl font-bold mb-4">Контакты</h4>
                    <ul class="space-y-2">
                        <li class="flex items-center">
                            <i class="fas fa-map-marker-alt mr-2"></i>
                            г. Москва, ул. Кондитерская, 15
                        </li>
                        <li class="flex items-center">
                            <i class="fas fa-phone mr-2"></i>
                            +7 (999) 123-45-67
                        </li>
                        <li class="flex items-center">
                            <i class="fas fa-envelope mr-2"></i>
                            info@sweetdreams.ru
                        </li>
                        <li class="flex items-center">
                            <i class="fas fa-clock mr-2"></i>
                            Ежедневно с 9:00 до 21:00
                        </li>
                    </ul>
                </div>
                
                <div>
                    <h4 class="title-font text-xl font-bold mb-4">Подписка</h4>
                    <p class="mb-4">Подпишитесь на наши новости и получите скидку 10% на первый заказ!</p>
                    <div class="flex">
                        <input type="email" placeholder="Ваш email" class="px-4 py-2 rounded-l-full w-full text-gray-800">
                        <button class="bg-pink-500 hover:bg-pink-600 px-4 py-2 rounded-r-full">
                            <i class="fas fa-paper-plane"></i>
                        </button>
                    </div>
                </div>
            </div>
            
            <div class="border-t border-pink-700 mt-8 pt-8 text-center text-sm">
                <p>© 2023 Sweet Dreams. Все права защищены.</p>
            </div>
        </div>
    </footer>

    <script>
        // Cake data with working images
        const cakes = [
            {
                id: 1,
                title: "Классический медовый",
                category: "classic",
                price: 2500,
                rating: 4.9,
                reviews: 128,
                weight: "1.5 кг",
                servings: "8-10",
                ingredients: "Мед, мука, яйца, сметана, сахар, сливочное масло",
                description: "Нежный медовый торт с тонкими коржами и сметанным кремом. Классика, проверенная временем.",
                image: "https://avatars.mds.yandex.net/i?id=52fb9407f5fa2c07532952c28f53e07d_l-12547901-images-thumbs&n=13"
            },
            {
                id: 2,
                title: "Красный бархат",
                category: "classic",
                price: 3200,
                rating: 4.8,
                reviews: 95,
                weight: "2 кг",
                servings: "10-12",
                ingredients: "Мука, какао, пахта, яйца, сливочный сыр, сахар, пищевой краситель",
                description: "Яркий торт с насыщенным вкусом и нежным кремом из сливочного сыра. Идеален для особых случаев.",
                image: "https://podacha-blud.com/uploads/posts/2022-12/thumbs/1671157291_14-podacha-blud-com-p-pirozhnoe-krasnii-barkhat-foto-14.jpg"
            },
            {
                id: 3,
                title: "Свадебный цветочный",
                category: "wedding",
                price: 12500,
                rating: 5.0,
                reviews: 42,
                weight: "5 кг",
                servings: "25-30",
                ingredients: "Мука, яйца, сливки, сливочное масло, сахар, ваниль, свежие цветы",
                description: "Элегантный свадебный торт с нежными ванильными нотками и украшением из свежих цветов.",
                image: "https://content2.flowwow-images.com/data/flowers/524x524/35/1673966038_69630235.jpg"
            },
            {
                id: 4,
                title: "Чизкейк Нью-Йорк",
                category: "cheesecake",
                price: 2800,
                rating: 4.9,
                reviews: 156,
                weight: "1.8 кг",
                servings: "8-10",
                ingredients: "Творожный сыр, яйца, сахар, сливки, печенье, сливочное масло",
                description: "Классический нью-йоркский чизкейк с нежной кремовой текстурой и хрустящей основой.",
                image: "https://uramaki163.ru/uploads/catalog/chizkejkkokos.jpg"
            },
            {
                id: 5,
                title: "Единорог",
                category: "kids",
                price: 3500,
                rating: 4.7,
                reviews: 87,
                weight: "2 кг",
                servings: "10-12",
                ingredients: "Мука, яйца, сливочное масло, сахар, сливки, пищевые красители",
                description: "Яркий и веселый торт для детского праздника с разноцветными слоями и украшением в виде единорога.",
                image: "https://images.unsplash.com/photo-1571115177098-24ec42ed204d?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1080&q=80"
            },
            {
                id: 6,
                title: "Шоколадный фондан",
                category: "classic",
                price: 2200,
                rating: 4.8,
                reviews: 112,
                weight: "1.2 кг",
                servings: "6-8",
                ingredients: "Темный шоколад, мука, яйца, сахар, сливочное масло",
                description: "Невероятно шоколадный торт с жидкой сердцевиной. Идеален для истинных ценителей шоколада.",
                image: "https://images.unsplash.com/photo-1562440499-64c9a111f713?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1080&q=80"
            },
            {
                id: 7,
                title: "Веганский кокосовый",
                category: "vegan",
                price: 2900,
                rating: 4.6,
                reviews: 64,
                weight: "1.5 кг",
                servings: "8-10",
                ingredients: "Кокосовое молоко, кокосовая стружка, мука без глютена, кленовый сироп, растительное масло",
                description: "Нежный веганский торт с насыщенным кокосовым вкусом. Без молочных продуктов и яиц.",
                image: "https://i.pinimg.com/originals/ea/4a/08/ea4a08388a473a3e4812fe508850f155.jpg"
            },
            {
                id: 8,
                title: "Трюфельный",
                category: "classic",
                price: 3800,
                rating: 4.9,
                reviews: 93,
                weight: "1.8 кг",
                servings: "10-12",
                ingredients: "Темный шоколад, сливки, сливочное масло, яйца, сахар, какао",
                description: "Богатый шоколадный торт с трюфельной начинкой и глазурью из темного шоколада.",
                image: "https://images.unsplash.com/photo-1603532648955-039310d9ed75?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1080&q=80"
            }
        ];
        // DOM elements
        const cakesContainer = document.getElementById('cakes-container');
        const filterButtons = document.querySelectorAll('.filter-btn');
        const modal = document.getElementById('cake-modal');
        const closeModal = document.getElementById('close-modal');
        const cartCount = document.getElementById('cart-count');
        const cartButton = document.getElementById('cart-button');
        const cartSidebar = document.getElementById('cart-sidebar');
        const closeCart = document.getElementById('close-cart');
        const cartItemsContainer = document.getElementById('cart-items');
        const cartTotal = document.getElementById('cart-total');
        const emptyCartMessage = document.getElementById('empty-cart-message');
        const pages = document.querySelectorAll('.page');
        const navLinks = document.querySelectorAll('.nav-link');
        const homeLink = document.getElementById('home-link');
        const addToCartButton = document.getElementById('add-to-cart');
        const quantityPlus = document.querySelector('.quantity-plus');
        const quantityMinus = document.querySelector('.quantity-minus');
        const modalQuantity = document.getElementById('modal-quantity');
        // State
        let cart = [];
        let currentCake = null;
        let currentQuantity = 1;
        // Display all cakes initially
        function displayCakes(cakesToDisplay) {
            cakesContainer.innerHTML = '';
            
            if (cakesToDisplay.length === 0) {
                cakesContainer.innerHTML = '<p class="text-center col-span-4 text-gray-500 py-12">Торты не найдены</p>';
                return;
            }
            
            cakesToDisplay.forEach(cake => {
                const cakeElement = document.createElement('div');
                cakeElement.className = 'cake-card bg-white rounded-xl overflow-hidden shadow-md hover:shadow-lg';
                cakeElement.innerHTML = `
                    <img src="${cake.image}" alt="${cake.title}" class="w-full h-64 object-cover">
                    <div class="p-4">
                        <div class="flex justify-between items-start mb-2">
                            <h3 class="title-font font-bold text-lg">${cake.title}</h3>
                            <span class="bg-pink-100 text-pink-800 text-xs px-2 py-1 rounded-full">${getCategoryName(cake.category)}</span>
                        </div>
                        <div class="flex items-center mb-3">
                            <i class="fas fa-star text-yellow-400 mr-1"></i>
                            <span class="font-medium">${cake.rating}</span>
                            <span class="text-gray-500 text-sm ml-2">(${cake.reviews} отзывов)</span>
                        </div>
                        <div class="flex justify-between items-center">
                            <span class="text-xl font-bold text-pink-600">${cake.price} ₽</span>
                            <button class="view-details bg-pink-500 hover:bg-pink-600 text-white px-4 py-2 rounded-full text-sm" data-id="${cake.id}">
                                Подробнее
                            </button>
                        </div>
                    </div>
                `;
                cakesContainer.appendChild(cakeElement);
            });
            
            // Add event listeners to "View Details" buttons
            document.querySelectorAll('.view-details').forEach(button => {
                button.addEventListener('click', (e) => {
                    const cakeId = parseInt(e.target.getAttribute('data-id'));
                    const selectedCake = cakes.find(cake => cake.id === cakeId);
                    openModal(selectedCake);
                });
            });
        }
        // Get category name in Russian
        function getCategoryName(category) {
            switch(category) {
                case 'classic': return 'Классика';
                case 'wedding': return 'Свадьба';
                case 'kids': return 'Детский';
                case 'cheesecake': return 'Чизкейк';
                case 'vegan': return 'Веган';
                default: return '';
            }
        }
        // Open modal with cake details
        function openModal(cake) {
            currentCake = cake;
            currentQuantity = 1;
            
            document.getElementById('modal-image').src = cake.image;
            document.getElementById('modal-title').textContent = cake.title;
            document.getElementById('modal-category').textContent = getCategoryName(cake.category);
            document.getElementById('modal-rating').textContent = cake.rating;
            document.getElementById('modal-reviews').textContent = `(${cake.reviews} отзывов)`;
            document.getElementById('modal-description').textContent = cake.description;
            document.getElementById('modal-weight').textContent = cake.weight;
            document.getElementById('modal-servings').textContent = cake.servings;
            document.getElementById('modal-ingredients').textContent = cake.ingredients;
            document.getElementById('modal-price').textContent = `${cake.price} ₽`;
            document.getElementById('modal-quantity').textContent = currentQuantity;
            
            modal.classList.remove('hidden');
            document.body.style.overflow = 'hidden';
        }
        // Close modal
        function closeModalFunc() {
            modal.classList.add('hidden');
            document.body.style.overflow = 'auto';
        }
        // Filter cakes by category
        function filterCakes(category) {
            if (category === 'all') {
                displayCakes(cakes);
            } else {
                const filteredCakes = cakes.filter(cake => cake.category === category);
                displayCakes(filteredCakes);
            }
        }
        // Open cart sidebar
        function openCart() {
            cartSidebar.classList.add('open');
            document.body.style.overflow = 'hidden';
            updateCartDisplay();
        }
        // Close cart sidebar
        function closeCartFunc() {
            cartSidebar.classList.remove('open');
            document.body.style.overflow = 'auto';
        }
        // Update cart count in header
        function updateCartCount() {
            const totalItems = cart.reduce((sum, item) => sum + item.quantity, 0);
            cartCount.textContent = totalItems;
            
            // Add bounce animation
            cartCount.classList.add('bounce');
            setTimeout(() => {
                cartCount.classList.remove('bounce');
            }, 1000);
        }
        // Update cart display in sidebar
        function updateCartDisplay() {
            if (cart.length === 0) {
                emptyCartMessage.classList.remove('hidden');
                cartItemsContainer.innerHTML = '';
                cartTotal.textContent = '0 ₽';
                return;
            }
            
            emptyCartMessage.classList.add('hidden');
            
            let cartHTML = '';
            let total = 0;
            
            cart.forEach(item => {
                const cake = cakes.find(c => c.id === item.id);
                total += cake.price * item.quantity;
                
                cartHTML += `
                    <div class="flex items-center justify-between py-4 border-b border-gray-200">
                        <div class="flex items-center">
                            <img src="${cake.image}" alt="${cake.title}" class="w-16 h-16 object-cover rounded-lg mr-4">
                            <div>
                                <h4 class="font-medium">${cake.title}</h4>
                                <p class="text-sm text-gray-500">${cake.price} ₽ × ${item.quantity}</p>
                            </div>
                        </div>
                        <div class="flex items-center">
                            <button class="remove-from-cart text-gray-400 hover:text-pink-500 mr-4" data-id="${cake.id}">
                                <i class="fas fa-trash"></i>
                            </button>
                            <span class="font-medium">${cake.price * item.quantity} ₽</span>
                        </div>
                    </div>
                `;
            });
            
            cartItemsContainer.innerHTML = cartHTML;
            cartTotal.textContent = `${total} ₽`;
            
            // Add event listeners to remove buttons
            document.querySelectorAll('.remove-from-cart').forEach(button => {
                button.addEventListener('click', (e) => {
                    const cakeId = parseInt(e.target.closest('button').getAttribute('data-id'));
                    removeFromCart(cakeId);
                });
            });
        }
        // Add item to cart
        function addToCart(cakeId, quantity) {
            const existingItem = cart.find(item => item.id === cakeId);
            
            if (existingItem) {
                existingItem.quantity += quantity;
            } else {
                cart.push({ id: cakeId, quantity });
            }
            
            updateCartCount();
            updateCartDisplay();
            
            // Show notification
            const cake = cakes.find(c => c.id === cakeId);
            const notification = document.createElement('div');
            notification.className = 'fixed bottom-4 right-4 bg-green-500 text-white px-4 py-2 rounded-full shadow-lg flex items-center animate-bounce';
            notification.innerHTML = `
                <i class="fas fa-check-circle mr-2"></i>
                "${cake.title}" добавлен в корзину!
            `;
            document.body.appendChild(notification);
            
            setTimeout(() => {
                notification.remove();
            }, 3000);
        }
        // Remove item from cart
        function removeFromCart(cakeId) {
            cart = cart.filter(item => item.id !== cakeId);
            updateCartCount();
            updateCartDisplay();
        }
        // Change page
        function changePage(pageId) {
            pages.forEach(page => {
                if (page.id === pageId) {
                    page.classList.add('active');
                } else {
                    page.classList.remove('active');
                }
            });
            
            // Update active link
            navLinks.forEach(link => {
                if (link.getAttribute('data-page') === pageId.replace('-page', '')) {
                    link.classList.add('text-pink-600');
                    link.classList.remove('text-gray-600');
                } else {
                    link.classList.remove('text-pink-600');
                    link.classList.add('text-gray-600');
                }
            });
            
            // Scroll to top
            window.scrollTo(0, 0);
        }
        // Initialize
        displayCakes(cakes);
        // Event listeners
        filterButtons.forEach(button => {
            button.addEventListener('click', () => {
                filterButtons.forEach(btn => btn.classList.remove('active'));
                button.classList.add('active');
                const category = button.getAttribute('data-category');
                filterCakes(category);
            });
        });
        closeModal.addEventListener('click', closeModalFunc);
        cartButton.addEventListener('click', openCart);
        closeCart.addEventListener('click', closeCartFunc);
        homeLink.addEventListener('click', () => changePage('home-page'));
        // Modal quantity controls
        quantityPlus.addEventListener('click', () => {
            currentQuantity++;
            modalQuantity.textContent = currentQuantity;
        });
        quantityMinus.addEventListener('click', () => {
            if (currentQuantity > 1) {
                currentQuantity--;
                modalQuantity.textContent = currentQuantity;
            }
        });
        // Add to cart from modal
        addToCartButton.addEventListener('click', () => {
            if (currentCake) {
                addToCart(currentCake.id, currentQuantity);
                closeModalFunc();
            }
        });
        // Navigation links
        navLinks.forEach(link => {
            link.addEventListener('click', (e) => {
                e.preventDefault();
                const pageId = link.getAttribute('data-page') + '-page';
                changePage(pageId);
            });
        });
        // Close modal when clicking outside
        modal.addEventListener('click', (e) => {
            if (e.target === modal) {
                closeModalFunc();
            }
        });
        // Close cart when clicking outside
        cartSidebar.addEventListener('click', (e) => {
            if (e.target === cartSidebar) {
                closeCartFunc();
            }
        });
    </script>
<p style="border-radius: 8px; text-align: center; font-size: 12px; color: #fff; margin-top: 16px;position: fixed; left: 8px; bottom: 8px; z-index: 10; background: rgba(0, 0, 0, 0.8); padding: 4px 8px;">Made with <img src="https://enzostvs-deepsite.hf.space/logo.svg" alt="DeepSite Logo" style="width: 16px; height: 16px; vertical-align: middle;display:inline-block;margin-right:3px;filter:brightness(0) invert(1);"><a href="https://enzostvs-deepsite.hf.space" style="color: #fff;text-decoration: underline;" target="_blank" >DeepSite</a> - 🧬 <a href="https://enzostvs-deepsite.hf.space?remix=Tim1123445123/sweetdreams-com" style="color: #fff;text-decoration: underline;" target="_blank" >Remix</a></p></body>
</html>
