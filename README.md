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
            --alert-red: #E74C3C;
            --shadow: 0 4px 6px rgba(0,0,0,0.05);
            --radius: 16px;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: "Noto Sans TC", "PingFang TC", "Microsoft JhengHei", sans-serif;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-main);
            padding-bottom: 80px; /* 預留底部空間 */
        }

        /* Header Area */
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
            font-size: 1.5rem;
            font-weight: bold;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .user-profile {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .user-name {
            font-weight: 500;
        }

        .btn-logout {
            background: rgba(255,255,255,0.2);
            border: none;
            color: white;
            padding: 8px 16px;
            border-radius: 20px;
            cursor: pointer;
            font-size: 0.9rem;
        }

        /* Grid Layout */
        .container {
            display: grid;
            grid-template-columns: repeat(12, 1fr);
            gap: 20px;
            padding: 20px;
            max-width: 1400px;
            margin: 0 auto;
        }

        /* Responsive Grid for Tablet */
        .col-4 { grid-column: span 4; }
        .col-6 { grid-column: span 6; }
        .col-8 { grid-column: span 8; }
        .col-12 { grid-column: span 12; }

        @media (max-width: 1024px) {
            .col-4 { grid-column: span 6; }
            .col-8 { grid-column: span 12; }
        }
        @media (max-width: 768px) {
            .col-4, .col-6, .col-8 { grid-column: span 12; }
        }

        /* Card Component */
        .card {
            background: var(--card-bg);
            border-radius: var(--radius);
            padding: 20px;
            box-shadow: var(--shadow);
            height: 100%;
            display: flex;
            flex-direction: column;
        }

        .card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
            border-bottom: 1px solid #eee;
            padding-bottom: 10px;
        }

        .card-title {
            font-size: 1.1rem;
            font-weight: bold;
            color: var(--nccu-blue);
            display: flex;
            align-items: center;
            gap: 8px;
        }

        /* System Grid (Apps) */
        .app-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(80px, 1fr));
            gap: 15px;
            text-align: center;
        }

        .app-icon {
            display: flex;
            flex-direction: column;
            align-items: center;
            text-decoration: none;
            color: var(--text-main);
            transition: transform 0.2s;
        }

        .app-icon:active { transform: scale(0.95); }

        .icon-box {
            width: 50px;
            height: 50px;
            background: #EBF2FA;
            border-radius: 12px;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 1.5rem;
            margin-bottom: 8px;
            color: var(--nccu-blue);
        }

        .app-name { font-size: 0.85rem; line-height: 1.2; }

        /* News & Announcements List */
        .news-tabs {
            display: flex;
            gap: 10px;
            margin-bottom: 15px;
        }
        .tab-btn {
            padding: 8px 16px;
            border-radius: 20px;
            border: 1px solid var(--nccu-blue);
            background: none;
            color: var(--nccu-blue);
            cursor: pointer;
        }
        .tab-btn.active {
            background: var(--nccu-blue);
            color: white;
        }
        .news-list {
            list-style: none;
            overflow-y: auto;
            max-height: 250px;
        }
        .news-item {
            padding: 10px 0;
            border-bottom: 1px solid #f0f0f0;
            font-size: 0.95rem;
            display: flex;
            gap: 10px;
        }
        .news-item::before {
            content: "•";
            color: var(--nccu-gold);
            font-weight: bold;
        }

        /* Notifications */
        .notif-list {
            display: flex;
            flex-direction: column;
            gap: 10px;
            max-height: 300px;
            overflow-y: auto;
        }
        .notif-item {
            background: #FFF9F0;
            border-left: 4px solid var(--nccu-gold);
            padding: 12px;
            border-radius: 4px;
            font-size: 0.9rem;
        }
        .notif-date {
            font-size: 0.8rem;
            color: #999;
            margin-bottom: 4px;
            display: block;
        }

        /* Library Search */
        .search-group {
            display: flex;
            gap: 10px;
            margin-bottom: 10px;
            flex-wrap: wrap;
        }
        .search-input {
            flex: 1;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 8px;
            min-width: 200px;
        }
        .search-select {
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 8px;
            background: white;
        }
        .btn-search {
            background: var(--nccu-blue);
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 8px;
            width: 100%;
            margin-top: 10px;
            font-weight: bold;
        }

        /* Calendar Table */
        .calendar-table {
            width: 100%;
            border-collapse: collapse;
            font-size: 0.9rem;
        }
        .calendar-table th {
            text-align: left;
            color: #999;
            padding: 5px;
            font-size: 0.8rem;
        }
        .calendar-table td {
            padding: 8px 5px;
            border-bottom: 1px solid #f0f0f0;
        }
        .date-badge {
            display: inline-block;
            background: #EBF2FA;
            color: var(--nccu-blue);
            padding: 2px 6px;
            border-radius: 4px;
            font-weight: bold;
            font-size: 0.8rem;
            margin-right: 8px;
        }
        
        /* Email & Portfolio Buttons */
        .action-card {
            display: flex;
            gap: 10px;
            margin-top: auto;
        }
        .action-btn {
            flex: 1;
            padding: 15px;
            border-radius: 12px;
            border: none;
            font-weight: bold;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }
        .btn-mail { background: #EA4335; color: white; }
        .btn-portfolio { background: #34A853; color: white; }

        /* Footer */
        .footer-info {
            grid-column: span 12;
            text-align: center;
            font-size: 0.8rem;
            color: #999;
            margin-top: 20px;
            padding-top: 20px;
            border-top: 1px solid #ddd;
        }

    </style>
</head>
<body>

<header>
    <div class="brand">
        <span>🏫</span> iNCCU 愛政大
    </div>
    <div class="user-profile">
        <div>
            <div class="user-name">蕭家浩 (HSIAO CHIA HAO)</div>
            <div style="font-size: 0.8rem; opacity: 0.8;">早安，今天也要加油！</div>
        </div>
        <button class="btn-logout">登出</button>
    </div>
</header>

<main class="container">

    <div class="col-4">
        <div class="card" style="margin-bottom: 20px;">
            <div class="card-header">
                <div class="card-title">⭐ 我的常用系統</div>
                <small>編輯</small>
            </div>
            <div class="app-grid">
                <a href="#" class="app-icon"><div class="icon-box">📊</div><div class="app-name">成績查詢</div></a>
                <a href="#" class="app-icon"><div class="icon-box">📅</div><div class="app-name">重要會議</div></a>
                <a href="#" class="app-icon"><div class="icon-box">📦</div><div class="app-name">包裹查詢</div></a>
                <a href="#" class="app-icon"><div class="icon-box">📖</div><div class="app-name">全校課程</div></a>
                <a href="#" class="app-icon"><div class="icon-box">📶</div><div class="app-name">eduroam</div></a>
                <a href="#" class="app-icon"><div class="icon-box">➕</div><div class="app-name">更多</div></a>
            </div>
        </div>

        <div class="card">
            <div class="card-header">
                <div class="card-title">📱 校園資訊系統</div>
            </div>
            <div class="app-grid">
                <a href="#" class="app-icon"><div class="icon-box">📚</div><div class="app-name">圖書館</div></a>
                <a href="#" class="app-icon"><div class="icon-box">🖥️</div><div class="app-name">校務Web</div></a>
                <a href="#" class="app-icon"><div class="icon-box">💾</div><div class="app-name">軟體授權</div></a>
                <a href="#" class="app-icon"><div class="icon-box">🔒</div><div class="app-name">VPN</div></a>
                <a href="#" class="app-icon"><div class="icon-box">🛠️</div><div class="app-name">IT Service</div></a>
                <a href="#" class="app-icon"><div class="icon-box">🎓</div><div class="app-name">Moodle</div></a>
                <a href="#" class="app-icon"><div class="icon-box">📝</div><div class="app-name">問卷</div></a>
                <a href="#" class="app-icon"><div class="icon-box">🆘</div><div class="app-name">線上服務</div></a>
            </div>
        </div>
    </div>

    <div class="col-4">
        <div class="card" style="margin-bottom: 20px; flex: 1;">
            <div class="card-header">
                <div class="card-title">🔔 個人訊息 (6則未讀)</div>
                <small>查看全部</small>
            </div>
            <div class="notif-list">
                <div class="notif-item">
                    <span class="notif-date">114/12/16</span>
                    提醒您參加「Google Gemini Enterprise 教育訓練課程」
                </div>
                <div class="notif-item">
                    <span class="notif-date">114/12/10</span>
                    提醒您參加「【商學院講座】青年×金融未來」
                </div>
                <div class="notif-item">
                    <span class="notif-date">114/11/25</span>
                    提醒您參加「《陌生人與他們的小孩》電影放映」
                </div>
                <div class="notif-item">
                    <span class="notif-date">114/10/07</span>
                    提醒您參加「人人亞博：舊金山亞洲藝術博物館」
                </div>
            </div>
            
            <div class="action-card" style="margin-top: 15px;">
                <button class="action-btn btn-mail">
                    📧 NCCU 郵件
                </button>
                <button class="action-btn btn-portfolio">
                    🌱 我的全人
                </button>
            </div>
        </div>

        <div class="card" style="flex: 1;">
            <div class="card-header">
                <div class="card-title">🗓️ 2025年12月 行事曆</div>
            </div>
            <table class="calendar-table">
                <thead><tr><th>日期</th><th>事項</th></tr></thead>
                <tbody>
                    <tr>
                        <td><span class="date-badge">1 (一)</span></td>
                        <td>第2次教務會議</td>
                    </tr>
                    <tr>
                        <td><span class="date-badge">1~30</span></td>
                        <td>碩士班轉系所申請</td>
                    </tr>
                    <tr>
                        <td><span class="date-badge">7 (日)</span></td>
                        <td>校園馬拉松 (交管 6:30-9:30)</td>
                    </tr>
                    <tr>
                        <td><span class="date-badge">8~12</span></td>
                        <td>學雜費減免預辦</td>
                    </tr>
                    <tr>
                        <td><span class="date-badge">12 (五)</span></td>
                        <td><span style="color:red">休學、學位考試截止</span></td>
                    </tr>
                     <tr>
                        <td><span class="date-badge">25 (四)</span></td>
                        <td>行憲紀念日</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>

    <div class="col-4">
        <div class="card" style="margin-bottom: 20px;">
            <div class="card-header">
                <div class="card-title">🔍 圖書館館藏查詢</div>
            </div>
            <div class="search-group">
                <input type="text" class="search-input" placeholder="輸入關鍵字...">
                <select class="search-select">
                    <option>不限類型</option>
                    <option>圖書</option>
                    <option>期刊</option>
                </select>
            </div>
            <div class="search-group">
                <select class="search-select" style="width: 100%">
                    <option>所有館藏地</option>
                    <option>總圖</option>
                    <option>商圖</option>
                </select>
            </div>
            <button class="btn-search">搜尋</button>
        </div>

        <div class="card" style="height: auto;">
            <div class="news-tabs">
                <button class="tab-btn active">校園新聞</button>
                <button class="tab-btn">校園公告</button>
            </div>
            
            <ul class="news-list">
                <li class="news-item">政大出版社多本專書獲肯定 展現人社研究厚實能量</li>
                <li class="news-item">全創碩深化媒體素養：澳洲學者談新聞變局</li>
                <li class="news-item">「金英講座」成果發表會 培育下一代金融菁英</li>
                <li class="news-item">謝發達大使暢談如何與新加坡成功協商</li>
                <li class="news-item">國關論壇：談臺灣對拉美的援助與挑戰</li>
                
                <li class="news-item" style="color: #666; font-size: 0.9em; margin-top: 10px; border-top: 2px dashed #eee; padding-top: 10px;">
                    <strong>[公告]</strong> 指南派出所旁機車停車場封閉
                </li>
                <li class="news-item" style="color: #666; font-size: 0.9em;">
                    <strong>[公告]</strong> 台聯大校際專車 12/20 起停駛
                </li>
                <li class="news-item" style="color: #666; font-size: 0.9em;">
                    <strong>[徵才]</strong> 哲學系徵聘專任約聘教師
                </li>
            </ul>
        </div>
    </div>

    <div class="footer-info">
        校址：11605 台北市文山區指南路二段64號 | 總機：02-29393091 | 緊急聯絡：校內分機 66119
    </div>

</main>

</body>
</html>
