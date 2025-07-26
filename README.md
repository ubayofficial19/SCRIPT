<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Generator Script Konten Affiliate</title>
    
    <!-- Pustaka untuk Export PDF -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>

    <style>
        :root {
            --primary-color: #4a90e2;
            --secondary-color: #50e3c2;
            --background-color: #f4f7f6;
            --card-bg-color: #ffffff;
            --text-color: #333;
            --header-color: #2c3e50;
            --border-color: #e0e0e0;
            --shadow: 0 4px 8px rgba(0,0,0,0.1);
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: var(--background-color);
            color: var(--text-color);
            margin: 0;
            padding: 20px;
            line-height: 1.6;
        }

        .container {
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
        }

        header {
            text-align: center;
            margin-bottom: 30px;
        }

        header h1 {
            color: var(--header-color);
            font-size: 2.5em;
            margin-bottom: 10px;
        }

        header p {
            font-size: 1.1em;
            color: #555;
        }

        .card {
            background-color: var(--card-bg-color);
            border-radius: 12px;
            padding: 25px;
            margin-bottom: 25px;
            box-shadow: var(--shadow);
            border: 1px solid var(--border-color);
        }

        .card h2 {
            margin-top: 0;
            color: var(--primary-color);
            border-bottom: 2px solid var(--border-color);
            padding-bottom: 10px;
            margin-bottom: 20px;
        }

        .form-group {
            margin-bottom: 20px;
        }

        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
        }

        .form-group input[type="text"],
        .form-group input[type="url"],
        .form-group input[type="number"],
        .form-group textarea,
        .form-group select {
            width: 100%;
            padding: 12px;
            border: 1px solid var(--border-color);
            border-radius: 8px;
            box-sizing: border-box;
            font-size: 1em;
            transition: border-color 0.3s;
        }

        .form-group input:focus,
        .form-group textarea:focus,
        .form-group select:focus {
            outline: none;
            border-color: var(--primary-color);
        }

        .form-group textarea {
            min-height: 120px;
            resize: vertical;
        }

        .generate-btn {
            display: block;
            width: 100%;
            padding: 15px;
            background: linear-gradient(45deg, var(--primary-color), var(--secondary-color));
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 1.2em;
            font-weight: bold;
            cursor: pointer;
            transition: transform 0.2s, box-shadow 0.2s;
        }

        .generate-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 12px rgba(74, 144, 226, 0.4);
        }

        #output-container {
            margin-top: 30px;
        }

        .result-card {
            background-color: var(--card-bg-color);
            border-radius: 12px;
            padding: 25px;
            margin-bottom: 25px;
            box-shadow: var(--shadow);
            border-left: 5px solid var(--secondary-color);
        }
        
        .result-card h3 {
            margin-top: 0;
            color: var(--header-color);
        }

        .result-content {
            white-space: pre-wrap;
            margin-bottom: 20px;
        }

        .result-actions {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
        }

        .action-btn {
            padding: 8px 15px;
            border: 1px solid var(--primary-color);
            background-color: transparent;
            color: var(--primary-color);
            border-radius: 6px;
            cursor: pointer;
            font-weight: 600;
            transition: background-color 0.3s, color 0.3s;
        }

        .action-btn:hover {
            background-color: var(--primary-color);
            color: white;
        }
        
        .action-btn.copied {
            background-color: var(--secondary-color);
            color: white;
            border-color: var(--secondary-color);
        }

        @media (max-width: 768px) {
            body {
                padding: 10px;
            }
            .container {
                padding: 10px;
            }
            header h1 {
                font-size: 2em;
            }
        }
    </style>
