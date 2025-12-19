<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>iNCCU 行動校務系統 - 全裝置通用版</title>
    <style>
        :root {
            --nccu-blue: #1B315E;
            --nccu-gold: #C69C6D;
            --bg-color: #F5F7FA;
            --card-bg: #FFFFFF;
            --text-main: #333333;
            --text-light: #666666;
            --shadow: 0 4px 12px rgba(0,0,0,0.06);
            --radius: 16px;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, "Noto Sans TC", sans-serif;
            -webkit-tap-highlight-color: transparent; /* 移除點擊時的藍色高光 */
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-main);
            padding-bottom: 60px; /* 底部留白 */
        }

        /* --------------------------------------
           Header 區域 (響應式調整)
           -------------------------------------- */
        header {
            background-color: var(--nccu-blue);
            color: white;
            padding: 1rem 1.5rem;
            position: sticky;
            top: 0;
            z-index: 100;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }

        .header-content {
            max-width: 1400px;
            margin: 0 auto;
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap; /* 允許手機版換行 */
            gap: 10px;
        }

        .brand {
            font-size: 1.3rem;
            font-weight: bold;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .user-profile {
            display: flex;
            align-items: center;
            gap: 12px;
            text-align: right;
        }

        .user-info {
            font-size: 0.9rem;
        }

        .user-subtext {
            font-size: 0.75rem;
            opacity: 0.8;
            display: block;
        }

        .btn-logout {
            background: rgba(255,255,255,0.15);
            border: 1px solid rgba(255,255,255,0.2);
            color: white;
            padding: 6px 14px;
            border-radius: 20px;
            cursor: pointer;
            font-size: 0.85rem;
        }

        /* --------------------------------------
           Grid 佈局系統 (核心響應式邏輯)
           -------------------------------------- */
        .container {
            display: grid;
            gap: 20px;
            padding: 20px;
            max-width: 1400px;
            margin: 0 auto;
            
            /* 預設：手機版 (單欄) */
            grid-template-columns: 1fr;
        }

        /* 平板直向 (Tablet Portrait): 雙欄 */
        @media (min-width: 768px) {
            .container {
                grid-template-columns: repeat(2, 1fr);
            }
        }

        /* 電腦/平板橫向 (Desktop/Landscape): 三欄 */
        @media (min-width: 1024px) {
            .container {
                grid-template-columns: repeat(3, 1fr);
            }
        }

        /* --------------------------------------
           卡片組件 (Card UI)
           -------------------------------------- */
        .card {
            background: var(--card-bg);
            border-radius: var(--radius);
            padding: 20px;
            box-shadow: var(--shadow);
            height: 100%; /* 讓並排的卡片等高 */
            display: flex;
            flex-direction: column;
            border: 1px solid rgba(0,0,0,0.02);
        }

        .card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
            padding-bottom: 10px;
            border-bottom: 1px solid #f0f0f0;
        }

        .card-title {
            font-size: 1.1rem;
            font-weight: 700;
            color: var(--nccu-blue);
            display: flex;
            align-items: center;
            gap: 6px;
        }

        .card-link {
            color: #999;
            text-decoration: none;
            font-size: 0.85rem;
        }

        /* --------------------------------------
           APP icon 網格
           -------------------------------------- */
        .app-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr); /* 手機預設4個一排 */
            gap: 10px;
            text-align: center;
        }

        /* 在超小手機上改為3個一排，避免擁擠 */
        @media (max-width: 360px) {
            .app-grid { grid-template-columns: repeat(3, 1fr); }
        }

        .app-icon {
            text-decoration: none;
            color: var(--text-main);
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 5px;
            border-radius: 8px;
            transition: background 0.2s;
        }

        .app-icon:active { background-color: #f5f5f5; }

        .icon-box {
            width: 50px;
            height: 50px;
            background: #EBF2FA;
            border-radius: 14px;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 1.5rem;
            margin-bottom: 6px;
            color: var(--nccu-blue);
        }

        .app-name { 
            font-size: 0.8rem; 
            line-height: 1.25;
            height: 2.5em; /* 限制兩行高度 */
            overflow: hidden;
        }

        /* --------------------------------------
           通知列表與新聞
           -------------------------------------- */
        .list-container {
            flex: 1;
            overflow-y: auto;
        }

        .notif-item {
            background: #FFFBF5;
            border-left: 4px solid var(--nccu-gold);
            padding: 10px 14px;
            border-radius: 6px;
            margin-bottom: 10px;
            font-size: 0.9rem;
            line-height: 1.5;
        }
        
        .notif-date {
            font-size: 0.75rem;
            color: #888;
            display: block;
            margin-bottom: 2px;
        }

        .news-item {
            padding: 12px 0;
            border-bottom: 1px solid #f0f0f0;
            font-size: 0.95rem;
            line-height: 1.5;
            display: flex;
            align-items: flex-start;
            gap: 8px;
        }
        .news-item::before {
            content: "•";
            color: var(--nccu-blue);
            font-weight: bold;
        }

        /* --------------------------------------
           行事曆表格
           -------------------------------------- */
        .calendar-wrapper {
            overflow-x: auto; /* 手機版表格若太寬可滑動 */
        }

        .calendar-table {
            width: 100%;
            border-collapse: collapse;
            min-width: 250px; /* 最小寬度防止壓縮 */
        }

        .calendar-table td {
            padding: 10px 5px;
            border-bottom: 1px solid #eee;
            font-size: 0.9rem;
        }

        .date-badge {
            background: #EBF2FA;
            color: var(--nccu-blue);
            padding: 3px 6px;
            border-radius: 4px;
            font-weight: 600;
            font-size: 0.8rem;
            white-space: nowrap;
        }

        /* --------------------------------------
           搜尋區域 (手機優化)
           -------------------------------------- */
        .search-area {
            display: flex;
            gap: 8px;
            margin-bottom: 12px;
            flex-wrap: wrap; /* 手機版換行 */
        }
        
        input, select {
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 8px;
            background: white;
            font-size: 0.95rem;
            flex: 1; /* 自動填滿空間 */
            min-width: 120px; /* 最小寬度 */
        }
        
        .btn-primary {
            background: var(--nccu-blue);
            color: white;
            border: none;
            padding: 12px;
            border-radius: 10px;
            font-weight: bold;
            text-align: center;
            cursor: pointer;
            width: 100%;
            font-size: 1rem;
            transition: background 0.2s;
        }
        
        .btn-primary:active { background: #142446; }

        /* 手機版特別調整 Header */
        @media (max-width: 480px) {
            .header-content {
                flex-direction: row; /* 保持橫向 */
            }
            .user-info { display: none; } /* 手機隱藏名字，只留按鈕 */
            .user-subtext { display: none; }
        }

    </style>
</head>
<body>

<header>
    <div class="header-content">
        <div class="brand">
            🏫 iNCCU 愛政大
        </div>
        <div class="user-profile">
            <div>
                <div class="user-info">蕭家浩</div>
                <span class="user-subtext">早安！</span>
            </div>
            <button class="btn-logout">登出</button>
        </div>
    </div>
</header>

<main class="container">

    <div class="card">
        <div class="card-header">
            <div class="card-title">⭐ 常用系統</div>
            <a href="#" class="card-link">編輯</a>
        </div>
        
        <div class="app-grid">
            <a href="#" class="app-icon"><div class="icon-box">📊</div><div class="app-name">成績查詢</div></a>
            <a href="#" class="app-icon"><div class="icon-box">📅</div><div class="app-name">重要會議</div></a>
            <a href="#" class="app-icon"><div class="icon-box">📦</div><div class="app-name">包裹查詢</div></a>
            <a href="#" class="app-icon"><div class="icon-box">📖</div><div class="app-name">全校課程</div></a>
            <a href="#" class="app-icon"><div class="icon-box">📶</div><div class="app-name">eduroam</div></a>
            <a href="#" class="app-icon"><div class="icon-box">🎓</div><div class="app-name">Moodle</div></a>
            <a href="#" class="app-icon"><div class="icon-box">📧</div><div class="app-name">郵件</div></a>
            <a href="#" class="app-icon"><div class="icon-box">➕</div><div class="app-name">更多</div></a>
        </div>

        <div class="card-header" style="margin-top: 25px;">
            <div class="card-title">📱 資訊系統</div>
        </div>
        <div class="app-grid">
            <a href="#" class="app-icon"><div class="icon-box">📚</div><div class="app-name">圖書館</div></a>
            <a href="#" class="app-icon"><div class="icon-box">🖥️</div><div class="app-name">校務Web</div></a>
            <a href="#" class="app-icon"><div class="icon-box">💾</div><div class="app-name">軟體授權</div></a>
            <a href="#" class="app-icon"><div class="icon-box">🔒</div><div class="app-name">VPN</div></a>
        </div>
    </div>

    <div class="card">
        <div class="card-header">
            <div class="card-title">🔔 個人訊息 (6)</div>
            <a href="#" class="card-link">全部</a>
        </div>
        <div class="list-container">
            <div class="notif-item">
                <span class="notif-date">114/12/16</span>
                提醒您參加「Google Gemini Enterprise 教育訓練課程」。
            </div>
            <div class="notif-item">
                <span class="notif-date">114/12/10</span>
                提醒您參加「【商學院講座】青年×金融未來」。
            </div>
            <div class="notif-item">
                <span class="notif-date">114/11/25</span>
                提醒您參加「《陌生人與他們的小孩》電影放映」。
            </div>
        </div>

        <div class="card-header" style="margin-top: 20px;">
            <div class="card-title">🗓️ 12月行事曆</div>
        </div>
        <div class="calendar-wrapper">
            <table class="calendar-table">
                <tr><td><span class="date-badge">12/01</span></td><td>第2次教務會議</td></tr>
                <tr><td><span class="date-badge">12/07</span></td><td>校園馬拉松 (交管)</td></tr>
                <tr><td><span class="date-badge">12/12</span></td><td style="color:#E74C3C">休學申請截止日</td></tr>
                <tr><td><span class="date-badge">12/25</span></td><td>行憲紀念日</td></tr>
            </table>
        </div>
    </div>

    <div class="card">
        <div class="card-header">
            <div class="card-title">📰 校園新聞</div>
            <div style="display:flex; gap:10px;">
                <span style="font-size:0.85rem; color:var(--nccu-blue); font-weight:bold;">新聞</span>
                <span style="font-size:0.85rem; color:#ccc;">公告</span>
            </div>
        </div>
        <div class="list-container" style="max-height: 300px;">
            <div class="news-item">政大出版社多本專書獲肯定 展現人社研究厚實能量</div>
            <div class="news-item">全創碩深化媒體素養：澳洲學者談新聞變局</div>
            <div class="news-item">「金英講座」成果發表會 培育下一代金融菁英</div>
            <div class="news-item">國關論壇：談臺灣對拉美的援助與挑戰</div>
            <div class="news-item">謝發達大使暢談如何與新加坡按部就班成功協商</div>
        </div>

        <div class="card-header" style="margin-top: 20px;">
            <div class="card-title">🔍 館藏查詢</div>
        </div>
        <div class="search-area">
            <input type="text" placeholder="輸入書名關鍵字...">
        </div>
        <div class="search-area">
            <select><option>不限類型</option><option>圖書</option><option>期刊</option></select>
            <select><option>總圖書館</option><option>商圖</option><option>傳圖</option></select>
        </div>
        <button class="btn-primary">搜尋</button>
    </div>

</main>

</body>
</html>
