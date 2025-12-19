<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>iNCCU 行動校務系統 - 平板優化版</title>
    <style>
        :root {
            --nccu-blue: #1B315E;
            --nccu-gold: #C69C6D;
            --bg-color: #F5F7FA;
            --card-bg: #FFFFFF;
            --text-main: #333333;
            --text-light: #666666;
            --shadow: 0 4px 12px rgba(0,0,0,0.08);
            --radius: 16px;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, "Noto Sans TC", sans-serif;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-main);
            padding-bottom: 40px;
        }

        /* 頂部導航列 */
        header {
            background-color: var(--nccu-blue);
            color: white;
            padding: 1rem 2rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
            position: sticky;
            top: 0;
            z-index: 100;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }

        .brand {
            font-size: 1.4rem;
            font-weight: bold;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .user-profile {
            display: flex;
            align-items: center;
            gap: 15px;
            text-align: right;
        }

        .btn-logout {
            background: rgba(255,255,255,0.2);
            border: 1px solid rgba(255,255,255,0.3);
            color: white;
            padding: 8px 20px;
            border-radius: 20px;
            cursor: pointer;
            font-size: 0.9rem;
            white-space: nowrap; /* 防止按鈕文字換行 */
        }

        /* 關鍵修復：使用 Auto-Fit + Minmax 
           這會確保每個欄位至少有 350px 寬，空間不夠會自動換行，
           絕對不會發生文字擠成直排的情況。
        */
        .container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(340px, 1fr)); 
            gap: 24px;
            padding: 24px;
            max-width: 1400px;
            margin: 0 auto;
        }

        /* 卡片樣式 */
        .card {
            background: var(--card-bg);
            border-radius: var(--radius);
            padding: 24px;
            box-shadow: var(--shadow);
            height: 100%; /* 讓同一列卡片等高 */
            display: flex;
            flex-direction: column;
            border: 1px solid rgba(0,0,0,0.02);
        }

        .card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 12px;
            border-bottom: 1px solid #f0f0f0;
        }

        .card-title {
            font-size: 1.2rem;
            font-weight: bold;
            color: var(--nccu-blue);
            white-space: nowrap; /* 防止標題換行 */
        }

        /* APP 圖示網格 */
        .app-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr); /* 強制每行4個 */
            gap: 12px;
            text-align: center;
        }

        .app-icon {
            text-decoration: none;
            color: var(--text-main);
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .icon-box {
            width: 56px;
            height: 56px;
            background: #EBF2FA;
            border-radius: 14px;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 1.6rem;
            margin-bottom: 8px;
            transition: transform 0.1s;
        }
        
        .app-icon:active .icon-box { transform: scale(0.95); }

        .app-name { 
            font-size: 0.85rem; 
            line-height: 1.3;
            height: 2.6em; /* 固定高度防止對齊跑掉 */
            overflow: hidden;
        }

        /* 列表與通知 */
        .list-container {
            flex: 1;
            overflow-y: auto;
        }

        .notif-item {
            background: #FFFBF5;
            border-left: 4px solid var(--nccu-gold);
            padding: 12px 16px;
            border-radius: 6px;
            margin-bottom: 10px;
            font-size: 0.95rem;
            line-height: 1.5;
        }
        
        .notif-date {
            font-size: 0.8rem;
            color: #888;
            display: block;
            margin-bottom: 4px;
        }

        /* 行事曆表格 */
        .calendar-table {
            width: 100%;
            border-collapse: collapse;
        }
        .calendar-table td {
            padding: 12px 8px;
            border-bottom: 1px solid #eee;
            font-size: 0.95rem;
        }
        .date-badge {
            background: #EBF2FA;
            color: var(--nccu-blue);
            padding: 4px 8px;
            border-radius: 6px;
            font-weight: 600;
            font-size: 0.85rem;
            margin-right: 8px;
            white-space: nowrap;
        }

        /* 搜尋與按鈕 */
        .search-area {
            display: flex;
            gap: 10px;
            margin-bottom: 15px;
        }
        
        input, select {
            padding: 12px;
            border: 1px solid #ddd;
            border-radius: 8px;
            background: white;
            font-size: 1rem;
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
        }

        .news-item {
            padding: 12px 0;
            border-bottom: 1px solid #f0f0f0;
            line-height: 1.5;
        }

        /* 平板橫向優化 */
        @media (min-width: 1024px) {
           /* 當螢幕夠寬時，可以微調佈局 */
        }
    </style>
</head>
<body>

<header>
    <div class="brand">
        🏫 iNCCU 愛政大
    </div>
    <div class="user-profile">
        <div>
            <div style="font-weight:bold;">蕭家浩 (HSIAO CHIA HAO)</div>
            <div style="font-size: 0.8rem; opacity: 0.8;">早安，今天也要加油！</div>
        </div>
        <button class="btn-logout">登出</button>
    </div>
</header>

<main class="container">

    <div class="card">
        <div class="card-header">
            <div class="card-title">⭐ 我的常用系統</div>
            <a href="#" style="color: #999; text-decoration: none; font-size:0.9rem;">編輯</a>
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

        <div class="card-header" style="margin-top: 30px;">
            <div class="card-title">📱 校園資訊系統</div>
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
            <a href="#" style="color: #999; text-decoration: none; font-size:0.9rem;">全部</a>
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
        <table class="calendar-table">
            <tr><td><span class="date-badge">12/01</span></td><td>第2次教務會議</td></tr>
            <tr><td><span class="date-badge">12/07</span></td><td>校園馬拉松 (交管)</td></tr>
            <tr><td><span class="date-badge">12/12</span></td><td style="color:#E74C3C">休學申請截止日</td></tr>
            <tr><td><span class="date-badge">12/25</span></td><td>行憲紀念日</td></tr>
        </table>
    </div>

    <div class="card">
        <div class="card-header">
            <div class="card-title">📰 校園新聞</div>
            <div style="display:flex; gap:10px;">
                <span style="color:var(--nccu-blue); font-weight:bold;">新聞</span>
                <span style="color:#ccc;">公告</span>
            </div>
        </div>
        <div class="list-container" style="max-height: 250px;">
            <div class="news-item">政大出版社多本專書獲肯定 展現人社研究厚實能量</div>
            <div class="news-item">全創碩深化媒體素養：澳洲學者談新聞變局</div>
            <div class="news-item">「金英講座」成果發表會 培育下一代金融菁英</div>
            <div class="news-item">國關論壇：談臺灣對拉美的援助與挑戰</div>
        </div>

        <div class="card-header" style="margin-top: 20px;">
            <div class="card-title">🔍 館藏查詢</div>
        </div>
        <div class="search-area">
            <input type="text" placeholder="輸入書名關鍵字..." style="flex:1;">
        </div>
        <div class="search-area">
            <select style="flex:1"><option>不限類型</option><option>圖書</option></select>
            <select style="flex:1"><option>總圖書館</option><option>商圖</option></select>
        </div>
        <button class="btn-primary">搜尋</button>
    </div>

</main>

<div style="text-align: center; color: #999; font-size: 0.8rem; padding: 20px;">
    © National Chengchi University
</div>

</body>
</html>
