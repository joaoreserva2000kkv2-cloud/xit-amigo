<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NexBot - Painel Profissional</title>
    <style>
        /* ─── RESET E BASE ─── */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', 'Gotham', system-ui, -apple-system, sans-serif;
            user-select: none;
        }

        body {
            background: #080808;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 24px;
        }

        /* ─── TEMA PRETO E BRANCO PROFISSIONAL ─── */
        :root {
            --bg-primary: #0c0c0c;
            --bg-secondary: #141414;
            --bg-card: #1e1e1e;
            --bg-input: #262626;
            --border: #2e2e2e;
            --border-light: #3a3a3a;
            --text-primary: #f2f2f2;
            --text-secondary: #b0b0b0;
            --text-muted: #6a6a6a;
            --accent: #ffffff;
            --accent-dim: #cccccc;
            --red: #e74c3c;
            --shadow: 0 20px 60px rgba(0,0,0,0.95);
        }

        /* ─── PAINEL PRINCIPAL ─── */
        .nex-panel {
            width: 680px;
            max-width: 100%;
            background: var(--bg-primary);
            border-radius: 16px;
            border: 1px solid var(--border);
            box-shadow: var(--shadow), 0 0 0 1px rgba(255,255,255,0.03);
            overflow: hidden;
            transition: opacity 0.3s, transform 0.3s;
        }

        /* ─── HEADER ─── */
        .panel-header {
            background: var(--bg-secondary);
            padding: 16px 24px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid var(--border);
        }

        .panel-header .title {
            color: var(--text-primary);
            font-weight: 800;
            font-size: 18px;
            letter-spacing: 0.5px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .panel-header .title .nex {
            color: var(--accent);
        }

        .panel-header .title .bot {
            color: var(--text-secondary);
            font-weight: 300;
        }

        .panel-header .version {
            color: var(--text-muted);
            font-size: 10px;
            font-family: 'Courier New', monospace;
            background: var(--bg-card);
            padding: 4px 14px;
            border-radius: 20px;
            border: 1px solid var(--border);
            letter-spacing: 0.5px;
        }

        /* ─── CORPO: SIDEBAR + CONTEÚDO ─── */
        .panel-body {
            display: flex;
            min-height: 400px;
        }

        /* ─── SIDEBAR ─── */
        .sidebar {
            width: 140px;
            background: var(--bg-secondary);
            padding: 14px 8px;
            border-right: 1px solid var(--border);
            display: flex;
            flex-direction: column;
            gap: 3px;
            flex-shrink: 0;
        }

        .tab-btn {
            background: transparent;
            border: none;
            color: var(--text-muted);
            padding: 10px 14px;
            text-align: left;
            font-size: 12px;
            font-weight: 600;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.15s;
            letter-spacing: 0.3px;
            width: 100%;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .tab-btn:hover {
            background: var(--bg-card);
            color: var(--text-primary);
        }

        .tab-btn.active {
            background: var(--accent);
            color: var(--bg-primary);
            box-shadow: 0 2px 12px rgba(255,255,255,0.08);
        }

        .tab-btn .icon {
            font-size: 14px;
        }

        /* ─── CONTEÚDO ─── */
        .content {
            flex: 1;
            padding: 16px 18px 12px 18px;
            background: var(--bg-primary);
            overflow: hidden;
            min-width: 0;
        }

        .tab-page {
            display: none;
            flex-direction: column;
            gap: 4px;
            height: 100%;
            max-height: 370px;
            overflow-y: auto;
            padding-right: 4px;
        }

        .tab-page.active {
            display: flex;
        }

        .tab-page::-webkit-scrollbar {
            width: 4px;
        }

        .tab-page::-webkit-scrollbar-track {
            background: transparent;
        }

        .tab-page::-webkit-scrollbar-thumb {
            background: var(--border);
            border-radius: 10px;
        }

        /* ─── WIDGETS ─── */
        .widget-row {
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 6px 4px;
            border-bottom: 1px solid rgba(255,255,255,0.03);
            min-height: 34px;
            gap: 6px;
        }

        .widget-row.label-only {
            border-bottom: none;
            padding: 4px 4px 8px 4px;
        }

        .widget-label {
            color: var(--text-primary);
            font-size: 12px;
            font-weight: 500;
            letter-spacing: 0.2px;
            white-space: nowrap;
        }

        .widget-label small {
            color: var(--text-muted);
            font-weight: 400;
            font-size: 9px;
            margin-left: 4px;
        }

        .widget-value {
            color: var(--accent);
            font-size: 11px;
            font-weight: 600;
            font-family: 'Courier New', monospace;
            min-width: 32px;
            text-align: right;
        }

        .flex {
            display: flex;
            align-items: center;
            gap: 8px;
        }
        .flex-1 { flex: 1; }
        .gap-1 { gap: 4px; }
        .w-full { width: 100%; }
        .justify-between { justify-content: space-between; }
        .ml-auto { margin-left: auto; }

        /* ─── TOGGLE (INTERRUPTOR) ─── */
        .toggle-track {
            width: 40px;
            height: 22px;
            background: var(--bg-input);
            border-radius: 40px;
            cursor: pointer;
            position: relative;
            transition: 0.2s;
            border: 1px solid var(--border);
            flex-shrink: 0;
        }

        .toggle-track.active {
            background: var(--accent);
            border-color: var(--accent);
        }

        .toggle-knob {
            width: 16px;
            height: 16px;
            background: #ffffff;
            border-radius: 50%;
            position: absolute;
            top: 2px;
            left: 2px;
            transition: 0.2s cubic-bezier(0.34, 1.56, 0.64, 1);
            box-shadow: 0 1px 4px rgba(0,0,0,0.4);
        }

        .toggle-track.active .toggle-knob {
            left: 20px;
            background: var(--bg-primary);
        }

        /* ─── SLIDER ─── */
        .slider-container {
            display: flex;
            align-items: center;
            gap: 10px;
            flex: 1;
            margin-left: 4px;
        }

        .slider-track {
            flex: 1;
            height: 4px;
            background: var(--bg-input);
            border-radius: 10px;
            position: relative;
            cursor: pointer;
            min-width: 40px;
        }

        .slider-fill {
            height: 100%;
            background: var(--accent);
            border-radius: 10px;
            width: 50%;
            transition: 0.05s;
        }

        .slider-value {
            color: var(--accent);
            font-size: 11px;
            font-weight: 600;
            min-width: 34px;
            text-align: right;
            font-family: 'Courier New', monospace;
        }

        /* ─── CYCLE BUTTON ─── */
        .cycle-btn {
            background: var(--bg-card);
            border: 1px solid var(--border);
            color: var(--text-primary);
            padding: 4px 16px;
            border-radius: 20px;
            font-size: 11px;
            font-weight: 600;
            cursor: pointer;
            transition: 0.15s;
            letter-spacing: 0.3px;
            font-family: 'Courier New', monospace;
        }

        .cycle-btn:hover {
            border-color: var(--accent);
            color: var(--accent);
            background: var(--bg-input);
        }

        /* ─── KEYBIND ─── */
        .keybind-btn {
            background: var(--bg-card);
            border: 1px solid var(--border);
            color: var(--accent);
            padding: 3px 14px;
            border-radius: 16px;
            font-size: 10px;
            font-family: 'Courier New', monospace;
            font-weight: 700;
            cursor: pointer;
            transition: 0.15s;
            min-width: 56px;
            text-align: center;
            letter-spacing: 0.5px;
        }

        .keybind-btn:hover {
            border-color: var(--accent);
            background: var(--bg-input);
        }

        .keybind-btn.recording {
            border-color: var(--accent);
            background: var(--bg-input);
            color: #fff;
            animation: pulse 0.9s infinite;
        }

        @keyframes pulse {
            0%, 100% { opacity: 0.5; }
            50% { opacity: 1; }
        }

        /* ─── ACTION BUTTON ─── */
        .action-btn {
            background: var(--bg-card);
            border: 1px solid var(--border);
            color: var(--text-primary);
            padding: 7px 14px;
            border-radius: 8px;
            font-size: 11px;
            font-weight: 600;
            cursor: pointer;
            transition: 0.15s;
            width: 100%;
            text-align: center;
            letter-spacing: 0.3px;
        }

        .action-btn:hover {
            border-color: var(--accent);
            color: var(--accent);
        }

        .action-btn.danger {
            border-color: #3a1a1a;
            color: var(--red);
        }

        .action-btn.danger:hover {
            border-color: var(--red);
            background: #1a0a0a;
        }

        .action-btn.success {
            border-color: #1a3a1a;
            color: #7fff7f;
        }

        .action-btn.success:hover {
            border-color: #7fff7f;
            background: #0a1a0a;
        }

        /* ─── STATUS BAR ─── */
        .status-bar {
            background: var(--bg-secondary);
            padding: 7px 20px;
            display: flex;
            justify-content: space-between;
            border-top: 1px solid var(--border);
            font-size: 10px;
            color: var(--text-muted);
            font-family: 'Courier New', monospace;
            letter-spacing: 0.2px;
        }

        .status-bar .status {
            color: var(--text-secondary);
            transition: 0.2s;
        }

        .status-bar .status.active {
            color: var(--accent);
            font-weight: 600;
        }

        .status-bar .hint {
            color: var(--text-muted);
        }

        /* ─── RESPONSIVO ─── */
        @media (max-width: 700px) {
            .nex-panel { width: 100%; }
            .panel-body { flex-direction: column; }
            .sidebar {
                width: 100%;
                flex-direction: row;
                flex-wrap: wrap;
                border-right: none;
                border-bottom: 1px solid var(--border);
                padding: 8px 10px;
                gap: 2px;
            }
            .tab-btn {
                flex: 1;
                text-align: center;
                padding: 6px 6px;
                font-size: 10px;
                min-width: 50px;
                justify-content: center;
            }
            .tab-btn .icon { font-size: 12px; }
            .content { padding: 12px; }
            .panel-header .title { font-size: 15px; }
            .widget-label { font-size: 11px; }
        }

        @media (max-width: 480px) {
            .widget-row { flex-wrap: wrap; gap: 4px; }
            .slider-container { min-width: 100px; }
            .widget-label { font-size: 10px; }
        }
    </style>
</head>
<body>

<div class="nex-panel" id="nexPanel">
    <!-- HEADER -->
    <div class="panel-header">
        <div class="title">
            <span class="nex">NEX</span><span class="bot">BOT</span>
            <span style="font-weight:300;font-size:10px;color:var(--text-muted);margin-left:2px;">v2.0</span>
        </div>
        <div class="version">PROFESSIONAL</div>
    </div>

    <!-- BODY -->
    <div class="panel-body">
        <!-- SIDEBAR -->
        <div class="sidebar" id="sidebar">
            <button class="tab-btn active" data-tab="combat"><span class="icon">⚔️</span> Combat</button>
            <button class="tab-btn" data-tab="movement"><span class="icon">🏃</span> Movement</button>
            <button class="tab-btn" data-tab="render"><span class="icon">🖥️</span> Render</button>
            <button class="tab-btn" data-tab="player"><span class="icon">🧑</span> Player</button>
            <button class="tab-btn" data-tab="weapon"><span class="icon">🔫</span> Weapon</button>
            <button class="tab-btn" data-tab="misc"><span class="icon">⚙️</span> Misc</button>
        </div>

        <!-- CONTENT -->
        <div class="content">
            <!-- ===== COMBAT ===== -->
            <div class="tab-page active" id="page-combat">
                <div class="widget-row"><span class="widget-label">KillAura</span><div class="toggle-track active" data-toggle="killaura"><div class="toggle-knob"></div></div></div>
                <div class="widget-row"><span class="widget-label">Anti-Wallbang</span><div class="toggle-track" data-toggle="antiwall"><div class="toggle-knob"></div></div></div>
                <div class="widget-row"><span class="widget-label">Skip Teammates</span><div class="toggle-track active" data-toggle="skipteam"><div class="toggle-knob"></div></div></div>
                <div class="widget-row"><span class="widget-label">Auto Reload</span><div class="toggle-track active" data-toggle="autoreload"><div class="toggle-knob"></div></div></div>
                <div class="widget-row"><span class="widget-label">Skip ForceField</span><div class="toggle-track" data-toggle="skipff"><div class="toggle-knob"></div></div></div>
                <div class="widget-row"><span class="widget-label">Only Nearest</span><div class="toggle-track" data-toggle="nearest"><div class="toggle-knob"></div></div></div>
                <div class="widget-row"><span class="widget-label">FOV Check</span><div class="toggle-track active" data-toggle="fovcheck"><div class="toggle-knob"></div></div></div>
                <div class="widget-row"><span class="widget-label">FOV</span><div class="slider-container"><div class="slider-track" data-slider="fov"><div class="slider-fill" style="width:50%"></div></div><span class="slider-value">180</span></div></div>
                <div class="widget-row"><span class="widget-label">Max Distance</span><div class="slider-container"><div class="slider-track" data-slider="maxdist"><div class="slider-fill" style="width:60%"></div></div><span class="slider-value">300</span></div></div>
                <div class="widget-row"><span class="widget-label">Ammo</span><div class="slider-container"><div class="slider-track" data-slider="ammo"><div class="slider-fill" style="width:26%"></div></div><span class="slider-value">13</span></div></div>
                <div class="widget-row"><span class="widget-label">Fire Delay (ms)</span><div class="slider-container"><div class="slider-track" data-slider="firedelay"><div class="slider-fill" style="width:10%"></div></div><span class="slider-value">10</span></div></div>
                <div class="widget-row"><span class="widget-label">AWB Delay (ms)</span><div class="slider-container"><div class="slider-track" data-slider="awbdelay"><div class="slider-fill" style="width:30%"></div></div><span class="slider-value">150</span></div></div>
                <div class="widget-row"><span class="widget-label">Shot Delay (ms)</span><div class="slider-container"><div class="slider-track" data-slider="shotdelay"><div class="slider-fill" style="width:8%"></div></div><span class="slider-value">10</span></div></div>
                <div class="widget-row"><span class="widget-label">Jitter Amount</span><div class="slider-container"><div class="slider-track" data-slider="jitteramt"><div class="slider-fill" style="width:20%"></div></div><span class="slider-value">0.02</span></div></div>
                <div class="widget-row"><span class="widget-label">Min Shot Interval</span><div class="slider-container"><div class="slider-track" data-slider="minshot"><div class="slider-fill" style="width:12%"></div></div><span class="slider-value">0.12</span></div></div>
            </div>

            <!-- ===== MOVEMENT ===== -->
            <div class="tab-page" id="page-movement">
                <div class="widget-row"><span class="widget-label">Bunny Hop</span><div class="toggle-track" data-toggle="bhop"><div class="toggle-knob"></div></div></div>
                <div class="widget-row"><span class="widget-label">Max Speed</span><div class="slider-container"><div class="slider-track" data-slider="bhopmax"><div class="slider-fill" style="width:44%"></div></div><span class="slider-value">35</span></div></div>
                <div class="widget-row"><span class="widget-label">Acceleration</span><div class="slider-container"><div class="slider-track" data-slider="bhopaccel"><div class="slider-fill" style="width:20%"></div></div><span class="slider-value">1.0</span></div></div>
                <div class="widget-row"><span class="widget-label">Strafe</span><div class="slider-container"><div class="slider-track" data-slider="bhopstrafe"><div class="slider-fill" style="width:40%"></div></div><span class="slider-value">1.2</span></div></div>
                <div class="widget-row"><span class="widget-label">Jump Distance</span><div class="slider-container"><div class="slider-track" data-slider="bhopjump"><div class="slider-fill" style="width:30%"></div></div><span class="slider-value">20</span></div></div>
                <div class="widget-row"><span class="widget-label">Friction</span><div class="slider-container"><div class="slider-track" data-slider="bhopfriction"><div class="slider-fill" style="width:85%"></div></div><span class="slider-value">0.85</span></div></div>
                <div class="widget-row"><span class="widget-label">Gain</span><div class="slider-container"><div class="slider-track" data-slider="bhopgain"><div class="slider-fill" style="width:80%"></div></div><span class="slider-value">0.8</span></div></div>
                <div class="widget-row"><span class="widget-label">Start Speed</span><div class="slider-container"><div class="slider-track" data-slider="bhopstart"><div class="slider-fill" style="width:20%"></div></div><span class="slider-value">16</span></div></div>
                <div class="widget-row"><span class="widget-label">Velocity</span><div class="slider-container"><div class="slider-track" data-slider="bhopvel"><div class="slider-fill" style="width:50%"></div></div><span class="slider-value">25</span></div></div>
            </div>

            <!-- ===== RENDER ===== -->
            <div class="tab-page" id="page-render">
                <div class="widget-row"><span class="widget-label">ESP</span><div class="toggle-track" data-toggle="esp"><div class="toggle-knob"></div></div></div>
                <div class="widget-row"><span class="widget-label">FP Camera</span><div class="toggle-track" data-toggle="fpcam"><div class="toggle-knob"></div></div></div>
                <div class="widget-row"><span class="widget-label">Cam Noclip</span><div class="toggle-track" data-toggle="camnoclip"><div class="toggle-knob"></div></div></div>
                <div class="widget-row"><span class="widget-label">ESP Distance</span><div class="slider-container"><div class="slider-track" data-slider="espdist"><div class="slider-fill" style="width:50%"></div></div><span class="slider-value">400</span></div></div>
                <div class="widget-row"><span class="widget-label">FP Sensitivity</span><div class="slider-container"><div class="slider-track" data-slider="fpsens"><div class="slider-fill" style="width:35%"></div></div><span class="slider-value">0.35</span></div></div>
                <div class="widget-row"><span class="widget-label">FP Pitch Min</span><div class="slider-container"><div class="slider-track" data-slider="fppitchmin"><div class="slider-fill" style="width:0%"></div></div><span class="slider-value">-85</span></div></div>
                <div class="widget-row"><span class="widget-label">FP Pitch Max</span><div class="slider-container"><div class="slider-track" data-slider="fppitchmax"><div class="slider-fill" style="width:85%"></div></div><span class="slider-value">85</span></div></div>
                <div class="widget-row"><span class="widget-label">LOS X Spread</span><div class="slider-container"><div class="slider-track" data-slider="losx"><div class="slider-fill" style="width:90%"></div></div><span class="slider-value">0.9</span></div></div>
                <div class="widget-row"><span class="widget-label">LOS Y Spread</span><div class="slider-container"><div class="slider-track" data-slider="losy"><div class="slider-fill" style="width:80%"></div></div><span class="slider-value">1.6</span></div></div>
                <div class="widget-row"><span class="widget-label">AFK Speed</span><div class="slider-container"><div class="slider-track" data-slider="afkspeed"><div class="slider-fill" style="width:12%"></div></div><span class="slider-value">1.2</span></div></div>
            </div>

            <!-- ===== PLAYER ===== -->
            <div class="tab-page" id="page-player">
                <div class="widget-row"><span class="widget-label">Anti-Aim</span><button class="cycle-btn" data-cycle="aa">SPIN</button></div>
                <div class="widget-row"><span class="widget-label">Emote AA</span><div class="toggle-track" data-toggle="emoteaa"><div class="toggle-knob"></div></div></div>
                <div class="widget-row"><span class="widget-label">AA Speed</span><div class="slider-container"><div class="slider-track" data-slider="aaspeed"><div class="slider-fill" style="width:37%"></div></div><span class="slider-value">22</span></div></div>
                <div class="widget-row"><span class="widget-label">AA Jitter</span><div class="slider-container"><div class="slider-track" data-slider="aajitter"><div class="slider-fill" style="width:39%"></div></div><span class="slider-value">70</span></div></div>
                <div class="widget-row"><span class="widget-label">AA Sway</span><div class="slider-container"><div class="slider-track" data-slider="aasway"><div class="slider-fill" style="width:39%"></div></div><span class="slider-value">35</span></div></div>
                <div class="widget-row"><span class="widget-label">Emote Speed</span><div class="slider-container"><div class="slider-track" data-slider="emotespeed"><div class="slider-fill" style="width:10%"></div></div><span class="slider-value">1.0</span></div></div>
                <div class="widget-row"><span class="widget-label">AA Emote ID</span><div style="flex:1;text-align:right;color:var(--text-muted);font-size:10px;font-family:monospace;">121890511737627</div></div>
            </div>

            <!-- ===== WEAPON ===== -->
            <div class="tab-page" id="page-weapon">
                <div class="widget-row"><span class="widget-label">Minecraft Sword</span><div class="toggle-track active" data-toggle="sword"><div class="toggle-knob"></div></div></div>
                <div class="widget-row"><span class="widget-label">VM X</span><div class="slider-container"><div class="slider-track" data-slider="vmx"><div class="slider-fill" style="width:64%"></div></div><span class="slider-value">2.7</span></div></div>
                <div class="widget-row"><span class="widget-label">VM Y</span><div class="slider-container"><div class="slider-track" data-slider="vmy"><div class="slider-fill" style="width:48%"></div></div><span class="slider-value">-0.3</span></div></div>
                <div class="widget-row"><span class="widget-label">VM Z</span><div class="slider-container"><div class="slider-track" data-slider="vmz"><div class="slider-fill" style="width:20%"></div></div><span class="slider-value">-6.3</span></div></div>
                <div class="widget-row"><span class="widget-label">VM RX</span><div class="slider-container"><div class="slider-track" data-slider="vmrx"><div class="slider-fill" style="width:78%"></div></div><span class="slider-value">100</span></div></div>
                <div class="widget-row"><span class="widget-label">VM RY</span><div class="slider-container"><div class="slider-track" data-slider="vmry"><div class="slider-fill" style="width:69%"></div></div><span class="slider-value">250</span></div></div>
                <div class="widget-row"><span class="widget-label">VM RZ</span><div class="slider-container"><div class="slider-track" data-slider="vmrz"><div class="slider-fill" style="width:50%"></div></div><span class="slider-value">0</span></div></div>
                <div class="widget-row"><span class="widget-label">VM Pivot Y</span><div class="slider-container"><div class="slider-track" data-slider="vmpivot"><div class="slider-fill" style="width:50%"></div></div><span class="slider-value">0.0</span></div></div>
                <div class="widget-row"><span class="widget-label">Swing Pivot X</span><div class="slider-container"><div class="slider-track" data-slider="swingx"><div class="slider-fill" style="width:50%"></div></div><span class="slider-value">0</span></div></div>
                <div class="widget-row"><span class="widget-label">Swing Pivot Y</span><div class="slider-container"><div class="slider-track" data-slider="swingy"><div class="slider-fill" style="width:50%"></div></div><span class="slider-value">0</span></div></div>
                <div class="widget-row"><span class="widget-label">Swing Pivot Z</span><div class="slider-container"><div class="slider-track" data-slider="swingz"><div class="slider-fill" style="width:20%"></div></div><span class="slider-value">-0.8</span></div></div>
                <div class="widget-row"><span class="widget-label">Swing Dir</span><div class="slider-container"><div class="slider-track" data-slider="swingdir"><div class="slider-fill" style="width:50%"></div></div><span class="slider-value">-1</span></div></div>
                <div class="widget-row label-only"><button class="action-btn" id="testSwing">🔁 TEST SWING</button></div>
            </div>

            <!-- ===== MISC ===== -->
            <div class="tab-page" id="page-misc">
                <div class="widget-row"><span class="widget-label">KillAura</span><button class="keybind-btn" data-keybind="killaura">Y</button></div>
                <div class="widget-row"><span class="widget-label">ESP</span><button class="keybind-btn" data-keybind="esp">N</button></div>
                <div class="widget-row"><span class="widget-label">Jitter</span><button class="keybind-btn" data-keybind="jitter">G</button></div>
                <div class="widget-row"><span class="widget-label">Bhop</span><button class="keybind-btn" data-keybind="bhop">B</button></div>
                <div class="widget-row"><span class="widget-label">FP</span><button class="keybind-btn" data-keybind="fp">F</button></div>
                <div class="widget-row"><span class="widget-label">Reload</span><button class="keybind-btn" data-keybind="reload">R</button></div>
                <div class="widget-row"><span class="widget-label">EmoteAA</span><button class="keybind-btn" data-keybind="emoteaa">U</button></div>
                <div class="widget-row"><span class="widget-label">CamNoclip</span><button class="keybind-btn" data-keybind="camnoclip">V</button></div>
                <div class="widget-row"><span class="widget-label">ToggleGUI</span><button class="keybind-btn" data-keybind="togglegui">\</button></div>
                <div class="widget-row label-only" style="margin-top:4px;"><button class="action-btn success" id="saveConfig">💾 SAVE CONFIG</button></div>
                <div class="widget-row label-only"><button class="action-btn danger" id="destroyPanel">⛔ DESTROY</button></div>
                <div class="widget-row label-only" style="border-bottom:none;padding-top:4px;">
                    <span style="color:var(--text-muted);font-size:9px;font-family:monospace;">NexBot · Made By Uriel · Preto & Branco</span>
                </div>
            </div>
        </div>
    </div>

    <!-- STATUS BAR -->
    <div class="status-bar">
        <span class="status" id="statusIndicator">● IDLE</span>
        <span class="hint">NexBot · \\ to toggle GUI</span>
    </div>
</div>

<script>
    (function() {
        "use strict";

        // ─── ESTADO SIMULADO ───
        const state = {
            killaura: true,
            antiwall: false,
            skipteam: true,
            autoreload: true,
            skipff: false,
            nearest: false,
            fovcheck: true,
            fov: 180,
            maxdist: 300,
            ammo: 13,
            firedelay: 10,
            awbdelay: 150,
            shotdelay: 10,
            jitteramt: 0.02,
            minshot: 0.12,
            bhop: false,
            bhopmax: 35,
            bhopaccel: 1.0,
            bhopstrafe: 1.2,
            bhopjump: 20,
            bhopfriction: 0.85,
            bhopgain: 0.8,
            bhopstart: 16,
            bhopvel: 25,
            esp: false,
            fpcam: false,
            camnoclip: false,
            espdist: 400,
            fpsens: 0.35,
            fppitchmin: -85,
            fppitchmax: 85,
            losx: 0.9,
            losy: 1.6,
            afkspeed: 1.2,
            aa: 'SPIN',
            emoteaa: false,
            aaspeed: 22,
            aajitter: 70,
            aasway: 35,
            emotespeed: 1.0,
            sword: true,
            vmx: 2.7,
            vmy: -0.3,
            vmz: -6.3,
            vmrx: 100,
            vmry: 250,
            vmrz: 0,
            vmpivot: 0.0,
            swingx: 0,
            swingy: 0,
            swingz: -0.8,
            swingdir: -1,
        };

        const aaOptions = ['OFF', 'SPIN', 'JITTER', 'INVERT', 'RANDOM', 'SWAY'];
        let aaIndex = 1;

        // ─── DOM REFS ───
        const tabs = document.querySelectorAll('.tab-btn');
        const pages = {
            combat: document.getElementById('page-combat'),
            movement: document.getElementById('page-movement'),
            render: document.getElementById('page-render'),
            player: document.getElementById('page-player'),
            weapon: document.getElementById('page-weapon'),
            misc: document.getElementById('page-misc')
        };
        const statusEl = document.getElementById('statusIndicator');

        // ─── HELPERS ───
        function updateStatus(text, active = false) {
            if (statusEl) {
                statusEl.textContent = text;
                statusEl.className = 'status' + (active ? ' active' : '');
            }
        }

        function clamp(v, min, max) { return Math.max(min, Math.min(max, v)); }

        // ─── TABS ───
        tabs.forEach(btn => {
            btn.addEventListener('click', function() {
                const tab = this.dataset.tab;
                tabs.forEach(b => b.classList.remove('active'));
                this.classList.add('active');
                Object.keys(pages).forEach(key => {
                    pages[key].classList.toggle('active', key === tab);
                });
            });
        });

        // ─── TOGGLES ───
        document.querySelectorAll('.toggle-track').forEach(track => {
            track.addEventListener('click', function(e) {
                e.stopPropagation();
                this.classList.toggle('active');
                const key = this.dataset.toggle;
                if (key) {
                    const val = this.classList.contains('active');
                    state[key] = val;
                    updateStatus(`● ${key.toUpperCase()} ${val ? 'ON' : 'OFF'}`, val);
                    if (key === 'killaura') {
                        updateStatus(val ? '● ACTIVE' : '● IDLE', val);
                    }
                }
            });
        });

        // ─── SLIDERS ───
        document.querySelectorAll('.slider-track').forEach(track => {
            const valueEl = track.parentElement.querySelector('.slider-value');
            const fill = track.querySelector('.slider-fill');
            const key = track.dataset.slider;

            function getConfig(key) {
                const map = {
                    fov: { min: 30, max: 360, step: 5, decimals: 0 },
                    maxdist: { min: 50, max: 600, step: 10, decimals: 0 },
                    ammo: { min: 1, max: 50, step: 1, decimals: 0 },
                    firedelay: { min: 1, max: 300, step: 1, decimals: 0 },
                    awbdelay: { min: 0, max: 500, step: 10, decimals: 0 },
                    shotdelay: { min: 1, max: 200, step: 1, decimals: 0 },
                    jitteramt: { min: 0, max: 0.1, step: 0.005, decimals: 3 },
                    minshot: { min: 0.01, max: 0.5, step: 0.01, decimals: 2 },
                    bhopmax: { min: 10, max: 80, step: 1, decimals: 0 },
                    bhopaccel: { min: 0.1, max: 5, step: 0.1, decimals: 1 },
                    bhopstrafe: { min: 0.2, max: 3, step: 0.1, decimals: 1 },
                    bhopjump: { min: 5, max: 50, step: 1, decimals: 0 },
                    bhopfriction: { min: 0.1, max: 1, step: 0.05, decimals: 2 },
                    bhopgain: { min: 0.1, max: 2, step: 0.1, decimals: 1 },
                    bhopstart: { min: 1, max: 40, step: 1, decimals: 0 },
                    bhopvel: { min: 5, max: 60, step: 1, decimals: 0 },
                    espdist: { min: 50, max: 800, step: 10, decimals: 0 },
                    fpsens: { min: 0.05, max: 1.0, step: 0.05, decimals: 2 },
                    fppitchmin: { min: -90, max: 0, step: 1, decimals: 0 },
                    fppitchmax: { min: 0, max: 90, step: 1, decimals: 0 },
                    losx: { min: 0.1, max: 3, step: 0.1, decimals: 1 },
                    losy: { min: 0.1, max: 4, step: 0.1, decimals: 1 },
                    afkspeed: { min: 0.1, max: 5, step: 0.1, decimals: 1 },
                    aaspeed: { min: 5, max: 60, step: 1, decimals: 0 },
                    aajitter: { min: 10, max: 180, step: 5, decimals: 0 },
                    aasway: { min: 5, max: 90, step: 5, decimals: 0 },
                    emotespeed: { min: 1, max: 10, step: 1, decimals: 0 },
                    vmx: { min: -10, max: 10, step: 0.1, decimals: 1 },
                    vmy: { min: -10, max: 10, step: 0.1, decimals: 1 },
                    vmz: { min: -15, max: 5, step: 0.1, decimals: 1 },
                    vmrx: { min: -180, max: 180, step: 5, decimals: 0 },
                    vmry: { min: -180, max: 360, step: 5, decimals: 0 },
                    vmrz: { min: -180, max: 180, step: 5, decimals: 0 },
                    vmpivot: { min: -5, max: 5, step: 0.1, decimals: 1 },
                    swingx: { min: -5, max: 5, step: 0.1, decimals: 1 },
                    swingy: { min: -5, max: 5, step: 0.1, decimals: 1 },
                    swingz: { min: -5, max: 5, step: 0.1, decimals: 1 },
                    swingdir: { min: -3, max: 3, step: 1, decimals: 0 },
                };
                return map[key] || { min: 0, max: 100, step: 1, decimals: 0 };
            }

            function updateSlider(clientX) {
                const rect = track.getBoundingClientRect();
                let x = (clientX - rect.left) / rect.width;
                x = clamp(x, 0, 1);
                fill.style.width = (x * 100) + '%';

                const cfg = getConfig(key);
                let val = cfg.min + x * (cfg.max - cfg.min);
                val = Math.round(val / cfg.step) * cfg.step;
                val = clamp(val, cfg.min, cfg.max);
                if (cfg.decimals === 0) val = Math.round(val);
                else val = Number(val.toFixed(cfg.decimals));

                if (valueEl) {
                    let display = val;
                    if (cfg.decimals === 0) display = Math.round(val);
                    else if (cfg.decimals === 1) display = val.toFixed(1);
                    else if (cfg.decimals === 2) display = val.toFixed(2);
                    else if (cfg.decimals === 3) display = val.toFixed(3);
                    valueEl.textContent = display;
                }
                if (key) state[key] = val;
            }

            track.addEventListener('mousedown', function(e) {
                e.preventDefault();
                updateSlider(e.clientX);
                const onMove = (ev) => updateSlider(ev.clientX);
                const onUp = () => {
                    document.removeEventListener('mousemove', onMove);
                    document.removeEventListener('mouseup', onUp);
                };
                document.addEventListener('mousemove', onMove);
                document.addEventListener('mouseup', onUp);
            });
        });

        // ─── CYCLE (ANTI-AIM) ───
        const cycleBtn = document.querySelector('[data-cycle="aa"]');
        if (cycleBtn) {
            cycleBtn.addEventListener('click', function() {
                aaIndex = (aaIndex + 1) % aaOptions.length;
                this.textContent = aaOptions[aaIndex];
                state.aa = aaOptions[aaIndex];
                updateStatus(`● AA: ${aaOptions[aaIndex]}`, true);
            });
        }

        // ─── KEYBINDS ───
        document.querySelectorAll('.keybind-btn').forEach(btn => {
            btn.addEventListener('click', function() {
                if (this.classList.contains('recording')) {
                    this.classList.remove('recording');
                    this.textContent = this.dataset.original || '?';
                    return;
                }
                this.dataset.original = this.textContent;
                this.classList.add('recording');
                this.textContent = '...';

                const self = this;
                let timeout = setTimeout(() => {
                    self.classList.remove('recording');
                    self.textContent = self.dataset.original || '?';
                }, 3000);

                const handler = (e) => {
                    if (e.key) {
                        const key = e.key.toUpperCase();
                        self.textContent = key;
                        self.classList.remove('recording');
                        clearTimeout(timeout);
                        document.removeEventListener('keydown', handler);
                        const action = self.dataset.keybind;
                        if (action) {
                            updateStatus(`● ${action} bind → ${key}`, true);
                        }
                    }
                };
                document.addEventListener('keydown', handler);

                const cancel = () => {
                    if (self.classList.contains('recording')) {
                        self.classList.remove('recording');
                        self.textContent = self.dataset.original || '?';
                        clearTimeout(timeout);
                        document.removeEventListener('keydown', handler);
                    }
                };
                self.addEventListener('click', cancel, { once: true });
                self._cleanup = cancel;
            });
        });

        // ─── AÇÕES ───
        document.getElementById('testSwing')?.addEventListener('click', function() {
            updateStatus('● SWING!', true);
            setTimeout(() => updateStatus('● IDLE', false), 800);
        });

        document.getElementById('saveConfig')?.addEventListener('click', function() {
            updateStatus('● CONFIG SAVED ✓', true);
            setTimeout(() => updateStatus('● IDLE', false), 1200);
        });

        document.getElementById('destroyPanel')?.addEventListener('click', function() {
            if (confirm('Destroy NexBot panel?')) {
                const panel = document.getElementById('nexPanel');
                if (panel) {
                    panel.style.transition = 'opacity 0.3s, transform 0.3s';
                    panel.style.opacity = '0';
                    panel.style.transform = 'scale(0.95)';
                    setTimeout(() => {
                        panel.style.display = 'none';
                        document.body.innerHTML = `
                            <div style="color:#f0f0f0;text-align:center;padding:60px 20px;font-family:monospace;background:#0a0a0a;min-height:100vh;display:flex;align-items:center;justify-content:center;flex-direction:column;gap:14px;">
                                <span style="font-size:28px;color:#fff;font-weight:700;">⛔ NEXBOT DESTROYED</span>
                                <span style="color:#666;font-size:14px;">Recarregue a página para reiniciar o painel</span>
                                <button onclick="location.reload()" style="margin-top:12px;background:#1e1e1e;border:1px solid #3a3a3a;color:#fff;padding:10px 28px;border-radius:8px;cursor:pointer;font-size:13px;font-weight:600;">↻ RECARREGAR</button>
                            </div>
                        `;
                    }, 350);
                }
            }
        });

        // ─── STATUS INICIAL ───
        updateStatus('● IDLE', false);

        // Sincroniza toggles com estado
        document.querySelectorAll('.toggle-track').forEach(t => {
            const key = t.dataset.toggle;
            if (key && state[key] !== undefined) {
                t.classList.toggle('active', !!state[key]);
            }
        });

        // KillAura ativo por padrão
        const kaToggle = document.querySelector('[data-toggle="killaura"]');
        if (kaToggle && state.killaura) {
            kaToggle.classList.add('active');
            updateStatus('● ACTIVE', true);
        }

        console.log('✅ NexBot Painel Profissional (Preto & Branco) carregado.');
    })();
</script>

</body>
</html>
