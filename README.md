
<html lang="en" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Wormhole Engineering Mission Control - Phases 1, 2 & 3</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        cyber: {
                            cyan: '#00f0ff',
                            purple: '#a855f7',
                            crimson: '#ff1744',
                            amber: '#ffab00',
                            dark: '#030712',
                            panel: '#0b0f19'
                        }
                    }
                }
            }
        }
    </script>
    <!-- Google Fonts: Orbitron & Inter -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Orbitron:wght@400;600;800;900&display=swap" rel="stylesheet">
    <!-- FontAwesome for Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #030712;
            color: #f3f4f6;
            overflow-x: hidden;
        }
        .font-orbitron {
            font-family: 'Orbitron', sans-serif;
        }
        .glass-panel {
            background: rgba(11, 15, 25, 0.9);
            backdrop-filter: blur(14px);
            border: 1px solid rgba(0, 240, 255, 0.15);
            box-shadow: 0 0 35px rgba(0, 0, 0, 0.7), inset 0 0 20px rgba(0, 240, 255, 0.03);
        }
        .glow-cyan {
            text-shadow: 0 0 12px rgba(0, 240, 255, 0.7);
        }
        .glow-purple {
            text-shadow: 0 0 12px rgba(168, 85, 247, 0.7);
        }
        .glow-amber {
            text-shadow: 0 0 12px rgba(255, 171, 0, 0.7);
        }
        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 5px;
        }
        ::-webkit-scrollbar-track {
            background: #030712;
        }
        ::-webkit-scrollbar-thumb {
            background: #1f2937;
            border-radius: 3px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #374151;
        }
        .scanlines {
            background: linear-gradient(rgba(18, 16, 16, 0) 50%, rgba(0, 0, 0, 0.25) 50%), linear-gradient(90deg, rgba(255, 0, 0, 0.03), rgba(0, 255, 0, 0.01), rgba(0, 0, 255, 0.03));
            background-size: 100% 3px, 3px 100%;
            pointer-events: none;
        }
    </style>
