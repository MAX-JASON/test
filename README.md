<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>保險智能分析整合平台</title>
    <style>
        /* 增强版霓虹赛博朋克风格 */
        :root {
            --grid-color: rgba(77, 45, 183, 0.3);
            --particle-color: rgba(0, 255, 255, 0.5);
            --glass-color: rgba(255, 255, 255, 0.1);
            --glass-border: rgba(255, 255, 255, 0.3);
            --neon-pulse: 0 0 15px currentColor;
            
            --primary-color: #0ff0fc;
            --success-color: #05f140;
            --warning-color: #f5d300;
            --danger-color: #ff3864;
            --light-bg: #0d0221;
            --card-bg: rgba(13, 2, 33, 0.7);
            --text-dark: #ffffff;
            --text-light: #d1f7ff;
            --border-color: #4d2db7;
            --shadow: 0 0 15px rgba(0, 255, 255, 0.5), 
                       0 0 30px rgba(0, 255, 255, 0.3);
            --neon-glow: 0 0 10px rgba(0, 255, 255, 0.8),
                         0 0 20px rgba(0, 255, 255, 0.6),
                         0 0 30px rgba(0, 255, 255, 0.4);
        }

        /* 网格背景 */
        body {
            background: 
                linear-gradient(rgba(13, 2, 33, 0.9), rgba(13, 2, 33, 0.9)),
                url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="100" height="100" viewBox="0 0 100 100"><rect width="100" height="100" fill="none" stroke="%234d2db7" stroke-width="0.5"/></svg>');
            background-size: 50px 50px;
            color: var(--text-dark);
            font-family: 'Rajdhani', 'Noto Sans TC', sans-serif;
            position: relative;
            overflow-x: hidden;
            background: #0d0221;
            background-image: 
                repeating-linear-gradient(0deg, rgba(77,45,183,0.18) 0 1px, transparent 1px 50px),
                repeating-linear-gradient(90deg, rgba(77,45,183,0.18) 0 1px, transparent 1px 50px);
        }

        /* 悬浮粒子效果 */
        .particles {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            pointer-events: none;
            z-index: -1;
        }

        .particle {
            position: absolute;
            border-radius: 50%;
            background: radial-gradient(circle, #0ff0fc 60%, transparent 100%);
            box-shadow: 0 0 16px 8px #0ff0fc88, 0 0 32px 8px #4d2db7aa;
            opacity: 0.7;
            animation: floatParticle 8s linear infinite;
        }

        @keyframes floatParticle {
            0% { transform: translateY(0) scale(1); opacity: 0.7; }
            50% { transform: translateY(-40px) scale(1.2); opacity: 1; }
            100% { transform: translateY(0) scale(1); opacity: 0.7; }
        }

        /* 霓虹边框效果 */
        .card {
            background: var(--card-bg);
            border: 1.5px solid #0ff0fc;
            box-shadow: 0 0 24px 2px #0ff0fc33, 0 0 60px 0 #4d2db744;
            position: relative;
            transition: box-shadow 0.3s, border 0.3s;
        }

        .card:hover {
            box-shadow: 0 0 40px 8px #0ff0fc99, 0 0 80px 0 #4d2db7cc;
            border: 2px solid #0ff0fc;
        }

        /* 霓虹按钮效果 */
        button {
            background: transparent;
            border: 2px solid var(--primary-color);
            color: var(--primary-color);
            text-shadow: 0 0 5px var(--primary-color);
            box-shadow: var(--neon-glow);
            transition: all 0.3s ease;
        }

        button:hover {
            background: rgba(0, 255, 255, 0.1);
            box-shadow: 0 0 20px var(--primary-color);
        }

        /* 冷光动效 */
        @keyframes coldGlow {
            0%, 100% { opacity: 0.7; }
            50% { opacity: 1; }
        }

        .cold-glow {
            animation: coldGlow 3s ease-in-out infinite;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            font-family: 'Noto Sans TC', 'Arial', sans-serif;
            background-color: var(--light-bg);
            color: var(--text-dark);
            line-height: 1.6;
            padding: 20px;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: flex-start;
        }

        .container {
            background-color: var(--card-bg);
            border-radius: 12px;
            box-shadow: var(--shadow);
            padding: 30px;
            max-width: 1400px; /* Increased max-width for more content */
            width: 100%;
            margin-top: 20px;
        }

        header {
            text-align: center;
            margin-bottom: 30px;
        }

        header h1 {
            color: var(--primary-color);
            font-size: 2.8em;
            margin-bottom: 10px;
        }

        header .subtitle {
            color: var(--text-light);
            font-size: 1.2em;
        }

        .tabs {
            display: flex;
            justify-content: center;
            margin-bottom: 30px;
            flex-wrap: wrap; /* Allow tabs to wrap on smaller screens */
        }

        .tab {
            padding: 12px 25px;
            cursor: pointer;
            border-bottom: 3px solid transparent;
            font-weight: 600;
            color: var(--text-light);
            transition: all 0.3s ease;
            margin: 0 10px;
            white-space: nowrap; /* Prevent tab titles from breaking */
        }

        .tab:hover {
            color: var(--primary-color);
        }

        .tab.active {
            border-color: var(--primary-color);
            color: var(--primary-color);
        }

        .tab-content {
            display: none;
            padding: 20px 0;
        }

        .tab-content.active {
            display: block;
        }

        .card {
            background-color: var(--card-bg);
            border-radius: 10px;
            box-shadow: var(--shadow);
            padding: 25px;
            margin-bottom: 25px;
            border: 1px solid var(--border-color);
        }

        .card h2 {
            color: var(--secondary-color);
            font-size: 1.6em;
            margin-bottom: 20px;
            border-bottom: 2px solid var(--primary-color);
            padding-bottom: 10px;
            display: flex;
            align-items: center;
        }

        .card h2 i {
            margin-right: 10px;
            color: var(--primary-color);
        }

        .form-group {
            margin-bottom: 18px;
        }

        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 500;
            color: var(--text-dark);
        }

        .form-group input[type="text"],
        .form-group input[type="number"],
        .form-group select {
            width: 100%;
            padding: 12px 15px;
            border: 1px solid var(--border-color);
            border-radius: 8px;
            font-size: 1em;
            color: var(--text-dark);
            transition: border-color 0.3s ease;
        }

        .form-group input[type="text"]:focus,
        .form-group input[type="number"]:focus,
        .form-group select:focus {
            outline: none;
            border-color: var(--primary-color);
            box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.2);
        }

        .form-group.inline {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .form-group.inline label {
            margin-bottom: 0;
            flex-shrink: 0;
        }

        .form-group.inline input {
            flex-grow: 1;
        }

        .checkbox-group {
            display: flex;
            flex-wrap: wrap;
            gap: 20px;
            margin-top: 10px;
        }

        .checkbox-group label {
            display: flex;
            align-items: center;
            font-weight: 400;
            cursor: pointer;
            color: var(--text-dark);
        }

        .checkbox-group input[type="checkbox"] {
            margin-right: 8px;
            transform: scale(1.2);
        }

        .btn-group {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-top: 30px;
        }

        button {
            padding: 12px 25px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: 1.1em;
            font-weight: 600;
            transition: all 0.3s ease;
            white-space: nowrap;
        }

        button.primary-btn {
            background-color: var(--primary-color);
            color: white;
        }

        button.primary-btn:hover {
            background-color: #1d4ed8;
            transform: translateY(-2px);
        }

        button.secondary-btn {
            background-color: var(--border-color);
            color: var(--text-dark);
        }

        button.secondary-btn:hover {
            background-color: #cbd5e1;
            transform: translateY(-2px);
        }

        #resultsSection {
            display: none;
            margin-top: 30px;
        }

        .results-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 25px;
            margin-bottom: 30px;
        }

        .result-card {
            background-color: var(--card-bg);
            border-radius: 10px;
            box-shadow: var(--shadow);
            padding: 25px;
            text-align: center;
            border: 1px solid var(--border-color);
        }

        .result-card h3 {
            color: var(--secondary-color);
            font-size: 1.4em;
            margin-bottom: 15px;
        }

        .result-card .score {
            font-size: 2.5em;
            font-weight: 700;
            margin-bottom: 10px;
            color: var(--primary-color);
        }

        .result-card .description {
            color: var(--text-light);
            font-size: 0.9em;
        }

        .chart-container {
            width: 100%;
            height: 400px;
            margin-bottom: 25px;
        }

        #recommendationTable {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }

        #recommendationTable th, #recommendationTable td {
            border: 1px solid var(--border-color);
            padding: 12px;
            text-align: left;
        }

        #recommendationTable th {
            background-color: var(--light-bg);
            color: var(--secondary-color);
            font-weight: 600;
        }

        #recommendationTable tr:nth-child(even) {
            background-color: #f1f5f9;
        }

        #recommendationTable tr:hover {
            background-color: #e2e8f0;
        }

        .alert {
            padding: 15px;
            border-radius: 8px;
            margin-bottom: 20px;
            font-weight: 500;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .alert-info {
            background-color: #eff6ff;
            color: #1e40af;
            border: 1px solid #bfdbfe;
        }

        .alert-warning {
            background-color: #fffbeb;
            color: #b45309;
            border: 1px solid #fde68a;
        }

        .alert-error {
            background-color: #fee2e2;
            color: #b91c1c;
            border: 1px solid #fca5a5;
        }

        /* CSS from 保教分析.html (Specific Components) */
        .tool-card {
            background-color: var(--card-bg); /* Using base card-bg */
            border-radius: 10px;
            box-shadow: var(--shadow);
            padding: 25px;
            margin-bottom: 25px;
            border: 1px solid var(--border-color);
        }
        .tool-card h2 {
            color: var(--secondary-color);
            font-size: 1.6em;
            margin-bottom: 20px;
            border-bottom: 2px solid var(--primary-color);
            padding-bottom: 10px;
            display: flex;
            align-items: center;
        }
        .tool-card .chart-canvas {
            width: 100%;
            height: 350px;
            margin-top: 20px;
            background-color: #f0f4f8; /* Light background for charts */
            border-radius: 8px;
        }
        #medicalLTC3DChart {
            width: 100%;
            height: 350px;
            margin-top: 20px;
            background-color: #f0f4f8;
            border-radius: 8px;
        }
        .premium-health-meter {
            width: 100%;
            height: 30px;
            background-color: #e0e0e0;
            border-radius: 15px;
            overflow: hidden;
            margin-top: 20px;
        }
        .premium-health-fill {
            height: 100%;
            background: linear-gradient(to right, #ef4444, #f59e0b, #10b981); /* Red-Yellow-Green gradient */
            border-radius: 15px;
            width: 0; /* Will be set by JS */
            transition: width 0.8s ease-out;
        }
        .cpv-bar {
            width: 100%;
            height: 25px;
            background-color: #e0e0e0;
            border-radius: 12px;
            overflow: hidden;
            margin-top: 15px;
        }
        .cpv-fill {
            height: 100%;
            background-color: var(--primary-color);
            border-radius: 12px;
            width: 0; /* Will be set by JS */
            transition: width 0.8s ease-out;
        }
        .info-text {
            color: var(--text-light);
            font-size: 0.9em;
            margin-top: 10px;
        }

        /* Responsive Adjustments */
        @media (max-width: 1024px) {
            .container {
                padding: 25px;
            }
            header h1 {
                font-size: 2.2em;
            }
            .tabs {
                flex-direction: column;
                align-items: center;
                gap: 10px;
            }
            .tab {
                margin: 5px 0;
                width: 90%;
                text-align: center;
            }
        }

        @media (max-width: 768px) {
            body {
                padding: 10px;
            }
            .container {
                padding: 15px;
            }
            header h1 {
                font-size: 1.8em;
            }
            .card h2, .tool-card h2 {
                font-size: 1.4em;
            }
            .form-group.inline {
                flex-direction: column;
                align-items: flex-start;
                gap: 8px;
            }
            .btn-group {
                flex-direction: column;
                gap: 15px;
            }
            button {
                width: 100%;
            }
            .results-grid {
                grid-template-columns: 1fr;
            }
            .chart-container, .tool-card .chart-canvas, #medicalLTC3DChart {
                height: 300px; /* Adjust height for smaller screens */
            }
        }
    </style>
    <!-- 粒子動態背景容器 -->
    <div class="particles" id="particles-bg"></div>
    <script>
    // --- 賽博朋克霓虹粒子動態背景 ---
    function createNeonParticles(num=32) {
        const container = document.getElementById('particles-bg');
        if (!container) return;
        container.innerHTML = '';
        for(let i=0;i<num;i++){
            const p = document.createElement('div');
            p.className = 'particle';
            const size = Math.random()*18+12;
            p.style.width = p.style.height = size+'px';
            p.style.left = (Math.random()*100)+'vw';
            p.style.top = (Math.random()*100)+'vh';
            p.style.animationDuration = (6+Math.random()*6)+'s';
            p.style.opacity = 0.5+Math.random()*0.5;
            container.appendChild(p);
        }
    }
    window.addEventListener('DOMContentLoaded',()=>{
        createNeonParticles(36);
        window.addEventListener('resize',()=>createNeonParticles(36));
    });
    </script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/echarts@5.4.3/dist/echarts.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js" defer></script>
    <script src="https://cdn.jsdelivr.net/npm/chartjs-plugin-datalabels@2.0.0"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">

