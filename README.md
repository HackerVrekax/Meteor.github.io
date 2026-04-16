<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>Meteor Script | 3D Panels & Advanced Roblox Lua Script</title>
    <meta name="description" content="Meteor is a powerful Lua script for Roblox with a stunning 3D UI. Features ESP, admin commands, auto-farm, and smooth 3D interactive panels.">
    <meta name="keywords" content="Roblox script, Meteor, Lua script, 3D panels, Roblox hack, script hub, executor script">
    <meta name="author" content="Meteor Dev">
    <!-- Fonts & Icons -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:opsz,wght@14..32,300;400;500;600;700;800&family=Space+Grotesk:wght@400;500;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Inter', 'Space Grotesk', sans-serif;
            background: #0A0A0F;
            color: #E0E0E0;
            line-height: 1.5;
            scroll-behavior: smooth;
            overflow-x: hidden;
            min-height: 100vh;
        }

        /* Dynamic gradient background */
        .bg-gradient {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -2;
            background: radial-gradient(circle at 30% 10%, #0f0c29, #02020a, #000000);
        }

        /* Animated stars */
        .stars {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            pointer-events: none;
            background-image: 
                radial-gradient(2px 2px at 15px 40px, #fff, rgba(0,0,0,0)),
                radial-gradient(1px 1px at 80px 160px, #f0f0f0, rgba(0,0,0,0)),
                radial-gradient(2px 2px at 300px 500px, #ffdd99, rgba(0,0,0,0)),
                radial-gradient(1px 1px at 700px 200px, #fff, rgba(0,0,0,0));
            background-repeat: no-repeat;
            background-size: 300px 300px, 400px 400px, 500px 500px, 600px 600px;
            animation: floatStars 20s infinite alternate;
            opacity: 0.6;
        }

        @keyframes floatStars {
            0% { transform: translateY(0px); opacity: 0.4; }
            100% { transform: translateY(30px); opacity: 0.9; }
        }

        ::-webkit-scrollbar { width: 8px; }
        ::-webkit-scrollbar-track { background: #1E1E2F; }
        ::-webkit-scrollbar-thumb { background: #FF3D7A; border-radius: 10px; }

        .container {
            max-width: 1300px;
            margin: 0 auto;
            padding: 0 30px;
            position: relative;
            z-index: 2;
        }

        /* Navigation - flat but clean */
        nav {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 25px 0;
            flex-wrap: wrap;
            gap: 20px;
            border-bottom: 1px solid rgba(255,61,122,0.3);
            backdrop-filter: blur(10px);
        }

        .logo {
            font-size: 2rem;
            font-weight: 800;
            background: linear-gradient(135deg, #FF3D7A, #FFB347);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }

        .logo i {
            background: none;
            color: #FF3D7A;
            margin-right: 8px;
        }

        .nav-links {
            display: flex;
            gap: 35px;
            list-style: none;
        }

        .nav-links a {
            text-decoration: none;
            color: #C0C0D0;
            font-weight: 500;
            transition: 0.3s;
        }

        .nav-links a:hover { color: #FF3D7A; text-shadow: 0 0 8px #FF3D7A; }

        .btn-primary {
            background: linear-gradient(95deg, #FF3D7A, #FFB347);
            border: none;
            padding: 12px 28px;
            border-radius: 40px;
            font-weight: 700;
            color: white;
            cursor: pointer;
            transition: 0.2s;
            box-shadow: 0 4px 15px rgba(255,61,122,0.4);
        }
        .btn-primary:hover { transform: scale(1.05); }

        /* ========== 3D PANEL STYLES ========== */
        .panel-3d {
            background: rgba(25, 25, 45, 0.65);
            backdrop-filter: blur(12px);
            border-radius: 32px;
            padding: 28px 24px;
            border: 1px solid rgba(255, 61, 122, 0.25);
            transition: all 0.2s ease;
            transform-style: preserve-3d;
            will-change: transform;
            box-shadow: 0 20px 35px -15px rgba(0,0,0,0.5);
        }

        /* Hover 3D effect will be applied via JS */
        .hero-3d-card {
            background: linear-gradient(135deg, rgba(255,61,122,0.15), rgba(255,180,71,0.1));
            border-radius: 48px;
            padding: 40px;
            transform-style: preserve-3d;
            transition: transform 0.1s ease;
            will-change: transform;
            border: 1px solid rgba(255,61,122,0.4);
        }

        .feature-card-3d {
            background: rgba(20, 20, 35, 0.7);
            backdrop-filter: blur(10px);
            border-radius: 28px;
            padding: 30px 24px;
            transform-style: preserve-3d;
            transition: transform 0.1s ease;
            will-change: transform;
            border: 1px solid rgba(255,61,122,0.2);
            cursor: default;
        }

        .download-panel-3d {
            background: radial-gradient(circle at 20% 30%, rgba(255,61,122,0.2), rgba(0,0,0,0.6));
            border-radius: 48px;
            padding: 50px 30px;
            transform-style: preserve-3d;
            transition: transform 0.1s ease;
            will-change: transform;
            backdrop-filter: blur(8px);
            border: 1px solid rgba(255,61,122,0.4);
        }

        /* Grid for features */
        .features-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 35px;
            margin: 50px 0;
        }

        .hero {
            display: flex;
            align-items: center;
            justify-content: space-between;
            flex-wrap: wrap;
            gap: 50px;
            margin: 60px 0 40px;
        }

        .hero-content { flex: 1; min-width: 280px; }
        .hero-content h1 {
            font-size: 3.8rem;
            font-weight: 800;
            background: linear-gradient(135deg, #FFFFFF, #FFB347);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            line-height: 1.2;
        }

        .code-block {
            background: #0a0a14;
            border-radius: 20px;
            padding: 18px;
            border-left: 4px solid #FF3D7A;
            font-family: monospace;
            font-size: 0.85rem;
            overflow-x: auto;
            margin: 20px 0;
        }

        .section-title {
            text-align: center;
            font-size: 2.5rem;
            font-weight: 700;
            margin: 70px 0 40px;
            background: linear-gradient(135deg, #fff, #FFB347);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }

        .stat-number { font-size: 2rem; font-weight: 800; color: #FF3D7A; }
        .hero-stats { display: flex; gap: 30px; margin-top: 20px; }

        footer {
            margin-top: 80px;
            padding: 40px 0;
            border-top: 1px solid rgba(255,255,255,0.1);
            text-align: center;
        }
        .social-links a { color: #aaa; font-size: 1.6rem; margin: 0 12px; transition: 0.2s; }
        .social-links a:hover { color: #FF3D7A; }

        @media (max-width: 768px) {
            .hero-content h1 { font-size: 2.3rem; }
            .section-title { font-size: 1.8rem; }
            nav { flex-direction: column; }
        }

        button { background: none; border: none; cursor: pointer; }
        .btn-outline {
            background: transparent;
            border: 1.5px solid #FF3D7A;
            padding: 10px 22px;
            border-radius: 40px;
            font-weight: 600;
            color: #FF3D7A;
            transition: 0.2s;
        }
        .btn-outline:hover { background: rgba(255,61,122,0.15); transform: translateY(-2px); }
        .btn-large { padding: 14px 38px; font-size: 1rem; margin: 8px; }
    </style>
</head>
<body>
<div class="bg-gradient"></div>
<div class="stars"></div>

<div class="container">
    <nav>
        <div class="logo"><i class="fas fa-meteor"></i> METEOR</div>
        <ul class="nav-links">
            <li><a href="#features">Features</a></li>
            <li><a href="#script">Script</a></li>
            <li><a href="#download">Get</a></li>
        </ul>
        <button class="btn-outline" id="copyLoadBtn"><i class="fas fa-code"></i> Copy Loadstring</button>
    </nav>

    <!-- Hero 3D Panel -->
    <div class="hero" id="hero3d">
        <div class="hero-content">
            <div class="hero-3d-card" id="heroPanel">
                <span style="background: rgba(255,61,122,0.2); padding: 5px 12px; border-radius: 30px; font-size: 0.8rem;"><i class="fas fa-bolt"></i> Premium Lua Script</span>
                <h1 style="margin: 20px 0 15px;">Meteor Script<br>3D Interactive UI</h1>
                <p style="color: #bbb; margin-bottom: 20px;">Advanced Roblox Lua script with ESP, admin commands, auto-farm & stunning 3D panels that follow your cursor.</p>
                <div class="code-block">
                    <code style="color:#FFB347;">loadstring(game:HttpGet("https://raw.githubusercontent.com/MeteorScript/main.lua"))()</code>
                </div>
                <div class="hero-stats">
                    <div><span class="stat-number">200+</span><br>Functions</div>
                    <div><span class="stat-number">100%</span><br>Open Source</div>
                    <div><span class="stat-number">24/7</span><br>Updates</div>
                </div>
                <button class="btn-primary" id="scrollBtn" style="margin-top: 20px;"><i class="fas fa-download"></i> Install Meteor</button>
            </div>
        </div>
        <div style="flex:1; text-align: center;">
            <i class="fas fa-cube" style="font-size: 160px; color: rgba(255,61,122,0.4); filter: drop-shadow(0 0 30px #FF3D7A);"></i>
        </div>
    </div>

    <!-- Features Section with 3D Cards -->
    <div id="features">
        <div class="section-title"><i class="fas fa-gripfire"></i> 3D Interactive Panels</div>
        <div class="features-grid" id="featuresGrid">
            <div class="feature-card-3d" data-tilt data-tilt-max="12" data-tilt-perspective="800">
                <div class="feature-icon" style="font-size: 2.5rem; color:#FF3D7A;"><i class="fas fa-bolt"></i></div>
                <h3>Ultra Fast</h3>
                <p>Optimized Lua execution, zero lag. Instant response for all scripts and modules.</p>
            </div>
            <div class="feature-card-3d" data-tilt data-tilt-max="12" data-tilt-perspective="800">
                <div class="feature-icon" style="font-size: 2.5rem; color:#FF3D7A;"><i class="fas fa-eye"></i></div>
                <h3>ESP & Visuals</h3>
                <p>Player ESP, Tracers, Boxes, Health bars, Item ESP, and Chams with smooth 3D.</p>
            </div>
            <div class="feature-card-3d" data-tilt data-tilt-max="12" data-tilt-perspective="800">
                <div class="feature-icon" style="font-size: 2.5rem; color:#FF3D7A;"><i class="fas fa-robot"></i></div>
                <h3>Auto-Farm</h3>
                <p>Auto farm, dungeon farmer, auto clicker and game-specific mods included.</p>
            </div>
            <div class="feature-card-3d" data-tilt data-tilt-max="12" data-tilt-perspective="800">
                <div class="feature-icon" style="font-size: 2.5rem; color:#FF3D7A;"><i class="fas fa-shield-alt"></i></div>
                <h3>Anti-Ban</h3>
                <p>Advanced bypass techniques, regularly updated to stay undetected.</p>
            </div>
            <div class="feature-card-3d" data-tilt data-tilt-max="12" data-tilt-perspective="800">
                <div class="feature-icon" style="font-size: 2.5rem; color:#FF3D7A;"><i class="fas fa-code-branch"></i></div>
                <h3>Script Hub</h3>
                <p>Built-in script browser with 100+ community scripts ready to load.</p>
            </div>
            <div class="feature-card-3d" data-tilt data-tilt-max="12" data-tilt-perspective="800">
                <div class="feature-icon" style="font-size: 2.5rem; color:#FF3D7A;"><i class="fas fa-palette"></i></div>
                <h3>Modern UI</h3>
                <p>Draggable interface, theme support, sliders, toggles — fully customizable.</p>
            </div>
        </div>
    </div>

    <!-- Script Preview 3D Panel -->
    <div id="script">
        <div class="section-title"><i class="fas fa-terminal"></i> Script Preview (3D Panel)</div>
        <div class="panel-3d" id="scriptPanel" style="padding: 30px; margin-bottom: 40px;">
            <div style="display: flex; justify-content: space-between; flex-wrap: wrap; gap: 10px;">
                <span><i class="fas fa-file-code"></i> <strong>meteor_init.lua</strong> — Main Script Core</span>
                <span style="color:#FFB347;"><i class="fas fa-check-circle"></i> Ready to inject</span>
            </div>
            <pre style="background: #0B0B14; padding: 20px; border-radius: 20px; overflow-x: auto; margin-top: 20px; font-size: 0.8rem;"><code>-- Meteor Script v4.0 | 3D Panel Edition
local Meteor = {
    Version = "4.0.0",
    Features = {"ESP", "Aimbot", "Fly", "Noclip", "Speed"}
}

-- Load UI Library
local Library = loadstring(game:HttpGet("https://pastebin.com/raw/UIlib"))()
local Window = Library:CreateWindow("Meteor 3D")

-- ESP System
local espEnabled = true
local function setupESP()
    -- Player ESP with 3D boxes
    for _, plr in ipairs(game.Players:GetPlayers()) do
        -- ESP logic here
    end
end

-- Admin Commands
Meteor.Commands = {
    [".fly"] = function() -- toggle fly end,
    [".god"] = function() -- god mode end,
}

setupESP()
print("Meteor 3D Script Loaded!")</code></pre>
            <button class="btn-outline" id="copyScriptCode" style="margin-top: 15px;"><i class="far fa-copy"></i> Copy Script Snippet</button>
        </div>
    </div>

    <!-- Download 3D Panel -->
    <div id="download">
        <div class="download-panel-3d" id="downloadPanel" style="text-align: center;">
            <i class="fas fa-meteor" style="font-size: 60px; color:#FF3D7A; margin-bottom: 15px;"></i>
            <h2 style="font-size: 2.2rem;">Get Meteor Script</h2>
            <p style="margin: 15px auto; max-width: 550px;">Use any Roblox executor (Krnl, Synapse X, ScriptWare, Vega X) to run the script.</p>
            <div class="code-block" style="display: inline-block; text-align: left; background: #000000aa;">
                loadstring(game:HttpGet("https://raw.githubusercontent.com/MeteorScript/Meteor/main/loader.lua"))()
            </div>
            <br><br>
            <button class="btn-primary btn-large" id="copyLoadstringBtn"><i class="fas fa-copy"></i> Copy Loadstring</button>
            <button class="btn-outline btn-large" id="githubMockBtn"><i class="fab fa-github"></i> GitHub Repo</button>
            <p style="margin-top: 25px;"><i class="fas fa-shield-alt"></i> 100% open source | No keys | Auto-updates</p>
        </div>
    </div>

    <!-- Info Row -->
    <div style="display: flex; justify-content: center; gap: 30px; flex-wrap: wrap; margin: 50px 0 20px;">
        <div class="panel-3d" style="padding: 18px 25px;"><i class="fab fa-discord" style="color:#FF3D7A;"></i> Discord: 72k+ members</div>
        <div class="panel-3d" style="padding: 18px 25px;"><i class="fas fa-sync-alt"></i> Updates every 48h</div>
        <div class="panel-3d" style="padding: 18px 25px;"><i class="fas fa-star"></i> Trusted by 150k+ users</div>
    </div>

    <footer>
        <div class="social-links">
            <a href="#"><i class="fab fa-discord"></i></a>
            <a href="#"><i class="fab fa-github"></i></a>
            <a href="#"><i class="fab fa-twitter"></i></a>
        </div>
        <p>© 2026 Meteor Script — Premium Lua Script for Roblox. Not affiliated with Roblox Corp.</p>
        <p>For educational purposes only. 3D interactive panels effect.</p>
    </footer>
</div>

<script>
    // ========== 3D TILT EFFECT FOR ALL PANELS ==========
    // Apply 3D rotation on mouse move for any element with class that contains '3d' or specific IDs
    const tiltElements = document.querySelectorAll('.hero-3d-card, .feature-card-3d, .panel-3d, .download-panel-3d');
    
    function apply3DTilt(element) {
        element.addEventListener('mousemove', function(e) {
            const rect = this.getBoundingClientRect();
            const x = e.clientX - rect.left; // x position within element
            const y = e.clientY - rect.top;  // y position within element
            const centerX = rect.width / 2;
            const centerY = rect.height / 2;
            
            // Calculate rotation: max 12 degrees for X and Y
            const rotateY = ((x - centerX) / centerX) * 12;
            const rotateX = ((centerY - y) / centerY) * 12;
            
            // Add subtle shadow shift
            this.style.transform = `perspective(1200px) rotateX(${rotateX}deg) rotateY(${rotateY}deg) translateZ(5px)`;
            this.style.transition = 'transform 0.08s linear';
            this.style.boxShadow = `0 25px 40px -15px rgba(0,0,0,0.5), 0 0 0 1px rgba(255,61,122,0.2)`;
        });
        
        element.addEventListener('mouseleave', function() {
            this.style.transform = `perspective(1200px) rotateX(0deg) rotateY(0deg) translateZ(0px)`;
            this.style.transition = 'transform 0.3s cubic-bezier(0.2, 0.9, 0.4, 1.1)';
            this.style.boxShadow = '';
        });
    }
    
    tiltElements.forEach(el => apply3DTilt(el));
    
    // Also add for the hero main panel (already included but ensure)
    const heroPanel = document.getElementById('heroPanel');
    if(heroPanel) apply3DTilt(heroPanel);
    const scriptPanel = document.getElementById('scriptPanel');
    if(scriptPanel) apply3DTilt(scriptPanel);
    const downloadPanel = document.getElementById('downloadPanel');
    if(downloadPanel) apply3DTilt(downloadPanel);
    
    // ========== COPY FUNCTIONALITY ==========
    const loadstringFull = `loadstring(game:HttpGet("https://raw.githubusercontent.com/MeteorScript/Meteor/main/loader.lua"))()`;
    
    function copyLoadstring() {
        navigator.clipboard.writeText(loadstringFull);
        alert("✅ Loadstring copied to clipboard!\nPaste it into your Roblox executor.");
    }
    
    document.getElementById('copyLoadBtn')?.addEventListener('click', copyLoadstring);
    document.getElementById('copyLoadstringBtn')?.addEventListener('click', copyLoadstring);
    
    document.getElementById('copyScriptCode')?.addEventListener('click', () => {
        const code = document.querySelector('#scriptPanel pre code')?.innerText || "-- Meteor Script code";
        navigator.clipboard.writeText(code);
        alert("📋 Lua script code copied!");
    });
    
    document.getElementById('scrollBtn')?.addEventListener('click', () => {
        document.getElementById('download')?.scrollIntoView({ behavior: 'smooth' });
    });
    
    document.getElementById('githubMockBtn')?.addEventListener('click', () => {
        window.open('https://github.com/MeteorScript/Meteor', '_blank');
    });
    
    // Smooth scroll for nav links
    document.querySelectorAll('.nav-links a').forEach(link => {
        link.addEventListener('click', function(e) {
            const href = this.getAttribute('href');
            if(href && href !== '#') {
                e.preventDefault();
                const target = document.querySelector(href);
                if(target) target.scrollIntoView({ behavior: 'smooth' });
            }
        });
    });
    
    // Optional: Add floating 3D effect on stats cards
    const extraCards = document.querySelectorAll('.hero-stats div, .info-row');
    extraCards.forEach(card => {
        if(card.classList) card.style.transition = 'transform 0.2s';
        card.addEventListener('mouseenter', function() { this.style.transform = 'translateY(-3px)'; });
        card.addEventListener('mouseleave', function() { this.style.transform = 'translateY(0)'; });
    });
</script>
</body>
</html>
