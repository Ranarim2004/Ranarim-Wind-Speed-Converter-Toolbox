# Ranarim-Wind-Speed-Converter-Toolbox
<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>测站风速换算工具 | Wind Speed Converter</title>
<style>
  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    font-family: 'Segoe UI', 'PingFang SC', 'Microsoft YaHei', sans-serif;
    background: linear-gradient(135deg, #0a1628 0%, #1a2a4a 50%, #0d1f3c 100%);
    min-height: 100vh;
    color: #e0e8f0;
    padding: 20px;
  }

  .container {
    max-width: 1200px;
    margin: 0 auto;
  }

  /* Header */
  .header {
    text-align: center;
    margin-bottom: 30px;
    padding: 30px 20px;
    background: rgba(255,255,255,0.03);
    border-radius: 16px;
    border: 1px solid rgba(100,180,255,0.15);
  }
  .header h1 {
    font-size: 28px;
    color: #7ec8ff;
    margin-bottom: 8px;
    letter-spacing: 1px;
  }
  .header p {
    color: #8aa8c8;
    font-size: 14px;
  }
  .header .formula-bar {
    margin-top: 15px;
    display: inline-block;
    background: rgba(30,60,100,0.6);
    padding: 10px 24px;
    border-radius: 8px;
    border: 1px solid rgba(100,180,255,0.2);
    font-family: 'Times New Roman', serif;
    font-size: 16px;
    color: #aed4ff;
  }

  /* Main grid */
  .main-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 24px;
    margin-bottom: 24px;
  }

  /* Card */
  .card {
    background: rgba(20,35,65,0.85);
    border-radius: 14px;
    padding: 24px;
    border: 1px solid rgba(100,180,255,0.12);
    backdrop-filter: blur(10px);
  }
  .card h2 {
    font-size: 18px;
    color: #7ec8ff;
    margin-bottom: 20px;
    display: flex;
    align-items: center;
    gap: 8px;
  }
  .card h2 .icon {
    width: 28px; height: 28px;
    display: inline-flex; align-items: center; justify-content: center;
    background: rgba(100,180,255,0.15);
    border-radius: 6px;
    font-size: 14px;
  }

  /* Form */
  .form-group {
    margin-bottom: 16px;
  }
  .form-group label {
    display: block;
    font-size: 13px;
    color: #8aa8c8;
    margin-bottom: 6px;
    font-weight: 500;
  }
  .form-group select,
  .form-group input {
    width: 100%;
    padding: 10px 14px;
    background: rgba(10,25,50,0.8);
    border: 1px solid rgba(100,180,255,0.2);
    border-radius: 8px;
    color: #e0e8f0;
    font-size: 14px;
    transition: border-color 0.3s, box-shadow 0.3s;
  }
  .form-group select:focus,
  .form-group input:focus {
    outline: none;
    border-color: #4a9eff;
    box-shadow: 0 0 0 3px rgba(74,158,255,0.15);
  }
  .form-group select option {
    background: #1a2a4a;
    color: #e0e8f0;
  }

  /* Radio group */
  .radio-group {
    display: flex;
    gap: 12px;
    margin-top: 4px;
  }
  .radio-card {
    flex: 1;
    position: relative;
  }
  .radio-card input[type="radio"] {
    position: absolute;
    opacity: 0;
    width: 0; height: 0;
  }
  .radio-card label {
    display: block;
    text-align: center;
    padding: 12px 8px;
    background: rgba(10,25,50,0.8);
    border: 1px solid rgba(100,180,255,0.2);
    border-radius: 8px;
    cursor: pointer;
    transition: all 0.3s;
    margin: 0;
    font-size: 13px;
    color: #8aa8c8;
  }
  .radio-card label .rc-title {
    display: block;
    font-size: 14px;
    font-weight: 600;
    color: #aed4ff;
    margin-bottom: 4px;
  }
  .radio-card label .rc-desc {
    display: block;
    font-size: 11px;
    color: #6a8aa8;
  }
  .radio-card input[type="radio"]:checked + label {
    background: rgba(74,158,255,0.15);
    border-color: #4a9eff;
    box-shadow: 0 0 12px rgba(74,158,255,0.2);
  }
  .radio-card input[type="radio"]:checked + label .rc-title {
    color: #4a9eff;
  }
  .radio-card input[type="radio"]:checked + label .rc-desc {
    color: #7ec8ff;
  }

  /* Buttons */
  .btn-calc {
    width: 100%;
    padding: 14px;
    background: linear-gradient(135deg, #2a6fd8, #4a9eff);
    border: none;
    border-radius: 10px;
    color: #fff;
    font-size: 16px;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.3s;
    letter-spacing: 1px;
    margin-top: 8px;
  }
  .btn-calc:hover {
    background: linear-gradient(135deg, #3580e8, #5aaeff);
    box-shadow: 0 4px 20px rgba(74,158,255,0.35);
    transform: translateY(-1px);
  }
  .btn-calc:active {
    transform: translateY(0);
  }

  .btn-secondary {
    padding: 8px 16px;
    background: rgba(74,158,255,0.1);
    border: 1px solid rgba(100,180,255,0.25);
    border-radius: 6px;
    color: #7ec8ff;
    font-size: 12px;
    cursor: pointer;
    transition: all 0.3s;
  }
  .btn-secondary:hover {
    background: rgba(74,158,255,0.2);
  }

  /* Results */
  .result-section {
    margin-top: 20px;
    padding-top: 20px;
    border-top: 1px solid rgba(100,180,255,0.1);
  }
  .result-section h3 {
    font-size: 15px;
    color: #7ec8ff;
    margin-bottom: 14px;
  }

  .u10-display {
    background: rgba(10,25,50,0.6);
    border: 1px solid rgba(100,180,255,0.15);
    border-radius: 10px;
    padding: 16px 20px;
    margin-bottom: 18px;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  .u10-display .u10-label {
    font-size: 13px;
    color: #8aa8c8;
  }
  .u10-display .u10-value {
    font-size: 28px;
    font-weight: 700;
    color: #4a9eff;
    font-family: 'Times New Roman', serif;
  }
  .u10-display .u10-unit {
    font-size: 14px;
    color: #6a8aa8;
    margin-left: 4px;
  }

  /* Result table */
  .result-table {
    width: 100%;
    border-collapse: collapse;
    font-size: 13px;
  }
  .result-table thead th {
    background: rgba(74,158,255,0.1);
    color: #7ec8ff;
    padding: 10px 12px;
    text-align: center;
    font-weight: 600;
    border-bottom: 2px solid rgba(74,158,255,0.2);
  }
  .result-table thead th:first-child {
    text-align: left;
    border-radius: 8px 0 0 0;
  }
  .result-table thead th:last-child {
    border-radius: 0 8px 0 0;
  }
  .result-table tbody td {
    padding: 10px 12px;
    text-align: center;
    border-bottom: 1px solid rgba(100,180,255,0.06);
    color: #c0d8f0;
  }
  .result-table tbody td:first-child {
    text-align: left;
    font-weight: 500;
    color: #aed4ff;
  }
  .result-table tbody tr:hover {
    background: rgba(74,158,255,0.05);
  }
  .result-table .factor-cell {
    color: #6a8aa8;
    font-size: 12px;
  }
  .result-table .wind-cell {
    font-weight: 600;
    color: #e0e8f0;
  }

  /* Beaufort scale colors */
  .bf-0 { color: #888; }
  .bf-1 { color: #8fbf8f; }
  .bf-2 { color: #7fb87f; }
  .bf-3 { color: #6fa86f; }
  .bf-4 { color: #dfd56a; }
  .bf-5 { color: #e8c84a; }
  .bf-6 { color: #f0a030; }
  .bf-7 { color: #f08030; }
  .bf-8 { color: #f06040; }
  .bf-9 { color: #e04050; }
  .bf-10 { color: #d02050; }
  .bf-11 { color: #c01060; }
  .bf-12 { color: #a01070; font-weight: 700; }

  /* Full width card */
  .full-width {
    grid-column: 1 / -1;
  }

  /* Coefficient table */
  .coeff-table-wrapper {
    overflow-x: auto;
    margin-top: 16px;
  }
  .coeff-table {
    width: 100%;
    border-collapse: collapse;
    font-size: 12px;
    min-width: 700px;
  }
  .coeff-table thead th {
    background: rgba(74,158,255,0.12);
    color: #7ec8ff;
    padding: 8px 10px;
    text-align: center;
    border: 1px solid rgba(100,180,255,0.1);
    font-weight: 600;
  }
  .coeff-table tbody td {
    padding: 7px 10px;
    text-align: center;
    border: 1px solid rgba(100,180,255,0.06);
    color: #b0c8e0;
  }
  .coeff-table tbody tr:hover {
    background: rgba(74,158,255,0.04);
  }
  .coeff-table .class-cell {
    text-align: left;
    font-weight: 600;
    color: #aed4ff;
    background: rgba(74,158,255,0.06);
  }
  .coeff-table .desc-cell {
    text-align: left;
    color: #8aa8c8;
    font-size: 11px;
    background: rgba(74,158,255,0.04);
  }

  /* Info box */
  .info-box {
    background: rgba(74,158,255,0.06);
    border: 1px solid rgba(100,180,255,0.12);
    border-radius: 10px;
    padding: 16px 20px;
    margin-top: 16px;
    font-size: 13px;
    color: #8aa8c8;
    line-height: 1.8;
  }
  .info-box strong {
    color: #7ec8ff;
  }

  /* Calculation detail */
  .calc-detail {
    background: rgba(10,25,50,0.6);
    border: 1px solid rgba(100,180,255,0.1);
    border-radius: 8px;
    padding: 14px 18px;
    margin-top: 14px;
    font-family: 'Times New Roman', serif;
    font-size: 13px;
    color: #aed4ff;
    line-height: 2;
  }
  .calc-detail .step {
    margin-bottom: 4px;
  }
  .calc-detail .highlight {
    color: #4a9eff;
    font-weight: 600;
  }

  .empty-state {
    text-align: center;
    padding: 40px 20px;
    color: #5a7a98;
    font-size: 14px;
  }
  .empty-state .es-icon {
    font-size: 36px;
    margin-bottom: 10px;
    opacity: 0.5;
  }

  /* Responsive */
  @media (max-width: 768px) {
    .main-grid {
      grid-template-columns: 1fr;
    }
    .header h1 { font-size: 22px; }
  }

  /* Toggle switch for direction */
  .direction-toggle {
    display: flex;
    align-items: center;
    gap: 10px;
    margin-bottom: 16px;
    padding: 12px 16px;
    background: rgba(10,25,50,0.5);
    border-radius: 10px;
    border: 1px solid rgba(100,180,255,0.1);
  }
  .direction-toggle .dt-label {
    font-size: 13px;
    color: #8aa8c8;
    white-space: nowrap;
  }
  .toggle-switch {
    position: relative;
    width: 200px;
    height: 36px;
    background: rgba(20,40,70,0.8);
    border-radius: 18px;
    border: 1px solid rgba(100,180,255,0.15);
    cursor: pointer;
    flex-shrink: 0;
  }
  .toggle-switch .ts-option {
    position: absolute;
    top: 0;
    width: 50%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 12px;
    font-weight: 600;
    z-index: 2;
    transition: color 0.3s;
    color: #6a8aa8;
  }
  .toggle-switch .ts-option.left { left: 0; }
  .toggle-switch .ts-option.right { right: 0; }
  .toggle-switch .ts-slider {
    position: absolute;
    top: 2px;
    left: 2px;
    width: calc(50% - 2px);
    height: calc(100% - 4px);
    background: linear-gradient(135deg, #2a6fd8, #4a9eff);
    border-radius: 16px;
    transition: transform 0.3s;
    z-index: 1;
  }
  .toggle-switch.forward .ts-slider { transform: translateX(0); }
  .toggle-switch.reverse .ts-slider { transform: translateX(100%); }
  .toggle-switch.forward .ts-option.left { color: #fff; }
  .toggle-switch.reverse .ts-option.right { color: #fff; }

  .input-hint {
    font-size: 11px;
    color: #5a7a98;
    margin-top: 4px;
  }
</style>
</head>
<body>

<div class="container">

  <!-- Header -->
  <div class="header">
    <h1>🌪️ 热带气旋10m风速换算工具</h1>
    <p>Tropical Cyclone 10m Wind Speed Conversion Tool</p>
    <p>© Ranarim 2026</p>
    <div class="formula-bar">
      U<sub>10</sub> = ln(10/Z₀) / ln(Z/Z₀) × U<sub>z</sub>(使用对数廓线进行计算)
    </div>
  </div>

  <div class="main-grid">

    <!-- Input Card -->
    <div class="card">
      <h2><span class="icon">⚙️</span> 部分参数设置(Settings)</h2>

      <!-- Direction Toggle -->
      <div class="direction-toggle">
        <span class="dt-label">换算方向：</span>
        <div class="toggle-switch forward" id="dirToggle" onclick="toggleDirection()">
          <div class="ts-slider"></div>
          <div class="ts-option left">➡️ 正向</div>
          <div class="ts-option right">⬅️ 反向</div>
        </div>
      </div>

      <div class="form-group">
        <label id="lblInputWind">测站风速 U<sub>z</sub> (m/s)</label>
        <input type="number" id="inputWind" step="0.1" min="0" max="100" value="20" placeholder="输入风速值">
        <div class="input-hint" id="hintInputWind">正向：输入平均风速 | 反向：输入阵风风速</div>
      </div>

      <div class="form-group">
        <label>测站高度 Z (m)</label>
        <input type="number" id="inputZ" step="0.1" min="0.1" max="500" value="10" placeholder="测站高度">
        <div class="input-hint">测风仪器安装高度（m）</div>
      </div>

      <div class="form-group">
        <label>地表粗糙度 Z₀ (m)</label>
        <input type="number" id="inputZ0" step="0.0001" min="0.0001" max="1" value="0.0015" placeholder="粗糙度长度">
        <div class="input-hint">默认 0.0015(海面/开阔水面) 0.003(开阔平坦地面)</div>
      </div>

      <div class="form-group">
        <label>测站位置及风速方向 (Station location and wind speed direction)</label>
        <select id="inputClass">
          <option value="inland">In-Land — Roughly open terrain（内陆开阔地形）</option>
          <option value="offland">Off-Land — Offshore winds at a coastline（海岸线离岸风）</option>
          <option value="offsea">Off-Sea — Onshore winds at a coastline（海岸线向岸风）</option>
          <option value="atsea">At-Sea — &gt; 20 km offshore（远海 &gt;20km）</option>
        </select>
      </div>

      <div class="form-group">
        <label>参考周期 T₀ (s)</label>
        <select id="inputT0">
          <option value="3600">3600s（1小时平均）</option>
          <option value="600">600s（10分钟平均）</option>
          <option value="180">180s（3分钟平均）</option>
          <option value="120">120s（2分钟平均）</option>
          <option value="60">60s（1分钟平均）</option>
          <option value="3">3s（3秒阵风）</option>
        </select>
      </div>

      <button class="btn-calc" onclick="calculate()">🔄 执行换算</button>

      <div class="info-box">
        <strong>换算逻辑说明：</strong><br>
        <span id="logicText">
        <strong>正向（平均风→阵风）</strong>：先通过风廓线公式将测站风速归算至10m高度，再<strong>乘以</strong>阵风系数G得到各时长阵风风速。<br>
        <strong>反向（阵风→平均风）</strong>：先通过风廓线公式将测站风速归算至10m高度，再<strong>除以</strong>阵风系数G还原为各时长平均风速。
        </span>
      </div>
    </div>

    <!-- Result Card -->
    <div class="card">
      <h2><span class="icon">📊</span> 换算结果</h2>

      <div id="resultArea">
        <div class="empty-state">
          <div class="es-icon">💨</div>
          请输入参数后点击「执行换算」<br>
          <span style="font-size:12px;">Calculation results will appear here</span>
        </div>
      </div>
    </div>

    <!-- Coefficient Table Card -->
    <div class="card full-width">
      <h2><span class="icon">📋</span> 阵风转换系数表 G<sub>r,T₀</sub></h2>
      <p style="font-size:12px;color:#6a8aa8;margin-bottom:10px;">
        数据来源：Table 1.1 Recommended wind speed conversion factors for tropical cyclone conditions
      </p>
      <div class="coeff-table-wrapper">
        <table class="coeff-table" id="coeffTable">
          <thead>
            <tr>
              <th rowspan="2" style="min-width:90px;">Class</th>
              <th rowspan="2" style="min-width:200px;">Description</th>
              <th rowspan="2" style="min-width:80px;">T₀ (s)</th>
              <th colspan="5" style="min-width:350px;">Gust Duration τ (s) → G<sub>r,T₀</sub></th>
            </tr>
            <tr>
              <th>3</th>
              <th>60</th>
              <th>120</th>
              <th>180</th>
              <th>600</th>
            </tr>
          </thead>
          <tbody id="coeffBody"></tbody>
        </table>
      </div>
    </div>

  </div>
</div>

<script>
// ============================================================
// 阵风转换系数表 (基于图片 Table 1.1)
// G[r][T0][tau] = value
// ============================================================
const G = {
  // In-Land: Roughly open terrain
  inland: {
    3600: { 3: 1.75, 60: 1.28, 120: 1.19, 180: 1.15, 600: 1.08 },
    600: { 3: 1.66, 60: 1.21, 120: 1.12, 180: 1.09, 600: 1.00 },
    180:  { 3: 1.58, 60: 1.15, 120: 1.07, 180: 1.00, 600: 1.09 },
    120:  { 3: 1.55, 60: 1.13, 120: 1.00, 180: 1.07 , 600: 1.12 },
    60:   { 3: 1.49, 60: 1.00, 120: 1.13, 180: 1.15, 600: 1.21 },
    3:    { 3: 1.00, 60: 1.49, 120: 1.55, 180: 1.58, 600: 1.66 }
  },
  // Off-Land: Offshore winds at a coastline
  offland: {
    3600: { 3: 1.60, 60: 1.22, 120: 1.15, 180: 1.12, 600: 1.06 },
    600: { 3: 1.52, 60: 1.16, 120: 1.09, 180: 1.06, 600: 1.00 },
    180:  { 3: 1.44, 60: 1.10, 120: 1.04, 180: 1.00, 600: 1.06 },
    120:  { 3: 1.42, 60: 1.08, 120: 1.00, 180: 1.04, 600: 1.09 },
    60:   { 3: 1.36, 60: 1.00, 120: 1.08, 180: 1.10, 600: 1.16 },
    3:    { 3: 1.00, 60: 1.36, 120: 1.42, 180: 1.44, 600: 1.52 }
  },
  // Off-Sea: Onshore winds at a coastline
  offsea: {
    3600: { 3: 1.45, 60: 1.17, 120: 1.11, 180: 1.09, 600: 1.05 },
    600: { 3: 1.38, 60: 1.11, 120: 1.05, 180: 1.03, 600: 1.00 },
    180:  { 3: 1.31, 60: 1.05, 120: 1.00, 180: 1.00, 600: 1.03 },
    120:  { 3: 1.28, 60: 1.03, 120: 1.00, 180: 1.00, 600: 1.05 },
    60:   { 3: 1.23, 60: 1.00, 120: 1.03, 180: 1.05, 600: 1.11 },
    3:    { 3: 1.00, 60: 1.23, 120: 1.28, 180: 1.31, 600: 1.38 }
  },
  // At-Sea: > 20 km offshore
  atsea: {
    3600: { 3: 1.30, 60: 1.11, 120: 1.07, 180: 1.06, 600: 1.03 },
    600: { 3: 1.23, 60: 1.05, 120: 1.02, 180: 1.00, 600: 1.00 },
    180:  { 3: 1.17, 60: 1.00, 120: 1.00, 180: 1.00, 600: 1.00 },
    120:  { 3: 1.15, 60: 1.00, 120: 1.00, 180: 1.00, 600: 1.02 },
    60:   { 3: 1.11, 60: 1.00, 120: 1.00, 180: 1.00, 600: 1.02 },
    3:    { 3: 1.00, 60: 1.11, 120: 1.15, 180: 1.17, 600: 1.23 }
  }
};

const CLASS_META = {
  inland:  { name: 'In-Land',  desc: 'Roughly open terrain' },
  offland: { name: 'Off-Land', desc: 'Offshore winds at a coastline' },
  offsea:  { name: 'Off-Sea',  desc: 'Onshore winds at a coastline' },
  atsea:   { name: 'At-Sea',   desc: '> 20 km offshore' }
};

const T0_LIST = [3600, 600, 180, 120, 60, 3];
const TAU_LIST = [3, 60, 120, 180, 600];

// Direction state
let direction = 'forward'; // 'forward' or 'reverse'

function toggleDirection() {
  direction = (direction === 'forward') ? 'reverse' : 'forward';
  const toggle = document.getElementById('dirToggle');
  toggle.className = 'toggle-switch ' + direction;

  const lbl = document.getElementById('lblInputWind');
  const hint = document.getElementById('hintInputWind');
  const logicText = document.getElementById('logicText');

  if (direction === 'forward') {
    lbl.innerHTML = '测站风速 U<sub>z</sub> (m/s)';
    hint.textContent = '正向：输入平均风速 | 将换算为各时长风速';
    logicText.innerHTML =
      '<strong>正向（平均风→阵风）</strong>：先通过对数风廓线公式将测站风速归算至10m高度，再<strong>乘以</strong>阵风系数G得到各时长阵风风速。';
  } else {
    lbl.innerHTML = '测站风速 U<sub>z</sub> (m/s)';
    hint.textContent = '反向：输入阵风风速 | 将换算为各时长平均风';
    logicText.innerHTML =
      '<strong>反向（阵风→平均风）</strong>：先通过风廓线公式将测站风速归算至10m高度，再<strong>除以</strong>阵风系数G还原为各时长平均风速。';
  }
}

// Beaufort scale
function beaufort(speed) {
  if (speed < 0.3) return { level: 0, name: 'Calm', cls: 'bf-0' };
  if (speed < 1.6) return { level: 1, name: 'Light air', cls: 'bf-1' };
  if (speed < 3.4) return { level: 2, name: 'Light breeze', cls: 'bf-2' };
  if (speed < 5.5) return { level: 3, name: 'Gentle breeze', cls: 'bf-3' };
  if (speed < 8.0) return { level: 4, name: 'Moderate breeze', cls: 'bf-4' };
  if (speed < 10.8) return { level: 5, name: 'Fresh breeze', cls: 'bf-5' };
  if (speed < 13.9) return { level: 6, name: 'Strong breeze', cls: 'bf-6' };
  if (speed < 17.2) return { level: 7, name: 'Near gale', cls: 'bf-7' };
  if (speed < 20.8) return { level: 8, name: 'Gale', cls: 'bf-8' };
  if (speed < 24.5) return { level: 9, name: 'Strong gale', cls: 'bf-9' };
  if (speed < 28.5) return { level: 10, name: 'Storm', cls: 'bf-10' };
  if (speed < 32.7) return { level: 11, name: 'Violent storm', cls: 'bf-11' };
  return { level: 12, name: 'Cyclone', cls: 'bf-12' };
}

function calculate() {
  const Uz = parseFloat(document.getElementById('inputWind').value);
  const Z = parseFloat(document.getElementById('inputZ').value);
  const Z0 = parseFloat(document.getElementById('inputZ0').value);
  const cls = document.getElementById('inputClass').value;
  const T0 = parseInt(document.getElementById('inputT0').value);

  if (isNaN(Uz) || isNaN(Z) || isNaN(Z0) || Z <= 0 || Z0 <= 0) {
    alert('请输入有效的数值参数！\nZ 和 Z₀ 必须大于 0。');
    return;
  }

  // Step 1: 风廓线换算到 10m
  const U10 = (Math.log(10 / Z0) / Math.log(Z / Z0)) * Uz;

  // Step 2: 获取系数
  const classData = G[cls];
  const t0Data = classData[T0];

  // Step 3: 计算各阵风时长
  const results = [];
  for (const tau of TAU_LIST) {
    const factor = t0Data[tau];
    let windVal;
    if (direction === 'forward') {
      // 正向：×系数（平均风→阵风）
      windVal = U10 * factor;
    } else {
      // 反向：÷系数（阵风→平均风）
      windVal = U10 / factor;
    }
    const bf = beaufort(windVal);
    results.push({ tau, factor, windVal, bf });
  }

  // Render results
  renderResults(Uz, Z, Z0, U10, cls, T0, results);
}

function renderResults(Uz, Z, Z0, U10, cls, T0, results) {
  const container = document.getElementById('resultArea');
  const meta = CLASS_META[cls];
  const dirText = direction === 'forward' ? '正向（×系数）' : '反向（÷系数）';
  const inputLabel = direction === 'forward' ? '输入平均风速' : '输入阵风风速';

  let html = '';

  // U10 display
  html += `
    <div class="u10-display">
      <div>
        <div class="u10-label">10m高度风速 U<sub>10</sub></div>
        <div style="font-size:11px;color:#5a7a98;margin-top:2px;">
          ln(10/${Z0}) / ln(${Z}/${Z0}) × ${Uz} = ${U10.toFixed(2)} m/s
        </div>
      </div>
      <div>
        <span class="u10-value">${U10.toFixed(2)}</span>
        <span class="u10-unit">m/s</span>
      </div>
    </div>
  `;

  // Direction & class info
  html += `
    <div style="display:flex;gap:10px;margin-bottom:14px;flex-wrap:wrap;">
      <span style="background:rgba(74,158,255,0.12);border:1px solid rgba(100,180,255,0.2);padding:4px 12px;border-radius:20px;font-size:12px;color:#7ec8ff;">${dirText}</span>
      <span style="background:rgba(74,158,255,0.08);border:1px solid rgba(100,180,255,0.15);padding:4px 12px;border-radius:20px;font-size:12px;color:#8aa8c8;">${meta.name}</span>
      <span style="background:rgba(74,158,255,0.08);border:1px solid rgba(100,180,255,0.15);padding:4px 12px;border-radius:20px;font-size:12px;color:#8aa8c8;">T₀=${T0}s</span>
    </div>
  `;

  // Results table
  html += `
    <table class="result-table">
      <thead>
        <tr>
          <th>阵风时长 τ</th>
          <th>系数 G</th>
          <th>换算风速 (m/s)</th>
          <th>蒲福等级</th>
        </tr>
      </thead>
      <tbody>
  `;

  for (const r of results) {
    const op = direction === 'forward' ? '×' : '÷';
    html += `
      <tr>
        <td>${r.tau} s</td>
        <td class="factor-cell">${r.factor.toFixed(2)}</td>
        <td class="wind-cell">${r.windVal.toFixed(2)} <span style="font-size:11px;color:#6a8aa8;">m/s</span></td>
        <td class="${r.bf.cls}">BF-${r.bf.level} ${r.bf.name}</td>
      </tr>
    `;
  }

  html += `
      </tbody>
    </table>
  `;

  // Calculation detail
  html += `
    <div class="calc-detail">
      <div class="step"><strong>① 高度换算：</strong></div>
      <div class="step">U<sub>10</sub> = ln(10/${Z0}) / ln(${Z}/${Z0}) × ${Uz} = <span class="highlight">${U10.toFixed(4)}</span> m/s</div>
      <div class="step" style="margin-top:8px;"><strong>② ${direction === 'forward' ? '正向换算（×系数）：' : '反向换算（÷系数）：'}</strong></div>
  `;
  for (const r of results) {
    const op = direction === 'forward' ? '×' : '÷';
    html += `<div class="step">τ=${r.tau}s: ${U10.toFixed(2)} ${op} ${r.factor.toFixed(2)} = <span class="highlight">${r.windVal.toFixed(2)}</span> m/s (BF-${r.bf.level})</div>`;
  }
  html += `</div>`;

  container.innerHTML = html;
}

// ============================================================
// Render coefficient table
// ============================================================
function renderCoeffTable() {
  const tbody = document.getElementById('coeffBody');
  const classes = ['inland', 'offland', 'offsea', 'atsea'];

  let html = '';
  for (const c of classes) {
    const meta = CLASS_META[c];
    const rowSpan = T0_LIST.length;

    T0_LIST.forEach((t0, idx) => {
      const data = G[c][t0];
      html += '<tr>';
      if (idx === 0) {
        html += `<td class="class-cell" rowspan="${rowSpan}"><strong>${meta.name}</strong></td>`;
        html += `<td class="desc-cell" rowspan="${rowSpan}">${meta.desc}</td>`;
      }
      html += `<td>${t0}</td>`;
      for (const tau of TAU_LIST) {
        const v = data[tau];
        html += `<td>${v.toFixed(2)}</td>`;
      }
      html += '</tr>';
    });
  }
  tbody.innerHTML = html;
}

// Init
renderCoeffTable();
</script>

<!-- 流星雨背景特效 (独立模块，不修改原有代码) -->
<script>
(function () {
  // 创建 canvas 并插入到 body 最底层
  const canvas = document.createElement('canvas');
  canvas.id = 'meteorShower';
  Object.assign(canvas.style, {
    position: 'fixed',
    top: '0',
    left: '0',
    width: '100vw',
    height: '100vh',
    zIndex: '-1',
    pointerEvents: 'none',
    display: 'block'
  });
  // 插入到 body 第一个节点之前，确保在最底层
  document.body.prepend(canvas);

  const ctx = canvas.getContext('2d');
  let W, H, meteors = [];

  function resize() {
    W = canvas.width = window.innerWidth;
    H = canvas.height = window.innerHeight;
  }
  resize();
  window.addEventListener('resize', resize);

  // 流星构造
  function createMeteor() {
    const x = Math.random() * W * 0.8;
    const y = -20 - Math.random() * 200;
    const len = 120 + Math.random() * 180;
    const speed = 6 + Math.random() * 8;
    const angle = (15 + Math.random() * 20) * Math.PI / 180;
    const opacity = 0.5 + Math.random() * 0.5;
    return { x, y, len, speed, angle, opacity, life: 1 };
  }

  function initMeteors(count) {
    meteors = [];
    for (let i = 0; i < count; i++) {
      const m = createMeteor();
      m.y = Math.random() * H * 0.6;
      m.x = Math.random() * W * 0.8;
      meteors.push(m);
    }
  }
  initMeteors(25);

  // 背景星星
  const stars = [];
  for (let i = 0; i < 120; i++) {
    stars.push({
      x: Math.random(),
      y: Math.random(),
      r: Math.random() * 1.2 + 0.3,
      twinkle: Math.random() * 0.02 + 0.005,
      phase: Math.random() * Math.PI * 2
    });
  }

  function drawStars(time) {
    for (const s of stars) {
      const alpha = 0.3 + 0.7 * Math.abs(Math.sin(s.phase + time * s.twinkle));
      ctx.beginPath();
      ctx.arc(s.x * W, s.y * H, s.r, 0, Math.PI * 2);
      ctx.fillStyle = 'rgba(180, 210, 255,' + alpha.toFixed(3) + ')';
      ctx.fill();
    }
  }

  function drawMeteor(m) {
    const dx = Math.cos(m.angle) * m.len;
    const dy = Math.sin(m.angle) * m.len;
    const tailX = m.x - dx;
    const tailY = m.y - dy;

    const grad = ctx.createLinearGradient(m.x, m.y, tailX, tailY);
    grad.addColorStop(0, 'rgba(220, 235, 255,' + (m.opacity * m.life).toFixed(3) + ')');
    grad.addColorStop(0.4, 'rgba(160, 200, 255,' + (m.opacity * m.life * 0.4).toFixed(3) + ')');
    grad.addColorStop(1, 'rgba(100, 140, 220, 0)');

    ctx.beginPath();
    ctx.moveTo(m.x, m.y);
    ctx.lineTo(tailX, tailY);
    ctx.lineWidth = 1.5;
    ctx.strokeStyle = grad;
    ctx.lineCap = 'round';
    ctx.stroke();

    ctx.beginPath();
    ctx.arc(m.x, m.y, 1.8, 0, Math.PI * 2);
    ctx.fillStyle = 'rgba(255, 255, 255,' + (m.opacity * m.life).toFixed(3) + ')';
    ctx.fill();
  }

  function frame(ts) {
    const t = ts / 1000;
    ctx.fillStyle = 'rgba(10, 22, 40, 0.25)';
    ctx.fillRect(0, 0, W, H);

    drawStars(t);

    if (Math.random() < 0.03 && meteors.length < 40) {
      meteors.push(createMeteor());
    }

    for (let i = meteors.length - 1; i >= 0; i--) {
      const m = meteors[i];
      m.x += Math.cos(m.angle) * m.speed;
      m.y += Math.sin(m.angle) * m.speed;
      m.life -= 0.006;

      drawMeteor(m);

      if (m.y > H + 50 || m.x > W + 50 || m.life <= 0) {
        meteors.splice(i, 1);
      }
    }

    while (meteors.length < 20) {
      meteors.push(createMeteor());
    }

    requestAnimationFrame(frame);
  }
  requestAnimationFrame(frame);
})();
</script>

</body>
</html>
