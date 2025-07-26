<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Affiliate Content Generator - Script Creator Pro</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/FileSaver.js/2.0.5/FileSaver.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html-docx-js/0.6.1/html-docx.min.js"></script>

    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        primary: '#5D5CDE',
                        'primary-dark': '#4C4BBF',
                        'primary-light': '#7B7AE8',
                        secondary: '#FF6B6B',
                        accent: '#4ECDC4',
                        success: '#51CF66',
                        warning: '#FFD93D',
                        danger: '#FF6B6B'
                    },
                    animation: {
                        'slide-up': 'slideUp 0.3s ease-out',
                        'fade-in': 'fadeIn 0.3s ease-out',
                        'bounce-in': 'bounceIn 0.5s ease-out',
                        'pulse-soft': 'pulseSoft 2s infinite'
                    }
                }
            }
        }

        tailwind.config.theme.extend.keyframes = {
            slideUp: {
                '0%': { transform: 'translateY(20px)', opacity: '0' },
                '100%': { transform: 'translateY(0)', opacity: '1' }
            },
            fadeIn: {
                '0%': { opacity: '0' },
                '100%': { opacity: '1' }
            },
            bounceIn: {
                '0%': { transform: 'scale(0.8)', opacity: '0' },
                '50%': { transform: 'scale(1.05)', opacity: '0.8' },
                '100%': { transform: 'scale(1)', opacity: '1' }
            },
            pulseSoft: {
                '0%, 100%': { opacity: '1' },
                '50%': { opacity: '0.7' }
            }
        }
    </script>
