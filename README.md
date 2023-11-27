# PRODIGY_WD_02
Experience accurate timekeeping with PrecisionTimer, a user-friendly stopwatch web application crafted using the power of HTML, CSS, and JavaScript. Whether you're timing a workout, a cooking session, or any other activity that requires precision, PrecisionTimer has you covere
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Stopwatch</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
        }
        .stopwatch {
            margin: 0 auto;
            padding: 20px;
            background-color: #f1f1f1;
            border-radius: 5px;
        }
        .controls {
            margin-top: 20px;
        }
        button {
            font-size: 18px;
            padding: 10px 20px;
            cursor: pointer;
        }
        #laps {
            margin-top: 30px;
            height: 200px;
            overflow-y: scroll;
        }
    </style>
</head>
<body>
    <div class="stopwatch">
        <span id="timer">00:00</span>
        <div class="controls">
            <button id="startBtn">Start</button>
            <button id="pauseBtn">Pause</button>
            <button id="resetBtn">Reset</button>
            <button id="lapBtn">Lap</button>
        </div>
        <ol id="laps"></ol>
    </div>
    <script>
        let startTime, elapsedTime = 0, interval;
        const timer = document.getElementById('timer'),
            startBtn = document.getElementById('startBtn'),
            pauseBtn = document.getElementById('pauseBtn'),
            resetBtn = document.getElementById('resetBtn'),
            lapBtn = document.getElementById('lapBtn'),
            laps = document.getElementById('laps');

        function start() {
            startTime = Date.now() - elapsedTime;
            interval = setInterval(updateTimer, 10);
            startBtn.disabled = true;
            pauseBtn.disabled = false;
            resetBtn.disabled = false;
            lapBtn.disabled = false;
        }

        function pause() {
            clearInterval(interval);
            elapsedTime = Date.now() - startTime;
            startBtn.disabled = false;
            pauseBtn.disabled = true;
            resetBtn.disabled = false;
            lapBtn.disabled = false;
        }

        function reset() {
            clearInterval(interval);
            elapsedTime = 0;
            timer.textContent = '00:00';
            laps.innerHTML = '';
            startBtn.disabled = false;
            pauseBtn.disabled = true;
            resetBtn.disabled = true;
            lapBtn.disabled = true;
        }

        function lap() {
            const li = document.createElement('li');
            li.textContent = timer.textContent;
            laps.appendChild(li);
        }

        function updateTimer() {
            elapsedTime = Date.now() - startTime;
            const minutes = Math.floor(elapsedTime / 60000);
            const seconds = Math.floor((elapsedTime % 60000) / 1000);
            timer.textContent = `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
        }

        startBtn.addEventListener('click', start);
        pauseBtn.addEventListener('click', pause);
        resetBtn.addEventListener('click', reset);
        lapBtn.addEventListener('click', lap);
    </script>
</body>
</html>
