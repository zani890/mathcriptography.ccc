<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=yes">
    <title>Математика и криптография</title>
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
            line-height: 1.4;
            padding: 8px;
            min-height: 100vh;
        }

        .container {
            max-width: 100%;
            margin: 0 auto;
        }

        /* Header */
        .header {
            display: flex;
            flex-direction: column;
            gap: 10px;
            padding: 10px 0 15px;
            border-bottom: 1px solid #1e293b;
            margin-bottom: 15px;
        }

        .logo {
            font-size: 22px;
            font-weight: bold;
            background: linear-gradient(135deg, #60a5fa, #a78bfa);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            text-align: center;
            line-height: 1.3;
        }

        .nav {
            display: flex;
            justify-content: center;
            gap: 10px;
        }

        .nav-item {
            color: #94a3b8;
            cursor: pointer;
            padding: 8px 16px;
            border-radius: 30px;
            transition: all 0.3s;
            font-size: 14px;
            background: #1e293b;
            flex: 0 1 auto;
            text-align: center;
            min-width: 90px;
            -webkit-tap-highlight-color: transparent;
        }

        .nav-item:active {
            background: #3b82f6;
            color: white;
        }

        /* Tabs */
        .tabs {
            display: flex;
            gap: 5px;
            margin-bottom: 15px;
            flex-wrap: nowrap;
            overflow-x: auto;
            padding-bottom: 5px;
            -webkit-overflow-scrolling: touch;
            scrollbar-width: none;
        }

        .tabs::-webkit-scrollbar {
            display: none;
        }

        .tab {
            padding: 10px 16px;
            background: #1e293b;
            border-radius: 30px;
            cursor: pointer;
            transition: all 0.3s;
            font-weight: 500;
            font-size: 14px;
            flex: 0 0 auto;
            text-align: center;
            white-space: nowrap;
            -webkit-tap-highlight-color: transparent;
        }

        .tab:active {
            background: #3b82f6;
            color: white;
        }

        .tab.active {
            background: #3b82f6;
            color: white;
        }

        /* Main Card */
        .cipher-card {
            background: #111827;
            border-radius: 20px;
            padding: 16px;
            border: 1px solid #1e293b;
            box-shadow: 0 10px 20px -10px rgba(0,0,0,0.5);
            margin-bottom: 15px;
        }

        /* Inputs */
        .input-group {
            margin-bottom: 16px;
        }

        label {
            display: block;
            margin-bottom: 5px;
            color: #94a3b8;
            font-size: 12px;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        input, textarea, select {
            width: 100%;
            padding: 12px 14px;
            background: #1e293b;
            border: 1px solid #334155;
            border-radius: 14px;
            color: #f1f5f9;
            font-size: 15px;
            transition: all 0.3s;
            font-family: 'JetBrains Mono', monospace;
            -webkit-appearance: none;
        }

        textarea {
            min-height: 80px;
            resize: vertical;
        }

        /* Range Slider */
        .slider-container {
            display: flex;
            align-items: center;
            gap: 12px;
        }

        input[type="range"] {
            width: 75%;
            padding: 0;
            height: 6px;
            background: #334155;
            border-radius: 3px;
            -webkit-appearance: none;
        }

        input[type="range"]::-webkit-slider-thumb {
            -webkit-appearance: none;
            width: 22px;
            height: 22px;
            background: #60a5fa;
            border-radius: 50%;
            cursor: pointer;
            border: 2px solid #fff;
        }

        .slider-value {
            min-width: 45px;
            text-align: center;
            font-size: 16px;
            font-weight: bold;
            color: #60a5fa;
        }

        /* Button */
        .btn {
            background: linear-gradient(135deg, #3b82f6, #8b5cf6);
            color: white;
            border: none;
            padding: 12px 16px;
            border-radius: 14px;
            font-size: 15px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s;
            width: 100%;
            margin: 12px 0;
            -webkit-tap-highlight-color: transparent;
        }

        .btn:active {
            transform: scale(0.97);
            opacity: 0.9;
        }

        /* Result Box */
        .result-box {
            background: #1e293b;
            border-radius: 14px;
            padding: 14px;
            margin: 12px 0;
            border-left: 4px solid #60a5fa;
        }

        .result-text {
            font-size: 18px;
            word-break: break-all;
            color: #60a5fa;
            font-family: 'JetBrains Mono', monospace;
        }

        /* Math Block */
        .math-block {
            background: #0f172a;
            border-radius: 14px;
            padding: 14px;
            margin-top: 12px;
            border: 1px solid #334155;
        }

        .math-title {
            color: #60a5fa;
            font-size: 15px;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            gap: 6px;
        }

        .math-title::before {
            content: "⚡";
            font-size: 18px;
        }

        .math-formula {
            font-size: 16px;
            background: #1e293b;
            padding: 10px;
            border-radius: 10px;
            font-family: 'JetBrains Mono', monospace;
            color: #a78bfa;
            overflow-x: auto;
            white-space: pre-line;
        }

        .math-explanation {
            margin-top: 10px;
            color: #94a3b8;
            font-size: 13px;
        }

        /* Grid for RSA */
        .rsa-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
            margin-top: 12px;
        }

        .key-box {
            background: #1e293b;
            padding: 12px;
            border-radius: 14px;
        }

        .key-label {
            color: #94a3b8;
            font-size: 10px;
            text-transform: uppercase;
            margin-bottom: 4px;
        }

        .key-value {
            font-size: 15px;
            color: #60a5fa;
            font-family: 'JetBrains Mono', monospace;
            word-break: break-all;
        }

        /* Modal Styles */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.95);
            backdrop-filter: blur(5px);
            z-index: 1000;
            justify-content: center;
            align-items: center;
            padding: 10px;
        }

        .modal.active {
            display: flex;
        }

        .modal-content {
            background: #111827;
            border-radius: 20px;
            padding: 20px;
            max-width: 100%;
            width: 100%;
            max-height: 80vh;
            overflow-y: auto;
            border: 1px solid #3b82f6;
            position: relative;
        }

        .modal-close {
            position: absolute;
            top: 10px;
            right: 15px;
            font-size: 28px;
            color: #94a3b8;
            cursor: pointer;
            transition: color 0.3s;
            line-height: 1;
            -webkit-tap-highlight-color: transparent;
        }

        .modal-close:active {
            color: #60a5fa;
        }

        .modal-title {
            font-size: 20px;
            color: #60a5fa;
            margin-bottom: 15px;
            padding-right: 25px;
        }

        .modal-text {
            color: #cbd5e1;
            line-height: 1.6;
            font-size: 14px;
        }

        .modal-text h3 {
            color: #a78bfa;
            margin: 15px 0 6px;
            font-size: 16px;
        }

        .modal-text ul {
            margin-left: 18px;
            margin-bottom: 8px;
        }

        .modal-text li {
            margin-bottom: 4px;
        }

        .footer {
            text-align: center;
            margin-top: 20px;
            padding: 12px;
            color: #4b5563;
            font-size: 12px;
            border-top: 1px solid #1e293b;
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Header -->
        <div class="header">
            <div class="logo">🔐 Математика и криптография</div>
            <div class="nav">
                <div class="nav-item" onclick="showTheory()">📚 Теория</div>
                <div class="nav-item" onclick="showAbout()">ℹ️ О проекте</div>
            </div>
        </div>

        <!-- Tabs (горизонтальная прокрутка) -->
        <div class="tabs">
            <div class="tab active" onclick="switchTab('caesar')">📜 Цезарь</div>
            <div class="tab" onclick="switchTab('vigenere')">🔑 Виженер</div>
            <div class="tab" onclick="switchTab('rsa')">🔬 RSA</div>
        </div>

        <!-- Caesar Cipher Section -->
        <div id="caesar-section" class="cipher-card">
            <h2 style="margin-bottom: 12px; color: #60a5fa; font-size: 20px;">📜 Шифр Цезаря</h2>
            <p style="color: #94a3b8; margin-bottom: 16px; font-size: 13px;">
                Каждая буква заменяется на букву, стоящую на фиксированное число позиций правее.
            </p>
            
            <div class="input-group">
                <label>📝 Текст</label>
                <textarea id="caesar-input" placeholder="Например: ПРИВЕТ" oninput="updateCaesar()">ПРИВЕТ</textarea>
            </div>

            <div class="input-group">
                <label>🔢 Сдвиг</label>
                <div class="slider-container">
                    <input type="range" id="caesar-shift" min="1" max="32" value="3" oninput="updateCaesar()">
                    <span class="slider-value" id="shift-value">3</span>
                </div>
            </div>

            <div class="result-box">
                <div style="color: #94a3b8; margin-bottom: 5px; font-size: 12px;">🔒 Результат:</div>
                <div class="result-text" id="caesar-result"></div>
            </div>

            <div class="math-block">
                <div class="math-title">Математика</div>
                <div class="math-formula">
                    E(x) = (x + k) mod 33
                </div>
                <div class="math-explanation">
                    x — номер буквы (А=0...Я=32),<br>
                    k — сдвиг.<br>
                    <span style="color: #60a5fa;">П (16) + 3 = 19 → Т</span>
                </div>
            </div>
        </div>

        <!-- Vigenere Cipher Section (hidden) -->
        <div id="vigenere-section" class="cipher-card" style="display: none;">
            <h2 style="margin-bottom: 12px; color: #60a5fa; font-size: 20px;">🔑 Шифр Виженера</h2>
            <p style="color: #94a3b8; margin-bottom: 16px; font-size: 13px;">
                Сдвиг для каждой буквы определяется ключевым словом.
            </p>
            
            <div class="input-group">
                <label>📝 Текст</label>
                <textarea id="vigenere-input" placeholder="Например: АТАКА" oninput="updateVigenere()">АТАКА</textarea>
            </div>

            <div class="input-group">
                <label>🔑 Ключ</label>
                <input type="text" id="vigenere-key" value="КЛЮЧ" placeholder="Ключевое слово" oninput="updateVigenere()">
            </div>

            <div class="result-box">
                <div style="color: #94a3b8; margin-bottom: 5px; font-size: 12px;">🔒 Результат:</div>
                <div class="result-text" id="vigenere-result"></div>
            </div>

            <div class="math-block">
                <div class="math-title">Математика</div>
                <div class="math-formula">
                    E = (tᵢ + kᵢ) mod 33
                </div>
                <div class="math-explanation">
                    tᵢ — буква текста,<br>
                    kᵢ — буква ключа.<br>
                    <span style="color: #60a5fa;">А(0) + К(11) = 11 → Л</span>
                </div>
            </div>
        </div>

        <!-- RSA Section (hidden) -->
        <div id="rsa-section" class="cipher-card" style="display: none;">
            <h2 style="margin-bottom: 12px; color: #60a5fa; font-size: 20px;">🔬 RSA (демо)</h2>
            <p style="color: #94a3b8; margin-bottom: 16px; font-size: 13px;">
                Основан на сложности разложения на простые множители.
            </p>
            
            <div class="rsa-grid">
                <div class="input-group">
                    <label>p</label>
                    <input type="number" id="rsa-p" value="17" min="2" max="100" onchange="generateRSAKeys()">
                </div>
                <div class="input-group">
                    <label>q</label>
                    <input type="number" id="rsa-q" value="19" min="2" max="100" onchange="generateRSAKeys()">
                </div>
            </div>

            <button class="btn" onclick="generateRSAKeys()" style="margin: 5px 0;">🔑 Сгенерировать ключи</button>

            <div class="rsa-grid">
                <div class="key-box">
                    <div class="key-label">Открытый ключ</div>
                    <div class="key-value" id="public-key">(5, 323)</div>
                </div>
                <div class="key-box">
                    <div class="key-label">Закрытый ключ</div>
                    <div class="key-value" id="private-key">(173, 323)</div>
                </div>
            </div>

            <div class="input-group" style="margin-top: 12px;">
                <label>Сообщение M</label>
                <input type="number" id="rsa-message" value="42" min="1">
            </div>

            <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 6px;">
                <button class="btn" onclick="encryptRSA()" style="margin: 5px 0;">🔒 Шифр</button>
                <button class="btn" onclick="decryptRSA()" style="margin: 5px 0;">🔓 Дешифр</button>
            </div>

            <div class="result-box">
                <div style="color: #94a3b8; margin-bottom: 5px; font-size: 12px;">📨 Результат:</div>
                <div class="result-text" id="rsa-result">42</div>
            </div>

            <div class="math-block">
                <div class="math-title">Математика RSA</div>
                <div class="math-formula" style="font-size: 14px;">
                    n = p×q<br>
                    φ(n) = (p-1)(q-1)<br>
                    e×d ≡ 1 mod φ(n)
                </div>
                <div class="math-explanation" id="rsa-example">
                    17×19=323, φ=288<br>
                    e=5, d=173
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
                    <p>Наука о методах защиты информации от несанкционированного доступа.</p>
                    
                    <h3>Математические основы</h3>
                    <ul>
                        <li><strong>Теория чисел</strong> — простые числа, функция Эйлера</li>
                        <li><strong>Модульная арифметика</strong> — операции по модулю</li>
                        <li><strong>Комбинаторика</strong> — количество ключей</li>
                    </ul>

                    <h3>Шифр Цезаря</h3>
                    <p>E(x) = (x + k) mod N. Простейший сдвиг. Уязвим для частотного анализа.</p>
                    
                    <h3>Шифр Виженера</h3>
                    <p>E(tᵢ, kᵢ) = (tᵢ + kᵢ) mod N. Ключ повторяется. Долго считался невзламываемым.</p>
                    
                    <h3>RSA</h3>
                    <p>Основан на сложности факторизации. Использует пару ключей.</p>
                    
                    <h3>Криптоанализ</h3>
                    <p>Наука о взломе шифров: частотный анализ, полный перебор, математические атаки.</p>
                </div>
            </div>
        </div>

        <!-- Modal for About -->
        <div id="about-modal" class="modal">
            <div class="modal-content">
                <span class="modal-close" onclick="closeModals()">&times;</span>
                <div class="modal-title">ℹ️ О проекте</div>
                <div class="modal-text">
                    <h3>Название</h3>
                    <p>«Математика и криптография»</p>

                    <h3>Цель</h3>
                    <p>Исследовать математические основы криптографии и продемонстрировать работу шифров.</p>

                    <h3>Автор</h3>
                    <p>Жарких Марина, 9Б, МБОУ СОШ №14</p>

                    <h3>Руководитель</h3>
                    <p>Хорошева Юлия Владимировна</p>

                    <h3>Шифры</h3>
                    <ul>
                        <li><strong>Цезарь</strong> — модульная арифметика</li>
                        <li><strong>Виженер</strong> — полиалфавитная замена</li>
                        <li><strong>RSA</strong> — теория чисел</li>
                    </ul>
                    
                    <h3>Контакты</h3>
                    <p>📧 marina.zharkih27@internet.ru</p>
                </div>
            </div>
        </div>

        <!-- Footer -->
        <div class="footer">
            Жарких Марина, 9Б, МБОУ СОШ №14
        </div>
    </div>

    <script>
        // Константы
        const RUSSIAN_ALPHABET = 'АБВГДЕЁЖЗИЙКЛМНОПРСТУФХЦЧШЩЪЫЬЭЮЯ';
        const ALPHABET_SIZE = 33;

        // Инициализация
        function init() {
            updateCaesar();
            updateVigenere();
            generateRSAKeys();
        }

        // Переключение вкладок
        function switchTab(tab) {
            document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
            event.target.classList.add('active');

            document.getElementById('caesar-section').style.display = 'none';
            document.getElementById('vigenere-section').style.display = 'none';
            document.getElementById('rsa-section').style.display = 'none';

            if (tab === 'caesar') {
                document.getElementById('caesar-section').style.display = 'block';
            } else if (tab === 'vigenere') {
                document.getElementById('vigenere-section').style.display = 'block';
            } else if (tab === 'rsa') {
                document.getElementById('rsa-section').style.display = 'block';
            }
        }

        // Caesar cipher
        document.getElementById('caesar-shift').addEventListener('input', function(e) {
            document.getElementById('shift-value').textContent = e.target.value;
        });

        function updateCaesar() {
            const text = document.getElementById('caesar-input').value.toUpperCase();
            const shift = parseInt(document.getElementById('caesar-shift').value);
            let result = '';

            for (let char of text) {
                if (RUSSIAN_ALPHABET.includes(char)) {
                    let index = RUSSIAN_ALPHABET.indexOf(char);
                    let newIndex = (index + shift) % ALPHABET_SIZE;
                    result += RUSSIAN_ALPHABET[newIndex];
                } else {
                    result += char;
                }
            }

            document.getElementById('caesar-result').textContent = result || '(пусто)';
        }

        // Vigenere cipher
        function updateVigenere() {
            const text = document.getElementById('vigenere-input').value.toUpperCase();
            const keyword = document.getElementById('vigenere-key').value.toUpperCase();
            
            if (!keyword) {
                document.getElementById('vigenere-result').textContent = text;
                return;
            }
            
            let result = '';
            let keyIndex = 0;

            for (let i = 0; i < text.length; i++) {
                const char = text[i];
                
                if (RUSSIAN_ALPHABET.includes(char)) {
                    const textPos = RUSSIAN_ALPHABET.indexOf(char);
                    const keyChar = keyword[keyIndex % keyword.length];
                    
                    if (RUSSIAN_ALPHABET.includes(keyChar)) {
                        const keyPos = RUSSIAN_ALPHABET.indexOf(keyChar);
                        const newPos = (textPos + keyPos) % ALPHABET_SIZE;
                        result += RUSSIAN_ALPHABET[newPos];
                        keyIndex++;
                    } else {
                        result += char;
                    }
                } else {
                    result += char;
                }
            }

            document.getElementById('vigenere-result').textContent = result || '(пусто)';
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

            let e = 2;
            while (e < phi && gcd(e, phi) !== 1) {
                e++;
            }

            let d = modInverse(e, phi);

            if (d === null) {
                alert('Не удалось найти обратный элемент.');
                return;
            }

            rsaPublicKey = { e, n };
            rsaPrivateKey = { d, n };

            document.getElementById('public-key').textContent = `(${e}, ${n})`;
            document.getElementById('private-key').textContent = `(${d}, ${n})`;
            
            document.getElementById('rsa-example').innerHTML = 
                `${p}×${q}=${n}, φ=${phi}<br>e=${e}, d=${d}`;
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

        // Показать теорию
        function showTheory() {
            document.getElementById('theory-modal').classList.add('active');
        }

        // Показать информацию о проекте
        function showAbout() {
            document.getElementById('about-modal').classList.add('active');
        }

        // Закрыть модальные окна
        function closeModals() {
            document.getElementById('theory-modal').classList.remove('active');
            document.getElementById('about-modal').classList.remove('active');
        }

        // Закрытие по клику вне окна
        window.onclick = function(event) {
            if (event.target.classList.contains('modal')) {
                closeModals();
            }
        }

        // Инициализация
        window.onload = init;
    </script>
</body>
</html>
