<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Kitchen Command Pro</title>
    <style>
        :root {
            --bg: #000;
            --card: #1a1a1a;
            --accent: #ff9800; /* Chef Orange */
            --text: #ffffff;
            --success: #4caf50;
        }

        body {
            background-color: var(--bg);
            color: var(--text);
            font-family: 'Segoe UI', sans-serif;
            padding: 10px;
            margin: 0;
        }

        h1 { color: var(--accent); text-align: center; text-transform: uppercase; font-size: 1.2rem; margin: 10px 0; }

        .grid {
            display: grid;
            grid-template-columns: 1fr;
            gap: 15px;
        }

        .card {
            background: var(--card);
            border-radius: 12px;
            padding: 15px;
            border: 1px solid #333;
        }

        h2 { font-size: 1rem; margin-bottom: 10px; border-bottom: 1px solid var(--accent); padding-bottom: 5px; color: var(--accent); }

        /* --- Timers --- */
        .timer-row { display: flex; align-items: center; justify-content: space-between; margin-bottom: 15px; }
        .timer-display { font-family: monospace; font-size: 2rem; color: var(--success); }
        .timer-btn { 
            background: var(--accent); border: none; padding: 10px 20px; 
            border-radius: 8px; font-weight: bold; cursor: pointer;
        }

        /* --- Checklist --- */
        .check-item { 
            display: flex; align-items: center; padding: 12px; 
            background: #252525; margin-bottom: 5px; border-radius: 5px;
        }
        .check-item input { transform: scale(1.5); margin-right: 15px; }

        /* --- Converter --- */
        .conv-input { width: 100%; padding: 10px; background: #333; border: none; color: white; border-radius: 5px; margin-bottom: 5px; }
        
        /* --- Temp Table --- */
        table { width: 100%; border-collapse: collapse; font-size: 0.9rem; }
        td { padding: 8px 0; border-bottom: 1px solid #333; }
        .temp { color: var(--accent); font-weight: bold; text-align: right; }

        @media (min-width: 600px) { .grid { grid-template-columns: 1fr 1fr; } }
    </style>
</head>
<body>

    <h1>👨‍🍳 Kitchen Command</h1>

    <div class="grid">
        
        <div class="card">
            <h2>⏱️ Active Timers</h2>
            <div class="timer-row">
                <div class="timer-display" id="t1">05:00</div>
                <button class="timer-btn" onclick="startTimer(300, 't1')">START</button>
            </div>
            <div class="timer-row">
                <div class="timer-display" id="t2">10:00</div>
                <button class="timer-btn" onclick="startTimer(600, 't2')">START</button>
            </div>
        </div>

        <div class="card">
            <h2>📝 Prep Checklist</h2>
            <div class="check-item"><input type="checkbox"> Wash Vegetables</div>
            <div class="check-item"><input type="checkbox"> Sharpen Knives</div>
            <div class="check-item"><input type="checkbox"> Pre-heat Ovens</div>
            <div class="check-item"><input type="checkbox"> Organize Mise en place</div>
        </div>

        <div class="card">
            <h2>⚖️ Conversion (Oz to Grams)</h2>
            <input type="number" class="conv-input" id="ozInput" placeholder="Ounces" oninput="convert(this.value)">
            <p id="gramResult">Result: 0g</p>
        </div>

        <div class="card">
            <h2>🌡️ Temp Guide</h2>
            <table>
                <tr><td>Poultry</td><td class="temp">74°C / 165°F</td></tr>
                <tr><td>Ground Meat</td><td class="temp">71°C / 160°F</td></tr>
                <tr><td>Steak (Med)</td><td class="temp">63°C / 145°F</td></tr>
                <tr><td>Fish</td><td class="temp">63°C / 145°F</td></tr>
            </table>
        </div>

    </div>

    <script>
        // Simple Timer Logic
        function startTimer(duration, displayId) {
            let timer = duration, minutes, seconds;
            const display = document.getElementById(displayId);
            const interval = setInterval(function () {
                minutes = parseInt(timer / 60, 10);
                seconds = parseInt(timer % 60, 10);

                minutes = minutes < 10 ? "0" + minutes : minutes;
                seconds = seconds < 10 ? "0" + seconds : seconds;

                display.textContent = minutes + ":" + seconds;

                if (--timer < 0) {
                    clearInterval(interval);
                    display.style.color = "red";
                    alert("Timer " + displayId + " finished!");
                }
            }, 1000);
        }

        // Conversion Logic
        function convert(oz) {
            const grams = oz * 28.35;
            document.getElementById('gramResult').textContent = "Result: " + grams.toFixed(1) + "g";
        }
    </script>
</body>
</html>
