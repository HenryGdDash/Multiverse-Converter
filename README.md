# Multiverse-Converter
A converter for values such as Text, Number, Morse and others.

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Multiverse Converter</title>
    <style>
        /* DEFAULT THEME: LIGHT (White and Black) */
        :root {
            --bg-color: #f8fafc;
            --card-bg: #ffffff;
            --accent-color: #0284c7; 
            --text-main: #0f172a;
            --text-muted: #64748b;
            --border-color: #e2e8f0;
            --input-focus: #0ea5e9;
            --input-bg: #f1f5f9;
            --selection-bg: rgba(2, 132, 199, 0.6); /* Blue theme with 0.6 opacity */
        }

        /* DARK THEME: Automatically activates if the system is in Dark Mode */
        @media (prefers-color-scheme: dark) {
            :root {
                --bg-color: #0f172a;
                --card-bg: #1e293b;
                --accent-color: #38bdf8; 
                --text-main: #f8fafc;
                --text-muted: #94a3b8;
                --border-color: #334155;
                --input-focus: #0284c7;
                --input-bg: #0f172a;
                --selection-bg: rgba(56, 189, 248, 0.6); /* Dark blue with 0.6 opacity */
            }
        }

        /* CUSTOM TEXT SELECTION */
        ::selection {
            background-color: var(--selection-bg);
            color: #ffffff;
        }
        ::-moz-selection {
            background-color: var(--selection-bg);
            color: #ffffff;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
            /* REMOVES THE BLUE TAP OVERLAY ON MOBILE */
            -webkit-tap-highlight-color: transparent; 
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-main);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 40px 20px;
            overflow-x: hidden;
            transition: background-color 0.3s ease, color 0.3s ease;
        }

        .container {
            width: 100%;
            max-width: 1000px;
            animation: fadeIn 0.8s ease-out;
        }

        header {
            text-align: center;
            margin-bottom: 40px;
        }

        header h1 {
            font-size: 2.5rem;
            font-weight: 700;
            letter-spacing: -0.05em;
            margin-bottom: 10px;
            background: linear-gradient(to right, var(--accent-color), #818cf8);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        header p {
            color: var(--text-muted);
            font-size: 1rem;
        }

        .grid-outputs {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 20px;
        }

        .card {
            background: var(--card-bg);
            padding: 20px;
            border-radius: 20px;
            border: 1px solid var(--border-color);
            transition: all 0.3s ease;
            opacity: 0;
            transform: translateY(20px);
            animation: slideUp 0.5s ease-out forwards;
            display: flex;
            flex-direction: column;
            position: relative;
        }

        .card:focus-within {
            border-color: var(--accent-color);
            transform: translateY(-2px);
            box-shadow: 0 10px 25px -5px cubic-bezier(0.1, 0, 0, 1);
        }

        .card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
        }

        .card-label {
            font-size: 0.8rem;
            text-transform: uppercase;
            letter-spacing: 0.05em;
            color: var(--text-muted);
            font-weight: 600;
        }

        .btn-copy {
            background: none;
            border: none;
            color: var(--text-muted);
            cursor: pointer;
            font-size: 0.75rem;
            font-weight: 600;
            padding: 4px 8px;
            border-radius: 6px;
            outline: none;
            transition: all 0.2s ease;
            user-select: none; 
        }

        .btn-copy:hover {
            color: var(--accent-color);
            background: var(--input-bg);
        }

        .btn-copy.copied {
            color: #10b981 !important; 
            animation: pop 0.3s ease-in-out;
        }

        .input-wrapper {
            position: relative;
            display: flex;
            align-items: center;
        }

        .card input {
            width: 100%;
            background: var(--input-bg);
            border: 1px solid var(--border-color);
            border-radius: 12px;
            padding: 12px 16px;
            color: var(--accent-color);
            font-size: 1.15rem;
            font-family: 'Courier New', Courier, monospace;
            outline: none;
            transition: all 0.2s ease;
        }

        .card input:focus {
            border-color: var(--input-focus);
            background: var(--card-bg);
        }

        /* Animations */
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        @keyframes slideUp {
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        @keyframes pop {
            0% { transform: scale(1); }
            50% { transform: scale(1.15); }
            100% { transform: scale(1); }
        }

        /* Staggered delays for card animation */
        .card:nth-child(1) { animation-delay: 0.05s; }
        .card:nth-child(2) { animation-delay: 0.10s; }
        .card:nth-child(3) { animation-delay: 0.15s; }
        .card:nth-child(4) { animation-delay: 0.20s; }
        .card:nth-child(5) { animation-delay: 0.25s; }
        .card:nth-child(6) { animation-delay: 0.30s; }
        .card:nth-child(7) { animation-delay: 0.35s; }
        .card:nth-child(8) { animation-delay: 0.40s; }

        @media (max-width: 600px) {
            header h1 { font-size: 2rem; }
            .grid-outputs { grid-template-columns: 1fr; }
        }
    </style>
</head>
<body>

    <div class="container">
        <header>
            <h1>Multiverse Converter</h1>
            <p>Type in any field and watch the live conversion happen instantly</p>
        </header>

        <div class="grid-outputs">
            <div class="card">
                <div class="card-header">
                    <div class="card-label">Number</div>
                    <button class="btn-copy" onclick="copyValue('input-decimal', this)">Copy</button>
                </div>
                <input type="text" id="input-decimal" placeholder="e.g., 42">
            </div>
            <div class="card">
                <div class="card-header">
                    <div class="card-label">Binary</div>
                    <button class="btn-copy" onclick="copyValue('input-binary', this)">Copy</button>
                </div>
                <input type="text" id="input-binary" placeholder="e.g., 101010">
            </div>
            <div class="card">
                <div class="card-header">
                    <div class="card-label">Hexadecimal</div>
                    <button class="btn-copy" onclick="copyValue('input-hexa', this)">Copy</button>
                </div>
                <input type="text" id="input-hexa" placeholder="e.g., 2A">
            </div>
            <div class="card">
                <div class="card-header">
                    <div class="card-label">Octal</div>
                    <button class="btn-copy" onclick="copyValue('input-octal', this)">Copy</button>
                </div>
                <input type="text" id="input-octal" placeholder="e.g., 52">
            </div>
            <div class="card">
                <div class="card-header">
                    <div class="card-label">Roman Numerals</div>
                    <button class="btn-copy" onclick="copyValue('input-roman', this)">Copy</button>
                </div>
                <input type="text" id="input-roman" placeholder="e.g., XLII">
            </div>
            <div class="card">
                <div class="card-header">
                    <div class="card-label">Egyptian Numerals</div>
                    <button class="btn-copy" onclick="copyValue('input-egyptian', this)">Copy</button>
                </div>
                <input type="text" id="input-egyptian" placeholder="e.g., 𓎆𓎆𓎆𓎆𓏽" readonly>
            </div>
            <div class="card">
                <div class="card-header">
                    <div class="card-label">Text / ASCII</div>
                    <button class="btn-copy" onclick="copyValue('input-text', this)">Copy</button>
                </div>
                <input type="text" id="input-text" placeholder="e.g., A">
            </div>
            <div class="card">
                <div class="card-header">
                    <div class="card-label">Morse Code</div>
                    <button class="btn-copy" onclick="copyValue('input-morse', this)">Copy</button>
                </div>
                <input type="text" id="input-morse" placeholder="e.g., .-">
            </div>
        </div>
    </div>

    <script>
        const morseToChar = {
            '.-': 'A', '-...': 'B', '-.-.': 'C', '-..': 'D', '.': 'E', '..-.': 'F', '--.': 'G', '....': 'H',
            '..': 'I', '.---': 'J', '-.-': 'K', '.-..': 'L', '--': 'M', '-.': 'N', '---': 'O', '.--.': 'P',
            '--.-': 'Q', '.-.': 'R', '...': 'S', '-': 'T', '..-': 'U', '...-': 'V', '.--': 'W', '-..-': 'X',
            '-.--': 'Y', '--..': 'Z', '.----': '1', '..---': '2', '...--': '3', '....-': '4', '.....': '5',
            '-....': '6', '--...': '7', '---..': '8', '----.': '9', '-----': '0', '/': ' '
        };
        const charToMorse = Object.fromEntries(Object.entries(morseToChar).map(([k, v]) => [v, k]));

        function toRoman(num) {
            if (num <= 0 || num > 3999) return '';
            const lookup = {M:1000,CM:900,D:500,CD:400,C:100,XC:90,L:50,XL:40,X:10,IX:9,V:5,IV:4,I:1};
            let roman = '';
            for (let i in lookup) {
                while (num >= lookup[i]) {
                    roman += i;
                    num -= lookup[i];
                }
            }
            return roman;
        }

        function fromRoman(roman) {
            let str = roman.toUpperCase();
            const lookup = {I:1,V:5,X:10,L:50,C:100,D:500,M:1000};
            let num = 0;
            let i = str.length;
            while (i--) {
                if (lookup[str[i]] < lookup[str[i+1]]) {
                    num -= lookup[str[i]];
                } else {
                    num += lookup[str[i]];
                }
            }
            return num;
        }

        function toEgyptian(num) {
            if (num <= 0 || num > 9999) return '';
            const glyphs = [
                {v: 1000, g: '𓆼'},
                {v: 100,  g: '𓍢'},
                {v: 10,   g: '𓎆'},
                {v: 1,    g: '𓏽'}
            ];
            let egyptian = '';
            glyphs.forEach(item => {
                let count = Math.floor(num / item.v);
                num %= item.v;
                egyptian += item.g.repeat(count);
            });
            return egyptian;
        }

        const inputs = {
            decimal: document.getElementById('input-decimal'),
            binary: document.getElementById('input-binary'),
            hexa: document.getElementById('input-hexa'),
            octal: document.getElementById('input-octal'),
            roman: document.getElementById('input-roman'),
            egyptian: document.getElementById('input-egyptian'),
            text: document.getElementById('input-text'),
            morse: document.getElementById('input-morse')
        };

        function toMorse(str) {
            return str.toUpperCase().split('').map(c => charToMorse[c] || '?').join(' ');
        }
        function fromMorse(morse) {
            return morse.trim().split(/\s+/).map(m => morseToChar[m] || '').join('');
        }

        function updateAllFields(decimalValue, textValue, originKey) {
            if (decimalValue !== null && !isNaN(decimalValue)) {
                if (originKey !== 'decimal')  inputs.decimal.value  = decimalValue.toString(10);
                if (originKey !== 'binary')   inputs.binary.value   = decimalValue.toString(2);
                if (originKey !== 'hexa')     inputs.hexa.value     = decimalValue.toString(16).toUpperCase();
                if (originKey !== 'octal')    inputs.octal.value    = decimalValue.toString(8);
                if (originKey !== 'roman')    inputs.roman.value    = toRoman(decimalValue);
                if (originKey !== 'egyptian') inputs.egyptian.value = toEgyptian(decimalValue);
                
                if (originKey !== 'text') {
                    inputs.text.value = (decimalValue >= 32 && decimalValue <= 126) ? String.fromCharCode(decimalValue) : '';
                }
                if (originKey !== 'morse') {
                    let char = String.fromCharCode(decimalValue).toUpperCase();
                    inputs.morse.value = charToMorse[char] || '';
                }
            } 
            else if (textValue !== null) {
                if (originKey !== 'text') inputs.text.value = textValue;
                
                if (textValue.length === 1) {
                    const code = textValue.charCodeAt(0);
                    if (originKey !== 'decimal')  inputs.decimal.value  = code;
                    if (originKey !== 'binary')   inputs.binary.value   = code.toString(2);
                    if (originKey !== 'hexa')     inputs.hexa.value     = code.toString(16).toUpperCase();
                    if (originKey !== 'octal')    inputs.octal.value    = code.toString(8);
                    if (originKey !== 'roman')    inputs.roman.value    = toRoman(code);
                    if (originKey !== 'egyptian') inputs.egyptian.value = toEgyptian(code);
                } else {
                    if (originKey !== 'decimal')  inputs.decimal.value  = '';
                    if (originKey !== 'roman')    inputs.roman.value    = '';
                    if (originKey !== 'egyptian') inputs.egyptian.value = '';
                    if (originKey !== 'binary')   inputs.binary.value   = textValue.split('').map(c => c.charCodeAt(0).toString(2)).join(' ');
                    if (originKey !== 'hexa')     inputs.hexa.value     = textValue.split('').map(c => c.charCodeAt(0).toString(16).toUpperCase()).join(' ');
                    if (originKey !== 'octal')    inputs.octal.value    = textValue.split('').map(c => c.charCodeAt(0).toString(8)).join(' ');
                }
                if (originKey !== 'morse') inputs.morse.value = toMorse(textValue);
            }
        }

        inputs.decimal.addEventListener('input', (e) => {
            const val = e.target.value; if(!val) return clearAll();
            updateAllFields(parseInt(val, 10), null, 'decimal');
        });

        inputs.binary.addEventListener('input', (e) => {
            const val = e.target.value.replace(/[^01 ]/g, ''); e.target.value = val;
            if(!val) return clearAll();
            if (val.includes(' ')) {
                let text = val.split(' ').map(b => b ? String.fromCharCode(parseInt(b, 2)) : '').join('');
                updateAllFields(null, text, 'binary');
            } else {
                updateAllFields(parseInt(val, 2), null, 'binary');
            }
        });

        inputs.hexa.addEventListener('input', (e) => {
            const val = e.target.value.replace(/[^0-9A-Fa-f ]/g, ''); e.target.value = val;
            if(!val) return clearAll();
            updateAllFields(parseInt(val.trim(), 16), null, 'hexa');
        });

        inputs.octal.addEventListener('input', (e) => {
            const val = e.target.value.replace(/[^0-7 ]/g, ''); e.target.value = val;
            if(!val) return clearAll();
            updateAllFields(parseInt(val, 8), null, 'octal');
        });

        inputs.roman.addEventListener('input', (e) => {
            const val = e.target.value.replace(/[^IVXLCDMivxlcdm]/g, ''); e.target.value = val.toUpperCase();
            if(!val) return clearAll();
            updateAllFields(fromRoman(val), null, 'roman');
        });

        inputs.text.addEventListener('input', (e) => {
            const val = e.target.value; if(!val) return clearAll();
            updateAllFields(null, val, 'text');
        });

        inputs.morse.addEventListener('input', (e) => {
            const val = e.target.value; if(!val) return clearAll();
            updateAllFields(null, fromMorse(val), 'morse');
        });

        function clearAll() {
            Object.values(inputs).forEach(input => input.value = '');
        }

        function copyValue(inputId, btn) {
            const inputEl = document.getElementById(inputId);
            if (!inputEl.value) return;

            navigator.clipboard.writeText(inputEl.value).then(() => {
                btn.textContent = "Copied!";
                btn.classList.add('copied');
                
                setTimeout(() => {
                    btn.textContent = "Copy";
                    btn.classList.remove('copied');
                }, 1200);
            }).catch(err => {
                console.error('Error copying text: ', err);
            });
        }
    </script>
</body>
</html>
