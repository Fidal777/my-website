
<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>องค์ประกอบศิลป์ | AI Transformation</title>
    
    <!-- Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Kanit:wght@200;300;400;600;800&family=Poppins:wght@300;400;600;800&display=swap" rel="stylesheet">
    
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- FontAwesome -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Kanit', 'Poppins', 'sans-serif'],
                    },
                    colors: {
                        brand: {
                            dark: '#0f0c29',
                            purple: '#302b63',
                            teal: '#24243e',
                            accent: '#00f260',
                            accent2: '#0575E6',
                        }
                    },
                    animation: {
                        'float': 'float 6s ease-in-out infinite',
                        'pulse-slow': 'pulse 4s cubic-bezier(0.4, 0, 0.6, 1) infinite',
                        'slide-up': 'slideUp 0.8s ease-out forwards',
                    },
                    keyframes: {
                        float: {
                            '0%, 100%': { transform: 'translateY(0)' },
                            '50%': { transform: 'translateY(-20px)' },
                        },
                        slideUp: {
                            '0%': { opacity: '0', transform: 'translateY(50px)' },
                            '100%': { opacity: '1', transform: 'translateY(0)' },
                        }
                    }
                }
            }
        }
    </script>

    <style>
        /* Global Styles */
        html {
            scroll-behavior: smooth; /* ทำให้การกดเลื่อนหน้านุ่มนวล */
        }
        body {
            background-color: #0f0c29;
            color: #ffffff;
            overflow-x: hidden;
        }

        /* Canvas Background */
        #bg-canvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            background: radial-gradient(circle at center, #1a1a2e 0%, #000000 100%);
        }

        /* Glassmorphism */
        .glass-panel {
            background: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(16px);
            -webkit-backdrop-filter: blur(16px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            box-shadow: 0 4px 30px rgba(0, 0, 0, 0.5);
        }

        .glass-card {
            background: linear-gradient(135deg, rgba(255, 255, 255, 0.1), rgba(255, 255, 255, 0.02));
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.05);
            transition: all 0.4s ease;
        }

        .glass-card:hover {
            transform: translateY(-10px) scale(1.02);
            background: linear-gradient(135deg, rgba(255, 255, 255, 0.15), rgba(255, 255, 255, 0.05));
            border-color: rgba(0, 242, 96, 0.5);
            box-shadow: 0 10px 40px -10px rgba(0, 242, 96, 0.3);
        }

        /* Typography */
        .text-gradient {
            background: linear-gradient(to right, #00f260, #0575E6);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        /* Scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #0f0c29;
        }
        ::-webkit-scrollbar-thumb {
            background: #302b63;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #00f260;
        }

        /* Cursor */
        .cursor-trail {
            position: fixed;
            width: 20px;
            height: 20px;
            border-radius: 50%;
            background: rgba(0, 242, 96, 0.5);
            pointer-events: none;
            z-index: 9999;
            transform: translate(-50%, -50%);
            mix-blend-mode: screen;
            transition: width 0.2s, height 0.2s;
        }

        /* Color Mixer */
        .color-swatch {
            transition: transform 0.2s;
        }
        .color-swatch:active {
            transform: scale(0.9);
        }
        
        /* Gallery Image Hover Effect */
        .gallery-item {
            position: relative;
            overflow: hidden;
        }
        .gallery-item img {
            transition: transform 0.6s ease;
        }
        .gallery-item:hover img {
            transform: scale(1.1);
        }
        .gallery-overlay {
            background: linear-gradient(to top, rgba(0,0,0,0.8), transparent);
            opacity: 0;
            transition: opacity 0.4s;
        }
        .gallery-item:hover .gallery-overlay {
            opacity: 1;
        }
    </style>
</head>
<body class="antialiased selection:bg-brand-accent selection:text-black">

    <!-- Custom Cursor -->
    <div id="cursor" class="cursor-trail hidden md:block"></div>

    <!-- Background Animation -->
    <canvas id="bg-canvas"></canvas>

    <!-- Navigation -->
    <nav class="fixed w-full z-50 transition-all duration-300 p-4 top-0" id="navbar">
        <div class="max-w-7xl mx-auto glass-panel rounded-full px-6 py-3 flex justify-between items-center">
            <div class="flex items-center space-x-2">
                <div class="w-8 h-8 rounded-full bg-gradient-to-tr from-brand-accent to-brand-accent2 flex items-center justify-center text-black font-bold">AI</div>
                <span class="text-xl font-bold tracking-wider">TRANS<span class="text-brand-accent">FORMATION</span></span>
            </div>
            <div class="hidden md:flex space-x-8 text-sm font-light tracking-widest">
                <a href="#hero" class="hover:text-brand-accent transition-colors">หน้าแรก</a>
                <a href="#elements" class="hover:text-brand-accent transition-colors">องค์ประกอบ</a>
                <a href="#playground" class="hover:text-brand-accent transition-colors">โจทย์ปฏิบัติ</a>
                <a href="#gallery" class="hover:text-brand-accent transition-colors">หอศิลป์</a>
                <a href="#curriculum" class="hover:text-brand-accent transition-colors">หลักสูตร</a>
            </div>
            <a href="ล็อกอิน.html">
            <button class="bg-white text-black px-6 py-2 rounded-full font-bold text-sm hover:bg-brand-accent transition-all duration-300 transform hover:scale-105 shadow-[0_0_15px_rgba(255,255,255,0.3)]">
                เข้าสู่ระบบ
            </button>
            </a>
        </div>
    </nav>

    <!-- Section 1: Hero -->
    <section id="hero" class="relative min-h-screen flex items-center justify-center pt-20 overflow-hidden">
        <div class="absolute top-1/4 left-10 w-64 h-64 bg-brand-accent rounded-full mix-blend-screen filter blur-[100px] opacity-20 animate-pulse-slow"></div>
        <div class="absolute bottom-1/4 right-10 w-96 h-96 bg-brand-accent2 rounded-full mix-blend-screen filter blur-[120px] opacity-20 animate-pulse-slow"></div>

        <div class="container mx-auto px-4 text-center z-10">
            <div class="inline-block mb-4 px-4 py-1 rounded-full border border-brand-accent/30 bg-brand-accent/10 backdrop-blur-md text-brand-accent text-xs tracking-[0.2em] uppercase animate-slide-up">
                <i class="fas fa-star mr-2"></i>  AI Transformation
            </div>
            
            <h1 class="text-5xl md:text-8xl font-black mb-6 leading-tight animate-slide-up" style="animation-delay: 0.1s;">
                องค์ประกอบศิลป์<br>
                <span class="text-gradient">สัมผัสการเรียนรู้</span>
            </h1>
            
            <p class="text-gray-400 text-lg md:text-2xl max-w-2xl mx-auto mb-10 font-light animate-slide-up" style="animation-delay: 0.2s;">
                แพลตฟอร์มการเรียนรู้องค์ประกอบศิลป์ออนไลน์แบบโต้ตอบเชิงลึก ที่ผสานเทคโนโลยีเข้ากับศิลปะอย่างลงตัว ช่วยให้คุณเข้าใจเส้น สี รูปทรง และพื้นผิวได้อย่างชัดเจน เปิดประสบการณ์การเรียนรู้ที่ไร้ขอบเขตและไม่จำกัดรูปแบบ
            </p>

            <div class="flex flex-col md:flex-row justify-center gap-6 animate-slide-up" style="animation-delay: 0.3s;">
                <a href="#playground" class="group relative px-8 py-4 bg-transparent overflow-hidden rounded-full border border-brand-accent text-brand-accent font-bold transition-all hover:bg-brand-accent hover:text-black">
                    <span class="absolute w-0 h-0 transition-all duration-500 ease-out bg-white rounded-full group-hover:w-56 group-hover:h-56 opacity-10"></span>
                    <span class="relative flex items-center">
                        เริ่มปฏิบัติการ <i class="fas fa-arrow-right ml-2 group-hover:translate-x-1 transition-transform"></i>
                    </span>
                </a>
                <a href="#curriculum" class="px-8 py-4 bg-white/5 backdrop-blur-md border border-white/10 rounded-full font-bold hover:bg-white/10 transition-all text-gray-300">
                    ดูหลักสูตร
                </a>
            </div>
        </div>
    </section>

    <!-- Section 2: Elements -->
    <section id="elements" class="py-24 relative">
        <div class="container mx-auto px-4">
            <div class="text-center mb-16">
                <h2 class="text-3xl md:text-5xl font-bold mb-4">องค์ประกอบพื้นฐาน</h2>
                <div class="h-1 w-20 bg-brand-accent mx-auto rounded-full"></div>
                <p class="mt-4 text-gray-400">คลิกเพื่อเรียนรู้และดูเนื้อหาเกี่ยวกับองค์ประกอบศิลป์พื้นฐาน</p>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6">
                <!-- Line -->
            <nav>
                <div class="glass-card p-8 rounded-2xl relative group cursor-pointer">
                    <a href="https://lersros-lookchin.my.canva.site/dag-iij7i8k">
                    <div class="text-4xl text-brand-accent mb-4 group-hover:scale-110 transition-transform duration-300">
                        <i class="fas fa-slash"></i>
                   </div>
                    <h3 class="text-xl font-bold mb-2">เส้น (Line)</h3>
                    <p class="text-sm text-gray-400 mb-4">การเคลื่อนที่ของจุดจุดหนึ่ง สร้างพลังและทิศทาง</p>
                    <div class="w-full h-1 bg-gray-700 rounded-full overflow-hidden">
                        <div class="h-full bg-brand-accent w-0 group-hover:w-full transition-all duration-700 ease-out"></div>
                    </a>
                    </div>
                </div>
            </nav>
                <!-- Shape -->
                <div class="glass-card p-8 rounded-2xl relative group cursor-pointer">
                    <a href="https://lersros-lookchin.my.canva.site/shape-form">
                    <div class="text-4xl text-pink-500 mb-4 group-hover:scale-110 transition-transform duration-300">
                        <i class="fas fa-shapes"></i>
                    </div>
                    <h3 class="text-xl font-bold mb-2">รูปร่าง รูปทรง (Shape & Form)</h3>
                    <p class="text-sm text-gray-400 mb-4">พื้นที่ปิดล้อมที่ถูกกำหนดด้วยเส้น</p>
                    <div class="w-full h-1 bg-gray-700 rounded-full overflow-hidden">
                        <div class="h-full bg-pink-500 w-0 group-hover:w-full transition-all duration-700 ease-out"></div>
                    </a>
                    </div>
                </div>
                <!-- Color -->
                <div class="glass-card p-8 rounded-2xl relative group cursor-pointer">
                    <a href="https://lersros-lookchin.my.canva.site/color">
                    <div class="text-4xl text-yellow-400 mb-4 group-hover:scale-110 transition-transform duration-300">
                        <i class="fas fa-fill-drip"></i>
                    </div>
                    <h3 class="text-xl font-bold mb-2">สี (Color)</h3>
                    <p class="text-sm text-gray-400 mb-4">แสงที่สะท้อนออกมาสู่สายตา สื่อถึงอารมณ์</p>
                    <div class="w-full h-1 bg-gray-700 rounded-full overflow-hidden">
                        <div class="h-full bg-yellow-400 w-0 group-hover:w-full transition-all duration-700 ease-out"></div>
                    </a>
                    </div>
                </div>
                <!-- Form -->
                <div class="glass-card p-8 rounded-2xl relative group cursor-pointer">
                    <a href="https://lersros-lookchin.my.canva.site/form">
                    <div class="text-4xl text-cyan-400 mb-4 group-hover:scale-110 transition-transform duration-300">
                        <i class="fas fa-cube"></i>
                    </div>
                    <h3 class="text-xl font-bold mb-2">รูปทรงตัน (Form)</h3>
                    <p class="text-sm text-gray-400 mb-4">รูปทรงที่มีความหนา มีมิติที่ 3</p>
                    <div class="w-full h-1 bg-gray-700 rounded-full overflow-hidden">
                        <div class="h-full bg-cyan-400 w-0 group-hover:w-full transition-all duration-700 ease-out"></div>
                    </a>
                    </div>
                </div>
                <!-- Value -->
                <div class="glass-card p-8 rounded-2xl relative group cursor-pointer">
                    <a href="https://lersros-lookchin.my.canva.site/value">
                    <div class="text-4xl text-purple-400 mb-4 group-hover:scale-110 transition-transform duration-300">
                        <i class="fas fa-text-height"></i>
                    </div>
                    <h3 class="text-xl font-bold mb-2">เนื้อ (Value)</h3>
                    <p class="text-sm text-gray-400 mb-4">ความสว่างหรือความมืดของสี</p>
                    <div class="w-full h-1 bg-gray-700 rounded-full overflow-hidden">
                        <div class="h-full bg-purple-400 w-0 group-hover:w-full transition-all duration-700 ease-out"></div>
                    </a>
                    </div>
                </div>
                <!-- Texture -->
                <div class="glass-card p-8 rounded-2xl relative group cursor-pointer">
                    <a href="https://lersros-lookchin.my.canva.site/line">
                    <div class="text-4xl text-red-400 mb-4 group-hover:scale-110 transition-transform duration-300">
                        <i class="fas fa-hand-paper"></i>
                    </div>
                    <h3 class="text-xl font-bold mb-2">พื้นผิว (Texture)</h3>
                    <p class="text-sm text-gray-400 mb-4">ความหยาบ ละเอียด ของวัตถุ</p>
                    <div class="w-full h-1 bg-gray-700 rounded-full overflow-hidden">
                        <div class="h-full bg-red-400 w-0 group-hover:w-full transition-all duration-700 ease-out"></div>
                    </a>
                    </div>
                </div>
                <!-- Space (Wide) -->
                <div class="glass-card p-8 rounded-2xl relative group cursor-pointer col-span-1 md:col-span-2">
                    <a href="https://krittayakorn.wordpress.com/2013/03/20/shape-and-form/">
                    <div class="flex flex-col md:flex-row items-center gap-6">
                        <div class="text-5xl text-indigo-400">
                            <i class="fas fa-cubes"></i>
                        </div>
                        <div>
                            <h3 class="text-2xl font-bold mb-2">อวกาศ (Space)</h3>
                            <p class="text-sm text-gray-400">พื้นที่ว่างรอบๆ ระหว่าง หรือภายในวัตถุ ทั้งในเชิงบวกและเชิงลบ</p>
                        </div>
                    </a>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Section 3: Playground -->
    <section id="playground" class="py-24 relative bg-gradient-to-b from-transparent to-black/50">
        <div class="container mx-auto px-4">
            <div class="flex flex-col lg:flex-row gap-12 items-center">
                
                <!-- Text -->
                <div class="lg:w-1/3">
                    <h2 class="text-3xl md:text-5xl font-bold mb-6"><span class="text-gradient-gold">สัมผัสการเรียนรู้:</span><br>ทฤษฎีสีแบบเชิงโต้ตอบ</h2>
                    <p class="text-gray-300 mb-6 leading-relaxed">
                        ในระบบการเรียนรู้ของเรา คุณจะไม่ได้เพียงแค่อ่านเท่านั้น แต่คุณจะได้ <strong>ลองผิดลองถูก</strong> จับคู่สีเอง และเข้าใจหลักการของ "Color Harmony" ได้ทันที
                    </p>
                    <ul class="space-y-3 text-gray-400">
                        <li class="flex items-center"><i class="fas fa-check-circle text-brand-accent mr-3"></i> ตรวจสอบส่วนผสมของสีเฉพาะ (RGB/CMYK)</li>
                        <li class="flex items-center"><i class="fas fa-check-circle text-brand-accent mr-3"></i> จำลองสีที่อยู่ตรงข้ามกัน (Complementary)</li>
                        <li class="flex items-center"><i class="fas fa-check-circle text-brand-accent mr-3"></i> สร้าง Mood Board ให้กับงานศิลปะ</li>
                    </ul>
                </div>

                <!-- Tool -->
                <div class="lg:w-2/3 w-full">
                    <div class="glass-panel p-6 md:p-10 rounded-3xl shadow-2xl border border-white/10 relative overflow-hidden">
                        <div class="flex justify-between items-center mb-8">
                            <h3 class="text-xl font-bold flex items-center"><i class="fas fa-palette mr-2 text-brand-accent"></i> Color Harmony Tool</h3>
                            <div class="flex gap-2">
                                <button onclick="setHarmony('analogous')" class="px-3 py-1 text-xs rounded border border-gray-600 hover:border-brand-accent hover:text-brand-accent transition">Analogous</button>
                                <button onclick="setHarmony('complementary')" class="px-3 py-1 text-xs rounded border border-gray-600 hover:border-brand-accent hover:text-brand-accent transition">Complementary</button>
                            </div>
                        </div>

                        <div id="color-display" class="flex h-48 md:h-64 rounded-xl overflow-hidden mb-6 transition-all duration-500 shadow-inner">
                            <div class="flex-1 bg-red-500 flex items-center justify-center transition-colors duration-500 color-swatch group relative">
                                <span class="text-white/0 group-hover:text-white font-bold text-lg drop-shadow-md transition-all">Primary</span>
                            </div>
                            <div class="flex-1 bg-orange-500 flex items-center justify-center transition-colors duration-500 color-swatch group relative">
                                <span class="text-white/0 group-hover:text-white font-bold text-lg drop-shadow-md transition-all">Secondary</span>
                            </div>
                            <div class="flex-1 bg-yellow-500 flex items-center justify-center transition-colors duration-500 color-swatch group relative">
                                <span class="text-black/0 group-hover:text-black font-bold text-lg drop-shadow-md transition-all">Tertiary</span>
                            </div>
                        </div>

                        <div class="bg-black/40 p-4 rounded-xl">
                            <label class="text-xs text-gray-400 uppercase tracking-wider mb-2 block">Adjust Hue</label>
                            <input type="range" min="0" max="360" value="0" class="w-full h-2 bg-gray-700 rounded-lg appearance-none cursor-pointer accent-brand-accent" oninput="updateColors(this.value)">
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Section 4: Gallery (เพิ่มหน้าใหม่) -->
    <section id="gallery" class="py-24 relative">
        <div class="container mx-auto px-4">
            <div class="text-center mb-16">
                <h2 class="text-4xl font-bold mb-4">Art composition exercises</h2>
                <p class="text-gray-400">แบบฝึกหัดเกี่ยวกับองค์ประกอบศิลป์</p>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                <!-- Gallery Item 1 -->
                <div class="glass-card rounded-xl overflow-hidden gallery-item group cursor-pointer">
                    <a href="แบบฝึกหัด1.html">
                    <div class="h-64 bg-gradient-to-br from-pink-500 to-rose-700 flex items-center justify-center">
                        <i class="fas fa-paint-brush text-6xl text-white/30 group-hover:scale-125 transition-transform duration-500"></i>
                    </div>
                    <div class="gallery-overlay absolute inset-0 flex flex-col justify-end p-6">
                        <h3 class="text-xl font-bold text-white">Exercise 1</h3>
                        <p class="text-sm text-gray-300">แบบฝึกหัด 1</p>
                    </div>
                    </a>
                </div>

                <!-- Gallery Item 2 -->
                <div class="glass-card rounded-xl overflow-hidden gallery-item group cursor-pointer">
                    <a href="แบบฝึกหัด2.html">
                    <div class="h-64 bg-gradient-to-bl from-blue-400 to-indigo-900 flex items-center justify-center">
                        <i class="fas fa-shapes text-6xl text-white/30 group-hover:scale-125 transition-transform duration-500"></i>
                    </div>
                    <div class="gallery-overlay absolute inset-0 flex flex-col justify-end p-6">
                        <h3 class="text-xl font-bold text-white">Exercise 2</h3>
                        <p class="text-sm text-gray-300">แบบฝึกหัด 2</p>
                    </div>
                    </a>
                </div>

                <!-- Gallery Item 3 -->
                <div class="glass-card rounded-xl overflow-hidden gallery-item group cursor-pointer">
                    <a href="แบบฝึกหัด3.html">
                    <div class="h-64 bg-gradient-to-tr from-green-400 to-teal-800 flex items-center justify-center">
                        <i class="fas fa-leaf text-6xl text-white/30 group-hover:scale-125 transition-transform duration-500"></i>
                    </div>
                    <div class="gallery-overlay absolute inset-0 flex flex-col justify-end p-6">
                        <h3 class="text-xl font-bold text-white">Exercise 3</h3>
                        <p class="text-sm text-gray-300">แบบฝึกหัด 3</p>
                    </div>
                    </a>
                </div>
                
                 <!-- Gallery Item 4 -->
                 <div class="glass-card rounded-xl overflow-hidden gallery-item group cursor-pointer">
                    <a href="แบบฝึกหัด4.html">
                    <div class="h-64 bg-gradient-to-br from-yellow-400 to-orange-600 flex items-center justify-center">
                        <i class="fas fa-sun text-6xl text-white/30 group-hover:scale-125 transition-transform duration-500"></i>
                    </div>
                    <div class="gallery-overlay absolute inset-0 flex flex-col justify-end p-6">
                        <h3 class="text-xl font-bold text-white">Exercise 4</h3>
                        <p class="text-sm text-gray-300">แบบฝึกหัด 4</p>
                    </div>
                    </a>
                </div>

                 <!-- Gallery Item 5 -->
                 <div class="glass-card rounded-xl overflow-hidden gallery-item group cursor-pointer">
                    <a href="แบบฝึกหัด5.html">
                    <div class="h-64 bg-gradient-to-r from-purple-500 to-pink-500 flex items-center justify-center">
                        <i class="fas fa-palette text-6xl text-white/30 group-hover:scale-125 transition-transform duration-500"></i>
                    </div>
                    <div class="gallery-overlay absolute inset-0 flex flex-col justify-end p-6">
                        <h3 class="text-xl font-bold text-white">Exercise 5</h3>
                        <p class="text-sm text-gray-300">แบบฝึกหัด 5</p>
                    </div>
                    </a>
                </div>

                 <!-- Gallery Item 6 -->
                 <div class="glass-card rounded-xl overflow-hidden gallery-item group cursor-pointer">
                    <a href="แบบฝึกหัด6.html">
                    <div class="h-64 bg-gradient-to-t from-gray-700 to-gray-900 flex items-center justify-center">
                        <i class="fas fa-cube text-6xl text-white/30 group-hover:scale-125 transition-transform duration-500"></i>
                    </div>
                    <div class="gallery-overlay absolute inset-0 flex flex-col justify-end p-6">
                        <h3 class="text-xl font-bold text-white">Exercise 6</h3>
                        <p class="text-sm text-gray-300">แบบฝึกหัด 6</p>
                    </div>
                </div>
            </div>
        </a>
        </div>
    </section>

    <!-- Section 5: Curriculum -->
    <section id="curriculum" class="py-24 relative">
        <div class="container mx-auto px-4">
            <div class="text-center mb-16">
                <h2 class="text-4xl font-bold mb-4">หลักสูตรสมบูรณ์</h2>
                <p class="text-gray-400">รายวิชาที่ออกแบบมาให้ครบถ้วนตามหลักสูตรมาตรฐานศิลปะ</p>
            </div>

            <div class="max-w-4xl mx-auto relative">
                <a href="https://lersros-lookchin.my.canva.site/1">
                <!-- Timeline Line -->
                <div class="absolute left-0 md:left-1/2 transform md:-translate-x-1/2 top-0 bottom-0 w-1 bg-gradient-to-b from-brand-accent via-purple-500 to-transparent opacity-30"></div>
                
                <!-- Module 1 -->
                <div class="flex flex-col md:flex-row items-center mb-12 relative group">
                    <div class="w-full md:w-1/2 md:pr-12 pl-8 md:pl-0 text-left md:text-right order-1">
                        <h3 class="text-2xl font-bold text-white group-hover:text-brand-accent transition">บทที่ 1: แนะนำศิลปะและการรับรู้</h3>
                        <p class="text-gray-400 mt-2">ความหมายของศิลปะ การออกแบบ และทัศนคติของศิลปิน</p>
                        <div class="mt-2 inline-block px-3 py-1 bg-green-500/20 text-green-400 text-xs rounded">พร้อมเรียน</div>
                    </a>
                    </div>
                    <div class="w-10 h-10 rounded-full bg-brand-dark border-4 border-brand-accent z-10 absolute left-0 md:left-1/2 transform md:-translate-x-1/2 shadow-[0_0_15px_#00f260]"></div>
                    <div class="w-full md:w-1/2 md:pl-12 order-2"></div>
                </div>

                <!-- Module 2 -->
                 <a href="https://lersros-lookchin.my.canva.site/archival-palette">
                <div class="flex flex-col md:flex-row items-center mb-12 relative group">
                    <div class="w-full md:w-1/2 md:pr-12 order-2 md:order-1"></div>
                    <div class="w-10 h-10 rounded-full bg-brand-dark border-4 border-brand-accent2 z-10 absolute left-0 md:left-1/2 transform md:-translate-x-1/2 shadow-[0_0_15px_#0575E6]"></div>
                    <div class="w-full md:w-1/2 md:pl-12 pl-8 order-1 md:order-2 text-left">
                        <h3 class="text-2xl font-bold text-white group-hover:text-brand-accent2 transition">บทที่ 2: เส้น (Line) และรูปทรง (Shape)</h3>
                        <p class="text-gray-400 mt-2">ประเภทของเส้น ลักษณะเส้น และการใช้เส้นสร้างรูปทรงเรขาคณิต</p>
                        <div class="mt-2 inline-block px-3 py-1 bg-blue-500/20 text-blue-400 text-xs rounded">พร้อมเรียน</div>
                    </div>
                </div>
                 </a>

                <!-- Module 3 -->
                 <a href="https://lersros-lookchin.my.canva.site/dahaaz35ibu">
                <div class="flex flex-col md:flex-row items-center mb-12 relative group">
                    <div class="w-full md:w-1/2 md:pr-12 pl-8 md:pl-0 text-left md:text-right order-1">
                        <h3 class="text-2xl font-bold text-white group-hover:text-yellow-400 transition">บทที่ 3: ทฤษฎีสี (Color Theory)</h3>
                        <p class="text-gray-400 mt-2">วงสี สีเฉพาะ สีอุตสาหะ และการจับคู่สี</p>
                        <div class="mt-2 inline-block px-3 py-1 bg-green-500/20 text-green-400 text-xs rounded">พร้อมเรียน</div>
                    </div>
                    <div class="w-10 h-10 rounded-full bg-brand-dark border-4 border-yellow-400 z-10 absolute left-0 md:left-1/2 transform md:-translate-x-1/2 shadow-[0_0_15px_orange]"></div>
                    <div class="w-full md:w-1/2 md:pl-12 order-2"></div>
                </div>
                 </a>

                <!-- Module 4 -->
                 <a href="https://lersros-lookchin.my.canva.site/4">
                <div class="flex flex-col md:flex-row items-center mb-12 relative group">
                    <div class="w-full md:w-1/2 md:pr-12 order-2 md:order-1"></div>
                    <div class="w-10 h-10 rounded-full bg-brand-dark border-4 border-pink-500 z-10 absolute left-0 md:left-1/2 transform md:-translate-x-1/2 shadow-[0_0_15px_pink]"></div>
                    <div class="w-full md:w-1/2 md:pl-12 pl-8 order-1 md:order-2 text-left">
                        <h3 class="text-2xl font-bold text-white group-hover:text-pink-500 transition">บทที่ 4: พื้นผิว (Texture) และเนื้อ (Value)</h3>
                        <p class="text-gray-400 mt-2">การสร้างเนื้อผิวเทียม (Visual Texture) และแสงเงา</p>
                        <div class="mt-2 inline-block px-3 py-1 bg-green-500/20 text-green-400 text-xs rounded">พร้อมเรียน</div>
                    </div>
                </div>
                 </a>
                 <!-- Module 5 -->
                  <a href="https://krittayakorn.wordpress.com/2013/03/20/shape-and-form/">
                 <div class="flex flex-col md:flex-row items-center mb-12 relative group">
                    <div class="w-full md:w-1/2 md:pr-12 pl-8 md:pl-0 text-left md:text-right order-1">
                        <h3 class="text-2xl font-bold text-white group-hover:text-purple-400 transition">บทที่ 5: องค์ประกอบจัดวาง (Space & Balance)</h3>
                        <p class="text-gray-400 mt-2">ความสมดุล จัตุรัส จัตุรัสทอง และอวกาศลบ</p>
                        <div class="mt-2 inline-block px-3 py-1 bg-green-500/20 text-green-400 text-xs rounded">พร้อมเรียน</div>
                    </div>
                    <div class="w-10 h-10 rounded-full bg-brand-dark border-4 border-purple-500 z-10 absolute left-0 md:left-1/2 transform md:-translate-x-1/2 shadow-[0_0_15px_purple]"></div>
                    <div class="w-full md:w-1/2 md:pl-12 order-2"></div>
                </div>
            </div>
        </div>
                  </a>
    </section>

    <!-- Footer (Updated) -->
    <footer class="py-12 bg-black border-t border-white/5 relative z-10">
        <div class="container mx-auto px-4 flex flex-col md:flex-row justify-between items-center">
            <div class="mb-6 md:mb-0">
                <h2 class="text-2xl font-bold mb-2">AI<span class="text-brand-accent">TRANSFORMATION</span></h2>
                <p class="text-gray-500 text-sm">เรียนรู้ศิลปะแบบใหม่ ด้วยระบบปฏิสัมพันธ์</p>
            </div>
            <div class="flex space-x-6">
                <a href="https://www.facebook.com/share/1E3Vi8uQE1/" class="w-10 h-10 rounded-full bg-white/5 flex items-center justify-center hover:bg-brand-accent hover:text-black transition-all"><i class="fab fa-facebook-f"></i></a>
                <a href="https://www.instagram.com/zvxzzzzxzzzzzzzzzzzzzzzzzzzzzz/" class="w-10 h-10 rounded-full bg-white/5 flex items-center justify-center hover:bg-brand-accent hover:text-black transition-all"><i class="fab fa-instagram"></i></a>
                <a href="https://www.youtube.com/@fitxfidal7" class="w-10 h-10 rounded-full bg-white/5 flex items-center justify-center hover:bg-brand-accent hover:text-black transition-all"><i class="fab fa-youtube"></i></a>
            </div>
        </div>
        <!-- Copyright Removed as requested -->
    </footer>

    <!-- Scripts -->
    <script>
        // Canvas Background Animation
        const canvas = document.getElementById('bg-canvas');
        const ctx = canvas.getContext('2d');
        let width, height;
        let particles = [];
        
        function resize() {
            width = canvas.width = window.innerWidth;
            height = canvas.height = window.innerHeight;
        }
        window.addEventListener('resize', resize);
        resize();

        class Particle {
            constructor() {
                this.x = Math.random() * width;
                this.y = Math.random() * height;
                this.size = Math.random() * 20 + 5;
                this.speedX = (Math.random() - 0.5) * 0.5;
                this.speedY = (Math.random() - 0.5) * 0.5;
                this.color = `hsla(${Math.random() * 360}, 70%, 50%, ${Math.random() * 0.1})`;
                this.shape = Math.random() > 0.5 ? 'circle' : 'square';
                this.angle = 0;
                this.spin = (Math.random() - 0.5) * 0.02;
            }

            update() {
                this.x += this.speedX;
                this.y += this.speedY;
                this.angle += this.spin;
                if (this.x > width || this.x < 0) this.speedX *= -1;
                if (this.y > height || this.y < 0) this.speedY *= -1;
            }

            draw() {
                ctx.save();
                ctx.translate(this.x, this.y);
                ctx.rotate(this.angle);
                ctx.fillStyle = this.color;
                ctx.shadowBlur = 15;
                ctx.shadowColor = this.color;
                if (this.shape === 'circle') {
                    ctx.beginPath();
                    ctx.arc(0, 0, this.size, 0, Math.PI * 2);
                    ctx.fill();
                } else {
                    ctx.fillRect(-this.size/2, -this.size/2, this.size, this.size);
                }
                ctx.restore();
            }
        }

        for (let i = 0; i < 40; i++) {
            particles.push(new Particle());
        }

        function animate() {
            ctx.clearRect(0, 0, width, height);
            ctx.strokeStyle = 'rgba(255, 255, 255, 0.03)';
            ctx.lineWidth = 1;
            for (let i = 0; i < particles.length; i++) {
                for (let j = i; j < particles.length; j++) {
                    const dx = particles[i].x - particles[j].x;
                    const dy = particles[i].y - particles[j].y;
                    const distance = Math.sqrt(dx * dx + dy * dy);
                    if (distance < 150) {
                        ctx.beginPath();
                        ctx.moveTo(particles[i].x, particles[i].y);
                        ctx.lineTo(particles[j].x, particles[j].y);
                        ctx.stroke();
                    }
                }
            }
            particles.forEach(p => {
                p.update();
                p.draw();
            });
            requestAnimationFrame(animate);
        }
        animate();

        // Color Tool Logic
        let currentHarmony = 'analogous';
        const swatches = document.querySelectorAll('.color-swatch');

        function setHarmony(type) {
            currentHarmony = type;
            const slider = document.querySelector('input[type="range"]');
            updateColors(slider.value);
        }

        function updateColors(hue) {
            const h = parseInt(hue);
            let colors = [];
            if (currentHarmony === 'analogous') {
                colors = [`hsl(${h}, 70%, 60%)`, `hsl(${(h + 30) % 360}, 70%, 60%)`, `hsl(${(h + 60) % 360}, 70%, 60%)`];
            } else if (currentHarmony === 'complementary') {
                colors = [`hsl(${h}, 80%, 55%)`, `hsl(${(h + 30) % 360}, 80%, 40%)`, `hsl(${(h + 180) % 360}, 80%, 55%)`];
            }
            swatches.forEach((swatch, index) => {
                if(colors[index]) {
                    swatch.style.backgroundColor = colors[index];
                }
            });
        }
        updateColors(0);

        // UI Interactions
        const cursor = document.getElementById('cursor');
        document.addEventListener('mousemove', (e) => {
            cursor.style.left = e.clientX + 'px';
            cursor.style.top = e.clientY + 'px';
        });

        const navbar = document.getElementById('navbar');
        window.addEventListener('scroll', () => {
            if (window.scrollY > 50) {
                navbar.classList.add('py-2');
                navbar.classList.remove('py-4');
                navbar.querySelector('.glass-panel').classList.add('bg-black/80');
            } else {
                navbar.classList.add('py-4');
                navbar.classList.remove('py-2');
                navbar.querySelector('.glass-panel').classList.remove('bg-black/80');
            }
        });

        const observerOptions = { threshold: 0.1 };
        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.style.opacity = '1';
                    entry.target.style.transform = 'translateY(0)';
                }
            });
        }, observerOptions);

        document.querySelectorAll('.glass-card, .gallery-item').forEach((card, index) => {
            card.style.opacity = '0';
            card.style.transform = 'translateY(50px)';
            card.style.transition = `all 0.6s ease-out ${index * 0.1}s`;
            observer.observe(card);
        });

    </script>
</body>
</html>
# my-website
