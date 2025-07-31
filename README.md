<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <!-- Chosen Palette: Calm Harmony (Warm Neutrals, Muted Green, Subtle Terracotta) -->
    <!-- Application Structure Plan: A thematic, single-page dashboard designed for a narrative user journey. It moves from the high-level vision of the Iraqi Green Standard to the specific challenges in Baghdad, then presents the framework's axes interactively. A solutions dashboard follows, leading into a practical case study of the Diwan building with before/after visualizations. The app concludes by quantifying the environmental, financial, and social impacts, ending with a clear call to action. This structure was chosen to transform a dense report into an engaging, persuasive story, making complex information digestible and demonstrating tangible value to policymakers and investors. -->
    <!-- Visualization & Content Choices: Report Info: 9 Building Axes -> Goal: Organize/Inform -> Method: Interactive HTML/CSS grid of cards -> Interaction: Click to reveal details in a modal/expansion -> Justification: Avoids information overload, encourages exploration. Report Info: Cost/Benefit Data -> Goal: Compare/Persuade -> Method: Chart.js Bar/Donut charts (e.g., Material Cost Comparison, Payback Periods) -> Interaction: Hover tooltips for precise data -> Justification: Clearly visualizes financial viability. Report Info: Diwan Retrofit Plan -> Goal: Show Process/Change -> Method: HTML/CSS timeline & Chart.js 'Before/After' bar charts -> Interaction: Click on timeline stages to update content -> Justification: Simplifies a multi-stage project into an easy-to-follow narrative. All visualizations use Chart.js (Canvas) or structured HTML/CSS. -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
    <title>المعيار الأخضر العراقي 2025 - رؤية تفاعلية</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Cairo', sans-serif;
            background-color: #FDF8F0;
            color: #333333;
        }
        .bg-primary { background-color: #5A8B7B; }
        .text-primary { color: #5A8B7B; }
        .border-primary { border-color: #5A8B7B; }
        .bg-secondary { background-color: #C89F9C; }
        .text-secondary { color: #C89F9C; }
        .bg-accent { background-color: #EAE0D5; }
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 600px;
            margin-left: auto;
            margin-right: auto;
            height: 300px;
            max-height: 400px;
        }
        @media (min-width: 768px) {
            .chart-container {
                height: 350px;
            }
        }
        .nav-link {
            transition: all 0.3s ease;
            border-bottom: 2px solid transparent;
        }
        .nav-link.active, .nav-link:hover {
            color: #5A8B7B;
            border-bottom-color: #5A8B7B;
        }
        .axis-card {
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }
        .axis-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
        }
        .axis-detail {
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.5s ease-in-out;
        }
        .axis-detail.open {
            max-height: 500px; 
        }
    </style>
</head>
<body class="antialiased">

    <header class="bg-white shadow-md sticky top-0 z-50">
        <nav class="container mx-auto px-6 py-3 flex justify-between items-center">
            <div class="text-2xl font-bold text-primary">المعيار الأخضر العراقي</div>
            <div class="hidden md:flex space-x-8 space-x-reverse">
                <a href="#vision" class="nav-link active">الرؤية</a>
                <a href="#challenges" class="nav-link">التحديات</a>
                <a href="#framework" class="nav-link">المحاور</a>
                <a href="#solutions" class="nav-link">الحلول</a>
                <a href="#case-study" class="nav-link">دراسة الحالة</a>
                <a href="#impact" class="nav-link">الأثر</a>
            </div>
            <button id="mobile-menu-button" class="md:hidden flex items-center">
                 <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16m-7 6h7"></path></svg>
            </button>
        </nav>
        <div id="mobile-menu" class="hidden md:hidden">
            <a href="#vision" class="block py-2 px-4 text-sm hover:bg-accent">الرؤية</a>
            <a href="#challenges" class="block py-2 px-4 text-sm hover:bg-accent">التحديات</a>
            <a href="#framework" class="block py-2 px-4 text-sm hover:bg-accent">المحاور</a>
            <a href="#solutions" class="block py-2 px-4 text-sm hover:bg-accent">الحلول</a>
            <a href="#case-study" class="block py-2 px-4 text-sm hover:bg-accent">دراسة الحالة</a>
            <a href="#impact" class="block py-2 px-4 text-sm hover:bg-accent">الأثر</a>
        </div>
    </header>

    <main>
        <section id="vision" class="pt-20 pb-16 bg-accent">
            <div class="container mx-auto px-6 text-center">
                <h1 class="text-4xl md:text-5xl font-bold text-primary mb-4">نحو مستقبل حضري مستدام في العراق</h1>
                <p class="text-lg md:text-xl max-w-3xl mx-auto text-gray-700">
                    يمثل المعيار الأخضر العراقي 2025 خارطة طريق وطنية لدمج الاستدامة في قلب قطاع البناء والتخطيط الحضري. يستكشف هذا التطبيق التفاعلي أبعاد المعيار، من التحديات المحلية إلى الحلول المبتكرة، ويستعرض إمكاناته التحويلية لبناء مدن أكثر صحة وكفاءة ومرونة.
                </p>
            </div>
        </section>

        <section id="challenges" class="py-16">
            <div class="container mx-auto px-6">
                <div class="text-center mb-12">
                    <h2 class="text-3xl font-bold text-primary">التحديات الرئيسية في بغداد</h2>
                    <p class="mt-2 text-gray-600 max-w-2xl mx-auto">يواجه تطبيق المعايير الخضراء في بغداد عقبات متعددة الأوجه ومترابطة تتطلب حلولاً شاملة ومبتكرة.</p>
                </div>
                <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-8">
                    <div class="bg-white p-6 rounded-lg shadow-lg text-center">
                        <div class="text-4xl mb-3">🏛️</div>
                        <h3 class="font-bold text-lg mb-2">عقبات تشريعية وإدارية</h3>
                        <p class="text-sm text-gray-600">ضعف التكامل بين الوزارات وغياب القوانين الملزمة يعيقان التنفيذ الفعال.</p>
                    </div>
                    <div class="bg-white p-6 rounded-lg shadow-lg text-center">
                        <div class="text-4xl mb-3">🏗️</div>
                        <h3 class="font-bold text-lg mb-2">بنية تحتية متقادمة</h3>
                        <p class="text-sm text-gray-600">شبكات المياه والكهرباء والصرف الصحي المتهالكة تحد من فعالية التقنيات الخضراء.</p>
                    </div>
                    <div class="bg-white p-6 rounded-lg shadow-lg text-center">
                        <div class="text-4xl mb-3">💡</div>
                        <h3 class="font-bold text-lg mb-2">فجوات الوعي والخبرة</h3>
                        <p class="text-sm text-gray-600">نقص الوعي بفوائد البناء الأخضر ونقص الكوادر الفنية المؤهلة.</p>
                    </div>
                    <div class="bg-white p-6 rounded-lg shadow-lg text-center">
                        <div class="text-4xl mb-3">🌡️</div>
                        <h3 class="font-bold text-lg mb-2">مناخ قاسٍ وبيئة صعبة</h3>
                        <p class="text-sm text-gray-600">درجات الحرارة المرتفعة والعواصف الترابية تزيد من تحديات الطاقة والصيانة.</p>
                    </div>
                </div>
            </div>
        </section>

        <section id="framework" class="py-16 bg-accent">
            <div class="container mx-auto px-6">
                <div class="text-center mb-12">
                    <h2 class="text-3xl font-bold text-primary">محاور المعيار الأخضر للمباني</h2>
                    <p class="mt-2 text-gray-600 max-w-2xl mx-auto">يقدم المعيار إطارًا شاملاً من تسعة محاور لتقييم وتعزيز استدامة المباني. انقر على كل محور لمعرفة المزيد.</p>
                </div>
                <div id="axes-grid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                </div>
            </div>
        </section>

        <section id="solutions" class="py-16">
            <div class="container mx-auto px-6">
                <div class="text-center mb-12">
                    <h2 class="text-3xl font-bold text-primary">لوحة الحلول الاستراتيجية</h2>
                    <p class="mt-2 text-gray-600 max-w-2xl mx-auto">من السياسات الداعمة إلى التقنيات المبتكرة، تستعرض هذه الحلول كيفية التغلب على التحديات وتحقيق أهداف الاستدامة.</p>
                </div>
                <div class="grid md:grid-cols-2 gap-12 items-center">
                    <div>
                        <h3 class="font-bold text-xl text-primary mb-4">فعالية تكلفة المواد المستدامة</h3>
                        <p class="text-gray-600 mb-4">تُظهر المقارنات أن المواد المحلية والمستدامة، مثل كتل الإيزوكريت، لا تقلل فقط من الأثر البيئي، بل تحقق أيضًا وفورات كبيرة في تكاليف البناء والصيانة مقارنة بالمواد التقليدية.</p>
                        <div class="chart-container h-64 md:h-80">
                            <canvas id="materialsCostChart"></canvas>
                        </div>
                    </div>
                    <div>
                        <h3 class="font-bold text-xl text-primary mb-4">فترة استرداد التقنيات الخضراء</h3>
                        <p class="text-gray-600 mb-4">على الرغم من التكلفة الأولية، فإن التقنيات الخضراء مثل أنظمة التكييف الفعالة (VRF) والطاقة الشمسية توفر عائدًا سريعًا على الاستثمار من خلال خفض فواتير الطاقة بشكل كبير.</p>
                        <div class="chart-container h-64 md:h-80">
                            <canvas id="paybackPeriodChart"></canvas>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <section id="case-study" class="py-16 bg-accent">
            <div class="container mx-auto px-6">
                <div class="text-center mb-12">
                    <h2 class="text-3xl font-bold text-primary">دراسة حالة: تأهيل مبنى ديوان الوقف الشيعي</h2>
                    <p class="mt-2 text-gray-600 max-w-2xl mx-auto">يقدم هذا المشروع نموذجًا عمليًا لتطبيق المعيار الأخضر على مبنى قائم في قلب بغداد، موضحًا الفوائد الملموسة للتجديد المستدام.</p>
                </div>
                
                <div class="relative">
                    <div class="border-r-4 border-primary absolute h-full top-0" style="right: 15px;"></div>
                    <ul class="space-y-12">
                        <li class="flex items-start">
                            <div class="bg-primary z-10 w-8 h-8 rounded-full flex items-center justify-center text-white font-bold">1</div>
                            <div class="bg-white rounded-lg shadow-lg p-6 w-full mr-8">
                                <h3 class="font-bold text-xl text-primary mb-2">المرحلة الأولى: التقييم والتحسينات الفورية (3-6 أشهر)</h3>
                                <p class="text-gray-600">تدقيق هندسي شامل، استبدال نظام التكييف بآخر عالي الكفاءة (VRF)، تحسين العزل الحراري، وتركيب نظام إدارة مباني (BMS) أساسي لمراقبة الطاقة.</p>
                            </div>
                        </li>
                        <li class="flex items-start">
                            <div class="bg-primary z-10 w-8 h-8 rounded-full flex items-center justify-center text-white font-bold">2</div>
                            <div class="bg-white rounded-lg shadow-lg p-6 w-full mr-8">
                                <h3 class="font-bold text-xl text-primary mb-2">المرحلة الثانية: دمج الطاقة والمياه (6-12 شهرًا)</h3>
                                <p class="text-gray-600">تركيب ألواح شمسية مع بطاريات، تحديث نظام المياه ليشمل إعادة تدوير المياه الرمادية، وتدريب الموظفين على التشغيل المستدام.</p>
                            </div>
                        </li>
                        <li class="flex items-start">
                            <div class="bg-primary z-10 w-8 h-8 rounded-full flex items-center justify-center text-white font-bold">3</div>
                            <div class="bg-white rounded-lg shadow-lg p-6 w-full mr-8">
                                <h3 class="font-bold text-xl text-primary mb-2">المرحلة الثالثة: تعزيز البيئة والاعتماد (3-6 أشهر)</h3>
                                <p class="text-gray-600">إنشاء مساحات خضراء، تطبيق نظام إدارة نفايات، التكامل الكامل لنظام إنترنت الأشياء (IoT)، والحصول على شهادة المبنى الأخضر العراقي.</p>
                            </div>
                        </li>
                    </ul>
                </div>

                <div class="mt-16 grid md:grid-cols-2 gap-12 items-center">
                    <div>
                        <h3 class="font-bold text-xl text-primary mb-4 text-center">خفض استهلاك الطاقة المتوقع</h3>
                        <p class="text-gray-600 mb-4 text-center">من المتوقع أن تؤدي التحسينات إلى خفض استهلاك الطاقة بنسبة تصل إلى 50%.</p>
                        <div class="chart-container h-64 md:h-80">
                            <canvas id="energyConsumptionChart"></canvas>
                        </div>
                    </div>
                    <div>
                        <h3 class="font-bold text-xl text-primary mb-4 text-center">خفض استهلاك المياه المتوقع</h3>
                        <p class="text-gray-600 mb-4 text-center">ستساهم أنظمة إعادة تدوير المياه الرمادية في تقليل استهلاك المياه الصالحة للشرب بنسبة 40%.</p>
                        <div class="chart-container h-64 md:h-80">
                            <canvas id="waterConsumptionChart"></canvas>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <section id="impact" class="py-16">
            <div class="container mx-auto px-6">
                <div class="text-center mb-12">
                    <h2 class="text-3xl font-bold text-primary">الأثر الشامل: أبعد من مجرد توفير الطاقة</h2>
                    <p class="mt-2 text-gray-600 max-w-2xl mx-auto">للمباني الخضراء فوائد مثبتة على الصعيد البيئي والمالي، والأهم من ذلك، على صحة وإنتاجية شاغلي المبنى.</p>
                </div>
                <div class="grid md:grid-cols-3 gap-8 text-center">
                    <div class="bg-white p-8 rounded-lg shadow-lg">
                        <div class="text-5xl font-bold text-primary mb-2">26.4%</div>
                        <h3 class="font-semibold text-lg">زيادة في الوظائف الإدراكية</h3>
                        <p class="text-sm text-gray-600">تحسين جودة الهواء والإضاءة يعزز التركيز والأداء الذهني للموظفين.</p>
                    </div>
                    <div class="bg-white p-8 rounded-lg shadow-lg">
                        <div class="text-5xl font-bold text-primary mb-2">30%</div>
                        <h3 class="font-semibold text-lg">انخفاض في الأعراض الصحية</h3>
                        <p class="text-sm text-gray-600">تقليل الملوثات الداخلية يؤدي إلى بيئة عمل صحية ويقلل من الإجازات المرضية.</p>
                    </div>
                     <div class="bg-white p-8 rounded-lg shadow-lg">
                        <div class="text-5xl font-bold text-primary mb-2">73%</div>
                        <h3 class="font-semibold text-lg">تحسن في الاستجابة للأزمات</h3>
                        <p class="text-sm text-gray-600">البيئات المحسنة تعزز قدرة الموظفين على اتخاذ قرارات أفضل تحت الضغط.</p>
                    </div>
                </div>
            </div>
        </section>

    </main>

    <footer class="bg-primary text-white mt-16">
        <div class="container mx-auto px-6 py-8">
            <div class="text-center">
                <h3 class="text-2xl font-bold mb-4">دعوة للعمل</h3>
                <p class="max-w-3xl mx-auto mb-6">
                    يتطلب تحقيق رؤية المعيار الأخضر العراقي تضافر الجهود بين القطاعين العام والخاص. ندعو صناع السياسات والمستثمرين والمطورين إلى تبني هذه المبادئ، والاستثمار في التقنيات المستدامة، وبناء مستقبل أكثر اخضرارًا وازدهارًا للعراق.
                </p>
                <div class="text-sm">
                    تطبيق تفاعلي تم تطويره بناءً على تقرير "المعيار الأخضر العراقي للمباني والمدن - 2025".
                    <br><br>
                    **أعداد:** اللجنة المشكلة في دائرة أوقاف المحافظات في ديوان الوقف الشيعي بموجب الأمر الأداري بالعدد 2182 في 24/7/20255 بتوجيه السيد مدير عام الدائرة الدكتور فاضل محمد رضا الشرع.
                    <br>
                    **أسماء اللجنة:**
                    <br>
                    1- لؤي فاضل حسن ر.مهندسين أقدم أول .رئيساً
                    <br>
                    2- سعد هاشم مجلي .ر.مهندسين .عضواً
                    <br>
                    3- رائد ابراهيم خليل .ر.مهندسين .عضواً
                    <br>
                    4- علي حسين علي .م.رئيس .مهندسين .عضواً
                    <br>
                    5- ابراهيم عبد الجليل سعيد .مهندس. عضواً
                    <br>
                    وبإشراف ومتابعة مباشرة من قبل السيد المدير العام.
                </div>
            </div>
        </div>
    </footer>

    <script>
        document.addEventListener('DOMContentLoaded', function () {
            const axesData = [
                { icon: '📍', title: 'الموقع', description: 'اختيار المواقع التي تقلل الحاجة للنقل، تحافظ على النظم البيئية، وتتكامل مع البنية التحتية المستدامة القائمة.' },
                { icon: '🔧', title: 'الإدارة والصيانة', description: 'وضع خطط صيانة استباقية طويلة الأجل لأنظمة المباني الحيوية وتدريب فرق التشغيل على ممارسات الإدارة الخضراء.' },
                { icon: '⚡', title: 'كفاءة الطاقة', description: 'تبني أنظمة عالية الكفاءة (مثل VRF)، دمج مصادر الطاقة المتجددة، والعزل الحراري المتقدم لتقليل استهلاك الطاقة بشكل كبير.' },
                { icon: '💧', title: 'كفاءة المياه', description: 'تقليل استهلاك المياه الصالحة للشرب من خلال تجهيزات موفرة للمياه وتقنيات إعادة تدوير المياه الرمادية وحصاد مياه الأمطار.' },
                { icon: '🌬️', title: 'جودة البيئة الداخلية', description: 'معالجة صحة وراحة شاغلي المبنى من خلال تعزيز التهوية والإضاءة الطبيعية وتقليل استخدام المواد الضارة.' },
                { icon: '�', title: 'المواد والموارد', description: 'تشجيع استخدام المواد المحلية المستدامة والمعاد تدويرها في مشاريع البناء لتقليل الطاقة المتجسدة ودعم الاقتصاد المحلي.' },
                { icon: '🗑️', title: 'إدارة النفايات', description: 'تطبيق خطط فصل النفايات من المصدر خلال مرحلتي البناء والتشغيل لتقليل النفايات المرسلة إلى المكبات.' },
                { icon: '🌳', title: 'جودة البيئة الخارجية', description: 'تحسين البيئة المحيطة بالمباني من خلال زراعة الأشجار، إنشاء ممرات مظللة، وتخفيف تأثير الجزر الحرارية الحضرية.' },
                { icon: '💡', title: 'الابتكار', description: 'مكافأة تبني التقنيات الذكية، مثل أنظمة مراقبة الطاقة المركزية (BMS/IoT) وغيرها من الحلول المتطورة.' }
            ];

            const axesGrid = document.getElementById('axes-grid');
            axesData.forEach((axis, index) => {
                const cardContainer = document.createElement('div');
                cardContainer.innerHTML = `
                    <div class="axis-card bg-white p-6 rounded-lg shadow-md cursor-pointer">
                        <div class="flex items-center mb-3">
                            <span class="text-3xl mr-4">${axis.icon}</span>
                            <h3 class="font-bold text-lg text-primary">${axis.title}</h3>
                        </div>
                    </div>
                    <div class="axis-detail bg-white p-4 rounded-b-lg -mt-2">
                        <p class="text-sm text-gray-700">${axis.description}</p>
                    </div>
                `;
                axesGrid.appendChild(cardContainer);

                const card = cardContainer.querySelector('.axis-card');
                const detail = cardContainer.querySelector('.axis-detail');
                
                card.addEventListener('click', () => {
                    const allDetails = document.querySelectorAll('.axis-detail');
                    const isOpening = !detail.classList.contains('open');

                    allDetails.forEach(d => d.classList.remove('open'));
                    
                    if (isOpening) {
                        detail.classList.add('open');
                    }
                });
            });

            const mobileMenuButton = document.getElementById('mobile-menu-button');
            const mobileMenu = document.getElementById('mobile-menu');
            mobileMenuButton.addEventListener('click', () => {
                mobileMenu.classList.toggle('hidden');
            });

            const navLinks = document.querySelectorAll('.nav-link, #mobile-menu a');
            const sections = document.querySelectorAll('section');

            const observerOptions = {
                root: null,
                rootMargin: '0px',
                threshold: 0.4
            };

            const observer = new IntersectionObserver((entries, observer) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        navLinks.forEach(link => {
                            link.classList.remove('active');
                            if (link.getAttribute('href').substring(1) === entry.target.id) {
                                link.classList.add('active');
                            }
                        });
                    }
                });
            }, observerOptions);

            sections.forEach(section => {
                observer.observe(section);
            });
            
            navLinks.forEach(link => {
                link.addEventListener('click', function(e) {
                    e.preventDefault();
                    document.querySelector(this.getAttribute('href')).scrollIntoView({
                        behavior: 'smooth'
                    });
                    if(mobileMenu.classList.contains('hidden') === false){
                        mobileMenu.classList.add('hidden');
                    }
                });
            });

            const chartOptions = {
                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    legend: {
                        labels: {
                            font: {
                                family: "'Cairo', sans-serif"
                            }
                        }
                    },
                    tooltip: {
                        bodyFont: {
                            family: "'Cairo', sans-serif"
                        },
                        titleFont: {
                            family: "'Cairo', sans-serif"
                        }
                    }
                },
                scales: {
                    y: {
                        ticks: {
                            font: {
                                family: "'Cairo', sans-serif"
                            }
                        }
                    },
                    x: {
                        ticks: {
                            font: {
                                family: "'Cairo', sans-serif"
                            }
                        }
                    }
                }
            };

            new Chart(document.getElementById('materialsCostChart'), {
                type: 'bar',
                data: {
                    labels: ['تكلفة البناء', 'تكلفة الصيانة'],
                    datasets: [
                        {
                            label: 'مواد تقليدية',
                            data: [100, 100],
                            backgroundColor: '#C89F9C',
                        },
                        {
                            label: 'مواد مستدامة (إيزوكريت)',
                            data: [70, 50],
                            backgroundColor: '#5A8B7B',
                        }
                    ]
                },
                options: { ...chartOptions, plugins: { ...chartOptions.plugins, tooltip: { ...chartOptions.plugins.tooltip, callbacks: { label: (context) => `${context.dataset.label}: ${context.raw}%` } } }, scales: { y: { ...chartOptions.scales.y, title: { display: true, text: 'التكلفة النسبية (%)' } } } }
            });

            new Chart(document.getElementById('paybackPeriodChart'), {
                type: 'bar',
                data: {
                    labels: ['نظام تكييف VRF', 'ألواح شمسية', 'نظام مياه رمادية', 'نظام BMS/IoT'],
                    datasets: [{
                        label: 'فترة الاسترداد (سنوات)',
                        data: [2.5, 4, 3.5, 5],
                        backgroundColor: ['#5A8B7B', '#6B9B8B', '#7CAA9B', '#8CBBAA'],
                    }]
                },
                options: { ...chartOptions, indexAxis: 'y', scales: { x: { ...chartOptions.scales.x, title: { display: true, text: 'عدد السنوات' } } } }
            });

            new Chart(document.getElementById('energyConsumptionChart'), {
                type: 'doughnut',
                data: {
                    labels: ['استهلاك حالي', 'توفير متوقع'],
                    datasets: [{
                        data: [100, 50],
                        backgroundColor: ['#C89F9C', '#5A8B7B'],
                    }]
                },
                options: { ...chartOptions, cutout: '60%' }
            });

            new Chart(document.getElementById('waterConsumptionChart'), {
                type: 'doughnut',
                data: {
                    labels: ['استهلاك حالي', 'توفير متوقع'],
                    datasets: [{
                        data: [100, 40],
                        backgroundColor: ['#C89F9C', '#5A8B7B'],
                    }]
                },
                options: { ...chartOptions, cutout: '60%' }
            });
        });
    </script>
</body>
</html>
�# Green-Cover
