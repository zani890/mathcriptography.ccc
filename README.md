<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Математика и криптография | Проект Марины Жарких</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', 'JetBrains Mono', monospace;
        }

        body {
            background: #0a0f1e;
            color: #e0e7ff;
            line-height: 1.6;
            padding: 20px;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
        }

        /* Header */
        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 20px 0;
            border-bottom: 1px solid #1e293b;
            margin-bottom: 30px;
        }

        .logo {
            font-size: 24px;
            font-weight: bold;
            background: linear-gradient(135deg, #60a5fa, #a78bfa);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            cursor: pointer;
        }

        .nav {
            display: flex;
            gap: 20px;
        }

        .nav-item {
            color: #94a3b8;
            cursor: pointer;
            padding: 8px 16px;
            border-radius: 8px;
            transition: all 0.3s;
        }

        .nav-item:hover, .nav-item.active {
            background: #1e293b;
            color: #60a5fa;
        }

        /* Main Card */
        .cipher-card {
            background: #111827;
            border-radius: 24px;
            padding: 32px;
            border: 1px solid #1e293b;
            box-shadow: 0 20px 40px -15px rgba(0,0,0,0.5);
            margin-bottom: 24px;
        }

        /* Inputs */
        .input-group {
            margin-bottom: 24px;
        }

        label {
            display: block;
            margin-bottom: 8px;
            color: #94a3b8;
            font-size: 14px;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        input, textarea, select {
            width: 100%;
            padding: 14px 18px;
            background: #1e293b;
            border: 1px solid #334155;
            border-radius: 16px;
            color: #f1f5f9;
            font-size: 16px;
            transition: all 0.3s;
            font-family: 'JetBrains Mono', monospace;
        }

        input:focus, textarea:focus, select:focus {
            outline: none;
            border-color: #60a5fa;
            box-shadow: 0 0 0 3px rgba(96, 165, 250, 0.2);
        }

        textarea {
            min-height: 100px;
            resize: vertical;
        }

        /* Range Slider */
        .slider-container {
            display: flex;
            align-items: center;
            gap: 20px;
        }

        input[type="range"] {
            width: 80%;
            padding: 0;
            height: 8px;
            background: #334155;
            border-radius: 4px;
            -webkit-appearance: none;
        }

        input[type="range"]::-webkit-slider-thumb {
            -webkit-appearance: none;
            width: 24px;
            height: 24px;
            background: #60a5fa;
            border-radius: 50%;
            cursor: pointer;
            border: 2px solid #fff;
        }

        .slider-value {
            min-width: 60px;
            text-align: center;
            font-size: 18px;
            font-weight: bold;
            color: #60a5fa;
        }

        /* Button */
        .btn {
            background: linear-gradient(135deg, #3b82f6, #8b5cf6);
            color: white;
            border: none;
            padding: 16px 32px;
            border-radius: 16px;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s;
            width: 100%;
            margin: 20px 0;
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 25px -5px #3b82f6;
        }

        /* Result Box */
        .result-box {
            background: #1e293b;
            border-radius: 16px;
            padding: 20px;
            margin: 20px 0;
            border-left: 4px solid #60a5fa;
        }

        .result-text {
            font-size: 24px;
            word-break: break-all;
            color: #60a5fa;
        }

        /* Math Block */
        .math-block {
            background: #0f172a;
            border-radius: 16px;
            padding: 20px;
            margin-top: 20px;
            border: 1px solid #334155;
        }

        .math-title {
            color: #60a5fa;
            font-size: 18px;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .math-title::before {
            content: "⚡";
            font-size: 24px;
        }

        .math-formula {
            font-size: 20px;
            background: #1e293b;
            padding: 15px;
            border-radius: 12px;
            font-family: 'JetBrains Mono', monospace;
            color: #a78bfa;
        }

        .math-explanation {
            margin-top: 15px;
            color: #94a3b8;
        }

        /* Tabs */
        .tabs {
            display: flex;
            gap: 10px;
            margin-bottom: 30px;
            flex-wrap: wrap;
        }

        .tab {
            padding: 12px 24px;
            background: #1e293b;
            border-radius: 40px;
            cursor: pointer;
            transition: all 0.3s;
            font-weight: 500;
        }

        .tab:hover, .tab.active {
            background: #3b82f6;
            color: white;
        }

        /* Grid for RSA */
        .rsa-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
            margin-top: 20px;
        }

        .key-box {
            background: #1e293b;
            padding: 20px;
            border-radius: 16px;
        }

        .key-label {
            color: #94a3b8;
            font-size: 12px;
            text-transform: uppercase;
        }

        .key-value {
            font-size: 20px;
            color: #60a5fa;
            font-family: 'JetBrains Mono', monospace;
        }

        /* Modal Styles */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.8);
            backdrop-filter: blur(5px);
            z-index: 1000;
            justify-content: center;
            align-items: center;
        }

        .modal.active {
            display: flex;
        }

        .modal-content {
            background: #111827;
            border-radius: 24px;
            padding: 40px;
            max-width: 600px;
            width: 90%;
            max-height: 80vh;
            overflow-y: auto;
            border: 1px solid #3b82f6;
            position: relative;
        }

        .modal-close {
            position: absolute;
            top: 20px;
            right: 20px;
            font-size: 30px;
            color: #94a3b8;
            cursor: pointer;
            transition: color 0.3s;
        }

        .modal-close:hover {
            color: #60a5fa;
        }

        .modal-title {
            font-size: 28px;
            color: #60a5fa;
            margin-bottom: 20px;
        }

        .modal-text {
            color: #cbd5e1;
            line-height: 1.8;
        }

        .modal-text h3 {
            color: #a78bfa;
            margin: 20px 0 10px;
        }

        .modal-text ul {
            margin-left: 20px;
        }

        .footer {
            text-align: center;
            margin-top: 40px;
            padding: 20px;
            color: #4b5563;
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Header -->
        <div class="header">
            <div class="logo" onclick="showMainContent()">🔐 Математика и криптография</div>
            <div class="nav">
                <div class="nav-item" onclick="showMainContent()">Главная</div>
                <div class="nav-item" onclick="showTheory()">Теория</div>
                <div class="nav-item" onclick="showAbout()">О проекте</div>
            </div>
        </div>

        <!-- Main Content (visible by default) -->
        <div id="main-content">
            <!-- Tabs -->
            <div class="tabs" id="tabs">
                <div class="tab active" onclick="switchTab('caesar')">📜 Цезарь</div>
                <div class="tab" onclick="switchTab('vigenere')">🔑 Виженер</div>
                <div class="tab" onclick="switchTab('rsa')">🔬 RSA (демо)</div>
            </div>

            <!-- Caesar Cipher Section -->
            <div id="caesar-section" class="cipher-card">
                <h2 style="margin-bottom: 20px; color: #60a5fa;">Шифр Цезаря</h2>
                <p style="color: #94a3b8; margin-bottom: 30px;">Каждая буква заменяется на букву, стоящую на фиксированное число позиций правее в алфавите.</p>
                
                <div class="input-group">
                    <label>Введите текст (только A-Z, пробелы допускаются)</label>
                    <textarea id="caesar-input" placeholder="Например: HELLO WORLD">HELLO WORLD</textarea>
                </div>

                <div class="input-group">
                    <label>Сдвиг (ключ)</label>
                    <div class="slider-container">
                        <input type="range" id="caesar-shift" min="1" max="25" value="3">
                        <span class="slider-value" id="shift-value">3</span>
                    </div>
                </div>

                <button class="btn" onclick="encryptCaesar()">🔒 Зашифровать</button>

                <div class="result-box">
                    <div style="color: #94a3b8; margin-bottom: 10px;">Результат:</div>
                    <div class="result-text" id="caesar-result">KHOOR ZRUOG</div>
                </div>

                <div class="math-block">
                    <div class="math-title">Математика шифра Цезаря</div>
                    <div class="math-formula">E(x) = (x + k) mod N</div>
                    <div class="math-explanation">
                        где x — номер буквы в алфавите (A=0, B=1, ..., Z=25),<br>
                        k — сдвиг (ключ),<br>
                        N — длина алфавита (26 для латиницы).<br>
                        <span style="color: #60a5fa;">Пример: H (x=7) + 3 = 10 → K</span>
                    </div>
                </div>
            </div>

            <!-- Vigenere Cipher Section (hidden by default) -->
            <div id="vigenere-section" class="cipher-card" style="display: none;">
                <h2 style="margin-bottom: 20px; color: #60a5fa;">Шифр Виженера</h2>
                <p style="color: #94a3b8; margin-bottom: 30px;">Используется ключевое слово. Сдвиг для каждой буквы определяется буквой ключа.</p>
                
                <div class="input-group">
                    <label>Введите текст (A-Z)</label>
                    <textarea id="vigenere-input" placeholder="Например: ATTACKATDAWN">ATTACKATDAWN</textarea>
                </div>

                <div class="input-group">
                    <label>Ключевое слово</label>
                    <input type="text" id="vigenere-key" value="LEMON" placeholder="Введите ключ">
                </div>

                <button class="btn" onclick="encryptVigenere()">🔒 Зашифровать</button>

                <div class="result-box">
                    <div style="color: #94a3b8; margin-bottom: 10px;">Результат:</div>
                    <div class="result-text" id="vigenere-result">LXFOPVEFRNHR</div>
                </div>

                <div class="math-block">
                    <div class="math-title">Математика шифра Виженера</div>
                    <div class="math-formula">E(tᵢ, kᵢ) = (tᵢ + kᵢ) mod N</div>
                    <div class="math-explanation">
                        где tᵢ — номер буквы текста,<br>
                        kᵢ — номер буквы ключа (ключ повторяется циклически),<br>
                        N = 26.<br>
                        <span style="color: #60a5fa;">Пример: A(0) + L(11) = 11 → L</span>
                    </div>
                </div>
            </div>

            <!-- RSA Section (hidden by default) -->
            <div id="rsa-section" class="cipher-card" style="display: none;">
                <h2 style="margin-bottom: 20px; color: #60a5fa;">RSA (демонстрация с числами)</h2>
                <p style="color: #94a3b8; margin-bottom: 30px;">Безопасность RSA основана на сложности факторизации больших чисел.</p>
                
                <div class="rsa-grid">
                    <div class="input-group">
                        <label>Простое число p</label>
                        <input type="number" id="rsa-p" value="17" min="2" max="100">
                    </div>
                    <div class="input-group">
                        <label>Простое число q</label>
                        <input type="number" id="rsa-q" value="19" min="2" max="100">
                    </div>
                </div>

                <button class="btn" onclick="generateRSAKeys()" style="margin: 10px 0;">🔑 Сгенерировать ключи</button>

                <div class="rsa-grid">
                    <div class="key-box">
                        <div class="key-label">Открытый ключ (e, n)</div>
                        <div class="key-value" id="public-key">(5, 323)</div>
                    </div>
                    <div class="key-box">
                        <div class="key-label">Закрытый ключ (d, n)</div>
                        <div class="key-value" id="private-key">(173, 323)</div>
                    </div>
                </div>

                <div class="input-group" style="margin-top: 20px;">
                    <label>Сообщение (число M, должно быть меньше n)</label>
                    <input type="number" id="rsa-message" value="42" min="1">
                </div>

                <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 10px;">
                    <button class="btn" onclick="encryptRSA()" style="margin: 10px 0;">🔒 Зашифровать</button>
                    <button class="btn" onclick="decryptRSA()" style="margin: 10px 0;">🔓 Расшифровать</button>
                </div>

                <div class="result-box">
                    <div style="color: #94a3b8; margin-bottom: 10px;">Результат:</div>
                    <div class="result-text" id="rsa-result">42</div>
                </div>

                <div class="math-block">
                    <div class="math-title">Математика RSA</div>
                    <div class="math-formula">
                        n = p × q<br>
                        φ(n) = (p-1)(q-1)<br>
                        e × d ≡ 1 (mod φ(n))<br>
                        Шифрование: C = Mᵉ mod n<br>
                        Расшифровка: M = Cᵈ mod n
                    </div>
                    <div class="math-explanation" id="rsa-math-desc">
                        p=17, q=19 → n=323, φ(n)=288<br>
                        e=5 (взаимно простое с 288)<br>
                        d=173 (5×173=865 ≡ 1 mod 288)
                    </div>
                </div>
            </div>
        </div>

        <!-- Modal for Theory -->
        <div id="theory-modal" class="modal">
            <div class="modal-content">
                <span class="modal-close" onclick="closeModals()">&times;</span>
                <div class="modal-title">📚 Теория криптографии</div>
                <div class="modal-text">
                    <h3>Что такое криптография?</h3>
                    <p>Криптография — наука о методах обеспечения конфиденциальности, целостности данных и аутентификации.</p>
                    
                    <h3>Математические основы</h3>
                    <p>Современная криптография базируется на нескольких разделах математики:</p>
                    <ul>
                        <li><strong>Теория чисел</strong> — простые числа, функция Эйлера, модульная арифметика</li>
                        <li><strong>Алгебра</strong> — группы, поля, кольца</li>
                        <li><strong>Теория сложности</strong> — однонаправленные функции</li>
                        <li><strong>Теория информации</strong> — энтропия, избыточность</li>
                    </ul>

                    <h3>Шифр Цезаря</h3>
                    <p>E(x) = (x + k) mod N — простейший пример модульной арифметики. Без знания ключа k расшифровка требует перебора всех вариантов.</p>

                    <h3>Шифр Виженера</h3>
                    <p>E(tᵢ, kᵢ) = (tᵢ + kᵢ) mod N — полиалфавитный шифр. Ключ повторяется циклически.</p>

                    <h3>RSA</h3>
                    <p>Основан на сложности факторизации больших чисел. Использует:</p>
                    <ul>
                        <li>φ(n) = (p-1)(q-1) — функция Эйлера</li>
                        <li>e·d ≡ 1 (mod φ(n)) — обратный элемент</li>
                        <li>C = Mᵉ mod n, M = Cᵈ mod n</li>
                    </ul>

                    <h3>Однонаправленные функции</h3>
                    <p>Функции, которые легко вычислить в прямую сторону, но почти невозможно обратить. Например: перемножить два простых числа легко, но разложить произведение на множители — трудно.</p>
                </div>
            </div>
        </div>

        <!-- Modal for About -->
        <div id="about-modal" class="modal">
            <div class="modal-content">
                <span class="modal-close" onclick="closeModals()">&times;</span>
                <div class="modal-title">ℹ️ О проекте</div>
                <div class="modal-text">
                    <h3>Название проекта</h3>
                    <p>«Математика и криптография: от Цезаря до RSA»</p>

                    <h3>Цель проекта</h3>
                    <p>Исследовать эволюцию криптографических методов, изучить роль математики в создании современных криптографических систем, продемонстрировать работу шифров.</p>

                    <h3>Автор</h3>
                    <p>Жарких Марина<br>9Б класс, МБОУ СОШ №14</p>

                    <h3>Руководитель</h3>
                    <p>Хорошева Юлия Владимировна</p>

                    <h3>О приложении</h3>
                    <p>Данное веб-приложение создано в рамках проектной работы и демонстрирует:</p>
                    <ul>
                        <li>Шифр Цезаря — модульная арифметика</li>
                        <li>Шифр Виженера — полиалфавитная замена</li>
                        <li>RSA — теория чисел, простые числа</li>
                    </ul>

                    <h3>Технологии</h3>
                    <p>HTML5, CSS3, JavaScript (чистый код, без фреймворков)</p>

                    <h3>Контакты</h3>
                    <p>📧 marina.zharkih27@internet.ru</p>
                </div>
            </div>
        </div>

        <!-- Footer -->
        <div class="footer">
            Проект "Математика и криптография" | Жарких Марина, 9Б, МБОУ СОШ №14
        </div>
    </div>

    <script>
        // Tab switching
        function switchTab(tab) {
            // Update tabs
            document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
            event.target.classList.add('active');

            // Hide all sections
            document.getElementById('caesar-section').style.display = 'none';
            document.getElementById('vigenere-section').style.display = 'none';
            document.getElementById('rsa-section').style.display = 'none';

            // Show selected section
            if (tab === 'caesar') {
                document.getElementById('caesar-section').style.display = 'block';
            } else if (tab === 'vigenere') {
                document.getElementById('vigenere-section').style.display = 'block';
            } else if (tab === 'rsa') {
                document.getElementById('rsa-section').style.display = 'block';
            }
        }

        // Show main content and hide modals
        function showMainContent() {
            document.getElementById('main-content').style.display = 'block';
            closeModals();
            
            // Update active nav
            document.querySelectorAll('.nav-item').forEach(item => item.classList.remove('active'));
            document.querySelector('.nav-item:first-child').classList.add('active');
        }

        // Show theory modal
        function showTheory() {
            document.getElementById('main-content').style.display = 'none';
            document.getElementById('theory-modal').classList.add('active');
            
            // Update active nav
            document.querySelectorAll('.nav-item').forEach(item => item.classList.remove('active'));
            event.target.classList.add('active');
        }

        // Show about modal
        function showAbout() {
            document.getElementById('main-content').style.display = 'none';
            document.getElementById('about-modal').classList.add('active');
            
            // Update active nav
            document.querySelectorAll('.nav-item').forEach(item => item.classList.remove('active'));
            event.target.classList.add('active');
        }

        // Close all modals
        function closeModals() {
            document.getElementById('theory-modal').classList.remove('active');
            document.getElementById('about-modal').classList.remove('active');
            document.getElementById('main-content').style.display = 'block';
            
            // Reset nav active state to Главная
            document.querySelectorAll('.nav-item').forEach(item => item.classList.remove('active'));
            document.querySelector('.nav-item:first-child').classList.add('active');
        }

        // Close modal when clicking outside
        window.onclick = function(event) {
            if (event.target.classList.contains('modal')) {
                closeModals();
            }
        }

        // Caesar cipher
        document.getElementById('caesar-shift').addEventListener('input', function(e) {
            document.getElementById('shift-value').textContent = e.target.value;
        });

        function encryptCaesar() {
            const text = document.getElementById('caesar-input').value.toUpperCase();
            const shift = parseInt(document.getElementById('caesar-shift').value);
            const alphabet = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
            let result = '';

            for (let char of text) {
                if (alphabet.includes(char)) {
                    let index = alphabet.indexOf(char);
                    let newIndex = (index + shift) % 26;
                    result += alphabet[newIndex];
                } else {
                    result += char; // Keep spaces and punctuation
                }
            }

            document.getElementById('caesar-result').textContent = result;
        }

        // Vigenere cipher
        function encryptVigenere() {
            const text = document.getElementById('vigenere-input').value.toUpperCase().replace(/[^A-Z]/g, '');
            const keyword = document.getElementById('vigenere-key').value.toUpperCase().replace(/[^A-Z]/g, '');
            const alphabet = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
            let result = '';
            let keyIndex = 0;

            for (let i = 0; i < text.length; i++) {
                const textChar = text[i];
                const keyChar = keyword[keyIndex % keyword.length];
                
                const textPos = alphabet.indexOf(textChar);
                const keyPos = alphabet.indexOf(keyChar);
                
                if (textPos !== -1 && keyPos !== -1) {
                    const newPos = (textPos + keyPos) % 26;
                    result += alphabet[newPos];
                    keyIndex++;
                }
            }

            document.getElementById('vigenere-result').textContent = result;
        }

        // RSA Functions
        function isPrime(num) {
            if (num < 2) return false;
            for (let i = 2; i <= Math.sqrt(num); i++) {
                if (num % i === 0) return false;
            }
            return true;
        }

        function gcd(a, b) {
            while (b !== 0) {
                let temp = b;
                b = a % b;
                a = temp;
            }
            return a;
        }

        function modInverse(e, phi) {
            for (let d = 1; d < phi; d++) {
                if ((e * d) % phi === 1) {
                    return d;
                }
            }
            return null;
        }

        function modPow(base, exp, mod) {
            let result = 1;
            base = base % mod;
            while (exp > 0) {
                if (exp % 2 === 1) {
                    result = (result * base) % mod;
                }
                exp = Math.floor(exp / 2);
                base = (base * base) % mod;
            }
            return result;
        }

        let rsaPublicKey = { e: 5, n: 323 };
        let rsaPrivateKey = { d: 173, n: 323 };

        function generateRSAKeys() {
            let p = parseInt(document.getElementById('rsa-p').value);
            let q = parseInt(document.getElementById('rsa-q').value);

            if (!isPrime(p) || !isPrime(q)) {
                alert('Оба числа должны быть простыми!');
                return;
            }

            if (p === q) {
                alert('p и q не должны быть равны!');
                return;
            }

            let n = p * q;
            let phi = (p - 1) * (q - 1);

            // Find e (coprime with phi)
            let e = 2;
            while (e < phi && gcd(e, phi) !== 1) {
                e++;
            }

            let d = modInverse(e, phi);

            if (d === null) {
                alert('Не удалось найти обратный элемент. Попробуйте другие числа.');
                return;
            }

            rsaPublicKey = { e, n };
            rsaPrivateKey = { d, n };

            document.getElementById('public-key').textContent = `(${e}, ${n})`;
            document.getElementById('private-key').textContent = `(${d}, ${n})`;
            
            document.getElementById('rsa-math-desc').innerHTML = 
                `p=${p}, q=${q} → n=${n}, φ(n)=${phi}<br>e=${e}, d=${d} (${e}×${d}=${e*d} ≡ 1 mod ${phi})`;
        }

        function encryptRSA() {
            let m = parseInt(document.getElementById('rsa-message').value);
            let { e, n } = rsaPublicKey;

            if (m >= n) {
                alert('Сообщение должно быть меньше n!');
                return;
            }

            let c = modPow(m, e, n);
            document.getElementById('rsa-result').textContent = c;
        }

        function decryptRSA() {
            let c = parseInt(document.getElementById('rsa-result').textContent);
            let { d, n } = rsaPrivateKey;

            let m = modPow(c, d, n);
            document.getElementById('rsa-result').textContent = m;
        }

        // Initial encryption for demo
        encryptCaesar();
    </script>
</body>
</html>
