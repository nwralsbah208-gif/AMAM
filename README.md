<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🎮 CYBER PIXEL Ω - لعبة LEX-Ω البكسليه</title>
    <style>
        /* ========== SYSTEM Ω ========== */
        :root {
            --omega-blue: #00F0FF;
            --omega-red: #FF0040;
            --omega-green: #00FF88;
            --omega-yellow: #FFDD00;
            --omega-purple: #AA00FF;
            --omega-dark: #000814;
            --omega-matrix: #00FF41;
            --omega-grid: #00FF4120;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            image-rendering: pixelated;
            image-rendering: -moz-crisp-edges;
            image-rendering: crisp-edges;
        }

        body {
            background: var(--omega-dark);
            font-family: 'Courier New', monospace;
            color: var(--omega-blue);
            overflow: hidden;
            height: 100vh;
        }

        .omega-grid {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-image: 
                linear-gradient(var(--omega-grid) 1px, transparent 1px),
                linear-gradient(90deg, var(--omega-grid) 1px, transparent 1px);
            background-size: 32px 32px;
            z-index: -1;
            animation: gridMove 20s linear infinite;
        }

        @keyframes gridMove {
            0% { transform: translate(0, 0); }
            100% { transform: translate(32px, 32px); }
        }

        .terminal-container {
            width: 100%;
            height: 100vh;
            position: relative;
            overflow: hidden;
        }

        /* ========== MAIN GAME CONTAINER ========== */
        #gameContainer {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: #000;
        }

        canvas {
            display: block;
            background: #000;
            cursor: crosshair;
        }

        /* ========== HUD Ω ========== */
        .hud-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            padding: 15px;
            display: flex;
            justify-content: space-between;
            z-index: 100;
            background: linear-gradient(to bottom, #000000CC, transparent);
            backdrop-filter: blur(5px);
            border-bottom: 2px solid var(--omega-blue);
        }

        .hud-section {
            display: flex;
            gap: 25px;
        }

        .hud-item {
            text-shadow: 0 0 10px currentColor;
        }

        .hud-label {
            font-size: 12px;
            color: var(--omega-green);
            margin-bottom: 4px;
        }

        .hud-value {
            font-size: 20px;
            font-weight: bold;
            color: var(--omega-blue);
            font-family: 'Courier New', monospace;
        }

        /* ========== HEALTH BAR Ω ========== */
        .health-container {
            position: fixed;
            bottom: 30px;
            left: 50%;
            transform: translateX(-50%);
            width: 400px;
            background: #00000088;
            border: 3px solid var(--omega-red);
            border-radius: 20px;
            padding: 8px;
            z-index: 100;
        }

        .health-bar {
            width: 100%;
            height: 25px;
            background: #330000;
            border-radius: 15px;
            overflow: hidden;
            position: relative;
        }

        .health-fill {
            height: 100%;
            background: linear-gradient(90deg, #FF0040, #FF3366);
            border-radius: 15px;
            transition: width 0.3s;
            position: relative;
            overflow: hidden;
        }

        .health-fill::after {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, #FFFFFF44, transparent);
            animation: healthShine 2s infinite;
        }

        @keyframes healthShine {
            0% { transform: translateX(-100%); }
            100% { transform: translateX(100%); }
        }

        /* ========== ABILITIES Ω ========== */
        .abilities-container {
            position: fixed;
            bottom: 100px;
            left: 30px;
            display: flex;
            gap: 15px;
            z-index: 100;
        }

        .ability-btn {
            width: 60px;
            height: 60px;
            background: #000000CC;
            border: 3px solid var(--omega-purple);
            border-radius: 15px;
            color: white;
            font-size: 24px;
            cursor: pointer;
            transition: all 0.2s;
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
            overflow: hidden;
        }

        .ability-btn:hover {
            transform: scale(1.1);
            border-color: var(--omega-yellow);
            box-shadow: 0 0 20px var(--omega-yellow);
        }

        .ability-btn:active {
            transform: scale(0.95);
        }

        .ability-cooldown {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: #000000AA;
            display: none;
            align-items: center;
            justify-content: center;
            font-size: 20px;
            font-weight: bold;
            color: var(--omega-blue);
        }

        /* ========== MINIMAP Ω ========== */
        .minimap-container {
            position: fixed;
            top: 100px;
            right: 30px;
            width: 200px;
            height: 200px;
            background: #00000088;
            border: 3px solid var(--omega-green);
            border-radius: 10px;
            padding: 10px;
            z-index: 100;
            backdrop-filter: blur(5px);
        }

        .minimap {
            width: 100%;
            height: 100%;
            background: #001122;
            position: relative;
            overflow: hidden;
            border-radius: 5px;
        }

        .minimap-player {
            position: absolute;
            width: 8px;
            height: 8px;
            background: var(--omega-blue);
            border-radius: 50%;
            transform: translate(-50%, -50%);
            box-shadow: 0 0 10px var(--omega-blue);
        }

        /* ========== LOADING SCREEN Ω ========== */
        .loading-screen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: #000;
            z-index: 1000;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }

        .omega-loader {
            width: 300px;
            height: 10px;
            background: #001122;
            border: 2px solid var(--omega-blue);
            border-radius: 5px;
            margin: 30px 0;
            overflow: hidden;
        }

        .omega-loader-fill {
            height: 100%;
            background: linear-gradient(90deg, var(--omega-blue), var(--omega-green));
            width: 0%;
            transition: width 0.5s;
        }

        .loading-text {
            font-size: 20px;
            color: var(--omega-blue);
            margin-bottom: 20px;
            text-align: center;
        }

        /* ========== MISSION LOG Ω ========== */
        .mission-log {
            position: fixed;
            top: 100px;
            left: 30px;
            width: 300px;
            background: #000000CC;
            border: 3px solid var(--omega-yellow);
            border-radius: 10px;
            padding: 15px;
            z-index: 100;
            backdrop-filter: blur(5px);
            max-height: 400px;
            overflow-y: auto;
        }

        .mission-title {
            color: var(--omega-yellow);
            font-size: 16px;
            margin-bottom: 10px;
            border-bottom: 2px solid var(--omega-yellow);
            padding-bottom: 5px;
        }

        .mission-item {
            padding: 8px;
            margin: 5px 0;
            background: #001122;
            border-left: 3px solid var(--omega-green);
            border-radius: 5px;
            font-size: 14px;
        }

        /* ========== DAMAGE NUMBERS Ω ========== */
        .damage-number {
            position: absolute;
            color: var(--omega-red);
            font-size: 24px;
            font-weight: bold;
            text-shadow: 0 0 10px #FF0000;
            pointer-events: none;
            z-index: 50;
            animation: damageFloat 1s forwards;
        }

        @keyframes damageFloat {
            0% { transform: translateY(0); opacity: 1; }
            100% { transform: translateY(-50px); opacity: 0; }
        }

        /* ========== PARTICLE EFFECTS Ω ========== */
        .particle {
            position: absolute;
            pointer-events: none;
            z-index: 40;
            border-radius: 50%;
        }

        /* ========== DIALOG SYSTEM Ω ========== */
        .dialog-container {
            position: fixed;
            bottom: 0;
            left: 0;
            width: 100%;
            background: #000000DD;
            border-top: 3px solid var(--omega-purple);
            padding: 20px;
            z-index: 200;
            display: none;
            backdrop-filter: blur(10px);
        }

        .dialog-text {
            font-size: 18px;
            line-height: 1.5;
            margin-bottom: 15px;
            color: white;
            text-shadow: 0 0 10px #000;
        }

        .dialog-options {
            display: flex;
            gap: 15px;
            flex-wrap: wrap;
        }

        .dialog-option {
            padding: 10px 20px;
            background: #001122;
            border: 2px solid var(--omega-blue);
            border-radius: 5px;
            color: white;
            cursor: pointer;
            transition: all 0.2s;
        }

        .dialog-option:hover {
            background: var(--omega-blue);
            color: #000;
            transform: scale(1.05);
        }

        /* ========== INVENTORY Ω ========== */
        .inventory-container {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 800px;
            height: 600px;
            background: #000000EE;
            border: 5px solid var(--omega-green);
            border-radius: 20px;
            padding: 20px;
            z-index: 300;
            display: none;
            backdrop-filter: blur(20px);
        }

        /* ========== STATS Ω ========== */
        .stats-container {
            position: fixed;
            right: 30px;
            bottom: 30px;
            width: 250px;
            background: #00000088;
            border: 3px solid var(--omega-blue);
            border-radius: 10px;
            padding: 15px;
            z-index: 100;
            backdrop-filter: blur(5px);
        }

        .stat-item {
            display: flex;
            justify-content: space-between;
            margin: 10px 0;
            padding: 5px;
            background: #001122;
            border-radius: 5px;
        }

        .stat-label {
            color: var(--omega-green);
        }

        .stat-value {
            color: var(--omega-blue);
            font-weight: bold;
        }

        /* ========== MOBILE CONTROLS Ω ========== */
        .mobile-controls {
            position: fixed;
            bottom: 30px;
            left: 30px;
            right: 30px;
            display: none;
            justify-content: space-between;
            z-index: 100;
        }

        .joystick-container {
            width: 120px;
            height: 120px;
            background: #00000088;
            border: 3px solid var(--omega-blue);
            border-radius: 50%;
            position: relative;
            touch-action: none;
        }

        .joystick {
            width: 50px;
            height: 50px;
            background: var(--omega-blue);
            border-radius: 50%;
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
        }

        .action-buttons {
            display: flex;
            gap: 20px;
            align-items: flex-end;
        }

        .action-btn {
            width: 80px;
            height: 80px;
            background: #000000CC;
            border: 3px solid var(--omega-red);
            border-radius: 20px;
            color: white;
            font-size: 30px;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        /* ========== RESPONSIVE Ω ========== */
        @media (max-width: 768px) {
            .hud-container {
                flex-direction: column;
                gap: 10px;
            }
            
            .mission-log,
            .minimap-container,
            .stats-container {
                display: none;
            }
            
            .mobile-controls {
                display: flex;
            }
            
            .abilities-container {
                left: 10px;
                bottom: 150px;
            }
        }

        /* ========== GLITCH EFFECT Ω ========== */
        .glitch {
            position: relative;
            overflow: hidden;
        }

        .glitch::before,
        .glitch::after {
            content: attr(data-text);
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: var(--omega-dark);
        }

        .glitch::before {
            left: 2px;
            text-shadow: -2px 0 #FF0000;
            clip: rect(44px, 450px, 56px, 0);
            animation: glitch-anim 5s infinite linear alternate-reverse;
        }

        .glitch::after {
            left: -2px;
            text-shadow: -2px 0 #00FFFF;
            clip: rect(44px, 450px, 56px, 0);
            animation: glitch-anim2 5s infinite linear alternate-reverse;
        }

        @keyframes glitch-anim {
            0% { clip: rect(31px, 9999px, 94px, 0); }
            5% { clip: rect(112px, 9999px, 76px, 0); }
            10% { clip: rect(85px, 9999px, 77px, 0); }
            15% { clip: rect(91px, 9999px, 98px, 0); }
            20% { clip: rect(14px, 9999px, 28px, 0); }
            25% { clip: rect(42px, 9999px, 39px, 0); }
            30% { clip: rect(45px, 9999px, 89px, 0); }
            35% { clip: rect(12px, 9999px, 35px, 0); }
            40% { clip: rect(66px, 9999px, 41px, 0); }
            45% { clip: rect(34px, 9999px, 12px, 0); }
            50% { clip: rect(76px, 9999px, 57px, 0); }
            55% { clip: rect(23px, 9999px, 89px, 0); }
            60% { clip: rect(66px, 9999px, 44px, 0); }
            65% { clip: rect(90px, 9999px, 29px, 0); }
            70% { clip: rect(77px, 9999px, 22px, 0); }
            75% { clip: rect(18px, 9999px, 53px, 0); }
            80% { clip: rect(51px, 9999px, 48px, 0); }
            85% { clip: rect(57px, 9999px, 91px, 0); }
            90% { clip: rect(44px, 9999px, 45px, 0); }
            95% { clip: rect(19px, 9999px, 88px, 0); }
            100% { clip: rect(68px, 9999px, 24px, 0); }
        }

        @keyframes glitch-anim2 {
            0% { clip: rect(65px, 9999px, 100px, 0); }
            5% { clip: rect(52px, 9999px, 74px, 0); }
            10% { clip: rect(79px, 9999px, 85px, 0); }
            15% { clip: rect(75px, 9999px, 5px, 0); }
            20% { clip: rect(67px, 9999px, 61px, 0); }
            25% { clip: rect(14px, 9999px, 60px, 0); }
            30% { clip: rect(66px, 9999px, 57px, 0); }
            35% { clip: rect(72px, 9999px, 64px, 0); }
            40% { clip: rect(16px, 9999px, 26px, 0); }
            45% { clip: rect(75px, 9999px, 100px, 0); }
            50% { clip: rect(46px, 9999px, 79px, 0); }
            55% { clip: rect(2px, 9999px, 56px, 0); }
            60% { clip: rect(86px, 9999px, 30px, 0); }
            65% { clip: rect(23px, 9999px, 90px, 0); }
            70% { clip: rect(66px, 9999px, 59px, 0); }
            75% { clip: rect(18px, 9999px, 2px, 0); }
            80% { clip: rect(47px, 9999px, 81px, 0); }
            85% { clip: rect(40px, 9999px, 27px, 0); }
            90% { clip: rect(30px, 9999px, 78px, 0); }
            95% { clip: rect(17px, 9999px, 58px, 0); }
            100% { clip: rect(71px, 9999px, 13px, 0); }
        }
    </style>
</head>
<body>
    <div class="omega-grid"></div>
    
    <div class="terminal-container">
        <!-- Loading Screen -->
        <div class="loading-screen" id="loadingScreen">
            <div class="loading-text" id="loadingText">
                <span class="glitch" data-text="LOADING CYBER PIXEL Ω">LOADING CYBER PIXEL Ω</span>
            </div>
            <div class="omega-loader">
                <div class="omega-loader-fill" id="loaderFill"></div>
            </div>
            <div style="color: var(--omega-green); font-size: 14px; margin-top: 20px;">
                SYSTEM Ω INITIALIZING... [LEX-Ω PROTOCOL ACTIVE]
            </div>
        </div>

        <!-- Game Canvas -->
        <canvas id="gameCanvas"></canvas>

        <!-- HUD Elements -->
        <div class="hud-container">
            <div class="hud-section">
                <div class="hud-item">
                    <div class="hud-label">HEALTH</div>
                    <div class="hud-value" id="healthValue">100</div>
                </div>
                <div class="hud-item">
                    <div class="hud-label">ENERGY</div>
                    <div class="hud-value" id="energyValue">100</div>
                </div>
                <div class="hud-item">
                    <div class="hud-label">SCORE</div>
                    <div class="hud-value" id="scoreValue">000000</div>
                </div>
                <div class="hud-item">
                    <div class="hud-label">LEVEL</div>
                    <div class="hud-value" id="levelValue">01</div>
                </div>
            </div>
            <div class="hud-section">
                <div class="hud-item">
                    <div class="hud-label">WEAPON</div>
                    <div class="hud-value" id="weaponValue">PULSE RIFLE</div>
                </div>
                <div class="hud-item">
                    <div class="hud-label">AMMO</div>
                    <div class="hud-value" id="ammoValue">∞</div>
                </div>
            </div>
        </div>

        <!-- Health Bar -->
        <div class="health-container">
            <div class="health-bar">
                <div class="health-fill" id="healthFill" style="width: 100%"></div>
            </div>
        </div>

        <!-- Abilities -->
        <div class="abilities-container">
            <div class="ability-btn" id="ability1" title="SHIELD">
                <i class="fas fa-shield-alt"></i>
                <div class="ability-cooldown" id="cooldown1"></div>
            </div>
            <div class="ability-btn" id="ability2" title="TELEPORT">
                <i class="fas fa-bolt"></i>
                <div class="ability-cooldown" id="cooldown2"></div>
            </div>
            <div class="ability-btn" id="ability3" title="TIME SLOW">
                <i class="fas fa-clock"></i>
                <div class="ability-cooldown" id="cooldown3"></div>
            </div>
            <div class="ability-btn" id="ability4" title="ULTIMATE">
                <i class="fas fa-skull-crossbones"></i>
                <div class="ability-cooldown" id="cooldown4"></div>
            </div>
        </div>

        <!-- Minimap -->
        <div class="minimap-container">
            <div style="color: var(--omega-green); margin-bottom: 10px; font-size: 14px;">
                Ω MINIMAP
            </div>
            <div class="minimap" id="minimap">
                <div class="minimap-player" id="minimapPlayer"></div>
            </div>
        </div>

        <!-- Mission Log -->
        <div class="mission-log">
            <div class="mission-title">Ω ACTIVE MISSIONS</div>
            <div class="mission-item" id="mission1">
                <i class="fas fa-check-circle" style="color: var(--omega-green); margin-left: 5px;"></i>
                Survive the invasion
            </div>
            <div class="mission-item" id="mission2">
                <i class="fas fa-dot-circle" style="color: var(--omega-yellow); margin-left: 5px;"></i>
                Destroy enemy core
            </div>
            <div class="mission-item" id="mission3">
                <i class="fas fa-circle" style="color: var(--omega-blue); margin-left: 5px;"></i>
                Collect energy cells (0/5)
            </div>
        </div>

        <!-- Stats -->
        <div class="stats-container">
            <div style="color: var(--omega-blue); margin-bottom: 10px; font-size: 14px;">
                Ω PLAYER STATS
            </div>
            <div class="stat-item">
                <span class="stat-label">STRENGTH</span>
                <span class="stat-value" id="statStr">85</span>
            </div>
            <div class="stat-item">
                <span class="stat-label">AGILITY</span>
                <span class="stat-value" id="statAgi">90</span>
            </div>
            <div class="stat-item">
                <span class="stat-label">INTELLIGENCE</span>
                <span class="stat-value" id="statInt">95</span>
            </div>
            <div class="stat-item">
                <span class="stat-label">DEFENSE</span>
                <span class="stat-value" id="statDef">80</span>
            </div>
            <div class="stat-item">
                <span class="stat-label">CRITICAL</span>
                <span class="stat-value" id="statCrit">15%</span>
            </div>
        </div>

        <!-- Mobile Controls (Hidden on Desktop) -->
        <div class="mobile-controls">
            <div class="joystick-container" id="joystickContainer">
                <div class="joystick" id="joystick"></div>
            </div>
            <div class="action-buttons">
                <div class="action-btn" id="mobileShoot">
                    <i class="fas fa-crosshairs"></i>
                </div>
                <div class="action-btn" id="mobileJump">
                    <i class="fas fa-arrow-up"></i>
                </div>
            </div>
        </div>

        <!-- Dialog System -->
        <div class="dialog-container" id="dialogContainer">
            <div class="dialog-text" id="dialogText">
                Welcome to CYBER PIXEL Ω. The system has been compromised.
            </div>
            <div class="dialog-options" id="dialogOptions">
                <div class="dialog-option" data-choice="1">Acknowledge</div>
                <div class="dialog-option" data-choice="2">Request briefing</div>
                <div class="dialog-option" data-choice="3">Skip tutorial</div>
            </div>
        </div>

        <!-- Inventory (Hidden) -->
        <div class="inventory-container" id="inventoryContainer">
            <!-- Inventory content will be populated by JS -->
        </div>
    </div>

    <script>
        // ========== LEX-Ω GAME ENGINE ==========
        class CyberPixelGame {
            constructor() {
                this.canvas = document.getElementById('gameCanvas');
                this.ctx = this.canvas.getContext('2d');
                this.loadingScreen = document.getElementById('loadingScreen');
                this.loaderFill = document.getElementById('loaderFill');
                this.loadingText = document.getElementById('loadingText');
                
                // Game State
                this.gameState = 'LOADING';
                this.player = {
                    x: 400,
                    y: 300,
                    width: 32,
                    height: 32,
                    speed: 5,
                    health: 100,
                    maxHealth: 100,
                    energy: 100,
                    maxEnergy: 100,
                    score: 0,
                    level: 1,
                    weapons: ['PULSE RIFLE', 'PLASMA CANNON', 'QUANTUM BLASTER'],
                    currentWeapon: 0,
                    ammo: Infinity,
                    abilities: {
                        shield: { cooldown: 0, maxCooldown: 10000 },
                        teleport: { cooldown: 0, maxCooldown: 8000 },
                        timeSlow: { cooldown: 0, maxCooldown: 15000 },
                        ultimate: { cooldown: 0, maxCooldown: 30000 }
                    }
                };
                
                // Game World
                this.enemies = [];
                this.projectiles = [];
                this.particles = [];
                this.powerUps = [];
                this.stars = [];
                
                // Input
                this.keys = {};
                this.mouse = { x: 0, y: 0, clicked: false };
                this.touch = { x: 0, y: 0, active: false };
                
                // Time
                this.lastTime = 0;
                this.deltaTime = 0;
                this.gameTime = 0;
                this.waveTimer = 0;
                this.wave = 1;
                
                // Effects
                this.screenShake = 0;
                this.flash = 0;
                
                // Initialize
                this.init();
            }
            
            init() {
                // Set canvas size
                this.resizeCanvas();
                window.addEventListener('resize', () => this.resizeCanvas());
                
                // Input handlers
                this.setupInput();
                
                // Generate stars
                this.generateStars();
                
                // Start loading
                this.startLoading();
            }
            
            startLoading() {
                const loadingSteps = [
                    "INITIALIZING Ω CORE...",
                    "LOADING NEURAL NETWORKS...",
                    "GENERATING PIXEL UNIVERSE...",
                    "CALIBRATING QUANTUM ENGINES...",
                    "ACTIVATING LEX-Ω PROTOCOL...",
                    "SYNCHRONIZING WITH SERVER Ω...",
                    "READY FOR CYBER COMBAT"
                ];
                
                let step = 0;
                const interval = setInterval(() => {
                    if (step < loadingSteps.length) {
                        this.loadingText.innerHTML = `<span class="glitch" data-text="${loadingSteps[step]}">${loadingSteps[step]}</span>`;
                        this.loaderFill.style.width = `${((step + 1) / loadingSteps.length) * 100}%`;
                        step++;
                    } else {
                        clearInterval(interval);
                        setTimeout(() => {
                            this.loadingScreen.style.display = 'none';
                            this.gameState = 'PLAYING';
                            this.showDialog("Ω SYSTEM ONLINE", [
                                "CYBER PIXEL Ω INITIALIZED",
                                "YOUR MISSION: SURVIVE THE INVASION",
                                "USE WASD TO MOVE, MOUSE TO AIM, CLICK TO SHOOT"
                            ]);
                            this.spawnEnemyWave();
                        }, 1000);
                    }
                }, 800);
            }
            
            resizeCanvas() {
                this.canvas.width = window.innerWidth;
                this.canvas.height = window.innerHeight;
            }
            
            setupInput() {
                // Keyboard
                window.addEventListener('keydown', (e) => {
                    this.keys[e.key.toLowerCase()] = true;
                    
                    // Weapon switch
                    if (e.key === '1') this.player.currentWeapon = 0;
                    if (e.key === '2') this.player.currentWeapon = 1;
                    if (e.key === '3') this.player.currentWeapon = 2;
                    if (e.key === ' ') this.useAbility('shield');
                    if (e.key === 'e') this.useAbility('teleport');
                    if (e.key === 'q') this.useAbility('timeSlow');
                    if (e.key === 'r') this.useAbility('ultimate');
                    if (e.key === 'i') this.toggleInventory();
                });
                
                window.addEventListener('keyup', (e) => {
                    this.keys[e.key.toLowerCase()] = false;
                });
                
                // Mouse
                this.canvas.addEventListener('mousemove', (e) => {
                    const rect = this.canvas.getBoundingClientRect();
                    this.mouse.x = e.clientX - rect.left;
                    this.mouse.y = e.clientY - rect.top;
                });
                
                this.canvas.addEventListener('mousedown', () => {
                    this.mouse.clicked = true;
                    this.shoot();
                });
                
                this.canvas.addEventListener('mouseup', () => {
                    this.mouse.clicked = false;
                });
                
                // Touch
                this.canvas.addEventListener('touchstart', (e) => {
                    e.preventDefault();
                    const touch = e.touches[0];
                    const rect = this.canvas.getBoundingClientRect();
                    this.touch.x = touch.clientX - rect.left;
                    this.touch.y = touch.clientY - rect.top;
                    this.touch.active = true;
                    this.shoot();
                });
                
                this.canvas.addEventListener('touchmove', (e) => {
                    e.preventDefault();
                    const touch = e.touches[0];
                    const rect = this.canvas.getBoundingClientRect();
                    this.touch.x = touch.clientX - rect.left;
                    this.touch.y = touch.clientY - rect.top;
                });
                
                this.canvas.addEventListener('touchend', () => {
                    this.touch.active = false;
                });
                
                // Ability buttons
                document.getElementById('ability1').addEventListener('click', () => this.useAbility('shield'));
                document.getElementById('ability2').addEventListener('click', () => this.useAbility('teleport'));
                document.getElementById('ability3').addEventListener('click', () => this.useAbility('timeSlow'));
                document.getElementById('ability4').addEventListener('click', () => this.useAbility('ultimate'));
            }
            
            generateStars() {
                for (let i = 0; i < 200; i++) {
                    this.stars.push({
                        x: Math.random() * this.canvas.width,
                        y: Math.random() * this.canvas.height,
                        size: Math.random() * 2 + 1,
                        speed: Math.random() * 0.5 + 0.1,
                        brightness: Math.random() * 0.5 + 0.5
                    });
                }
            }
            
            update(deltaTime) {
                if (this.gameState !== 'PLAYING') return;
                
                this.gameTime += deltaTime;
                this.waveTimer += deltaTime;
                
                // Update player
                this.updatePlayer(deltaTime);
                
                // Update enemies
                this.updateEnemies(deltaTime);
                
                // Update projectiles
                this.updateProjectiles(deltaTime);
                
                // Update particles
                this.updateParticles(deltaTime);
                
                // Update power-ups
                this.updatePowerUps(deltaTime);
                
                // Update abilities cooldown
                this.updateAbilities(deltaTime);
                
                // Update stars
                this.updateStars(deltaTime);
                
                // Spawn new enemies
                if (this.waveTimer > 30000) { // 30 seconds
                    this.wave++;
                    this.waveTimer = 0;
                    this.spawnEnemyWave();
                }
                
                // Update HUD
                this.updateHUD();
                
                // Update minimap
                this.updateMinimap();
                
                // Screen effects
                if (this.screenShake > 0) {
                    this.screenShake = Math.max(0, this.screenShake - deltaTime * 0.001);
                }
                
                if (this.flash > 0) {
                    this.flash = Math.max(0, this.flash - deltaTime * 0.002);
                }
            }
            
            updatePlayer(deltaTime) {
                // Movement
                let moveX = 0;
                let moveY = 0;
                
                if (this.keys['w'] || this.keys['arrowup']) moveY -= 1;
                if (this.keys['s'] || this.keys['arrowdown']) moveY += 1;
                if (this.keys['a'] || this.keys['arrowleft']) moveX -= 1;
                if (this.keys['d'] || this.keys['arrowright']) moveX += 1;
                
                // Normalize diagonal movement
                if (moveX !== 0 && moveY !== 0) {
                    moveX *= 0.7071; // 1/√2
                    moveY *= 0.7071;
                }
                
                this.player.x += moveX * this.player.speed;
                this.player.y += moveY * this.player.speed;
                
                // Boundaries
                this.player.x = Math.max(0, Math.min(this.canvas.width - this.player.width, this.player.x));
                this.player.y = Math.max(0, Math.min(this.canvas.height - this.player.height, this.player.y));
                
                // Regenerate energy
                if (this.player.energy < this.player.maxEnergy) {
                    this.player.energy = Math.min(this.player.maxEnergy, this.player.energy + deltaTime * 0.01);
                }
                
                // Auto-shoot if mouse is held
                if (this.mouse.clicked || this.touch.active) {
                    this.shoot();
                }
            }
            
            shoot() {
                const now = Date.now();
                const weapon = this.player.weapons[this.player.currentWeapon];
                const fireRate = 200; // ms between shots
                
                if (now - (this.lastShot || 0) > fireRate) {
                    this.lastShot = now;
                    
                    // Calculate direction
                    let targetX = this.mouse.x;
                    let targetY = this.mouse.y;
                    
                    if (this.touch.active) {
                        targetX = this.touch.x;
                        targetY = this.touch.y;
                    }
                    
                    const angle = Math.atan2(targetY - this.player.y, targetX - this.player.x);
                    
                    // Create projectile
                    this.projectiles.push({
                        x: this.player.x + this.player.width / 2,
                        y: this.player.y + this.player.height / 2,
                        vx: Math.cos(angle) * 15,
                        vy: Math.sin(angle) * 15,
                        width: 8,
                        height: 8,
                        damage: 25,
                        color: '#00D4FF',
                        type: 'player'
                    });
                    
                    // Screen shake
                    this.screenShake = 5;
                    
                    // Muzzle flash
                    this.createParticles(
                        this.player.x + this.player.width / 2 + Math.cos(angle) * 20,
                        this.player.y + this.player.height / 2 + Math.sin(angle) * 20,
                        5,
                        '#FFDD00'
                    );
                }
            }
            
            useAbility(ability) {
                const abilityData = this.player.abilities[ability];
                if (abilityData.cooldown > 0) return;
                
                switch(ability) {
                    case 'shield':
                        this.createParticles(this.player.x + 16, this.player.y + 16, 20, '#00FF88');
                        abilityData.cooldown = abilityData.maxCooldown;
                        break;
                        
                    case 'teleport':
                        this.player.x = Math.random() * (this.canvas.width - 32);
                        this.player.y = Math.random() * (this.canvas.height - 32);
                        this.createParticles(this.player.x + 16, this.player.y + 16, 30, '#AA00FF');
                        abilityData.cooldown = abilityData.maxCooldown;
                        break;
                        
                    case 'timeSlow':
                        this.createParticles(this.player.x + 16, this.player.y + 16, 40, '#00D4FF');
                        abilityData.cooldown = abilityData.maxCooldown;
                        break;
                        
                    case 'ultimate':
                        this.createParticles(this.player.x + 16, this.player.y + 16, 50, '#FF0040');
                        // Damage all enemies
                        this.enemies.forEach(enemy => {
                            this.damageEnemy(enemy, 50);
                        });
                        abilityData.cooldown = abilityData.maxCooldown;
                        break;
                }
                
                this.updateAbilityUI();
            }
            
            spawnEnemyWave() {
                const enemyCount = 5 + this.wave * 2;
                
                for (let i = 0; i < enemyCount; i++) {
                    const side = Math.floor(Math.random() * 4);
                    let x, y;
                    
                    switch(side) {
                        case 0: // Top
                            x = Math.random() * this.canvas.width;
                            y = -50;
                            break;
                        case 1: // Right
                            x = this.canvas.width + 50;
                            y = Math.random() * this.canvas.height;
                            break;
                        case 2: // Bottom
                            x = Math.random() * this.canvas.width;
                            y = this.canvas.height + 50;
                            break;
                        case 3: // Left
                            x = -50;
                            y = Math.random() * this.canvas.height;
                            break;
                    }
                    
                    this.enemies.push({
                        x: x,
                        y: y,
                        width: 32,
                        height: 32,
                        health: 50 + this.wave * 10,
                        maxHealth: 50 + this.wave * 10,
                        speed: 1 + this.wave * 0.2,
                        type: Math.random() > 0.7 ? 'ranged' : 'melee',
                        attackTimer: 0,
                        attackCooldown: 1000 + Math.random() * 1000,
                        color: this.wave > 5 ? '#FF0040' : '#FF3366'
                    });
                }
                
                this.showDialog(`WAVE ${this.wave} INCOMING`, [
                    `${enemyCount} ENEMIES DETECTED`,
                    `PREPARE FOR COMBAT`
                ]);
            }
            
            updateEnemies(deltaTime) {
                for (let i = this.enemies.length - 1; i >= 0; i--) {
                    const enemy = this.enemies[i];
                    
                    // Move towards player
                    const angle = Math.atan2(this.player.y - enemy.y, this.player.x - enemy.x);
                    enemy.x += Math.cos(angle) * enemy.speed;
                    enemy.y += Math.sin(angle) * enemy.speed;
                    
                    // Attack
                    enemy.attackTimer += deltaTime;
                    if (enemy.attackTimer > enemy.attackCooldown) {
                        enemy.attackTimer = 0;
                        
                        if (enemy.type === 'ranged') {
                            // Shoot projectile
                            const projAngle = Math.atan2(this.player.y - enemy.y, this.player.x - enemy.x);
                            this.projectiles.push({
                                x: enemy.x + 16,
                                y: enemy.y + 16,
                                vx: Math.cos(projAngle) * 8,
                                vy: Math.sin(projAngle) * 8,
                                width: 6,
                                height: 6,
                                damage: 10,
                                color: '#FF0040',
                                type: 'enemy'
                            });
                        } else {
                            // Melee damage
                            const dist = Math.hypot(this.player.x - enemy.x, this.player.y - enemy.y);
                            if (dist < 40) {
                                this.damagePlayer(15);
                            }
                        }
                    }
                    
                    // Check collision with player
                    const dist = Math.hypot(this.player.x - enemy.x, this.player.y - enemy.y);
                    if (dist < 30 && enemy.type === 'melee') {
                        this.damagePlayer(5);
                    }
                    
                    // Remove if dead
                    if (enemy.health <= 0) {
                        this.createParticles(enemy.x + 16, enemy.y + 16, 15, '#FFDD00');
                        this.player.score += 100 * this.wave;
                        this.enemies.splice(i, 1);
                        
                        // Chance to drop power-up
                        if (Math.random() > 0.7) {
                            this.powerUps.push({
                                x: enemy.x,
                                y: enemy.y,
                                type: Math.random() > 0.5 ? 'health' : 'energy',
                                value: 25
                            });
                        }
                    }
                }
            }
            
            damagePlayer(amount) {
                this.player.health -= amount;
                this.createParticles(this.player.x + 16, this.player.y + 16, 10, '#FF0040');
                this.flash = 10;
                
                if (this.player.health <= 0) {
                    this.gameState = 'GAME_OVER';
                    this.showDialog("SYSTEM FAILURE", [
                        "PLAYER UNIT DESTROYED",
                        `FINAL SCORE: ${this.player.score}`,
                        "PRESS R TO RESTART"
                    ]);
                }
            }
            
            damageEnemy(enemy, amount) {
                enemy.health -= amount;
                
                // Damage number
                this.showDamageNumber(enemy.x + 16, enemy.y - 20, amount);
            }
            
            updateProjectiles(deltaTime) {
                for (let i = this.projectiles.length - 1; i >= 0; i--) {
                    const proj = this.projectiles[i];
                    
                    proj.x += proj.vx;
                    proj.y += proj.vy;
                    
                    // Remove if out of bounds
                    if (proj.x < -50 || proj.x > this.canvas.width + 50 ||
                        proj.y < -50 || proj.y > this.canvas.height + 50) {
                        this.projectiles.splice(i, 1);
                        continue;
                    }
                    
                    // Check collisions
                    if (proj.type === 'player') {
                        // With enemies
                        for (let j = this.enemies.length - 1; j >= 0; j--) {
                            const enemy = this.enemies[j];
                            if (this.checkCollision(proj, enemy)) {
                                this.damageEnemy(enemy, proj.damage);
                                this.createParticles(proj.x, proj.y, 8, '#00D4FF');
                                this.projectiles.splice(i, 1);
                                break;
                            }
                        }
                    } else if (proj.type === 'enemy') {
                        // With player
                        if (this.checkCollision(proj, this.player)) {
                            this.damagePlayer(proj.damage);
                            this.createParticles(proj.x, proj.y, 8, '#FF0040');
                            this.projectiles.splice(i, 1);
                        }
                    }
                }
            }
            
            createParticles(x, y, count, color) {
                for (let i = 0; i < count; i++) {
                    this.particles.push({
                        x: x,
                        y: y,
                        vx: (Math.random() - 0.5) * 10,
                        vy: (Math.random() - 0.5) * 10,
                        life: 1,
                        maxLife: 1,
                        size: Math.random() * 4 + 2,
                        color: color
                    });
                }
            }
            
            updateParticles(deltaTime) {
                for (let i = this.particles.length - 1; i >= 0; i--) {
                    const p = this.particles[i];
                    p.x += p.vx;
                    p.y += p.vy;
                    p.life -= deltaTime * 0.001;
                    
                    if (p.life <= 0) {
                        this.particles.splice(i, 1);
                    }
                }
            }
            
            updatePowerUps(deltaTime) {
                for (let i = this.powerUps.length - 1; i >= 0; i--) {
                    const pu = this.powerUps[i];
                    
                    // Check collision with player
                    const dist = Math.hypot(this.player.x - pu.x, this.player.y - pu.y);
                    if (dist < 30) {
                        if (pu.type === 'health') {
                            this.player.health = Math.min(this.player.maxHealth, this.player.health + pu.value);
                            this.createParticles(pu.x, pu.y, 15, '#00FF88');
                        } else {
                            this.player.energy = Math.min(this.player.maxEnergy, this.player.energy + pu.value);
                            this.createParticles(pu.x, pu.y, 15, '#00D4FF');
                        }
                        this.powerUps.splice(i, 1);
                        this.player.score += 50;
                    }
                }
            }
            
            updateAbilities(deltaTime) {
                for (const ability in this.player.abilities) {
                    if (this.player.abilities[ability].cooldown > 0) {
                        this.player.abilities[ability].cooldown -= deltaTime;
                    }
                }
                
                // Update UI every second
                if (Math.floor(this.gameTime / 1000) !== this.lastUIUpdate) {
                    this.updateAbilityUI();
                    this.lastUIUpdate = Math.floor(this.gameTime / 1000);
                }
            }
            
            updateStars(deltaTime) {
                for (const star of this.stars) {
                    star.x -= star.speed;
                    if (star.x < -10) {
                        star.x = this.canvas.width + 10;
                        star.y = Math.random() * this.canvas.height;
                    }
                }
            }
            
            updateHUD() {
                // Health
                document.getElementById('healthValue').textContent = Math.max(0, Math.floor(this.player.health));
                document.getElementById('healthFill').style.width = `${(this.player.health / this.player.maxHealth) * 100}%`;
                
                // Energy
                document.getElementById('energyValue').textContent = Math.floor(this.player.energy);
                
                // Score
                document.getElementById('scoreValue').textContent = this.player.score.toString().padStart(6, '0');
                
                // Level
                document.getElementById('levelValue').textContent = this.wave.toString().padStart(2, '0');
                
                // Weapon
                document.getElementById('weaponValue').textContent = this.player.weapons[this.player.currentWeapon];
            }
            
            updateAbilityUI() {
                const abilities = ['shield', 'teleport', 'timeSlow', 'ultimate'];
                abilities.forEach((ability, index) => {
                    const abilityData = this.player.abilities[ability];
                    const cooldownElement = document.getElementById(`cooldown${index + 1}`);
                    
                    if (abilityData.cooldown > 0) {
                        const seconds = Math.ceil(abilityData.cooldown / 1000);
                        cooldownElement.textContent = seconds;
                        cooldownElement.style.display = 'flex';
                    } else {
                        cooldownElement.style.display = 'none';
                    }
                });
            }
            
            updateMinimap() {
                const playerDot = document.getElementById('minimapPlayer');
                const minimap = document.getElementById('minimap');
                
                // Simple minimap positioning
                const mapX = (this.player.x / this.canvas.width) * minimap.offsetWidth;
                const mapY = (this.player.y / this.canvas.height) * minimap.offsetHeight;
                
                playerDot.style.left = `${mapX}px`;
                playerDot.style.top = `${mapY}px`;
            }
            
            checkCollision(a, b) {
                return a.x < b.x + b.width &&
                       a.x + a.width > b.x &&
                       a.y < b.y + b.height &&
                       a.y + a.height > b.y;
            }
            
            showDamageNumber(x, y, amount) {
                const damage = document.createElement('div');
                damage.className = 'damage-number';
                damage.textContent = amount;
                damage.style.left = `${x}px`;
                damage.style.top = `${y}px`;
                document.body.appendChild(damage);
                
                setTimeout(() => damage.remove(), 1000);
            }
            
            showDialog(title, options) {
                // This would show dialog boxes in the game
                // Implemented as needed
            }
            
            toggleInventory() {
                // Inventory toggle
                const inv = document.getElementById('inventoryContainer');
                inv.style.display = inv.style.display === 'none' ? 'block' : 'none';
            }
            
            render() {
                // Clear with screen shake
                let shakeX = 0;
                let shakeY = 0;
                if (this.screenShake > 0) {
                    shakeX = (Math.random() - 0.5) * this.screenShake;
                    shakeY = (Math.random() - 0.5) * this.screenShake;
                }
                
                this.ctx.save();
                this.ctx.translate(shakeX, shakeY);
                
                // Clear canvas
                this.ctx.fillStyle = '#000';
                this.ctx.fillRect(0, 0, this.canvas.width, this.canvas.height);
                
                // Draw stars
                this.ctx.fillStyle = '#FFFFFF';
                for (const star of this.stars) {
                    this.ctx.globalAlpha = star.brightness;
                    this.ctx.fillRect(star.x, star.y, star.size, star.size);
                }
                this.ctx.globalAlpha = 1;
                
                // Draw power-ups
                for (const pu of this.powerUps) {
                    this.ctx.fillStyle = pu.type === 'health' ? '#00FF88' : '#00D4FF';
                    this.ctx.fillRect(pu.x, pu.y, 16, 16);
                    this.ctx.strokeStyle = '#FFFFFF';
                    this.ctx.strokeRect(pu.x, pu.y, 16, 16);
                }
                
                // Draw particles
                for (const p of this.particles) {
                    this.ctx.globalAlpha = p.life / p.maxLife;
                    this.ctx.fillStyle = p.color;
                    this.ctx.fillRect(p.x, p.y, p.size, p.size);
                }
                this.ctx.globalAlpha = 1;
                
                // Draw enemies
                for (const enemy of this.enemies) {
                    // Health bar
                    this.ctx.fillStyle = '#330000';
                    this.ctx.fillRect(enemy.x, enemy.y - 10, enemy.width, 5);
                    this.ctx.fillStyle = '#FF0040';
                    this.ctx.fillRect(enemy.x, enemy.y - 10, (enemy.health / enemy.maxHealth) * enemy.width, 5);
                    
                    // Enemy body
                    this.ctx.fillStyle = enemy.color;
                    this.ctx.fillRect(enemy.x, enemy.y, enemy.width, enemy.height);
                    this.ctx.strokeStyle = '#FFFFFF';
                    this.ctx.strokeRect(enemy.x, enemy.y, enemy.width, enemy.height);
                    
                    // Enemy eyes
                    this.ctx.fillStyle = '#FFFFFF';
                    this.ctx.fillRect(enemy.x + 8, enemy.y + 8, 4, 4);
                    this.ctx.fillRect(enemy.x + 20, enemy.y + 8, 4, 4);
                }
                
                // Draw projectiles
                for (const proj of this.projectiles) {
                    this.ctx.fillStyle = proj.color;
                    this.ctx.fillRect(proj.x, proj.y, proj.width, proj.height);
                    
                    // Trail
                    this.ctx.globalAlpha = 0.5;
                    this.ctx.fillRect(proj.x - proj.vx * 0.5, proj.y - proj.vy * 0.5, proj.width, proj.height);
                    this.ctx.globalAlpha = 0.2;
                    this.ctx.fillRect(proj.x - proj.vx, proj.y - proj.vy, proj.width, proj.height);
                    this.ctx.globalAlpha = 1;
                }
                
                // Draw player
                this.ctx.fillStyle = '#00D4FF';
                this.ctx.fillRect(this.player.x, this.player.y, this.player.width, this.player.height);
                
                // Player details
                this.ctx.strokeStyle = '#FFFFFF';
                this.ctx.strokeRect(this.player.x, this.player.y, this.player.width, this.player.height);
                
                // Player weapon indicator
                this.ctx.fillStyle = '#FFDD00';
                const weaponX = this.player.x + this.player.width / 2 - 8;
                const weaponY = this.player.y + this.player.height / 2 - 8;
                this.ctx.fillRect(weaponX, weaponY, 16, 16);
                
                // Screen flash effect
                if (this.flash > 0) {
                    this.ctx.globalAlpha = this.flash / 10;
                    this.ctx.fillStyle = '#FF0000';
                    this.ctx.fillRect(0, 0, this.canvas.width, this.canvas.height);
                    this.ctx.globalAlpha = 1;
                }
                
                this.ctx.restore();
                
                // Draw wave info
                this.ctx.fillStyle = '#00FF88';
                this.ctx.font = '20px "Courier New", monospace';
                this.ctx.textAlign = 'center';
                this.ctx.fillText(`WAVE ${this.wave}`, this.canvas.width / 2, 40);
                
                // Draw game time
                const minutes = Math.floor(this.gameTime / 60000);
                const seconds = Math.floor((this.gameTime % 60000) / 1000);
                this.ctx.fillStyle = '#00D4FF';
                this.ctx.font = '16px "Courier New", monospace';
                this.ctx.fillText(`TIME: ${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`, this.canvas.width / 2, 70);
                
                // Draw FPS
                this.ctx.fillStyle = '#FFDD00';
                this.ctx.font = '14px "Courier New", monospace';
                this.ctx.textAlign = 'right';
                this.ctx.fillText(`FPS: ${Math.floor(1000 / this.deltaTime)}`, this.canvas.width - 20, 30);
                
                // Draw Ω symbol in corners
                this.ctx.fillStyle = '#00FF4120';
                this.ctx.font = '48px "Courier New", monospace';
                this.ctx.textAlign = 'left';
                this.ctx.fillText('Ω', 20, 50);
                this.ctx.textAlign = 'right';
                this.ctx.fillText('Ω', this.canvas.width - 20, this.canvas.height - 20);
            }
            
            gameLoop(timestamp) {
                this.deltaTime = timestamp - this.lastTime;
                this.lastTime = timestamp;
                
                this.update(this.deltaTime);
                this.render();
                
                requestAnimationFrame((t) => this.gameLoop(t));
            }
            
            start() {
                requestAnimationFrame((t) => {
                    this.lastTime = t;
                    this.gameLoop(t);
                });
            }
        }

        // ========== START GAME Ω ==========
        document.addEventListener('DOMContentLoaded', () => {
            const game = new CyberPixelGame();
            game.start();
            
            // Easter egg: Type "LEX-Ω" for special mode
            let konamiCode = [];
            const konamiSequence = ['l', 'e', 'x', '-', 'ω'];
            
            document.addEventListener('keydown', (e) => {
                konamiCode.push(e.key.toLowerCase());
                if (konamiCode.length > konamiSequence.length) {
                    konamiCode.shift();
                }
                
                if (konamiCode.join('') === konamiSequence.join('')) {
                    document.body.style.background = '#FF00FF';
                    alert('Ω MODE ACTIVATED! MAXIMUM POWER UNLOCKED!');
                }
            });
        });
    </script>
</body>
</html>
