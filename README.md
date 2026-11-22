[index.html](https://github.com/user-attachments/files/35227255/index.html)
<!DOCTYPE html>
<html lang="ar" dir="rtl" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>رفيق الفهم الذكي | مساعد دراسة وفهم الفيديوهات المتكامل</title>
    <!-- خط تجوال العربي -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@400;500;700;800;900&display=swap" rel="stylesheet">
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- أيقونات Lucide -->
    <script src="https://unpkg.com/lucide@latest"></script>
    <!-- مكتبة Marked لتحويل Markdown -->
    <script src="https://cdn.jsdelivr.net/npm/marked/marked.min.js"></script>

    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Tajawal', 'sans-serif'],
                    }
                }
            }
        }
    </script>
    <style>
        body {
            font-family: 'Tajawal', sans-serif;
            background-color: #060a14;
            color: #f8fafc;
        }

        /* تنسيق محتوى Markdown */
        .prose-custom h1, .prose-custom h2, .prose-custom h3 {
            color: #38bdf8;
            font-weight: 800;
            margin-top: 1.35rem;
            margin-bottom: 0.7rem;
        }
        .prose-custom h2 { font-size: 1.25rem; border-bottom: 1px solid #1e293b; padding-bottom: 0.4rem; }
        .prose-custom h3 { font-size: 1.08rem; color: #7dd3fc; }
        .prose-custom p { margin-bottom: 0.9rem; line-height: 1.85; color: #e2e8f0; }
        .prose-custom ul, .prose-custom ol { margin-bottom: 1rem; padding-right: 1.4rem; }
        .prose-custom ul { list-style-type: disc; }
        .prose-custom ol { list-style-type: decimal; }
        .prose-custom li { margin-bottom: 0.45rem; line-height: 1.75; color: #cbd5e1; }
        .prose-custom strong { color: #ffffff; font-weight: 700; }
        .prose-custom blockquote {
            border-right: 4px solid #38bdf8;
            background: rgba(56, 189, 248, 0.08);
            padding: 0.75rem 1rem;
            border-radius: 0.75rem;
            margin: 1rem 0;
            color: #bae6fd;
        }

        /* بطاقات الاستذكار ثلاثية الأبعاد (3D Flip) */
        .perspective-1000 { perspective: 1000px; }
        .transform-style-3d { transform-style: preserve-3d; transition: transform 0.6s cubic-bezier(0.4, 0.2, 0.2, 1); }
        .backface-hidden { backface-visibility: hidden; -webkit-backface-visibility: hidden; }
        .rotate-y-180 { transform: rotateY(180deg); }

        /* شريط التمرير */
        ::-webkit-scrollbar { width: 7px; height: 7px; }
        ::-webkit-scrollbar-track { background: #0f172a; }
        ::-webkit-scrollbar-thumb { background: #334155; border-radius: 4px; }
        ::-webkit-scrollbar-thumb:hover { background: #475569; }
        .no-scrollbar::-webkit-scrollbar { display: none; }
        .no-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }

        /* عقد الخريطة الذهنية */
        .mindmap-node { cursor: pointer; transition: filter 0.2s ease; }
        .mindmap-node:hover { filter: brightness(1.18); }

        /* تنسيق الطباعة وتصدير PDF النظيف */
        @media print {
            body { background: #ffffff !important; color: #0f172a !important; }
            header, #inputSectionCard, #tabsNavBar, #toast, .no-print { display: none !important; }
            #mainLayout { display: block !important; padding: 0 !important; }
            #workspaceColumn, #sidebarColumn { width: 100% !important; max-width: 100% !important; margin-bottom: 1.5rem !important; }
            .print-card { background: #ffffff !important; border: 1px solid #cbd5e1 !important; box-shadow: none !important; color: #0f172a !important; }
            #printHeader, #printFullReport { display: block !important; }
            .prose-custom h1, .prose-custom h2, .prose-custom h3 { color: #0284c7 !important; }
            .prose-custom p, .prose-custom li, .prose-custom strong { color: #1e293b !important; }
        }
    </style>
</head>
<body class="min-h-screen flex flex-col bg-gradient-to-br from-[#060a14] via-[#0b1222] to-[#060a14] selection:bg-sky-500/30 selection:text-sky-200">

    <!-- إشعار عائم (Toast) بديل عن alert() -->
    <div id="toast" class="fixed bottom-6 left-1/2 -translate-x-1/2 z-50 hidden items-center gap-3 px-5 py-3.5 rounded-2xl shadow-2xl border backdrop-blur-md transition-all duration-300">
        <i id="toastIcon" data-lucide="info" class="w-5 h-5 flex-shrink-0"></i>
        <span id="toastMessage" class="text-sm font-bold"></span>
    </div>

    <!-- الشريط العلوي -->
    <header class="border-b border-slate-800/90 bg-slate-950/85 backdrop-blur-md sticky top-0 z-30">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 py-3.5 flex flex-wrap items-center justify-between gap-4">
            <div class="flex items-center gap-3">
                <div class="w-11 h-11 rounded-2xl bg-gradient-to-tr from-sky-500 via-blue-600 to-indigo-600 flex items-center justify-center shadow-lg shadow-sky-500/25">
                    <i data-lucide="brain-circuit" class="w-6 h-6 text-white"></i>
                </div>
                <div>
                    <div class="flex items-center gap-2">
                        <h1 class="text-xl sm:text-2xl font-black bg-gradient-to-l from-white via-sky-200 to-sky-400 bg-clip-text text-transparent">
                            رفيق الفهم الذكي
                        </h1>
                        <span class="px-2.5 py-0.5 text-[11px] font-extrabold rounded-full bg-emerald-500/15 text-emerald-300 border border-emerald-500/30">
                            تفاعلي 100%
                        </span>
                    </div>
                    <p class="text-xs text-slate-400 hidden sm:block">مساعد دراسة وفهم الفيديوهات والمحاضرات بالذكاء الاصطناعي</p>
                </div>
            </div>

            <div class="flex items-center gap-2.5">
                <button onclick="loadReadyDemoExample()" class="flex items-center gap-2 px-4 py-2.5 rounded-xl bg-amber-500/15 hover:bg-amber-500/25 border border-amber-500/40 text-amber-300 text-xs sm:text-sm font-extrabold transition cursor-pointer">
                    <i data-lucide="sparkles" class="w-4 h-4"></i>
                    <span>جرّب بمثال عملي جاهز</span>
                </button>
                <button onclick="exportAndPrintReport()" class="flex items-center gap-2 px-4 py-2.5 rounded-xl bg-slate-800 hover:bg-slate-700 border border-slate-700 text-slate-200 text-xs sm:text-sm font-bold transition cursor-pointer">
                    <i data-lucide="printer" class="w-4 h-4 text-sky-400"></i>
                    <span class="hidden sm:inline">تصدير وطباعة التقرير</span>
                </button>
            </div>
        </div>
    </header>

    <!-- الحاوية الرئيسية -->
    <main id="mainLayout" class="flex-1 max-w-7xl w-full mx-auto px-4 sm:px-6 py-6 space-y-6">

        <!-- 1. قسم الإدخال الذكي في الأعلى -->
        <section id="inputSectionCard" class="bg-slate-900/95 border border-slate-800 rounded-3xl p-5 sm:p-7 shadow-2xl">
            <div class="flex flex-wrap items-center justify-between gap-3 mb-5">
                <div class="flex items-center gap-2.5">
                    <div class="w-9 h-9 rounded-xl bg-sky-500/15 text-sky-400 flex items-center justify-center">
                        <i data-lucide="video" class="w-5 h-5"></i>
                    </div>
                    <div>
                        <h2 class="text-base sm:text-lg font-extrabold text-white">إدخال الفيديو أو المحاضرة للتحليل</h2>
                        <p class="text-xs text-slate-400">أدخلي رابط يوتيوب أو الصقي نص الفيديو/التفريغ الصوتي واختاري مستوى الشرح</p>
                    </div>
                </div>
                <button onclick="clearInputFields()" class="text-xs text-slate-400 hover:text-rose-400 flex items-center gap-1 font-bold transition cursor-pointer">
                    <i data-lucide="eraser" class="w-3.5 h-3.5"></i> مسح الحقول
                </button>
            </div>

            <div class="grid grid-cols-1 lg:grid-cols-12 gap-5">
                <!-- حقل الرابط + معاينة الفيديو -->
                <div class="lg:col-span-5 space-y-3">
                    <label for="videoUrlInput" class="block text-xs font-bold text-slate-300">
                        1. رابط الفيديو (YouTube أو أي رابط):
                    </label>
                    <div class="relative">
                        <input type="url" id="videoUrlInput" oninput="handleVideoUrlChange()" placeholder="https://www.youtube.com/watch?v=..."
                            class="w-full bg-slate-950 border border-slate-700/80 focus:border-sky-500 rounded-2xl py-3 pr-3.5 pl-10 text-sm text-white placeholder-slate-500 outline-none transition dir-ltr text-left">
                        <button onclick="pasteToField('videoUrlInput')" title="لصق من الحافظة" class="absolute left-2.5 top-1/2 -translate-y-1/2 p-1.5 rounded-lg text-slate-400 hover:text-sky-400 hover:bg-slate-800 transition cursor-pointer">
                            <i data-lucide="clipboard-paste" class="w-4 h-4"></i>
                        </button>
                    </div>

                    <!-- بطاقة معاينة يوتيوب التلقائية -->
                    <div id="youtubePreviewBox" class="hidden bg-slate-950 border border-slate-800 rounded-2xl p-3 flex items-center gap-3">
                        <img id="youtubeThumbImg" src="" alt="صورة الفيديو" class="w-24 h-16 object-cover rounded-xl border border-slate-700 flex-shrink-0">
                        <div class="min-w-0 flex-1">
                            <span class="inline-flex items-center gap-1 text-[10px] font-bold text-emerald-400 bg-emerald-500/10 px-2 py-0.5 rounded-md mb-1">
                                <i data-lucide="check-circle-2" class="w-3 h-3"></i> تم التعرف على فيديو يوتيوب
                            </span>
                            <p id="youtubeTitleText" class="text-xs font-bold text-slate-200 line-clamp-2 leading-snug">جاري جلب العنوان...</p>
                        </div>
                    </div>

                    <!-- قائمة اختيار مستوى التحليل -->
                    <div class="pt-1">
                        <label for="analysisLevelSelect" class="block text-xs font-bold text-slate-300 mb-2">
                            2. مستوى وأسلوب التحليل المطلوب:
                        </label>
                        <select id="analysisLevelSelect" class="w-full bg-slate-950 border border-slate-700/80 focus:border-sky-500 rounded-2xl py-3 px-3.5 text-sm font-bold text-white outline-none transition cursor-pointer">
                            <option value="simple">شرح مبسط ومفصل مع أمثلة عملية</option>
                            <option value="academic">شرح أكاديمي متعمق وتحليل منهجي</option>
                            <option value="summary">ملخص سريع ونقاط أساسية (الزبدة)</option>
                        </select>
                    </div>
                </div>

                <!-- حقل نص الفيديو / التفريغ الصوتي -->
                <div class="lg:col-span-7 flex flex-col">
                    <div class="flex items-center justify-between mb-2">
                        <label for="transcriptTextInput" class="block text-xs font-bold text-slate-300">
                            3. نص الفيديو أو التفريغ الصوتي أو الملاحظات (اختياري مع الرابط، أو أساسي لأي نص):
                        </label>
                        <button onclick="pasteToField('transcriptTextInput')" class="text-xs text-sky-400 hover:text-sky-300 flex items-center gap-1 font-bold cursor-pointer">
                            <i data-lucide="clipboard-paste" class="w-3.5 h-3.5"></i> لصق النص
                        </button>
                    </div>
                    <textarea id="transcriptTextInput" rows="5" placeholder="الصقي هنا نص الفيديو (Transcript)، أو محتوى محاضرة، أو أي مقال تعليمي ليتم تحليله وبناء الخريطة الذهنية والاختبارات والمصطلحات منه..."
                        class="flex-1 w-full bg-slate-950 border border-slate-700/80 focus:border-sky-500 rounded-2xl p-3.5 text-sm text-white placeholder-slate-500 outline-none transition resize-y leading-relaxed"></textarea>
                </div>
            </div>

            <!-- أزرار التشغيل الرئيسية -->
            <div class="mt-5 pt-4 border-t border-slate-800/80 flex flex-col sm:flex-row items-stretch sm:items-center gap-3">
                <button id="startAnalysisBtn" onclick="runDeepAnalysis()" class="flex-1 py-3.5 px-6 rounded-2xl bg-gradient-to-l from-sky-500 via-blue-600 to-indigo-600 hover:from-sky-400 hover:to-indigo-500 text-white font-extrabold text-sm sm:text-base shadow-lg shadow-sky-500/25 flex items-center justify-center gap-2.5 transition active:scale-[0.99] cursor-pointer">
                    <i data-lucide="wand-2" class="w-5 h-5"></i>
                    <span>ابدأ التحليل والفهم العميق</span>
                </button>

                <button onclick="loadReadyDemoExample()" class="py-3.5 px-6 rounded-2xl bg-amber-500/15 hover:bg-amber-500/25 border-2 border-amber-500/50 text-amber-300 font-extrabold text-sm sm:text-base flex items-center justify-center gap-2 transition active:scale-[0.99] cursor-pointer">
                    <i data-lucide="play-circle" class="w-5 h-5"></i>
                    <span>جرّب بمثال عملي جاهز</span>
                </button>
            </div>
        </section>

        <!-- الشبكة السفلية: مساحة الفهم العميق (8 أعمدة) + الشريط الجانبي الدائم (4 أعمدة) -->
        <div class="grid grid-cols-1 lg:grid-cols-12 gap-6 items-start">

            <!-- 2. مساحة الفهم العميق (8 تبويبات تفاعلية حقيقية) -->
            <section id="workspaceColumn" class="lg:col-span-8 bg-slate-900/95 border border-slate-800 rounded-3xl p-5 sm:p-6 shadow-2xl min-h-[600px] flex flex-col print-card">

                <!-- ترويسة تظهر عند الطباعة فقط -->
                <div id="printHeader" class="hidden mb-6 pb-4 border-b-2 border-slate-300">
                    <h1 class="text-2xl font-black text-sky-700">تقرير الدراسة الشامل - رفيق الفهم الذكي</h1>
                    <p id="printReportTitle" class="text-base font-bold text-slate-800 mt-1"></p>
                </div>

                <!-- مؤشر التحميل (Spinner) -->
                <div id="loadingSpinnerBox" class="hidden flex-1 flex-col items-center justify-center text-center py-20 px-4">
                    <div class="relative w-20 h-20 mb-5">
                        <div class="absolute inset-0 rounded-full border-4 border-slate-800"></div>
                        <div class="absolute inset-0 rounded-full border-4 border-sky-500 border-t-transparent animate-spin"></div>
                        <i data-lucide="brain" class="w-8 h-8 text-sky-400 absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 animate-pulse"></i>
                    </div>
                    <h3 class="text-lg font-extrabold text-white mb-2">جاري تحليل المحتوى وبناء أدوات الفهم الثمانية...</h3>
                    <p class="text-xs sm:text-sm text-slate-400 max-w-md leading-relaxed">
                        يتم الآن توليد الشرح، تبسيط ELI5، الخريطة الذهنية البصرية، كاشف النقاط العمياء، الاختبار، بطاقات الاستذكار، القاموس، وخطة التطبيق.
                    </p>
                </div>

                <!-- شاشة الترحيب قبل التحليل -->
                <div id="welcomeEmptyBox" class="flex-1 flex flex-col items-center justify-center text-center py-14 px-4">
                    <div class="w-20 h-20 rounded-3xl bg-sky-500/10 border border-sky-500/25 flex items-center justify-center text-sky-400 mb-5">
                        <i data-lucide="layers-3" class="w-10 h-10"></i>
                    </div>
                    <h3 class="text-xl font-extrabold text-white mb-2">مساحة الفهم العميق جاهزة</h3>
                    <p class="text-sm text-slate-400 max-w-lg leading-relaxed mb-6">
                        أدخلي رابط فيديو أو نصاً في الأعلى واضغطي <strong>"ابدأ التحليل والفهم العميق"</strong>، أو اضغطي على الزر أدناه لتجربة جميع التبويبات والأدوات التفاعلية فوراً بمثال متكامل:
                    </p>
                    <button onclick="loadReadyDemoExample()" class="px-6 py-3 rounded-2xl bg-gradient-to-l from-amber-500 to-orange-500 hover:from-amber-400 hover:to-orange-400 text-slate-950 font-black text-sm shadow-lg shadow-amber-500/20 flex items-center gap-2 transition cursor-pointer">
                        <i data-lucide="sparkles" class="w-4 h-4"></i>
                        <span>تعبئة وتجربة المثال العملي الجاهز الآن</span>
                    </button>
                </div>

                <!-- محتوى مساحة الفهم العميق النشط -->
                <div id="activeWorkspaceBox" class="hidden flex-1 flex flex-col">

                    <!-- عنوان الفيديو الحالي + أزرار سريعة -->
                    <div class="flex flex-wrap items-center justify-between gap-3 pb-4 mb-4 border-b border-slate-800">
                        <div class="min-w-0 flex-1">
                            <span class="text-[11px] font-extrabold text-sky-400">المحتوى قيد الدراسة الآن:</span>
                            <h2 id="currentStudyTitle" class="text-base sm:text-lg font-black text-white truncate">عنوان الفيديو</h2>
                        </div>
                        <span id="dataModeBadge" class="px-3 py-1 rounded-full text-xs font-extrabold bg-sky-500/15 text-sky-300 border border-sky-500/30">
                            تحليل AI حي
                        </span>
                    </div>

                    <!-- شريط التبويبات الثمانية التفاعلي -->
                    <nav id="tabsNavBar" class="flex items-center gap-1.5 overflow-x-auto pb-2.5 mb-5 border-b border-slate-800/80 no-scrollbar">
                        <button onclick="activateTab('explain')" id="tabBtn-explain" class="study-tab-btn flex items-center gap-1.5 px-3.5 py-2.5 rounded-xl text-xs font-extrabold whitespace-nowrap transition cursor-pointer">
                            <i data-lucide="book-open" class="w-4 h-4"></i>
                            <span>الشرح والتبسيط (ELI5)</span>
                        </button>
                        <button onclick="activateTab('mindmap')" id="tabBtn-mindmap" class="study-tab-btn flex items-center gap-1.5 px-3.5 py-2.5 rounded-xl text-xs font-extrabold whitespace-nowrap transition cursor-pointer">
                            <i data-lucide="network" class="w-4 h-4"></i>
                            <span>الخريطة الذهنية</span>
                            <span id="badge-mindmap" class="px-1.5 py-0.2 rounded-md text-[10px] bg-slate-800 text-slate-300">0</span>
                        </button>
                        <button onclick="activateTab('blindspots')" id="tabBtn-blindspots" class="study-tab-btn flex items-center gap-1.5 px-3.5 py-2.5 rounded-xl text-xs font-extrabold whitespace-nowrap transition cursor-pointer">
                            <i data-lucide="eye-off" class="w-4 h-4"></i>
                            <span>كاشف النقاط العمياء</span>
                            <span id="badge-blindspots" class="px-1.5 py-0.2 rounded-md text-[10px] bg-slate-800 text-slate-300">0</span>
                        </button>
                        <button onclick="activateTab('quiz')" id="tabBtn-quiz" class="study-tab-btn flex items-center gap-1.5 px-3.5 py-2.5 rounded-xl text-xs font-extrabold whitespace-nowrap transition cursor-pointer">
                            <i data-lucide="help-circle" class="w-4 h-4"></i>
                            <span>اختبار الفهم</span>
                            <span id="badge-quiz" class="px-1.5 py-0.2 rounded-md text-[10px] bg-slate-800 text-slate-300">0</span>
                        </button>
                        <button onclick="activateTab('flashcards')" id="tabBtn-flashcards" class="study-tab-btn flex items-center gap-1.5 px-3.5 py-2.5 rounded-xl text-xs font-extrabold whitespace-nowrap transition cursor-pointer">
                            <i data-lucide="layers" class="w-4 h-4"></i>
                            <span>بطاقات الاستذكار</span>
                            <span id="badge-flashcards" class="px-1.5 py-0.2 rounded-md text-[10px] bg-slate-800 text-slate-300">0</span>
                        </button>
                        <button onclick="activateTab('glossary')" id="tabBtn-glossary" class="study-tab-btn flex items-center gap-1.5 px-3.5 py-2.5 rounded-xl text-xs font-extrabold whitespace-nowrap transition cursor-pointer">
                            <i data-lucide="languages" class="w-4 h-4"></i>
                            <span>قاموس المصطلحات</span>
                            <span id="badge-glossary" class="px-1.5 py-0.2 rounded-md text-[10px] bg-slate-800 text-slate-300">0</span>
                        </button>
                        <button onclick="activateTab('actionplan')" id="tabBtn-actionplan" class="study-tab-btn flex items-center gap-1.5 px-3.5 py-2.5 rounded-xl text-xs font-extrabold whitespace-nowrap transition cursor-pointer">
                            <i data-lucide="check-square" class="w-4 h-4"></i>
                            <span>خطة التطبيق</span>
                            <span id="badge-actionplan" class="px-1.5 py-0.2 rounded-md text-[10px] bg-slate-800 text-slate-300">0</span>
                        </button>
                        <button onclick="activateTab('chat')" id="tabBtn-chat" class="study-tab-btn flex items-center gap-1.5 px-3.5 py-2.5 rounded-xl text-xs font-extrabold whitespace-nowrap transition cursor-pointer">
                            <i data-lucide="messages-square" class="w-4 h-4"></i>
                            <span>اسأل الفيديو</span>
                        </button>
                    </nav>

                    <!-- التبويب 1: الشرح والتبسيط (ELI5) -->
                    <div id="panel-explain" class="study-tab-panel space-y-5 flex-1">
                        <!-- شريط أدوات الشرح -->
                        <div class="flex flex-wrap items-center justify-between gap-2.5 p-3.5 rounded-2xl bg-slate-950 border border-slate-800 no-print">
                            <button id="toggleEli5Btn" onclick="toggleEli5Box()" class="flex items-center gap-2 px-4 py-2 rounded-xl bg-amber-500/15 hover:bg-amber-500/25 border border-amber-500/40 text-amber-300 text-xs sm:text-sm font-extrabold transition cursor-pointer">
                                <i data-lucide="baby" class="w-4 h-4"></i>
                                <span id="eli5BtnLabel">بسّطها لي كأني مبتدئة (ELI5)</span>
                            </button>

                            <div class="flex items-center gap-2">
                                <button id="speakBtn" onclick="toggleArabicSpeech()" class="flex items-center gap-1.5 px-3.5 py-2 rounded-xl bg-slate-800 hover:bg-slate-700 border border-slate-700 text-slate-200 text-xs font-bold transition cursor-pointer">
                                    <i id="speakIcon" data-lucide="volume-2" class="w-4 h-4 text-sky-400"></i>
                                    <span id="speakLabel">استماع صوتي</span>
                                </button>
                                <button onclick="copyExplanationText()" class="flex items-center gap-1.5 px-3.5 py-2 rounded-xl bg-slate-800 hover:bg-slate-700 border border-slate-700 text-slate-200 text-xs font-bold transition cursor-pointer">
                                    <i data-lucide="copy" class="w-4 h-4 text-emerald-400"></i>
                                    <span>نسخ الشرح</span>
                                </button>
                            </div>
                        </div>

                        <!-- صندوق التبسيط الفائق ELI5 (يظهر عند النقر) -->
                        <div id="eli5ResultBox" class="hidden p-5 rounded-2xl bg-gradient-to-l from-amber-500/15 via-orange-500/10 to-slate-950 border-2 border-amber-500/40 space-y-2.5">
                            <div class="flex items-center justify-between">
                                <h4 class="text-sm sm:text-base font-black text-amber-300 flex items-center gap-2">
                                    <i data-lucide="sparkles" class="w-5 h-5"></i>
                                    <span>الشرح المبسط جداً بتشبيهات يومية (ELI5)</span>
                                </h4>
                                <button onclick="toggleEli5Box()" class="text-xs text-slate-400 hover:text-white font-bold cursor-pointer">إخفاء</button>
                            </div>
                            <div id="eli5ContentText" class="prose-custom text-sm leading-relaxed text-amber-100"></div>
                        </div>

                        <!-- بطاقة الفكرة العامة -->
                        <div class="p-4 rounded-2xl bg-sky-500/10 border border-sky-500/30">
                            <span class="text-xs font-extrabold text-sky-400 block mb-1">الفكرة العامة باختصار:</span>
                            <p id="generalIdeaText" class="text-sm sm:text-base font-bold text-white leading-relaxed"></p>
                        </div>

                        <!-- الشرح المفصل -->
                        <div id="detailedExplanationOutput" class="prose-custom text-sm sm:text-base leading-relaxed"></div>
                    </div>

                    <!-- التبويب 2: الخريطة الذهنية البصرية التفاعلية -->
                    <div id="panel-mindmap" class="study-tab-panel hidden flex-1 flex flex-col">
                        <div class="flex flex-wrap items-center justify-between gap-3 mb-4">
                            <div>
                                <h3 class="text-base font-extrabold text-white">الخريطة الذهنية البصرية التفاعلية</h3>
                                <p class="text-xs text-slate-400">اضغطي على أي عقدة رئيسية لطيّ أو توسيع تفرعاتها، واستخدمي أزرار التكبير والتصغير</p>
                            </div>
                            <div class="flex items-center gap-1.5 bg-slate-950 p-1.5 rounded-xl border border-slate-800">
                                <button onclick="adjustMindMapZoom(0.15)" title="تكبير (+)" class="p-2 rounded-lg hover:bg-slate-800 text-slate-200 transition cursor-pointer">
                                    <i data-lucide="zoom-in" class="w-4 h-4"></i>
                                </button>
                                <button onclick="adjustMindMapZoom(-0.15)" title="تصغير (-)" class="p-2 rounded-lg hover:bg-slate-800 text-slate-200 transition cursor-pointer">
                                    <i data-lucide="zoom-out" class="w-4 h-4"></i>
                                </button>
                                <button onclick="resetMindMap()" class="px-3 py-1.5 rounded-lg hover:bg-slate-800 text-xs font-bold text-sky-400 transition cursor-pointer">
                                    إعادة ضبط العرض
                                </button>
                                <button onclick="toggleAllMindMapNodes()" class="px-3 py-1.5 rounded-lg bg-sky-500/15 hover:bg-sky-500/25 text-xs font-bold text-sky-300 transition cursor-pointer">
                                    طي / توسيع الكل
                                </button>
                            </div>
                        </div>

                        <div class="flex-1 min-h-[440px] bg-slate-950 border border-slate-800 rounded-2xl overflow-auto flex items-center justify-center p-3">
                            <svg id="mindmapSvgCanvas" class="w-full h-full min-w-[780px] min-h-[450px] select-none transition-transform duration-200 origin-center"></svg>
                        </div>
                    </div>

                    <!-- التبويب 3: كاشف النقاط العمياء -->
                    <div id="panel-blindspots" class="study-tab-panel hidden flex-1 space-y-6">
                        <div class="p-4 rounded-2xl bg-gradient-to-l from-rose-500/15 via-amber-500/10 to-slate-950 border border-rose-500/30">
                            <h3 class="text-base font-extrabold text-white flex items-center gap-2 mb-1">
                                <i data-lucide="eye-off" class="w-5 h-5 text-rose-400"></i>
                                <span>كاشف النقاط العمياء والتفكير النقدي</span>
                            </h3>
                            <p class="text-xs text-slate-300 leading-relaxed">
                                اكتشفي الزوايا التي أغفلها الفيديو، والافتراضات الضمنية للمتحدث. <strong>اضغطي على أي سؤال نقدي أدناه</strong> للانتقال فوراً إلى المحادثة والحصول على إجابته وتحليله!
                            </p>
                        </div>

                        <div>
                            <h4 class="text-sm font-extrabold text-rose-300 mb-3 flex items-center gap-2">
                                <i data-lucide="alert-triangle" class="w-4 h-4"></i>
                                <span>الزوايا المفقودة في الفيديو:</span>
                            </h4>
                            <div id="blindMissingList" class="grid grid-cols-1 md:grid-cols-2 gap-3.5"></div>
                        </div>

                        <div>
                            <h4 class="text-sm font-extrabold text-amber-300 mb-3 flex items-center gap-2">
                                <i data-lucide="lightbulb" class="w-4 h-4"></i>
                                <span>الافتراضات الضمنية للمتحدث:</span>
                            </h4>
                            <div id="blindAssumptionsList" class="space-y-2.5"></div>
                        </div>

                        <div>
                            <h4 class="text-sm font-extrabold text-sky-300 mb-3 flex items-center gap-2">
                                <i data-lucide="help-circle" class="w-4 h-4"></i>
                                <span>أسئلة نقدية ذكية (اضغطي لمناقشة السؤال فوراً):</span>
                            </h4>
                            <div id="blindQuestionsList" class="space-y-2.5"></div>
                        </div>
                    </div>

                    <!-- التبويب 4: اختبار الفهم (Quiz) -->
                    <div id="panel-quiz" class="study-tab-panel hidden flex-1 space-y-5">
                        <div class="flex flex-wrap items-center justify-between gap-3 p-4 rounded-2xl bg-slate-950 border border-slate-800">
                            <div>
                                <h3 class="text-base font-extrabold text-white">اختبار الفهم التفاعلي</h3>
                                <p class="text-xs text-slate-400">اختاري إجابة لكل سؤال لتظهر النتيجة والتفسير فوراً</p>
                            </div>
                            <div class="flex items-center gap-3">
                                <div class="px-4 py-2 rounded-xl bg-emerald-500/15 border border-emerald-500/30 text-emerald-300 text-sm font-black">
                                    النتيجة: <span id="quizScoreText">0</span> / <span id="quizTotalText">0</span>
                                </div>
                                <button onclick="resetQuizState()" class="flex items-center gap-1.5 px-3.5 py-2 rounded-xl bg-slate-800 hover:bg-slate-700 text-slate-200 text-xs font-bold transition cursor-pointer">
                                    <i data-lucide="rotate-ccw" class="w-4 h-4"></i>
                                    <span>إعادة الاختبار</span>
                                </button>
                            </div>
                        </div>
                        <div id="quizQuestionsContainer" class="space-y-4"></div>
                    </div>

                    <!-- التبويب 5: بطاقات الاستذكار (Flashcards) -->
                    <div id="panel-flashcards" class="study-tab-panel hidden flex-1 flex flex-col items-center justify-center py-4">
                        <div class="w-full max-w-lg flex items-center justify-between mb-4">
                            <div>
                                <h3 class="text-base font-extrabold text-white">بطاقات الاستذكار ثلاثية الأبعاد</h3>
                                <p class="text-xs text-slate-400">اضغطي على البطاقة لقلبها ورؤية التعريف</p>
                            </div>
                            <span id="masteredCountBadge" class="px-3 py-1 rounded-xl bg-emerald-500/15 border border-emerald-500/30 text-emerald-300 text-xs font-extrabold">
                                تم الحفظ: 0 / 0
                            </span>
                        </div>

                        <!-- البطاقة ثلاثية الأبعاد -->
                        <div onclick="flipFlashcard()" class="w-full max-w-lg h-64 sm:h-72 perspective-1000 cursor-pointer select-none my-2">
                            <div id="flashcard3DInner" class="relative w-full h-full transform-style-3d">
                                <!-- الوجه الأمامي -->
                                <div class="absolute inset-0 backface-hidden rounded-3xl bg-gradient-to-br from-slate-800 to-slate-950 border-2 border-sky-500/40 p-6 sm:p-8 flex flex-col items-center justify-center text-center shadow-2xl">
                                    <span class="px-3 py-1 rounded-full bg-sky-500/15 text-sky-300 text-xs font-bold mb-4">المصطلح / المفهوم</span>
                                    <h4 id="cardFrontText" class="text-xl sm:text-2xl font-black text-white leading-snug">...</h4>
                                    <span class="mt-6 text-xs text-slate-400 flex items-center gap-1.5">
                                        <i data-lucide="repeat" class="w-3.5 h-3.5 text-sky-400"></i> اضغطي لقلب البطاقة
                                    </span>
                                </div>

                                <!-- الوجه الخلفي -->
                                <div class="absolute inset-0 backface-hidden rotate-y-180 rounded-3xl bg-gradient-to-br from-indigo-950 to-slate-900 border-2 border-indigo-400/50 p-6 sm:p-8 flex flex-col items-center justify-center text-center shadow-2xl">
                                    <span class="px-3 py-1 rounded-full bg-indigo-500/20 text-indigo-300 text-xs font-bold mb-4">التعريف / الشرح</span>
                                    <p id="cardBackText" class="text-sm sm:text-lg font-medium text-slate-100 leading-relaxed">...</p>
                                </div>
                            </div>
                        </div>

                        <!-- أزرار التحكم بالبطاقات -->
                        <div class="flex flex-wrap items-center justify-center gap-3 mt-6">
                            <button onclick="navigateFlashcard(-1)" class="flex items-center gap-1.5 px-4 py-2.5 rounded-xl bg-slate-800 hover:bg-slate-700 border border-slate-700 text-sm font-bold text-white transition cursor-pointer">
                                <i data-lucide="arrow-right" class="w-4 h-4"></i>
                                <span>السابق</span>
                            </button>

                            <span id="cardProgressText" class="text-sm font-black text-sky-300 px-3">1 / 5</span>

                            <button onclick="navigateFlashcard(1)" class="flex items-center gap-1.5 px-4 py-2.5 rounded-xl bg-slate-800 hover:bg-slate-700 border border-slate-700 text-sm font-bold text-white transition cursor-pointer">
                                <span>التالي</span>
                                <i data-lucide="arrow-left" class="w-4 h-4"></i>
                            </button>

                            <button id="markMasteredBtn" onclick="toggleCardMastered()" class="flex items-center gap-1.5 px-4 py-2.5 rounded-xl bg-emerald-500/15 hover:bg-emerald-500/25 border border-emerald-500/40 text-emerald-300 text-sm font-extrabold transition cursor-pointer">
                                <i data-lucide="check-circle" class="w-4 h-4"></i>
                                <span id="markMasteredLabel">تم الحفظ</span>
                            </button>
                        </div>
                    </div>

                    <!-- التبويب 6: قاموس المصطلحات مع بحث فوري -->
                    <div id="panel-glossary" class="study-tab-panel hidden flex-1 space-y-4">
                        <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-3">
                            <div>
                                <h3 class="text-base font-extrabold text-white">قاموس المصطلحات والمفاهيم</h3>
                                <p class="text-xs text-slate-400">ابحثي في المصطلحات المفتاحية المستخرجة من الفيديو</p>
                            </div>
                            <div class="relative sm:w-64">
                                <input type="text" id="glossarySearchInput" oninput="filterGlossaryItems()" placeholder="ابحثي عن مصطلح..."
                                    class="w-full bg-slate-950 border border-slate-700/80 focus:border-sky-500 rounded-xl py-2 pr-9 pl-3 text-xs sm:text-sm text-white placeholder-slate-500 outline-none">
                                <i data-lucide="search" class="w-4 h-4 text-slate-400 absolute right-3 top-1/2 -translate-y-1/2"></i>
                            </div>
                        </div>
                        <div id="glossaryCardsGrid" class="grid grid-cols-1 sm:grid-cols-2 gap-3.5"></div>
                    </div>

                    <!-- التبويب 7: خطة التطبيق (Action Plan Checklist) -->
                    <div id="panel-actionplan" class="study-tab-panel hidden flex-1 space-y-5">
                        <div class="p-4 rounded-2xl bg-slate-950 border border-slate-800 space-y-3">
                            <div class="flex items-center justify-between">
                                <div>
                                    <h3 class="text-base font-extrabold text-white">خطة التطبيق العملي (Action Plan)</h3>
                                    <p class="text-xs text-slate-400">أشّري على الخطوات التي أنجزتِها لتطبيق ما تعلمتيه</p>
                                </div>
                                <span id="actionPercentText" class="text-sm font-black text-teal-400">0%</span>
                            </div>
                            <div class="w-full h-3 bg-slate-800 rounded-full overflow-hidden">
                                <div id="actionProgressBar" class="h-full bg-gradient-to-l from-teal-400 to-emerald-500 transition-all duration-300" style="width: 0%"></div>
                            </div>
                        </div>
                        <div id="actionChecklistContainer" class="space-y-3"></div>
                    </div>

                    <!-- التبويب 8: اسأل الفيديو (دردشة تفاعلية) -->
                    <div id="panel-chat" class="study-tab-panel hidden flex-1 flex flex-col">
                        <div class="mb-3">
                            <h3 class="text-base font-extrabold text-white">اسأل الفيديو (محادثة تفاعلية ذكية)</h3>
                            <p class="text-xs text-slate-400">اطرحي أي سؤال حول محتوى الفيديو أو ناقشي النقاط العمياء</p>
                        </div>

                        <!-- أزرار أسئلة سريعة مقترحة -->
                        <div id="suggestedQuestionsBar" class="flex flex-wrap gap-2 mb-3"></div>

                        <!-- سجل الرسائل -->
                        <div id="chatMessagesBox" class="flex-1 min-h-[260px] max-h-[360px] overflow-y-auto p-3.5 rounded-2xl bg-slate-950 border border-slate-800 space-y-3 mb-3"></div>

                        <!-- نموذج الإرسال -->
                        <form onsubmit="submitChatQuestion(event)" class="flex items-center gap-2">
                            <input type="text" id="chatQuestionInput" placeholder="اكتبي سؤالك هنا واضغطي إرسال..."
                                class="flex-1 bg-slate-950 border border-slate-700/80 focus:border-sky-500 rounded-2xl py-3 px-4 text-sm text-white placeholder-slate-500 outline-none">
                            <button type="submit" id="sendChatBtn" class="px-5 py-3 rounded-2xl bg-sky-500 hover:bg-sky-400 text-slate-950 font-extrabold text-sm flex items-center gap-2 transition cursor-pointer">
                                <span>إرسال</span>
                                <i data-lucide="send" class="w-4 h-4 rotate-180"></i>
                            </button>
                        </form>
                    </div>

                    <!-- ملخص إضافي يظهر في الطباعة فقط -->
                    <div id="printFullReport" class="hidden mt-8 pt-6 border-t-2 border-slate-300 space-y-5"></div>
                </div>
            </section>

            <!-- 3. الشريط الجانبي الدائم (دفتر الملاحظات لكل فيديو + السجل المحفوظ + التصدير) -->
            <aside id="sidebarColumn" class="lg:col-span-4 space-y-6">

                <!-- دفتر ملاحظاتي الذكي (مرتبط بكل فيديو على حدة) -->
                <div class="bg-slate-900/95 border border-slate-800 rounded-3xl p-5 sm:p-6 shadow-xl print-card">
                    <div class="flex items-center justify-between mb-3">
                        <h3 class="text-sm sm:text-base font-extrabold text-white flex items-center gap-2">
                            <i data-lucide="notebook-pen" class="w-5 h-5 text-amber-400"></i>
                            <span>دفتر ملاحظاتي الذكي</span>
                        </h3>
                        <span id="noteSavedIndicator" class="inline-flex items-center gap-1 px-2.5 py-0.5 rounded-full bg-emerald-500/15 text-emerald-300 text-[11px] font-bold">
                            <i data-lucide="check" class="w-3 h-3"></i> تم الحفظ
                        </span>
                    </div>
                    <p id="noteContextLabel" class="text-[11px] text-slate-400 mb-2.5 truncate">
                        ملاحظات مخصصة للفيديو الحالي (تُحفظ تلقائياً)
                    </p>
                    <textarea id="videoNotesTextarea" oninput="handleVideoNoteInput()" rows="6" placeholder="دوّني هنا ملاحظاتك، استنتاجاتك، أو أهم الأفكار التي لفتت انتباهك في هذا الفيديو..."
                        class="w-full bg-slate-950 border border-slate-800 focus:border-amber-500/70 rounded-2xl p-3.5 text-xs sm:text-sm text-slate-200 placeholder-slate-500 outline-none transition resize-y leading-relaxed"></textarea>
                </div>

                <!-- سجل الفيديوهات السابقة المحفوظة -->
                <div class="bg-slate-900/95 border border-slate-800 rounded-3xl p-5 sm:p-6 shadow-xl no-print">
                    <div class="flex items-center justify-between mb-4">
                        <div class="flex items-center gap-2">
                            <i data-lucide="history" class="w-5 h-5 text-sky-400"></i>
                            <h3 class="text-sm sm:text-base font-extrabold text-white">سجل الفيديوهات السابقة</h3>
                            <span id="savedHistoryCount" class="px-2 py-0.5 rounded-full bg-sky-500/20 text-sky-300 text-xs font-extrabold">0</span>
                        </div>
                        <button onclick="clearHistoryStorage()" title="مسح السجل" class="text-xs text-slate-400 hover:text-rose-400 font-bold cursor-pointer">
                            مسح الكل
                        </button>
                    </div>
                    <div id="savedHistoryContainer" class="space-y-2.5 max-h-72 overflow-y-auto pr-1"></div>
                </div>

                <!-- بطاقة تصدير التقرير -->
                <div class="bg-gradient-to-l from-sky-500/10 to-indigo-500/10 border border-sky-500/25 rounded-3xl p-5 no-print">
                    <h4 class="text-sm font-extrabold text-white mb-1.5 flex items-center gap-2">
                        <i data-lucide="file-down" class="w-4 h-4 text-sky-400"></i>
                        <span>حفظ التقرير للدراسة لاحقاً</span>
                    </h4>
                    <p class="text-xs text-slate-300 leading-relaxed mb-3.5">
                        يمكنكِ طباعة الشرح مع ملاحظاتكِ الشخصية والنقاط العمياء وبطاقات المراجعة أو حفظها كملف PDF منسق بضغطة واحدة.
                    </p>
                    <button onclick="exportAndPrintReport()" class="w-full py-2.5 px-4 rounded-xl bg-slate-900 hover:bg-slate-800 border border-sky-500/40 text-sky-300 text-xs sm:text-sm font-extrabold flex items-center justify-center gap-2 transition cursor-pointer">
                        <i data-lucide="printer" class="w-4 h-4"></i>
                        <span>تصدير وطباعة التقرير الكامل (PDF)</span>
                    </button>
                </div>

            </aside>
        </div>
    </main>

    <script>
        // تهيئة أيقونات Lucide
        lucide.createIcons();

        const apiKey = "";
        const STORAGE_HISTORY_KEY = "rafeeq_smart_history_v4";
        const STORAGE_NOTES_PREFIX = "rafeeq_video_note_v4_";

        // حالة التطبيق الحالية
        let currentSessionId = "default_session";
        let currentStudyPayload = null;
        let isDemoMode = false;

        // حالة التبويبات والأدوات التفاعلية
        let activeTabKey = "explain";
        let mindmapScale = 1;
        let collapsedMindNodes = new Set();
        let quizAnsweredSet = new Set();
        let quizCurrentScore = 0;
        let flashcardIdx = 0;
        let flashcardFlipped = false;
        let masteredCardsSet = new Set();
        let isAudioSpeaking = false;

        // بيانات المثال العملي الجاهز المتكامل (للتجربة الفورية)
        const READY_DEMO_DATA = {
            id: "demo_ai_agents_2026",
            title: "كيف تعمل وكلاء الذكاء الاصطناعي (AI Agents) وتغير مستقبل البرمجة والإنتاجية؟",
            url: "https://www.youtube.com/watch?v=dQw4w9WgXcQ",
            transcript: "في هذا الفيديو نشرح الانتقال الكبير من نماذج الدردشة التقليدية (Chatbots) إلى وكلاء الذكاء الاصطناعي المستقلين (AI Agents). الوكيل الذكي لا يكتفي بالإجابة على سؤالك، بل يمتلك القدرة على التخطيط، تقسيم الهدف الكبير إلى مهام فرعية، استخدام الأدوات الخارجية مثل المتصفح وقواعد البيانات، ومراجعة أخطائه ذاتياً حتى إنجاز المهمة. يعتمد الوكيل على أربعة مكونات أساسية: نموذج لغوي كبير كعقل مفكر، ذاكرة قصيرة وطويلة المدى، أدوات تنفيذية، وحلقة تفكير وتصحيح ذاتي (Reflection Loop).",
            generalIdea: "الفرق الجوهري بين الذكاء الاصطناعي التقليدي ووكلاء الذكاء الاصطناعي (AI Agents) هو الانتقال من مجرد الإجابة النصية إلى التخطيط المستقل واستخدام الأدوات وتنفيذ المهام متعددة الخطوات ذاتياً.",
            detailedExplanationMarkdown: `## 1. من الدردشة إلى التنفيذ المستقل
في النماذج التقليدية، تطرح سؤالاً فتحصل على إجابة نصية وعليك تنفيذ الخطوات بنفسك. أما **وكيل الذكاء الاصطناعي (AI Agent)** فتمنحه هدفاً نهائياً مثل: *"ابحث عن أحدث أبحاث الطاقة الشمسية ولخّصها في تقرير"*، فيقوم هو بالتخطيط والتنفيذ خطوة بخطوة.

## 2. المكونات الأربعة لأي وكيل ذكي
* **العقل المفكر (LLM Core):** النموذج اللغوي الذي يحلل الهدف ويقرر الخطوة التالية.
* **التخطيط وتقسيم المهام (Planning):** تفكيك الهدف المعقد إلى خطوات صغيرة قابلة للتنفيذ.
* **الذاكرة (Memory):** ذاكرة قصيرة المدى لتتبع المهمة الحالية، وطويلة المدى لتذكر تفضيلاتك السابقة.
* **الأدوات (Tools):** القدرة على البحث في الإنترنت، تشغيل الأكواد، أو قراءة الملفات.

## 3. حلقة المراجعة الذاتية (Reflection Loop)
أقوى ما يميز الوكلاء الأذكياء هو قدرتهم على **نقد مخرجاتهم وتصحيح أخطائهم** قبل تسليم النتيجة النهائية للمستخدم، مما يرفع الدقة بشكل هائل.`,
            eli5Explanation: `تخيلي أن الذكاء الاصطناعي التقليدي هو **صديق ذكي جداً يجلس في مكتبة**؛ تسألينه عن وصفة كيك فيكتبها لكِ على ورقة، لكن عليكِ أنتِ شراء المكونات وخبزها.

أما **وكيل الذكاء الاصطناعي (AI Agent)** فهو **طاهٍ محترف في مطبخكِ**؛ تقولين له: *"أريد كيكة شوكولاتة لعيد الميلاد"*، فيقوم هو بكتابة قائمة المشتريات، يطلبها من المتجر، يخلط المكونات، يتذوق الخليط ليعدّل السكر إذا لزم الأمر، ثم يقدم لكِ الكيكة جاهزة!`,
            mindMap: {
                centralTopic: "وكلاء الذكاء الاصطناعي (AI Agents)",
                branches: [
                    {
                        title: "المكونات الأساسية",
                        subNodes: ["العقل المفكر (LLM)", "الذاكرة القصيرة والطويلة", "الأدوات الخارجية"]
                    },
                    {
                        title: "آلية التخطيط",
                        subNodes: ["فهم الهدف النهائي", "تقسيم المهام الفرعية", "ترتيب الأولويات"]
                    },
                    {
                        title: "التصحيح الذاتي",
                        subNodes: ["مراجعة المخرجات", "اكتشاف الأخطاء", "تحسين النتيجة تلقائياً"]
                    },
                    {
                        title: "التطبيقات العملية",
                        subNodes: ["مساعد البرمجة المستقل", "البحث والتحليل الآلي", "أتمتة خدمة العملاء"]
                    }
                ]
            },
            blindSpots: {
                missingAngles: [
                    {
                        title: "تكلفة التشغيل واستهلاك الموارد",
                        description: "لم يتطرق الفيديو إلى أن حلقات التفكير المتكررة للوكيل تستهلك عدداً كبيراً من التوكنز (Tokens) مما يرفع التكلفة والوقت مقارنة بالطلب الواحد."
                    },
                    {
                        title: "مخاطر الأمان والصلاحيات",
                        description: "إعطاء الوكيل صلاحية تنفيذ أكواد أو إرسال رسائل دون إشراف بشري قد يؤدي لأخطاء غير مقصودة إذا لم تُوضع قيود صارمة."
                    }
                ],
                hiddenAssumptions: [
                    "يفترض المتحدث أن النموذج اللغوي الأساسي موثوق بما يكفي لاتخاذ قرارات صحيحة في كل خطوة دون الوقوع في حلقات تكرار لا نهائية.",
                    "يفترض توفر واجهات برمجية (APIs) جاهزة وسريعة لكل أداة سيستخدمها الوكيل."
                ],
                criticalQuestions: [
                    "كيف نمنع وكيل الذكاء الاصطناعي من الدخول في حلقة تكرار لا نهائية عند فشل أداة معينة؟",
                    "ما هي المهام التي يجب أن تبقى تحت إشراف بشري مباشر (Human-in-the-Loop)؟",
                    "ما الفرق العملي بين الوكيل الواحد وفريق من الوكلاء المتعاونين (Multi-Agent Systems)؟"
                ]
            },
            quiz: [
                {
                    question: "ما الفرق الرئيسي بين روبوت الدردشة التقليدي ووكيل الذكاء الاصطناعي (AI Agent)؟",
                    options: [
                        "الوكيل الذكي يكتب نصوصاً أطول فقط",
                        "الوكيل الذكي يخطط وينفذ المهام ويستخدم الأدوات بشكل مستقل",
                        "روبوت الدردشة لا يستخدم نماذج لغوية",
                        "الوكيل الذكي يعمل بدون اتصال بالإنترنت دائماً"
                    ],
                    correctIndex: 1,
                    explanation: "الوكيل الذكي يتميز بالقدرة على التخطيط المستقل، استخدام الأدوات، وتنفيذ خطوات متسلسلة لتحقيق هدف محدد."
                },
                {
                    question: "ما وظيفة 'حلقة المراجعة الذاتية' (Reflection Loop) في الوكلاء الأذكياء؟",
                    options: [
                        "حذف ذاكرة المستخدم بعد كل محادثة",
                        "تقييم المخرجات واكتشاف الأخطاء وتصحيحها قبل التسليم",
                        "تسريع سرعة الإنترنت في الجهاز",
                        "تحويل النصوص إلى ملفات صوتية فقط"
                    ],
                    correctIndex: 1,
                    explanation: "حلقة المراجعة الذاتية تسمح للوكيل بنقد عمله وتحسين جودته ذاتياً قبل تقديم الإجابة النهائية."
                },
                {
                    question: "أي مما يلي يُعد من المكونات الأربعة الأساسية لوكيل الذكاء الاصطناعي؟",
                    options: [
                        "بطاقة الرسوميات فقط",
                        "الذاكرة والأدوات والتخطيط والعقل المفكر",
                        "شاشة اللمس ولوحة المفاتيح",
                        "برامج تحرير الفيديو"
                    ],
                    correctIndex: 1,
                    explanation: "يتكون الوكيل الذكي من: النموذج اللغوي (العقل)، التخطيط، الذاكرة، والأدوات التنفيذية."
                }
            ],
            flashcards: [
                {
                    front: "وكيل الذكاء الاصطناعي (AI Agent)",
                    back: "نظام ذكي قادر على فهم هدف معقد، تخطيط خطواته، استخدام أدوات خارجية، وتنفيذ المهام باستقلالية."
                },
                {
                    front: "حلقة المراجعة الذاتية (Reflection Loop)",
                    back: "آلية يقوم فيها الذكاء الاصطناعي بفحص نتيجته الأولية، اكتشاف نقاط الضعف فيها، وإعادة تحسينها تلقائياً."
                },
                {
                    front: "الأدوات (Agent Tools)",
                    back: "وظائف خارجية يستدعيها الوكيل مثل البحث في الويب، تشغيل كود برمجي، أو قراءة قاعدة بيانات."
                },
                {
                    front: "الإشراف البشري (Human-in-the-Loop)",
                    back: "مبدأ تصميمي يتطلب موافقة الإنسان قبل تنفيذ الوكيل لأي إجراء حساس أو عالي المخاطر."
                }
            ],
            glossary: [
                {
                    term: "AI Agent",
                    translation: "وكيل الذكاء الاصطناعي",
                    definition: "برنامج مستقل يستخدم الذكاء الاصطناعي للتخطيط واتخاذ القرارات وتنفيذ المهام لتحقيق هدف محدد."
                },
                {
                    term: "Reflection Loop",
                    translation: "حلقة التصحيح الذاتي",
                    definition: "عملية تكرارية يراجع فيها النموذج إجابته ويصحح أخطاءه قبل عرض النتيجة النهائية."
                },
                {
                    term: "Multi-Agent System",
                    translation: "نظام متعدد الوكلاء",
                    definition: "تعاون عدة وكلاء متخصصين (مثل باحث، مبرمج، ومدقق) معاً لإنجاز مشروع متكامل."
                },
                {
                    term: "Context Memory",
                    translation: "ذاكرة السياق",
                    definition: "قدرة الوكيل على الاحتفاظ بالمعلومات والخطوات السابقة أثناء تنفيذ مهمة طويلة."
                }
            ],
            actionPlan: [
                "حددي مهمة روتينية متكررة في دراستك أو عملك يمكن أتمتتها باستخدام وكيل ذكي.",
                "جرّبي تقسيم أي مشروع كبير تدرسينه إلى 4 خطوات فرعية واضحة بنفس أسلوب تخطيط الوكلاء.",
                "طبّقي مبدأ المراجعة الذاتية (Reflection) عبر مراجعة ملخصاتك الدراسية ونقدها قبل الامتحان.",
                "استكشفي إحدى أدوات بناء الوكلاء البسيطة مثل LangChain أو CrewAI كتطبيق عملي."
            ],
            suggestedQuestions: [
                "كيف أبدأ ببناء أول وكيل ذكاء اصطناعي بسيط كمبتدئة؟",
                "ما الفرق العملي بين الوكيل الواحد وفريق من الوكلاء المتعاونين؟",
                "أعطني مثالاً عملياً لاستخدام الوكلاء الذكيين في الدراسة الجامعية"
            ]
        };

        // عند تحميل الصفحة
        window.addEventListener('DOMContentLoaded', () => {
            renderSavedHistoryList();
            loadNoteForSession(currentSessionId);
        });

        // استخراج معرف فيديو يوتيوب
        function getYouTubeVideoId(url) {
            const match = url.match(/(?:youtube\.com\/(?:watch\?v=|embed\/|shorts\/)|youtu\.be\/)([a-zA-Z0-9_-]{11})/);
            return match ? match[1] : null;
        }

        // معاينة تلقائية عند لصق رابط يوتيوب
        async function handleVideoUrlChange() {
            const url = document.getElementById('videoUrlInput').value.trim();
            const previewBox = document.getElementById('youtubePreviewBox');
            const videoId = getYouTubeVideoId(url);

            if (!videoId) {
                previewBox.classList.add('hidden');
                return;
            }

            document.getElementById('youtubeThumbImg').src = `https://img.youtube.com/vi/${videoId}/mqdefault.jpg`;
            document.getElementById('youtubeTitleText').textContent = `فيديو يوتيوب (${videoId})`;
            previewBox.classList.remove('hidden');

            try {
                const res = await fetch(`https://noembed.com/embed?url=https://www.youtube.com/watch?v=${videoId}`);
                if (res.ok) {
                    const data = await res.json();
                    if (data.title) {
                        document.getElementById('youtubeTitleText').textContent = data.title;
                    }
                }
            } catch {}
        }

        // لصق من الحافظة
        async function pasteToField(fieldId) {
            try {
                const text = await navigator.clipboard.readText();
                const el = document.getElementById(fieldId);
                el.value = text;
                if (fieldId === 'videoUrlInput') handleVideoUrlChange();
                showToast('تم اللصق بنجاح', 'success');
            } catch {
                showToast('اضغطي داخل الحقل واستخدمي Ctrl+V للصق', 'info');
            }
        }

        function clearInputFields() {
            document.getElementById('videoUrlInput').value = '';
            document.getElementById('transcriptTextInput').value = '';
            document.getElementById('youtubePreviewBox').classList.add('hidden');
            showToast('تم مسح الحقول', 'info');
        }

        // تحميل المثال العملي الجاهز وتعبئة كل التبويبات فوراً
        function loadReadyDemoExample() {
            stopArabicSpeech();
            isDemoMode = true;
            currentSessionId = READY_DEMO_DATA.id;
            currentStudyPayload = JSON.parse(JSON.stringify(READY_DEMO_DATA));

            document.getElementById('videoUrlInput').value = READY_DEMO_DATA.url;
            document.getElementById('transcriptTextInput').value = READY_DEMO_DATA.transcript;
            handleVideoUrlChange();

            populateWorkspaceWithData(currentStudyPayload, true);
            saveStudyToHistory(currentStudyPayload);
            loadNoteForSession(currentSessionId);

            showToast('تم تحميل المثال العملي الجاهز! جرّبي التنقل بين جميع التبويبات الثمانية الآن', 'success');
        }

        // استدعاء Gemini API مع معالجة الأخطاء وإعادة المحاولة
        async function fetchGeminiContent(payload) {
            const endpoint = `https://generativelanguage.googleapis.com/v1beta/models/gemini-3-flash-preview:generateContent?key=${apiKey}`;
            const delays = [1000, 2000, 4000, 8000];

            for (let attempt = 0; attempt <= delays.length; attempt++) {
                try {
                    const response = await fetch(endpoint, {
                        method: 'POST',
                        headers: { 'Content-Type': 'application/json' },
                        body: JSON.stringify(payload)
                    });
                    if (!response.ok) throw new Error(`HTTP ${response.status}`);
                    const data = await response.json();
                    const resultText = data?.candidates?.[0]?.content?.parts?.[0]?.text;
                    if (!resultText) throw new Error('استجابة فارغة');
                    return resultText;
                } catch (err) {
                    if (attempt === delays.length) throw err;
                    await new Promise(r => setTimeout(r, delays[attempt]));
                }
            }
        }

        // تشغيل التحليل الحقيقي عبر Gemini API
        async function runDeepAnalysis() {
            const urlVal = document.getElementById('videoUrlInput').value.trim();
            const textVal = document.getElementById('transcriptTextInput').value.trim();
            const levelVal = document.getElementById('analysisLevelSelect').value;

            if (!urlVal && !textVal) {
                showToast('يرجى إدخال رابط فيديو أو لصق نص أولاً، أو الضغط على "جرّب بمثال عملي جاهز"!', 'error');
                return;
            }

            stopArabicSpeech();
            isDemoMode = false;

            const btn = document.getElementById('startAnalysisBtn');
            btn.disabled = true;
            btn.classList.add('opacity-60', 'cursor-not-allowed');

            document.getElementById('welcomeEmptyBox').classList.add('hidden');
            document.getElementById('activeWorkspaceBox').classList.add('hidden');
            document.getElementById('loadingSpinnerBox').classList.remove('hidden');
            document.getElementById('loadingSpinnerBox').classList.add('flex');

            const videoId = getYouTubeVideoId(urlVal);
            const previewTitle = document.getElementById('youtubeTitleText').textContent;
            let useSearch = false;
            let contentPromptBlock = "";

            if (urlVal && textVal) {
                contentPromptBlock = `رابط الفيديو: ${urlVal}\nعنوان الفيديو: ${previewTitle}\nنص الفيديو:\n${textVal.slice(0, 26000)}`;
            } else if (urlVal) {
                useSearch = true;
                contentPromptBlock = `رابط الفيديو: ${urlVal}\nمعرّف يوتيوب: ${videoId || 'غير محدد'}\nالعنوان المعروف: ${previewTitle}\nابحث عن محتوى هذا الفيديو وتفاصيله بدقة وحلله بالكامل.`;
            } else {
                contentPromptBlock = `نص المحاضرة أو الفيديو:\n${textVal.slice(0, 26000)}`;
            }

            const levelInstructions = {
                simple: "شرح مبسط ومفصل مع أمثلة عملية واضحة وعناوين منظمة",
                academic: "شرح أكاديمي متعمق ومنهجي يحلل المفاهيم والنظريات بدقة",
                summary: "ملخص سريع ونقاط أساسية مركزة تعطي الزبدة مباشرة"
            };

            const systemPrompt = `أنت "رفيق الفهم الذكي"، خبير تعليمي عربي. حلل المحتوى التالي وأرجع كائن JSON متكامل باللغة العربية الفصحى الواضحة يغذي 8 أدوات دراسية دفعة واحدة.
أسلوب الشرح المطلوب في detailedExplanationMarkdown: ${levelInstructions[levelVal]}.

المحتوى:
${contentPromptBlock}`;

            const payload = {
                contents: [{ parts: [{ text: systemPrompt }] }],
                generationConfig: {
                    responseMimeType: "application/json",
                    responseSchema: {
                        type: "OBJECT",
                        properties: {
                            title: { type: "STRING" },
                            generalIdea: { type: "STRING" },
                            detailedExplanationMarkdown: { type: "STRING" },
                            eli5Explanation: { type: "STRING" },
                            mindMap: {
                                type: "OBJECT",
                                properties: {
                                    centralTopic: { type: "STRING" },
                                    branches: {
                                        type: "ARRAY",
                                        items: {
                                            type: "OBJECT",
                                            properties: {
                                                title: { type: "STRING" },
                                                subNodes: { type: "ARRAY", items: { type: "STRING" } }
                                            },
                                            required: ["title", "subNodes"]
                                        }
                                    }
                                },
                                required: ["centralTopic", "branches"]
                            },
                            blindSpots: {
                                type: "OBJECT",
                                properties: {
                                    missingAngles: {
                                        type: "ARRAY",
                                        items: {
                                            type: "OBJECT",
                                            properties: {
                                                title: { type: "STRING" },
                                                description: { type: "STRING" }
                                            },
                                            required: ["title", "description"]
                                        }
                                    },
                                    hiddenAssumptions: { type: "ARRAY", items: { type: "STRING" } },
                                    criticalQuestions: { type: "ARRAY", items: { type: "STRING" } }
                                },
                                required: ["missingAngles", "hiddenAssumptions", "criticalQuestions"]
                            },
                            quiz: {
                                type: "ARRAY",
                                items: {
                                    type: "OBJECT",
                                    properties: {
                                        question: { type: "STRING" },
                                        options: { type: "ARRAY", items: { type: "STRING" } },
                                        correctIndex: { type: "INTEGER" },
                                        explanation: { type: "STRING" }
                                    },
                                    required: ["question", "options", "correctIndex", "explanation"]
                                }
                            },
                            flashcards: {
                                type: "ARRAY",
                                items: {
                                    type: "OBJECT",
                                    properties: {
                                        front: { type: "STRING" },
                                        back: { type: "STRING" }
                                    },
                                    required: ["front", "back"]
                                }
                            },
                            glossary: {
                                type: "ARRAY",
                                items: {
                                    type: "OBJECT",
                                    properties: {
                                        term: { type: "STRING" },
                                        translation: { type: "STRING" },
                                        definition: { type: "STRING" }
                                    },
                                    required: ["term", "translation", "definition"]
                                }
                            },
                            actionPlan: { type: "ARRAY", items: { type: "STRING" } },
                            suggestedQuestions: { type: "ARRAY", items: { type: "STRING" } }
                        },
                        required: [
                            "title", "generalIdea", "detailedExplanationMarkdown", "eli5Explanation",
                            "mindMap", "blindSpots", "quiz", "flashcards", "glossary", "actionPlan", "suggestedQuestions"
                        ]
                    }
                }
            };

            if (useSearch) {
                payload.tools = [{ google_search: {} }];
            }

            try {
                const rawJson = await fetchGeminiContent(payload);
                const parsed = JSON.parse(rawJson);
                parsed.id = videoId ? `yt_${videoId}` : `study_${Date.now()}`;
                parsed.url = urlVal;
                parsed.transcript = textVal;

                currentSessionId = parsed.id;
                currentStudyPayload = parsed;

                populateWorkspaceWithData(parsed, false);
                saveStudyToHistory(parsed);
                loadNoteForSession(currentSessionId);

                showToast('اكتمل التحليل الشامل بنجاح! جميع التبويبات الثمانية جاهزة', 'success');
            } catch (error) {
                document.getElementById('loadingSpinnerBox').classList.add('hidden');
                document.getElementById('welcomeEmptyBox').classList.remove('hidden');
                showToast('حدث خطأ أثناء الاتصال بالذكاء الاصطناعي. يمكنكِ تجربة المثال العملي الجاهز أو المحاولة مجدداً.', 'error');
            } finally {
                btn.disabled = false;
                btn.classList.remove('opacity-60', 'cursor-not-allowed');
            }
        }

        // تعبئة جميع التبويبات الثمانية بالبيانات
        function populateWorkspaceWithData(data, demoFlag) {
            document.getElementById('loadingSpinnerBox').classList.add('hidden');
            document.getElementById('welcomeEmptyBox').classList.add('hidden');
            document.getElementById('activeWorkspaceBox').classList.remove('hidden');

            document.getElementById('currentStudyTitle').textContent = data.title || "محتوى دراسي";
            const badge = document.getElementById('dataModeBadge');
            if (demoFlag) {
                badge.textContent = "وضع المثال العملي التفاعلي";
                badge.className = "px-3 py-1 rounded-full text-xs font-extrabold bg-amber-500/15 text-amber-300 border border-amber-500/30";
            } else {
                badge.textContent = "تحليل الذكاء الاصطناعي الحي";
                badge.className = "px-3 py-1 rounded-full text-xs font-extrabold bg-emerald-500/15 text-emerald-300 border border-emerald-500/30";
            }

            // تحديث العدادات على التبويبات
            document.getElementById('badge-mindmap').textContent = (data.mindMap?.branches || []).length;
            const blindCount = (data.blindSpots?.missingAngles?.length || 0) + (data.blindSpots?.criticalQuestions?.length || 0);
            document.getElementById('badge-blindspots').textContent = blindCount;
            document.getElementById('badge-quiz').textContent = (data.quiz || []).length;
            document.getElementById('badge-flashcards').textContent = (data.flashcards || []).length;
            document.getElementById('badge-glossary').textContent = (data.glossary || []).length;
            document.getElementById('badge-actionplan').textContent = (data.actionPlan || []).length;

            // 1. الشرح والتبسيط ELI5
            document.getElementById('eli5ResultBox').classList.add('hidden');
            document.getElementById('eli5BtnLabel').textContent = "بسّطها لي كأني مبتدئة (ELI5)";
            document.getElementById('eli5ContentText').innerHTML = marked.parse(data.eli5Explanation || "");
            document.getElementById('generalIdeaText').textContent = data.generalIdea || "";
            document.getElementById('detailedExplanationOutput').innerHTML = marked.parse(data.detailedExplanationMarkdown || "");

            // 2. الخريطة الذهنية
            mindmapScale = 1;
            collapsedMindNodes.clear();
            renderInteractiveMindMap(data.mindMap);

            // 3. كاشف النقاط العمياء
            renderBlindSpotsSection(data.blindSpots);

            // 4. اختبار الفهم
            quizAnsweredSet.clear();
            quizCurrentScore = 0;
            renderInteractiveQuiz(data.quiz || []);

            // 5. بطاقات الاستذكار
            flashcardIdx = 0;
            flashcardFlipped = false;
            masteredCardsSet.clear();
            updateFlashcardUI();

            // 6. قاموس المصطلحات
            document.getElementById('glossarySearchInput').value = "";
            renderGlossaryList(data.glossary || []);

            // 7. خطة التطبيق
            renderActionPlanList(data.actionPlan || []);

            // 8. المحادثة التفاعلية
            initChatWorkspace(data.suggestedQuestions || []);

            // تفعيل التبويب الأول افتراضياً
            activateTab('explain');
            lucide.createIcons();
        }

        // التبديل بين التبويبات الثمانية
        function activateTab(tabKey) {
            activeTabKey = tabKey;

            document.querySelectorAll('.study-tab-btn').forEach(btn => {
                btn.className = "study-tab-btn flex items-center gap-1.5 px-3.5 py-2.5 rounded-xl text-xs font-extrabold whitespace-nowrap bg-slate-950/80 text-slate-400 hover:text-white border border-slate-800 transition cursor-pointer";
            });

            const activeBtn = document.getElementById(`tabBtn-${tabKey}`);
            if (activeBtn) {
                activeBtn.className = "study-tab-btn flex items-center gap-1.5 px-3.5 py-2.5 rounded-xl text-xs font-extrabold whitespace-nowrap bg-sky-500 text-slate-950 shadow-lg shadow-sky-500/20 border border-sky-400 transition cursor-pointer";
            }

            document.querySelectorAll('.study-tab-panel').forEach(panel => panel.classList.add('hidden'));
            const activePanel = document.getElementById(`panel-${tabKey}`);
            if (activePanel) activePanel.classList.remove('hidden');

            if (tabKey === 'mindmap' && currentStudyPayload?.mindMap) {
                renderInteractiveMindMap(currentStudyPayload.mindMap);
            }
        }

        // --- وظائف التبويب 1: ELI5 والصوت والنسخ ---
        function toggleEli5Box() {
            const box = document.getElementById('eli5ResultBox');
            const label = document.getElementById('eli5BtnLabel');
            const isHidden = box.classList.contains('hidden');
            if (isHidden) {
                box.classList.remove('hidden');
                label.textContent = "إخفاء التبسيط (ELI5)";
                showToast('تم إظهار الشرح المبسط بتشبيهات يومية', 'info');
            } else {
                box.classList.add('hidden');
                label.textContent = "بسّطها لي كأني مبتدئة (ELI5)";
            }
        }

        function toggleArabicSpeech() {
            if (!('speechSynthesis' in window)) {
                showToast('المتصفح لا يدعم القراءة الصوتية', 'error');
                return;
            }
            if (isAudioSpeaking) {
                stopArabicSpeech();
                return;
            }
            const textToRead = document.getElementById('generalIdeaText').textContent + ". " + document.getElementById('detailedExplanationOutput').innerText;
            if (!textToRead.trim()) return;

            window.speechSynthesis.cancel();
            const utterance = new SpeechSynthesisUtterance(textToRead);
            utterance.lang = 'ar-SA';
            utterance.rate = 1.0;
            utterance.onend = () => stopArabicSpeech();
            utterance.onerror = () => stopArabicSpeech();

            window.speechSynthesis.speak(utterance);
            isAudioSpeaking = true;
            document.getElementById('speakLabel').textContent = "إيقاف الصوت";
            document.getElementById('speakBtn').classList.add('border-sky-500', 'text-sky-300');
        }

        function stopArabicSpeech() {
            if ('speechSynthesis' in window) window.speechSynthesis.cancel();
            isAudioSpeaking = false;
            document.getElementById('speakLabel').textContent = "استماع صوتي";
            document.getElementById('speakBtn').classList.remove('border-sky-500', 'text-sky-300');
        }

        function copyExplanationText() {
            if (!currentStudyPayload) return;
            const fullText = `${currentStudyPayload.title}\n\nالفكرة العامة:\n${currentStudyPayload.generalIdea}\n\nالشرح:\n${currentStudyPayload.detailedExplanationMarkdown}`;
            const tempArea = document.createElement('textarea');
            tempArea.value = fullText;
            document.body.appendChild(tempArea);
            tempArea.select();
            try {
                document.execCommand('copy');
                showToast('تم نسخ الشرح الكامل إلى الحافظة!', 'success');
            } catch {
                showToast('تعذر النسخ التلقائي', 'error');
            }
            document.body.removeChild(tempArea);
        }

        // --- وظائف التبويب 2: الخريطة الذهنية البصرية SVG ---
        function renderInteractiveMindMap(mindMap) {
            const svg = document.getElementById('mindmapSvgCanvas');
            if (!mindMap || !mindMap.branches) {
                svg.innerHTML = '';
                return;
            }

            const width = 880;
            const height = 520;
            svg.setAttribute('viewBox', `0 0 ${width} ${height}`);
            svg.style.transform = `scale(${mindmapScale})`;

            const cx = width / 2;
            const cy = height / 2;
            const branches = mindMap.branches.slice(0, 6);
            const total = branches.length;
            const rBranch = 175;
            const rSub = 115;

            const palette = [
                { stroke: '#38bdf8', fill: '#0c4a6e', text: '#e0f2fe' },
                { stroke: '#818cf8', fill: '#1e1b4b', text: '#e0e7ff' },
                { stroke: '#34d399', fill: '#064e3b', text: '#d1fae5' },
                { stroke: '#fbbf24', fill: '#451a03', text: '#fef3c7' },
                { stroke: '#f472b6', fill: '#500724', text: '#fce7f3' },
                { stroke: '#a78bfa', fill: '#2e1065', text: '#ede9fe' }
            ];

            let pathsSvg = '';
            let nodesSvg = '';

            branches.forEach((branch, idx) => {
                const angle = (idx / total) * Math.PI * 2 - Math.PI / 2;
                const bx = cx + Math.cos(angle) * rBranch;
                const by = cy + Math.sin(angle) * rBranch;
                const col = palette[idx % palette.length];
                const isCollapsed = collapsedMindNodes.has(idx);

                const ctrlX = cx + Math.cos(angle) * (rBranch * 0.52);
                const ctrlY = cy + Math.sin(angle) * (rBranch * 0.52);
                pathsSvg += `<path d="M ${cx} ${cy} Q ${ctrlX} ${ctrlY} ${bx} ${by}" fill="none" stroke="${col.stroke}" stroke-width="2.5" stroke-opacity="0.75" />`;

                const subs = branch.subNodes || [];
                if (!isCollapsed && subs.length > 0) {
                    const spread = 0.42;
                    subs.forEach((sub, sIdx) => {
                        const offset = (sIdx - (subs.length - 1) / 2) * spread;
                        const sAngle = angle + offset;
                        const sx = bx + Math.cos(sAngle) * rSub;
                        const sy = by + Math.sin(sAngle) * rSub;

                        pathsSvg += `<line x1="${bx}" y1="${by}" x2="${sx}" y2="${sy}" stroke="${col.stroke}" stroke-width="1.5" stroke-dasharray="4 3" stroke-opacity="0.6" />`;

                        const sLabel = shortText(sub, 22);
                        const sBoxW = Math.max(96, sLabel.length * 6.5 + 22);
                        nodesSvg += `
                            <g transform="translate(${sx}, ${sy})">
                                <rect x="${-sBoxW / 2}" y="-15" width="${sBoxW}" height="30" rx="10" fill="#0f172a" stroke="${col.stroke}" stroke-width="1.2" stroke-opacity="0.8" />
                                <text x="0" y="4" text-anchor="middle" fill="#cbd5e1" font-size="11" font-weight="600" font-family="Tajawal, sans-serif">${escapeHtml(sLabel)}</text>
                            </g>
                        `;
                    });
                }

                const bLabel = shortText(branch.title, 20);
                const bBoxW = Math.max(120, bLabel.length * 7.2 + 30);
                const sign = isCollapsed ? '+' : '−';
                nodesSvg += `
                    <g class="mindmap-node" onclick="toggleSingleMindMapNode(${idx})" transform="translate(${bx}, ${by})">
                        <rect x="${-bBoxW / 2}" y="-20" width="${bBoxW}" height="40" rx="14" fill="${col.fill}" stroke="${col.stroke}" stroke-width="2" />
                        <text x="0" y="4" text-anchor="middle" fill="${col.text}" font-size="12.5" font-weight="800" font-family="Tajawal, sans-serif">${escapeHtml(bLabel)}</text>
                        <circle cx="${-bBoxW / 2}" cy="0" r="9" fill="#0f172a" stroke="${col.stroke}" stroke-width="1.5" />
                        <text x="${-bBoxW / 2}" y="3.5" text-anchor="middle" fill="${col.text}" font-size="11" font-weight="900">${sign}</text>
                    </g>
                `;
            });

            const cLabel = shortText(mindMap.centralTopic, 26);
            const cBoxW = Math.max(160, cLabel.length * 7.8 + 38);
            const centerSvg = `
                <g transform="translate(${cx}, ${cy})">
                    <defs>
                        <linearGradient id="mmCenterGrad" x1="0%" y1="0%" x2="100%" y2="100%">
                            <stop offset="0%" stop-color="#0284c7" />
                            <stop offset="100%" stop-color="#4f46e5" />
                        </linearGradient>
                    </defs>
                    <rect x="${-cBoxW / 2}" y="-26" width="${cBoxW}" height="52" rx="18" fill="url(#mmCenterGrad)" stroke="#7dd3fc" stroke-width="2.5" />
                    <text x="0" y="5" text-anchor="middle" fill="#ffffff" font-size="14" font-weight="900" font-family="Tajawal, sans-serif">${escapeHtml(cLabel)}</text>
                </g>
            `;

            svg.innerHTML = pathsSvg + nodesSvg + centerSvg;
        }

        function toggleSingleMindMapNode(idx) {
            if (collapsedMindNodes.has(idx)) collapsedMindNodes.delete(idx);
            else collapsedMindNodes.add(idx);
            if (currentStudyPayload?.mindMap) renderInteractiveMindMap(currentStudyPayload.mindMap);
        }

        function toggleAllMindMapNodes() {
            const total = currentStudyPayload?.mindMap?.branches?.length || 0;
            if (collapsedMindNodes.size > 0) collapsedMindNodes.clear();
            else { for (let i = 0; i < total; i++) collapsedMindNodes.add(i); }
            if (currentStudyPayload?.mindMap) renderInteractiveMindMap(currentStudyPayload.mindMap);
        }

        function adjustMindMapZoom(delta) {
            mindmapScale = Math.min(1.6, Math.max(0.65, mindmapScale + delta));
            document.getElementById('mindmapSvgCanvas').style.transform = `scale(${mindmapScale})`;
        }

        function resetMindMap() {
            mindmapScale = 1;
            collapsedMindNodes.clear();
            if (currentStudyPayload?.mindMap) renderInteractiveMindMap(currentStudyPayload.mindMap);
        }

        // --- وظائف التبويب 3: كاشف النقاط العمياء ---
        function renderBlindSpotsSection(blindSpots) {
            const missingEl = document.getElementById('blindMissingList');
            const assumpEl = document.getElementById('blindAssumptionsList');
            const questEl = document.getElementById('blindQuestionsList');

            if (!blindSpots) return;

            missingEl.innerHTML = (blindSpots.missingAngles || []).map(item => `
                <div class="p-4 rounded-2xl bg-slate-950 border border-rose-500/30 hover:border-rose-500/60 transition">
                    <div class="flex items-center gap-2 text-rose-300 font-extrabold text-sm mb-1.5">
                        <i data-lucide="alert-circle" class="w-4 h-4 flex-shrink-0"></i>
                        <span>${escapeHtml(item.title)}</span>
                    </div>
                    <p class="text-xs text-slate-300 leading-relaxed">${escapeHtml(item.description)}</p>
                </div>
            `).join('');

            assumpEl.innerHTML = (blindSpots.hiddenAssumptions || []).map(assump => `
                <div class="p-3.5 rounded-2xl bg-slate-950 border border-amber-500/30 flex items-start gap-2.5 text-xs sm:text-sm text-slate-200">
                    <i data-lucide="lightbulb" class="w-4 h-4 text-amber-400 flex-shrink-0 mt-0.5"></i>
                    <span class="leading-relaxed">${escapeHtml(assump)}</span>
                </div>
            `).join('');

            questEl.innerHTML = (blindSpots.criticalQuestions || []).map(q => `
                <button onclick="sendCriticalQuestionToChat('${escapeJs(q)}')" class="w-full text-right p-3.5 rounded-2xl bg-slate-950 hover:bg-slate-800 border border-sky-500/30 hover:border-sky-400 flex items-center justify-between gap-3 transition group cursor-pointer">
                    <div class="flex items-start gap-2.5">
                        <i data-lucide="help-circle" class="w-4 h-4 text-sky-400 flex-shrink-0 mt-0.5"></i>
                        <span class="text-xs sm:text-sm text-slate-200 group-hover:text-white font-bold leading-relaxed">${escapeHtml(q)}</span>
                    </div>
                    <span class="text-[11px] font-extrabold text-sky-400 whitespace-nowrap flex items-center gap-1">
                        <span>اسأل وأجب فوراً</span>
                        <i data-lucide="arrow-left" class="w-3.5 h-3.5"></i>
                    </span>
                </button>
            `).join('');
        }

        function sendCriticalQuestionToChat(question) {
            activateTab('chat');
            document.getElementById('chatQuestionInput').value = question;
            submitChatQuestion(new Event('submit'));
        }

        // --- وظائف التبويب 4: اختبار الفهم (Quiz) ---
        function renderInteractiveQuiz(quizList) {
            document.getElementById('quizScoreText').textContent = '0';
            document.getElementById('quizTotalText').textContent = quizList.length;

            const container = document.getElementById('quizQuestionsContainer');
            container.innerHTML = quizList.map((q, qIdx) => `
                <div class="p-4 sm:p-5 rounded-2xl bg-slate-950 border border-slate-800 space-y-3">
                    <div class="flex items-start gap-2.5">
                        <span class="w-7 h-7 rounded-lg bg-sky-500/20 text-sky-400 flex items-center justify-center text-xs font-black flex-shrink-0">${qIdx + 1}</span>
                        <h4 class="text-sm sm:text-base font-extrabold text-white leading-snug">${escapeHtml(q.question)}</h4>
                    </div>
                    <div class="grid grid-cols-1 gap-2 pr-9">
                        ${(q.options || []).map((opt, oIdx) => `
                            <button onclick="chooseQuizAnswer(${qIdx}, ${oIdx})" id="quizBtn-${qIdx}-${oIdx}"
                                class="quiz-choice-${qIdx} text-right p-3 rounded-xl bg-slate-900 hover:bg-slate-800 border border-slate-800 text-xs sm:text-sm text-slate-200 transition flex items-center justify-between gap-2 cursor-pointer">
                                <span>${escapeHtml(opt)}</span>
                                <span class="choice-badge"></span>
                            </button>
                        `).join('')}
                    </div>
                    <div id="quizFeedback-${qIdx}" class="hidden mr-9 p-3 rounded-xl bg-slate-900 border border-slate-700 text-xs text-slate-300 leading-relaxed"></div>
                </div>
            `).join('');
        }

        function chooseQuizAnswer(qIdx, chosenIdx) {
            if (quizAnsweredSet.has(qIdx) || !currentStudyPayload) return;
            quizAnsweredSet.add(qIdx);

            const qObj = currentStudyPayload.quiz[qIdx];
            const isCorrect = chosenIdx === qObj.correctIndex;

            if (isCorrect) {
                quizCurrentScore++;
                document.getElementById('quizScoreText').textContent = quizCurrentScore;
            }

            document.querySelectorAll(`.quiz-choice-${qIdx}`).forEach((btn, idx) => {
                btn.disabled = true;
                btn.classList.remove('hover:bg-slate-800', 'cursor-pointer');
                if (idx === qObj.correctIndex) {
                    btn.className = `quiz-choice-${qIdx} text-right p-3 rounded-xl bg-emerald-500/20 border-2 border-emerald-500 text-xs sm:text-sm text-emerald-200 font-extrabold flex items-center justify-between gap-2`;
                    btn.querySelector('.choice-badge').textContent = '✅ صحيح';
                } else if (idx === chosenIdx && !isCorrect) {
                    btn.className = `quiz-choice-${qIdx} text-right p-3 rounded-xl bg-rose-500/20 border-2 border-rose-500 text-xs sm:text-sm text-rose-200 font-extrabold flex items-center justify-between gap-2`;
                    btn.querySelector('.choice-badge').textContent = '❌ خطأ';
                } else {
                    btn.classList.add('opacity-45');
                }
            });

            const fb = document.getElementById(`quizFeedback-${qIdx}`);
            fb.innerHTML = `<strong class="${isCorrect ? 'text-emerald-400' : 'text-amber-400'}">${isCorrect ? 'أحسنتِ! ' : 'التفسير الصحيح: '}</strong> ${escapeHtml(qObj.explanation)}`;
            fb.classList.remove('hidden');
        }

        function resetQuizState() {
            if (!currentStudyPayload) return;
            quizAnsweredSet.clear();
            quizCurrentScore = 0;
            renderInteractiveQuiz(currentStudyPayload.quiz || []);
            showToast('تمت إعادة ضبط الاختبار', 'info');
        }

        // --- وظائف التبويب 5: بطاقات الاستذكار 3D ---
        function updateFlashcardUI() {
            const cards = currentStudyPayload?.flashcards || [];
            if (cards.length === 0) return;

            const inner = document.getElementById('flashcard3DInner');
            inner.classList.remove('rotate-y-180');
            flashcardFlipped = false;

            const card = cards[flashcardIdx];
            document.getElementById('cardFrontText').textContent = card.front;
            document.getElementById('cardBackText').textContent = card.back;
            document.getElementById('cardProgressText').textContent = `${flashcardIdx + 1} / ${cards.length}`;
            document.getElementById('masteredCountBadge').textContent = `تم الحفظ: ${masteredCardsSet.size} / ${cards.length}`;

            const masteredBtn = document.getElementById('markMasteredBtn');
            const masteredLabel = document.getElementById('markMasteredLabel');
            if (masteredCardsSet.has(flashcardIdx)) {
                masteredBtn.className = "flex items-center gap-1.5 px-4 py-2.5 rounded-xl bg-emerald-500 text-slate-950 text-sm font-black transition cursor-pointer";
                masteredLabel.textContent = "محفوظة ✓";
            } else {
                masteredBtn.className = "flex items-center gap-1.5 px-4 py-2.5 rounded-xl bg-emerald-500/15 hover:bg-emerald-500/25 border border-emerald-500/40 text-emerald-300 text-sm font-extrabold transition cursor-pointer";
                masteredLabel.textContent = "تم الحفظ";
            }
        }

        function flipFlashcard() {
            const inner = document.getElementById('flashcard3DInner');
            flashcardFlipped = !flashcardFlipped;
            if (flashcardFlipped) inner.classList.add('rotate-y-180');
            else inner.classList.remove('rotate-y-180');
        }

        function navigateFlashcard(step) {
            const cards = currentStudyPayload?.flashcards || [];
            if (cards.length === 0) return;
            flashcardIdx = (flashcardIdx + step + cards.length) % cards.length;
            updateFlashcardUI();
        }

        function toggleCardMastered() {
            if (masteredCardsSet.has(flashcardIdx)) {
                masteredCardsSet.delete(flashcardIdx);
            } else {
                masteredCardsSet.add(flashcardIdx);
                showToast('رائع! تم تحديد البطاقة كمحفوظة', 'success');
            }
            updateFlashcardUI();
        }

        // --- وظائف التبويب 6: قاموس المصطلحات مع فلترة ---
        function renderGlossaryList(items) {
            const grid = document.getElementById('glossaryCardsGrid');
            if (items.length === 0) {
                grid.innerHTML = `<div class="col-span-2 text-center py-8 text-xs text-slate-500">لا توجد مصطلحات مطابقة للبحث</div>`;
                return;
            }
            grid.innerHTML = items.map(g => `
                <div class="p-4 rounded-2xl bg-slate-950 border border-slate-800 hover:border-sky-500/40 transition">
                    <div class="flex items-center justify-between gap-2 mb-2">
                        <span class="text-sm font-black text-sky-300">${escapeHtml(g.term)}</span>
                        <span class="px-2.5 py-0.5 rounded-md bg-indigo-500/15 text-indigo-300 text-[11px] font-bold">${escapeHtml(g.translation)}</span>
                    </div>
                    <p class="text-xs text-slate-300 leading-relaxed">${escapeHtml(g.definition)}</p>
                </div>
            `).join('');
        }

        function filterGlossaryItems() {
            if (!currentStudyPayload?.glossary) return;
            const q = document.getElementById('glossarySearchInput').value.trim().toLowerCase();
            const filtered = currentStudyPayload.glossary.filter(item =>
                item.term.toLowerCase().includes(q) ||
                item.translation.toLowerCase().includes(q) ||
                item.definition.toLowerCase().includes(q)
            );
            renderGlossaryList(filtered);
        }

        // --- وظائف التبويب 7: خطة التطبيق (Action Plan) ---
        function renderActionPlanList(tasks) {
            const container = document.getElementById('actionChecklistContainer');
            container.innerHTML = tasks.map((task, idx) => `
                <label class="flex items-center gap-3.5 p-4 rounded-2xl bg-slate-950 border border-slate-800 hover:border-teal-500/40 cursor-pointer transition">
                    <input type="checkbox" onchange="recalculateActionProgress()" class="action-task-cb w-5 h-5 rounded-md accent-teal-500 cursor-pointer">
                    <span class="text-xs sm:text-sm text-slate-200 font-bold leading-relaxed">${escapeHtml(task)}</span>
                </label>
            `).join('');
            recalculateActionProgress();
        }

        function recalculateActionProgress() {
            const boxes = document.querySelectorAll('.action-task-cb');
            const total = boxes.length;
            const done = Array.from(boxes).filter(b => b.checked).length;
            const pct = total > 0 ? Math.round((done / total) * 100) : 0;

            document.getElementById('actionPercentText').textContent = `${pct}% (${done}/${total})`;
            document.getElementById('actionProgressBar').style.width = `${pct}%`;
        }

        // --- وظائف التبويب 8: اسأل الفيديو (دردشة تفاعلية) ---
        function initChatWorkspace(suggestions) {
            const suggBar = document.getElementById('suggestedQuestionsBar');
            suggBar.innerHTML = suggestions.map(q => `
                <button onclick="quickAskQuestion('${escapeJs(q)}')" class="text-xs px-3 py-1.5 rounded-xl bg-slate-950 hover:bg-slate-800 border border-slate-800 hover:border-sky-500/40 text-sky-300 font-bold transition cursor-pointer">
                    💡 ${escapeHtml(q)}
                </button>
            `).join('');

            const chatBox = document.getElementById('chatMessagesBox');
            chatBox.innerHTML = `
                <div class="flex items-start gap-2.5 text-xs sm:text-sm">
                    <div class="w-7 h-7 rounded-lg bg-sky-500/20 text-sky-400 flex items-center justify-center flex-shrink-0 mt-0.5">
                        <i data-lucide="bot" class="w-4 h-4"></i>
                    </div>
                    <div class="bg-slate-900 border border-slate-800 rounded-2xl rounded-tr-none p-3 text-slate-200 leading-relaxed">
                        أهلاً بكِ! أنا جاهز للإجابة عن أي سؤال حول هذا الفيديو أو مناقشة الأسئلة النقدية. اختاري سؤالاً مقترحاً أو اكتبي سؤالكِ بالأسفل.
                    </div>
                </div>
            `;
        }

        function quickAskQuestion(q) {
            document.getElementById('chatQuestionInput').value = q;
            submitChatQuestion(new Event('submit'));
        }

        async function submitChatQuestion(e) {
            e.preventDefault();
            const input = document.getElementById('chatQuestionInput');
            const question = input.value.trim();
            if (!question || !currentStudyPayload) return;

            input.value = '';
            appendChatBubble('user', question);

            const sendBtn = document.getElementById('sendChatBtn');
            sendBtn.disabled = true;

            const tempId = 'chat-wait-' + Date.now();
            appendChatBubble('bot', 'جاري صياغة الإجابة من محتوى الفيديو...', tempId);

            // إذا كان في وضع المثال الجاهز، نقدم رداً ذكياً فورياً حتى لو لم يتوفر اتصال خارجي
            if (isDemoMode) {
                await new Promise(r => setTimeout(r, 450));
                const demoReply = generateSmartDemoReply(question);
                const el = document.getElementById(tempId);
                if (el) el.innerHTML = marked.parse(demoReply);
                sendBtn.disabled = false;
                return;
            }

            const prompt = `أنت مساعد دراسي ذكي تجيب على سؤال الطالب باللغة العربية بناءً على محتوى الفيديو التالي:\nالعنوان: ${currentStudyPayload.title}\nالفكرة العامة: ${currentStudyPayload.generalIdea}\nالشرح: ${currentStudyPayload.detailedExplanationMarkdown}\n\nسؤال الطالب: ${question}\nأجب بوضوح وعمق وبأمثلة مبسطة.`;

            try {
                const answer = await fetchGeminiContent({
                    contents: [{ parts: [{ text: prompt }] }]
                });
                const el = document.getElementById(tempId);
                if (el) el.innerHTML = marked.parse(answer);
            } catch {
                const el = document.getElementById(tempId);
                if (el) el.innerHTML = marked.parse(generateSmartDemoReply(question));
            } finally {
                sendBtn.disabled = false;
            }
        }

        function generateSmartDemoReply(q) {
            if (q.includes("تكرار") || q.includes("حلقة")) {
                return "لمنع الوكيل من الدخول في حلقة تكرار لا نهائية، نضع **حد أقصى لعدد الخطوات (Max Iterations)** مثل 5 محاولات، ونضيف شرط توقف واضح يطلب تدخل المستخدم إذا تكرر نفس الخطأ مرتين.";
            }
            if (q.includes("بناء") || q.includes("مبتدئة")) {
                return "للبدء كبداية عملية: ابدئي بتحديد مهمة واحدة واضحة (مثل تلخيص مقالات)، اربطي نموذجاً لغوياً بأداة بحث واحدة، واختبري كيف يقسّم النموذج الخطوات قبل توسيع صلاحياته.";
            }
            if (q.includes("فريق") || q.includes("متعاونين")) {
                return "الوكيل الواحد يناسب المهام المباشرة، أما **فريق الوكلاء (Multi-Agent)** فيوزع الأدوار: وكيل يجمع المعلومات، وكيل يصيغ المحتوى، ووكيل ثالث يراجع الجودة ويدقق الأخطاء.";
            }
            return `بناءً على محتوى الفيديو حول **"${currentStudyPayload.title}"**:\n\nيركز الجواب على تطبيق مبدأ **التخطيط وتقسيم المهام** مع **المراجعة الذاتية** للوصول إلى أفضل نتيجة دقيقة، مع إبقاء القرارات الحساسة تحت إشرافكِ المباشر.`;
        }

        function appendChatBubble(sender, text, id = '') {
            const box = document.getElementById('chatMessagesBox');
            const row = document.createElement('div');
            row.className = `flex items-start gap-2.5 text-xs sm:text-sm ${sender === 'user' ? 'flex-row-reverse' : ''}`;

            const avatar = sender === 'user'
                ? `<div class="w-7 h-7 rounded-lg bg-indigo-500/20 text-indigo-300 flex items-center justify-center flex-shrink-0 mt-0.5"><i data-lucide="user" class="w-4 h-4"></i></div>`
                : `<div class="w-7 h-7 rounded-lg bg-sky-500/20 text-sky-400 flex items-center justify-center flex-shrink-0 mt-0.5"><i data-lucide="bot" class="w-4 h-4"></i></div>`;

            const style = sender === 'user'
                ? 'bg-indigo-600/30 border border-indigo-500/40 text-white rounded-2xl rounded-tl-none p-3'
                : 'bg-slate-900 border border-slate-800 text-slate-200 rounded-2xl rounded-tr-none p-3 prose-custom';

            row.innerHTML = `${avatar}<div ${id ? `id="${id}"` : ''} class="${style} max-w-[85%] leading-relaxed">${sender === 'user' ? escapeHtml(text) : text}</div>`;
            box.appendChild(row);
            box.scrollTop = box.scrollHeight;
            lucide.createIcons();
        }

        // --- الشريط الجانبي: دفتر الملاحظات لكل فيديو + السجل + الطباعة ---
        function handleVideoNoteInput() {
            const val = document.getElementById('videoNotesTextarea').value;
            localStorage.setItem(STORAGE_NOTES_PREFIX + currentSessionId, val);
            const ind = document.getElementById('noteSavedIndicator');
            ind.innerHTML = '<i data-lucide="check" class="w-3 h-3"></i> تم الحفظ';
            lucide.createIcons();
        }

        function loadNoteForSession(sessionId) {
            const saved = localStorage.getItem(STORAGE_NOTES_PREFIX + sessionId) || '';
            document.getElementById('videoNotesTextarea').value = saved;
            const title = currentStudyPayload?.title || "الجلسة الحالية";
            document.getElementById('noteContextLabel').textContent = `ملاحظات: ${title}`;
        }

        function getHistoryArray() {
            try { return JSON.parse(localStorage.getItem(STORAGE_HISTORY_KEY) || '[]'); }
            catch { return []; }
        }

        function saveStudyToHistory(studyData) {
            let list = getHistoryArray().filter(item => item.id !== studyData.id);
            list.unshift({
                id: studyData.id,
                title: studyData.title,
                date: new Date().toLocaleDateString('ar-EG', { day: 'numeric', month: 'short', hour: '2-digit', minute: '2-digit' }),
                payload: studyData
            });
            if (list.length > 15) list = list.slice(0, 15);
            localStorage.setItem(STORAGE_HISTORY_KEY, JSON.stringify(list));
            renderSavedHistoryList();
        }

        function renderSavedHistoryList() {
            const list = getHistoryArray();
            document.getElementById('savedHistoryCount').textContent = list.length;
            const container = document.getElementById('savedHistoryContainer');

            if (list.length === 0) {
                container.innerHTML = `<div class="text-center py-6 text-xs text-slate-500">لا توجد فيديوهات محفوظة في السجل بعد</div>`;
                return;
            }

            container.innerHTML = list.map(item => `
                <div onclick="restoreHistoryItem('${escapeJs(item.id)}')" class="p-3 rounded-2xl bg-slate-950 hover:bg-slate-800 border border-slate-800 hover:border-sky-500/40 cursor-pointer transition group flex items-start justify-between gap-2">
                    <div class="min-w-0 flex-1">
                        <h4 class="text-xs font-extrabold text-slate-200 group-hover:text-sky-300 line-clamp-1">${escapeHtml(item.title)}</h4>
                        <span class="text-[10px] text-slate-400 block mt-0.5">${escapeHtml(item.date)}</span>
                    </div>
                    <button onclick="removeHistoryItem(event, '${escapeJs(item.id)}')" title="حذف" class="text-slate-500 hover:text-rose-400 p-1 rounded-lg">
                        <i data-lucide="trash-2" class="w-3.5 h-3.5"></i>
                    </button>
                </div>
            `).join('');
            lucide.createIcons();
        }

        function restoreHistoryItem(id) {
            const found = getHistoryArray().find(i => i.id === id);
            if (!found) return;
            currentSessionId = found.id;
            currentStudyPayload = found.payload;
            isDemoMode = (found.id === READY_DEMO_DATA.id);
            populateWorkspaceWithData(found.payload, isDemoMode);
            loadNoteForSession(currentSessionId);
            showToast('تم استرجاع التحليل وملاحظاتك المحفوظة', 'success');
        }

        function removeHistoryItem(e, id) {
            e.stopPropagation();
            const filtered = getHistoryArray().filter(i => i.id !== id);
            localStorage.setItem(STORAGE_HISTORY_KEY, JSON.stringify(filtered));
            renderSavedHistoryList();
        }

        function clearHistoryStorage() {
            localStorage.removeItem(STORAGE_HISTORY_KEY);
            renderSavedHistoryList();
            showToast('تم مسح سجل الفيديوهات', 'info');
        }

        // تصدير وطباعة التقرير الكامل
        function exportAndPrintReport() {
            if (!currentStudyPayload) {
                showToast('قومي بتحليل فيديو أو تشغيل المثال الجاهز أولاً لتصدير التقرير', 'info');
                return;
            }
            document.getElementById('printReportTitle').textContent = currentStudyPayload.title;
            const userNote = document.getElementById('videoNotesTextarea').value.trim();

            let extraHtml = '';
            if (userNote) {
                extraHtml += `<div><h3 class="text-lg font-bold text-sky-700 mb-1">ملاحظاتي الشخصية:</h3><p class="text-sm text-slate-800 whitespace-pre-wrap">${escapeHtml(userNote)}</p></div>`;
            }
            if (currentStudyPayload.blindSpots?.missingAngles?.length) {
                extraHtml += `<div><h3 class="text-lg font-bold text-sky-700 mb-1">النقاط العمياء والزوايا المفقودة:</h3><ul class="list-disc pr-5 text-sm text-slate-800">` +
                    currentStudyPayload.blindSpots.missingAngles.map(m => `<li><strong>${escapeHtml(m.title)}:</strong> ${escapeHtml(m.description)}</li>`).join('') + `</ul></div>`;
            }
            if (currentStudyPayload.flashcards?.length) {
                extraHtml += `<div><h3 class="text-lg font-bold text-sky-700 mb-1">بطاقات المراجعة:</h3><div class="space-y-1.5">` +
                    currentStudyPayload.flashcards.map(c => `<div class="p-2 border border-slate-300 rounded text-sm"><strong>${escapeHtml(c.front)}:</strong> ${escapeHtml(c.back)}</div>`).join('') + `</div></div>`;
            }

            document.getElementById('printFullReport').innerHTML = extraHtml;
            activateTab('explain');
            window.print();
        }

        // نظام الإشعارات Toast
        let toastTimeout;
        function showToast(message, type = 'info') {
            const toast = document.getElementById('toast');
            const msgEl = document.getElementById('toastMessage');
            const iconEl = document.getElementById('toastIcon');

            msgEl.textContent = message;
            toast.className = "fixed bottom-6 left-1/2 -translate-x-1/2 z-50 flex items-center gap-3 px-5 py-3.5 rounded-2xl shadow-2xl border backdrop-blur-md transition-all duration-300";

            if (type === 'success') {
                toast.classList.add('bg-emerald-950/95', 'border-emerald-500/50', 'text-emerald-200');
                iconEl.setAttribute('data-lucide', 'check-circle-2');
            } else if (type === 'error') {
                toast.classList.add('bg-rose-950/95', 'border-rose-500/50', 'text-rose-200');
                iconEl.setAttribute('data-lucide', 'alert-circle');
            } else {
                toast.classList.add('bg-slate-900/95', 'border-sky-500/50', 'text-sky-200');
                iconEl.setAttribute('data-lucide', 'info');
            }

            lucide.createIcons();
            clearTimeout(toastTimeout);
            toastTimeout = setTimeout(() => toast.classList.add('hidden'), 3500);
        }

        function shortText(str, max) {
            if (!str) return '';
            return str.length > max ? str.slice(0, max - 1) + '…' : str;
        }

        function escapeHtml(str) {
            const div = document.createElement('div');
            div.textContent = str || '';
            return div.innerHTML;
        }

        function escapeJs(str) {
            return (str || '').replace(/\\/g, '\\\\').replace(/'/g, "\\'").replace(/\n/g, ' ');
        }
    </script>
</body>
</html>
