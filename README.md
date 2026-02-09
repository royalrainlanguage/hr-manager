# hr-manager[index.html.html](https://github.com/user-attachments/files/25176402/index.html.html)
<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>人資加班與休假管理系統</title>
    <link href="https://fonts.googleapis.com/css2?family=Outfit:wght@400;500;600;700;800;900&family=Noto+Sans+TC:wght@400;500;700;900&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #6366f1;
            --primary-dark: #4f46e5;
            --secondary: #ec4899;
            --accent: #f59e0b;
            --success: #10b981;
            --danger: #ef4444;
            --warning: #f59e0b;
            --info: #06b6d4;
            
            --bg-main: #0f172a;
            --bg-card: #1e293b;
            --bg-elevated: #334155;
            
            --text-primary: #f1f5f9;
            --text-secondary: #cbd5e1;
            --text-muted: #64748b;
            
            --gradient-primary: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            --gradient-card: linear-gradient(135deg, #1e293b 0%, #334155 100%);
        }

        * { margin: 0; padding: 0; box-sizing: border-box; }

        body {
            font-family: 'Outfit', 'Noto Sans TC', sans-serif;
            background: var(--bg-main);
            color: var(--text-primary);
            min-height: 100vh;
            padding: 0;
            overflow-x: hidden;
        }

        body::before {
            content: '';
            position: fixed;
            top: 0; left: 0; right: 0; bottom: 0;
            background: 
                radial-gradient(circle at 20% 20%, rgba(99, 102, 241, 0.15) 0%, transparent 50%),
                radial-gradient(circle at 80% 80%, rgba(236, 72, 153, 0.15) 0%, transparent 50%),
                radial-gradient(circle at 50% 50%, rgba(245, 158, 11, 0.1) 0%, transparent 50%);
            pointer-events: none;
            z-index: 0;
        }

        .container { max-width: 1600px; margin: 0 auto; padding: 24px; position: relative; z-index: 1; }

        /* 頂部導航 */
        .top-nav {
            display: flex; justify-content: space-between; align-items: center;
            padding: 20px 32px; background: rgba(30, 41, 59, 0.8);
            backdrop-filter: blur(20px); border-radius: 20px; margin-bottom: 24px;
            border: 1px solid rgba(255, 255, 255, 0.05);
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
        }

        .logo { display: flex; align-items: center; gap: 12px; font-size: 24px; font-weight: 900; letter-spacing: -0.5px; }
        .logo-icon { width: 40px; height: 40px; background: var(--gradient-primary); border-radius: 10px; display: flex; align-items: center; justify-content: center; font-size: 20px; }
        .nav-controls { display: flex; gap: 12px; align-items: center; flex-wrap: wrap; }

        .btn {
            padding: 10px 20px; border: none; border-radius: 12px;
            font-size: 14px; font-weight: 600; cursor: pointer;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            display: inline-flex; align-items: center; gap: 6px;
            font-family: inherit; position: relative; overflow: hidden;
        }

        .btn::before {
            content: ''; position: absolute; top: 0; left: -100%;
            width: 100%; height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.2), transparent);
            transition: left 0.5s;
        }

        .btn:hover::before { left: 100%; }

        .btn-primary { background: var(--gradient-primary); color: white; box-shadow: 0 4px 12px rgba(99, 102, 241, 0.4); }
        .btn-primary:hover { transform: translateY(-2px); box-shadow: 0 8px 20px rgba(99, 102, 241, 0.5); }
        .btn-ghost { background: rgba(255, 255, 255, 0.05); color: var(--text-primary); border: 1px solid rgba(255, 255, 255, 0.1); }
        .btn-ghost:hover { background: rgba(255, 255, 255, 0.1); border-color: rgba(255, 255, 255, 0.2); }
        .btn-success { background: linear-gradient(135deg, #10b981 0%, #059669 100%); color: white; box-shadow: 0 4px 12px rgba(16, 185, 129, 0.4); }
        .btn-success:hover { transform: translateY(-2px); box-shadow: 0 8px 20px rgba(16, 185, 129, 0.5); }
        .btn-danger { background: linear-gradient(135deg, #ef4444 0%, #dc2626 100%); color: white; }
        .btn-danger:hover { transform: translateY(-2px); box-shadow: 0 8px 20px rgba(239, 68, 68, 0.5); }
        .btn-full { flex: 1; }

        /* 年度特休卡片 */
        .annual-leave-card {
            background: linear-gradient(135deg, rgba(16, 185, 129, 0.15) 0%, rgba(16, 185, 129, 0.05) 100%);
            border: 2px solid rgba(16, 185, 129, 0.3);
            padding: 28px; border-radius: 20px;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
            margin-bottom: 24px;
        }

        .annual-leave-header {
            display: flex; justify-content: space-between; align-items: center;
            margin-bottom: 24px;
        }

        .annual-leave-title { font-size: 24px; font-weight: 900; display: flex; align-items: center; gap: 12px; }

        .leave-stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 16px;
        }

        .leave-stat-item {
            background: rgba(255, 255, 255, 0.05);
            padding: 20px; border-radius: 16px;
            border: 1px solid rgba(255, 255, 255, 0.1);
            text-align: center; transition: all 0.3s ease;
        }

        .leave-stat-item:hover { background: rgba(255, 255, 255, 0.08); transform: translateY(-4px); }
        .leave-stat-label { font-size: 12px; color: var(--text-muted); margin-bottom: 10px; font-weight: 600; text-transform: uppercase; }
        .leave-stat-value { font-size: 32px; font-weight: 900; color: var(--success); line-height: 1; }

        /* 主要內容區 */
        .main-content { display: grid; grid-template-columns: 1fr; gap: 24px; }

        /* 月份標題 */
        .month-header {
            background: var(--gradient-card); padding: 32px; border-radius: 24px;
            border: 1px solid rgba(255, 255, 255, 0.05);
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
            position: relative; overflow: hidden;
        }

        .month-header::before {
            content: ''; position: absolute; top: -50%; right: -10%;
            width: 300px; height: 300px;
            background: radial-gradient(circle, rgba(99, 102, 241, 0.2) 0%, transparent 70%);
            border-radius: 50%;
        }

        .month-title-row { display: flex; justify-content: space-between; align-items: center; margin-bottom: 20px; position: relative; }
        .month-title { font-size: 42px; font-weight: 900; background: linear-gradient(135deg, #f1f5f9 0%, #cbd5e1 100%); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text; letter-spacing: -1px; }
        .month-nav { display: flex; gap: 12px; }

        /* 統計切換標籤 */
        .stats-tabs { display: flex; gap: 12px; margin-bottom: 20px; position: relative; flex-wrap: wrap; }
        .stats-tab {
            padding: 12px 24px; background: rgba(255, 255, 255, 0.05);
            border: 1px solid rgba(255, 255, 255, 0.1); border-radius: 12px;
            cursor: pointer; transition: all 0.3s ease;
            font-weight: 600; font-size: 14px;
        }
        .stats-tab:hover { background: rgba(255, 255, 255, 0.1); }
        .stats-tab.active { background: var(--gradient-primary); border-color: var(--primary); box-shadow: 0 4px 12px rgba(99, 102, 241, 0.4); }

        .quick-stats {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
            gap: 16px; position: relative;
        }

        .quick-stat {
            background: rgba(255, 255, 255, 0.03); padding: 16px 20px;
            border-radius: 16px; border: 1px solid rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(10px); transition: all 0.3s ease;
        }
        .quick-stat:hover { background: rgba(255, 255, 255, 0.06); border-color: rgba(255, 255, 255, 0.1); transform: translateY(-2px); }
        .quick-stat-label { font-size: 12px; color: var(--text-muted); margin-bottom: 8px; font-weight: 500; text-transform: uppercase; letter-spacing: 0.5px; }
        .quick-stat-value { font-size: 28px; font-weight: 900; background: var(--gradient-primary); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text; }

        /* 日曆 */
        .calendar-container { background: var(--gradient-card); padding: 32px; border-radius: 24px; border: 1px solid rgba(255, 255, 255, 0.05); box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3); }
        .calendar-grid { display: grid; grid-template-columns: repeat(7, 1fr); gap: 16px; }
        .weekday { text-align: center; font-weight: 700; padding: 16px; color: var(--text-muted); font-size: 13px; text-transform: uppercase; letter-spacing: 1px; }

        .day-cell {
            aspect-ratio: 1; background: rgba(255, 255, 255, 0.03);
            border: 2px solid rgba(255, 255, 255, 0.05); border-radius: 20px;
            padding: 16px; cursor: pointer; position: relative;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            display: flex; flex-direction: column; overflow: hidden;
        }

        .day-cell::before {
            content: ''; position: absolute; top: 0; left: 0; right: 0; bottom: 0;
            background: radial-gradient(circle at center, rgba(99, 102, 241, 0.1) 0%, transparent 70%);
            opacity: 0; transition: opacity 0.3s ease;
        }

        .day-cell:hover::before { opacity: 1; }
        .day-cell:hover { transform: translateY(-4px) scale(1.02); border-color: rgba(99, 102, 241, 0.5); box-shadow: 0 12px 24px rgba(99, 102, 241, 0.2); }
        .day-number { font-size: 20px; font-weight: 700; color: var(--text-primary); margin-bottom: auto; position: relative; z-index: 1; }

        /* 週末 */
        .day-rest { background: linear-gradient(135deg, rgba(236, 72, 153, 0.15) 0%, rgba(236, 72, 153, 0.05) 100%); border-color: rgba(236, 72, 153, 0.2); }
        .rest-badge { position: absolute; top: 12px; right: 12px; background: rgba(236, 72, 153, 0.9); color: white; font-size: 10px; font-weight: 700; padding: 4px 8px; border-radius: 6px; z-index: 2; }

        /* 國定假日 */
        .day-national-holiday { background: linear-gradient(135deg, rgba(245, 158, 11, 0.25) 0%, rgba(245, 158, 11, 0.1) 100%); border-color: rgba(245, 158, 11, 0.4); }
        .holiday-badge { position: absolute; top: 40px; right: 12px; background: rgba(245, 158, 11, 0.95); color: white; font-size: 9px; font-weight: 700; padding: 4px 8px; border-radius: 6px; max-width: 70%; text-align: center; line-height: 1.3; z-index: 2; }

        /* 補班日 */
        .day-makeup { background: linear-gradient(135deg, rgba(99, 102, 241, 0.2) 0%, rgba(99, 102, 241, 0.08) 100%); border: 2px dashed rgba(99, 102, 241, 0.5); }
        .makeup-badge { background: rgba(99, 102, 241, 0.95); }

        /* 臨時假日 */
        .day-custom-holiday { background: linear-gradient(135deg, rgba(16, 185, 129, 0.2) 0%, rgba(16, 185, 129, 0.08) 100%); border-color: rgba(16, 185, 129, 0.4); }
        .custom-badge { background: rgba(16, 185, 129, 0.95); }

        /* 有加班 */
        .has-overtime {
            background: linear-gradient(135deg, rgba(245, 158, 11, 0.3) 0%, rgba(245, 158, 11, 0.15) 100%) !important;
            border: 2px solid rgba(245, 158, 11, 0.6) !important;
            box-shadow: 0 0 24px rgba(245, 158, 11, 0.3) !important;
        }
        .has-overtime::before { background: radial-gradient(circle at center, rgba(245, 158, 11, 0.2) 0%, transparent 70%); opacity: 1; }

        /* 有請假 */
        .has-leave { background: linear-gradient(135deg, rgba(6, 182, 212, 0.25) 0%, rgba(6, 182, 212, 0.1) 100%) !important; border: 2px solid rgba(6, 182, 212, 0.5) !important; }

        /* 已報備 */
        .day-is-reported { border-left: 6px solid var(--primary) !important; box-shadow: 0 0 32px rgba(99, 102, 241, 0.4) !important; }
        .day-is-reported.has-overtime { background: linear-gradient(135deg, rgba(99, 102, 241, 0.25) 0%, rgba(245, 158, 11, 0.25) 100%) !important; }

        .reported-indicator { position: absolute; top: 12px; left: 12px; background: var(--primary); color: white; font-size: 10px; font-weight: 700; padding: 4px 8px; border-radius: 6px; z-index: 2; box-shadow: 0 2px 8px rgba(99, 102, 241, 0.4); }
        .deferred-indicator { position: absolute; top: 38px; left: 12px; background: rgba(245, 158, 11, 0.95); color: white; font-size: 9px; font-weight: 700; padding: 3px 6px; border-radius: 5px; z-index: 2; }
        .leave-indicator { position: absolute; bottom: 42px; left: 12px; background: rgba(6, 182, 212, 0.95); color: white; font-size: 10px; font-weight: 700; padding: 4px 8px; border-radius: 6px; z-index: 2; }
        .day-ot-hours { color: #fb923c; font-weight: 900; text-align: right; margin-top: auto; font-size: 24px; text-shadow: 0 2px 8px rgba(251, 146, 60, 0.4); position: relative; z-index: 1; letter-spacing: -0.5px; }

        /* 側邊欄 */
        .sidebar { display: grid; gap: 24px; }
        .info-card { background: var(--gradient-card); padding: 28px; border-radius: 20px; border: 1px solid rgba(255, 255, 255, 0.05); box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3); transition: all 0.3s ease; }
        .info-card:hover { transform: translateY(-4px); box-shadow: 0 12px 40px rgba(0, 0, 0, 0.4); }
        .card-title { font-size: 18px; font-weight: 700; margin-bottom: 20px; display: flex; align-items: center; gap: 10px; color: var(--text-primary); }
        .card-icon { font-size: 24px; }

        .stats-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 16px; }
        .stat-item { background: rgba(255, 255, 255, 0.03); padding: 20px; border-radius: 16px; border: 1px solid rgba(255, 255, 255, 0.05); text-align: center; transition: all 0.3s ease; }
        .stat-item:hover { background: rgba(255, 255, 255, 0.06); transform: scale(1.05); }
        .stat-label { font-size: 11px; color: var(--text-muted); margin-bottom: 10px; font-weight: 600; text-transform: uppercase; letter-spacing: 0.5px; }
        .stat-value { font-size: 32px; font-weight: 900; background: var(--gradient-primary); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text; line-height: 1; }
        .stat-unit { font-size: 14px; margin-left: 4px; }

        /* 圖例 */
        .legend-grid { display: grid; gap: 12px; }
        .legend-item { display: flex; align-items: center; gap: 12px; padding: 12px; background: rgba(255, 255, 255, 0.03); border-radius: 12px; border: 1px solid rgba(255, 255, 255, 0.05); }
        .legend-color { width: 32px; height: 32px; border-radius: 8px; border: 2px solid; flex-shrink: 0; }
        .legend-text { font-size: 13px; font-weight: 500; color: var(--text-secondary); }

        /* 彈窗 */
        .modal {
            display: none; position: fixed; top: 0; left: 0; right: 0; bottom: 0;
            background: rgba(0, 0, 0, 0.8); backdrop-filter: blur(8px);
            z-index: 1000; align-items: center; justify-content: center;
            padding: 24px; animation: fadeIn 0.3s ease;
        }
        .modal.active { display: flex; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        .modal-content {
            background: var(--bg-card); border-radius: 24px; padding: 40px;
            max-width: 600px; width: 100%; max-height: 90vh; overflow-y: auto;
            border: 1px solid rgba(255, 255, 255, 0.1);
            box-shadow: 0 24px 64px rgba(0, 0, 0, 0.5);
            animation: slideUp 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        }
        @keyframes slideUp { from { opacity: 0; transform: translateY(40px); } to { opacity: 1; transform: translateY(0); } }

        .modal-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 32px; padding-bottom: 20px; border-bottom: 2px solid rgba(255, 255, 255, 0.1); }
        .modal-title { font-size: 28px; font-weight: 900; color: var(--text-primary); }
        .modal-close {
            background: rgba(255, 255, 255, 0.05); border: 1px solid rgba(255, 255, 255, 0.1);
            width: 40px; height: 40px; border-radius: 12px;
            display: flex; align-items: center; justify-content: center;
            cursor: pointer; font-size: 24px; color: var(--text-secondary);
            transition: all 0.3s ease;
        }
        .modal-close:hover { background: rgba(255, 255, 255, 0.1); color: var(--text-primary); transform: rotate(90deg); }

        /* 表單 */
        .form-group { margin-bottom: 24px; }
        .form-label { display: block; font-size: 14px; font-weight: 600; color: var(--text-secondary); margin-bottom: 10px; }
        .form-input, .form-select {
            width: 100%; padding: 14px 18px;
            background: #ffffff;
            border: 2px solid rgba(255, 255, 255, 0.1);
            border-radius: 12px; color: #1f2937;
            font-size: 15px; font-family: inherit;
            transition: all 0.3s ease;
        }
        .form-select option {
            background: #ffffff;
            color: #1f2937;
        }
        .form-input:focus, .form-select:focus {
            outline: none; border-color: var(--primary);
            background: rgba(255, 255, 255, 0.08);
            box-shadow: 0 0 0 4px rgba(99, 102, 241, 0.1);
        }

        .checkbox-wrapper {
            display: flex; align-items: center; gap: 12px;
            padding: 16px; background: rgba(255, 255, 255, 0.03);
            border-radius: 12px; cursor: pointer;
            transition: all 0.3s ease; margin-bottom: 12px;
        }
        .checkbox-wrapper:hover { background: rgba(255, 255, 255, 0.06); }
        .checkbox-wrapper input[type="checkbox"] { width: 24px; height: 24px; cursor: pointer; accent-color: var(--primary); }

        .form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
        .btn-group { display: flex; gap: 12px; margin-top: 32px; }

        /* 響應式 */
        @media (min-width: 1024px) { .main-content { grid-template-columns: 1fr 380px; } }
        @media (max-width: 768px) {
            .container { padding: 16px; }
            .top-nav { flex-direction: column; gap: 16px; padding: 20px; }
            .nav-controls { width: 100%; justify-content: center; flex-wrap: wrap; }
            .month-title { font-size: 32px; }
            .calendar-grid { gap: 10px; }
            .day-cell { padding: 10px; border-radius: 12px; }
            .day-number { font-size: 16px; }
            .day-ot-hours { font-size: 18px; }
            .quick-stats, .stats-grid { grid-template-columns: 1fr; }
            .form-row { grid-template-columns: 1fr; }
            .modal-content { padding: 28px; }
            .leave-stats-grid { grid-template-columns: 1fr; }
            .stats-tabs { flex-wrap: wrap; }
        }

        /* 滾動條 */
        ::-webkit-scrollbar { width: 12px; }
        ::-webkit-scrollbar-track { background: rgba(255, 255, 255, 0.05); }
        ::-webkit-scrollbar-thumb { background: rgba(99, 102, 241, 0.5); border-radius: 6px; }
        ::-webkit-scrollbar-thumb:hover { background: rgba(99, 102, 241, 0.7); }
    </style>
</head>
<body>
    <div class="container">
        <!-- 頂部導航 -->
        <nav class="top-nav">
            <div class="logo">
                <div class="logo-icon">⏰</div>
                <span>人資管理系統</span>
            </div>
            <div class="nav-controls">
                <button class="btn btn-ghost" onclick="toggleAnnualLeaveSettings()">🏖️ 年假設定</button>
                <button class="btn btn-ghost" onclick="toggleSettings()">⚙️ 設定</button>
                <button class="btn btn-ghost" onclick="showHolidayManager()">🎌 假日</button>
                <button class="btn btn-primary" onclick="exportData()">💾 匯出</button>
                <button class="btn btn-ghost" onclick="document.getElementById('importFile').click()">📥 匯入</button>
                <input type="file" id="importFile" style="display: none;" onchange="importData(this)" accept=".json">
            </div>
        </nav>

        <!-- 年度特休卡片 -->
        <div class="annual-leave-card">
            <div class="annual-leave-header">
                <div class="annual-leave-title">
                    <span>🏖️</span>
                    <span id="annualLeaveYear">2026年度 特休管理</span>
                </div>
                <button class="btn btn-success" onclick="toggleAnnualLeaveSettings()">⚙️ 設定年假</button>
            </div>
            <div class="leave-stats-grid">
                <div class="leave-stat-item">
                    <div class="leave-stat-label">年度總天數</div>
                    <div class="leave-stat-value" id="annualTotal">0</div>
                </div>
                <div class="leave-stat-item">
                    <div class="leave-stat-label">已使用</div>
                    <div class="leave-stat-value" id="annualUsed" style="color: var(--danger);">0</div>
                </div>
                <div class="leave-stat-item">
                    <div class="leave-stat-label">剩餘天數</div>
                    <div class="leave-stat-value" id="annualRemaining" style="color: var(--success);">0</div>
                </div>
                <div class="leave-stat-item">
                    <div class="leave-stat-label">使用率</div>
                    <div class="leave-stat-value" id="annualUsageRate" style="color: var(--warning);">0%</div>
                </div>
            </div>
        </div>

        <!-- 主要內容 -->
        <div class="main-content">
            <!-- 左側：日曆 -->
            <div>
                <!-- 月份標題 -->
                <div class="month-header">
                    <div class="month-title-row">
                        <h1 class="month-title" id="monthTitle">2026年 2月</h1>
                        <div class="month-nav">
                            <button class="btn btn-ghost" onclick="changeMonth(-1)">❮ 上月</button>
                            <button class="btn btn-ghost" onclick="changeMonth(1)">下月 ❯</button>
                        </div>
                    </div>
                    
                    <!-- 統計切換標籤 -->
                    <div class="stats-tabs">
                        <div class="stats-tab active" onclick="switchStatsView('current')" id="tabCurrent">
                            📅 當月統計
                        </div>
                        <div class="stats-tab" onclick="switchStatsView('cycle')" id="tabCycle">
                            📊 考勤週期統計
                        </div>
                    </div>

                    <div class="quick-stats" id="quickStatsContainer">
                        <!-- 動態生成 -->
                    </div>
                </div>

                <!-- 日曆 -->
                <div class="calendar-container">
                    <div class="calendar-grid">
                        <div class="weekday">週一</div>
                        <div class="weekday">週二</div>
                        <div class="weekday">週三</div>
                        <div class="weekday">週四</div>
                        <div class="weekday">週五</div>
                        <div class="weekday">週六</div>
                        <div class="weekday">週日</div>
                    </div>
                    <div id="calendarDays" class="calendar-grid" style="margin-top: 16px;">
                        <!-- 動態生成 -->
                    </div>
                </div>
            </div>

            <!-- 右側：資訊卡片 -->
            <div class="sidebar">
                <!-- 統計資訊 -->
                <div class="info-card">
                    <h3 class="card-title">
                        <span class="card-icon">📊</span>
                        <span id="statCardTitle">本月詳細統計</span>
                    </h3>
                    <div class="stats-grid" id="statsGrid">
                        <!-- 動態生成 -->
                    </div>
                </div>

                <!-- 日曆圖例 -->
                <div class="info-card">
                    <h3 class="card-title">
                        <span class="card-icon">🎨</span>
                        日曆圖例
                    </h3>
                    <div class="legend-grid">
                        <div class="legend-item">
                            <div class="legend-color" style="background: linear-gradient(135deg, rgba(245, 158, 11, 0.3) 0%, rgba(245, 158, 11, 0.15) 100%); border-color: rgba(245, 158, 11, 0.6);"></div>
                            <span class="legend-text">國定假日</span>
                        </div>
                        <div class="legend-item">
                            <div class="legend-color" style="background: linear-gradient(135deg, rgba(99, 102, 241, 0.2) 0%, rgba(99, 102, 241, 0.08) 100%); border: 2px dashed rgba(99, 102, 241, 0.5);"></div>
                            <span class="legend-text">補班日</span>
                        </div>
                        <div class="legend-item">
                            <div class="legend-color" style="background: linear-gradient(135deg, rgba(16, 185, 129, 0.2) 0%, rgba(16, 185, 129, 0.08) 100%); border-color: rgba(16, 185, 129, 0.4);"></div>
                            <span class="legend-text">臨時假日</span>
                        </div>
                        <div class="legend-item">
                            <div class="legend-color" style="background: linear-gradient(135deg, rgba(236, 72, 153, 0.15) 0%, rgba(236, 72, 153, 0.05) 100%); border-color: rgba(236, 72, 153, 0.2);"></div>
                            <span class="legend-text">週末休息</span>
                        </div>
                        <div class="legend-item">
                            <div class="legend-color" style="background: linear-gradient(135deg, rgba(245, 158, 11, 0.3) 0%, rgba(245, 158, 11, 0.15) 100%); border: 2px solid rgba(245, 158, 11, 0.6);"></div>
                            <span class="legend-text">有加班</span>
                        </div>
                        <div class="legend-item">
                            <div class="legend-color" style="background: linear-gradient(135deg, rgba(6, 182, 212, 0.25) 0%, rgba(6, 182, 212, 0.1) 100%); border: 2px solid rgba(6, 182, 212, 0.5);"></div>
                            <span class="legend-text">有請假</span>
                        </div>
                        <div class="legend-item">
                            <div class="legend-color" style="background: linear-gradient(135deg, rgba(99, 102, 241, 0.25) 0%, rgba(245, 158, 11, 0.25) 100%); border-left: 6px solid var(--primary);"></div>
                            <span class="legend-text">已報備</span>
                        </div>
                    </div>
                </div>

                <!-- 考勤週期 -->
                <div class="info-card">
                    <h3 class="card-title">
                        <span class="card-icon">📅</span>
                        考勤週期
                    </h3>
                    <div id="cyclePeriodDisplay" style="color: var(--text-secondary); margin-bottom: 16px;">
                        請設定考勤週期
                    </div>
                    <button class="btn btn-primary" style="width: 100%;" onclick="toggleCyclePanel()">
                        設定週期
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- 加班/請假記錄彈窗 -->
    <div id="inputModal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 class="modal-title" id="inputModalTitle">記錄</h2>
                <button class="modal-close" onclick="closeInputModal()">×</button>
            </div>
            
            <!-- 加班區塊 -->
            <div style="margin-bottom: 28px;">
                <h3 style="font-size: 18px; margin-bottom: 16px; font-weight: 700; color: var(--warning);">⏰ 加班記錄</h3>
                
                <div class="form-group">
                    <label class="form-label">加班時數</label>
                    <input type="number" step="0.5" id="otHours" class="form-input" placeholder="例如：8" oninput="updateOTPreview()">
                </div>

                <div id="otPreview" style="background: rgba(99, 102, 241, 0.1); padding: 16px; border-radius: 12px; margin-bottom: 16px; display: none;">
                    <div style="font-size: 13px; color: var(--text-secondary); margin-bottom: 8px;">💰 加班費試算</div>
                    <div id="otBreakdown" style="font-size: 14px; color: var(--text-primary);"></div>
                    <div style="border-top: 1px solid rgba(255,255,255,0.1); margin-top: 12px; padding-top: 12px;">
                        <div style="display: flex; justify-content: space-between; font-weight: 700;">
                            <span>總加班費：</span>
                            <span id="otTotalPay" style="color: var(--success); font-size: 18px;">$0</span>
                        </div>
                    </div>
                </div>

                <div class="checkbox-wrapper">
                    <input type="checkbox" id="reportedOT">
                    <label for="reportedOT" style="cursor: pointer; font-weight: 600;">✅ 已向公司報備此加班</label>
                </div>

                <div class="checkbox-wrapper">
                    <input type="checkbox" id="deferredPayment">
                    <label for="deferredPayment" style="cursor: pointer; font-weight: 600;">📅 延至下月計薪</label>
                </div>
            </div>

            <!-- 請假區塊 -->
            <div style="margin-bottom: 28px;">
                <h3 style="font-size: 18px; margin-bottom: 16px; font-weight: 700; color: var(--info);">🏖️ 請假記錄</h3>
                <div class="form-row">
                    <div class="form-group">
                        <label class="form-label">請假類型</label>
                        <select id="leaveType" class="form-select">
                            <option value="">無請假</option>
                            <option value="annual">特休假</option>
                            <option value="sick">病假</option>
                            <option value="personal">事假</option>
                            <option value="other">其他假別</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label class="form-label">請假時數</label>
                        <input type="number" step="0.5" id="leaveDays" class="form-input" placeholder="例如：8 或 4">
                    </div>
                </div>
            </div>

            <div class="btn-group">
                <button class="btn btn-success btn-full" onclick="saveRecord()">💾 儲存</button>
                <button class="btn btn-danger" onclick="deleteRecord()">🗑️ 刪除</button>
                <button class="btn btn-ghost" onclick="closeInputModal()">取消</button>
            </div>
        </div>
    </div>

    <!-- 年假設定彈窗 -->
    <div id="annualLeaveModal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 class="modal-title">年度特休設定</h2>
                <button class="modal-close" onclick="toggleAnnualLeaveSettings()">×</button>
            </div>

            <div class="form-group">
                <label class="form-label">選擇年度</label>
                <select id="annualLeaveYearSelect" class="form-select" onchange="loadAnnualLeaveYear()">
                    <option value="2024">2024年</option>
                    <option value="2025">2025年</option>
                    <option value="2026" selected>2026年</option>
                    <option value="2027">2027年</option>
                </select>
            </div>

            <div class="form-group">
                <label class="form-label">年度特休總天數</label>
                <input type="number" step="0.5" id="annualLeaveTotalInput" class="form-input" placeholder="例如：14" onchange="saveAnnualLeaveSettings()">
            </div>

            <div style="background: rgba(255,255,255,0.03); padding: 20px; border-radius: 16px; margin-top: 20px;">
                <div style="font-size: 14px; color: var(--text-secondary); margin-bottom: 12px;">📊 年度使用統計</div>
                <div style="display: grid; gap: 12px;">
                    <div style="display: flex; justify-content: space-between;">
                        <span style="color: var(--text-muted);">總天數：</span>
                        <span style="font-weight: 700; color: var(--success);" id="modalAnnualTotal">0 天</span>
                    </div>
                    <div style="display: flex; justify-content: space-between;">
                        <span style="color: var(--text-muted);">已使用：</span>
                        <span style="font-weight: 700; color: var(--danger);" id="modalAnnualUsed">0 天</span>
                    </div>
                    <div style="display: flex; justify-content: space-between;">
                        <span style="color: var(--text-muted);">剩餘：</span>
                        <span style="font-weight: 700; color: var(--success);" id="modalAnnualRemaining">0 天</span>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- 系統設定彈窗 -->
    <div id="settingsModal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 class="modal-title">系統設定</h2>
                <button class="modal-close" onclick="toggleSettings()">×</button>
            </div>

            <div class="form-group">
                <label class="form-label">月薪（元）</label>
                <input type="number" id="monthlySalary" class="form-input" placeholder="例如：30000" onchange="saveSettings()">
            </div>

            <div class="form-group">
                <label class="form-label">時薪（自動計算）</label>
                <input type="text" id="hourlyRate" class="form-input" readonly style="background: rgba(255,255,255,0.5); color: #64748b;">
            </div>

            <div class="form-group">
                <label class="form-label">目標加班費（元）</label>
                <input type="number" id="targetPay" class="form-input" placeholder="例如：6000" onchange="calculateTargetHours()">
            </div>

            <div style="background: rgba(255,255,255,0.05); padding: 20px; border-radius: 16px; margin-top: 20px;">
                <div style="font-size: 14px; color: var(--text-secondary); margin-bottom: 12px;">📊 建議加班時數組合</div>
                <div id="targetHoursBreakdown" style="display: grid; gap: 12px; color: var(--text-secondary);">
                    <!-- 動態生成 -->
                </div>
            </div>
        </div>
    </div>

    <!-- 考勤週期彈窗 -->
    <div id="cycleModal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 class="modal-title">設定考勤週期</h2>
                <button class="modal-close" onclick="toggleCyclePanel()">×</button>
            </div>

            <div class="form-row">
                <div class="form-group">
                    <label class="form-label">起始日期</label>
                    <input type="date" id="cycleStartDate" class="form-input" onchange="saveMonthlyCycle()">
                </div>
                <div class="form-group">
                    <label class="form-label">結束日期</label>
                    <input type="date" id="cycleEndDate" class="form-input" onchange="saveMonthlyCycle()">
                </div>
            </div>

            <div style="display: grid; gap: 12px; margin-top: 20px;">
                <button class="btn btn-ghost" onclick="useCurrentMonth()">📅 使用整月（1日～月底）</button>
                <button class="btn btn-ghost" onclick="use16thCycle()">🔄 使用16號制（跨月）</button>
                <button class="btn btn-ghost" onclick="copyPreviousCycle()">📋 複製上月設定</button>
            </div>
        </div>
    </div>

    <!-- 假日管理彈窗 -->
    <div id="holidayModal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 class="modal-title">假日調休管理</h2>
                <button class="modal-close" onclick="closeHolidayManager()">×</button>
            </div>

            <div style="margin-bottom: 28px;">
                <h3 style="font-size: 16px; margin-bottom: 12px; font-weight: 700;">📅 新增臨時假日</h3>
                <div style="display: flex; gap: 12px; flex-wrap: wrap;">
                    <input type="date" id="customHolidayDate" class="form-input" style="flex: 0 0 auto; width: auto;">
                    <input type="text" id="customHolidayName" class="form-input" placeholder="假日名稱" style="flex: 1;">
                    <button class="btn btn-success" onclick="addCustomHoliday()">➕ 新增</button>
                </div>
            </div>

            <div style="margin-bottom: 28px;">
                <h3 style="font-size: 16px; margin-bottom: 12px; font-weight: 700;">🔄 新增補班日</h3>
                <div style="display: flex; gap: 12px; flex-wrap: wrap;">
                    <input type="date" id="makeupWorkDate" class="form-input" style="flex: 0 0 auto; width: auto;">
                    <input type="text" id="makeupWorkReason" class="form-input" placeholder="補班原因" style="flex: 1;">
                    <button class="btn btn-primary" onclick="addMakeupWorkDay()">➕ 新增</button>
                </div>
            </div>

            <div style="background: rgba(255,255,255,0.03); border-radius: 16px; padding: 20px;">
                <h3 style="font-size: 16px; margin-bottom: 16px; font-weight: 700;">📋 已設定的假日</h3>
                <div id="holidayList" style="max-height: 400px; overflow-y: auto;">
                    <!-- 動態生成 -->
                </div>
            </div>
        </div>
    </div>

    <script>
        // 全域變數
        let currentDate = new Date();
        let selectedDay = null;
        let overtimeData = {};
        let leaveData = {};
        let monthlyCycles = {};
        let nationalHolidays = {};
        let makeupWorkDays = {};
        let customHolidays = {};
        let annualLeaveSettings = {};
        let currentStatsView = 'current';

        const DEFAULT_HOLIDAYS_2026 = {
            "2026-01-01": "元旦", "2026-02-15": "小年夜", "2026-02-16": "除夕",
            "2026-02-17": "春節", "2026-02-18": "春節", "2026-02-19": "春節",
            "2026-02-20": "小年夜補假", "2026-02-27": "和平紀念日補假",
            "2026-02-28": "和平紀念日", "2026-04-03": "兒童節",
            "2026-04-04": "清明節", "2026-04-05": "清明節補假",
            "2026-05-01": "勞動節", "2026-06-25": "端午節",
            "2026-09-28": "教師節", "2026-10-01": "中秋節",
            "2026-10-10": "國慶日", "2026-10-25": "台灣光復節",
            "2026-12-25": "行憲紀念日"
        };

        function init() {
            loadData();
            if (!nationalHolidays || Object.keys(nationalHolidays).length === 0) {
                nationalHolidays = {...DEFAULT_HOLIDAYS_2026};
                saveData();
            }
            renderCalendar();
            updateStats();
            updateAnnualLeaveDisplay();
            const monthKey = getCurrentMonthKey();
            if (!monthlyCycles[monthKey]) autoSetMonthlyCycle();
            else loadMonthlyCycle();
        }

        function saveData() {
            localStorage.setItem('hr_overtime_data', JSON.stringify(overtimeData));
            localStorage.setItem('hr_leave_data', JSON.stringify(leaveData));
            localStorage.setItem('hr_holidays', JSON.stringify(nationalHolidays));
            localStorage.setItem('hr_makeup', JSON.stringify(makeupWorkDays));
            localStorage.setItem('hr_custom', JSON.stringify(customHolidays));
            localStorage.setItem('hr_annual_leave', JSON.stringify(annualLeaveSettings));
        }

        function loadData() {
            overtimeData = JSON.parse(localStorage.getItem('hr_overtime_data') || '{}');
            leaveData = JSON.parse(localStorage.getItem('hr_leave_data') || '{}');
            nationalHolidays = JSON.parse(localStorage.getItem('hr_holidays') || JSON.stringify(DEFAULT_HOLIDAYS_2026));
            makeupWorkDays = JSON.parse(localStorage.getItem('hr_makeup') || '{}');
            customHolidays = JSON.parse(localStorage.getItem('hr_custom') || '{}');
            monthlyCycles = JSON.parse(localStorage.getItem('hr_cycles') || '{}');
            annualLeaveSettings = JSON.parse(localStorage.getItem('hr_annual_leave') || '{}');

            const monthlySalary = localStorage.getItem('monthlySalary');
            const targetPay = localStorage.getItem('targetPay');
            if (monthlySalary) document.getElementById('monthlySalary').value = monthlySalary;
            if (targetPay) document.getElementById('targetPay').value = targetPay;
            calculateHourlyRate();
            calculateTargetHours();
        }

        function saveSettings() {
            const monthlySalary = document.getElementById('monthlySalary').value;
            const targetPayInput = document.getElementById('targetPay').value;
            if (monthlySalary) localStorage.setItem('monthlySalary', monthlySalary);
            if (targetPayInput) localStorage.setItem('targetPay', targetPayInput);
            calculateHourlyRate();
            calculateTargetHours();
            updateStats();
        }

        function calculateHourlyRate() {
            const monthlySalary = parseFloat(document.getElementById('monthlySalary').value) || 0;
            if (monthlySalary > 0) {
                const hourlyRate = Math.round(monthlySalary / 30 / 8);
                document.getElementById('hourlyRate').value = `${hourlyRate} 元/時`;
            }
        }

        function calculateTargetHours() {
            const targetPayValue = parseFloat(document.getElementById('targetPay').value) || 0;
            const monthlySalary = parseFloat(document.getElementById('monthlySalary').value) || 0;
            
            if (targetPayValue === 0 || monthlySalary === 0) {
                document.getElementById('targetHoursBreakdown').innerHTML = '<div style="text-align: center; color: var(--text-muted); padding: 10px;">請先設定月薪和目標加班費</div>';
                return;
            }
            
            const hourlyRate = monthlySalary / 30 / 8;
            const hours_134 = targetPayValue / (hourlyRate * 1.34);
            
            // 方案1: 主要用1.34倍
            let combo1_134 = Math.floor(hours_134 * 0.7);
            const remaining1 = targetPayValue - (combo1_134 * hourlyRate * 1.34);
            let combo1_167 = Math.ceil(remaining1 / (hourlyRate * 1.67));
            const combo1_total = (combo1_134 * hourlyRate * 1.34) + (combo1_167 * hourlyRate * 1.67);
            
            // 方案2: 平衡組合
            let combo2_134 = Math.floor(hours_134 * 0.5);
            const remaining2 = targetPayValue - (combo2_134 * hourlyRate * 1.34);
            let combo2_167 = Math.ceil(remaining2 / (hourlyRate * 1.67));
            const combo2_total = (combo2_134 * hourlyRate * 1.34) + (combo2_167 * hourlyRate * 1.67);
            
            let html = `
                <div style="background: rgba(99, 102, 241, 0.1); padding: 16px; border-radius: 12px; border: 1px solid rgba(99, 102, 241, 0.3);">
                    <div style="font-weight: 700; margin-bottom: 10px; color: var(--primary);">💡 方案一（多用前2h）</div>
                    <div style="display: grid; gap: 8px; font-size: 14px;">
                        <div style="display: flex; justify-content: space-between;">
                            <span>前2小時 (1.34倍)：</span>
                            <span style="font-weight: 700; color: var(--text-primary);">${combo1_134}小時</span>
                        </div>
                        <div style="display: flex; justify-content: space-between;">
                            <span>3小時起 (1.67倍)：</span>
                            <span style="font-weight: 700; color: var(--text-primary);">${combo1_167}小時</span>
                        </div>
                        <div style="border-top: 1px solid rgba(255,255,255,0.1); margin-top: 8px; padding-top: 8px; display: flex; justify-content: space-between;">
                            <span>預計加班費：</span>
                            <span style="font-weight: 900; color: var(--success);">$${Math.round(combo1_total).toLocaleString()}</span>
                        </div>
                    </div>
                </div>
                
                <div style="background: rgba(16, 185, 129, 0.1); padding: 16px; border-radius: 12px; border: 1px solid rgba(16, 185, 129, 0.3);">
                    <div style="font-weight: 700; margin-bottom: 10px; color: var(--success);">🎯 方案二（平衡組合）</div>
                    <div style="display: grid; gap: 8px; font-size: 14px;">
                        <div style="display: flex; justify-content: space-between;">
                            <span>前2小時 (1.34倍)：</span>
                            <span style="font-weight: 700; color: var(--text-primary);">${combo2_134}小時</span>
                        </div>
                        <div style="display: flex; justify-content: space-between;">
                            <span>3小時起 (1.67倍)：</span>
                            <span style="font-weight: 700; color: var(--text-primary);">${combo2_167}小時</span>
                        </div>
                        <div style="border-top: 1px solid rgba(255,255,255,0.1); margin-top: 8px; padding-top: 8px; display: flex; justify-content: space-between;">
                            <span>預計加班費：</span>
                            <span style="font-weight: 900; color: var(--success);">$${Math.round(combo2_total).toLocaleString()}</span>
                        </div>
                    </div>
                </div>
                
                <div style="background: rgba(255, 255, 255, 0.03); padding: 12px; border-radius: 8px; font-size: 13px; color: var(--text-muted);">
                    ℹ️ 若全部為前2小時 (1.34倍)：需 <strong style="color: var(--text-primary);">${hours_134.toFixed(1)}</strong> 小時
                </div>
            `;
            
            document.getElementById('targetHoursBreakdown').innerHTML = html;
        }

        function switchStatsView(view) {
            currentStatsView = view;
            document.getElementById('tabCurrent').classList.toggle('active', view === 'current');
            document.getElementById('tabCycle').classList.toggle('active', view === 'cycle');
            document.getElementById('statCardTitle').textContent = view === 'current' ? '本月詳細統計' : '考勤週期詳細統計';
            updateStats();
        }

        function renderCalendar() {
            const year = currentDate.getFullYear();
            const month = currentDate.getMonth();
            document.getElementById('monthTitle').textContent = `${year}年 ${month + 1}月`;
            
            const firstDay = new Date(year, month, 1);
            const lastDay = new Date(year, month + 1, 0);
            const daysInMonth = lastDay.getDate();
            let startOffset = firstDay.getDay() - 1;
            if (startOffset < 0) startOffset = 6;
            
            const calendarDays = document.getElementById('calendarDays');
            calendarDays.innerHTML = '';
            
            for (let i = 0; i < startOffset; i++) {
                calendarDays.innerHTML += '<div></div>';
            }
            
            for (let day = 1; day <= daysInMonth; day++) {
                const dateStr = `${year}-${String(month + 1).padStart(2, '0')}-${String(day).padStart(2, '0')}`;
                const dayOfWeek = new Date(year, month, day).getDay();
                const isWeekend = dayOfWeek === 0 || dayOfWeek === 6;
                const isNationalHoliday = nationalHolidays[dateStr];
                const isMakeupDay = makeupWorkDays[dateStr];
                const isCustomHoliday = customHolidays[dateStr];
                const otRecord = overtimeData[dateStr];
                const leaveRecord = leaveData[dateStr];
                
                let classes = ['day-cell'];
                if (isWeekend && !isMakeupDay) classes.push('day-rest');
                if (isNationalHoliday) classes.push('day-national-holiday');
                if (isMakeupDay) classes.push('day-makeup');
                if (isCustomHoliday) classes.push('day-custom-holiday');
                if (otRecord) {
                    classes.push('has-overtime');
                    if (otRecord.reported) classes.push('day-is-reported');
                }
                if (leaveRecord) classes.push('has-leave');
                
                let badges = '';
                if (isWeekend && !isMakeupDay) badges += '<div class="rest-badge">休</div>';
                if (isNationalHoliday) badges += `<div class="holiday-badge">${isNationalHoliday}</div>`;
                if (isMakeupDay) badges += `<div class="holiday-badge makeup-badge">${isMakeupDay}</div>`;
                if (isCustomHoliday) badges += `<div class="holiday-badge custom-badge">${isCustomHoliday}</div>`;
                if (otRecord) {
                    if (otRecord.reported) badges += '<div class="reported-indicator">已報</div>';
                    if (otRecord.deferred) badges += '<div class="deferred-indicator">延計</div>';
                }
                if (leaveRecord && leaveRecord.type) {
                    const leaveLabels = { 'annual': '特休', 'sick': '病假', 'personal': '事假', 'other': '其他' };
                    badges += `<div class="leave-indicator">${leaveLabels[leaveRecord.type]}</div>`;
                }
                
                let otDisplay = '';
                if (otRecord) otDisplay = `<div class="day-ot-hours">${otRecord.hours}h</div>`;
                
                calendarDays.innerHTML += `
                    <div class="${classes.join(' ')}" onclick="selectDay('${dateStr}')">
                        ${badges}
                        <div class="day-number">${day}</div>
                        ${otDisplay}
                    </div>
                `;
            }
        }

        function selectDay(dateStr) {
            selectedDay = dateStr;
            const otRecord = overtimeData[dateStr];
            const leaveRecord = leaveData[dateStr];
            
            document.getElementById('inputModalTitle').textContent = `${dateStr} 記錄`;
            
            if (otRecord) {
                document.getElementById('otHours').value = otRecord.hours || '';
                document.getElementById('reportedOT').checked = otRecord.reported || false;
                document.getElementById('deferredPayment').checked = otRecord.deferred || false;
            } else {
                document.getElementById('otHours').value = '';
                document.getElementById('reportedOT').checked = false;
                document.getElementById('deferredPayment').checked = false;
            }
            
            updateOTPreview();
            
            if (leaveRecord) {
                document.getElementById('leaveType').value = leaveRecord.type || '';
                document.getElementById('leaveDays').value = leaveRecord.days || '';
            } else {
                document.getElementById('leaveType').value = '';
                document.getElementById('leaveDays').value = '';
            }
            
            document.getElementById('inputModal').classList.add('active');
            document.getElementById('otHours').focus();
        }

        function updateOTPreview() {
            const hours = parseFloat(document.getElementById('otHours').value) || 0;
            const preview = document.getElementById('otPreview');
            
            if (hours <= 0 || !selectedDay) {
                preview.style.display = 'none';
                return;
            }
            
            const monthlySalary = parseFloat(document.getElementById('monthlySalary').value) || 0;
            if (monthlySalary === 0) {
                preview.style.display = 'none';
                return;
            }
            
            const hourlyRate = monthlySalary / 30 / 8;
            
            let hours_134 = 0;
            let hours_167 = 0;
            let pay_134 = 0;
            let pay_167 = 0;
            
            if (hours <= 2) {
                hours_134 = hours;
                pay_134 = hours_134 * hourlyRate * 1.34;
            } else {
                hours_134 = 2;
                hours_167 = hours - 2;
                pay_134 = hours_134 * hourlyRate * 1.34;
                pay_167 = hours_167 * hourlyRate * 1.67;
            }
            
            const totalPay = pay_134 + pay_167;
            
            let breakdown = `
                <div style="display: grid; gap: 6px;">
                    <div style="display: flex; justify-content: space-between;">
                        <span>前2小時 (1.34倍)：${hours_134.toFixed(1)}h</span>
                        <span>$${Math.round(pay_134).toLocaleString()}</span>
                    </div>
            `;
            
            if (hours_167 > 0) {
                breakdown += `
                    <div style="display: flex; justify-content: space-between;">
                        <span>超過2小時 (1.67倍)：${hours_167.toFixed(1)}h</span>
                        <span>$${Math.round(pay_167).toLocaleString()}</span>
                    </div>
                `;
            }
            
            breakdown += `</div>`;
            
            document.getElementById('otBreakdown').innerHTML = breakdown;
            document.getElementById('otTotalPay').textContent = `$${Math.round(totalPay).toLocaleString()}`;
            preview.style.display = 'block';
        }

        function closeInputModal() {
            document.getElementById('inputModal').classList.remove('active');
            selectedDay = null;
        }

        function saveRecord() {
            if (!selectedDay) return;
            
            const hours = parseFloat(document.getElementById('otHours').value);
            const reported = document.getElementById('reportedOT').checked;
            const deferred = document.getElementById('deferredPayment').checked;
            
            if (hours && hours > 0) {
                overtimeData[selectedDay] = { hours, reported, deferred };
            } else {
                delete overtimeData[selectedDay];
            }
            
            const leaveType = document.getElementById('leaveType').value;
            const leaveDays = parseFloat(document.getElementById('leaveDays').value);
            
            if (leaveType && leaveDays && leaveDays > 0) {
                leaveData[selectedDay] = { type: leaveType, days: leaveDays };
            } else {
                delete leaveData[selectedDay];
            }
            
            saveData();
            renderCalendar();
            updateStats();
            updateAnnualLeaveDisplay();
            closeInputModal();
        }

        function deleteRecord() {
            if (!selectedDay) return;
            if (confirm(`確定要刪除 ${selectedDay} 的所有記錄嗎？`)) {
                delete overtimeData[selectedDay];
                delete leaveData[selectedDay];
                saveData();
                renderCalendar();
                updateStats();
                updateAnnualLeaveDisplay();
                closeInputModal();
            }
        }

        function calculateOTPay(hours) {
            const monthlySalary = parseFloat(document.getElementById('monthlySalary').value) || 0;
            if (monthlySalary === 0 || !hours) return 0;
            const hourlyRate = monthlySalary / 30 / 8;
            
            let pay = 0;
            if (hours <= 2) {
                pay = hours * hourlyRate * 1.34;
            } else {
                pay = (2 * hourlyRate * 1.34) + ((hours - 2) * hourlyRate * 1.67);
            }
            return Math.round(pay);
        }

        function updateStats() {
            const year = currentDate.getFullYear();
            const month = currentDate.getMonth();
            
            let statsData = {
                totalHours: 0, totalPay: 0, reportedHours: 0, reportedPay: 0,
                unreportedHours: 0, unreportedPay: 0, deferredHours: 0, deferredPay: 0,
                currentMonthPay: 0, daysWithOT: 0, leaveDays: 0
            };
            
            if (currentStatsView === 'current') {
                const firstDay = new Date(year, month, 1);
                const lastDay = new Date(year, month + 1, 0);
                
                for (let d = new Date(firstDay); d <= lastDay; d.setDate(d.getDate() + 1)) {
                    const dateStr = formatDateStr(d);
                    const record = overtimeData[dateStr];
                    const leave = leaveData[dateStr];
                    
                    if (record) {
                        const pay = calculateOTPay(record.hours);
                        statsData.totalHours += record.hours;
                        statsData.totalPay += pay;
                        statsData.daysWithOT++;
                        
                        if (record.reported) {
                            statsData.reportedHours += record.hours;
                            statsData.reportedPay += pay;
                        } else {
                            statsData.unreportedHours += record.hours;
                            statsData.unreportedPay += pay;
                        }
                        
                        if (record.deferred) {
                            statsData.deferredHours += record.hours;
                            statsData.deferredPay += pay;
                        } else {
                            statsData.currentMonthPay += pay;
                        }
                    }
                    
                    if (leave && leave.days) statsData.leaveDays += leave.days;
                }
            } else {
                const monthKey = getCurrentMonthKey();
                const cycle = monthlyCycles[monthKey];
                
                if (cycle) {
                    const startDate = new Date(cycle.startDate);
                    const endDate = new Date(cycle.endDate);
                    
                    for (let d = new Date(startDate); d <= endDate; d.setDate(d.getDate() + 1)) {
                        const dateStr = formatDateStr(d);
                        const record = overtimeData[dateStr];
                        const leave = leaveData[dateStr];
                        
                        if (record) {
                            const pay = calculateOTPay(record.hours);
                            statsData.totalHours += record.hours;
                            statsData.totalPay += pay;
                            statsData.daysWithOT++;
                            
                            if (record.reported) {
                                statsData.reportedHours += record.hours;
                                statsData.reportedPay += pay;
                            } else {
                                statsData.unreportedHours += record.hours;
                                statsData.unreportedPay += pay;
                            }
                            
                            if (record.deferred) {
                                statsData.deferredHours += record.hours;
                                statsData.deferredPay += pay;
                            } else {
                                statsData.currentMonthPay += pay;
                            }
                        }
                        
                        if (leave && leave.days) statsData.leaveDays += leave.days;
                    }
                }
            }
            
            const targetPayValue = parseFloat(localStorage.getItem('targetPay')) || 0;
            const monthlySalary = parseFloat(document.getElementById('monthlySalary').value) || 0;
            let targetOT = 0;
            if (targetPayValue > 0 && monthlySalary > 0) {
                const hourlyRate = monthlySalary / 30 / 8;
                targetOT = targetPayValue / (hourlyRate * 1.34); // 用1.34倍計算目標時數
            }
            const progressPercent = targetOT > 0 ? Math.round((statsData.totalHours / targetOT) * 100) : 0;
            
            const quickStatsHTML = `
                <div class="quick-stat">
                    <div class="quick-stat-label">總加班時數</div>
                    <div class="quick-stat-value">${statsData.totalHours.toFixed(1)}h</div>
                </div>
                <div class="quick-stat">
                    <div class="quick-stat-label">總加班費</div>
                    <div class="quick-stat-value">$${statsData.totalPay.toLocaleString()}</div>
                </div>
                <div class="quick-stat">
                    <div class="quick-stat-label">本月實領</div>
                    <div class="quick-stat-value" style="color: var(--success);">$${statsData.currentMonthPay.toLocaleString()}</div>
                </div>
                <div class="quick-stat">
                    <div class="quick-stat-label">延至下月</div>
                    <div class="quick-stat-value" style="color: var(--warning);">$${statsData.deferredPay.toLocaleString()}</div>
                </div>
                <div class="quick-stat">
                    <div class="quick-stat-label">請假時數</div>
                    <div class="quick-stat-value" style="color: var(--info);">${statsData.leaveDays.toFixed(1)}h</div>
                </div>
                <div class="quick-stat">
                    <div class="quick-stat-label">目標達成</div>
                    <div class="quick-stat-value">${progressPercent}%</div>
                </div>
            `;
            document.getElementById('quickStatsContainer').innerHTML = quickStatsHTML;
            
            const detailStatsHTML = `
                <div class="stat-item">
                    <div class="stat-label">已報備</div>
                    <div class="stat-value">${statsData.reportedHours.toFixed(1)}<span class="stat-unit">h</span></div>
                </div>
                <div class="stat-item">
                    <div class="stat-label">未報備</div>
                    <div class="stat-value">${statsData.unreportedHours.toFixed(1)}<span class="stat-unit">h</span></div>
                </div>
                <div class="stat-item">
                    <div class="stat-label">加班天數</div>
                    <div class="stat-value">${statsData.daysWithOT}<span class="stat-unit">天</span></div>
                </div>
                <div class="stat-item">
                    <div class="stat-label">平均時數</div>
                    <div class="stat-value">${statsData.daysWithOT > 0 ? (statsData.totalHours / statsData.daysWithOT).toFixed(1) : '0'}<span class="stat-unit">h</span></div>
                </div>
                <div class="stat-item">
                    <div class="stat-label">延計時數</div>
                    <div class="stat-value">${statsData.deferredHours.toFixed(1)}<span class="stat-unit">h</span></div>
                </div>
                <div class="stat-item">
                    <div class="stat-label">請假時數</div>
                    <div class="stat-value">${statsData.leaveDays.toFixed(1)}<span class="stat-unit">h</span></div>
                </div>
            `;
            document.getElementById('statsGrid').innerHTML = detailStatsHTML;
        }

        function updateAnnualLeaveDisplay() {
            const year = currentDate.getFullYear();
            document.getElementById('annualLeaveYear').textContent = `${year}年度 特休管理`;
            
            const yearKey = String(year);
            const settings = annualLeaveSettings[yearKey] || { total: 0 };
            
            let usedDays = 0;
            Object.entries(leaveData).forEach(([date, record]) => {
                if (record.type === 'annual' && date.startsWith(yearKey)) {
                    usedDays += record.days || 0;
                }
            });
            
            const totalDays = settings.total || 0;
            const remainingDays = totalDays - usedDays;
            const usageRate = totalDays > 0 ? Math.round((usedDays / totalDays) * 100) : 0;
            
            document.getElementById('annualTotal').textContent = totalDays.toFixed(1);
            document.getElementById('annualUsed').textContent = usedDays.toFixed(1);
            document.getElementById('annualRemaining').textContent = remainingDays.toFixed(1);
            document.getElementById('annualUsageRate').textContent = `${usageRate}%`;
        }

        function toggleAnnualLeaveSettings() {
            const modal = document.getElementById('annualLeaveModal');
            modal.classList.toggle('active');
            if (modal.classList.contains('active')) loadAnnualLeaveYear();
        }

        function loadAnnualLeaveYear() {
            const year = document.getElementById('annualLeaveYearSelect').value;
            const settings = annualLeaveSettings[year] || { total: 0 };
            
            document.getElementById('annualLeaveTotalInput').value = settings.total || '';
            
            let usedDays = 0;
            Object.entries(leaveData).forEach(([date, record]) => {
                if (record.type === 'annual' && date.startsWith(year)) {
                    usedDays += record.days || 0;
                }
            });
            
            const totalDays = settings.total || 0;
            const remainingDays = totalDays - usedDays;
            
            document.getElementById('modalAnnualTotal').textContent = `${totalDays.toFixed(1)} 天`;
            document.getElementById('modalAnnualUsed').textContent = `${usedDays.toFixed(1)} 天`;
            document.getElementById('modalAnnualRemaining').textContent = `${remainingDays.toFixed(1)} 天`;
        }

        function saveAnnualLeaveSettings() {
            const year = document.getElementById('annualLeaveYearSelect').value;
            const total = parseFloat(document.getElementById('annualLeaveTotalInput').value) || 0;
            
            annualLeaveSettings[year] = { total };
            saveData();
            loadAnnualLeaveYear();
            updateAnnualLeaveDisplay();
        }

        function changeMonth(delta) {
            currentDate.setMonth(currentDate.getMonth() + delta);
            renderCalendar();
            updateStats();
            updateAnnualLeaveDisplay();
            
            const monthKey = getCurrentMonthKey();
            if (!monthlyCycles[monthKey]) autoSetMonthlyCycle();
            else loadMonthlyCycle();
        }

        function toggleSettings() {
            document.getElementById('settingsModal').classList.toggle('active');
        }

        function toggleCyclePanel() {
            document.getElementById('cycleModal').classList.toggle('active');
        }

        function showHolidayManager() {
            updateHolidayList();
            document.getElementById('holidayModal').classList.add('active');
        }

        function closeHolidayManager() {
            document.getElementById('holidayModal').classList.remove('active');
        }

        function addCustomHoliday() {
            const date = document.getElementById('customHolidayDate').value;
            const name = document.getElementById('customHolidayName').value;
            
            if (!date || !name) {
                alert('請填寫完整資訊！');
                return;
            }
            
            customHolidays[date] = name;
            saveData();
            renderCalendar();
            updateHolidayList();
            
            document.getElementById('customHolidayDate').value = '';
            document.getElementById('customHolidayName').value = '';
        }

        function addMakeupWorkDay() {
            const date = document.getElementById('makeupWorkDate').value;
            const reason = document.getElementById('makeupWorkReason').value;
            
            if (!date || !reason) {
                alert('請填寫完整資訊！');
                return;
            }
            
            makeupWorkDays[date] = reason;
            saveData();
            renderCalendar();
            updateHolidayList();
            
            document.getElementById('makeupWorkDate').value = '';
            document.getElementById('makeupWorkReason').value = '';
        }

        function updateHolidayList() {
            let html = '';
            
            const allHolidays = [
                ...Object.entries(nationalHolidays).map(([date, name]) => ({date, name, type: '國定'})),
                ...Object.entries(makeupWorkDays).map(([date, name]) => ({date, name, type: '補班'})),
                ...Object.entries(customHolidays).map(([date, name]) => ({date, name, type: '臨時'}))
            ].sort((a, b) => a.date.localeCompare(b.date));
            
            if (allHolidays.length === 0) {
                html = '<div style="text-align: center; color: var(--text-muted); padding: 20px;">尚未設定</div>';
            } else {
                allHolidays.forEach(({date, name, type}) => {
                    const bgColor = type === '國定' ? 'rgba(245,158,11,0.2)' : type === '補班' ? 'rgba(99,102,241,0.2)' : 'rgba(16,185,129,0.2)';
                    html += `
                        <div style="display: flex; justify-content: space-between; align-items: center; padding: 12px; background: ${bgColor}; border-radius: 10px; margin-bottom: 8px;">
                            <span style="font-size: 13px;"><strong>${date}</strong> - [${type}] ${name}</span>
                            <button class="btn btn-danger" style="padding: 6px 12px; font-size: 12px;" onclick="deleteHoliday('${date}', '${type}')">刪除</button>
                        </div>
                    `;
                });
            }
            
            document.getElementById('holidayList').innerHTML = html;
        }

        function deleteHoliday(date, type) {
            if (!confirm('確定要刪除嗎？')) return;
            
            if (type === '國定') delete nationalHolidays[date];
            else if (type === '補班') delete makeupWorkDays[date];
            else if (type === '臨時') delete customHolidays[date];
            
            saveData();
            renderCalendar();
            updateHolidayList();
        }

        function getCurrentMonthKey() {
            const year = currentDate.getFullYear();
            const month = currentDate.getMonth() + 1;
            return `${year}-${String(month).padStart(2, '0')}`;
        }

        function loadMonthlyCycle() {
            const monthKey = getCurrentMonthKey();
            const cycle = monthlyCycles[monthKey];
            
            if (cycle) {
                document.getElementById('cycleStartDate').value = cycle.startDate;
                document.getElementById('cycleEndDate').value = cycle.endDate;
                updateCyclePeriodDisplay();
            }
        }

        function autoSetMonthlyCycle() {
            const monthKey = getCurrentMonthKey();
            const year = currentDate.getFullYear();
            const month = currentDate.getMonth() + 1;
            
            const startDate = `${year}-${String(month).padStart(2, '0')}-01`;
            const lastDay = new Date(year, month, 0).getDate();
            const endDate = `${year}-${String(month).padStart(2, '0')}-${String(lastDay).padStart(2, '0')}`;
            
            document.getElementById('cycleStartDate').value = startDate;
            document.getElementById('cycleEndDate').value = endDate;
            saveMonthlyCycle();
        }

        function saveMonthlyCycle() {
            const monthKey = getCurrentMonthKey();
            const startDate = document.getElementById('cycleStartDate').value;
            const endDate = document.getElementById('cycleEndDate').value;
            
            if (startDate && endDate) {
                monthlyCycles[monthKey] = {
                    startDate: startDate,
                    endDate: endDate,
                    savedAt: new Date().toISOString()
                };
                localStorage.setItem('hr_cycles', JSON.stringify(monthlyCycles));
                updateCyclePeriodDisplay();
                updateStats();
            }
        }

        function updateCyclePeriodDisplay() {
            const startDate = document.getElementById('cycleStartDate').value;
            const endDate = document.getElementById('cycleEndDate').value;
            const display = document.getElementById('cyclePeriodDisplay');
            
            if (startDate && endDate) {
                const start = new Date(startDate);
                const end = new Date(endDate);
                const days = Math.ceil((end - start) / (1000 * 60 * 60 * 24)) + 1;
                display.innerHTML = `${startDate} ～ ${endDate}<br><span style="color: var(--text-muted); font-size: 13px;">(共 ${days} 天)</span>`;
            } else {
                display.textContent = '請設定考勤週期';
            }
        }

        function useCurrentMonth() {
            const year = currentDate.getFullYear();
            const month = currentDate.getMonth() + 1;
            const firstDay = `${year}-${String(month).padStart(2, '0')}-01`;
            const lastDay = new Date(year, month, 0);
            const endDay = `${year}-${String(month).padStart(2, '0')}-${String(lastDay.getDate()).padStart(2, '0')}`;
            
            document.getElementById('cycleStartDate').value = firstDay;
            document.getElementById('cycleEndDate').value = endDay;
            saveMonthlyCycle();
        }

        function use16thCycle() {
            const year = currentDate.getFullYear();
            const month = currentDate.getMonth() + 1;
            const prevMonth = month === 1 ? 12 : month - 1;
            const prevYear = month === 1 ? year - 1 : year;
            
            const startDate = `${prevYear}-${String(prevMonth).padStart(2, '0')}-16`;
            const endDate = `${year}-${String(month).padStart(2, '0')}-15`;
            
            document.getElementById('cycleStartDate').value = startDate;
            document.getElementById('cycleEndDate').value = endDate;
            saveMonthlyCycle();
        }

        function copyPreviousCycle() {
            const year = currentDate.getFullYear();
            const month = currentDate.getMonth() + 1;
            const prevMonth = month === 1 ? 12 : month - 1;
            const prevYear = month === 1 ? year - 1 : year;
            const prevMonthKey = `${prevYear}-${String(prevMonth).padStart(2, '0')}`;
            
            if (monthlyCycles[prevMonthKey]) {
                const prevCycle = monthlyCycles[prevMonthKey];
                const prevStart = new Date(prevCycle.startDate);
                const prevEnd = new Date(prevCycle.endDate);
                
                const startDay = prevStart.getDate();
                const endDay = prevEnd.getDate();
                
                const thisMonthStart = new Date(year, month - 1, startDay);
                const nextMonth = month === 12 ? 1 : month + 1;
                const nextYear = month === 12 ? year + 1 : year;
                const thisMonthEnd = new Date(nextYear, nextMonth - 1, endDay);
                
                document.getElementById('cycleStartDate').value = formatDateForInput(thisMonthStart);
                document.getElementById('cycleEndDate').value = formatDateForInput(thisMonthEnd);
                saveMonthlyCycle();
            } else {
                alert('上個月尚未設定考勤週期');
            }
        }

        function exportData() {
            const data = {
                overtimeData, leaveData, monthlyCycles, nationalHolidays,
                makeupWorkDays, customHolidays, annualLeaveSettings,
                settings: {
                    monthlySalary: document.getElementById('monthlySalary').value,
                    targetPay: document.getElementById('targetPay').value
                },
                exportDate: new Date().toISOString(),
                version: 'hr-2.0'
            };
            
            const blob = new Blob([JSON.stringify(data, null, 2)], { type: 'application/json' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `人資系統備份_${getCurrentMonthKey()}.json`;
            a.click();
            URL.revokeObjectURL(url);
        }

        function importData(input) {
            const file = input.files[0];
            if (!file) return;
            
            const reader = new FileReader();
            reader.onload = function(e) {
                try {
                    const data = JSON.parse(e.target.result);
                    
                    if (confirm('確定要匯入資料嗎？這將覆蓋現有記錄！')) {
                        overtimeData = data.overtimeData || {};
                        leaveData = data.leaveData || {};
                        monthlyCycles = data.monthlyCycles || {};
                        nationalHolidays = data.nationalHolidays || {};
                        makeupWorkDays = data.makeupWorkDays || {};
                        customHolidays = data.customHolidays || {};
                        annualLeaveSettings = data.annualLeaveSettings || {};
                        
                        if (data.settings) {
                            if (data.settings.monthlySalary) {
                                document.getElementById('monthlySalary').value = data.settings.monthlySalary;
                                localStorage.setItem('monthlySalary', data.settings.monthlySalary);
                            }
                            if (data.settings.targetPay) {
                                document.getElementById('targetPay').value = data.settings.targetPay;
                                localStorage.setItem('targetPay', data.settings.targetPay);
                            }
                        }
                        
                        saveData();
                        localStorage.setItem('hr_cycles', JSON.stringify(monthlyCycles));
                        
                        renderCalendar();
                        updateStats();
                        calculateHourlyRate();
                        calculateTargetHours();
                        loadMonthlyCycle();
                        updateAnnualLeaveDisplay();
                        
                        alert('資料匯入成功！');
                    }
                } catch (error) {
                    alert('匯入失敗：檔案格式不正確');
                    console.error(error);
                }
            };
            reader.readAsText(file);
            input.value = '';
        }

        function formatDateStr(date) {
            const year = date.getFullYear();
            const month = String(date.getMonth() + 1).padStart(2, '0');
            const day = String(date.getDate()).padStart(2, '0');
            return `${year}-${month}-${day}`;
        }

        function formatDateForInput(date) {
            return formatDateStr(date);
        }

        init();
    </script>
</body>
</html>
