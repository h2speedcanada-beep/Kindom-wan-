# Kindom-wan<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NeoRacer 2077 - Futuristic Kid F1 Championship</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Orbitron', sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #0c0c1d 0%, #1a1a3e 100%);
            color: #fff;
            overflow: hidden;
            height: 100vh;
            width: 100vw;
        }
        
        #game-container {
            position: relative;
            width: 100%;
            height: 100%;
        }
        
        #game-canvas {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 1;
        }
        
        #ui-overlay {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 2;
            pointer-events: none;
        }
        
        .main-menu {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            text-align: center;
            background: rgba(10, 15, 40, 0.85);
            backdrop-filter: blur(10px);
            border: 2px solid rgba(0, 200, 255, 0.3);
            border-radius: 20px;
            padding: 40px;
            min-width: 500px;
            pointer-events: all;
            box-shadow: 0 0 50px rgba(0, 200, 255, 0.2);
        }
        
        .game-title {
            font-size: 4rem;
            background: linear-gradient(90deg, #00e0ff 0%, #ff00ff 100%);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            margin-bottom: 10px;
            text-shadow: 0 0 20px rgba(0, 224, 255, 0.5);
            letter-spacing: 2px;
        }
        
        .subtitle {
            font-size: 1.2rem;
            color: #a0e0ff;
            margin-bottom: 40px;
        }
        
        .menu-button {
            display: block;
            width: 100%;
            padding: 18px;
            margin: 15px 0;
            background: linear-gradient(90deg, #0055ff 0%, #00aaff 100%);
            border: none;
            border-radius: 12px;
            color: white;
            font-size: 1.3rem;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            text-transform: uppercase;
            letter-spacing: 1px;
            box-shadow: 0 5px 15px rgba(0, 85, 255, 0.3);
        }
        
        .menu-button:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(0, 170, 255, 0.5);
            background: linear-gradient(90deg, #0088ff 0%, #00ddff 100%);
        }
        
        .hud {
            position: absolute;
            width: 100%;
            padding: 20px;
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
        }
        
        .hud-left {
            display: flex;
            flex-direction: column;
            gap: 15px;
        }
        
        .hud-right {
            display: flex;
            flex-direction: column;
            align-items: flex-end;
            gap: 15px;
        }
        
        .hud-element {
            background: rgba(0, 0, 0, 0.6);
            backdrop-filter: blur(5px);
            border-radius: 10px;
            padding: 15px 20px;
            border: 1px solid rgba(0, 200, 255, 0.3);
        }
        
        .speed-display {
            font-size: 2.5rem;
            font-weight: bold;
            color: #00ffaa;
            text-shadow: 0 0 10px rgba(0, 255, 170, 0.5);
        }
        
        .speed-label {
            font-size: 0.9rem;
            color: #a0e0ff;
            text-transform: uppercase;
            letter-spacing: 1px;
        }
        
        .boost-meter {
            width: 200px;
            height: 20px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 10px;
            overflow: hidden;
            margin-top: 5px;
        }
        
        .boost-fill {
            height: 100%;
            background: linear-gradient(90deg, #ff5500 0%, #ffff00 100%);
            border-radius: 10px;
            transition: width 0.2s ease;
        }
        
        .lap-counter {
            font-size: 1.8rem;
            color: #ffffff;
        }
        
        .lap-label {
            font-size: 0.9rem;
            color: #a0e0ff;
        }
        
        .position-display {
            font-size: 2rem;
            color: #ffcc00;
            text-shadow: 0 0 10px rgba(255, 204, 0, 0.5);
        }
        
        .position-label {
            font-size: 0.9rem;
            color: #a0e0ff;
        }
        
        .world-name {
            font-size: 1.5rem;
            color: #ff66cc;
            text-shadow: 0 0 10px rgba(255, 102, 204, 0.5);
        }
        
        .track-name {
            font-size: 1rem;
            color: #a0e0ff;
        }
        
        .mini-map {
            width: 180px;
            height: 180px;
            background: rgba(0, 0, 0, 0.5);
            border: 2px solid rgba(0, 200, 255, 0.5);
            border-radius: 10px;
            overflow: hidden;
        }
        
        .loading-screen {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: #0a0f28;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            z-index: 10;
        }
        
        .loading-bar-container {
            width: 300px;
            height: 20px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 10px;
            margin-top: 30px;
            overflow: hidden;
        }
        
        .loading-bar {
            height: 100%;
            background: linear-gradient(90deg, #0055ff 0%, #00aaff 100%);
            border-radius: 10px;
            transition: width 0.5s ease;
        }
        
        .loading-text {
            margin-top: 15px;
            font-size: 1.2rem;
            color: #a0e0ff;
        }
        
        .pause-menu {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: rgba(10, 15, 40, 0.9);
            backdrop-filter: blur(10px);
            border: 2px solid rgba(255, 50, 100, 0.3);
            border-radius: 20px;
            padding: 40px;
            min-width: 400px;
            text-align: center;
            display: none;
            pointer-events: all;
        }
        
        .pause-title {
            font-size: 2.5rem;
            color: #ff3366;
            margin-bottom: 30px;
            text-shadow: 0 0 15px rgba(255, 51, 102, 0.5);
        }
        
        .world-select {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: rgba(10, 15, 40, 0.9);
            backdrop-filter: blur(10px);
            border: 2px solid rgba(0, 255, 200, 0.3);
            border-radius: 20px;
            padding: 40px;
            width: 800px;
            display: none;
            grid-template-columns: repeat(3, 1fr);
            gap: 20px;
            pointer-events: all;
        }
        
        .world-card {
            background: rgba(20, 30, 70, 0.7);
            border-radius: 15px;
            padding: 20px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s ease;
            border: 2px solid transparent;
        }
        
        .world-card:hover {
            transform: translateY(-10px);
            border: 2px solid #00ffaa;
            box-shadow: 0 10px 20px rgba(0, 255, 170, 0.3);
        }
        
        .world-icon {
            font-size: 3rem;
            margin-bottom: 15px;
        }
        
        .world-card-title {
            font-size: 1.3rem;
            margin-bottom: 10px;
            color: #ffffff;
        }
        
        .world-card-desc {
            font-size: 0.9rem;
            color: #a0e0ff;
            margin-bottom: 15px;
        }
        
        .world-card-status {
            font-size: 0.8rem;
            padding: 5px 10px;
            border-radius: 20px;
            display: inline-block;
        }
        
        .locked {
            background: rgba(255, 50, 50, 0.3);
            color: #ff6666;
        }
        
        .unlocked {
            background: rgba(50, 255, 50, 0.3);
            color: #66ff66;
        }
        
        .upgrade-menu {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: rgba(10, 15, 40, 0.95);
            backdrop-filter: blur(10px);
            border: 2px solid rgba(255, 215, 0, 0.3);
            border-radius: 20px;
            padding: 40px;
            width: 700px;
            display: none;
            pointer-events: all;
        }
        
        .upgrade-title {
            font-size: 2rem;
            color: #ffcc00;
            margin-bottom: 30px;
            text-align: center;
        }
        
        .upgrade-stats {
            display: flex;
            justify-content: space-between;
            margin-bottom: 30px;
        }
        
        .stat-item {
            text-align: center;
        }
        
        .stat-value {
            font-size: 1.8rem;
            color: #00ffaa;
        }
        
        .stat-name {
            font-size: 0.9rem;
            color: #a0e0ff;
            text-transform: uppercase;
            letter-spacing: 1px;
        }
        
        .upgrade-buttons {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 20px;
        }
        
        .upgrade-button {
            padding: 15px;
            background: linear-gradient(90deg, #222244 0%, #334477 100%);
            border: none;
            border-radius: 10px;
            color: white;
            font-size: 1.1rem;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .upgrade-button:hover:not(:disabled) {
            background: linear-gradient(90deg, #334477 0%, #4466aa 100%);
            transform: translateY(-5px);
        }
        
        .upgrade-button:disabled {
            opacity: 0.5;
            cursor: not-allowed;
        }
        
        .race-results {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: rgba(10, 15, 40, 0.95);
            backdrop-filter: blur(10px);
            border: 2px solid rgba(0, 255, 200, 0.3);
            border-radius: 20px;
            padding: 40px;
            width: 500px;
            display: none;
            pointer-events: all;
            text-align: center;
        }
        
        .results-title {
            font-size: 2.5rem;
            margin-bottom: 30px;
            color: #ffcc00;
        }
        
        .position-large {
            font-size: 4rem;
            color: #00ffaa;
            text-shadow: 0 0 20px rgba(0, 255, 170, 0.5);
            margin: 20px 0;
        }
        
        .results-time {
            font-size: 1.5rem;
            color: #a0e0ff;
            margin-bottom: 30px;
        }
        
        .instructions {
            position: absolute;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%);
            background: rgba(0, 0, 0, 0.5);
            padding: 15px 30px;
            border-radius: 10px;
            font-size: 0.9rem;
            color: #a0e0ff;
            text-align: center;
            border: 1px solid rgba(0, 200, 255, 0.3);
        }
        
        .key {
            display: inline-block;
            background: rgba(255, 255, 255, 0.1);
            padding: 3px 10px;
            margin: 0 5px;
            border-radius: 5px;
            border: 1px solid rgba(255, 255, 255, 0.3);
        }
        
        .credits {
            position: absolute;
            bottom: 10px;
            right: 10px;
            font-size: 0.8rem;
            color: rgba(160, 224, 255, 0.5);
        }
    </style>
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;500;700;900&display=swap" rel="stylesheet">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/three@0.128.0/examples/js/controls/OrbitControls.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/three@0.128.0/examples/js/loaders/GLTFLoader.min.js"></script>
</head>
<body>
    <div id="game-container">
        <canvas id="game-canvas"></canvas>
        
        <div id="ui-overlay">
            <!-- Loading Screen -->
            <div class="loading-screen" id="loading-screen">
                <h1 class="game-title">NEORACER 2077</h1>
                <p class="subtitle">FUTURISTIC KID F1 CHAMPIONSHIP</p>
                <div class="loading-bar-container">
                    <div class="loading-bar" id="loading-bar"></div>
                </div>
                <div class="loading-text" id="loading-text">Loading game assets...</div>
            </div>
            
            <!-- Main Menu -->
            <div class="main-menu" id="main-menu" style="display: none;">
                <h1 class="game-title">NEORACER 2077</h1>
                <p class="subtitle">FUTURISTIC KID F1 CHAMPIONSHIP</p>
                <button class="menu-button" id="start-game">START RACE</button>
                <button class="menu-button" id="world-select-btn">SELECT WORLD</button>
                <button class="menu-button" id="upgrade-car">UPGRADE CAR</button>
                <button class="menu-button" id="view-stats">PLAYER STATS</button>
                <button class="menu-button" id="quit-game">QUIT GAME</button>
            </div>
            
            <!-- HUD -->
            <div class="hud" id="game-hud" style="display: none;">
                <div class="hud-left">
                    <div class="hud-element">
                        <div class="speed-display" id="speed-display">320</div>
                        <div class="speed-label">KM/H</div>
                        <div class="boost-meter">
                            <div class="boost-fill" id="boost-fill" style="width: 80%"></div>
                        </div>
                    </div>
                    
                    <div class="hud-element">
                        <div class="lap-counter" id="lap-counter">1/3</div>
                        <div class="lap-label">LAP</div>
                    </div>
                    
                    <div class="hud-element">
                        <div class="world-name" id="world-name">Neo City Circuit</div>
                        <div class="track-name" id="track-name">Neon Boulevard</div>
                    </div>
                </div>
                
                <div class="hud-right">
                    <div class="hud-element">
                        <div class="position-display" id="position-display">1st</div>
                        <div class="position-label">POSITION</div>
                    </div>
                    
                    <div class="mini-map" id="mini-map"></div>
                    
                    <div class="hud-element">
                        <div id="time-display">01:24.56</div>
                        <div class="lap-label">RACE TIME</div>
                    </div>
                </div>
            </div>
            
            <!-- Pause Menu -->
            <div class="pause-menu" id="pause-menu">
                <h2 class="pause-title">GAME PAUSED</h2>
                <button class="menu-button" id="resume-game">RESUME RACE</button>
                <button class="menu-button" id="restart-race">RESTART RACE</button>
                <button class="menu-button" id="quit-to-menu">MAIN MENU</button>
            </div>
            
            <!-- World Select -->
            <div class="world-select" id="world-select">
                <div class="world-card" data-world="0">
                    <div class="world-icon">🏙️</div>
                    <div class="world-card-title">Neo City Circuit</div>
                    <div class="world-card-desc">Neon skyscrapers, night racing, and floating bridges</div>
                    <div class="world-card-status unlocked">UNLOCKED</div>
                </div>
                
                <div class="world-card" data-world="1">
                    <div class="world-icon">🏜️</div>
                    <div class="world-card-title">Desert Hyper-Track</div>
                    <div class="world-card-desc">Sand storms, speed tunnels, and ancient ruins</div>
                    <div class="world-card-status unlocked">UNLOCKED</div>
                </div>
                
                <div class="world-card" data-world="2">
                    <div class="world-icon">☁️</div>
                    <div class="world-card-title">Skyway Islands</div>
                    <div class="world-card-desc">Floating tracks, gravity drops, and cloud boosts</div>
                    <div class="world-card-status locked">LOCKED</div>
                </div>
                
                <div class="world-card" data-world="3">
                    <div class="world-icon">❄️</div>
                    <div class="world-card-title">Arctic Velocity Zone</div>
                    <div class="world-card-desc">Ice drifting, frozen boosts, and aurora skies</div>
                    <div class="world-card-status locked">LOCKED</div>
                </div>
                
                <div class="world-card" data-world="4">
                    <div class="world-icon">🌋</div>
                    <div class="world-card-title">Volcano Core</div>
                    <div class="world-card-desc">Lava tracks, extreme heat hazards, and magma jumps</div>
                    <div class="world-card-status locked">LOCKED</div>
                </div>
                
                <div class="world-card" data-world="5">
                    <div class="world-icon">🏆</div>
                    <div class="world-card-title">Championship World</div>
                    <div class="world-card-desc">Elite AI rivals, ultimate tracks, and final showdown</div>
                    <div class="world-card-status locked">LOCKED</div>
                </div>
            </div>
            
            <!-- Upgrade Menu -->
            <div class="upgrade-menu" id="upgrade-menu">
                <h2 class="upgrade-title">CAR UPGRADES</h2>
                <div class="upgrade-stats">
                    <div class="stat-item">
                        <div class="stat-value" id="speed-stat">8/10</div>
                        <div class="stat-name">Speed</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-value" id="handling-stat">7/10</div>
                        <div class="stat-name">Handling</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-value" id="boost-stat">6/10</div>
                        <div class="stat-name">Boost Power</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-value" id="shield-stat">5/10</div>
                        <div class="stat-name">Shield</div>
                    </div>
                </div>
                
                <div class="upgrade-buttons">
                    <button class="upgrade-button" id="upgrade-speed">Upgrade Speed (500 XP)</button>
                    <button class="upgrade-button" id="upgrade-handling">Upgrade Handling (400 XP)</button>
                    <button class="upgrade-button" id="upgrade-boost">Upgrade Boost (600 XP)</button>
                    <button class="upgrade-button" id="upgrade-shield">Upgrade Shield (450 XP)</button>
                </div>
                
                <div style="margin-top: 30px; text-align: center;">
                    <div style="font-size: 1.2rem; color: #ffcc00;">Available XP: <span id="xp-amount">1250</span></div>
                </div>
                
                <button class="menu-button" style="margin-top: 30px;" id="close-upgrade">BACK TO MENU</button>
            </div>
            
            <!-- Race Results -->
            <div class="race-results" id="race-results">
                <h2 class="results-title">RACE COMPLETE!</h2>
                <div class="position-large" id="final-position">1st</div>
                <div class="results-time" id="final-time">Time: 02:15.42</div>
                <div class="results-time" id="xp-earned">+250 XP Earned</div>
                <button class="menu-button" id="next-race">NEXT RACE</button>
                <button class="menu-button" style="margin-top: 15px;" id="results-to-menu">MAIN MENU</button>
            </div>
            
            <!-- Instructions -->
            <div class="instructions" id="instructions" style="display: none;">
                <span class="key">W</span>/<span class="key">↑</span> Accelerate | 
                <span class="key">A</span>/<span class="key">←</span> Turn Left | 
                <span class="key">D</span>/<span class="key">→</span> Turn Right | 
                <span class="key">SPACE</span> Boost | 
                <span class="key">SHIFT</span> Drift | 
                <span class="key">ESC</span> Pause
            </div>
            
            <div class="credits">© 2023 NeoRacer Studios | Futuristic Kid F1 Racing</div>
        </div>
    </div>

    <script>
        // Game State
        const gameState = {
            currentScreen: 'loading',
            isPaused: false,
            isRacing: false,
            currentWorld: 0,
            currentTrack: 0,
            playerStats: {
                speed: 8,
                handling: 7,
                boost: 6,
                shield: 5,
                xp: 1250,
                level: 5
            },
            unlockedWorlds: [0, 1],
            racePosition: 1,
            speed: 0,
            boost: 80,
            currentLap: 1,
            totalLaps: 3,
            raceTime: 0
        };

        // Three.js variables
        let scene, camera, renderer, controls;
        let playerCar, track, opponents = [];
        let lights = [];
        let clock = new THREE.Clock();
        
        // Track data for different worlds
        const worlds = [
            {
                name: "Neo City Circuit",
                color: 0x0066ff,
                tracks: [
                    { name: "Neon Boulevard", length: 3500, difficulty: 1 },
                    { name: "Skyline Loop", length: 4200, difficulty: 2 },
                    { name: "Hologram Highway", length: 3800, difficulty: 3 }
                ]
            },
            {
                name: "Desert Hyper-Track",
                color: 0xff9900,
                tracks: [
                    { name: "Sandstorm Speedway", length: 4000, difficulty: 2 },
                    { name: "Ruins Rally", length: 4500, difficulty: 3 },
                    { name: "Mirage Circuit", length: 5000, difficulty: 4 }
                ]
            },
            {
                name: "Skyway Islands",
                color: 0x66ccff,
                tracks: [
                    { name: "Cloud Chaser", length: 3800, difficulty: 3 },
                    { name: "Gravity Drop", length: 4200, difficulty: 4 },
                    { name: "Aether Raceway", length: 4600, difficulty: 5 }
                ]
            }
        ];

        // Initialize the game
        function init() {
            // Setup Three.js scene
            scene = new THREE.Scene();
            scene.fog = new THREE.Fog(0x0a0f28, 10, 1000);
            
            // Setup camera
            camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 5000);
            camera.position.set(0, 10, 20);
            
            // Setup renderer
            renderer = new THREE.WebGLRenderer({ 
                canvas: document.getElementById('game-canvas'),
                antialias: true,
                alpha: true
            });
            renderer.setSize(window.innerWidth, window.innerHeight);
            renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
            renderer.shadowMap.enabled = true;
            renderer.shadowMap.type = THREE.PCFSoftShadowMap;
            
            // Add lighting
            const ambientLight = new THREE.AmbientLight(0x444444);
            scene.add(ambientLight);
            lights.push(ambientLight);
            
            const directionalLight = new THREE.DirectionalLight(0xffffff, 1);
            directionalLight.position.set(10, 20, 5);
            directionalLight.castShadow = true;
            directionalLight.shadow.camera.left = -50;
            directionalLight.shadow.camera.right = 50;
            directionalLight.shadow.camera.top = 50;
            directionalLight.shadow.camera.bottom = -50;
            directionalLight.shadow.mapSize.width = 2048;
            directionalLight.shadow.mapSize.height = 2048;
            scene.add(directionalLight);
            lights.push(directionalLight);
            
            // Add colorful point lights for futuristic effect
            const colors = [0xff0066, 0x00ffaa, 0x0066ff, 0xffaa00];
            for (let i = 0; i < 8; i++) {
                const color = colors[i % colors.length];
                const pointLight = new THREE.PointLight(color, 0.5, 100);
                pointLight.position.set(
                    Math.sin(i * Math.PI / 4) * 30,
                    5,
                    Math.cos(i * Math.PI / 4) * 30
                );
                scene.add(pointLight);
                lights.push(pointLight);
            }
            
            // Create player car
            createPlayerCar();
            
            // Create track
            createTrack();
            
            // Create opponents
            createOpponents(7);
            
            // Add environment elements
            createEnvironment();
            
            // Setup event listeners
            setupEventListeners();
            
            // Start loading assets
            simulateLoading();
            
            // Start animation loop
            animate();
        }
        
        function createPlayerCar() {
            // Create a futuristic F1-style car for the kid hero
            const carGroup = new THREE.Group();
            
            // Car body (main chassis)
            const bodyGeometry = new THREE.BoxGeometry(3, 0.8, 6);
            const bodyMaterial = new THREE.MeshPhongMaterial({ 
                color: 0xff3366,
                shininess: 100,
                specular: 0x444444
            });
            const body = new THREE.Mesh(bodyGeometry, bodyMaterial);
            body.castShadow = true;
            body.receiveShadow = true;
            carGroup.add(body);
            
            // Cockpit
            const cockpitGeometry = new THREE.BoxGeometry(1.2, 0.6, 2);
            const cockpitMaterial = new THREE.MeshPhongMaterial({ 
                color: 0x222222,
                transparent: true,
                opacity: 0.7
            });
            const cockpit = new THREE.Mesh(cockpitGeometry, cockpitMaterial);
            cockpit.position.y = 0.5;
            cockpit.castShadow = true;
            carGroup.add(cockpit);
            
            // Front wing
            const frontWingGeometry = new THREE.BoxGeometry(3.5, 0.1, 1);
            const frontWingMaterial = new THREE.MeshPhongMaterial({ color: 0x00aaff });
            const frontWing = new THREE.Mesh(frontWingGeometry, frontWingMaterial);
            frontWing.position.z = -3;
            frontWing.castShadow = true;
            carGroup.add(frontWing);
            
            // Rear wing
            const rearWingGeometry = new THREE.BoxGeometry(2.5, 0.8, 0.2);
            const rearWingMaterial = new THREE.MeshPhongMaterial({ color: 0x00aaff });
            const rearWing = new THREE.Mesh(rearWingGeometry, rearWingMaterial);
            rearWing.position.z = 2.8;
            rearWing.position.y = 0.8;
            rearWing.castShadow = true;
            carGroup.add(rearWing);
            
            // Wheels
            const wheelGeometry = new THREE.CylinderGeometry(0.5, 0.5, 0.3, 16);
            const wheelMaterial = new THREE.MeshPhongMaterial({ color: 0x222222 });
            
            // Create 4 wheels
            const wheelPositions = [
                { x: 1.2, z: -2 },
                { x: -1.2, z: -2 },
                { x: 1.2, z: 2 },
                { x: -1.2, z: 2 }
            ];
            
            wheelPositions.forEach(pos => {
                const wheel = new THREE.Mesh(wheelGeometry, wheelMaterial);
                wheel.rotation.z = Math.PI / 2;
                wheel.position.x = pos.x;
                wheel.position.z = pos.z;
                wheel.position.y = -0.5;
                wheel.castShadow = true;
                carGroup.add(wheel);
            });
            
            // Energy effects
            const energyGeometry = new THREE.SphereGeometry(0.3, 8, 8);
            const energyMaterial = new THREE.MeshBasicMaterial({ 
                color: 0x00ffff,
                transparent: true,
                opacity: 0.7
            });
            
            const leftEnergy = new THREE.Mesh(energyGeometry, energyMaterial);
            leftEnergy.position.set(-1.5, 0.2, 0);
            carGroup.add(leftEnergy);
            
            const rightEnergy = new THREE.Mesh(energyGeometry, energyMaterial);
            rightEnergy.position.set(1.5, 0.2, 0);
            carGroup.add(rightEnergy);
            
            carGroup.position.y = 0.5;
            scene.add(carGroup);
            playerCar = carGroup;
        }
        
        function createTrack() {
            const trackGroup = new THREE.Group();
            
            // Create a circular track with futuristic elements
            const trackRadius = 50;
            const trackWidth = 10;
            const trackSegments = 64;
            
            // Track surface
            const trackGeometry = new THREE.RingGeometry(
                trackRadius - trackWidth / 2,
                trackRadius + trackWidth / 2,
                trackSegments
            );
            
            // Rotate to be horizontal
            trackGeometry.rotateX(-Math.PI / 2);
            
            const trackMaterial = new THREE.MeshPhongMaterial({ 
                color: worlds[gameState.currentWorld].color,
                side: THREE.DoubleSide,
                shininess: 30
            });
            
            const trackSurface = new THREE.Mesh(trackGeometry, trackMaterial);
            trackSurface.receiveShadow = true;
            trackGroup.add(trackSurface);
            
            // Track edges with neon glow
            const edgeGeometry = new THREE.TorusGeometry(trackRadius, 0.5, 16, trackSegments);
            const edgeMaterial = new THREE.MeshBasicMaterial({ 
                color: 0x00ffff,
                transparent: true,
                opacity: 0.8
            });
            
            const outerEdge = new THREE.Mesh(edgeGeometry, edgeMaterial);
            outerEdge.rotation.x = Math.PI / 2;
            trackGroup.add(outerEdge);
            
            const innerEdge = new THREE.Mesh(edgeGeometry, edgeMaterial);
            innerEdge.scale.set(0.9, 0.9, 0.9);
            innerEdge.rotation.x = Math.PI / 2;
            trackGroup.add(innerEdge);
            
            // Boost pads on track
            const boostPadGeometry = new THREE.BoxGeometry(3, 0.1, 2);
            const boostPadMaterial = new THREE.MeshBasicMaterial({ color: 0xffff00 });
            
            for (let i = 0; i < 8; i++) {
                const angle = (i / 8) * Math.PI * 2;
                const boostPad = new THREE.Mesh(boostPadGeometry, boostPadMaterial);
                boostPad.position.x = Math.sin(angle) * trackRadius;
                boostPad.position.z = Math.cos(angle) * trackRadius;
                boostPad.rotation.y = -angle;
                boostPad.userData.isBoostPad = true;
                trackGroup.add(boostPad);
            }
            
            // Futuristic pillars around track
            const pillarGeometry = new THREE.CylinderGeometry(0.5, 0.5, 20, 8);
            const pillarMaterial = new THREE.MeshPhongMaterial({ color: 0x4444ff });
            
            for (let i = 0; i < 16; i++) {
                const angle = (i / 16) * Math.PI * 2;
                const pillarRadius = trackRadius + 15;
                
                const pillar = new THREE.Mesh(pillarGeometry, pillarMaterial);
                pillar.position.x = Math.sin(angle) * pillarRadius;
                pillar.position.z = Math.cos(angle) * pillarRadius;
                pillar.position.y = 10;
                pillar.castShadow = true;
                trackGroup.add(pillar);
                
                // Add light on top of pillar
                const pillarLight = new THREE.PointLight(0x00aaff, 0.5, 50);
                pillarLight.position.copy(pillar.position);
                pillarLight.position.y += 10;
                trackGroup.add(pillarLight);
                lights.push(pillarLight);
            }
            
            scene.add(trackGroup);
            track = trackGroup;
        }
        
        function createOpponents(count) {
            const opponentColors = [0xff9900, 0x00cc66, 0x9966ff, 0xff66cc, 0x66ccff, 0xffff00, 0xff6666];
            
            for (let i = 0; i < count; i++) {
                const opponentGroup = new THREE.Group();
                
                // Car body
                const bodyGeometry = new THREE.BoxGeometry(2.8, 0.7, 5.5);
                const bodyMaterial = new THREE.MeshPhongMaterial({ 
                    color: opponentColors[i % opponentColors.length],
                    shininess: 80
                });
                const body = new THREE.Mesh(bodyGeometry, bodyMaterial);
                body.castShadow = true;
                opponentGroup.add(body);
                
                // Wheels
                const wheelGeometry = new THREE.CylinderGeometry(0.4, 0.4, 0.25, 12);
                const wheelMaterial = new THREE.MeshPhongMaterial({ color: 0x333333 });
                
                const wheelPositions = [
                    { x: 1, z: -1.8 },
                    { x: -1, z: -1.8 },
                    { x: 1, z: 1.8 },
                    { x: -1, z: 1.8 }
                ];
                
                wheelPositions.forEach(pos => {
                    const wheel = new THREE.Mesh(wheelGeometry, wheelMaterial);
                    wheel.rotation.z = Math.PI / 2;
                    wheel.position.x = pos.x;
                    wheel.position.z = pos.z;
                    wheel.position.y = -0.4;
                    wheel.castShadow = true;
                    opponentGroup.add(wheel);
                });
                
                // Position opponents around track
                const angle = (i / count) * Math.PI * 2;
                const trackRadius = 50;
                const offset = 3;
                
                opponentGroup.position.x = Math.sin(angle) * (trackRadius + offset);
                opponentGroup.position.z = Math.cos(angle) * (trackRadius + offset);
                opponentGroup.position.y = 0.5;
                opponentGroup.rotation.y = -angle + Math.PI / 2;
                
                opponentGroup.userData = {
                    speed: 20 + Math.random() * 10,
                    angle: angle,
                    offset: offset,
                    position: i + 2
                };
                
                scene.add(opponentGroup);
                opponents.push(opponentGroup);
            }
        }
        
        function createEnvironment() {
            // Add skybox
            const skyGeometry = new THREE.SphereGeometry(1000, 32, 32);
            const skyMaterial = new THREE.MeshBasicMaterial({ 
                color: 0x0a0f28,
                side: THREE.BackSide
            });
            const sky = new THREE.Mesh(skyGeometry, skyMaterial);
            scene.add(sky);
            
            // Add stars
            const starsGeometry = new THREE.BufferGeometry();
            const starsCount = 1000;
            const starsPositions = new Float32Array(starsCount * 3);
            
            for (let i = 0; i < starsCount * 3; i += 3) {
                starsPositions[i] = (Math.random() - 0.5) * 2000;
                starsPositions[i + 1] = (Math.random() - 0.5) * 2000;
                starsPositions[i + 2] = (Math.random() - 0.5) * 2000;
            }
            
            starsGeometry.setAttribute('position', new THREE.BufferAttribute(starsPositions, 3));
            
            const starsMaterial = new THREE.PointsMaterial({
                color: 0xffffff,
                size: 2,
                transparent: true
            });
            
            const stars = new THREE.Points(starsGeometry, starsMaterial);
            scene.add(stars);
            
            // Add ground
            const groundGeometry = new THREE.PlaneGeometry(1000, 1000);
            const groundMaterial = new THREE.MeshPhongMaterial({ 
                color: 0x222233,
                shininess: 10
            });
            const ground = new THREE.Mesh(groundGeometry, groundMaterial);
            ground.rotation.x = -Math.PI / 2;
            ground.position.y = -1;
            ground.receiveShadow = true;
            scene.add(ground);
            
            // Add futuristic buildings in the distance
            for (let i = 0; i < 20; i++) {
                const buildingHeight = 20 + Math.random() * 50;
                const buildingGeometry = new THREE.BoxGeometry(
                    5 + Math.random() * 10,
                    buildingHeight,
                    5 + Math.random() * 10
                );
                
                const hue = Math.random() * 0.3 + 0.6; // Blue-purple range
                const buildingMaterial = new THREE.MeshPhongMaterial({ 
                    color: new THREE.Color().setHSL(hue, 0.8, 0.3),
                    emissive: new THREE.Color().setHSL(hue, 0.8, 0.1),
                    shininess: 90
                });
                
                const building = new THREE.Mesh(buildingGeometry, buildingMaterial);
                
                const angle = Math.random() * Math.PI * 2;
                const distance = 150 + Math.random() * 200;
                
                building.position.x = Math.sin(angle) * distance;
                building.position.z = Math.cos(angle) * distance;
                building.position.y = buildingHeight / 2;
                building.castShadow = true;
                
                scene.add(building);
            }
        }
        
        function simulateLoading() {
            let progress = 0;
            const loadingInterval = setInterval(() => {
                progress += Math.random() * 15;
                if (progress > 100) progress = 100;
                
                document.getElementById('loading-bar').style.width = `${progress}%`;
                
                const loadingTexts = [
                    "Loading game assets...",
                    "Initializing 3D engine...",
                    "Preparing tracks...",
                    "Setting up opponents...",
                    "Calibrating speed sensors...",
                    "Almost ready to race!"
                ];
                
                const textIndex = Math.floor(progress / (100 / loadingTexts.length));
                document.getElementById('loading-text').textContent = loadingTexts[Math.min(textIndex, loadingTexts.length - 1)];
                
                if (progress >= 100) {
                    clearInterval(loadingInterval);
                    setTimeout(() => {
                        showScreen('main-menu');
                    }, 500);
                }
            }, 200);
        }
        
        function showScreen(screenName) {
            // Hide all screens
            document.getElementById('loading-screen').style.display = 'none';
            document.getElementById('main-menu').style.display = 'none';
            document.getElementById('game-hud').style.display = 'none';
            document.getElementById('pause-menu').style.display = 'none';
            document.getElementById('world-select').style.display = 'none';
            document.getElementById('upgrade-menu').style.display = 'none';
            document.getElementById('race-results').style.display = 'none';
            document.getElementById('instructions').style.display = 'none';
            
            // Show requested screen
            switch(screenName) {
                case 'loading':
                    document.getElementById('loading-screen').style.display = 'flex';
                    break;
                case 'main-menu':
                    document.getElementById('main-menu').style.display = 'block';
                    break;
                case 'game':
                    document.getElementById('game-hud').style.display = 'flex';
                    document.getElementById('instructions').style.display = 'block';
                    gameState.isRacing = true;
                    break;
                case 'pause':
                    document.getElementById('pause-menu').style.display = 'block';
                    break;
                case 'world-select':
                    document.getElementById('world-select').style.display = 'grid';
                    break;
                case 'upgrade':
                    document.getElementById('upgrade-menu').style.display = 'block';
                    updateUpgradeMenu();
                    break;
                case 'results':
                    document.getElementById('race-results').style.display = 'block';
                    break;
            }
            
            gameState.currentScreen = screenName;
        }
        
        function updateUpgradeMenu() {
            document.getElementById('speed-stat').textContent = 
                `${gameState.playerStats.speed}/10`;
            document.getElementById('handling-stat').textContent = 
                `${gameState.playerStats.handling}/10`;
            document.getElementById('boost-stat').textContent = 
                `${gameState.playerStats.boost}/10`;
            document.getElementById('shield-stat').textContent = 
                `${gameState.playerStats.shield}/10`;
            document.getElementById('xp-amount').textContent = 
                gameState.playerStats.xp;
            
            // Enable/disable upgrade buttons based on XP and max level
            document.getElementById('upgrade-speed').disabled = 
                gameState.playerStats.xp < 500 || gameState.playerStats.speed >= 10;
            document.getElementById('upgrade-handling').disabled = 
                gameState.playerStats.xp < 400 || gameState.playerStats.handling >= 10;
            document.getElementById('upgrade-boost').disabled = 
                gameState.playerStats.xp < 600 || gameState.playerStats.boost >= 10;
            document.getElementById('upgrade-shield').disabled = 
                gameState.playerStats.xp < 450 || gameState.playerStats.shield >= 10;
        }
        
        function updateHUD() {
            // Update speed display
            document.getElementById('speed-display').textContent = 
                Math.floor(gameState.speed);
            
            // Update boost meter
            document.getElementById('boost-fill').style.width = 
                `${gameState.boost}%`;
            
            // Update lap counter
            document.getElementById('lap-counter').textContent = 
                `${gameState.currentLap}/${gameState.totalLaps}`;
            
            // Update position
            const positionSuffix = gameState.racePosition === 1 ? 'st' : 
                                  gameState.racePosition === 2 ? 'nd' : 
                                  gameState.racePosition === 3 ? 'rd' : 'th';
            document.getElementById('position-display').textContent = 
                `${gameState.racePosition}${positionSuffix}`;
            
            // Update world and track names
            document.getElementById('world-name').textContent = 
                worlds[gameState.currentWorld].name;
            document.getElementById('track-name').textContent = 
                worlds[gameState.currentWorld].tracks[gameState.currentTrack].name;
            
            // Update race time
            const minutes = Math.floor(gameState.raceTime / 60);
            const seconds = Math.floor(gameState.raceTime % 60);
            const milliseconds = Math.floor((gameState.raceTime % 1) * 100);
            document.getElementById('time-display').textContent = 
                `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}.${milliseconds.toString().padStart(2, '0')}`;
        }
        
        function setupEventListeners() {
            // Main menu buttons
            document.getElementById('start-game').addEventListener('click', () => {
                startRace();
            });
            
            document.getElementById('world-select-btn').addEventListener('click', () => {
                showScreen('world-select');
            });
            
            document.getElementById('upgrade-car').addEventListener('click', () => {
                showScreen('upgrade');
            });
            
            document.getElementById('quit-game').addEventListener('click', () => {
                // In a real game, this would exit the application
                alert("Thanks for playing NeoRacer 2077!");
            });
            
            // World select
            document.querySelectorAll('.world-card').forEach(card => {
                card.addEventListener('click', () => {
                    const worldId = parseInt(card.dataset.world);
                    if (gameState.unlockedWorlds.includes(worldId)) {
                        gameState.currentWorld = worldId;
                        // Change track color based on world
                        if (track) {
                            scene.remove(track);
                            createTrack();
                        }
                        showScreen('main-menu');
                    } else {
                        alert("World locked! Complete previous races to unlock.");
                    }
                });
            });
            
            // Upgrade buttons
            document.getElementById('upgrade-speed').addEventListener('click', () => {
                if (gameState.playerStats.xp >= 500 && gameState.playerStats.speed < 10) {
                    gameState.playerStats.xp -= 500;
                    gameState.playerStats.speed++;
                    updateUpgradeMenu();
                }
            });
            
            document.getElementById('upgrade-handling').addEventListener('click', () => {
                if (gameState.playerStats.xp >= 400 && gameState.playerStats.handling < 10) {
                    gameState.playerStats.xp -= 400;
                    gameState.playerStats.handling++;
                    updateUpgradeMenu();
                }
            });
            
            document.getElementById('upgrade-boost').addEventListener('click', () => {
                if (gameState.playerStats.xp >= 600 && gameState.playerStats.boost < 10) {
                    gameState.playerStats.xp -= 600;
                    gameState.playerStats.boost++;
                    updateUpgradeMenu();
                }
            });
            
            document.getElementById('upgrade-shield').addEventListener('click', () => {
                if (gameState.playerStats.xp >= 450 && gameState.playerStats.shield < 10) {
                    gameState.playerStats.xp -= 450;
                    gameState.playerStats.shield++;
                    updateUpgradeMenu();
                }
            });
            
            document.getElementById('close-upgrade').addEventListener('click', () => {
                showScreen('main-menu');
            });
            
            // Pause menu buttons
            document.getElementById('resume-game').addEventListener('click', () => {
                gameState.isPaused = false;
                showScreen('game');
            });
            
            document.getElementById('restart-race').addEventListener('click', () => {
                gameState.isPaused = false;
                resetRace();
                showScreen('game');
            });
            
            document.getElementById('quit-to-menu').addEventListener('click', () => {
                gameState.isPaused = false;
                gameState.isRacing = false;
                showScreen('main-menu');
            });
            
            // Race results buttons
            document.getElementById('next-race').addEventListener('click', () => {
                gameState.currentTrack = (gameState.currentTrack + 1) % 3;
                resetRace();
                showScreen('game');
            });
            
            document.getElementById('results-to-menu').addEventListener('click', () => {
                showScreen('main-menu');
            });
            
            // Keyboard controls
            const keys = {};
            
            window.addEventListener('keydown', (e) => {
                keys[e.key.toLowerCase()] = true;
                
                // Toggle pause with ESC
                if (e.key === 'Escape' && gameState.currentScreen === 'game') {
                    gameState.isPaused = !gameState.isPaused;
                    showScreen(gameState.isPaused ? 'pause' : 'game');
                }
                
                // Boost with space
                if (e.key === ' ' && gameState.isRacing && !gameState.isPaused) {
                    if (gameState.boost > 0) {
                        gameState.speed = Math.min(gameState.speed + 50, 400);
                        gameState.boost = Math.max(gameState.boost - 10, 0);
                    }
                }
            });
            
            window.addEventListener('keyup', (e) => {
                keys[e.key.toLowerCase()] = false;
            });
            
            // Game control loop
            function handleControls() {
                if (!gameState.isRacing || gameState.isPaused) return;
                
                // Acceleration
                if (keys['w'] || keys['arrowup']) {
                    gameState.speed = Math.min(gameState.speed + 0.5, 350);
                } else {
                    gameState.speed = Math.max(gameState.speed - 0.2, 0);
                }
                
                // Braking
                if (keys['s'] || keys['arrowdown']) {
                    gameState.speed = Math.max(gameState.speed - 1, 0);
                }
                
                // Steering
                if (keys['a'] || keys['arrowleft']) {
                    if (playerCar) {
                        playerCar.rotation.y += 0.03;
                    }
                }
                
                if (keys['d'] || keys['arrowright']) {
                    if (playerCar) {
                        playerCar.rotation.y -= 0.03;
                    }
                }
                
                // Drift with shift
                if (keys['shift']) {
                    // Drift effect - wider turns
                    if (playerCar) {
                        const driftAmount = 0.05;
                        if (keys['a'] || keys['arrowleft']) {
                            playerCar.rotation.y += driftAmount;
                        }
                        if (keys['d'] || keys['arrowright']) {
                            playerCar.rotation.y -= driftAmount;
                        }
                    }
                }
                
                // Regenerate boost when not in use
                if (!keys[' '] && gameState.boost < 100) {
                    gameState.boost = Math.min(gameState.boost + 0.1, 100);
                }
            }
            
            // Add control handling to animation loop
            const originalAnimate = animate;
            animate = function() {
                handleControls();
                originalAnimate();
            };
            
            // Window resize
            window.addEventListener('resize', () => {
                camera.aspect = window.innerWidth / window.innerHeight;
                camera.updateProjectionMatrix();
                renderer.setSize(window.innerWidth, window.innerHeight);
            });
        }
        
        function startRace() {
            resetRace();
            showScreen('game');
        }
        
        function resetRace() {
            gameState.speed = 0;
            gameState.boost = 100;
            gameState.currentLap = 1;
            gameState.racePosition = 1;
            gameState.raceTime = 0;
            
            // Reset player car position
            if (playerCar) {
                playerCar.position.set(0, 0.5, 40);
                playerCar.rotation.set(0, 0, 0);
            }
            
            // Reset opponents
            opponents.forEach((opponent, i) => {
                const angle = (i / opponents.length) * Math.PI * 2;
                const trackRadius = 50;
                const offset = 3;
                
                opponent.position.x = Math.sin(angle) * (trackRadius + offset);
                opponent.position.z = Math.cos(angle) * (trackRadius + offset);
                opponent.rotation.y = -angle + Math.PI / 2;
                
                opponent.userData.angle = angle;
                opponent.userData.position = i + 2;
            });
        }
        
        function finishRace() {
            gameState.isRacing = false;
            
            // Calculate XP earned based on position
            const xpEarned = 500 - ((gameState.racePosition - 1) * 100);
            gameState.playerStats.xp += xpEarned;
            
            // Update results screen
            const positionSuffix = gameState.racePosition === 1 ? 'st' : 
                                  gameState.racePosition === 2 ? 'nd' : 
                                  gameState.racePosition === 3 ? 'rd' : 'th';
            document.getElementById('final-position').textContent = 
                `${gameState.racePosition}${positionSuffix}`;
            
            const minutes = Math.floor(gameState.raceTime / 60);
            const seconds = Math.floor(gameState.raceTime % 60);
            const milliseconds = Math.floor((gameState.raceTime % 1) * 100);
            document.getElementById('final-time').textContent = 
                `Time: ${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}.${milliseconds.toString().padStart(2, '0')}`;
            
            document.getElementById('xp-earned').textContent = 
                `+${xpEarned} XP Earned`;
            
            showScreen('results');
        }
        
        function animate() {
            requestAnimationFrame(animate);
            
            const delta = clock.getDelta();
            
            // Only update game logic if racing and not paused
            if (gameState.isRacing && !gameState.isPaused) {
                // Update race time
                gameState.raceTime += delta;
                
                // Move player car based on speed
                if (playerCar) {
                    const moveDistance = gameState.speed * delta * 0.1;
                    playerCar.position.x += Math.sin(playerCar.rotation.y) * moveDistance;
                    playerCar.position.z += Math.cos(playerCar.rotation.y) * moveDistance;
                    
                    // Keep car on track (simplified)
                    const distanceFromCenter = Math.sqrt(
                        playerCar.position.x * playerCar.position.x + 
                        playerCar.position.z * playerCar.position.z
                    );
                    
                    if (distanceFromCenter > 60) {
                        // Car is off track - slow down
                        gameState.speed *= 0.95;
                    }
                    
                    // Update camera to follow player
                    const cameraDistance = 20;
                    const cameraHeight = 10;
                    camera.position.x = playerCar.position.x - Math.sin(playerCar.rotation.y) * cameraDistance;
                    camera.position.z = playerCar.position.z - Math.cos(playerCar.rotation.y) * cameraDistance;
                    camera.position.y = playerCar.position.y + cameraHeight;
                    camera.lookAt(playerCar.position);
                }
                
                // Move opponents
                opponents.forEach(opponent => {
                    const opponentData = opponent.userData;
                    
                    // Move opponent along track
                    opponentData.angle += opponentData.speed * delta * 0.01;
                    const trackRadius = 50;
                    
                    opponent.position.x = Math.sin(opponentData.angle) * (trackRadius + opponentData.offset);
                    opponent.position.z = Math.cos(opponentData.angle) * (trackRadius + opponentData.offset);
                    opponent.rotation.y = -opponentData.angle + Math.PI / 2;
                    
                    // Randomly change speed slightly
                    opponentData.speed += (Math.random() - 0.5) * 0.5;
                    opponentData.speed = Math.max(15, Math.min(35, opponentData.speed));
                    
                    // Update opponent position based on performance
                    const playerAngle = Math.atan2(playerCar.position.z, playerCar.position.x);
                    const angleDiff = Math.abs(opponentData.angle - playerAngle);
                    
                    // Simple position calculation based on angle difference
                    if (angleDiff < 0.5) {
                        opponentData.position = gameState.racePosition + 1;
                    } else if (angleDiff > 1.0) {
                        opponentData.position = gameState.racePosition - 1;
                    }
                    
                    // Ensure position is within bounds
                    opponentData.position = Math.max(2, Math.min(opponents.length + 1, opponentData.position));
                });
                
                // Check lap completion (simplified)
                if (playerCar && playerCar.position.z > 40 && Math.abs(playerCar.position.x) < 10) {
                    gameState.currentLap++;
                    
                    if (gameState.currentLap > gameState.totalLaps) {
                        finishRace();
                    }
                }
                
                // Update HUD
                updateHUD();
                
                // Animate lights for futuristic effect
                lights.forEach((light, i) => {
                    if (light.isPointLight) {
                        light.intensity = 0.3 + Math.sin(Date.now() * 0.001 + i) * 0.2;
                    }
                });
                
                // Animate player car wheels
                if (playerCar && gameState.speed > 0) {
                    playerCar.children.forEach(child => {
                        if (child.geometry && child.geometry.type === 'CylinderGeometry') {
                            child.rotation.x += gameState.speed * delta * 0.1;
                        }
                    });
                }
            }
            
            // Render scene
            renderer.render(scene, camera);
        }
        
        // Initialize game when page loads
        window.addEventListener('load', init);
    </script>
</body>
</html>
