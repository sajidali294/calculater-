# calculater-
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Responsive Calculator</title>
  <style>
    body {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      background: #222;
      font-family: sans-serif;
      margin: 0;
      flex-direction: column;
    }

    .calculator {
      background: #333;
      padding: 20px;
      border-radius: 15px;
      box-shadow: 0 0 20px #000;
      width: 300px;
    }

    #display {
      width: 100%;
      height: 50px;
      font-size: 24px;
      text-align: right;
      padding: 10px;
      border-radius: 10px;
      border: none;
      margin-bottom: 15px;
      background: #eee;
    }

    .buttons {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 10px;
    }

    .btn {
      padding: 20px;
      font-size: 18px;
      background: #444;
      color: white;
      border: none;
      border-radius: 10px;
      cursor: pointer;
      transition: background 0.3s;
    }

    .btn:hover {
      background: #666;
    }

    .btn:active {
      background: #888;
    }

    .theme-toggle {
      position: absolute;
      top: 20px;
      right: 20px;
      color: white;
      font-size: 14px;
    }

    /* Light Theme */
    body.light {
      background: #f0f0f0;
    }

    body.light .calculator {
      background: #fff;
      box-shadow: 0 0 15px #bbb;
    }

    body.light #display {
      background: #fff;
      color: #000;
    }

    body.light .btn {
      background: #ddd;
      color: #000;
    }

    body.light .btn:hover {
      background: #ccc;
    }

    /* Responsive Design */
    @media (max-width: 480px) {
      .calculator {
        width: 90%;
        max-width: 400px;
      }

      .buttons {
        grid-template-columns: repeat(4, 1fr);
        gap: 8px;
      }

      .btn {
        padding: 16px;
        font-size: 16px;
      }

      #display {
        font-size: 20px;
        height: 45px;
      }
    }
  </style>
</head>
<body>
  <div class="theme-toggle">
    <label>
      <input type="checkbox" id="toggleTheme" />
      🌞 Light / 🌙 Dark
    </label>
  </div>

  <div class="calculator">
    <input type="text" id="display" disabled />
    <div class="buttons">
      <button class="btn" onclick="clearDisplay()">C</button>
      <button class="btn" onclick="appendValue('(')">(</button>
      <button class="btn" onclick="appendValue(')')">)</button>
      <button class="btn" onclick="appendValue('/')">÷</button>

      <button class="btn" onclick="appendValue('7')">7</button>
      <button class="btn" onclick="appendValue('8')">8</button>
      <button class="btn" onclick="appendValue('9')">9</button>
      <button class="btn" onclick="appendValue('*')">×</button>

      <button class="btn" onclick="appendValue('4')">4</button>
      <button class="btn" onclick="appendValue('5')">5</button>
      <button class="btn" onclick="appendValue('6')">6</button>
      <button class="btn" onclick="appendValue('-')">−</button>

      <button class="btn" onclick="appendValue('1')">1</button>
      <button class="btn" onclick="appendValue('2')">2</button>
      <button class="btn" onclick="appendValue('3')">3</button>
      <button class="btn" onclick="appendValue('+')">+</button>

      <button class="btn" onclick="appendValue('0')">0</button>
      <button class="btn" onclick="appendValue('.')">.</button>
      <button class="btn" onclick="calculate()">=</button>
    </div>
  </div>

  <script>
    let display = document.getElementById("display");

    function appendValue(value) {
      display.value += value;
    }

    function clearDisplay() {
      display.value = '';
    }

    function calculate() {
      try {
        display.value = eval(display.value);
      } catch {
        display.value = "Error";
      }
    }

    // Keyboard Support
    document.addEventListener("keydown", function (event) {
      const key = event.key;
      if (/[0-9+\-*/().]/.test(key)) {
        appendValue(key);
      } else if (key === "Enter") {
        event.preventDefault();
        calculate();
      } else if (key === "Backspace") {
        display.value = display.value.slice(0, -1);
      } else if (key.toLowerCase() === "c") {
        clearDisplay();
      }
    });

    // Theme Toggle
    const themeToggle = document.getElementById("toggleTheme");

    themeToggle.addEventListener("change", function () {
      const isLight = this.checked;
      document.body.classList.toggle("light", isLight);
      localStorage.setItem("theme", isLight ? "light" : "dark");
    });

    // Load saved theme
    window.onload = function () {
      const savedTheme = localStorage.getItem("theme");
      if (savedTheme === "light") {
        document.body.classList.add("light");
        themeToggle.checked = true;
      }
    };
  </script>
</body>
</html>

