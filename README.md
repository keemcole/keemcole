<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>音频视频计算器</title>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"></script>
  <!-- Materialize CSS & Material Icons -->
  <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
  <link href="https://cdn.jsdelivr.net/npm/materialize-css@1.0.0/dist/css/materialize.min.css" rel="stylesheet">
  <script src="https://cdn.jsdelivr.net/npm/materialize-css@1.0.0/dist/js/materialize.min.js"></script>
  <style>
    :root {
      --primary-color: #111;
      --secondary-color: #444;
      --border-color: #e0e0e0;
      --bg-main: #f7f7f7;
      --bg-card: #fff;
      --text-main: #111;
      --text-secondary: #666;
      --btn-bg: #111;
      --btn-bg-hover: #333;
      --btn-text: #fff;
      --footer-bg: #111;
      --footer-text: #fff;
    }
    
    body {
      background: var(--bg-main);
      min-height: 100vh;
      font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
      color: var(--text-main);
    }
    
    .container {
      max-width: 900px;
      padding: 2rem 1rem;
    }
    
    .header {
      text-align: center;
      margin-bottom: 2rem;
    }
    
    .header h1 {
      font-size: 2.2rem;
      font-weight: bold;
      color: var(--text-main);
      margin-bottom: 0.5rem;
    }
    
    .header p {
      font-size: 1.1rem;
      color: var(--text-secondary);
      margin-bottom: 0;
    }
    
    .calculator-card {
      background: var(--bg-card);
      border-radius: 0.7rem;
      box-shadow: 0 2px 12px #0001;
      padding: 1.5rem 1.2rem 1.2rem 1.2rem;
      margin-bottom: 2rem;
      border: 1px solid var(--border-color);
    }
    
    .calculator-card h2 {
      color: var(--text-main);
      font-size: 1.18rem;
      margin-bottom: 1.2rem;
      font-weight: 600;
      border-bottom: 1px solid var(--border-color);
      padding-bottom: 0.5rem;
    }
    
    .form-label {
      font-weight: 500;
      color: var(--text-secondary);
      font-size: 1rem;
    }
    
    .form-control {
      border-radius: 0.4rem;
      border: 1px solid var(--border-color);
      padding: 0.7rem;
      color: var(--text-main);
      background: #fff;
      font-size: 1rem;
      box-shadow: none;
      transition: border 0.2s;
    }
    
    .form-control:focus {
      border-color: var(--secondary-color);
      outline: none;
      box-shadow: none;
    }
    
    .btn {
      border-radius: 0.4rem;
      padding: 0.7rem 1.5rem;
      font-weight: 500;
      background: var(--btn-bg);
      color: var(--btn-text);
      border: none;
      transition: background 0.18s, color 0.18s;
      font-size: 1.05rem;
    }
    
    .btn:hover, .btn:focus {
      background: var(--btn-bg-hover);
      color: var(--btn-text);
    }
    
    .result-box {
      background: #fafafa;
      border-radius: 0.4rem;
      padding: 1rem;
      margin-top: 1rem;
      border-left: 3px solid var(--secondary-color);
      color: var(--text-main);
      font-size: 1.05rem;
    }
    
    .history-table {
      width: 100%;
      margin-top: 1rem;
      border-collapse: collapse;
    }
    
    .history-table th, .history-table td {
      padding: 0.7rem 0.5rem;
      border-bottom: 1px solid var(--border-color);
      text-align: left;
      font-size: 0.98rem;
    }
    
    .history-table th {
      background: #f3f3f3;
      color: var(--text-secondary);
      font-weight: 600;
    }
    
    .footer {
      background: var(--footer-bg);
      color: var(--footer-text);
      text-align: center;
      padding: 2rem 0 1rem 0;
      margin-top: 2rem;
      border-top: 1px solid #222;
    }
    
    .footer-brand {
      font-family: 'Orbitron', sans-serif;
      font-size: 1.1rem;
      font-weight: bold;
      color: var(--footer-text);
      margin-bottom: 0.3rem;
      letter-spacing: 0.08em;
    }
    
    .footer-copyright {
      font-size: 0.95rem;
      color: #bbb;
    }
    
    @media (max-width: 600px) {
      .container { padding: 0.5rem; }
      .calculator-card { padding: 1rem 0.5rem; }
    }
  </style>
  <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@600;700&family=Orbitron:wght@600&family=Audiowide&display=swap" rel="stylesheet">