</head>
<body>
    <div class="container">
        <header>
            <h1>保險智能分析整合平台</h1>
            <div class="subtitle">全面洞察，智慧規劃您的未來</div>
        </header>

        <div class="tabs">
            <div class="tab active" onclick="switchTab(0)">總覽與基本輸入</div>
            <div class="tab" onclick="switchTab(1)">壽險缺口分析</div>
            <div class="tab" onclick="switchTab(2)">醫療長照預估</div>
            <div class="tab" onclick="switchTab(3)">保費健康度與CP值</div>
            <div class="tab" onclick="switchTab(4)">現金價值分析</div>
            <div class="tab" onclick="switchTab(5)">綜合健診報告</div>
            <div class="tab" onclick="switchTab(6)">情境模擬</div>
            <div class="tab" onclick="switchTab(7)">多保單比較</div>
        </div>

        <div class="tab-content active" id="tab-0">
            <div class="card">
                <h2><i class="fas fa-user-circle"></i>基本資料</h2>
                <div class="form-group">
                    <label for="clientName">姓名</label>
                    <input type="text" id="clientName" placeholder="請輸入客戶姓名">
                </div>
                <div class="form-group inline">
                    <label for="clientAge">年齡</label>
                    <input type="number" id="clientAge" min="0" placeholder="請輸入年齡">
                </div>
                <div class="form-group inline">
                    <label for="annualIncome">年收入 (NTD)</label>
                    <input type="number" id="annualIncome" min="0" placeholder="請輸入家庭年收入">
                </div>
                <div class="form-group">
                    <label for="familyStatus">家庭狀況</label>
                    <select id="familyStatus">
                        <option value="single">單身</option>
                        <option value="married-no-children">已婚無子女</option>
                        <option value="married-with-children">已婚有子女</option>
                        <option value="other">其他</option>
                    </select>
                </div>
            </div>

            <div class="card">
                <h2><i class="fas fa-file-invoice-dollar"></i>保單概覽</h2>
                <div class="form-group inline">
                    <label for="totalCoverage">總保額 (NTD)</label>
                    <input type="number" id="totalCoverage" min="0" placeholder="所有保單總保額">
                </div>
                <div class="form-group inline">
                    <label for="totalPremium">總保費 (NTD)</label>
                    <input type="number" id="totalPremium" min="0" placeholder="所有保單總保費（累計）">
                </div>
                <div class="form-group inline">
                    <label for="annualPremium">年繳保費 (NTD)</label>
                    <input type="number" id="annualPremium" min="0" placeholder="所有保單年繳保費總額">
                </div>
                <div class="form-group inline">
                    <label for="coverageItems">保障項目數</label>
                    <input type="number" id="coverageItems" min="0" placeholder="例如：醫療險、癌症險、壽險...等">
                </div>
                <div class="form-group inline">
                    <label for="duplicateItems">重複保障項目數</label>
                    <input type="number" id="duplicateItems" min="0" placeholder="例如：兩份醫療險、兩份癌症險">
                </div>
                <div class="form-group inline">
                    <label for="totalItems">總保單份數</label>
                    <input type="number" id="totalItems" min="0" placeholder="實際持有保單的份數">
                </div>
            </div>

            <div class="card">
                <h2><i class="fas fa-chart-pie"></i>保單類型配置 (佔年繳保費百分比)</h2>
                <div class="form-group inline">
                    <label for="medicalInsurance">醫療險 (%)</label>
                    <input type="number" id="medicalInsurance" min="0" max="100" placeholder="例如：30">
                </div>
                <div class="form-group inline">
                    <label for="lifeInsurance">壽險 (%)</label>
                    <input type="number" id="lifeInsurance" min="0" max="100" placeholder="例如：25">
                </div>
                <div class="form-group inline">
                    <label for="savingsInsurance">儲蓄險 (%)</label>
                    <input type="number" id="savingsInsurance" min="0" max="100" placeholder="例如：20">
                </div>
                <div class="form-group inline">
                    <label for="accidentInsurance">意外險 (%)</label>
                    <input type="number" id="accidentInsurance" min="0" max="100" placeholder="例如：15">
                </div>
                <div class="form-group inline">
                    <label for="otherInsurance">其他險 (%)</label>
                    <input type="number" id="otherInsurance" min="0" max="100" placeholder="例如：10">
                </div>
                <div id="percentageSumWarning" class="alert alert-warning" style="display: none;">
                    <i class="fas fa-exclamation-triangle"></i> 百分比總和必須為100%！
                </div>
            </div>

            <div class="card">
                <h2><i class="fas fa-chart-line"></i>保障缺口分析</h2>
                <div class="checkbox-group">
                    <label><input type="checkbox" id="eduGap"> 教育金缺口</label>
                    <label><input type="checkbox" id="incomeGap"> 收入補償缺口</label>
                    <label><input type="checkbox" id="careGap"> 長期照顧缺口</label>
                    <label><input type="checkbox" id="retirementGap"> 退休金缺口</label>
                </div>
            </div>

            <div class="btn-group">
                <button class="primary-btn" onclick="runAllAnalyses()">
                    <i class="fas fa-play-circle"></i> 啟動綜合分析
                </button>
                <button class="secondary-btn" onclick="resetForm()">
                    <i class="fas fa-sync-alt"></i> 重設表單
                </button>
            </div>
        </div>

        <div class="tab-content" id="tab-1">
            <div class="tool-card">
                <h2><i class="fas fa-calculator"></i> 壽險保障缺口分析 (D.I.M.E. 法則)</h2>
                <div class="form-group inline">
                    <label for="dimeDebt">債務 (貸款、卡債等)</label>
                    <input type="number" id="dimeDebt" min="0" value="0">
                </div>
                <div class="form-group inline">
                    <label for="dimeIncomeYears">家庭收入需求年數</label>
                    <input type="number" id="dimeIncomeYears" min="1" value="10">
                </div>
                <div class="form-group inline">
                    <label for="dimeIncomeAnnual">家庭年收入</label>
                    <input type="number" id="dimeIncomeAnnual" min="0" value="0">
                </div>
                <div class="form-group inline">
                    <label for="dimeMortgage">房貸/車貸餘額</label>
                    <input type="number" id="dimeMortgage" min="0" value="0">
                </div>
                <div class="form-group inline">
                    <label for="dimeEducation">子女教育金需求</label>
                    <input type="number" id="dimeEducation" min="0" value="0">
                </div>
                <div class="form-group inline">
                    <label for="dimeCurrentLifeInsurance">現有壽險保額</label>
                    <input type="number" id="dimeCurrentLifeInsurance" min="0" value="0">
                </div>
                <div class="btn-group">
                    <button class="primary-btn" onclick="calculateDIME()">計算壽險缺口</button>
                </div>
                <p class="info-text">總壽險需求: <span id="dimeTotalDemand">0</span> NTD</p>
                <p class="info-text">壽險保障缺口: <span id="dimeGap">0</span> NTD</p>
                <canvas id="dimeChart" class="chart-canvas"></canvas>
            </div>
        </div>

        <div class="tab-content" id="tab-2">
            <div class="tool-card">
                <h2><i class="fas fa-hospital"></i> 醫療/長照費用預估與保障比對</h2>
                <div class="form-group inline">
                    <label for="medLTC_age">目前年齡</label>
                    <input type="number" id="medLTC_age" min="0" value="30">
                </div>
                <div class="form-group inline">
                    <label for="medLTC_lifeExpectancy">預期壽命</label>
                    <input type="number" id="medLTC_lifeExpectancy" min="1" value="85">
                </div>
                <div class="form-group inline">
                    <label for="medLTC_annualMedicalCost">每年平均醫療費用 (假設)</label>
                    <input type="number" id="medLTC_annualMedicalCost" min="0" value="50000">
                </div>
                <div class="form-group inline">
                    <label for="medLTC_ltcYears">預計長期照護年數</label>
                    <input type="number" id="medLTC_ltcYears" min="0" value="10">
                </div>
                <div class="form-group inline">
                    <label for="medLTC_annualLTCcost">每年長期照護費用 (假設)</label>
                    <input type="number" id="medLTC_annualLTCcost" min="0" value="300000">
                </div>
                <div class="form-group inline">
                    <label for="medLTC_currentCoverage">現有醫療/長照險總額</label>
                    <input type="number" id="medLTC_currentCoverage" min="0" value="0">
                </div>
                <div class="btn-group">
                    <button class="primary-btn" onclick="calculateMedicalLTC()">計算醫療/長照費用</button>
                </div>
                <p class="info-text">預估總醫療費用: <span id="estimatedMedicalCost">0</span> NTD</p>
                <p class="info-text">預估總長照費用: <span id="estimatedLTCCost">0</span> NTD</p>
                <p class="info-text">總醫療/長照需求: <span id="totalMedicalLTCDemand">0</span> NTD</p>
                <p class="info-text">醫療/長照保障缺口: <span id="medicalLTCDifference">0</span> NTD</p>
                <div id="medicalLTC3DChart" class="chart-canvas"></div>
            </div>
        </div>

        <div class="tab-content" id="tab-3">
            <div class="tool-card">
                <h2><i class="fas fa-heartbeat"></i> 保費健康度與CP值評分</h2>
                <div class="form-group inline">
                    <label for="ph_annualHouseholdIncome">家庭年收入</label>
                    <input type="number" id="ph_annualHouseholdIncome" min="0" value="0">
                </div>
                <div class="form-group inline">
                    <label for="ph_annualTotalPremium">年繳保費總額</label>
                    <input type="number" id="ph_annualTotalPremium" min="0" value="0">
                </div>
                <div class="form-group inline">
                    <label for="ph_mainCoverageAmount">主要保障類保額 (壽險、重大疾病等)</label>
                    <input type="number" id="ph_mainCoverageAmount" min="0" value="0">
                </div>
                <div class="form-group inline">
                    <label for="ph_premiumPerCoverage">每百萬保額年繳保費 (元)</label>
                    <input type="number" id="ph_premiumPerCoverage" min="0" value="0" placeholder="例如：10000">
                </div>
                <div class="btn-group">
                    <button class="primary-btn" onclick="calculatePremiumHealthCPV()">計算健康度與CP值</button>
                </div>
                <h3>保費佔收入比例: <span id="premiumPercentage">0.00%</span></h3>
                <div class="premium-health-meter">
                    <div id="premiumHealthFill" class="premium-health-fill"></div>
                </div>
                <p class="info-text" id="premiumHealthStatus">狀態: 良好</p>

                <h3 style="margin-top: 30px;">CP值 (每百萬保障的保費效率): <span id="cpvValue">0</span></h3>
                <div class="cpv-bar">
                    <div id="cpvFill" class="cpv-fill"></div>
                </div>
                <p class="info-text" id="cpvStatus">CP值狀態: 一般</p>
            </div>
        </div>

        <div class="tab-content" id="tab-4">
            <div class="tool-card">
                <h2><i class="fas fa-money-bill-wave"></i> 現金價值成長與通膨比較分析</h2>
                <div class="form-group inline">
                    <label for="cv_annualPremium">每年繳交保費</label>
                    <input type="number" id="cv_annualPremium" min="0" value="0">
                </div>
                <div class="form-group inline">
                    <label for="cv_paymentYears">繳費年期</label>
                    <input type="number" id="cv_paymentYears" min="1" value="20">
                </div>
                <div class="form-group inline">
                    <label for="cv_expectedReturnRate">預期內部報酬率 (%)</label>
                    <input type="number" id="cv_expectedReturnRate" min="0" max="100" step="0.1" value="2">
                </div>
                <div class="form-group inline">
                    <label for="cv_inflationRate">預期通膨率 (%)</label>
                    <input type="number" id="cv_inflationRate" min="0" max="100" step="0.1" value="1.5">
                </div>
                <div class="form-group inline">
                    <label for="cv_analysisYears">分析總年期</label>
                    <input type="number" id="cv_analysisYears" min="1" value="30">
                </div>
                <div class="btn-group">
                    <button class="primary-btn" onclick="analyzeCashValue()">分析現金價值</button>
                </div>
                <p class="info-text">總繳保費: <span id="totalPremiumPaid">0</span> NTD</p>
                <p class="info-text">最終現金價值 (未考慮通膨): <span id="finalCashValue">0</span> NTD</p>
                <p class="info-text">最終實質現金價值 (考慮通膨): <span id="finalRealValue">0</span> NTD</p>
                <p class="info-text">投資報酬率 (IRR): <span id="irrValue">0.00%</span></p>
                <canvas id="cashValueChart" class="chart-canvas"></canvas>
            </div>
        </div>


        <div class="tab-content" id="tab-5"></div>
        <!-- 情境模擬區塊 -->
        <div class="tab-content" id="tab-6">
            <div class="card">
                <h2><i class="fas fa-random"></i> 情境模擬</h2>
                <div class="form-group inline">
                    <label for="sim_futureIncome">未來年收入 (NTD)</label>
                    <input type="number" id="sim_futureIncome" min="0" value="0">
                </div>
                <div class="form-group inline">
                    <label for="sim_familyChange">家庭結構變動</label>
                    <select id="sim_familyChange">
                        <option value="none">無變動</option>
                        <option value="married">結婚</option>
                        <option value="child">有子女</option>
                        <option value="divorce">離婚</option>
                        <option value="other">其他</option>
                    </select>
                </div>
                <div class="form-group inline">
                    <label for="sim_criticalIllness">重大疾病發生</label>
                    <select id="sim_criticalIllness">
                        <option value="none">無</option>
                        <option value="cancer">癌症</option>
                        <option value="stroke">中風</option>
                        <option value="heart">心臟病</option>
                        <option value="other">其他</option>
                    </select>
                </div>
                <div class="btn-group">
                    <button class="primary-btn" onclick="applyScenario()"><i class="fas fa-magic"></i> 套用情境</button>
                </div>
                <div class="info-text" id="scenarioResult">請調整參數，系統將即時預覽保障缺口變化。</div>
            </div>
            <div class="card">
                <h2><i class="fas fa-chart-bar"></i> 情境模擬互動圖表</h2>
                <div class="chart-container">
                    <canvas id="scenarioChart"></canvas>
                </div>
            </div>
            <div class="card">
                <h2><i class="fas fa-users"></i> 同齡層/市場對比</h2>
                <div id="peerCompareResult">(載入中...)</div>
            </div>
        </div>

        <!-- 多保單比較區塊 -->
        <div class="tab-content" id="tab-7">
            <div class="card">
                <h2><i class="fas fa-layer-group"></i> 多保單輸入與比較</h2>
                <div id="policyList"></div>
                <div class="btn-group">
                    <button class="primary-btn" onclick="addPolicy()"><i class="fas fa-plus"></i> 新增保單</button>
                </div>
            </div>
            <div class="card">
                <h2><i class="fas fa-table"></i> 保單橫向比較表</h2>
                <div id="policyCompareTable"></div>
            </div>
            <div class="card">
                <h2><i class="fas fa-chart-line"></i> 保單比較互動圖表</h2>
                <div class="chart-container">
                    <canvas id="policyCompareChart"></canvas>
                </div>
            </div>
        </div>

        <!-- 多保單比較區塊 -->
        <div class="tab-content" id="tab-7">
            <div class="card">
                <h2><i class="fas fa-layer-group"></i> 多保單輸入與比較</h2>
                <div id="policyList"></div>
                <div class="btn-group">
                    <button class="primary-btn" onclick="addPolicy()"><i class="fas fa-plus"></i> 新增保單</button>
                </div>
            </div>
            <div class="card">
                <h2><i class="fas fa-table"></i> 保單橫向比較表</h2>
                <div id="policyCompareTable"></div>
            </div>
            <div class="card">
                <h2><i class="fas fa-chart-line"></i> 保單比較互動圖表</h2>
                <div class="chart-container">
                    <canvas id="policyCompareChart"></canvas>
                </div>
            </div>
        </div>
            <div id="resultsSection" style="display: block;">
                <div class="results-grid">
                    <div class="result-card">
                        <h3>總分</h3>
                        <div class="score" id="totalScoreValue">N/A</div>
                        <div class="description">綜合評估您的保單健康程度。</div>
                    </div>
                    <div class="result-card">
                        <h3>保費槓桿比</h3>
                        <div class="score" id="leverageRatioValue">N/A</div>
                        <div class="description">用較少保費換取較高保障的能力。</div>
                    </div>
                    <div class="result-card">
                        <h3>理賠覆蓋率</h3>
                        <div class="score" id="coverageRatioValue">N/A</div>
                        <div class="description">保障範圍與潛在風險的匹配程度。</div>
                    </div>
                    <div class="result-card">
                        <h3>保單效率</h3>
                        <div class="score" id="efficiencyScoreValue">N/A</div>
                        <div class="description">保單結構是否達到最佳效益。</div>
                    </div>
                    <div class="result-card">
                        <h3>保費壓力</h3>
                        <div class="score" id="premiumStressValue">N/A</div>
                        <div class="description">年繳保費佔年收入的比例。</div>
                    </div>
                </div>

                <div class="card">
                    <h2><i class="fas fa-chart-area"></i>綜合保障雷達圖</h2>
                    <div class="chart-container">
                        <canvas id="radarChart"></canvas>
                    </div>
                </div>

                <div class="card">
                    <h2><i class="fas fa-chart-pie"></i>保單類型配置圓餅圖</h2>
                    <div class="chart-container">
                        <canvas id="pieChart"></canvas>
                    </div>
                </div>

                <div class="card">
                    <h2><i class="fas fa-dollar-sign"></i>槓桿比與保費支出趨勢</h2>
                    <div class="chart-container">
                        <canvas id="trendChart"></canvas>
                    </div>
                </div>

                <div class="card">
                    <h2><i class="fas fa-calendar-alt"></i>人生階段目標與缺口時間軸</h2>
                    <div class="chart-container" style="height: 250px;">
                        <canvas id="lifetimeTimeline"></canvas>
                    </div>
                </div>

                <div class="card">
                    <h2><i class="fas fa-lightbulb"></i>優化建議</h2>
                    <table id="recommendationTable">
                        <thead>
                            <tr>
                                <th>建議項目</th>
                                <th>說明</th>
                            </tr>
                        </thead>
                        <tbody>
                            </tbody>
                    </table>
                </div>

                <div class="btn-group">
                    <button class="primary-btn" onclick="printResults()">
                        <i class="fas fa-print"></i> 列印分析報告
                    </button>
                    <button class="secondary-btn" onclick="resetForm()">
                        <i class="fas fa-sync-alt"></i> 重新分析
                    </button>
                </div>
            </div>
        </div>
    </div>

    <script>
        // --- 情境模擬即時預覽 ---
        let scenarioChartInstance;
        function updateScenario() {
            // 取得情境參數
            const futureIncome = parseFloat(document.getElementById('sim_futureIncome').value) || 0;
            const familyChange = document.getElementById('sim_familyChange').value;
            const criticalIllness = document.getElementById('sim_criticalIllness').value;

            // 模擬分析：根據參數動態調整保障缺口（簡化版，實際可根據需求細化）
            let baseGap = analysisData.dimeGap || 1000000;
            let gap = baseGap;
            let desc = [];
            if (futureIncome > 0) {
                gap += (futureIncome * 2); // 假設未來收入提升，缺口增加
                desc.push('未來收入提升，缺口增加');
            }
            if (familyChange === 'married') {
                gap += 300000;
                desc.push('結婚，家庭責任增加');
            } else if (familyChange === 'child') {
                gap += 500000;
                desc.push('有子女，教育/生活責任增加');
            } else if (familyChange === 'divorce') {
                gap -= 200000;
                desc.push('離婚，部分責任減少');
            }
            if (criticalIllness !== 'none') {
                gap += 800000;
                desc.push('重大疾病發生，醫療/照護需求大增');
            }
            gap = Math.max(0, gap);
            document.getElementById('scenarioResult').innerHTML = `預估保障缺口：<b>${gap.toLocaleString()}</b> NTD<br>${desc.join('，')}`;
            // 畫互動圖表
            updateScenarioChart(gap);
        }
        function updateScenarioChart(gap) {
            if (scenarioChartInstance) scenarioChartInstance.destroy();
            const ctx = document.getElementById('scenarioChart').getContext('2d');
            scenarioChartInstance = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: ['情境下保障缺口'],
                    datasets: [{
                        label: '缺口金額',
                        data: [gap],
                        backgroundColor: '#0ff',
                        borderColor: '#0ff',
                        borderWidth: 2
                    }]
                },
                options: {
                    responsive: true,
                    plugins: {
                        legend: { display: false },
                        title: { display: true, text: '情境模擬缺口預覽' }
                    },
                    scales: {
                        y: { beginAtZero: true, title: { display: true, text: '金額 (NTD)' } }
                    }
                }
            });
        }
        // 綁定即時預覽
        setTimeout(() => {
            ['sim_futureIncome','sim_familyChange','sim_criticalIllness'].forEach(id => {
                const el = document.getElementById(id);
                if (el) el.addEventListener('input', updateScenario);
                if (el && el.tagName==='SELECT') el.addEventListener('change', updateScenario);
            });
        }, 500);

        // --- 多保單動態增刪與比較 ---
        let policies = [createEmptyPolicy()];
        function createEmptyPolicy() {
            return {
                name: '',
                type: '',
                coverage: 0,
                premium: 0,
                insured: '',
                start: '',
                end: ''
            };
        }
        function renderPolicyList() {
            const list = document.getElementById('policyList');
            if (!list) return;
            list.innerHTML = '';
            policies.forEach((p, idx) => {
                const div = document.createElement('div');
                div.className = 'policy-input-card';
                div.innerHTML = `
                    <div class="form-group inline">
                        <label>保單名稱</label>
                        <input type="text" value="${p.name}" onchange="updatePolicyField(${idx},'name',this.value)">
                        <label>類型</label>
                        <input type="text" value="${p.type}" onchange="updatePolicyField(${idx},'type',this.value)">
                        <label>保額</label>
                        <input type="number" value="${p.coverage}" min="0" onchange="updatePolicyField(${idx},'coverage',this.value)">
                        <label>年繳保費</label>
                        <input type="number" value="${p.premium}" min="0" onchange="updatePolicyField(${idx},'premium',this.value)">
                        <label>被保人</label>
                        <input type="text" value="${p.insured}" onchange="updatePolicyField(${idx},'insured',this.value)">
                        <label>起訖</label>
                        <input type="text" value="${p.start}" placeholder="起" style="width:60px" onchange="updatePolicyField(${idx},'start',this.value)">
                        <input type="text" value="${p.end}" placeholder="迄" style="width:60px" onchange="updatePolicyField(${idx},'end',this.value)">
                        <button class="danger-btn" onclick="removePolicy(${idx})">刪除</button>
                    </div>
                `;
                list.appendChild(div);
            });
        }
        function addPolicy() {
            policies.push(createEmptyPolicy());
            renderPolicyList();
            renderPolicyCompareTable();
            renderPolicyCompareChart();
        }
        function removePolicy(idx) {
            if (policies.length <= 1) return;
            policies.splice(idx, 1);
            renderPolicyList();
            renderPolicyCompareTable();
            renderPolicyCompareChart();
        }
        function updatePolicyField(idx, field, value) {
            if (field === 'coverage' || field === 'premium') value = parseFloat(value) || 0;
            policies[idx][field] = value;
            renderPolicyCompareTable();
            renderPolicyCompareChart();
        }
        // 初始渲染
        setTimeout(() => { renderPolicyList(); renderPolicyCompareTable(); renderPolicyCompareChart(); }, 500);

        // --- 多保單橫向比較表 ---
        function renderPolicyCompareTable() {
            const tableDiv = document.getElementById('policyCompareTable');
            if (!tableDiv) return;
            if (!policies.length) { tableDiv.innerHTML = '尚無保單'; return; }
            let html = '<table class="compare-table"><thead><tr>' +
                '<th>名稱</th><th>類型</th><th>保額</th><th>年繳保費</th><th>被保人</th><th>起訖</th></tr></thead><tbody>';
            policies.forEach(p => {
                html += `<tr><td>${p.name}</td><td>${p.type}</td><td>${p.coverage}</td><td>${p.premium}</td><td>${p.insured}</td><td>${p.start}~${p.end}</td></tr>`;
            });
            html += '</tbody></table>';
            tableDiv.innerHTML = html;
        }

        // --- 多保單互動圖表 ---
        let policyCompareChartInstance;
        function renderPolicyCompareChart() {
            const ctx = document.getElementById('policyCompareChart');
            if (!ctx) return;
            const chartCtx = ctx.getContext('2d');
            if (policyCompareChartInstance) policyCompareChartInstance.destroy();
            const labels = policies.map(p => p.name || '保單'+(policies.indexOf(p)+1));
            const coverages = policies.map(p => p.coverage);
            const premiums = policies.map(p => p.premium);
            policyCompareChartInstance = new Chart(chartCtx, {
                type: 'bar',
                data: {
                    labels: labels,
                    datasets: [
                        { label: '保額', data: coverages, backgroundColor: '#0ff', borderColor: '#0ff', borderWidth: 1 },
                        { label: '年繳保費', data: premiums, backgroundColor: '#f0f', borderColor: '#f0f', borderWidth: 1 }
                    ]
                },
                options: {
                    responsive: true,
                    plugins: {
                        legend: { position: 'top' },
                        title: { display: true, text: '多保單保額/保費比較' },
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    return context.dataset.label + ': ' + context.parsed.y.toLocaleString() + ' NTD';
                                }
                            }
                        }
                    },
                    scales: {
                        y: { beginAtZero: true, title: { display: true, text: '金額 (NTD)' } }
                    },
                    onClick: function(evt, elements) {
                        if (elements.length > 0) {
                            const idx = elements[0].index;
                            alert('點擊保單：' + labels[idx] + '\n保額：' + coverages[idx].toLocaleString() + '\n年繳保費：' + premiums[idx].toLocaleString());
                        }
                    }
                }
            });
        }

        // --- 同齡層/市場對比（簡易版）---
        function renderPeerCompare() {
            const el = document.getElementById('peerCompareResult');
            if (!el) return;
            // 假設同齡層/市場平均資料（實際應串接API或資料庫）
            const peer = { gap: 1200000, coverage: 3000000, premium: 40000 };
            const userGap = analysisData.dimeGap || 0;
            const userCoverage = analysisData.totalCoverage || 0;
            const userPremium = analysisData.annualPremium || 0;
            let html = `<ul>`;
            html += `<li>您的保障缺口：<b>${userGap.toLocaleString()}</b> NTD</li>`;
            html += `<li>同齡層平均缺口：<b>${peer.gap.toLocaleString()}</b> NTD</li>`;
            html += `<li>您的總保額：<b>${userCoverage.toLocaleString()}</b> NTD</li>`;
            html += `<li>同齡層平均保額：<b>${peer.coverage.toLocaleString()}</b> NTD</li>`;
            html += `<li>您的年繳保費：<b>${userPremium.toLocaleString()}</b> NTD</li>`;
            html += `<li>同齡層平均年繳保費：<b>${peer.premium.toLocaleString()}</b> NTD</li>`;
            html += `</ul>`;
            el.innerHTML = html;
        }
        setTimeout(renderPeerCompare, 1000);
        // Global variables for data and chart instances
        let analysisData = {
            // Inputs from tab-0
            clientName: '', clientAge: 0, annualIncome: 0, familyStatus: 'single',
            totalCoverage: 0, totalPremium: 0, annualPremium: 0,
            coverageItems: 0, duplicateItems: 0, totalItems: 0,
            medicalInsurance: 0, lifeInsurance: 0, savingsInsurance: 0, accidentInsurance: 0, otherInsurance: 0,
            eduGap: false, incomeGap: false, careGap: false, retirementGap: false,

            // Results of Policy Health Check
            totalScore: 0, leverageRatio: 0, coverageRatio: 0, efficiencyScore: 0, premiumStress: 0,

            // DIME analysis
            dimeDebt: 0, dimeIncomeYears: 0, dimeIncomeAnnual: 0, dimeMortgage: 0, dimeEducation: 0, dimeCurrentLifeInsurance: 0,
            dimeTotalDemand: 0, dimeGap: 0,

            // Medical/LTC analysis
            medLTC_age: 0, medLTC_lifeExpectancy: 0, medLTC_annualMedicalCost: 0, medLTC_ltcYears: 0, medLTC_annualLTCcost: 0, medLTC_currentCoverage: 0,
            estimatedMedicalCost: 0, estimatedLTCCost: 0, totalMedicalLTCDemand: 0, medicalLTCDifference: 0,

            // Premium Health & CPV
            ph_annualHouseholdIncome: 0, ph_annualTotalPremium: 0, ph_mainCoverageAmount: 0, ph_premiumPerCoverage: 0,
            premiumPercentage: 0, cpvValue: 0,

            // Cash Value Analysis
            cv_annualPremium: 0, cv_paymentYears: 0, cv_expectedReturnRate: 0, cv_inflationRate: 0, cv_analysisYears: 0,
            totalPremiumPaid: 0, finalCashValue: 0, finalRealValue: 0, irrValue: 0,

            recommendations: []
        };

        // Chart instances
        let radarChartInstance, pieChartInstance, trendChartInstance, lifetimeTimelineInstance;
        let dimeChartInstance, cashValueChartInstance;
        let scene, camera, renderer, medicalLTC3DChartContainer;

        // --- Tab Switching Logic ---
        function switchTab(index) {
            const tabs = document.querySelectorAll('.tab');
            const contents = document.querySelectorAll('.tab-content');

            tabs.forEach((tab, i) => {
                if (i === index) {
                    tab.classList.add('active');
                    contents[i].classList.add('active');
                } else {
                    tab.classList.remove('active');
                    contents[i].classList.remove('active');
                }
            });

            // Specific actions on tab switch
            if (index === 2) { // Medical/LTC tab
                if (!scene) { // Initialize 3D chart only once
                    init3DMedicalChart();
                }
                // Ensure the 3D chart is rendered if it's visible
                if (scene) animate3DMedicalChart();
            } else if (index === 5) { // Comprehensive Report tab
                // Ensure results are visible when switching to this tab manually
                document.getElementById('resultsSection').style.display = 'block';
                // Redraw charts to ensure they render correctly if tab was hidden
                if (radarChartInstance) radarChartInstance.resize();
                if (pieChartInstance) pieChartInstance.resize();
                if (trendChartInstance) trendChartInstance.resize();
                if (lifetimeTimelineInstance) lifetimeTimelineInstance.resize();
            }
        }

        // --- Data Input and Validation ---
        function getInputValue(id, type = 'number', defaultValue = 0) {
            const element = document.getElementById(id);
            if (!element) return defaultValue;
            if (type === 'number') {
                const value = parseFloat(element.value);
                return isNaN(value) ? defaultValue : value;
            } else if (type === 'text') {
                return element.value.trim();
            } else if (type === 'boolean') {
                return element.checked;
            }
            return defaultValue;
        }

        function collectInputs() {
            // General Inputs
            analysisData.clientName = getInputValue('clientName', 'text');
            analysisData.clientAge = getInputValue('clientAge');
            analysisData.annualIncome = getInputValue('annualIncome');
            analysisData.familyStatus = getInputValue('familyStatus', 'text');

            analysisData.totalCoverage = getInputValue('totalCoverage');
            analysisData.totalPremium = getInputValue('totalPremium');
            analysisData.annualPremium = getInputValue('annualPremium');
            analysisData.coverageItems = getInputValue('coverageItems');
            analysisData.duplicateItems = getInputValue('duplicateItems');
            analysisData.totalItems = getInputValue('totalItems');

            analysisData.medicalInsurance = getInputValue('medicalInsurance');
            analysisData.lifeInsurance = getInputValue('lifeInsurance');
            analysisData.savingsInsurance = getInputValue('savingsInsurance');
            analysisData.accidentInsurance = getInputValue('accidentInsurance');
            analysisData.otherInsurance = getInputValue('otherInsurance');

            analysisData.eduGap = getInputValue('eduGap', 'boolean');
            analysisData.incomeGap = getInputValue('incomeGap', 'boolean');
            analysisData.careGap = getInputValue('careGap', 'boolean');
            analysisData.retirementGap = getInputValue('retirementGap', 'boolean');

            // DIME Inputs
            analysisData.dimeDebt = getInputValue('dimeDebt');
            analysisData.dimeIncomeYears = getInputValue('dimeIncomeYears');
            analysisData.dimeIncomeAnnual = getInputValue('dimeIncomeAnnual');
            analysisData.dimeMortgage = getInputValue('dimeMortgage');
            analysisData.dimeEducation = getInputValue('dimeEducation');
            analysisData.dimeCurrentLifeInsurance = getInputValue('dimeCurrentLifeInsurance');

            // Medical/LTC Inputs
            analysisData.medLTC_age = getInputValue('medLTC_age');
            analysisData.medLTC_lifeExpectancy = getInputValue('medLTC_lifeExpectancy');
            analysisData.medLTC_annualMedicalCost = getInputValue('medLTC_annualMedicalCost');
            analysisData.medLTC_ltcYears = getInputValue('medLTC_ltcYears');
            analysisData.medLTC_annualLTCcost = getInputValue('medLTC_annualLTCcost');
            analysisData.medLTC_currentCoverage = getInputValue('medLTC_currentCoverage');

            // Premium Health & CPV Inputs
            analysisData.ph_annualHouseholdIncome = getInputValue('ph_annualHouseholdIncome');
            analysisData.ph_annualTotalPremium = getInputValue('ph_annualTotalPremium');
            analysisData.ph_mainCoverageAmount = getInputValue('ph_mainCoverageAmount');
            analysisData.ph_premiumPerCoverage = getInputValue('ph_premiumPerCoverage');

            // Cash Value Analysis Inputs
            analysisData.cv_annualPremium = getInputValue('cv_annualPremium');
            analysisData.cv_paymentYears = getInputValue('cv_paymentYears');
            analysisData.cv_expectedReturnRate = getInputValue('cv_expectedReturnRate');
            analysisData.cv_inflationRate = getInputValue('cv_inflationRate');
            analysisData.cv_analysisYears = getInputValue('cv_analysisYears');
        }

        function validatePercentageSum() {
            const med = getInputValue('medicalInsurance');
            const life = getInputValue('lifeInsurance');
            const savings = getInputValue('savingsInsurance');
            const accident = getInputValue('accidentInsurance');
            const other = getInputValue('otherInsurance');
            const sum = med + life + savings + accident + other;
            const warningElement = document.getElementById('percentageSumWarning');

            if (sum !== 100 && sum !== 0) { // Allow 0 if nothing is entered, but warn if it's not 100
                warningElement.style.display = 'flex';
                return false;
            } else {
                warningElement.style.display = 'none';
                return true;
            }
        }

        // Event listeners for percentage inputs
        document.querySelectorAll('#tab-0 input[type="number"][id$="Insurance"]').forEach(input => {
            input.addEventListener('input', validatePercentageSum);
        });


        // --- Core Analysis Functions (Adapted from 保教分析2.html) ---

        function calculateLeverageScore(annualPremium, totalCoverage) {
            if (annualPremium === 0 || totalCoverage === 0) return 0;
            const ratio = totalCoverage / annualPremium;
            if (ratio >= 50) return 100;
            if (ratio >= 30) return 80;
            if (ratio >= 10) return 60;
            return 30;
        }

        function calculateCoverageScore(coverageItems, duplicateItems) {
            if (coverageItems === 0) return 0;
            const effectiveItems = coverageItems - duplicateItems;
            const duplicationRate = duplicateItems / coverageItems;
            if (duplicationRate <= 0.1 && effectiveItems >= 5) return 100;
            if (duplicationRate <= 0.2 && effectiveItems >= 3) return 80;
            if (duplicationRate <= 0.3 && effectiveItems >= 2) return 60;
            return 40;
        }

        function calculateEfficiencyScore(totalPremium, totalCoverage) {
            if (totalPremium === 0 || totalCoverage === 0) return 0;
            const costPerMillion = (totalPremium / totalCoverage) * 1000000;
            if (costPerMillion <= 50000) return 100; // Example threshold
            if (costPerMillion <= 100000) return 80;
            if (costPerMillion <= 200000) return 60;
            return 30;
        }

        function calculateStressScore(annualPremium, annualIncome) {
            if (annualIncome === 0) return 0;
            const percentage = (annualPremium / annualIncome) * 100;
            if (percentage <= 10) return 100;
            if (percentage <= 15) return 80;
            if (percentage <= 20) return 60;
            return 30;
        }

        function calculateProtectionGapsScore(eduGap, incomeGap, careGap, retirementGap) {
            let score = 100;
            if (eduGap) score -= 15;
            if (incomeGap) score -= 25;
            if (careGap) score -= 30;
            if (retirementGap) score -= 30;
            return Math.max(0, score);
        }

        function calculateTotalScore() {
            const { annualPremium, totalCoverage, coverageItems, duplicateItems, annualIncome,
                eduGap, incomeGap, careGap, retirementGap, totalPremium } = analysisData;

            const leverage = calculateLeverageScore(annualPremium, totalCoverage);
            const coverage = calculateCoverageScore(coverageItems, duplicateItems);
            const efficiency = calculateEfficiencyScore(totalPremium, totalCoverage);
            const stress = calculateStressScore(annualPremium, annualIncome);
            const gaps = calculateProtectionGapsScore(eduGap, incomeGap, careGap, retirementGap);

            // Weighted average example, adjust weights as needed
            const total = (leverage * 0.2) + (coverage * 0.2) + (efficiency * 0.2) + (stress * 0.2) + (gaps * 0.2);
            analysisData.leverageRatio = leverage;
            analysisData.coverageRatio = coverage;
            analysisData.efficiencyScore = efficiency;
            analysisData.premiumStress = stress;
            analysisData.totalScore = Math.round(total);
        }

        // --- DIME Analysis (Adapted from 保教分析.html) ---
        function calculateDIME() {
            const D = analysisData.dimeDebt;
            const I = analysisData.dimeIncomeYears * analysisData.dimeIncomeAnnual;
            const M = analysisData.dimeMortgage;
            const E = analysisData.dimeEducation;
            const currentLifeInsurance = analysisData.dimeCurrentLifeInsurance;

            const totalDemand = D + I + M + E;
            const gap = Math.max(0, totalDemand - currentLifeInsurance);

            analysisData.dimeTotalDemand = totalDemand;
            analysisData.dimeGap = gap;

            document.getElementById('dimeTotalDemand').innerText = totalDemand.toLocaleString();
            document.getElementById('dimeGap').innerText = gap.toLocaleString();
            updateDIMEChart();
        }

        function updateDIMEChart() {
            if (dimeChartInstance) dimeChartInstance.destroy();

            const ctx = document.getElementById('dimeChart').getContext('2d');
            dimeChartInstance = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: ['總壽險需求', '現有壽險', '壽險缺口'],
                    datasets: [{
                        label: '金額 (NTD)',
                        data: [analysisData.dimeTotalDemand, analysisData.dimeCurrentLifeInsurance, analysisData.dimeGap],
                        backgroundColor: ['#2563eb', '#10b981', '#ef4444'],
                        borderColor: ['#2563eb', '#10b981', '#ef4444'],
                        borderWidth: 1
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: { display: false },
                        title: {
                            display: true,
                            text: '壽險需求與缺口分析'
                        },
                        datalabels: {
                            anchor: 'end',
                            align: 'top',
                            formatter: (value) => value.toLocaleString(),
                            color: '#333'
                        }
                    },
                    scales: {
                        y: {
                            beginAtZero: true,
                            title: {
                                display: true,
                                text: '金額 (NTD)'
                            },
                            ticks: {
                                callback: function(value) {
                                    return value.toLocaleString();
                                }
                            }
                        }
                    }
                },
                plugins: [ChartDataLabels]
            });
        }

        // --- Medical/LTC Analysis (Adapted from 保教分析.html) ---
        function init3DMedicalChart() {
            medicalLTC3DChartContainer = document.getElementById('medicalLTC3DChart');
            if (!medicalLTC3DChartContainer) return; // Exit if container not found

            scene = new THREE.Scene();
            camera = new THREE.PerspectiveCamera(75, medicalLTC3DChartContainer.clientWidth / medicalLTC3DChartContainer.clientHeight, 0.1, 1000);
            renderer = new THREE.WebGLRenderer({ antialias: true, alpha: true }); // alpha: true for transparent background
            renderer.setSize(medicalLTC3DChartContainer.clientWidth, medicalLTC3DChartContainer.clientHeight);
            medicalLTC3DChartContainer.appendChild(renderer.domElement);

            camera.position.z = 5;

            // Add some basic lighting
            const ambientLight = new THREE.AmbientLight(0x404040); // Soft white light
            scene.add(ambientLight);
            const directionalLight = new THREE.DirectionalLight(0xffffff, 0.5);
            directionalLight.position.set(0, 1, 0);
            scene.add(directionalLight);
        }

        function animate3DMedicalChart() {
            if (!renderer) return; // Ensure renderer is initialized
            requestAnimationFrame(animate3DMedicalChart);

            // Simple animation: rotate the cube
            if (scene.children.length > 2) { // Check if cube is added (ambient light + directional light + cube)
                const cube = scene.children[2]; // Assuming the cube is the third child
                cube.rotation.x += 0.005;
                cube.rotation.y += 0.005;
            }

            renderer.render(scene, camera);
        }

        function calculateMedicalLTC() {
            const age = analysisData.medLTC_age;
            const lifeExpectancy = analysisData.medLTC_lifeExpectancy;
            const annualMedicalCost = analysisData.medLTC_annualMedicalCost;
            const ltcYears = analysisData.medLTC_ltcYears;
            const annualLTCcost = analysisData.medLTC_annualLTCcost;
            const currentCoverage = analysisData.medLTC_currentCoverage;

            const remainingLifeYears = Math.max(0, lifeExpectancy - age);
            const estimatedMedicalCost = remainingLifeYears * annualMedicalCost;
            const estimatedLTCCost = ltcYears * annualLTCcost;
            const totalDemand = estimatedMedicalCost + estimatedLTCCost;
            const difference = Math.max(0, totalDemand - currentCoverage);

            analysisData.estimatedMedicalCost = estimatedMedicalCost;
            analysisData.estimatedLTCCost = estimatedLTCCost;
            analysisData.totalMedicalLTCDemand = totalDemand;
            analysisData.medicalLTCDifference = difference;

            document.getElementById('estimatedMedicalCost').innerText = estimatedMedicalCost.toLocaleString();
            document.getElementById('estimatedLTCCost').innerText = estimatedLTCCost.toLocaleString();
            document.getElementById('totalMedicalLTCDemand').innerText = totalDemand.toLocaleString();
            document.getElementById('medicalLTCDifference').innerText = difference.toLocaleString();

            create3DMedicalChart(totalDemand, currentCoverage, difference);
        }

        function create3DMedicalChart(totalDemand, currentCoverage, difference) {
            if (!scene || !renderer) {
                init3DMedicalChart(); // Re-initialize if not done
                if (!scene || !renderer) return; // Still not initialized, something went wrong
            }

            // Clear previous objects (except lights)
            while (scene.children.length > 2) { // Keep ambient and directional light
                scene.remove(scene.children[2]);
            }

            // Represent values with different sized boxes/objects
            const materialDemand = new THREE.MeshBasicMaterial({ color: 0x2563eb, transparent: true, opacity: 0.7 });
            const materialCoverage = new THREE.MeshBasicMaterial({ color: 0x10b981, transparent: true, opacity: 0.7 });
            const materialDifference = new THREE.MeshBasicMaterial({ color: 0xef4444, transparent: true, opacity: 0.7 });

            // Scale factor for visualization (adjust as needed)
            const scaleFactor = 0.000005;

            // Demand cube
            if (totalDemand > 0) {
                const geometryDemand = new THREE.BoxGeometry(1, 1, 1);
                const cubeDemand = new THREE.Mesh(geometryDemand, materialDemand);
                cubeDemand.scale.setScalar(totalDemand * scaleFactor);
                cubeDemand.position.x = -1.5;
                scene.add(cubeDemand);
            }

            // Coverage cube
            if (currentCoverage > 0) {
                const geometryCoverage = new THREE.BoxGeometry(1, 1, 1);
                const cubeCoverage = new THREE.Mesh(geometryCoverage, materialCoverage);
                cubeCoverage.scale.setScalar(currentCoverage * scaleFactor);
                cubeCoverage.position.x = 0;
                scene.add(cubeCoverage);
            }

            // Difference cube
            if (difference > 0) {
                const geometryDifference = new THREE.BoxGeometry(1, 1, 1);
                const cubeDifference = new THREE.Mesh(geometryDifference, materialDifference);
                cubeDifference.scale.setScalar(difference * scaleFactor);
                cubeDifference.position.x = 1.5;
                scene.add(cubeDifference);
            }

            // Add labels (using DOM elements for simplicity or advanced Three.js text)
            // For now, only visual cubes, text labels are more complex with Three.js.
            // A simple DOM overlay could be used for labels.

            animate3DMedicalChart(); // Start or restart animation
        }


        // --- Premium Health & CPV (Adapted from 保教分析.html) ---
        function calculatePremiumHealthCPV() {
            const annualHouseholdIncome = analysisData.ph_annualHouseholdIncome;
            const annualTotalPremium = analysisData.ph_annualTotalPremium;
            const mainCoverageAmount = analysisData.ph_mainCoverageAmount;
            const premiumPerCoverage = analysisData.ph_premiumPerCoverage;

            // Premium Health
            let premiumPercentage = 0;
            if (annualHouseholdIncome > 0) {
                premiumPercentage = (annualTotalPremium / annualHouseholdIncome) * 100;
            }
            analysisData.premiumPercentage = premiumPercentage;
            document.getElementById('premiumPercentage').innerText = premiumPercentage.toFixed(2) + '%';

            const premiumHealthFill = document.getElementById('premiumHealthFill');
            let healthStatus = '';
            let fillWidth = 0; // percentage for the meter

            if (premiumPercentage <= 10) {
                healthStatus = '非常良好 (保費佔收入比例低於10%)';
                fillWidth = Math.min(100, (premiumPercentage / 10) * 33.3); // Scale to first third of bar
            } else if (premiumPercentage <= 15) {
                healthStatus = '良好 (保費佔收入比例10%-15%)';
                fillWidth = Math.min(100, 33.3 + ((premiumPercentage - 10) / 5) * 33.3); // Scale to middle third
            } else if (premiumPercentage <= 20) {
                healthStatus = '一般 (保費佔收入比例15%-20%)';
                fillWidth = Math.min(100, 66.6 + ((premiumPercentage - 15) / 5) * 33.3); // Scale to last third
            } else {
                healthStatus = '需調整 (保費佔收入比例超過20%)';
                fillWidth = 100; // Full bar, implies over budget
            }
            premiumHealthFill.style.width = fillWidth + '%';
            document.getElementById('premiumHealthStatus').innerText = '狀態: ' + healthStatus;

            // CPV (Cost-Performance Value)
            let cpvValue = 0;
            if (mainCoverageAmount > 0 && premiumPerCoverage > 0) {
                // CPV = (Main Coverage Amount / (Premium per Coverage * 1,000,000))
                cpvValue = (mainCoverageAmount / (premiumPerCoverage * 1000000)) * 1000; // Scale to a more readable number
            }
            analysisData.cpvValue = cpvValue;
            document.getElementById('cpvValue').innerText = cpvValue.toFixed(2);

            const cpvFill = document.getElementById('cpvFill');
            let cpvStatus = '';
            let cpvFillWidth = 0; // percentage for the meter

            if (cpvValue >= 10) { // High CPV
                cpvStatus = '極佳 (每百萬保障保費效率高)';
                cpvFillWidth = 100;
                cpvFill.style.backgroundColor = varColor('--success-color');
            } else if (cpvValue >= 5) { // Medium CPV
                cpvStatus = '良好 (CP值適中)';
                cpvFillWidth = 75;
                cpvFill.style.backgroundColor = varColor('--primary-color');
            } else if (cpvValue >= 2) { // Low CPV
                cpvStatus = '一般 (CP值偏低，可考慮優化)';
                cpvFillWidth = 50;
                cpvFill.style.backgroundColor = varColor('--warning-color');
            } else { // Very Low CPV
                cpvStatus = '較差 (CP值過低，急需檢視)';
                cpvFillWidth = 25;
                cpvFill.style.backgroundColor = varColor('--danger-color');
            }
            cpvFill.style.width = cpvFillWidth + '%';
            document.getElementById('cpvStatus').innerText = 'CP值狀態: ' + cpvStatus;
        }

        // Helper to get CSS variable
        function varColor(variableName) {
            return getComputedStyle(document.documentElement).getPropertyValue(variableName).trim();
        }

        // --- Cash Value Analysis (Adapted from 保教分析.html) ---
        function analyzeCashValue() {
            const annualPremium = analysisData.cv_annualPremium;
            const paymentYears = analysisData.cv_paymentYears;
            const expectedReturnRate = analysisData.cv_expectedReturnRate / 100; // Convert to decimal
            const inflationRate = analysisData.cv_inflationRate / 100; // Convert to decimal
            const analysisYears = analysisData.cv_analysisYears;

            const labels = [];
            const cashValues = [];
            const realValues = [];
            let currentCashValue = 0;
            let totalPremiumPaid = 0;
            let cashFlows = []; // For IRR calculation

            for (let year = 1; year <= analysisYears; year++) {
                labels.push(`第 ${year} 年`);

                if (year <= paymentYears) {
                    currentCashValue += annualPremium;
                    totalPremiumPaid += annualPremium;
                    cashFlows.push(-annualPremium); // Outflow for IRR
                } else {
                    cashFlows.push(0); // No premium paid
                }
                currentCashValue *= (1 + expectedReturnRate);
                cashValues.push(currentCashValue);

                const realValue = currentCashValue / Math.pow(1 + inflationRate, year);
                realValues.push(realValue);
            }
            cashFlows[cashFlows.length - 1] += currentCashValue; // Add final cash value as inflow

            analysisData.totalPremiumPaid = totalPremiumPaid;
            analysisData.finalCashValue = currentCashValue;
            analysisData.finalRealValue = realValues[realValues.length - 1];
            analysisData.irrValue = calculateIRR(cashFlows) * 100; // Convert to percentage

            document.getElementById('totalPremiumPaid').innerText = totalPremiumPaid.toLocaleString();
            document.getElementById('finalCashValue').innerText = currentCashValue.toLocaleString();
            document.getElementById('finalRealValue').innerText = realValues[realValues.length - 1].toLocaleString();
            document.getElementById('irrValue').innerText = analysisData.irrValue.toFixed(2) + '%';

            updateCashValueChart(labels, cashValues, realValues);
        }

        function updateCashValueChart(labels, cashValues, realValues) {
            if (cashValueChartInstance) cashValueChartInstance.destroy();

            const ctx = document.getElementById('cashValueChart').getContext('2d');
            cashValueChartInstance = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: labels,
                    datasets: [
                        {
                            label: '現金價值 (未考慮通膨)',
                            data: cashValues,
                            borderColor: '#2563eb',
                            backgroundColor: 'rgba(37, 99, 235, 0.2)',
                            fill: true,
                            tension: 0.1
                        },
                        {
                            label: '實質現金價值 (考慮通膨)',
                            data: realValues,
                            borderColor: '#ef4444',
                            backgroundColor: 'rgba(239, 68, 68, 0.2)',
                            fill: true,
                            tension: 0.1
                        }
                    ]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: { position: 'top' },
                        title: {
                            display: true,
                            text: '現金價值與實質價值成長趨勢'
                        },
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    return context.dataset.label + ': ' + context.raw.toLocaleString() + ' NTD';
                                }
                            }
                        }
                    },
                    scales: {
                        x: {
                            title: {
                                display: true,
                                text: '年期'
                            }
                        },
                        y: {
                            beginAtZero: true,
                            title: {
                                display: true,
                                text: '金額 (NTD)'
                            },
                            ticks: {
                                callback: function(value) {
                                    return value.toLocaleString();
                                }
                            }
                        }
                    }
                }
            });
        }

        // Helper for IRR calculation (Newton-Raphson method)
        function calculateIRR(cashFlows) {
            const MAX_ITERATIONS = 100;
            const ACCURACY = 1e-7;

            let irr = 0.1; // Initial guess for IRR

            for (let i = 0; i < MAX_ITERATIONS; i++) {
                let npv = 0;
                let derivative = 0;
                for (let j = 0; j < cashFlows.length; j++) {
                    npv += cashFlows[j] / Math.pow(1 + irr, j);
                    derivative -= j * cashFlows[j] / Math.pow(1 + irr, j + 1);
                }

                if (Math.abs(npv) < ACCURACY) {
                    return irr;
                }

                irr = irr - npv / derivative;
            }
            return NaN; // Could not converge
        }


        // --- Chart Drawing Functions (Adapted from 保教分析2.html, using Echarts and Chart.js) ---

        function drawScoreGauge(score, elementId) {
            const chartDom = document.getElementById(elementId);
            const myChart = echarts.init(chartDom);
            const option = {
                series: [
                    {
                        type: 'gauge',
                        startAngle: 180,
                        endAngle: 0,
                        min: 0,
                        max: 100,
                        splitNumber: 5,
                        itemStyle: {
                            color: varColor('--primary-color')
                        },
                        progress: {
                            show: true,
                            width: 15
                        },
                        axisLine: {
                            lineStyle: {
                                width: 15
                            }
                        },
                        axisTick: {
                            show: false
                        },
                        splitLine: {
                            length: 10,
                            lineStyle: {
                                width: 2,
                                color: '#999'
                            }
                        },
                        axisLabel: {
                            distance: 20,
                            color: varColor('--text-light'),
                            fontSize: 12
                        },
                        anchor: {
                            show: true,
                            showAbove: true,
                            size: 15,
                            itemStyle: {
                                color: varColor('--primary-color')
                            }
                        },
                        title: {
                            show: false
                        },
                        detail: {
                            valueAnimation: true,
                            fontSize: 25,
                            offsetCenter: [0, '70%'],
                            formatter: '{value}',
                            color: varColor('--secondary-color')
                        },
                        data: [{
                            value: score
                        }]
                    }
                ]
            };
            myChart.setOption(option);
            return myChart; // Return instance for resizing
        }

        function drawRadarChart() {
            if (radarChartInstance) radarChartInstance.dispose(); // Use dispose for Echarts

            const chartDom = document.getElementById('radarChart');
            radarChartInstance = echarts.init(chartDom);

            const { leverageRatio, coverageRatio, efficiencyScore, premiumStress, totalScore } = analysisData;

            const option = {
                radar: {
                    indicator: [
                        { name: '槓桿比', max: 100 },
                        { name: '覆蓋率', max: 100 },
                        { name: '效率', max: 100 },
                        { name: '保費壓力', max: 100 },
                        { name: '綜合缺口', max: 100 }
                    ],
                    radius: '65%',
                    axisName: {
                        color: varColor('--text-dark'),
                        fontSize: 14
                    },
                    splitArea: {
                        areaStyle: {
                            color: ['#f2f7ff', '#eaf2ff', '#e2edff', '#dae8ff', '#d2e3ff']
                        }
                    },
                    splitLine: {
                        lineStyle: {
                            color: varColor('--border-color')
                        }
                    }
                },
                series: [
                    {
                        name: '保單綜合分析',
                        type: 'radar',
                        data: [
                            {
                                value: [
                                    leverageRatio,
                                    coverageRatio,
                                    efficiencyScore,
                                    100 - premiumStress, // Invert stress for better radar representation
                                    100 - (analysisData.totalScore * 0.2 / 20) * 100 // Example: Gaps score (needs re-calculation for this display)
                                ],
                                name: '當前分數',
                                areaStyle: {
                                    opacity: 0.7,
                                    color: varColor('--primary-color')
                                },
                                lineStyle: {
                                    color: varColor('--primary-color')
                                },
                                itemStyle: {
                                    color: varColor('--primary-color')
                                }
                            }
                        ],
                        symbol: 'none',
                        label: {
                            show: true,
                            formatter: '{c}',
                            color: varColor('--secondary-color')
                        }
                    }
                ]
            };
            radarChartInstance.setOption(option);
            window.addEventListener('resize', radarChartInstance.resize); // Ensure resize on window resize
        }

        function drawPieChart() {
            if (pieChartInstance) pieChartInstance.destroy(); // Use destroy for Chart.js

            const ctx = document.getElementById('pieChart').getContext('2d');
            const { medicalInsurance, lifeInsurance, savingsInsurance, accidentInsurance, otherInsurance } = analysisData;

            pieChartInstance = new Chart(ctx, {
                type: 'pie',
                data: {
                    labels: ['醫療險', '壽險', '儲蓄險', '意外險', '其他險'],
                    datasets: [{
                        data: [medicalInsurance, lifeInsurance, savingsInsurance, accidentInsurance, otherInsurance],
                        backgroundColor: [
                            '#2563eb', // primary
                            '#10b981', // success
                            '#f59e0b', // warning
                            '#ef4444', // danger
                            '#64748b'  // text-light
                        ],
                        hoverOffset: 10
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: { position: 'right' },
                        title: {
                            display: true,
                            text: '保單類型年繳保費配置比例'
                        },
                        datalabels: {
                            formatter: (value, ctx) => {
                                let sum = 0;
                                let dataArr = ctx.chart.data.datasets[0].data;
                                dataArr.map(data => {
                                    sum += data;
                                });
                                let percentage = (value * 100 / sum).toFixed(2) + '%';
                                return percentage;
                            },
                            color: '#fff',
                            textShadowColor: 'rgba(0,0,0,0.5)',
                            textShadowBlur: 4,
                            font: {
                                weight: 'bold'
                            }
                        }
                    }
                },
                plugins: [ChartDataLabels]
            });
        }

        function drawTrendChart() {
            if (trendChartInstance) trendChartInstance.destroy();

            const ctx = document.getElementById('trendChart').getContext('2d');
            const years = Array.from({ length: 10 }, (_, i) => `第 ${i + 1} 年`); // Example: 10 years trend
            const leverageData = years.map(() => Math.floor(Math.random() * 50) + 50); // Example random data
            const premiumData = years.map(() => Math.floor(Math.random() * 50000) + 100000); // Example random data

            trendChartInstance = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: years,
                    datasets: [
                        {
                            label: '保費槓桿比 (分數)',
                            data: leverageData,
                            borderColor: '#2563eb',
                            backgroundColor: 'rgba(37, 99, 235, 0.2)',
                            yAxisID: 'y',
                            tension: 0.3,
                            fill: true
                        },
                        {
                            label: '年繳保費支出 (NTD)',
                            data: premiumData,
                            borderColor: '#ef4444',
                            backgroundColor: 'rgba(239, 68, 68, 0.2)',
                            yAxisID: 'y1',
                            tension: 0.3,
                            fill: false
                        }
                    ]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    interaction: {
                        mode: 'index',
                        intersect: false
                    },
                    plugins: {
                        title: {
                            display: true,
                            text: '保費槓桿比與保費支出年度趨勢模擬'
                        },
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    let label = context.dataset.label || '';
                                    if (label) {
                                        label += ': ';
                                    }
                                    if (context.dataset.yAxisID === 'y') {
                                        label += context.raw + ' 分';
                                    } else {
                                        label += context.raw.toLocaleString() + ' NTD';
                                    }
                                    return label;
                                }
                            }
                        }
                    },
                    scales: {
                        x: {
                            title: {
                                display: true,
                                text: '年度'
                            }
                        },
                        y: {
                            type: 'linear',
                            display: true,
                            position: 'left',
                            title: {
                                display: true,
                                text: '槓桿比分數'
                            },
                            min: 0,
                            max: 100
                        },
                        y1: {
                            type: 'linear',
                            display: true,
                            position: 'right',
                            title: {
                                display: true,
                                text: '年繳保費 (NTD)'
                            },
                            grid: {
                                drawOnChartArea: false
                            },
                            ticks: {
                                callback: function(value) {
                                    return value.toLocaleString();
                                }
                            }
                        }
                    }
                }
            });
        }

        function drawLifetimeTimeline() {
            if (lifetimeTimelineInstance) lifetimeTimelineInstance.destroy();

            const ctx = document.getElementById('lifetimeTimeline').getContext('2d');
            const currentAge = analysisData.clientAge || 30; // Default if not provided
            const labels = [];
            const dataPoints = [];
            const backgroundColors = [];
            const borderColors = [];

            // Define key life stages/events
            const events = [
                { age: 25, event: '工作起步', color: '#64748b' },
                { age: 30, event: '成家立業', color: '#2563eb' },
                { age: 40, event: '子女教育', color: '#f59e0b' },
                { age: 50, event: '事業高峰/退休準備', color: '#10b981' },
                { age: 60, event: '退休生活', color: '#ef4444' },
                { age: 70, event: '樂齡照顧', color: '#8b5cf6' } // Purple for care
            ];

            // Add events based on user's current age
            const relevantEvents = events.filter(e => e.age >= currentAge - 5 && e.age <= currentAge + 40); // Show a range around current age
            relevantEvents.forEach(event => {
                labels.push(`${event.age}歲\n${event.event}`);
                dataPoints.push(1); // Dummy data point for visualization
                backgroundColors.push(event.color + '80'); // 80 for opacity
                borderColors.push(event.color);
            });

            // Add protection gaps as annotations/additional data if they exist
            if (analysisData.eduGap) {
                labels.push('教育金缺口');
                dataPoints.push(0.8);
                backgroundColors.push('rgba(255, 99, 132, 0.5)');
                borderColors.push('rgb(255, 99, 132)');
            }
            if (analysisData.incomeGap) {
                labels.push('收入補償缺口');
                dataPoints.push(0.8);
                backgroundColors.push('rgba(255, 159, 64, 0.5)');
                borderColors.push('rgb(255, 159, 64)');
            }
            if (analysisData.careGap) {
                labels.push('長照缺口');
                dataPoints.push(0.8);
                backgroundColors.push('rgba(75, 192, 192, 0.5)');
                borderColors.push('rgb(75, 192, 192)');
            }
            if (analysisData.retirementGap) {
                labels.push('退休金缺口');
                dataPoints.push(0.8);
                backgroundColors.push('rgba(153, 102, 255, 0.5)');
                borderColors.push('rgb(153, 102, 255)');
            }


            lifetimeTimelineInstance = new Chart(ctx, {
                type: 'bar', // Using bar chart for timeline visualization
                data: {
                    labels: labels,
                    datasets: [{
                        label: '人生事件與保障缺口',
                        data: dataPoints,
                        backgroundColor: backgroundColors,
                        borderColor: borderColors,
                        borderWidth: 1
                    }]
                },
                options: {
                    indexAxis: 'y', // Horizontal bars
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: { display: false },
                        title: {
                            display: true,
                            text: `人生階段目標與保障缺口時間軸 (以${currentAge}歲為中心)`
                        },
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    return context.label;
                                }
                            }
                        }
                    },
                    scales: {
                        x: {
                            display: false // Hide x-axis
                        },
                        y: {
                            grid: {
                                display: false // Hide y-axis grid lines
                            }
                        }
                    }
                }
            });
        }


        // --- Recommendation Generation (Adapted from 保教分析2.html) ---
        function generateRecommendations() {
            analysisData.recommendations = []; // Clear previous recommendations
            const { totalScore, leverageRatio, coverageRatio, efficiencyScore, premiumStress,
                eduGap, incomeGap, careGap, retirementGap, annualIncome, annualPremium, totalCoverage } = analysisData;

            if (totalScore < 60) {
                analysisData.recommendations.push({ item: '整體保單檢視', description: '您的保單總體健康度較低，建議進行全面檢視與調整。' });
            } else if (totalScore < 80) {
                analysisData.recommendations.push({ item: '保單優化', description: '您的保單健康度良好，但仍有優化空間，建議針對弱項加強。' });
            } else {
                analysisData.recommendations.push({ item: '持續保持', description: '您的保單非常健康，請持續保持良好的保險規劃。' });
            }

            if (leverageRatio < 60) {
                analysisData.recommendations.push({ item: '提高保額', description: '保費槓桿比偏低，考慮以較低保費換取更高保障的產品，例如定期壽險。' });
            }
            if (coverageRatio < 60) {
                analysisData.recommendations.push({ item: '擴增保障範圍', description: '理賠覆蓋率不足，建議補足醫療、癌症、失能等主要保障。' });
            }
            if (efficiencyScore < 60) {
                analysisData.recommendations.push({ item: '優化保單結構', description: '保單效率有待提升，檢查是否存在重複購買或高保費低保障的產品。' });
            }
            if (premiumStress < 60) { // Inverted score (lower is better for stress)
                analysisData.recommendations.push({ item: '合理化保費支出', description: '保費佔收入比例過高，建議檢視保費負擔是否合理，避免影響生活品質。' });
            }

            if (eduGap) {
                analysisData.recommendations.push({ item: '教育金規劃', description: '存在子女教育金缺口，建議提早規劃，考慮儲蓄險或教育基金。' });
            }
            if (incomeGap) {
                analysisData.recommendations.push({ item: '收入補償規劃', description: '存在收入補償缺口，建議增加定期壽險或失能險保額，保障家庭收入來源。' });
            }
            if (careGap) {
                analysisData.recommendations.push({ item: '長期照顧規劃', description: '存在長期照顧缺口，考慮購買長期照顧險或重大傷病險，以應對高額醫療與照護費用。' });
            }
            if (retirementGap) {
                analysisData.recommendations.push({ item: '退休金規劃', description: '存在退休金缺口，建議提早開始退休金儲備，如年金險或投資型保單。' });
            }

            // General financial health check
            if (annualIncome > 0 && annualPremium / annualIncome > 0.2) {
                analysisData.recommendations.push({ item: '財務壓力預警', description: `您的年繳保費佔年收入 ${((annualPremium / annualIncome) * 100).toFixed(2)}%，可能存在財務壓力，建議審慎評估。` });
            }
            if (totalCoverage < annualIncome * 10) { // Example: 10x income coverage
                 analysisData.recommendations.push({ item: '保障額度不足', description: `您的總保額 ${totalCoverage.toLocaleString()} NTD 相對於年收入 ${annualIncome.toLocaleString()} NTD 而言可能不足，建議提高。` });
            }

            populateRecommendationTable();
        }

        function populateRecommendationTable() {
            const tableBody = document.getElementById('recommendationTable').getElementsByTagName('tbody')[0];
            tableBody.innerHTML = ''; // Clear existing rows

            if (analysisData.recommendations.length === 0) {
                const row = tableBody.insertRow();
                const cell = row.insertCell();
                cell.colSpan = 2;
                cell.innerText = '目前無特定優化建議，您的保單規劃良好。';
                cell.style.textAlign = 'center';
                cell.style.color = varColor('--text-light');
            } else {
                analysisData.recommendations.forEach(rec => {
                    const row = tableBody.insertRow();
                    const itemCell = row.insertCell();
                    const descCell = row.insertCell();
                    itemCell.innerText = rec.item;
                    descCell.innerText = rec.description;
                });
            }
        }

        // --- UI Update and Reset ---
        function updateResultsUI() {
            document.getElementById('totalScoreValue').innerText = analysisData.totalScore + '分';
            document.getElementById('leverageRatioValue').innerText = analysisData.leverageRatio + '分';
            document.getElementById('coverageRatioValue').innerText = analysisData.coverageRatio + '分';
            document.getElementById('efficiencyScoreValue').innerText = analysisData.efficiencyScore + '分';
            document.getElementById('premiumStressValue').innerText = analysisData.premiumStress + '分';

            // Draw Charts
            drawRadarChart();
            drawPieChart();
            drawTrendChart();
            drawLifetimeTimeline();

            generateRecommendations(); // Generate and populate recommendations
            document.getElementById('resultsSection').style.display = 'block';
        }

        function runAllAnalyses() {
            collectInputs(); // Gather all input data

            // Validate percentage sum before proceeding with main analysis
            if (!validatePercentageSum()) {
                alert('保單類型配置的百分比總和必須為100%！');
                return;
            }

            // Execute all analysis functions
            calculateTotalScore(); // Policy Health Check
            calculateDIME(); // Life Insurance Gap
            calculateMedicalLTC(); // Medical/LTC
            calculatePremiumHealthCPV(); // Premium Health & CPV
            analyzeCashValue(); // Cash Value Analysis

            updateResultsUI(); // Update Policy Health Check results UI
            switchTab(5); // Switch to the comprehensive report tab
        }

        function resetForm() {
            document.getElementById('clientName').value = "";
            document.getElementById('clientAge').value = "";
            document.getElementById('annualIncome').value = "";
            document.getElementById('familyStatus').value = "single";

            document.getElementById('totalCoverage').value = "";
            document.getElementById('totalPremium').value = "";
            document.getElementById('annualPremium').value = "";
            document.getElementById('coverageItems').value = "";
            document.getElementById('duplicateItems').value = "";
            document.getElementById('totalItems').value = "";

            document.getElementById('medicalInsurance').value = "";
            document.getElementById('lifeInsurance').value = "";
            document.getElementById('savingsInsurance').value = "";
            document.getElementById('accidentInsurance').value = "";
            document.getElementById('otherInsurance').value = "";
            document.getElementById('percentageSumWarning').style.display = 'none';

            document.getElementById('eduGap').checked = false;
            document.getElementById('incomeGap').checked = false;
            document.getElementById('careGap').checked = false;
            document.getElementById('retirementGap').checked = false;

            // Reset DIME inputs
            document.getElementById('dimeDebt').value = "0";
            document.getElementById('dimeIncomeYears').value = "10";
            document.getElementById('dimeIncomeAnnual').value = "0";
            document.getElementById('dimeMortgage').value = "0";
            document.getElementById('dimeEducation').value = "0";
            document.getElementById('dimeCurrentLifeInsurance').value = "0";
            document.getElementById('dimeTotalDemand').innerText = "0";
            document.getElementById('dimeGap').innerText = "0";
            if (dimeChartInstance) dimeChartInstance.destroy();

            // Reset Medical/LTC inputs
            document.getElementById('medLTC_age').value = "30";
            document.getElementById('medLTC_lifeExpectancy').value = "85";
            document.getElementById('medLTC_annualMedicalCost').value = "50000";
            document.getElementById('medLTC_ltcYears').value = "10";
            document.getElementById('medLTC_annualLTCcost').value = "300000";
            document.getElementById('medLTC_currentCoverage').value = "0";
            document.getElementById('estimatedMedicalCost').innerText = "0";
            document.getElementById('estimatedLTCCost').innerText = "0";
            document.getElementById('totalMedicalLTCDemand').innerText = "0";
            document.getElementById('medicalLTCDifference').innerText = "0";
            if (scene) {
                while (scene.children.length > 2) { scene.remove(scene.children[2]); } // Remove cubes
                renderer.render(scene, camera); // Re-render empty scene
            }

            // Reset Premium Health & CPV inputs
            document.getElementById('ph_annualHouseholdIncome').value = "0";
            document.getElementById('ph_annualTotalPremium').value = "0";
            document.getElementById('ph_mainCoverageAmount').value = "0";
            document.getElementById('ph_premiumPerCoverage').value = "0";
            document.getElementById('premiumPercentage').innerText = "0.00%";
            document.getElementById('premiumHealthFill').style.width = "0";
            document.getElementById('premiumHealthStatus').innerText = "狀態: 良好";
            document.getElementById('cpvValue').innerText = "0";
            document.getElementById('cpvFill').style.width = "0";
            document.getElementById('cpvStatus').innerText = "CP值狀態: 一般";

            // Reset Cash Value inputs
            document.getElementById('cv_annualPremium').value = "0";
            document.getElementById('cv_paymentYears').value = "20";
            document.getElementById('cv_expectedReturnRate').value = "2";
            document.getElementById('cv_inflationRate').value = "1.5";
            document.getElementById('cv_analysisYears').value = "30";
            document.getElementById('totalPremiumPaid').innerText = "0";
            document.getElementById('finalCashValue').innerText = "0";
            document.getElementById('finalRealValue').innerText = "0";
            document.getElementById('irrValue').innerText = "0.00%";
            if (cashValueChartInstance) cashValueChartInstance.destroy();

            // Reset analysisData object
            for (const key in analysisData) {
                if (typeof analysisData[key] === 'number') analysisData[key] = 0;
                if (typeof analysisData[key] === 'string') analysisData[key] = '';
                if (typeof analysisData[key] === 'boolean') analysisData[key] = false;
                if (Array.isArray(analysisData[key])) analysisData[key] = [];
            }
            analysisData.familyStatus = 'single';
            analysisData.dimeIncomeYears = 10;
            analysisData.medLTC_age = 30;
            analysisData.medLTC_lifeExpectancy = 85;
            analysisData.medLTC_annualMedicalCost = 50000;
            analysisData.medLTC_ltcYears = 10;
            analysisData.medLTC_annualLTCcost = 300000;
            analysisData.cv_paymentYears = 20;
            analysisData.cv_expectedReturnRate = 2;
            analysisData.cv_inflationRate = 1.5;
            analysisData.cv_analysisYears = 30;


            // Hide results section and clear tables/charts
            document.getElementById('resultsSection').style.display = 'none';
            document.getElementById('recommendationTable').getElementsByTagName('tbody')[0].innerHTML = '';

            // Destroy Chart.js instances if they exist
            if (radarChartInstance) radarChartInstance.dispose(); // Echarts uses dispose
            if (pieChartInstance) pieChartInstance.destroy();
            if (trendChartInstance) trendChartInstance.destroy();
            if (lifetimeTimelineInstance) lifetimeTimelineInstance.destroy();

            window.scrollTo({ top: 0, behavior: 'smooth' });
            switchTab(0); // Go back to the initial input tab
        }

        function printResults() {
            const printContent = document.getElementById('resultsSection');
            const printWindow = window.open('', '_blank');
            printWindow.document.write(`
                <!DOCTYPE html>
                <html lang="zh-TW">
                <head>
                    <meta charset="UTF-8">
                    <meta name="viewport" content="width=device-width, initial-scale=1.0">
                    <title>保險分析報告</title>
                    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
                    <style>
                        /* Print-specific styles, simplified from main styles */
                        body { font-family: 'Noto Sans TC', 'Arial', sans-serif; margin: 20px; color: #333; }
                        h1, h2, h3 { color: #2563eb; margin-bottom: 10px; }
                        .card { border: 1px solid #e2e8f0; padding: 20px; margin-bottom: 20px; border-radius: 8px; box-shadow: 0 2px 4px rgba(0,0,0,0.05); }
                        .results-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 15px; margin-bottom: 20px; }
                        .result-card { text-align: center; padding: 15px; border: 1px solid #e2e8f0; border-radius: 8px; }
                        .result-card .score { font-size: 2em; font-weight: bold; color: #2563eb; }
                        .chart-container { width: 100%; height: 350px; margin-bottom: 20px; }
                        table { width: 100%; border-collapse: collapse; margin-top: 15px; }
                        th, td { border: 1px solid #e2e8f0; padding: 10px; text-align: left; }
                        th { background-color: #f8fafc; }
                        /* Ensure charts render correctly in print */
                        canvas { max-width: 100%; height: auto !important; }
                        @media print {
                            body { background-color: #fff; }
                            .btn-group { display: none; }
                            .tab-content { display: block !important; }
                        }
                    </style>
                </head>
                <body>
                    <h1>保險綜合分析報告</h1>
                    <p>報告生成日期: ${new Date().toLocaleDateString('zh-TW', { year: 'numeric', month: 'long', day: 'numeric' })}</p>
                    <p>客戶姓名: ${analysisData.clientName || 'N/A'}</p>
                    <p>年齡: ${analysisData.clientAge || 'N/A'} 歲</p>
                    <hr style="margin: 20px 0; border-color: #e2e8f0;">
                    ${printContent.innerHTML}
                </body>
                </html>
            `);

            printWindow.document.close();

            // Wait for charts to render in the new window, then print
            setTimeout(() => {
                // Re-initialize charts in the print window if needed.
                // This is a common challenge for printing dynamically generated charts.
                // For Chart.js, ensure ChartDataLabels plugin is also available in printWindow if used.
                // For Echarts, you might need to copy the entire Echarts script or ensure it's loaded.
                // For simplicity, we assume the print window's environment is similar enough.
                printWindow.print();
                printWindow.close();
            }, 1000); // Increased timeout for charts to render
        }

        // --- Initial Load ---
        document.addEventListener('DOMContentLoaded', function() {
            switchTab(0); // Default to the first tab on load
        });
    </script>
</body>
</html>