</head>
<body class="min-h-screen flex flex-col relative">

    <!-- CRT Scanlines Overlay -->
    <div class="absolute inset-0 scanlines z-30 pointer-events-none"></div>

    <!-- Top Mission Control Header -->
    <header class="glass-panel border-b border-cyan-500/20 px-6 py-3.5 flex flex-wrap justify-between items-center z-20">
        <div class="flex items-center space-x-3">
            <div class="w-10 h-10 rounded-xl bg-cyan-500/10 border border-cyan-400/40 flex items-center justify-center text-cyan-400">
                <i class="fa-solid fa-satellite-dish text-xl animate-pulse"></i>
            </div>
            <div>
                <h1 class="font-orbitron font-extrabold text-lg tracking-wider text-white glow-cyan">PROJECT EINSTEIN-ROSEN: MISSION CONTROL</h1>
                <p class="text-[11px] text-cyan-400/70 tracking-widest uppercase font-orbitron">Unified Triad Operations: SROS • MHD • SAMS</p>
            </div>
        </div>
        
        <div class="flex items-center space-x-4 mt-3 md:mt-0">
            <!-- Mission Timer & Status -->
            <div class="hidden sm:flex items-center space-x-3 bg-slate-900/90 border border-slate-800 px-4 py-1.5 rounded-xl text-xs font-orbitron">
                <span class="text-slate-400">MISSION CLOCK:</span>
                <span id="mission-timer" class="text-cyan-400 font-bold">T+ 00:00:00</span>
            </div>

            <button id="codex-btn" class="px-3.5 py-2 rounded-xl bg-slate-800/80 hover:bg-slate-700 border border-cyan-500/30 text-cyan-300 text-xs font-orbitron transition flex items-center space-x-2">
                <i class="fa-solid fa-book-atlas"></i>
                <span>Engineering Codex</span>
            </button>

            <div class="flex items-center space-x-2 bg-slate-900/90 border border-slate-800 px-3 py-1.5 rounded-xl">
                <span id="global-status-indicator" class="w-2.5 h-2.5 rounded-full bg-cyan-400 animate-ping"></span>
                <span id="global-status-text" class="text-xs font-orbitron text-cyan-400 font-bold">ACTIVE PHASE 1</span>
            </div>
        </div>
    </header>

    <!-- Main Mission Control Grid -->
    <div class="flex-1 grid grid-cols-1 lg:grid-cols-12 gap-4 p-4 max-w-[1920px] w-full mx-auto z-10">

        <!-- Left / Center: Simulation Canvas Panel (Cols 1-8) -->
        <div class="lg:col-span-8 glass-panel rounded-2xl p-4 flex flex-col relative overflow-hidden min-h-[550px] lg:min-h-[720px]">
            <!-- Canvas Header & Phase Toolbar -->
            <div class="flex flex-wrap justify-between items-center mb-3 gap-2">
                <div class="flex items-center space-x-2">
                    <i class="fa-solid fa-vr-cardboard text-cyan-400"></i>
                    <h2 class="font-orbitron font-semibold text-xs tracking-wider text-cyan-300">REAL-TIME SPACETIME METRIC & FLEET TELEMETRY VIEW</h2>
                </div>

                <!-- Phase Selection Toolbar -->
                <div class="flex items-center space-x-1.5 bg-slate-950/80 p-1 rounded-xl border border-slate-800">
                    <button id="phase-1-btn" class="px-3 py-1.5 rounded-lg bg-cyan-500 text-slate-950 text-xs font-orbitron font-bold transition">Phase 1: SROS</button>
                    <button id="phase-2-btn" class="px-3 py-1.5 rounded-lg bg-slate-900 text-slate-400 hover:text-white text-xs font-orbitron transition">Phase 2: MHD</button>
                    <button id="phase-3-btn" class="px-3 py-1.5 rounded-lg bg-slate-900 text-slate-400 hover:text-white text-xs font-orbitron transition">Phase 3: SAMS</button>
                    <button id="autocycle-btn" class="px-3 py-1.5 rounded-lg bg-slate-900 text-purple-400 hover:bg-purple-950/50 text-xs font-orbitron border border-purple-500/30 transition flex items-center space-x-1">
                        <i class="fa-solid fa-rotate"></i>
                        <span>Auto-Cycle</span>
                    </button>
                </div>
            </div>

            <!-- Canvas Container -->
            <div class="flex-1 relative rounded-xl overflow-hidden border border-cyan-500/10 bg-black/70 flex items-center justify-center">
                <canvas id="simCanvas" class="w-full h-full block cursor-crosshair"></canvas>
                
                <!-- Dynamic Phase Overlay Badge -->
                <div id="phase-hud-badge" class="absolute top-3 left-3 pointer-events-none bg-slate-950/85 backdrop-blur-md px-3.5 py-2 rounded-xl border border-cyan-500/30 text-xs font-orbitron text-cyan-300 flex items-center space-x-2 shadow-lg">
                    <i class="fa-solid fa-atom text-cyan-400 animate-spin"></i>
                    <div>
                        <div id="badge-title" class="font-bold tracking-wider">PHASE 1: SROS ALIGNMENT LATTICE</div>
                        <div id="badge-sub" class="text-[10px] text-slate-400">AutoNav laser quantum lock in progress...</div>
                    </div>
                </div>

                <!-- Canvas Control Overlays -->
                <div class="absolute bottom-3 right-3 flex items-center space-x-2">
                    <button id="pause-sim" class="px-3 py-1.5 bg-slate-900/90 hover:bg-slate-800 border border-slate-700 text-slate-300 rounded-lg text-xs font-orbitron transition">
                        <i class="fa-solid fa-pause mr-1"></i> Pause
                    </button>
                    <button id="reset-sim" class="px-3 py-1.5 bg-slate-900/90 hover:bg-slate-800 border border-slate-700 text-slate-300 rounded-lg text-xs font-orbitron transition">
                        <i class="fa-solid fa-rotate-right mr-1"></i> Reset
                    </button>
                </div>
            </div>
        </div>

        <!-- Right: Telemetry, Controls & Mission Log (Cols 9-12) -->
        <div class="lg:col-span-4 flex flex-col space-y-4">
            
            <!-- Telemetry Metrics Card -->
            <div class="glass-panel rounded-2xl p-4 space-y-3.5">
                <h3 class="font-orbitron font-semibold text-xs tracking-wider text-cyan-400 flex items-center space-x-2">
                    <i class="fa-solid fa-chart-line"></i>
                    <span>SYSTEM TELEMETRY & METRICS</span>
                </h3>

                <div class="grid grid-cols-2 gap-2.5">
                    <div class="bg-slate-950/70 p-2.5 rounded-xl border border-cyan-500/10">
                        <div class="text-[10px] text-slate-400 font-orbitron">QUANTUM COHERENCE</div>
                        <div id="val-coherence" class="text-base font-orbitron font-bold text-cyan-300 glow-cyan">99.98%</div>
                    </div>
                    <div class="bg-slate-950/70 p-2.5 rounded-xl border border-cyan-500/10">
                        <div class="text-[10px] text-slate-400 font-orbitron">VACUUM ENERGY (J/m³)</div>
                        <div id="val-vacuum" class="text-base font-orbitron font-bold text-purple-400 glow-purple">4.82e21</div>
                    </div>
                    <div class="bg-slate-950/70 p-2.5 rounded-xl border border-cyan-500/10">
                        <div class="text-[10px] text-slate-400 font-orbitron">THROAT STABILITY</div>
                        <div id="val-stability" class="text-base font-orbitron font-bold text-amber-400 glow-amber">84.5%</div>
                    </div>
                    <div class="bg-slate-950/70 p-2.5 rounded-xl border border-cyan-500/10">
                        <div class="text-[10px] text-slate-400 font-orbitron">TIDAL STRESS (G)</div>
                        <div id="val-tidal" class="text-base font-orbitron font-bold text-rose-400">0.04 G</div>
                    </div>
                </div>

                <!-- Integrity Progress Bar -->
                <div class="bg-slate-950/80 p-3 rounded-xl border border-slate-800 space-y-1.5">
                    <div class="flex justify-between items-center text-xs font-orbitron">
                        <span class="text-slate-300">BRIDGE HORIZON INTEGRITY</span>
                        <span id="integrity-percent" class="text-cyan-400 font-bold">84.5%</span>
                    </div>
                    <div class="w-full bg-slate-800 h-2 rounded-full overflow-hidden">
                        <div id="bar-integrity" class="bg-gradient-to-r from-purple-500 via-cyan-400 to-amber-400 h-full transition-all duration-300" style="width: 84.5%;"></div>
                    </div>
                </div>
            </div>

            <!-- Interactive Subsystem Sliders Card -->
            <div class="glass-panel rounded-2xl p-4 space-y-3">
                <h3 class="font-orbitron font-semibold text-xs tracking-wider text-cyan-400 flex items-center space-x-2">
                    <i class="fa-solid fa-sliders"></i>
                    <span>SUBSYSTEM CONTROLS</span>
                </h3>

                <!-- Relativistic Velocity Slider -->
                <div class="space-y-1">
                    <div class="flex justify-between text-xs font-orbitron">
                        <span class="text-slate-300">MHD Fleet Relativistic Velocity</span>
                        <span id="val-velocity" class="text-cyan-400 font-bold">0.85 c</span>
                    </div>
                    <input id="range-velocity" type="range" min="0.50" max="0.99" step="0.01" value="0.85" 
                           class="w-full h-2 bg-slate-800 rounded-lg appearance-none cursor-pointer accent-cyan-400">
                </div>

                <!-- SAMS Dampening Frequency Slider -->
                <div class="space-y-1">
                    <div class="flex justify-between text-xs font-orbitron">
                        <span class="text-slate-300">SAMS Piezo Dampening Frequency</span>
                        <span id="val-frequency" class="text-purple-400 font-bold">142.8 GHz</span>
                    </div>
                    <input id="range-frequency" type="range" min="50.0" max="300.0" step="1.0" value="142.8" 
                           class="w-full h-2 bg-slate-800 rounded-lg appearance-none cursor-pointer accent-purple-500">
                </div>

                <!-- Vacuum Excitation Rate Slider -->
                <div class="space-y-1">
                    <div class="flex justify-between text-xs font-orbitron">
                        <span class="text-slate-300">Vacuum Quantum Excitation Rate</span>
                        <span id="val-excitation" class="text-amber-400 font-bold">78.4%</span>
                    </div>
                    <input id="range-excitation" type="range" min="10.0" max="100.0" step="0.5" value="78.4" 
                           class="w-full h-2 bg-slate-800 rounded-lg appearance-none cursor-pointer accent-amber-400">
                </div>
            </div>

            <!-- Mission Log Terminal Card -->
            <div class="glass-panel rounded-2xl p-4 flex flex-col h-[180px]">
                <h3 class="font-orbitron font-semibold text-xs tracking-wider text-cyan-400 flex items-center space-x-2 mb-2">
                    <i class="fa-solid fa-terminal"></i>
                    <span>MISSION LOG TERMINAL</span>
                </h3>
                <div id="terminal-logs" class="flex-1 bg-slate-950/90 rounded-xl p-2.5 font-mono text-[11px] text-cyan-300 overflow-y-auto space-y-1 border border-slate-800">
                    <div>[00:00:01] SROS Fleet deployed between Point A & B.</div>
                    <div>[00:00:04] AutoNav AI laser mesh established.</div>
                    <div>[00:00:08] Transitioning to Phase 2: MHD Generation.</div>
                </div>
            </div>

        </div>

    </div>

    <!-- Engineering Codex Modal -->
    <div id="codex-modal" class="fixed inset-0 z-50 flex items-center justify-center bg-black/85 backdrop-blur-md hidden p-4">
        <div class="glass-panel rounded-2xl max-w-3xl w-full p-6 space-y-4 max-h-[85vh] overflow-y-auto border border-cyan-500/40 relative">
            <div class="flex justify-between items-center border-b border-cyan-500/20 pb-3">
                <div class="flex items-center space-x-2 text-cyan-400 font-orbitron font-bold text-lg">
                    <i class="fa-solid fa-book-atlas"></i>
                    <span>WORMHOLE ENGINEERING PROJECT CODEX</span>
                </div>
                <button id="close-codex" class="text-slate-400 hover:text-white text-xl p-1">
                    <i class="fa-solid fa-xmark"></i>
                </button>
            </div>
            
            <div class="space-y-4 text-sm text-slate-300 leading-relaxed">
                <div>
                    <h4 class="font-orbitron font-bold text-cyan-400 mb-1">Phase 1: Preparation & Alignment (SROS Fleet)</h4>
                    <p>Multiple SROS (Synchronized Optical Network System) drones position themselves between Point A (Entry) and Point B (Exit). They fire a dense shimmering laser mesh guided by AutoNav AI. This channel locks the exact quantum coordinates of spacetime between the two regions without carrying matter yet.</p>
                </div>

                <div>
                    <h4 class="font-orbitron font-bold text-purple-400 mb-1">Phase 2: Generation & Extraction (MHD Fleet & Portal Genesis)</h4>
                    <p>High-speed relativistic drone swarms execute continuous circular orbits around Points A and B. Frame-dragging (Lense-Thirring effect) agitates the quantum vacuum, exciting virtual particles into real energy states. The MHD reactor captures this energy, feeding Nave A (positive gravitational collapse) and Nave B (negative Casimir pressure expansion) to open the Einstein-Rosen bridge.</p>
                </div>

                <div>
                    <h4 class="font-orbitron font-bold text-amber-400 mb-1">Phase 3: Stabilization & Crossing (SAMS Support Fleet)</h4>
                    <p>With the wormhole open, support ships equipped with SAMS (Spatial Acoustic & Magnetic Stabilizers) position themselves at the throat boundaries. Using high-frequency piezoelectric actuators and magnetorheological fluids, they act as spacetime shock absorbers, damping brutal tidal forces and ensuring safe transit for cargo ships.</p>
                </div>
            </div>

            <div class="pt-4 border-t border-slate-800 flex justify-end">
                <button id="close-codex-btn" class="px-5 py-2 bg-cyan-500 hover:bg-cyan-400 text-slate-950 font-orbitron font-bold rounded-lg text-xs transition">
                    Acknowledge Protocols
                </button>
            </div>
        </div>
    </div>

    <script>
        window.addEventListener('DOMContentLoaded', () => {
            const canvas = document.getElementById('simCanvas');
            const ctx = canvas.getContext('2d');

            let isPaused = false;
            let time = 0;
            let missionSeconds = 0;
            let currentPhase = 1; // 1, 2, or 3
            let autoCycle = false;
            let autoCycleTimer = 0;

            // Interactive parameters
            let relativisticVel = 0.85;
            let samsFreq = 142.8;
            let vacuumExcite = 78.4;

            // UI Elements
            const phase1Btn = document.getElementById('phase-1-btn');
            const phase2Btn = document.getElementById('phase-2-btn');
            const phase3Btn = document.getElementById('phase-3-btn');
            const autoCycleBtn = document.getElementById('autocycle-btn');
            const pauseSimBtn = document.getElementById('pause-sim');
            const resetSimBtn = document.getElementById('reset-sim');
            const globalStatusText = document.getElementById('global-status-text');
            const globalStatusIndicator = document.getElementById('global-status-indicator');
            const badgeTitle = document.getElementById('badge-title');
            const badgeSub = document.getElementById('badge-sub');
            const missionTimerEl = document.getElementById('mission-timer');
            const terminalLogs = document.getElementById('terminal-logs');

            // Telemetry UI
            const valCoherence = document.getElementById('val-coherence');
            const valVacuum = document.getElementById('val-vacuum');
            const valStability = document.getElementById('val-stability');
            const valTidal = document.getElementById('val-tidal');
            const integrityPercent = document.getElementById('integrity-percent');
            const barIntegrity = document.getElementById('bar-integrity');

            // Sliders
            const rangeVelocity = document.getElementById('range-velocity');
            const valVelocity = document.getElementById('val-velocity');
            const rangeFreq = document.getElementById('range-frequency');
            const valFreq = document.getElementById('val-frequency');
            const rangeExcite = document.getElementById('range-excitation');
            const valExcite = document.getElementById('val-excitation');

            // Codex modal
            const codexBtn = document.getElementById('codex-btn');
            const codexModal = document.getElementById('codex-modal');
            const closeCodex = document.getElementById('close-codex');
            const closeCodexBtn = document.getElementById('close-codex-btn');

            // Starfield particles
            const stars = [];
            const numStars = 120;
            for (let i = 0; i < numStars; i++) {
                stars.push({
                    x: Math.random() * 2000 - 1000,
                    y: Math.random() * 2000 - 1000,
                    z: Math.random() * 1000 + 10,
                    size: Math.random() * 2 + 0.5
                });
            }

            // Canvas Resize Handler
            function resizeCanvas() {
                const rect = canvas.parentElement.getBoundingClientRect();
                canvas.width = rect.width * window.devicePixelRatio;
                canvas.height = rect.height * window.devicePixelRatio;
                ctx.scale(window.devicePixelRatio, window.devicePixelRatio);
            }
            window.addEventListener('resize', resizeCanvas);
            resizeCanvas();

            // Logger utility
            function logTerminal(msg) {
                const div = document.createElement('div');
                const mins = String(Math.floor(missionSeconds / 60)).padStart(2, '0');
                const secs = String(missionSeconds % 60).padStart(2, '0');
                div.textContent = `[00:${mins}:${secs}] ${msg}`;
                terminalLogs.appendChild(div);
                terminalLogs.scrollTop = terminalLogs.scrollHeight;
            }

            // Phase Switching Logic
            function setPhase(phase) {
                currentPhase = phase;
                phase1Btn.className = phase === 1 ? 'px-3 py-1.5 rounded-lg bg-cyan-500 text-slate-950 text-xs font-orbitron font-bold transition' : 'px-3 py-1.5 rounded-lg bg-slate-900 text-slate-400 hover:text-white text-xs font-orbitron transition';
                phase2Btn.className = phase === 2 ? 'px-3 py-1.5 rounded-lg bg-purple-500 text-slate-950 text-xs font-orbitron font-bold transition' : 'px-3 py-1.5 rounded-lg bg-slate-900 text-slate-400 hover:text-white text-xs font-orbitron transition';
                phase3Btn.className = phase === 3 ? 'px-3 py-1.5 rounded-lg bg-amber-400 text-slate-950 text-xs font-orbitron font-bold transition' : 'px-3 py-1.5 rounded-lg bg-slate-900 text-slate-400 hover:text-white text-xs font-orbitron transition';

                if (phase === 1) {
                    globalStatusText.textContent = 'ACTIVE PHASE 1';
                    globalStatusIndicator.className = 'w-2.5 h-2.5 rounded-full bg-cyan-400 animate-ping';
                    badgeTitle.textContent = 'PHASE 1: SROS ALIGNMENT LATTICE';
                    badgeSub.textContent = 'AutoNav laser quantum lock in progress...';
                    logTerminal('Switching telemetry to Phase 1 (SROS Alignment).');
                } else if (phase === 2) {
                    globalStatusText.textContent = 'ACTIVE PHASE 2';
                    globalStatusIndicator.className = 'w-2.5 h-2.5 rounded-full bg-purple-400 animate-ping';
                    badgeTitle.textContent = 'PHASE 2: MHD GENERATION & PORTAL GENESIS';
                    badgeSub.textContent = 'Relativistic circular vortex & vacuum excitation active.';
                    logTerminal('Switching telemetry to Phase 2 (MHD Generation & Portal).');
                } else if (phase === 3) {
                    globalStatusText.textContent = 'ACTIVE PHASE 3';
                    globalStatusIndicator.className = 'w-2.5 h-2.5 rounded-full bg-amber-400 animate-ping';
                    badgeTitle.textContent = 'PHASE 3: SAMS STABILIZATION & CROSSING';
                    badgeSub.textContent = 'Piezo/magnetorheological damping online. Transit corridor open.';
                    logTerminal('Switching telemetry to Phase 3 (SAMS Stabilization & Transit).');
                }
            }

            phase1Btn.addEventListener('click', () => { autoCycle = false; autoCycleBtn.className = 'px-3 py-1.5 rounded-lg bg-slate-900 text-purple-400 hover:bg-purple-950/50 text-xs font-orbitron border border-purple-500/30 transition flex items-center space-x-1'; setPhase(1); });
            phase2Btn.addEventListener('click', () => { autoCycle = false; autoCycleBtn.className = 'px-3 py-1.5 rounded-lg bg-slate-900 text-purple-400 hover:bg-purple-950/50 text-xs font-orbitron border border-purple-500/30 transition flex items-center space-x-1'; setPhase(2); });
            phase3Btn.addEventListener('click', () => { autoCycle = false; autoCycleBtn.className = 'px-3 py-1.5 rounded-lg bg-slate-900 text-purple-400 hover:bg-purple-950/50 text-xs font-orbitron border border-purple-500/30 transition flex items-center space-x-1'; setPhase(3); });

            autoCycleBtn.addEventListener('click', () => {
                autoCycle = !autoCycle;
                if (autoCycle) {
                    autoCycleBtn.className = 'px-3 py-1.5 rounded-lg bg-purple-600 text-white text-xs font-orbitron border border-purple-400 transition flex items-center space-x-1 shadow-lg shadow-purple-950';
                    logTerminal('Auto-cycle mode engaged across Phases 1, 2, and 3.');
                } else {
                    autoCycleBtn.className = 'px-3 py-1.5 rounded-lg bg-slate-900 text-purple-400 hover:bg-purple-950/50 text-xs font-orbitron border border-purple-500/30 transition flex items-center space-x-1';
                    logTerminal('Auto-cycle mode disengaged.');
                }
            });

            pauseSimBtn.addEventListener('click', () => {
                isPaused = !isPaused;
                pauseSimBtn.innerHTML = isPaused ? '<i class="fa-solid fa-play mr-1"></i> Resume' : '<i class="fa-solid fa-pause mr-1"></i> Pause';
            });

            resetSimBtn.addEventListener('click', () => {
                time = 0;
                missionSeconds = 0;
                setPhase(1);
                logTerminal('Simulation telemetry reset to initial state.');
            });

            // Sliders event listeners
            rangeVelocity.addEventListener('input', (e) => {
                relativisticVel = parseFloat(e.target.value);
                valVelocity.textContent = relativisticVel.toFixed(2) + ' c';
            });
            rangeFreq.addEventListener('input', (e) => {
                samsFreq = parseFloat(e.target.value);
                valFreq.textContent = samsFreq.toFixed(1) + ' GHz';
            });
            rangeExcite.addEventListener('input', (e) => {
                vacuumExcite = parseFloat(e.target.value);
                valExcite.textContent = vacuumExcite.toFixed(1) + '%';
            });

            // Codex modal controls
            codexBtn.addEventListener('click', () => codexModal.classList.remove('hidden'));
            closeCodex.addEventListener('click', () => codexModal.classList.add('hidden'));
            closeCodexBtn.addEventListener('click', () => codexModal.classList.add('hidden'));

            // Mission timer interval
            setInterval(() => {
                if (!isPaused) {
                    missionSeconds++;
                    const hrs = String(Math.floor(missionSeconds / 3600)).padStart(2, '0');
                    const mins = String(Math.floor((missionSeconds % 3600) / 60)).padStart(2, '0');
                    const secs = String(missionSeconds % 60).padStart(2, '0');
                    missionTimerEl.textContent = `T+ ${hrs}:${mins}:${secs}`;

                    // Auto-cycle phases every 15 seconds if active
                    if (autoCycle) {
                        autoCycleTimer++;
                        if (autoCycleTimer >= 15) {
                            autoCycleTimer = 0;
                            const nextPhase = (currentPhase % 3) + 1;
                            setPhase(nextPhase);
                        }
                    }
                }
            }, 1000);

            function animate() {
                const width = canvas.parentElement.clientWidth;
                const height = canvas.parentElement.clientHeight;

                ctx.clearRect(0, 0, width, height);

                if (!isPaused) {
                    time += 0.03;
                }

                // 1. Parallax Starfield with Relativistic Speed Blur
                ctx.save();
                const starSpeed = relativisticVel * 4;
                stars.forEach(star => {
                    star.z -= starSpeed;
                    if (star.z <= 0) star.z = 1000;
                    
                    const k = 300 / star.z;
                    const px = star.x * k + width / 2;
                    const py = star.y * k + height / 2;

                    if (px >= 0 && px <= width && py >= 0 && py <= height) {
                        const pSize = Math.max(0.1, star.size * k);
                        ctx.fillStyle = `rgba(255, 255, 255, ${Math.min(1, k)})`;
                        ctx.beginPath();
                        ctx.arc(px, py, pSize, 0, Math.PI * 2);
                        ctx.fill();
                    }
                });
                ctx.restore();

                // Coordinates for Point A (Entry) and Point B (Exit)
                const pointAX = width * 0.28;
                const pointAY = height * 0.5;
                const pointBX = width * 0.72;
                const pointBY = height * 0.5;

                // Update Telemetry based on Phase
                let coherence = 99.98;
                let vacuumVal = "4.82e21";
                let stabilityVal = 84.5;
                let tidalVal = "0.04 G";

                if (currentPhase === 1) {
                    coherence = 99.99;
                    vacuumVal = "1.20e18";
                    stabilityVal = 45.0;
                    tidalVal = "0.01 G";
                } else if (currentPhase === 2) {
                    coherence = 96.85;
                    vacuumVal = (vacuumExcite * 1.25).toFixed(2) + "e21";
                    stabilityVal = 72.4;
                    tidalVal = "1.85 G";
                } else if (currentPhase === 3) {
                    coherence = 99.42;
                    vacuumVal = "8.95e21";
                    stabilityVal = 98.9;
                    tidalVal = "0.12 G";
                }

                valCoherence.textContent = coherence.toFixed(2) + '%';
                valVacuum.textContent = vacuumVal;
                valStability.textContent = stabilityVal.toFixed(1) + '%';
                valTidal.textContent = tidalVal;
                integrityPercent.textContent = stabilityVal.toFixed(1) + '%';
                barIntegrity.style.width = stabilityVal + '%';

                // ==========================================
                // PHASE 1: SROS Fleet - Laser Alignment Lattice
                // ==========================================
                if (currentPhase === 1) {
                    ctx.save();
                    // SROS Drone Nodes between Point A and Point B
                    const numSrosDrones = 6;
                    for (let i = 0; i <= numSrosDrones; i++) {
                        const t = i / numSrosDrones;
                        const dx = pointAX + (pointBX - pointAX) * t;
                        const dy = pointAY + Math.sin(time * 2 + i) * 15;

                        // Draw Laser Grid Mesh Lines
                        if (i < numSrosDrones) {
                            const nextT = (i + 1) / numSrosDrones;
                            const nextDx = pointAX + (pointBX - pointAX) * nextT;
                            const nextDy = pointAY + Math.sin(time * 2 + (i + 1)) * 15;

                            ctx.beginPath();
                            ctx.moveTo(dx, dy);
                            ctx.lineTo(nextDx, nextDy);
                            ctx.strokeStyle = 'rgba(0, 240, 255, 0.4)';
                            ctx.lineWidth = 1.5;
                            ctx.setLineDash([4, 4]);
                            ctx.stroke();
                            ctx.setLineDash([]);
                        }

                        // SROS Drone Icon
                        ctx.beginPath();
                        ctx.arc(dx, dy, 7, 0, Math.PI * 2);
                        ctx.fillStyle = '#030712';
                        ctx.strokeStyle = '#00f0ff';
                        ctx.lineWidth = 2;
                        ctx.shadowColor = '#00f0ff';
                        ctx.shadowBlur = 10;
                        ctx.fill();
                        ctx.stroke();
                        ctx.shadowBlur = 0;

                        // Laser beam pulse
                        const beamPulse = (time * 15 + i * 20) % 100;
                        ctx.beginPath();
                        ctx.arc(dx, dy, (beamPulse % 20) * 0.6, 0, Math.PI * 2);
                        ctx.strokeStyle = `rgba(0, 240, 255, ${1 - (beamPulse % 20) / 20})`;
                        ctx.stroke();
                    }

                    // Point A & B Markers (SROS Target anchors)
                    [ {x: pointAX, y: pointAY, label: 'POINT A (ENTRY)'}, {x: pointBX, y: pointBY, label: 'POINT B (EXIT)'} ].forEach(pt => {
                        ctx.beginPath();
                        ctx.arc(pt.x, pt.y, 18, 0, Math.PI * 2);
                        ctx.strokeStyle = 'rgba(0, 240, 255, 0.6)';
                        ctx.lineWidth = 1.5;
                        ctx.stroke();

                        ctx.fillStyle = '#00f0ff';
                        ctx.font = '10px Orbitron';
                        ctx.textAlign = 'center';
                        ctx.fillText(pt.label, pt.x, pt.y - 25);
                    });

                    ctx.restore();
                }

                // ==========================================
                // PHASE 2: MHD Fleet - Generation & Portal Genesis
                // ==========================================
                else if (currentPhase === 2) {
                    ctx.save();
                    
                    // Relativistic Circular Drone Swarms around Point A and Point B
                    [ {x: pointAX, y: pointAY, color: '#ff1744', name: 'NAVE A (ATTRACTOR)'}, 
                      {x: pointBX, y: pointBY, color: '#00f0ff', name: 'NAVE B (EXPANSOR)'} ].forEach((node, idx) => {
                        
                        // Circular Orbit Ring
                        ctx.beginPath();
                        ctx.arc(node.x, node.y, 65, 0, Math.PI * 2);
                        ctx.strokeStyle = `${node.color}33`;
                        ctx.lineWidth = 1;
                        ctx.setLineDash([3, 3]);
                        ctx.stroke();
                        ctx.setLineDash([]);

                        // Orbiting Relativistic Drones
                        for (let d = 0; d < 4; d++) {
                            const angle = time * (relativisticVel * 3) + (d * Math.PI / 2);
                            const droneX = node.x + Math.cos(angle) * 65;
                            const droneY = node.y + Math.sin(angle) * 65;

                            ctx.beginPath();
                            ctx.arc(droneX, droneY, 4, 0, Math.PI * 2);
                            ctx.fillStyle = node.color;
                            ctx.shadowColor = node.color;
                            ctx.shadowBlur = 12;
                            ctx.fill();
                            ctx.shadowBlur = 0;
                        }

                        // Central Ship Core
                        ctx.beginPath();
                        ctx.arc(node.x, node.y, 14, 0, Math.PI * 2);
                        ctx.fillStyle = '#030712';
                        ctx.strokeStyle = node.color;
                        ctx.lineWidth = 2.5;
                        ctx.shadowColor = node.color;
                        ctx.shadowBlur = 15;
                        ctx.fill();
                        ctx.stroke();
                        ctx.shadowBlur = 0;

                        ctx.fillStyle = node.color;
                        ctx.font = '10px Orbitron';
                        ctx.textAlign = 'center';
                        ctx.fillText(node.name, node.x, node.y - 25);
                    });

                    // Einstein-Rosen Bridge Opening Portal between A and B
                    const portalRadius = 45 + Math.sin(time * 3) * 5;
                    const portalGrad = ctx.createRadialGradient(pointAX, pointAY, 5, pointAX, pointAY, portalRadius * 1.5);
                    portalGrad.addColorStop(0, 'rgba(168, 85, 247, 0.9)');
                    portalGrad.addColorStop(0.6, 'rgba(0, 240, 255, 0.4)');
                    portalGrad.addColorStop(1, 'transparent');

                    ctx.fillStyle = portalGrad;
                    ctx.beginPath();
                    ctx.arc(pointAX, pointAY, portalRadius * 1.5, 0, Math.PI * 2);
                    ctx.fill();

                    // Tunnel Connection Curve to Point B
                    ctx.beginPath();
                    ctx.moveTo(pointAX, pointAY - portalRadius);
                    ctx.bezierCurveTo(width * 0.4, pointAY - portalRadius * 2, width * 0.6, pointBY - portalRadius * 2, pointBX, pointBY - portalRadius);
                    ctx.lineTo(pointBX, pointBY + portalRadius);
                    ctx.bezierCurveTo(width * 0.6, pointBY + portalRadius * 2, width * 0.4, pointAY + portalRadius * 2, pointAX, pointAY + portalRadius);
                    ctx.closePath();
                    ctx.fillStyle = 'rgba(168, 85, 247, 0.15)';
                    ctx.strokeStyle = 'rgba(168, 85, 247, 0.6)';
                    ctx.lineWidth = 2;
                    ctx.fill();
                    ctx.stroke();

                    ctx.restore();
                }

                // ==========================================
                // PHASE 3: SAMS Fleet - Stabilization & Crossing
                // ==========================================
                else if (currentPhase === 3) {
                    ctx.save();

                    // Established Wormhole Throat Corridor
                    const throatRadius = 55;
                    const throatGrad = ctx.createRadialGradient(pointAX, pointAY, 10, pointAX, pointAY, throatRadius * 1.8);
                    throatGrad.addColorStop(0, 'rgba(255, 171, 0, 0.8)');
                    throatGrad.addColorStop(0.5, 'rgba(0, 240, 255, 0.3)');
                    throatGrad.addColorStop(1, 'transparent');

                    ctx.fillStyle = throatGrad;
                    ctx.beginPath();
                    ctx.arc(pointAX, pointAY, throatRadius * 1.8, 0, Math.PI * 2);
                    ctx.fill();

                    // SAMS Support Drones at Throat Boundaries emitting Piezo Waves
                    const samsCount = 6;
                    for (let s = 0; s < samsCount; s++) {
                        const angle = (s / samsCount) * Math.PI * 2 + (time * 0.5);
                        const sx = pointAX + Math.cos(angle) * 75;
                        const sy = pointAY + Math.sin(angle) * 75;

                        ctx.beginPath();
                        ctx.arc(sx, sy, 5, 0, Math.PI * 2);
                        ctx.fillStyle = '#ffab00';
                        ctx.shadowColor = '#ffab00';
                        ctx.shadowBlur = 10;
                        ctx.fill();
                        ctx.shadowBlur = 0;

                        // Piezoelectric dampening frequency wave rings
                        ctx.beginPath();
                        ctx.arc(sx, sy, 15 + Math.sin(time * 8 + s) * 8, 0, Math.PI * 2);
                        ctx.strokeStyle = 'rgba(255, 171, 0, 0.35)';
                        ctx.lineWidth = 1;
                        ctx.stroke();
                    }

                    // Transit Cargo Ship safely crossing through the tunnel from Point A to Point B
                    const transitProgress = (time * 0.25) % 1.0;
                    const cargoX = pointAX + (pointBX - pointAX) * transitProgress;
                    const cargoY = pointAY + Math.sin(transitProgress * Math.PI * 2) * 10;

                    ctx.save();
                    ctx.translate(cargoX, cargoY);
                    ctx.rotate(Math.sin(transitProgress * Math.PI) * 0.2);

                    // Cargo Hull
                    ctx.beginPath();
                    ctx.moveTo(12, 0);
                    ctx.lineTo(-10, -6);
                    ctx.lineTo(-6, 0);
                    ctx.lineTo(-10, 6);
                    ctx.closePath();
                    ctx.fillStyle = '#ffffff';
                    ctx.shadowColor = '#00f0ff';
                    ctx.shadowBlur = 15;
                    ctx.fill();
                    ctx.shadowBlur = 0;

                    ctx.fillStyle = '#00f0ff';
                    ctx.font = '9px Orbitron';
                    ctx.textAlign = 'center';
                    ctx.fillText('TRANSIT CARGO SHIP', 0, -18);
                    ctx.restore();

                    // Point A & B Exit Markers
                    [ {x: pointAX, y: pointAY, label: 'ENTRY MOUTH'}, {x: pointBX, y: pointBY, label: 'EXIT MOUTH'} ].forEach(pt => {
                        ctx.beginPath();
                        ctx.arc(pt.x, pt.y, 22, 0, Math.PI * 2);
                        ctx.strokeStyle = 'rgba(255, 171, 0, 0.6)';
                        ctx.lineWidth = 2;
                        ctx.stroke();

                        ctx.fillStyle = '#ffab00';
                        ctx.font = '10px Orbitron';
                        ctx.textAlign = 'center';
                        ctx.fillText(pt.label, pt.x, pt.y - 30);
                    });

                    ctx.restore();
                }

                requestAnimationFrame(animate);
            }

            requestAnimationFrame(animate);
        });
    </script>
</body>
</html>