</head>
<body>
  <div class="container">
    <div class="header">
      <h1>音频视频计算器</h1>
      <p>专业的音视频参数计算工具</p>
    </div>

    <!-- 音频计算器 -->
    <div class="calculator-card">
      <h2>音频参数计算</h2>
      <div class="row">
        <div class="col-md-4 mb-3">
          <label class="form-label">文件大小 (MB)</label>
          <input type="number" class="form-control" id="audioSize" placeholder="输入文件大小">
        </div>
        <div class="col-md-4 mb-3">
          <label class="form-label">码率 (kbps)</label>
          <input type="number" class="form-control" id="audioBitrate" placeholder="输入码率">
        </div>
        <div class="col-md-4 mb-3">
          <label class="form-label">时长 (秒)</label>
          <input type="number" class="form-control" id="audioDuration" placeholder="输入时长">
        </div>
      </div>
      <div class="row">
        <div class="col-12">
          <button class="btn btn-primary w-100" onclick="calculateAudio()">计算</button>
        </div>
      </div>
      <div id="audioResult" class="result-box" style="display: none;"></div>
    </div>

    <!-- 视频计算器 -->
    <div class="calculator-card">
      <h2>视频参数计算</h2>
      <div class="row">
        <div class="col-md-4 mb-3">
          <label class="form-label">文件大小 (MB)</label>
          <input type="number" class="form-control" id="videoSize" placeholder="输入文件大小">
        </div>
        <div class="col-md-4 mb-3">
          <label class="form-label">码率 (kbps)</label>
          <input type="number" class="form-control" id="videoBitrate" placeholder="输入码率">
        </div>
        <div class="col-md-4 mb-3">
          <label class="form-label">时长 (秒)</label>
          <input type="number" class="form-control" id="videoDuration" placeholder="输入时长">
        </div>
      </div>
      <div class="row">
        <div class="col-md-6 mb-3">
          <label class="form-label">分辨率</label>
          <select class="form-control" id="videoResolution">
            <option value="1920x1080">1080p (1920x1080)</option>
            <option value="1280x720">720p (1280x720)</option>
            <option value="3840x2160">4K (3840x2160)</option>
          </select>
        </div>
        <div class="col-md-6 mb-3">
          <label class="form-label">帧率 (fps)</label>
          <input type="number" class="form-control" id="videoFps" placeholder="输入帧率" value="30">
        </div>
      </div>
      <div class="row">
        <div class="col-12">
          <button class="btn btn-primary w-100" onclick="calculateVideo()">计算</button>
        </div>
      </div>
      <div id="videoResult" class="result-box" style="display: none;"></div>
    </div>

    <!-- 帧率转换器 -->
    <div class="calculator-card">
      <h2>帧率转换</h2>
      <div class="row">
        <div class="col-md-4 mb-3">
          <label class="form-label">原始帧率 (fps)</label>
          <input type="number" class="form-control" id="sourceFps" value="24">
        </div>
        <div class="col-md-4 mb-3">
          <label class="form-label">目标帧率 (fps)</label>
          <input type="number" class="form-control" id="targetFps" value="30">
        </div>
        <div class="col-md-4 mb-3">
          <label class="form-label">总帧数</label>
          <input type="number" class="form-control" id="totalFrames" placeholder="输入总帧数">
        </div>
      </div>
      <div class="row">
        <div class="col-12">
          <button class="btn btn-primary w-100" onclick="convertFps()">转换</button>
        </div>
      </div>
      <div id="fpsResult" class="result-box" style="display: none;"></div>
    </div>

    <!-- 计算历史 -->
    <div class="calculator-card">
      <h2>计算历史</h2>
      <table class="history-table">
        <thead>
          <tr>
            <th>类型</th>
            <th>输入参数</th>
            <th>计算结果</th>
          </tr>
        </thead>
        <tbody id="historyTable"></tbody>
      </table>
      <button class="btn btn-primary mt-3" onclick="exportHistory()">导出历史记录</button>
    </div>

    <div class="footer">
      <div class="footer-brand">
        <span style="margin-right: 0.5rem;">⚡️</span>
        KeemCole
        <span style="margin-left: 0.5rem;">🟣</span>
      </div>
      <div class="footer-copyright">
        © 2025 KeemCole. All rights reserved.
        <span style="margin-left: 0.5rem; color: var(--primary-color);">Inspired by KeemCole | Since 2024</span>
      </div>
    </div>
  </div>

  <script>
    // 全局变量
    let calculationHistory = [];

    // 添加历史记录
    function addToHistory(type, input, result) {
      calculationHistory.push({ type, input, result });
      updateHistoryTable();
    }

    // 更新历史记录表格
    function updateHistoryTable() {
      const tbody = document.getElementById('historyTable');
      tbody.innerHTML = '';
      calculationHistory.forEach(item => {
        const tr = document.createElement('tr');
        tr.innerHTML = `
          <td>${item.type}</td>
          <td>${item.input}</td>
          <td>${item.result}</td>
        `;
        tbody.appendChild(tr);
      });
    }

    // 音频计算
    function calculateAudio() {
      const size = parseFloat(document.getElementById('audioSize').value);
      const bitrate = parseFloat(document.getElementById('audioBitrate').value);
      const duration = parseFloat(document.getElementById('audioDuration').value);
      
      let result = '';
      let input = '';
      
      if (size && bitrate && !duration) {
        const calculatedDuration = (size * 8 * 1024) / bitrate;
        result = `时长：${formatDuration(calculatedDuration)}`;
        input = `大小=${size}MB, 码率=${bitrate}kbps`;
      } else if (size && duration && !bitrate) {
        const calculatedBitrate = (size * 8 * 1024) / duration;
        result = `码率：${calculatedBitrate.toFixed(2)} kbps`;
        input = `大小=${size}MB, 时长=${duration}秒`;
      } else if (bitrate && duration && !size) {
        const calculatedSize = (bitrate * duration) / (8 * 1024);
        result = `文件大小：${calculatedSize.toFixed(2)} MB`;
        input = `码率=${bitrate}kbps, 时长=${duration}秒`;
      } else {
        result = '请填写任意两项进行计算';
      }
      
      document.getElementById('audioResult').textContent = result;
      document.getElementById('audioResult').style.display = 'block';
      
      if (result !== '请填写任意两项进行计算') {
        addToHistory('音频计算', input, result);
      }
    }

    // 视频计算
    function calculateVideo() {
      const size = parseFloat(document.getElementById('videoSize').value);
      const bitrate = parseFloat(document.getElementById('videoBitrate').value);
      const duration = parseFloat(document.getElementById('videoDuration').value);
      const resolution = document.getElementById('videoResolution').value;
      const fps = parseFloat(document.getElementById('videoFps').value);
      
      let result = '';
      let input = '';
      
      if (size && bitrate && !duration) {
        const calculatedDuration = (size * 8 * 1024) / bitrate;
        result = `时长：${formatDuration(calculatedDuration)}`;
        input = `大小=${size}MB, 码率=${bitrate}kbps, 分辨率=${resolution}, ${fps}fps`;
      } else if (size && duration && !bitrate) {
        const calculatedBitrate = (size * 8 * 1024) / duration;
        result = `码率：${calculatedBitrate.toFixed(2)} kbps`;
        input = `大小=${size}MB, 时长=${duration}秒, 分辨率=${resolution}, ${fps}fps`;
      } else if (bitrate && duration && !size) {
        const calculatedSize = (bitrate * duration) / (8 * 1024);
        result = `文件大小：${calculatedSize.toFixed(2)} MB`;
        input = `码率=${bitrate}kbps, 时长=${duration}秒, 分辨率=${resolution}, ${fps}fps`;
      } else {
        result = '请填写任意两项进行计算';
      }
      
      document.getElementById('videoResult').textContent = result;
      document.getElementById('videoResult').style.display = 'block';
      
      if (result !== '请填写任意两项进行计算') {
        addToHistory('视频计算', input, result);
      }
    }

    // 帧率转换
    function convertFps() {
      const sourceFps = parseFloat(document.getElementById('sourceFps').value);
      const targetFps = parseFloat(document.getElementById('targetFps').value);
      const totalFrames = parseFloat(document.getElementById('totalFrames').value);
      
      if (!sourceFps || !targetFps || !totalFrames) {
        document.getElementById('fpsResult').textContent = '请填写所有参数';
        document.getElementById('fpsResult').style.display = 'block';
        return;
      }
      
      const duration = totalFrames / sourceFps;
      const newFrames = Math.round(duration * targetFps);
      
      const result = `原时长：${formatDuration(duration)}\n目标帧数：${newFrames}`;
      const input = `源帧率=${sourceFps}fps, 目标帧率=${targetFps}fps, 总帧数=${totalFrames}`;
      
      document.getElementById('fpsResult').textContent = result;
      document.getElementById('fpsResult').style.display = 'block';
      
      addToHistory('帧率转换', input, result);
    }

    // 格式化时长
    function formatDuration(seconds) {
      const minutes = Math.floor(seconds / 60);
      const remainingSeconds = Math.round(seconds % 60);
      return `${minutes}分${remainingSeconds}秒 (${seconds.toFixed(1)}秒)`;
    }

    // 导出历史记录
    function exportHistory() {
      if (calculationHistory.length === 0) {
        alert('暂无历史记录可导出');
        return;
      }
      
      let csv = '类型,输入参数,计算结果\n';
      calculationHistory.forEach(item => {
        csv += `${item.type},"${item.input}","${item.result}"\n`;
      });
      
      const blob = new Blob([csv], { type: 'text/csv;charset=utf-8;' });
      const url = URL.createObjectURL(blob);
      const a = document.createElement('a');
      a.href = url;
      a.download = '计算历史.csv';
      a.click();
      URL.revokeObjectURL(url);
    }
  </script>
</body>
</html>