</head>
<body class="bg-gradient-to-br from-gray-50 to-gray-100 dark:from-gray-900 dark:to-gray-800 min-h-screen">
    <!-- Dark mode detection -->
    <script>
        if (window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches) {
            document.documentElement.classList.add('dark');
        }
        window.matchMedia('(prefers-color-scheme: dark)').addEventListener('change', event => {
            if (event.matches) {
                document.documentElement.classList.add('dark');
            } else {
                document.documentElement.classList.remove('dark');
            }
        });
    </script>

    <!-- Header -->
    <header class="bg-gradient-to-r from-primary to-primary-dark text-white shadow-xl">
        <div class="max-w-7xl mx-auto px-4 py-6">
            <div class="flex items-center justify-between">
                <div class="flex items-center space-x-3">
                    <div class="w-12 h-12 bg-white/20 rounded-xl flex items-center justify-center">
                        <span class="text-2xl">🚀</span>
                    </div>
                    <div>
                        <h1 class="text-2xl font-bold">Affiliate Content Generator</h1>
                        <p class="text-primary-light text-sm">Script Creator Pro - Generate konten affiliate berkualitas tinggi</p>
                    </div>
                </div>
                <div class="hidden md:flex items-center space-x-4">
                    <div class="text-right">
                        <div class="text-sm opacity-90">Total Generated</div>
                        <div class="text-xl font-bold" id="total-generated">0</div>
                    </div>
                    <div class="w-px h-8 bg-white/30"></div>
                    <button onclick="toggleDarkMode()" class="p-2 rounded-lg bg-white/10 hover:bg-white/20 transition-all">
                        <span id="theme-icon">🌙</span>
                    </button>
                </div>
            </div>
        </div>
    </header>

    <div class="max-w-7xl mx-auto px-4 py-8">
        <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
            <!-- Input & Settings Panel -->
            <div class="lg:col-span-1">
                <div class="bg-white dark:bg-gray-800 rounded-2xl shadow-xl p-6 sticky top-8">
                    <h2 class="text-xl font-bold text-gray-800 dark:text-white mb-6 flex items-center">
                        <span class="mr-3">⚙️</span>
                        Pengaturan Generator
                    </h2>

                    <form id="content-generator-form" class="space-y-6">
                        <!-- Product Link -->
                        <div>
                            <label class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-2">
                                🔗 Link Produk Affiliate
                            </label>
                            <div class="relative">
                                <input type="url" id="product-link" required 
                                       placeholder="https://shopee.co.id/product/..." 
                                       class="w-full px-4 py-3 text-base border border-gray-300 dark:border-gray-600 rounded-xl bg-white dark:bg-gray-700 text-gray-900 dark:text-white focus:ring-2 focus:ring-primary focus:border-transparent transition-all">
                                <button type="button" onclick="analyzeProduct()" class="absolute right-2 top-2 px-3 py-1 bg-primary text-white rounded-lg text-sm hover:bg-primary-dark transition-all">
                                    Analisa
                                </button>
                            </div>
                            <p class="text-xs text-gray-500 dark:text-gray-400 mt-1">
                                Support: Shopee, Tokopedia, Amazon, dll.
                            </p>
                        </div>

                        <!-- Product Info Display -->
                        <div id="product-info" class="hidden bg-gradient-to-r from-blue-50 to-purple-50 dark:from-blue-900/20 dark:to-purple-900/20 rounded-xl p-4">
                            <h4 class="font-semibold text-gray-800 dark:text-white mb-2">📦 Info Produk</h4>
                            <div id="product-details" class="text-sm text-gray-600 dark:text-gray-400 space-y-1">
                                <!-- Will be populated by analyzeProduct() -->
                            </div>
                        </div>

                        <!-- Content Settings -->
                        <div class="space-y-4">
                            <div>
                                <label class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-2">
                                    📊 Jumlah Konten Generate
                                </label>
                                <select id="content-count" class="w-full px-4 py-3 text-base border border-gray-300 dark:border-gray-600 rounded-xl bg-white dark:bg-gray-700 text-gray-900 dark:text-white focus:ring-2 focus:ring-primary">
                                    <option value="1">1 Konten</option>
                                    <option value="3" selected>3 Konten</option>
                                    <option value="5">5 Konten</option>
                                    <option value="10">10 Konten</option>
                                </select>
                            </div>

                            <div>
                                <label class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-2">
                                    🎨 Style Bahasa
                                </label>
                                <select id="language-style" class="w-full px-4 py-3 text-base border border-gray-300 dark:border-gray-600 rounded-xl bg-white dark:bg-gray-700 text-gray-900 dark:text-white focus:ring-2 focus:ring-primary">
                                    <option value="casual">😊 Casual & Friendly</option>
                                    <option value="professional">💼 Profesional</option>
                                    <option value="persuasive" selected>🎯 Persuasif</option>
                                    <option value="emotional">❤️ Emosional</option>
                                    <option value="trendy">🔥 Trendy & Gaul</option>
                                    <option value="storytelling">📖 Storytelling</option>
                                </select>
                            </div>

                            <div>
                                <label class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-2">
                                    📏 Panjang Tulisan
                                </label>
                                <select id="content-length" class="w-full px-4 py-3 text-base border border-gray-300 dark:border-gray-600 rounded-xl bg-white dark:bg-gray-700 text-gray-900 dark:text-white focus:ring-2 focus:ring-primary">
                                    <option value="short">📝 Pendek (50-100 kata)</option>
                                    <option value="medium" selected>📄 Sedang (100-200 kata)</option>
                                    <option value="long">📃 Panjang (200-300 kata)</option>
                                    <option value="very-long">📚 Sangat Panjang (300+ kata)</option>
                                </select>
                            </div>

                            <div>
                                <label class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-2">
                                    🎭 Tipe Konten
                                </label>
                                <select id="content-type" class="w-full px-4 py-3 text-base border border-gray-300 dark:border-gray-600 rounded-xl bg-white dark:bg-gray-700 text-gray-900 dark:text-white focus:ring-2 focus:ring-primary">
                                    <option value="review" selected>⭐ Review Produk</option>
                                    <option value="unboxing">📦 Unboxing</option>
                                    <option value="comparison">⚖️ Perbandingan</option>
                                    <option value="tutorial">🎓 Tutorial/Tips</option>
                                    <option value="lifestyle">🌟 Lifestyle</option>
                                    <option value="promo">🔥 Promosi/Sale</option>
                                </select>
                            </div>

                            <div>
                                <label class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-2">
                                    🎯 Target Audience
                                </label>
                                <select id="target-audience" class="w-full px-4 py-3 text-base border border-gray-300 dark:border-gray-600 rounded-xl bg-white dark:bg-gray-700 text-gray-900 dark:text-white focus:ring-2 focus:ring-primary">
                                    <option value="general" selected>🌐 Umum</option>
                                    <option value="women">👩 Wanita</option>
                                    <option value="men">👨 Pria</option>
                                    <option value="teens">👧 Remaja</option>
                                    <option value="parents">👨‍👩‍👧‍👦 Orang Tua</option>
                                    <option value="professionals">💼 Profesional</option>
                                </select>
                            </div>
                        </div>

                        <!-- Additional Keywords -->
                        <div>
                            <label class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-2">
                                🏷️ Keyword Tambahan (Opsional)
                            </label>
                            <input type="text" id="additional-keywords" 
                                   placeholder="viral, trending, best seller, dll." 
                                   class="w-full px-4 py-3 text-base border border-gray-300 dark:border-gray-600 rounded-xl bg-white dark:bg-gray-700 text-gray-900 dark:text-white focus:ring-2 focus:ring-primary focus:border-transparent transition-all">
                            <p class="text-xs text-gray-500 dark:text-gray-400 mt-1">
                                Pisahkan dengan koma (,)
                            </p>
                        </div>

                        <!-- Generate Button -->
                        <button type="submit" class="w-full bg-gradient-to-r from-primary to-primary-dark text-white py-4 px-6 rounded-xl hover:from-primary-dark hover:to-primary transform hover:scale-105 transition-all duration-300 font-semibold shadow-lg">
                            <span id="generate-btn-text">🚀 Generate Konten Affiliate</span>
                            <div id="generate-loading" class="hidden flex items-center justify-center">
                                <div class="animate-spin rounded-full h-5 w-5 border-b-2 border-white mr-2"></div>
                                Generating...
                            </div>
                        </button>
                    </form>

                    <!-- Quick Actions -->
                    <div class="mt-6 pt-6 border-t border-gray-200 dark:border-gray-700">
                        <h4 class="text-sm font-semibold text-gray-700 dark:text-gray-300 mb-3">⚡ Quick Actions</h4>
                        <div class="grid grid-cols-2 gap-3">
                            <button onclick="clearAllResults()" class="px-3 py-2 text-sm bg-gray-100 dark:bg-gray-700 text-gray-700 dark:text-gray-300 rounded-lg hover:bg-gray-200 dark:hover:bg-gray-600 transition-all">
                                🗑️ Clear All
                            </button>
                            <button onclick="exportAllToWord()" class="px-3 py-2 text-sm bg-primary text-white rounded-lg hover:bg-primary-dark transition-all">
                                📄 Export Word
                            </button>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Results Panel -->
            <div class="lg:col-span-2">
                <!-- Stats Bar -->
                <div class="bg-white dark:bg-gray-800 rounded-2xl shadow-xl p-6 mb-8">
                    <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
                        <div class="text-center">
                            <div class="text-2xl font-bold text-primary" id="stat-generated">0</div>
                            <div class="text-sm text-gray-600 dark:text-gray-400">Generated</div>
                        </div>
                        <div class="text-center">
                            <div class="text-2xl font-bold text-secondary" id="stat-copied">0</div>
                            <div class="text-sm text-gray-600 dark:text-gray-400">Copied</div>
                        </div>
                        <div class="text-center">
                            <div class="text-2xl font-bold text-accent" id="stat-words">0</div>
                            <div class="text-sm text-gray-600 dark:text-gray-400">Total Words</div>
                        </div>
                        <div class="text-center">
                            <div class="text-2xl font-bold text-success" id="stat-exports">0</div>
                            <div class="text-sm text-gray-600 dark:text-gray-400">Exports</div>
                        </div>
                    </div>
                </div>

                <!-- Results Container -->
                <div id="results-container">
                    <!-- Welcome Screen -->
                    <div id="welcome-screen" class="bg-white dark:bg-gray-800 rounded-2xl shadow-xl p-12 text-center">
                        <div class="w-24 h-24 bg-gradient-to-r from-primary to-secondary rounded-full flex items-center justify-center mx-auto mb-6">
                            <span class="text-4xl">🎯</span>
                        </div>
                        <h3 class="text-2xl font-bold text-gray-800 dark:text-white mb-4">
                            Welcome to Affiliate Content Generator!
                        </h3>
                        <p class="text-gray-600 dark:text-gray-400 mb-8 max-w-md mx-auto">
                            Masukkan link produk affiliate Anda dan atur pengaturan di panel kiri untuk mulai generate konten berkualitas tinggi secara otomatis.
                        </p>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4 max-w-md mx-auto">
                            <div class="bg-primary/10 rounded-xl p-4">
                                <div class="text-2xl mb-2">⚡</div>
                                <div class="text-sm font-semibold text-gray-800 dark:text-white">Fast Generation</div>
                                <div class="text-xs text-gray-600 dark:text-gray-400">Generate multiple content variations quickly</div>
                            </div>
                            <div class="bg-secondary/10 rounded-xl p-4">
                                <div class="text-2xl mb-2">🎨</div>
                                <div class="text-sm font-semibold text-gray-800 dark:text-white">Multiple Styles</div>
                                <div class="text-xs text-gray-600 dark:text-gray-400">Choose from various writing styles</div>
                            </div>
                        </div>
                    </div>

                    <!-- Generated Content Will Appear Here -->
                    <div id="generated-content" class="space-y-6 hidden">
                        <!-- Content cards will be dynamically added here -->
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Custom Confirm Dialog -->
    <div id="confirm-modal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 hidden">
        <div class="bg-white dark:bg-gray-800 rounded-2xl shadow-2xl max-w-md w-full mx-4 p-6">
            <div class="text-center">
                <div class="w-16 h-16 bg-warning/20 rounded-full flex items-center justify-center mx-auto mb-4">
                    <span class="text-2xl">⚠️</span>
                </div>
                <h3 class="text-lg font-semibold text-gray-800 dark:text-white mb-2" id="confirm-title">Konfirmasi</h3>
                <p class="text-gray-600 dark:text-gray-400 mb-6" id="confirm-message">Apakah Anda yakin?</p>
                <div class="flex space-x-3">
                    <button onclick="closeConfirmModal()" class="flex-1 px-4 py-2 text-gray-600 dark:text-gray-400 hover:bg-gray-100 dark:hover:bg-gray-700 rounded-lg transition-all">
                        Batal
                    </button>
                    <button onclick="confirmAction()" class="flex-1 px-4 py-2 bg-primary text-white hover:bg-primary-dark rounded-lg transition-all">
                        Ya, Lanjutkan
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- Success Toast -->
    <div id="success-toast" class="fixed top-4 right-4 bg-success text-white px-6 py-3 rounded-lg shadow-lg transform translate-x-full transition-transform duration-300 z-50">
        <div class="flex items-center">
            <span class="mr-2">✅</span>
            <span id="toast-message">Action completed successfully!</span>
        </div>
    </div>

    <script>
        // Global variables
        let generatedCount = 0;
        let copiedCount = 0;
        let totalWords = 0;
        let exportCount = 0;
        let generatedContents = [];
        let confirmCallback = null;

        // Initialize Poe API handlers
        function initializePoeHandlers() {
            if (typeof window.Poe !== 'undefined') {
                window.Poe.registerHandler('content-generator', (result, context) => {
                    handleContentGeneration(result, context);
                });
            }
        }

        // Product analysis simulation
        function analyzeProduct() {
            const link = document.getElementById('product-link').value;
            if (!link) {
                showToast('Masukkan link produk terlebih dahulu!', 'error');
                return;
            }

            // Show loading state
            const btn = event.target;
            const originalText = btn.textContent;
            btn.textContent = 'Analyzing...';
            btn.disabled = true;

            // Simulate product analysis
            setTimeout(() => {
                const productInfo = extractProductInfo(link);
                displayProductInfo(productInfo);
                btn.textContent = originalText;
                btn.disabled = false;
                showToast('Produk berhasil dianalisa!');
            }, 2000);
        }

        function extractProductInfo(link) {
            // Mock product information extraction
            const domains = {
                'shopee.co.id': { platform: 'Shopee', icon: '🛍️' },
                'tokopedia.com': { platform: 'Tokopedia', icon: '🏪' },
                'amazon.com': { platform: 'Amazon', icon: '📦' },
                'lazada.co.id': { platform: 'Lazada', icon: '🛒' }
            };

            let platform = { platform: 'Unknown', icon: '🔗' };
            for (const [domain, info] of Object.entries(domains)) {
                if (link.includes(domain)) {
                    platform = info;
                    break;
                }
            }

            // Mock extracted data
            return {
                platform: platform.platform,
                icon: platform.icon,
                title: 'Smart Watch Fitness Tracker Premium',
                price: 'Rp 299.000',
                rating: '4.8/5',
                category: 'Electronics',
                brand: 'TechBrand',
                features: ['Heart Rate Monitor', 'Waterproof', 'Long Battery Life']
            };
        }

        function displayProductInfo(info) {
            const container = document.getElementById('product-details');
            container.innerHTML = `
                <div class="flex items-center mb-2">
                    <span class="mr-2">${info.icon}</span>
                    <strong>${info.platform}</strong>
                </div>
                <div><strong>Produk:</strong> ${info.title}</div>
                <div><strong>Harga:</strong> ${info.price}</div>
                <div><strong>Rating:</strong> ⭐ ${info.rating}</div>
                <div><strong>Kategori:</strong> ${info.category}</div>
                <div><strong>Brand:</strong> ${info.brand}</div>
                <div><strong>Fitur:</strong> ${info.features.join(', ')}</div>
            `;
            document.getElementById('product-info').classList.remove('hidden');
        }

        // Content generation
        document.getElementById('content-generator-form').addEventListener('submit', async function(e) {
            e.preventDefault();
            
            const formData = {
                productLink: document.getElementById('product-link').value,
                contentCount: parseInt(document.getElementById('content-count').value),
                languageStyle: document.getElementById('language-style').value,
                contentLength: document.getElementById('content-length').value,
                contentType: document.getElementById('content-type').value,
                targetAudience: document.getElementById('target-audience').value,
                additionalKeywords: document.getElementById('additional-keywords').value
            };

            if (!formData.productLink) {
                showToast('Link produk harus diisi!', 'error');
                return;
            }

            startGenerating();
            
            try {
                await generateContent(formData);
            } catch (error) {
                console.error('Generation error:', error);
                showToast('Terjadi kesalahan saat generate konten!', 'error');
                stopGenerating();
            }
        });

        async function generateContent(formData) {
            // Hide welcome screen and show results
            document.getElementById('welcome-screen').classList.add('hidden');
            document.getElementById('generated-content').classList.remove('hidden');

            // Create prompt for AI
            const prompt = createPrompt(formData);
            
            // Use Poe API if available, otherwise simulate
            if (typeof window.Poe !== 'undefined') {
                try {
                    await window.Poe.sendUserMessage(prompt, {
                        handler: 'content-generator',
                        stream: true,
                        openChat: false,
                        handlerContext: { formData }
                    });
                } catch (error) {
                    console.error('Poe API error:', error);
                    // Fallback to simulation
                    simulateContentGeneration(formData);
                }
            } else {
                // Simulate content generation
                simulateContentGeneration(formData);
            }
        }

        function createPrompt(formData) {
            const styleDescriptions = {
                casual: 'santai dan friendly',
                professional: 'profesional dan formal',
                persuasive: 'persuasif dan meyakinkan',
                emotional: 'emosional dan menyentuh hati',
                trendy: 'trendy dan gaul',
                storytelling: 'bercerita dan engaging'
            };

            const lengthDescriptions = {
                short: '50-100 kata',
                medium: '100-200 kata',
                long: '200-300 kata',
                'very-long': '300+ kata'
            };

            const typeDescriptions = {
                review: 'review produk yang menarik',
                unboxing: 'konten unboxing yang engaging',
                comparison: 'perbandingan produk',
                tutorial: 'tutorial atau tips penggunaan',
                lifestyle: 'konten lifestyle',
                promo: 'konten promosi atau sale'
            };

            return `@Claude-Sonnet-4 Buatkan ${formData.contentCount} variasi konten affiliate untuk produk di link: ${formData.productLink}

Spesifikasi konten:
- Style: ${styleDescriptions[formData.languageStyle]}
- Panjang: ${lengthDescriptions[formData.contentLength]}
- Tipe: ${typeDescriptions[formData.contentType]}
- Target: ${formData.targetAudience}
${formData.additionalKeywords ? `- Keywords: ${formData.additionalKeywords}` : ''}

Buat konten dalam bahasa Indonesia yang menarik untuk affiliate marketing. Setiap konten harus unik dan engaging. Format output dalam JSON seperti ini:

{
  "contents": [
    {
      "title": "Judul menarik",
      "content": "Isi konten lengkap...",
      "hashtags": ["#hashtag1", "#hashtag2"],
      "callToAction": "Call to action yang menarik"
    }
  ]
}

Provide ONLY raw JSON in your response with no explanations, additional text, or code block formatting.`;
        }

        function handleContentGeneration(result, context) {
            if (result.status === 'complete') {
                try {
                    const response = result.responses[0].content;
                    const data = JSON.parse(response);
                    displayGeneratedContent(data.contents, context.formData);
                    stopGenerating();
                } catch (error) {
                    console.error('JSON parse error:', error);
                    // Fallback to simulation
                    simulateContentGeneration(context.formData);
                }
            } else if (result.status === 'error') {
                showToast('Error generating content with AI', 'error');
                simulateContentGeneration(context.formData);
            }
        }

        function simulateContentGeneration(formData) {
            // Simulate API delay
            setTimeout(() => {
                const mockContents = generateMockContent(formData);
                displayGeneratedContent(mockContents, formData);
                stopGenerating();
            }, 3000);
        }

        function generateMockContent(formData) {
            const contents = [];
            
            const templates = {
                review: [
                    {
                        title: "Review Jujur: Produk ini Benar-Benar Worth It!",
                        content: "Guys, aku baru aja cobain produk ini dan honestly, mind = blown! 🤯 Awalnya skeptis juga sih, tapi setelah pakai beberapa hari, beneran recommended banget. Kualitasnya premium tapi harganya masih affordable. Perfect banget buat yang lagi cari produk berkualitas dengan budget pas-pasan. Trust me, you won't regret it!",
                        hashtags: ["#review", "#recommended", "#worthit", "#qualityproduct"],
                        callToAction: "Grab yours now sebelum kehabisan! Link di bio 👆"
                    }
                ],
                unboxing: [
                    {
                        title: "Unboxing: First Impression yang Bikin WOW!",
                        content: "Unboxing time! 📦✨ Packaging-nya udah bikin excited dari awal. Premium banget dan sustainable juga! Isinya? Lebih dari ekspektasi! Detail dan finishing-nya top notch. Dari segi build quality, bener-bener feel expensive meskipun harganya affordable. Ini dia kenapa produk ini jadi bestseller!",
                        hashtags: ["#unboxing", "#firstimpression", "#premium", "#bestseller"],
                        callToAction: "Penasaran? Check link di bio untuk dapetin yang sama! 🔥"
                    }
                ]
            };

            // Generate content based on count
            for (let i = 0; i < formData.contentCount; i++) {
                const template = templates[formData.contentType] || templates.review;
                const content = template[0]; // For simplicity, using first template
                
                contents.push({
                    title: `${content.title} (Variasi ${i + 1})`,
                    content: content.content,
                    hashtags: content.hashtags,
                    callToAction: content.callToAction
                });
            }

            return contents;
        }

        function displayGeneratedContent(contents, formData) {
            const container = document.getElementById('generated-content');
            
            contents.forEach((content, index) => {
                const contentCard = createContentCard(content, index, formData);
                container.appendChild(contentCard);
                
                // Add to global storage
                generatedContents.push(content);
                
                // Animate in
                setTimeout(() => {
                    contentCard.classList.add('animate-slide-up');
                }, index * 200);
            });

            // Update stats
            generatedCount += contents.length;
            totalWords += contents.reduce((sum, content) => sum + content.content.split(' ').length, 0);
            updateStats();
            
            showToast(`${contents.length} konten berhasil di-generate!`);
        }

        function createContentCard(content, index, formData) {
            const card = document.createElement('div');
            card.className = 'bg-white dark:bg-gray-800 rounded-2xl shadow-xl p-6 opacity-0 transform translate-y-4 transition-all duration-500';
            
            const wordCount = content.content.split(' ').length;
            
            card.innerHTML = `
                <div class="flex justify-between items-start mb-4">
                    <div class="flex items-center space-x-3">
                        <div class="w-8 h-8 bg-gradient-to-r from-primary to-secondary rounded-lg flex items-center justify-center text-white font-bold text-sm">
                            ${index + 1}
                        </div>
                        <div>
                            <h3 class="font-semibold text-gray-800 dark:text-white">${content.title}</h3>
                            <div class="flex items-center space-x-4 text-xs text-gray-500 dark:text-gray-400">
                                <span>📊 ${wordCount} kata</span>
                                <span>🎨 ${formData.languageStyle}</span>
                                <span>🎯 ${formData.contentType}</span>
                            </div>
                        </div>
                    </div>
                    <div class="flex space-x-2">
                        <button onclick="copyContent(${generatedContents.length})" class="p-2 bg-primary/10 text-primary rounded-lg hover:bg-primary/20 transition-all" title="Copy Content">
                            📋
                        </button>
                        <button onclick="editContent(${generatedContents.length})" class="p-2 bg-secondary/10 text-secondary rounded-lg hover:bg-secondary/20 transition-all" title="Edit Content">
                            ✏️
                        </button>
                        <button onclick="exportSingleToWord(${generatedContents.length})" class="p-2 bg-accent/10 text-accent rounded-lg hover:bg-accent/20 transition-all" title="Export to Word">
                            📄
                        </button>
                    </div>
                </div>

                <div class="bg-gray-50 dark:bg-gray-700 rounded-xl p-4 mb-4">
                    <div class="text-gray-800 dark:text-white whitespace-pre-wrap" id="content-text-${generatedContents.length}">${content.content}</div>
                </div>

                ${content.hashtags && content.hashtags.length > 0 ? `
                <div class="mb-4">
                    <div class="text-sm text-gray-600 dark:text-gray-400 mb-2">Hashtags:</div>
                    <div class="flex flex-wrap gap-2">
                        ${content.hashtags.map(tag => `<span class="px-2 py-1 bg-primary/10 text-primary rounded-full text-sm">${tag}</span>`).join('')}
                    </div>
                </div>
                ` : ''}

                ${content.callToAction ? `
                <div class="bg-gradient-to-r from-primary/10 to-secondary/10 rounded-xl p-4">
                    <div class="text-sm text-gray-600 dark:text-gray-400 mb-1">Call to Action:</div>
                    <div class="font-medium text-gray-800 dark:text-white">${content.callToAction}</div>
                </div>
                ` : ''}
            `;

            return card;
        }

        function startGenerating() {
            document.getElementById('generate-btn-text').classList.add('hidden');
            document.getElementById('generate-loading').classList.remove('hidden');
            document.querySelector('button[type="submit"]').disabled = true;
        }

        function stopGenerating() {
            document.getElementById('generate-btn-text').classList.remove('hidden');
            document.getElementById('generate-loading').classList.add('hidden');
            document.querySelector('button[type="submit"]').disabled = false;
        }

        // Copy functionality
        function copyContent(index) {
            const content = generatedContents[index];
            if (!content) return;

            const fullText = `${content.title}\n\n${content.content}\n\n${content.hashtags ? content.hashtags.join(' ') : ''}\n\n${content.callToAction || ''}`;
            
            navigator.clipboard.writeText(fullText).then(() => {
                copiedCount++;
                updateStats();
                showToast('Konten berhasil disalin ke clipboard!');
            }).catch(err => {
                console.error('Copy failed:', err);
                showToast('Gagal menyalin konten!', 'error');
            });
        }

        // Edit functionality
        function editContent(index) {
            showToast('Fitur edit akan segera hadir!', 'info');
        }

        // Export functionality
        function exportSingleToWord(index) {
            const content = generatedContents[index];
            if (!content) return;

            const htmlContent = `
                <div style="font-family: Arial, sans-serif; line-height: 1.6; margin: 20px;">
                    <h1 style="color: #5D5CDE; border-bottom: 2px solid #5D5CDE; padding-bottom: 10px;">${content.title}</h1>
                    <div style="margin: 20px 0; padding: 15px; background-color: #f8f9fa; border-left: 4px solid #5D5CDE;">
                        ${content.content.replace(/\n/g, '<br>')}
                    </div>
                    ${content.hashtags ? `
                    <div style="margin: 20px 0;">
                        <strong>Hashtags:</strong><br>
                        ${content.hashtags.join(' ')}
                    </div>
                    ` : ''}
                    ${content.callToAction ? `
                    <div style="margin: 20px 0; padding: 15px; background-color: #e8f4fd; border: 1px solid #5D5CDE; border-radius: 5px;">
                        <strong>Call to Action:</strong><br>
                        ${content.callToAction}
                    </div>
                    ` : ''}
                    <div style="margin-top: 30px; text-align: center; color: #666; font-size: 12px;">
                        Generated by Affiliate Content Generator
                    </div>
                </div>
            `;

            const converted = htmlDocx.asBlob(htmlContent);
            saveAs(converted, `affiliate-content-${index + 1}.docx`);
            
            exportCount++;
            updateStats();
            showToast('Konten berhasil di-export ke Word!');
        }

        function exportAllToWord() {
            if (generatedContents.length === 0) {
                showToast('Belum ada konten yang di-generate!', 'error');
                return;
            }

            let allContent = `
                <div style="font-family: Arial, sans-serif; line-height: 1.6; margin: 20px;">
                    <h1 style="color: #5D5CDE; text-align: center; border-bottom: 3px solid #5D5CDE; padding-bottom: 15px;">
                        Affiliate Content Collection
                    </h1>
                    <div style="text-align: center; margin: 20px 0; color: #666;">
                        Generated: ${new Date().toLocaleDateString('id-ID')}<br>
                        Total Contents: ${generatedContents.length}
                    </div>
            `;

            generatedContents.forEach((content, index) => {
                allContent += `
                    <div style="page-break-before: ${index > 0 ? 'always' : 'auto'}; margin: 30px 0;">
                        <h2 style="color: #5D5CDE; border-bottom: 2px solid #5D5CDE; padding-bottom: 10px;">
                            ${index + 1}. ${content.title}
                        </h2>
                        <div style="margin: 20px 0; padding: 15px; background-color: #f8f9fa; border-left: 4px solid #5D5CDE;">
                            ${content.content.replace(/\n/g, '<br>')}
                        </div>
                        ${content.hashtags ? `
                        <div style="margin: 15px 0;">
                            <strong>Hashtags:</strong><br>
                            <span style="color: #5D5CDE;">${content.hashtags.join(' ')}</span>
                        </div>
                        ` : ''}
                        ${content.callToAction ? `
                        <div style="margin: 15px 0; padding: 15px; background-color: #e8f4fd; border: 1px solid #5D5CDE; border-radius: 5px;">
                            <strong>Call to Action:</strong><br>
                            ${content.callToAction}
                        </div>
                        ` : ''}
                    </div>
                `;
            });

            allContent += `
                    <div style="margin-top: 50px; text-align: center; color: #666; font-size: 12px; border-top: 1px solid #ddd; padding-top: 20px;">
                        Generated by Affiliate Content Generator<br>
                        Total Words: ${totalWords} | Export Date: ${new Date().toLocaleString('id-ID')}
                    </div>
                </div>
            `;

            const converted = htmlDocx.asBlob(allContent);
            saveAs(converted, `affiliate-content-collection-${new Date().toISOString().split('T')[0]}.docx`);
            
            exportCount++;
            updateStats();
            showToast(`${generatedContents.length} konten berhasil di-export ke Word!`);
        }

        // Clear functionality
        function clearAllResults() {
            if (generatedContents.length === 0) {
                showToast('Tidak ada konten untuk dihapus!', 'error');
                return;
            }

            showConfirmDialog(
                'Hapus Semua Konten',
                `Apakah Anda yakin ingin menghapus ${generatedContents.length} konten yang telah di-generate?`,
                () => {
                    document.getElementById('generated-content').innerHTML = '';
                    document.getElementById('generated-content').classList.add('hidden');
                    document.getElementById('welcome-screen').classList.remove('hidden');
                    
                    generatedContents = [];
                    generatedCount = 0;
                    totalWords = 0;
                    updateStats();
                    
                    showToast('Semua konten berhasil dihapus!');
                }
            );
        }

        // Stats update
        function updateStats() {
            document.getElementById('total-generated').textContent = generatedCount;
            document.getElementById('stat-generated').textContent = generatedCount;
            document.getElementById('stat-copied').textContent = copiedCount;
            document.getElementById('stat-words').textContent = totalWords;
            document.getElementById('stat-exports').textContent = exportCount;
        }

        // Utility functions
        function showToast(message, type = 'success') {
            const toast = document.getElementById('success-toast');
            const messageEl = document.getElementById('toast-message');
            
            messageEl.textContent = message;
            
            // Set colors based on type
            if (type === 'error') {
                toast.className = toast.className.replace('bg-success', 'bg-danger');
            } else if (type === 'info') {
                toast.className = toast.className.replace('bg-success bg-danger', 'bg-primary');
            } else {
                toast.className = toast.className.replace('bg-danger bg-primary', 'bg-success');
            }
            
            // Show toast
            toast.classList.remove('translate-x-full');
            
            // Hide after 3 seconds
            setTimeout(() => {
                toast.classList.add('translate-x-full');
            }, 3000);
        }

        function showConfirmDialog(title, message, callback) {
            document.getElementById('confirm-title').textContent = title;
            document.getElementById('confirm-message').textContent = message;
            confirmCallback = callback;
            document.getElementById('confirm-modal').classList.remove('hidden');
        }

        function closeConfirmModal() {
            document.getElementById('confirm-modal').classList.add('hidden');
            confirmCallback = null;
        }

        function confirmAction() {
            if (confirmCallback) {
                confirmCallback();
            }
            closeConfirmModal();
        }

        function toggleDarkMode() {
            document.documentElement.classList.toggle('dark');
            const icon = document.getElementById('theme-icon');
            icon.textContent = document.documentElement.classList.contains('dark') ? '☀️' : '🌙';
        }

        // Initialize
        document.addEventListener('DOMContentLoaded', function() {
            initializePoeHandlers();
            updateStats();
            
            // Set theme icon based on current mode
            const icon = document.getElementById('theme-icon');
            icon.textContent = document.documentElement.classList.contains('dark') ? '☀️' : '🌙';
        });
    </script>
</body>
</html>