</head>
<body>

    <div class="container">
        <header>
            <h1>Generator Script Konten Affiliate</h1>
            <p>Buat skrip promosi yang menarik untuk produk afiliasi Anda dalam hitungan detik.</p>
        </header>

        <div class="card">
            <h2>1. Masukkan Detail Produk</h2>
            <div class="form-group">
                <label for="product-link">Link Produk (untuk referensi Anda)</label>
                <input type="url" id="product-link" placeholder="https://tokopedia.com/contoh/produk-keren">
            </div>
            <div class="form-group">
                <label for="product-name">Nama Produk</label>
                <input type="text" id="product-name" placeholder="Contoh: Smartwatch X2 Pro">
            </div>
            <div class="form-group">
                <label for="product-features">Fitur / Keunggulan Utama (satu per baris)</label>
                <textarea id="product-features" placeholder="Contoh:&#10;Tahan air hingga 50m&#10;Baterai tahan 14 hari&#10;Layar AMOLED jernih"></textarea>
            </div>
            <div class="form-group">
                <label for="target-audience">Target Audiens</label>
                <input type="text" id="target-audience" placeholder="Contoh: Penggemar olahraga, profesional muda">
            </div>
             <div class="form-group">
                <label for="call-to-action">Call to Action (CTA)</label>
                <input type="text" id="call-to-action" placeholder="Contoh: Cek link di bio!, Beli sekarang juga!">
            </div>
        </div>

        <div class="card">
            <h2>2. Atur Opsi Konten</h2>
            <div class="form-group">
                <label for="style">Style Bahasa</label>
                <select id="style">
                    <option value="enthusiastic">Antusias & Ceria</option>
                    <option value="professional">Profesional & Informatif</option>
                    <option value="casual">Santai & Gaul</option>
                    <option value="storytelling">Storytelling / Bercerita</option>
                </select>
            </div>
            <div class="form-group">
                <label for="length">Panjang Tulisan</label>
                <select id="length">
                    <option value="short">Pendek (1-2 Paragraf)</option>
                    <option value="medium">Sedang (3-4 Paragraf)</option>
                    <option value="long">Panjang (5+ Paragraf)</option>
                </select>
            </div>
            <div class="form-group">
                <label for="count">Jumlah Hasil Generate</label>
                <input type="number" id="count" value="1" min="1" max="5">
            </div>
        </div>

        <button class="generate-btn" id="generate-btn">🚀 Generate Script Sekarang!</button>

        <div id="output-container"></div>
    </div>

    <script>
        document.getElementById('generate-btn').addEventListener('click', generateScripts);

        function generateScripts() {
            // Mengambil semua nilai dari input
            const productName = document.getElementById('product-name').value;
            const featuresText = document.getElementById('product-features').value;
            const audience = document.getElementById('target-audience').value;
            const cta = document.getElementById('call-to-action').value;
            const style = document.getElementById('style').value;
            const length = document.getElementById('length').value;
            const count = parseInt(document.getElementById('count').value);
            
            const outputContainer = document.getElementById('output-container');
            outputContainer.innerHTML = ''; // Bersihkan hasil sebelumnya

            if (!productName || !featuresText || !cta) {
                alert('Harap isi Nama Produk, Fitur, dan Call to Action.');
                return;
            }

            const features = featuresText.split('\n').filter(f => f.trim() !== '');

            for (let i = 0; i < count; i++) {
                const scriptText = createScript(productName, features, audience, cta, style, length);
                createResultCard(scriptText, i);
            }
        }

        function createScript(productName, features, audience, cta, style, length) {
            let script = '';
            const randomFeatures = [...features].sort(() => 0.5 - Math.random());

            // Bagian Pembuka (Hook)
            const hooks = {
                enthusiastic: [
                    `WOW! 🤩 Gak nyangka banget ada produk sekeren ini! Buat kamu para ${audience}, wajib banget punya ${productName}!`,
                    `Siap-siap jatuh cinta sama ${productName}! 😍 Ini dia solusi yang kalian cari selama ini!`,
                    `BREAKING NEWS buat para ${audience}! ${productName} akhirnya hadir untuk mengubah hidup kalian jadi lebih mudah!`,
                ],
                professional: [
                    `Memperkenalkan ${productName}, sebuah inovasi yang dirancang khusus untuk memenuhi kebutuhan ${audience}.`,
                    `Untuk Anda para ${audience}, kami hadirkan solusi efisien dan canggih: ${productName}.`,
                    `Analisis mendalam menunjukkan bahwa ${productName} adalah pilihan optimal untuk meningkatkan produktivitas dan gaya hidup para ${audience}.`,
                ],
                casual: [
                    `Eh, udah pada tau belom soal ${productName}? Sumpah, ini barang oke banget buat lo yang ${audience}.`,
                    `Nih, gue mau spill produk mantep, namanya ${productName}. Cocok parah buat ${audience}.`,
                    `Santai dulu, guys. Coba deh cek ${productName}, barangnya asik banget buat nemenin hari-hari lo.`,
                ],
                storytelling: [
                    `Dulu, aku sering banget kesulitan cari produk yang pas. Tapi semua berubah sejak aku kenal ${productName}. Ini ceritaku...`,
                    `Bayangin deh, kamu bisa lebih produktif dan santai setiap hari. Itulah yang aku rasain setelah pakai ${productName}.`,
                    `Setiap orang punya cerita, dan ${productName} jadi bagian penting dalam ceritaku untuk menjadi lebih baik.`,
                ]
            };
            
            script += getRandomElement(hooks[style]) + '\n\n';

            // Bagian Isi (Fitur)
            const featureIntros = {
                enthusiastic: `Apa aja sih yang bikin produk ini spesial? Banyak banget! Nih beberapa di antaranya:\n`,
                professional: `Produk ini dilengkapi dengan berbagai fitur unggulan untuk menunjang aktivitas Anda, antara lain:\n`,
                casual: `Kerennya tuh di mana? Cekidot fiturnya:\n`,
                storytelling: `Yang paling aku suka dari produk ini adalah detail-detail kecil yang sangat membantu, misalnya:\n`
            };
            script += featureIntros[style];
            randomFeatures.slice(0, 3).forEach(f => {
                script += `✅ ${f}\n`;
            });
            script += '\n';

            // Bagian Tambahan berdasarkan Panjang
            if (length === 'medium' || length === 'long') {
                const mediumContent = {
                    enthusiastic: `Gak cuma itu, desainnya juga stylish banget dan pas buat nemenin OOTD kamu! Pokoknya, paket lengkap deh!`,
                    professional: `Selain fitur teknis, ${productName} juga menawarkan desain ergonomis dan material berkualitas tinggi, memastikan kenyamanan dan daya tahan jangka panjang.`,
                    casual: `Udah gitu, pakenya juga gampang banget, gak ribet. Cocok buat lo yang sat-set-sat-set.`,
                    storytelling: `Awalnya aku ragu, tapi setelah coba sendiri, ternyata ${productName} ini bener-bener 'game-changer'. Setiap fiturnya terasa dipikirkan dengan matang untuk pengguna seperti aku.`
                };
                script += mediumContent[style] + '\n\n';
            }

            if (length === 'long') {
                 const longContent = {
                    enthusiastic: `Aku udah coba sendiri dan hasilnya LUAR BIASA! Aktivitas jadi makin lancar dan seru. Kamu harus rasain sendiri sensasinya! Jangan sampai kehabisan, ya!`,
                    professional: `Investasi pada ${productName} merupakan langkah strategis untuk efisiensi dan peningkatan kualitas kerja maupun personal. Data menunjukkan tingkat kepuasan pengguna yang sangat tinggi.`,
                    casual: `Gue jamin lo gak bakal nyesel sih. Worth it parah sama harganya. Daripada penasaran, mending langsung sikat aja.`,
                    storytelling: `Ini bukan cuma soal produk, tapi soal investasi ke diri sendiri. Aku jadi lebih percaya diri dan terorganisir. Pengalaman yang benar-benar tak ternilai.`
                };
                script += longContent[style] + '\n\n';
            }

            // Bagian Penutup (CTA)
            script += `Tunggu apa lagi? ${cta}\n`;

            // Hashtags
            const productHashtag = productName.replace(/\s+/g, '');
            script += `\n#${productHashtag} #rekomendasiproduk #${audience.split(',')[0].trim().replace(/\s+/g, '')} #affiliate`;

            return script;
        }

        function createResultCard(scriptText, index) {
            const outputContainer = document.getElementById('output-container');
            
            const card = document.createElement('div');
            card.className = 'result-card';
            
            const contentId = `result-content-${index}`;

            card.innerHTML = `
                <h3>Hasil Skrip #${index + 1}</h3>
                <div class="result-content" id="${contentId}">${scriptText}</div>
                <div class="result-actions">
                    <button class="action-btn" onclick="copyToClipboard(this, '${contentId}')">Salin Teks</button>
                    <button class="action-btn" onclick="exportToWord('${contentId}', 'script-affiliate-${index+1}')">Export ke Word</button>
                    <button class="action-btn" onclick="exportToPDF('${contentId}', 'script-affiliate-${index+1}')">Export ke PDF</button>
                </div>
            `;
            outputContainer.appendChild(card);
        }

        function getRandomElement(arr) {
            return arr[Math.floor(Math.random() * arr.length)];
        }

        // --- Fungsi Utilitas (Salin, Word, PDF) ---

        function copyToClipboard(button, elementId) {
            const content = document.getElementById(elementId).innerText;
            navigator.clipboard.writeText(content).then(() => {
                button.textContent = 'Tersalin!';
                button.classList.add('copied');
                setTimeout(() => {
                    button.textContent = 'Salin Teks';
                    button.classList.remove('copied');
                }, 2000);
            }).catch(err => {
                console.error('Gagal menyalin: ', err);
                alert('Gagal menyalin teks.');
            });
        }

        function exportToWord(elementId, filename) {
            const contentElement = document.getElementById(elementId);
            const content = contentElement.innerHTML.replace(/\n/g, '<br>');
            
            const header = "<html xmlns:o='urn:schemas-microsoft-com:office:office' "+
                "xmlns:w='urn:schemas-microsoft-com:office:word' "+
                "xmlns='http://www.w3.org/TR/REC-html40'>"+
                "<head><meta charset='utf-8'><title>Export HTML to Word Document</title></head><body>";
            const footer = "</body></html>";
            const sourceHTML = header + content + footer;

            const source = 'data:application/vnd.ms-word;charset=utf-8,' + encodeURIComponent(sourceHTML);
            const fileDownload = document.createElement("a");
            document.body.appendChild(fileDownload);
            fileDownload.href = source;
            fileDownload.download = filename + '.doc';
            fileDownload.click();
            document.body.removeChild(fileDownload);
        }

        function exportToPDF(elementId, filename) {
            const { jsPDF } = window.jspdf;
            const contentElement = document.getElementById(elementId);
            
            alert('Harap tunggu, PDF sedang dibuat...');

            html2canvas(contentElement, {
                scale: 2, // Meningkatkan resolusi
                useCORS: true,
                logging: false,
                backgroundColor: '#ffffff'
            }).then(canvas => {
                const imgData = canvas.toDataURL('image/png');
                const pdf = new jsPDF('p', 'mm', 'a4');
                
                const pdfWidth = pdf.internal.pageSize.getWidth();
                const pdfHeight = pdf.internal.pageSize.getHeight();
                const canvasWidth = canvas.width;
                const canvasHeight = canvas.height;
                const ratio = canvasWidth / canvasHeight;
                
                let imgWidth = pdfWidth - 20; // dengan margin 10mm di setiap sisi
                let imgHeight = imgWidth / ratio;

                if (imgHeight > pdfHeight - 20) {
                    imgHeight = pdfHeight - 20;
                    imgWidth = imgHeight * ratio;
                }

                const x = (pdfWidth - imgWidth) / 2;
                const y = 10; // margin atas 10mm

                pdf.addImage(imgData, 'PNG', x, y, imgWidth, imgHeight);
                pdf.save(filename + '.pdf');
            }).catch(err => {
                console.error("Gagal membuat PDF: ", err);
                alert("Maaf, terjadi kesalahan saat membuat PDF.");
            });
        }
    </script>

</body>
</html>
