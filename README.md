<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quantum Multi-Reality Viewer Lab</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Courier New', monospace;
        }

        body {
            background: linear-gradient(135deg, #0a0a1a 0%, #1a0033 100%);
            color: #00ffea;
            min-height: 100vh;
            overflow-x: hidden;
            position: relative;
        }

        /* Quantum background effects */
        .quantum-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: -1;
        }

        .quantum-particle {
            position: absolute;
            width: 2px;
            height: 2px;
            background: #00ffea;
            border-radius: 50%;
            opacity: 0.3;
            animation: quantum-float 20s infinite linear;
        }

        @keyframes quantum-float {
            0%, 100% { transform: translate(0, 0) scale(1); opacity: 0.2; }
            50% { transform: translate(100px, -100px) scale(2); opacity: 0.6; }
        }

        /* Main container */
        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 20px;
        }

        /* Header */
        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 20px;
            border-bottom: 2px solid #00ffea;
            margin-bottom: 30px;
            background: rgba(0, 20, 40, 0.7);
            border-radius: 10px;
            box-shadow: 0 0 20px rgba(0, 255, 234, 0.3);
        }

        .logo {
            font-size: 2rem;
            font-weight: bold;
            background: linear-gradient(90deg, #00ffea, #ff00ff);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            text-shadow: 0 0 10px rgba(0, 255, 234, 0.5);
        }

        .system-status {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .status-indicator {
            width: 12px;
            height: 12px;
            border-radius: 50%;
            background: #00ff00;
            box-shadow: 0 0 10px #00ff00;
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.5; }
        }

        /* Main lab layout */
        .lab-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            grid-template-rows: auto auto;
            gap: 20px;
            margin-bottom: 30px;
        }

        .panel {
            background: rgba(0, 20, 40, 0.8);
            border: 1px solid #00ffea;
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 0 15px rgba(0, 255, 234, 0.2);
            backdrop-filter: blur(10px);
        }

        .main-viewer {
            grid-column: 1 / -1;
            height: 400px;
            position: relative;
            overflow: hidden;
        }

        /* Reality viewer screen */
        .reality-screen {
            width: 100%;
            height: 100%;
            position: relative;
            border: 2px solid #00ffea;
            border-radius: 5px;
            overflow: hidden;
        }

        .reality-display {
            width: 100%;
            height: 100%;
            position: absolute;
            transition: filter 0.5s, transform 0.5s;
        }

        .dimension-grid {
            position: absolute;
            width: 200%;
            height: 200%;
            background: linear-gradient(90deg, transparent 49%, rgba(0, 255, 234, 0.1) 50%, transparent 51%),
                        linear-gradient(0deg, transparent 49%, rgba(0, 255, 234, 0.1) 50%, transparent 51%);
            background-size: 50px 50px;
            animation: grid-move 20s infinite linear;
        }

        @keyframes grid-move {
            0% { transform: translate(0, 0); }
            100% { transform: translate(-50px, -50px); }
        }

        /* Control panels */
        .control-panel {
            height: 300px;
        }

        .control-title {
            font-size: 1.2rem;
            margin-bottom: 15px;
            color: #ff00ff;
            border-bottom: 1px solid #ff00ff;
            padding-bottom: 5px;
        }

        .parameter {
            margin: 15px 0;
        }

        .param-label {
            display: block;
            margin-bottom: 5px;
            font-size: 0.9rem;
        }

        .slider-container {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        input[type="range"] {
            flex: 1;
            height: 4px;
            -webkit-appearance: none;
            background: #003333;
            border-radius: 2px;
            outline: none;
        }

        input[type="range"]::-webkit-slider-thumb {
            -webkit-appearance: none;
            width: 16px;
            height: 16px;
            border-radius: 50%;
            background: #00ffea;
            cursor: pointer;
            box-shadow: 0 0 10px #00ffea;
        }

        .param-value {
            min-width: 60px;
            text-align: right;
            font-weight: bold;
        }

        /* Universe selector */
        .universe-list {
            max-height: 200px;
            overflow-y: auto;
            margin-top: 10px;
        }

        .universe-item {
            padding: 10px;
            margin: 5px 0;
            background: rgba(0, 40, 80, 0.3);
            border: 1px solid transparent;
            border-radius: 5px;
            cursor: pointer;
            transition: all 0.3s;
        }

        .universe-item:hover {
            border-color: #00ffea;
            background: rgba(0, 40, 80, 0.6);
        }

        .universe-item.active {
            border-color: #ff00ff;
            background: rgba(255, 0, 255, 0.1);
        }

        .universe-id {
            font-weight: bold;
            color: #ff00ff;
        }

        .universe-props {
            font-size: 0.8rem;
            color: #80ffff;
        }

        /* Action buttons */
        .action-panel {
            grid-column: 1 / -1;
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 15px;
            margin-top: 20px;
        }

        .action-btn {
            padding: 15px;
            background: linear-gradient(135deg, #004466, #003344);
            border: 1px solid #00ffea;
            border-radius: 5px;
            color: #00ffea;
            cursor: pointer;
            font-weight: bold;
            text-transform: uppercase;
            letter-spacing: 1px;
            transition: all 0.3s;
        }

        .action-btn:hover {
            background: linear-gradient(135deg, #006688, #004466);
            box-shadow: 0 0 20px rgba(0, 255, 234, 0.5);
            transform: translateY(-2px);
        }

        .action-btn.danger {
            border-color: #ff0066;
            color: #ff0066;
            background: linear-gradient(135deg, #660033, #440022);
        }

        .action-btn.danger:hover {
            box-shadow: 0 0 20px rgba(255, 0, 102, 0.5);
        }

        .action-btn.success {
            border-color: #00ff66;
            color: #00ff66;
            background: linear-gradient(135deg, #006633, #004422);
        }

        .action-btn.success:hover {
            box-shadow: 0 0 20px rgba(0, 255, 102, 0.5);
        }

        /* Quantum state display */
        .quantum-state {
            position: absolute;
            top: 20px;
            right: 20px;
            background: rgba(0, 20, 40, 0.9);
            padding: 15px;
            border: 1px solid #ff00ff;
            border-radius: 5px;
            min-width: 200px;
        }

        .qubit-display {
            display: flex;
            align-items: center;
            margin: 10px 0;
        }

        .qubit-sphere {
            width: 30px;
            height: 30px;
            border-radius: 50%;
            background: radial-gradient(circle at 30% 30%, #ff00ff, #330033);
            margin-right: 10px;
            position: relative;
            animation: qubit-spin 3s infinite linear;
        }

        @keyframes qubit-spin {
            0% { transform: rotateY(0deg); }
            100% { transform: rotateY(360deg); }
        }

        .superposition-bar {
            height: 20px;
            background: linear-gradient(90deg, #ff00ff, #00ffea);
            border-radius: 10px;
            margin: 5px 0;
            position: relative;
            overflow: hidden;
        }

        .probability-wave {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.3), transparent);
            animation: wave-scan 2s infinite linear;
        }

        @keyframes wave-scan {
            0% { transform: translateX(-100%); }
            100% { transform: translateX(100%); }
        }

        /* Terminal output */
        .terminal {
            grid-column: 1 / -1;
            background: rgba(0, 0, 0, 0.8);
            border: 1px solid #00ff00;
            border-radius: 5px;
            padding: 15px;
            font-family: 'Courier New', monospace;
            font-size: 0.9rem;
            color: #00ff00;
            height: 150px;
            overflow-y: auto;
            margin-top: 20px;
        }

        .terminal-line {
            margin: 5px 0;
        }

        .terminal-line::before {
            content: "> ";
            color: #ff00ff;
        }

        /* Footer */
        .footer {
            text-align: center;
            padding: 20px;
            margin-top: 30px;
            border-top: 1px solid #00ffea;
            color: #80ffff;
            font-size: 0.9rem;
        }

        /* Responsive */
        @media (max-width: 768px) {
            .lab-grid {
                grid-template-columns: 1fr;
            }
            
            .action-panel {
                grid-template-columns: repeat(2, 1fr);
            }
        }
    </style>
</head>
<body>
    <!-- Quantum background particles -->
    <div class="quantum-bg" id="quantumBg"></div>

    <div class="container">
        <!-- Header -->
        <header class="header">
            <div class="logo">QMV-LAB v2.7</div>
            <div class="system-status">
                <div class="status-indicator"></div>
                <span>QUANTUM COHERENCE: STABLE</span>
            </div>
        </header>

        <!-- Main lab interface -->
        <main class="lab-grid">
            <!-- Main reality viewer -->
            <div class="panel main-viewer">
                <h2 class="control-title">REALITY VIEWER: UNIVERSE PROBE</h2>
                <div class="reality-screen">
                    <div class="reality-display" id="realityDisplay">
                        <div class="dimension-grid"></div>
                        <!-- Universe visualization will be drawn here by JS -->
                    </div>
                    <div class="quantum-state">
                        <div class="qubit-display">
                            <div class="qubit-sphere"></div>
                            <span>QUBIT ENTANGLEMENT: 98.7%</span>
                        </div>
                        <div class="superposition-bar">
                            <div class="probability-wave"></div>
                        </div>
                        <div id="coherenceLevel">COHERENCE: 87%</div>
                    </div>
                </div>
            </div>

            <!-- Control Panel 1: Physics Parameters -->
            <div class="panel control-panel">
                <h2 class="control-title">PHYSICS PARAMETERS</h2>
                <div class="parameter">
                    <label class="param-label">DIMENSIONAL BRANCHING</label>
                    <div class="slider-container">
                        <input type="range" min="0" max="100" value="50" class="physics-slider" id="dimensionSlider">
                        <span class="param-value" id="dimensionValue">3.5D</span>
                    </div>
                </div>
                <div class="parameter">
                    <label class="param-label">TIME FLOW RATE</label>
                    <div class="slider-container">
                        <input type="range" min="-100" max="100" value="0" class="physics-slider" id="timeSlider">
                        <span class="param-value" id="timeValue">1.0x</span>
                    </div>
                </div>
                <div class="parameter">
                    <label class="param-label">GRAVITATIONAL CONSTANT</label>
                    <div class="slider-container">
                        <input type="range" min="10" max="1000" value="100" class="physics-slider" id="gravitySlider">
                        <span class="param-value" id="gravityValue">1G</span>
                    </div>
                </div>
                <div class="parameter">
                    <label class="param-label">ENTROPY LEVEL</label>
                    <div class="slider-container">
                        <input type="range" min="0" max="100" value="30" class="physics-slider" id="entropySlider">
                        <span class="param-value" id="entropyValue">30%</span>
                    </div>
                </div>
            </div>

            <!-- Control Panel 2: Universe Selection -->
            <div class="panel control-panel">
                <h2 class="control-title">UNIVERSE DATABASE</h2>
                <div class="universe-list" id="universeList">
                    <!-- Universe items will be generated by JS -->
                </div>
                <div class="parameter" style="margin-top: 15px;">
                    <label class="param-label">REALITY SIGNATURE</label>
                    <input type="text" id="signatureInput" value="0x7F3A9B2C" style="width:100%; padding:8px; background:#002244; border:1px solid #00ffea; color:#00ffea; border-radius:3px;">
                </div>
            </div>

            <!-- Action Panel -->
            <div class="action-panel">
                <button class="action-btn" id="btnInitiate">INITIATE PROBE</button>
                <button class="action-btn success" id="btnStabilize">STABILIZE BRIDGE</button>
                <button class="action-btn" id="btnStoreData">STORE DATA</button>
                <button class="action-btn danger" id="btnEmergency">EMERGENCY DISCONNECT</button>
            </div>

            <!-- Terminal Output -->
            <div class="terminal" id="terminal">
                <div class="terminal-line">QMV-LAB SYSTEM BOOTED</div>
                <div class="terminal-line">QUANTUM PROCESSOR: ONLINE</div>
                <div class="terminal-line">REALITY INTERFACE: CALIBRATING...</div>
                <div class="terminal-line">MULTIVERSE DATABASE: 1,247,893 REALITIES INDEXED</div>
            </div>
        </main>

        <!-- Footer -->
        <footer class="footer">
            QUANTUM MULTI-REALITY VIEWER LAB v2.7 | WARNING: REALITY SHIFTING DETECTED | 
            COHERENCE FIELD ACTIVE | DO NOT DISCONNECT DURING OPERATION
        </footer>
    </div>

    <script>
        // Initialize quantum background particles
        function initQuantumBackground() {
            const bg = document.getElementById('quantumBg');
            for (let i = 0; i < 50; i++) {
                const particle = document.createElement('div');
                particle.className = 'quantum-particle';
                particle.style.left = `${Math.random() * 100}%`;
                particle.style.top = `${Math.random() * 100}%`;
                particle.style.animationDelay = `${Math.random() * 5}s`;
                bg.appendChild(particle);
            }
        }

        // Universe database
        const universes = [
            { id: "U-001", signature: "0x7F3A9B2C", name: "Prime Reality", dimensions: 3, timeFlow: 1.0, gravity: 1.0, entropy: 30, color: "#00ffea" },
            { id: "U-247", signature: "0x3B8A9F4D", name: "Fractalverse", dimensions: 2.8, timeFlow: 0.3, gravity: 0.2, entropy: 15, color: "#ff00ff" },
            { id: "U-532", signature: "0x9C2F7A1E", name: "Crystalline Realm", dimensions: 4.2, timeFlow: 2.5, gravity: 3.1, entropy: 5, color: "#ffff00" },
            { id: "U-789", signature: "0x5E1A3C9F", name: "Entropic Void", dimensions: 3.1, timeFlow: 0.1, gravity: 0.05, entropy: 95, color: "#ff5500" },
            { id: "U-112", signature: "0x2D8B6F3A", name: "Neutronium Realm", dimensions: 3.0, timeFlow: 0.01, gravity: 1000, entropy: 10, color: "#00ffff" },
            { id: "U-956", signature: "0x8A3F6C2D", name: "Quantum Foam", dimensions: 6.7, timeFlow: 100, gravity: 0.001, entropy: 80, color: "#aa00ff" }
        ];

        let currentUniverse = universes[0];
        let isProbing = false;
        let coherence = 87;

        // Initialize universe list
        function initUniverseList() {
            const list = document.getElementById('universeList');
            list.innerHTML = '';
            
            universes.forEach(universe => {
                const item = document.createElement('div');
                item.className = 'universe-item';
                if (universe.id === currentUniverse.id) item.classList.add('active');
                
                item.innerHTML = `
                    <div class="universe-id">${universe.id}: ${universe.name}</div>
                    <div class="universe-props">D:${universe.dimensions} | T:${universe.timeFlow}x | G:${universe.gravity}G</div>
                `;
                
                item.addEventListener('click', () => selectUniverse(universe));
                list.appendChild(item);
            });
        }

        // Select a universe
        function selectUniverse(universe) {
            currentUniverse = universe;
            document.getElementById('signatureInput').value = universe.signature;
            
            // Update sliders to match universe
            document.getElementById('dimensionSlider').value = (universe.dimensions - 2) * 50;
            document.getElementById('timeSlider').value = (universe.timeFlow - 1) * 100;
            document.getElementById('gravitySlider').value = universe.gravity * 100;
            document.getElementById('entropySlider').value = universe.entropy;
            
            updateSliderValues();
            updateRealityVisualization();
            initUniverseList();
            logToTerminal(`SELECTED UNIVERSE: ${universe.id} - ${universe.name}`);
        }

        // Update slider value displays
        function updateSliderValues() {
            const dimVal = parseFloat(document.getElementById('dimensionSlider').value);
            const timeVal = parseFloat(document.getElementById('timeSlider').value);
            const gravityVal = parseFloat(document.getElementById('gravitySlider').value);
            const entropyVal = parseFloat(document.getElementById('entropySlider').value);
            
            document.getElementById('dimensionValue').textContent = (2 + dimVal/50).toFixed(1) + "D";
            document.getElementById('timeValue').textContent = (1 + timeVal/100).toFixed(1) + "x";
            document.getElementById('gravityValue').textContent = (gravityVal/100).toFixed(2) + "G";
            document.getElementById('entropyValue').textContent = entropyVal + "%";
        }

        // Create reality visualization
        function updateRealityVisualization() {
            const display = document.getElementById('realityDisplay');
            const dim = 2 + parseFloat(document.getElementById('dimensionSlider').value) / 50;
            const entropy = parseFloat(document.getElementById('entropySlider').value);
            
            // Clear previous visualization
            display.innerHTML = '<div class="dimension-grid"></div>';
            
            // Create dimensional visualization based on dimension value
            if (dim > 3.5) {
                // Higher dimensions: complex fractal patterns
                for (let i = 0; i < 20; i++) {
                    const shape = document.createElement('div');
                    shape.style.position = 'absolute';
                    shape.style.width = `${10 + i * 5}px`;
                    shape.style.height = `${10 + i * 5}px`;
                    shape.style.left = `${30 + i * 15}%`;
                    shape.style.top = `${30 + i % 10 * 15}%`;
                    shape.style.border = `2px solid ${currentUniverse.color}`;
                    shape.style.transform = `rotate(${i * 18}deg)`;
                    shape.style.opacity = '0.6';
                    display.appendChild(shape);
                }
            } else if (dim < 3) {
                // Lower dimensions: flat, grid-like
                display.style.background = `repeating-linear-gradient(
                    45deg,
                    transparent,
                    transparent 10px,
                    ${currentUniverse.color}22 10px,
                    ${currentUniverse.color}22 20px
                )`;
            }
            
            // Add entropy effect (noise/particles)
            for (let i = 0; i < entropy; i++) {
                const particle = document.createElement('div');
                particle.style.position = 'absolute';
                particle.style.width = '4px';
                particle.style.height = '4px';
                particle.style.background = '#ffffff';
                particle.style.borderRadius = '50%';
                particle.style.left = `${Math.random() * 100}%`;
                particle.style.top = `${Math.random() * 100}%`;
                particle.style.opacity = Math.random() * 0.5;
                particle.style.animation = `quantum-float ${2 + Math.random() * 3}s infinite linear`;
                display.appendChild(particle);
            }
            
            // Update coherence based on parameter stability
            const paramVariance = Math.abs(dim - currentUniverse.dimensions) + 
                                 Math.abs(entropy - currentUniverse.entropy);
            coherence = Math.max(30, 100 - paramVariance * 10);
            document.getElementById('coherenceLevel').textContent = `COHERENCE: ${coherence.toFixed(0)}%`;
        }

        // Terminal logging
        function logToTerminal(message) {
            const terminal = document.getElementById('terminal');
            const line = document.createElement('div');
            line.className = 'terminal-line';
            line.textContent = message;
            terminal.appendChild(line);
            terminal.scrollTop = terminal.scrollHeight;
            
            // Keep only last 10 lines
            const lines = terminal.querySelectorAll('.terminal-line');
            if (lines.length > 10) {
                lines[0].remove();
            }
        }

        // Initiate reality probe
        function initiateProbe() {
            if (isProbing) return;
            
            isProbing = true;
            logToTerminal(`INITIATING REALITY PROBE TO: ${currentUniverse.signature}`);
            logToTermical(`DIMENSIONAL SYNCHRONIZATION IN PROGRESS...`);
            
            // Animate the reality display
            const display = document.getElementById('realityDisplay');
            display.style.filter = 'brightness(1.5) contrast(1.2)';
            display.style.transform = 'scale(1.02)';
            
            // Simulate quantum computation
            let progress = 0;
            const probeInterval = setInterval(() => {
                progress += 10;
                logToTerminal(`PROBE PROGRESS: ${progress}%`);
                
                if (progress >= 100) {
                    clearInterval(probeInterval);
                    logToTerminal(`REALITY BRIDGE ESTABLISHED WITH ${currentUniverse.name}`);
                    logToTerminal(`WARNING: LOCAL PHYSICS MAY BE UNSTABLE`);
                    display.style.filter = 'brightness(1.8) contrast(1.5) hue-rotate(90deg)';
                    isProbing = false;
                }
            }, 300);
        }

        // Stabilize quantum bridge
        function stabilizeBridge() {
            logToTerminal(`STABILIZING QUANTUM BRIDGE...`);
            logToTerminal(`APPLYING ENTANGLEMENT CORRECTION...`);
            
            coherence = Math.min(100, coherence + 15);
            document.getElementById('coherenceLevel').textContent = `COHERENCE: ${coherence.toFixed(0)}%`;
            
            const display = document.getElementById('realityDisplay');
            display.style.filter = 'brightness(1.2) contrast(1.1)';
            display.style.transform = 'scale(1)';
            
            setTimeout(() => {
                logToTerminal(`BRIDGE STABILIZED AT ${coherence}% COHERENCE`);
                logToTerminal(`SAFE FOR DATA TRANSFER`);
            }, 1000);
        }

        // Store data in alternate reality
        function storeData() {
            if (coherence < 60) {
                logToTerminal(`ERROR: INSUFFICIENT COHERENCE FOR DATA STORAGE`);
                logToTerminal(`REQUIRED: 60% | CURRENT: ${coherence.toFixed(0)}%`);
                return;
            }
            
            const dataSize = Math.floor(Math.random() * 1000) + 100;
            logToTerminal(`INITIATING QUANTUM DATA STORAGE...`);
            logToTerminal(`ENCODING ${dataSize} QBITS TO ${currentUniverse.name}`);
            
            let stored = 0;
            const storageInterval = setInterval(() => {
                stored += 100;
                logToTerminal(`STORAGE PROGRESS: ${Math.min(stored, dataSize)}/${dataSize} QBITS`);
                
                if (stored >= dataSize) {
                    clearInterval(storageInterval);
                    logToTerminal(`DATA STORED IN ${currentUniverse.signature}`);
                    logToTerminal(`RETRIEVAL SIGNATURE: 0x${Math.random().toString(16).substr(2,8).toUpperCase()}`);
                    
                    // Simulate data transfer effect
                    const particles = document.querySelectorAll('.quantum-particle');
                    particles.forEach(p => {
                        p.style.background = '#00ff00';
                        setTimeout(() => p.style.background = '#00ffea', 500);
                    });
                }
            }, 200);
        }

        // Emergency disconnect
        function emergencyDisconnect() {
            logToTerminal(`!!! EMERGENCY DISCONNECT INITIATED !!!`);
            logToTerminal(`COLLAPSING REALITY BRIDGE...`);
            logToTerminal(`PURGING QUANTUM ENTANGLEMENT...`);
            
            const display = document.getElementById('realityDisplay');
            display.style.filter = 'brightness(0.5) contrast(0.8) blur(5px)';
            display.style.transform = 'scale(0.98)';
            
            coherence = 30;
            document.getElementById('coherenceLevel').textContent = `COHERENCE: ${coherence}%`;
            
            setTimeout(() => {
                display.style.filter = 'none';
                display.style.transform = 'scale(1)';
                logToTerminal(`DISCONNECT COMPLETE`);
                logToTerminal(`SYSTEM REBOOTING...`);
                setTimeout(() => logToTerminal(`SYSTEM READY`), 1000);
            }, 1500);
        }

        // Initialize everything
        document.addEventListener('DOMContentLoaded', function() {
            initQuantumBackground();
            initUniverseList();
            updateSliderValues();
            updateRealityVisualization();
            
            // Event listeners for sliders
            document.querySelectorAll('.physics-slider').forEach(slider => {
                slider.addEventListener('input', function() {
                    updateSliderValues();
                    updateRealityVisualization();
                });
            });
            
            // Event listeners for buttons
            document.getElementById('btnInitiate').addEventListener('click', initiateProbe);
            document.getElementById('btnStabilize').addEventListener('click', stabilizeBridge);
            document.getElementById('btnStoreData').addEventListener('click', storeData);
            document.getElementById('btnEmergency').addEventListener('click', emergencyDisconnect);
            
            // Initialize terminal
            logToTerminal(`SYSTEM READY - AWAITING COMMANDS`);
        });

        // Add random system updates
        setInterval(() => {
            if (Math.random() > 0.7 && !isProbing) {
                const messages = [
                    "QUANTUM FLUCTUATIONS DETECTED",
                    "BACKGROUND ENTROPY: STABLE",
                    "MULTIVERSE DATABASE UPDATED",
                    "REALITY SIGNATURES VERIFIED",
                    "COHERENCE FIELD: NOMINAL"
                ];
                logToTerminal(messages[Math.floor(Math.random() * messages.length)]);
            }
        }, 5000);
    </script>
</body>
</html>
