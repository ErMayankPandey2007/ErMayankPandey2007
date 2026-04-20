<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>⚡ Mayank Pandey - Hacker Elite Dashboard ⚡</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        html, body {
            width: 100%;
            height: 100%;
            overflow-x: hidden;
        }

        body {
            font-family: 'JetBrains Mono', 'Courier New', monospace;
            background: linear-gradient(135deg, #0a0e27 0%, #1a1f3a 100%);
            color: #00ff00;
            position: relative;
        }

        body::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: repeating-linear-gradient(
                0deg,
                rgba(0, 255, 0, 0.03) 0px,
                rgba(0, 255, 0, 0.03) 1px,
                transparent 1px,
                transparent 2px
            );
            pointer-events: none;
            z-index: 1;
            animation: scanlines 8s linear infinite;
        }

        @keyframes scanlines {
            0% { transform: translateY(0); }
            100% { transform: translateY(10px); }
        }

        .container {
            width: 100%;
            min-height: 100vh;
            padding: 20px;
            position: relative;
            z-index: 0;
        }

        .header {
            display: flex;
            align-items: center;
            gap: 30px;
            margin-bottom: 40px;
            animation: slideIn 1s ease-out;
            padding: 20px;
            background: rgba(26, 31, 58, 0.4);
            border-radius: 12px;
            border: 2px solid #00ff00;
            box-shadow: 0 0 30px rgba(0, 255, 0, 0.3);
        }

        @keyframes slideIn {
            from {
                opacity: 0;
                transform: translateX(-100px);
            }
            to {
                opacity: 1;
                transform: translateX(0);
            }
        }

        .eye-socket {
            width: 120px;
            height: 120px;
            background: #0a0e27;
            border: 4px solid #ff0000;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
            flex-shrink: 0;
            box-shadow: 0 0 30px rgba(255, 0, 0, 0.9), inset 0 0 30px rgba(255, 0, 0, 0.5);
            animation: redGlowIntense 0.6s infinite;
        }

        @keyframes redGlowIntense {
            0%, 100% {
                box-shadow: 0 0 30px rgba(255, 0, 0, 0.9), inset 0 0 30px rgba(255, 0, 0, 0.5);
            }
            50% {
                box-shadow: 0 0 60px rgba(255, 0, 0, 1), inset 0 0 50px rgba(255, 0, 0, 0.8);
            }
        }

        .pupil {
            width: 40px;
            height: 40px;
            background: radial-gradient(circle at 30% 30%, #ff3333, #ff0000);
            border-radius: 50%;
            position: relative;
            animation: eyeBlink 2.5s infinite;
            box-shadow: 0 0 20px #ff0000, inset 0 0 10px rgba(0, 0, 0, 0.5);
        }

        @keyframes eyeBlink {
            0%, 1%, 10%, 11%, 100% {
                height: 40px;
                box-shadow: 0 0 20px #ff0000, inset 0 0 10px rgba(0, 0, 0, 0.5);
            }
            2%, 9% {
                height: 0;
                box-shadow: none;
            }
        }

        .shine {
            width: 12px;
            height: 12px;
            background: #ffff00;
            border-radius: 50%;
            position: absolute;
            top: 6px;
            left: 10px;
            animation: shinePulse 1.2s infinite;
            box-shadow: 0 0 15px #ffff00;
        }

        @keyframes shinePulse {
            0%, 100% {
                opacity: 1;
                transform: scale(1);
            }
            50% {
                opacity: 0.6;
                transform: scale(1.2);
            }
        }

        .header-content {
            flex: 1;
        }

        .title {
            font-size: 42px;
            font-weight: bold;
            color: #00ff00;
            text-shadow: 0 0 15px #00ff00, 0 0 30px rgba(0, 255, 0, 0.6), 0 0 45px rgba(0, 255, 0, 0.3);
            animation: glitchEffect 3s infinite;
            letter-spacing: 3px;
            margin-bottom: 10px;
        }

        @keyframes glitchEffect {
            0%, 100% {
                text-shadow: 0 0 15px #00ff00, 0 0 30px rgba(0, 255, 0, 0.6);
            }
            25% {
                text-shadow: 0 0 10px #00ff00, 0 0 20px rgba(0, 255, 0, 0.3);
            }
            50% {
                text-shadow: 0 0 20px #00ff00, 0 0 40px rgba(0, 255, 0, 0.8);
            }
            75% {
                text-shadow: 0 0 12px #00ff00, 0 0 25px rgba(0, 255, 0, 0.4);
            }
        }

        .status {
            font-size: 13px;
            color: #00ff00;
            margin-bottom: 8px;
            letter-spacing: 1px;
            opacity: 0.9;
        }

        .warning-pulse {
            display: inline-block;
            color: #ff0000;
            animation: warningBlink 0.4s infinite;
            font-weight: bold;
        }

        @keyframes warningBlink {
            0%, 49%, 100% {
                opacity: 1;
            }
            50%, 99% {
                opacity: 0.2;
            }
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }

        .stat-card {
            background: rgba(26, 31, 58, 0.7);
            border: 2px solid #0088ff;
            border-radius: 10px;
            padding: 25px;
            text-align: center;
            animation: statGlow 2.5s infinite;
            cursor: pointer;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .stat-card::before {
            content: '';
            position: absolute;
            top: -100%;
            left: -100%;
            width: 300%;
            height: 300%;
            background: linear-gradient(45deg, transparent, rgba(0, 136, 255, 0.1), transparent);
            animation: shimmer 3s infinite;
        }

        @keyframes shimmer {
            0% {
                transform: translate(-100%, -100%) rotate(45deg);
            }
            100% {
                transform: translate(100%, 100%) rotate(45deg);
            }
        }

        .stat-card:hover {
            border-color: #00ff00;
            box-shadow: 0 0 30px rgba(0, 136, 255, 0.6), inset 0 0 20px rgba(0, 136, 255, 0.2);
            transform: translateY(-5px);
        }

        @keyframes statGlow {
            0%, 100% {
                box-shadow: 0 0 15px rgba(0, 136, 255, 0.4);
            }
            50% {
                box-shadow: 0 0 30px rgba(0, 136, 255, 0.7);
            }
        }

        .stat-number {
            font-size: 36px;
            color: #0088ff;
            font-weight: bold;
            margin-bottom: 10px;
            animation: numberFlash 2s ease-in-out infinite;
            text-shadow: 0 0 10px #0088ff;
        }

        @keyframes numberFlash {
            0%, 100% {
                color: #0088ff;
                text-shadow: 0 0 10px #0088ff;
            }
            50% {
                color: #00ffff;
                text-shadow: 0 0 15px #00ffff;
            }
        }

        .stat-label {
            font-size: 12px;
            color: #00ff00;
            text-transform: uppercase;
            letter-spacing: 2px;
            position: relative;
            z-index: 1;
        }

        .charts-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(500px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }

        .chart-box {
            background: rgba(26, 31, 58, 0.8);
            border: 2px solid #00ff00;
            border-radius: 12px;
            padding: 25px;
            position: relative;
            overflow: hidden;
            animation: boxGlowPulse 3s infinite;
            box-shadow: 0 0 20px rgba(0, 255, 0, 0.3), inset 0 0 15px rgba(0, 255, 0, 0.1);
        }

        @keyframes boxGlowPulse {
            0%, 100% {
                box-shadow: 0 0 20px rgba(0, 255, 0, 0.3), inset 0 0 15px rgba(0, 255, 0, 0.1);
            }
            50% {
                box-shadow: 0 0 40px rgba(0, 255, 0, 0.6), inset 0 0 25px rgba(0, 255, 0, 0.2);
            }
        }

        .chart-box::after {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 2px;
            background: linear-gradient(90deg, transparent, #00ff00, transparent);
            animation: scanBar 2s linear infinite;
        }

        @keyframes scanBar {
            0% {
                top: 0;
            }
            100% {
                top: 100%;
            }
        }

        .chart-title {
            color: #00ff00;
            font-size: 16px;
            margin-bottom: 20px;
            text-transform: uppercase;
            letter-spacing: 3px;
            font-weight: bold;
            text-shadow: 0 0 10px #00ff00;
            position: relative;
            z-index: 2;
        }

        .chart-container {
            position: relative;
            height: 300px;
            z-index: 2;
        }

        .bar-chart {
            display: flex;
            align-items: flex-end;
            gap: 12px;
            height: 100%;
            justify-content: space-around;
        }

        .bar {
            flex: 1;
            background: linear-gradient(180deg, #ff0000 0%, #ff6600 50%, #ffaa00 100%);
            border-radius: 6px 6px 0 0;
            position: relative;
            animation: barGrow 1.5s cubic-bezier(0.34, 1.56, 0.64, 1) forwards;
            box-shadow: 0 0 15px rgba(255, 0, 0, 0.8), inset 0 2px 5px rgba(255, 255, 255, 0.2);
            cursor: pointer;
            transition: all 0.3s;
            border: 1px solid rgba(255, 255, 255, 0.3);
        }

        .bar:hover {
            filter: brightness(1.4);
            box-shadow: 0 0 30px rgba(255, 0, 0, 1), inset 0 2px 10px rgba(255, 255, 255, 0.4);
            transform: scaleY(1.05);
        }

        @keyframes barGrow {
            from {
                height: 0;
                opacity: 0;
            }
            to {
                height: var(--height);
                opacity: 1;
            }
        }

        .bar-label {
            position: absolute;
            bottom: -30px;
            left: 50%;
            transform: translateX(-50%);
            color: #00ff00;
            font-size: 12px;
            white-space: nowrap;
            font-weight: bold;
            text-shadow: 0 0 5px #00ff00;
        }

        .progress-bar {
            width: 100%;
            height: 8px;
            background: rgba(0, 0, 0, 0.5);
            border-radius: 4px;
            margin-top: 20px;
            overflow: hidden;
            border: 1px solid #00ff00;
            position: relative;
            z-index: 2;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #00ff00, #0088ff, #ff00ff, #00ff00);
            border-radius: 4px;
            animation: progressAnimation 3s infinite;
            box-shadow: 0 0 15px rgba(0, 255, 0, 0.8);
        }

        @keyframes progressAnimation {
            0% {
                width: 0%;
                box-shadow: 0 0 15px rgba(0, 255, 0, 0.8);
            }
            50% {
                width: 100%;
                box-shadow: 0 0 25px rgba(0, 255, 0, 1);
            }
            100% {
                width: 0%;
                box-shadow: 0 0 15px rgba(0, 255, 0, 0.8);
            }
        }

        .network-monitor {
            background: rgba(26, 31, 58, 0.9);
            border: 2px solid #ff00ff;
            border-radius: 12px;
            padding: 25px;
            font-size: 12px;
            color: #ff00ff;
            line-height: 2;
            animation: monitorGlow 2s infinite;
            box-shadow: 0 0 25px rgba(255, 0, 255, 0.4), inset 0 0 20px rgba(255, 0, 255, 0.1);
            margin-bottom: 30px;
            position: relative;
            max-height: 350px;
            overflow-y: auto;
        }

        @keyframes monitorGlow {
            0%, 100% {
                box-shadow: 0 0 25px rgba(255, 0, 255, 0.4), inset 0 0 20px rgba(255, 0, 255, 0.1);
            }
            50% {
                box-shadow: 0 0 40px rgba(255, 0, 255, 0.7), inset 0 0 30px rgba(255, 0, 255, 0.2);
            }
        }

        .network-monitor::-webkit-scrollbar {
            width: 10px;
        }

        .network-monitor::-webkit-scrollbar-track {
            background: rgba(0, 0, 0, 0.3);
            border-radius: 5px;
        }

        .network-monitor::-webkit-scrollbar-thumb {
            background: #ff00ff;
            border-radius: 5px;
            box-shadow: 0 0 10px #ff00ff;
        }

        .net-line {
            animation: lineGlitch 0.6s infinite;
            margin: 8px 0;
            font-weight: bold;
            letter-spacing: 1px;
            text-shadow: 0 0 8px #ff00ff;
        }

        @keyframes lineGlitch {
            0%, 100% {
                opacity: 1;
            }
            50% {
                opacity: 0.8;
            }
        }

        .terminal-line {
            display: flex;
            gap: 15px;
            align-items: center;
        }

        .terminal-icon {
            color: #ff00ff;
            font-weight: bold;
            min-width: 12px;
        }

        .success {
            color: #00ff00;
            text-shadow: 0 0 8px #00ff00;
        }

        .warning {
            color: #ffaa00;
            text-shadow: 0 0 8px #ffaa00;
        }

        .error {
            color: #ff0000;
            text-shadow: 0 0 8px #ff0000;
            font-weight: bold;
        }

        .canvas-wrapper {
            position: relative;
            height: 300px;
            z-index: 2;
            margin: 20px 0;
        }

        canvas {
            position: relative;
            z-index: 2;
        }

        .footer {
            text-align: center;
            padding: 30px;
            border-top: 2px solid #00ff00;
            margin-top: 40px;
            background: rgba(26, 31, 58, 0.4);
            border-radius: 12px;
            color: #00ff00;
            font-size: 13px;
            letter-spacing: 2px;
            text-shadow: 0 0 10px #00ff00;
            animation: footerGlow 2s infinite;
        }

        @keyframes footerGlow {
            0%, 100% {
                box-shadow: inset 0 0 20px rgba(0, 255, 0, 0.1);
            }
            50% {
                box-shadow: inset 0 0 30px rgba(0, 255, 0, 0.2);
            }
        }

        @media (max-width: 1200px) {
            .charts-grid {
                grid-template-columns: 1fr;
            }

            .header {
                flex-direction: column;
                align-items: flex-start;
            }

            .title {
                font-size: 32px;
            }
        }

        @media (max-width: 768px) {
            .stats-grid {
                grid-template-columns: repeat(2, 1fr);
            }

            .eye-socket {
                width: 80px;
                height: 80px;
            }

            .title {
                font-size: 24px;
            }

            .container {
                padding: 15px;
            }
        }
    </style>
</head>
<body>

    <div class="container">
        <div class="header">
            <div class="eye-socket">
                <div class="pupil">
                    <div class="shine"></div>
                </div>
            </div>
            <div class="header-content">
                <h1 class="title">⚡ MAYANK HACKER SYSTEM ⚡</h1>
                <div class="status">
                    >>> NEURAL NETWORK ONLINE | STATUS: <span class="warning-pulse">ACTIVE</span> | THREAT LEVEL: <span class="warning-pulse">MAXIMUM</span>
                </div>
                <div class="status">
                    >>> MERN STACK ELITE | CEO MODE: ENABLED | READY FOR COMBAT
                </div>
            </div>
        </div>

        <div class="stats-grid">
            <div class="stat-card">
                <div class="stat-number" id="stat1">0</div>
                <div class="stat-label">Projects Built</div>
            </div>
            <div class="stat-card">
                <div class="stat-number" id="stat2">0</div>
                <div class="stat-label">Code Lines Written</div>
            </div>
            <div class="stat-card">
                <div class="stat-number" id="stat3">0</div>
                <div class="stat-label">System Uptime %</div>
            </div>
            <div class="stat-card">
                <div class="stat-number" id="stat4">0</div>
                <div class="stat-label">Clients Satisfied</div>
            </div>
        </div>

        <div class="charts-grid">
            <div class="chart-box">
                <div class="chart-title">📊 PROJECT ANALYTICS</div>
                <div class="chart-container">
                    <div class="bar-chart">
                        <div class="bar" style="--height: 75%; animation-delay: 0s;">
                            <div class="bar-label">Frontend</div>
                        </div>
                        <div class="bar" style="--height: 85%; animation-delay: 0.1s;">
                            <div class="bar-label">Backend</div>
                        </div>
                        <div class="bar" style="--height: 65%; animation-delay: 0.2s;">
                            <div class="bar-label">Deploy</div>
                        </div>
                        <div class="bar" style="--height: 90%; animation-delay: 0.3s;">
                            <div class="bar-label">Testing</div>
                        </div>
                        <div class="bar" style="--height: 70%; animation-delay: 0.4s;">
                            <div class="bar-label">Docs</div>
                        </div>
                    </div>
                </div>
                <div class="progress-bar">
                    <div class="progress-fill"></div>
                </div>
            </div>

            <div class="chart-box">
                <div class="chart-title">🔥 SKILL INTENSITY MATRIX</div>
                <div class="chart-container">
                    <div class="bar-chart">
                        <div class="bar" style="--height: 95%; animation-delay: 0s; background: linear-gradient(180deg, #ff0000 0%, #00ff00 100%);">
                            <div class="bar-label">React</div>
                        </div>
                        <div class="bar" style="--height: 88%; animation-delay: 0.1s; background: linear-gradient(180deg, #0088ff 0%, #ff00ff 100%);">
                            <div class="bar-label">Node.js</div>
                        </div>
                        <div class="bar" style="--height: 82%; animation-delay: 0.2s; background: linear-gradient(180deg, #00ff00 0%, #ffaa00 100%);">
                            <div class="bar-label">MongoDB</div>
                        </div>
                        <div class="bar" style="--height: 90%; animation-delay: 0.3s; background: linear-gradient(180deg, #ff00ff 0%, #00ffff 100%);">
                            <div class="bar-label">JavaScript</div>
                        </div>
                        <div class="bar" style="--height: 85%; animation-delay: 0.4s; background: linear-gradient(180deg, #ffaa00 0%, #ff0000 100%);">
                            <div class="bar-label">Tailwind</div>
                        </div>
                    </div>
                </div>
                <div class="progress-bar">
                    <div class="progress-fill"></div>
                </div>
            </div>
        </div>

        <div class="charts-grid">
            <div class="chart-box">
                <div class="chart-title">📈 PERFORMANCE GROWTH TRAJECTORY</div>
                <div class="canvas-wrapper">
                    <canvas id="performanceChart" role="img" aria-label="Performance growth over months"></canvas>
                </div>
            </div>

            <div class="chart-box">
                <div class="chart-title">⚙️ SYSTEM RESOURCE LOAD ANALYSIS</div>
                <div class="canvas-wrapper">
                    <canvas id="loadChart" role="img" aria-label="System resource allocation"></canvas>
                </div>
            </div>
        </div>

        <div class="network-monitor">
            <div class="chart-title">🌐 NETWORK INTELLIGENCE MONITOR</div>
            <div class="net-line terminal-line">
                <span class="terminal-icon">→</span>
                <span class="warning-pulse">[INIT]</span>
                <span class="success">System initialized successfully</span>
            </div>
            <div class="net-line terminal-line">
                <span class="terminal-icon">→</span>
                <span class="warning-pulse">[SCAN]</span>
                <span class="success">50+ projects detected in database</span>
            </div>
            <div class="net-line terminal-line">
                <span class="terminal-icon">→</span>
                <span class="warning-pulse">[LOAD]</span>
                <span class="success">Connecting to GitHub API...</span>
            </div>
            <div class="net-line terminal-line">
                <span class="terminal-icon">→</span>
                <span class="warning-pulse">[SYNC]</span>
                <span class="success">Portfolio: mayankpandey.onrender.com</span>
            </div>
            <div class="net-line terminal-line">
                <span class="terminal-icon">→</span>
                <span class="warning-pulse">[VERIFY]</span>
                <span class="success">MERN Stack Certified Developer</span>
            </div>
            <div class="net-line terminal-line">
                <span class="terminal-icon">→</span>
                <span class="warning-pulse">[CHECK]</span>
                <span class="error">⚠️ Enterprise features unlocked</span>
            </div>
            <div class="net-line terminal-line">
                <span class="terminal-icon">→</span>
                <span class="warning-pulse">[STATS]</span>
                <span class="success">4.9/5 Client satisfaction rate</span>
            </div>
            <div class="net-line terminal-line">
                <span class="terminal-icon">→</span>
                <span class="warning-pulse">[UPLOAD]</span>
                <span class="success">Pushing to: github.com/ErMayankPandey2007</span>
            </div>
            <div class="net-line terminal-line">
                <span class="terminal-icon">→</span>
                <span class="warning-pulse">[EMAIL]</span>
                <span class="success">Contact: mp04042007@gmail.com</span>
            </div>
            <div class="net-line terminal-line">
                <span class="terminal-icon">→</span>
                <span class="warning-pulse">[SOCIAL]</span>
                <span class="success">LinkedIn | Instagram | Portfolio</span>
            </div>
            <div class="net-line terminal-line">
                <span class="terminal-icon">→</span>
                <span class="warning-pulse">[READY]</span>
                <span class="success">System fully operational - Ready for deployment</span>
            </div>
        </div>

        <div class="footer">
            ⚡ Built with extreme hacker energy by ErMayankPandey2007 ⚡<br>
            >>> Always Learning | Always Building | Always Evolving<br>
            STATUS: ONLINE ✅ | MODE: PRODUCTION | PERFORMANCE: OPTIMIZED
        </div>
    </div>

    <script>
        function animateCounter(id, target, duration = 2500) {
            const element = document.getElementById(id);
            let current = 0;
            const increment = target / (duration / 16);
            const interval = setInterval(() => {
                current += increment;
                if (current >= target) {
                    element.textContent = target + '+';
                    clearInterval(interval);
                } else {
                    element.textContent = Math.floor(current);
                }
            }, 16);
        }

        setTimeout(() => {
            animateCounter('stat1', 50);
            animateCounter('stat2', 25000);
            animateCounter('stat3', 99);
            animateCounter('stat4', 40);
        }, 800);

        // Performance Chart
        const ctx1 = document.getElementById('performanceChart').getContext('2d');
        new Chart(ctx1, {
            type: 'line',
            data: {
                labels: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug'],
                datasets: [{
                    label: 'Development Progress',
                    data: [30, 45, 60, 75, 85, 92, 98, 100],
                    borderColor: '#00ff00',
                    backgroundColor: 'rgba(0, 255, 0, 0.15)',
                    borderWidth: 4,
                    fill: true,
                    tension: 0.5,
                    pointRadius: 7,
                    pointBackgroundColor: '#ff0000',
                    pointBorderColor: '#ffff00',
                    pointBorderWidth: 3,
                    pointHoverRadius: 10,
                    pointHoverBackgroundColor: '#ffaa00',
                    shadowOffsetX: 2,
                    shadowOffsetY: 2,
                    shadowBlur: 10,
                    shadowColor: 'rgba(0, 255, 0, 0.5)'
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                interaction: {
                    mode: 'index',
                    intersect: false
                },
                plugins: {
                    legend: {
                        display: true,
                        labels: {
                            color: '#00ff00',
                            font: {
                                family: "'JetBrains Mono', monospace",
                                size: 13,
                                weight: 'bold'
                            },
                            padding: 20,
                            boxWidth: 15,
                            boxHeight: 3
                        }
                    },
                    tooltip: {
                        backgroundColor: 'rgba(0, 0, 0, 0.8)',
                        titleColor: '#00ff00',
                        bodyColor: '#0088ff',
                        borderColor: '#00ff00',
                        borderWidth: 2,
                        padding: 12,
                        displayColors: true,
                        callbacks: {
                            title: function(context) {
                                return '📊 ' + context[0].label;
                            }
                        }
                    }
                },
                scales: {
                    y: {
                        beginAtZero: true,
                        max: 110,
                        ticks: {
                            color: '#00ff00',
                            font: {
                                family: "'JetBrains Mono', monospace",
                                weight: 'bold'
                            },
                            callback: function(value) {
                                return value + '%';
                            }
                        },
                        grid: {
                            color: 'rgba(0, 255, 0, 0.15)',
                            lineWidth: 1.5,
                            drawBorder: true,
                            borderColor: 'rgba(0, 255, 0, 0.3)'
                        }
                    },
                    x: {
                        ticks: {
                            color: '#00ff00',
                            font: {
                                family: "'JetBrains Mono', monospace",
                                weight: 'bold'
                            }
                        },
                        grid: {
                            color: 'rgba(0, 255, 0, 0.1)',
                            lineWidth: 1,
                            drawBorder: true,
                            borderColor: 'rgba(0, 255, 0, 0.3)'
                        }
                    }
                }
            }
        });

        // System Load Chart
        const ctx2 = document.getElementById('loadChart').getContext('2d');
        new Chart(ctx2, {
            type: 'doughnut',
            data: {
                labels: ['Frontend Dev', 'Backend Dev', 'DevOps', 'Testing', 'Documentation'],
                datasets: [{
                    data: [30, 35, 15, 12, 8],
                    backgroundColor: [
                        '#ff0000',
                        '#0088ff',
                        '#00ff00',
                        '#ffaa00',
                        '#ff00ff'
                    ],
                    borderColor: [
                        '#ff3333',
                        '#00aaff',
                        '#00ff44',
                        '#ffcc00',
                        '#ff33ff'
                    ],
                    borderWidth: 3,
                    hoverOffset: 15
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    legend: {
                        position: 'bottom',
                        labels: {
                            color: '#00ff00',
                            font: {
                                family: "'JetBrains Mono', monospace",
                                size: 12,
                                weight: 'bold'
                            },
                            padding: 20,
                            boxWidth: 15,
                            boxHeight: 3
                        }
                    },
                    tooltip: {
                        backgroundColor: 'rgba(0, 0, 0, 0.9)',
                        titleColor: '#ff00ff',
                        bodyColor: '#00ff00',
                        borderColor: '#ff00ff',
                        borderWidth: 2,
                        padding: 12,
                        callbacks: {
                            label: function(context) {
                                return context.label + ': ' + context.parsed + '%';
                            }
                        }
                    }
                }
            }
        });
    </script>

</body>
</html>
