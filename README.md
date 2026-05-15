[index.html](https://github.com/user-attachments/files/27798699/index.html)
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>МедиаЦентр Temp | Матрёшка РП + Email + Личный кабинет</title>
    <!-- Font Awesome -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', 'Inter', system-ui, sans-serif;
            transition: background 0.2s ease, color 0.2s ease, border-color 0.2s;
        }

        body.light-theme {
            background: #f4f1fc;
            color: #1e1a2f;
        }
        body.light-theme .auth-card,
        body.light-theme .card,
        body.light-theme .activity-area,
        body.light-theme .action-bar,
        body.light-theme .report-section,
        body.light-theme .user-badge,
        body.light-theme .online-users-area,
        body.light-theme .registered-users-area,
        body.light-theme .profile-modal .modal-content {
            background: #ffffff;
            border-color: #ddd2f0;
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.05);
        }
        body.light-theme .card-header {
            background: #f7f2ff;
            border-bottom-color: #e5d9f5;
            color: #31286e;
        }
        body.light-theme .input-field input,
        body.light-theme .input-field textarea {
            background: #fefcff;
            border-color: #d6c8f0;
            color: #1e1a2f;
        }
        body.light-theme .report-output {
            background: #fbf9ff;
            color: #1f1b3a;
        }
        body.light-theme .log-item {
            background: #f5efff;
            border-left-color: #8b6bcb;
            color: #322a66;
        }
        body.light-theme .btn {
            background: #ece4ff;
            color: #3a2a6e;
        }
        body.light-theme .logout-btn {
            background: #e4d9ff;
            color: #3a2a6e;
        }
        body.light-theme .start-report-btn {
            background: linear-gradient(125deg, #7c3aed, #b45eff);
            color: white;
        }
        body.light-theme .online-badge, body.light-theme .registered-badge {
            background: #ece3ff;
            color: #3e2c7a;
        }
        body.light-theme .profile-badge {
            background: #e0d6ff;
            color: #2e1f6e;
        }

        body {
            background: #0b0710;
            background-image: radial-gradient(circle at 25% 20%, rgba(106, 13, 173, 0.15) 0%, #03010a 95%);
            color: #f0eef7;
        }

        /* Матрёшка РП */
        .matryoshka-bg {
            position: fixed;
            bottom: 20px;
            left: 20px;
            width: 80px;
            height: 80px;
            opacity: 0.7;
            z-index: 99;
            pointer-events: none;
            transition: 0.3s;
        }
        .matryoshka-bg:hover {
            opacity: 1;
            transform: scale(1.05);
        }

        .theme-toggle {
            position: fixed;
            bottom: 28px;
            right: 28px;
            background: #25203a;
            border-radius: 50px;
            padding: 12px 20px;
            cursor: pointer;
            z-index: 200;
            backdrop-filter: blur(8px);
            font-weight: bold;
            border: 1px solid #9a6eff;
            display: flex;
            gap: 10px;
            box-shadow: 0 5px 14px rgba(0, 0, 0, 0.4);
        }

        .container {
            max-width: 1500px;
            margin: 0 auto;
            padding: 0 12px;
        }

        /* Модальное окно профиля */
        .profile-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.8);
            z-index: 1000;
            justify-content: center;
            align-items: center;
        }
        .profile-modal .modal-content {
            background: #110c1a;
            border-radius: 48px;
            padding: 28px;
            max-width: 450px;
            width: 90%;
            border: 1px solid #8b6bcb;
            position: relative;
        }
        .close-modal {
            position: absolute;
            top: 18px;
            right: 22px;
            font-size: 28px;
            cursor: pointer;
            color: #b77eff;
        }
        .profile-stats {
            margin-top: 20px;
            display: flex;
            flex-direction: column;
            gap: 12px;
        }
        .stat-item {
            background: #1f1730;
            padding: 12px 16px;
            border-radius: 28px;
            display: flex;
            justify-content: space-between;
        }
        .profile-badge {
            background: #2a1d44;
            padding: 6px 14px;
            border-radius: 40px;
            display: inline-block;
            margin-bottom: 12px;
        }

        /* АВТОРИЗАЦИЯ */
        .auth-wrapper {
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 80vh;
        }
        .auth-card {
            background: #110c1a;
            border-radius: 56px;
            padding: 2.2rem 2rem 2.5rem;
            width: 100%;
            max-width: 500px;
            border: 1px solid #3c2a5a;
            box-shadow: 0 25px 40px rgba(0, 0, 0, 0.5);
        }
        .auth-card h2 {
            font-size: 2rem;
            font-weight: 800;
            background: linear-gradient(135deg, #e3cbff, #b77eff);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            text-align: center;
        }
        .input-group {
            margin-bottom: 1.3rem;
            display: flex;
            flex-direction: column;
            gap: 6px;
        }
        .input-group label {
            font-size: 0.8rem;
            font-weight: 700;
            color: #cdb5ff;
        }
        .input-group input {
            background: #08040f;
            border: 1.5px solid #33275a;
            border-radius: 40px;
            padding: 12px 18px;
            font-size: 1rem;
            color: #f0eef7;
            outline: none;
        }
        .input-group input:focus {
            border-color: #aa66ff;
            box-shadow: 0 0 0 3px rgba(170, 102, 255, 0.3);
        }
        .hint-text {
            font-size: 0.7rem;
            color: #ab97cf;
            margin-top: 4px;
        }
        .gen-password-btn, .forgot-password-btn {
            background: #2a1f44;
            border: none;
            border-radius: 60px;
            padding: 8px 18px;
            font-size: 0.8rem;
            font-weight: 600;
            color: #e2d3ff;
            cursor: pointer;
            display: inline-flex;
            align-items: center;
            gap: 8px;
            margin-top: 5px;
        }
        .forgot-password-btn {
            background: #1f1730;
            width: 100%;
            justify-content: center;
        }
        .auth-btn {
            background: linear-gradient(95deg, #7c3aed, #b45eff);
            border: none;
            border-radius: 60px;
            padding: 12px;
            font-weight: bold;
            font-size: 1rem;
            color: white;
            cursor: pointer;
            width: 100%;
            margin-top: 12px;
        }
        .error-msg {
            color: #ffaa9f;
            font-size: 0.75rem;
            margin-bottom: 8px;
        }

        .start-section {
            display: flex;
            justify-content: center;
            margin: 25px 0 20px;
        }
        .start-report-btn {
            background: linear-gradient(125deg, #7c3aed, #b45eff);
            border: none;
            padding: 12px 42px;
            border-radius: 80px;
            font-size: 1.2rem;
            font-weight: 700;
            cursor: pointer;
            display: inline-flex;
            align-items: center;
            gap: 12px;
            box-shadow: 0 6px 14px rgba(0, 0, 0, 0.3);
        }
        .user-bar {
            display: flex;
            justify-content: flex-end;
            align-items: center;
            gap: 18px;
            margin-bottom: 8px;
        }
        .user-badge {
            background: #1a122b;
            padding: 6px 24px;
            border-radius: 40px;
            font-weight: 500;
            cursor: pointer;
        }
        .logout-btn {
            background: #2a1d3f;
            padding: 6px 20px;
            border-radius: 40px;
            cursor: pointer;
        }
        .dashboard {
            display: flex;
            gap: 28px;
            flex-wrap: wrap;
            margin-top: 25px;
        }
        .cards-area {
            flex: 3;
            min-width: 280px;
        }
        .side-area {
            flex: 1.2;
            min-width: 280px;
            display: flex;
            flex-direction: column;
            gap: 20px;
        }
        .info-widget {
            background: #0e0917;
            border-radius: 36px;
            border: 1px solid #3a2d55;
            padding: 18px;
        }
        .widget-title {
            font-weight: 700;
            font-size: 1.1rem;
            margin-bottom: 14px;
            display: flex;
            gap: 8px;
            align-items: center;
            border-bottom: 1px solid #3a2d55;
            padding-bottom: 8px;
        }
        .users-list {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
        }
        .registered-badge, .online-badge {
            background: #1f1730;
            border-radius: 60px;
            padding: 5px 16px;
            font-size: 0.8rem;
            display: inline-flex;
            align-items: center;
            gap: 8px;
            cursor: pointer;
            transition: 0.1s;
        }
        .registered-badge:hover {
            background: #3a2a6e;
            transform: scale(1.02);
        }
        .online-dot {
            width: 9px;
            height: 9px;
            background: #1fdf7a;
            border-radius: 50%;
            display: inline-block;
            box-shadow: 0 0 4px #56ff9e;
        }
        .activity-log {
            display: flex;
            flex-direction: column;
            gap: 14px;
            max-height: 400px;
            overflow-y: auto;
        }
        .log-item {
            background: #08040f;
            border-radius: 24px;
            padding: 12px;
            border-left: 3px solid #b77eff;
        }
        .log-user {
            font-weight: 800;
            font-size: 0.75rem;
            color: #dbbaff;
        }
        .log-action {
            font-size: 0.75rem;
            margin: 5px 0;
            word-break: break-word;
        }
        .log-time {
            font-size: 0.6rem;
            text-align: right;
            opacity: 0.6;
        }

        .cards-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
            gap: 24px;
            margin: 20px 0 30px;
        }
        .card {
            background: #110c1a;
            border-radius: 36px;
            border: 1px solid #352b4b;
            overflow: hidden;
        }
        .card.completed {
            border-color: #b77eff;
            box-shadow: 0 0 0 1px #b77eff55;
        }
        .card-header {
            background: #1f1730;
            padding: 14px 18px;
            font-weight: 700;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .check-icon {
            color: #b45eff;
            font-size: 1.2rem;
            opacity: 0;
        }
        .card.completed .check-icon {
            opacity: 1;
        }
        .card-body {
            padding: 18px;
            display: flex;
            flex-direction: column;
            gap: 16px;
        }
        .input-field {
            display: flex;
            flex-direction: column;
            gap: 6px;
        }
        .input-field label {
            font-size: 0.7rem;
            font-weight: 700;
        }
        .input-field input, .input-field textarea {
            background: #06020c;
            border: 1px solid #332752;
            border-radius: 24px;
            padding: 10px 16px;
            width: 100%;
            color: inherit;
        }
        .action-bar {
            background: #0f0a17;
            border-radius: 80px;
            padding: 12px 22px;
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 18px;
            margin: 10px 0 25px;
        }
        .btn {
            border: none;
            padding: 10px 30px;
            border-radius: 60px;
            font-weight: 800;
            font-size: 1rem;
            cursor: pointer;
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.3);
        }
        .btn-primary {
            background: linear-gradient(105deg, #ff8c00, #ff3c8e);
            color: white;
        }
        .btn-danger {
            background: linear-gradient(105deg, #ff4d4d, #b0003a);
            color: white;
        }
        .report-output {
            background: #03010a;
            border-radius: 32px;
            padding: 22px;
            font-family: monospace;
            font-size: 0.82rem;
            white-space: pre-wrap;
            word-break: break-word;
            max-height: 500px;
            overflow-y: auto;
            line-height: 1.5;
        }
        .hidden { display: none; }
        footer {
            text-align: center;
            margin-top: 40px;
            font-size: 0.7rem;
            opacity: 0.7;
        }
        @media (max-width: 860px) {
            .dashboard { flex-direction: column; }
        }
    </style>
</head>
<body>
<img src="https://i.pinimg.com/736x/8a/4d/3a/8a4d3a6e5b2c1d8f9e7a3b5c0d4f2e1a.jpg" 
     alt="Матрёшка РП" class="matryoshka-bg"
     onerror="this.src='https://cdn-icons-png.flaticon.com/512/1995/1995572.png'">

<div class="theme-toggle" id="themeToggleBtn"><i class="fas fa-palette"></i> <span>Тема</span></div>

<div class="container">
    <div id="authScreen"></div>
    <div id="mainInterface" class="hidden">
        <div class="user-bar">
            <div class="user-badge" id="myProfileBtn"><i class="fas fa-id-card"></i> <span id="displayNick"></span></div>
            <div class="logout-btn" id="logoutBtn"><i class="fas fa-sign-out-alt"></i> Выйти</div>
        </div>
        <div class="start-section" id="startSection">
            <button id="enterReportBtn" class="start-report-btn"><i class="fas fa-file-signature"></i> Приступить к отчёту</button>
        </div>
        <div id="reportContent" class="hidden">
            <div class="dashboard">
                <div class="cards-area">
                    <div class="cards-grid" id="cardsGrid"></div>
                    <div class="action-bar">
                        <button class="btn btn-primary" id="generateReportBtn"><i class="fas fa-scroll"></i> ОТЧЁТ</button>
                        <div style="display: flex; align-items: center; gap: 12px; background:#110b1c; padding: 4px 20px; border-radius: 60px;">
                            <i class="fas fa-calendar-week"></i>
                            <input type="date" id="reportDateInput" style="background:transparent; border:none; color:inherit;">
                        </div>
                        <button class="btn btn-danger" id="clearAllBtn"><i class="fas fa-brush"></i> ОТЧИСТКА</button>
                    </div>
                    <div class="report-section" style="background:#0e0917; border-radius: 40px; padding: 16px;">
                        <div class="report-output" id="reportPreview">✨ Нажмите «Отчёт»</div>
                    </div>
                </div>
                <div class="side-area">
                    <div class="info-widget">
                        <div class="widget-title"><i class="fas fa-users"></i> Зарегистрированные</div>
                        <div class="users-list" id="registeredUsersList">Загрузка...</div>
                    </div>
                    <div class="info-widget">
                        <div class="widget-title"><i class="fas fa-globe"></i> Онлайн сейчас</div>
                        <div class="users-list" id="onlineList">🌙 загрузка...</div>
                    </div>
                    <div class="info-widget">
                        <div class="widget-title"><i class="fas fa-history"></i> Лента действий</div>
                        <div class="activity-log" id="activityLog">✨ Здесь будут действия</div>
                    </div>
                </div>
            </div>
            <footer>⚡ Ссылки синхронизируются. Нажмите на ник — личный кабинет со статистикой.</footer>
        </div>
    </div>
</div>

<!-- Модальное окно профиля -->
<div id="profileModal" class="profile-modal">
    <div class="modal-content">
        <span class="close-modal">&times;</span>
        <h3><i class="fas fa-user-circle"></i> <span id="profileNick"></span></h3>
        <div class="profile-badge" id="profileEmail"></div>
        <div class="profile-stats" id="profileStats"></div>
    </div>
</div>

<script>
    // ---------- ХРАНИЛИЩЕ ----------
    const STORAGE_GLOBAL_DATA = 'global_media_cards_email';
    const STORAGE_USERS = 'media_users_email_full';
    const STORAGE_CURRENT_USER = 'media_current_user_email';
    const STORAGE_ACTIVITY_PREFIX = 'user_activity_email_';
    const STORAGE_ONLINE_KEY = 'online_users_email';
    const STORAGE_USER_STATS = 'user_stats_'; // статистика по каждому пользователю

    const PREREGISTERED_USERS = {
        "Ileya_Grinchers": { password: "media123", email: "ileyagrinchers@mediacenter.ru" },
        "Sanya_Harrington": { password: "pass456", email: "sanya@mediacenter.ru" }
    };

    const categories = [
        { id: "interview1", label: "Собеседование 1" }, { id: "interview2", label: "Собеседование 2" },
        { id: "interview3", label: "Собеседование 3" }, { id: "interview4", label: "Собеседование 4" },
        { id: "training1", label: "Тренировка 1" }, { id: "training2", label: "Тренировка 2" },
        { id: "lectures", label: "Лекции" }, { id: "live1", label: "Эфир 1" },
        { id: "live2", label: "Эфир 2" }, { id: "rpSituation", label: "РП ситуация" },
        { id: "commonRp", label: "Совместная РП" }
    ];

    let currentUser = null;
    let currentUserEmail = null;
    let globalCardsData = {};
    let activityLogs = [];
    let cardsRendered = false;

    // Статистика пользователя
    function getUserStats(nick) {
        let stats = localStorage.getItem(STORAGE_USER_STATS + nick);
        if (stats) return JSON.parse(stats);
        return { interviews: 0, lives: 0, trainings: 0, lectures: 0, rpSituations: 0, commonRp: 0 };
    }

    function saveUserStats(nick, stats) {
        localStorage.setItem(STORAGE_USER_STATS + nick, JSON.stringify(stats));
    }

    // Обновление статистики на основе глобальных данных
    function updateStatsForAllUsers() {
        // Для каждого зарегистрированного пользователя пересчитываем его вклад в глобальные данные
        const users = JSON.parse(localStorage.getItem(STORAGE_USERS) || '{}');
        for (let nick of Object.keys(users)) {
            // Статистика теперь глобальная — все видят одну и ту же работу
            // Считаем заполненные поля в глобальных данных
            let interviewsCount = 0, livesCount = 0, trainingsCount = 0, lecturesCount = 0, rpCount = 0, commonRpCount = 0;
            for (let i = 1; i <= 4; i++) {
                let d = globalCardsData[`interview${i}`] || {};
                if (d.link?.trim() || d.comment?.trim()) interviewsCount++;
            }
            for (let i = 1; i <= 2; i++) {
                let d = globalCardsData[`live${i}`] || {};
                if (d.link?.trim() || d.comment?.trim()) livesCount++;
            }
            for (let i = 1; i <= 2; i++) {
                let d = globalCardsData[`training${i}`] || {};
                if (d.link?.trim() || d.comment?.trim()) trainingsCount++;
            }
            let lec = globalCardsData["lectures"] || {};
            if (lec.link?.trim() || lec.comment?.trim()) lecturesCount = 1;
            let rp = globalCardsData["rpSituation"] || {};
            if (rp.link?.trim() || rp.comment?.trim()) rpCount = 1;
            let crp = globalCardsData["commonRp"] || {};
            if (crp.link?.trim() || crp.comment?.trim()) commonRpCount = 1;
            
            const stats = { interviews: interviewsCount, lives: livesCount, trainings: trainingsCount, lectures: lecturesCount, rpSituations: rpCount, commonRp: commonRpCount };
            saveUserStats(nick, stats);
        }
    }

    function initGlobalData() {
        let saved = localStorage.getItem(STORAGE_GLOBAL_DATA);
        if (saved) {
            globalCardsData = JSON.parse(saved);
        } else {
            globalCardsData = {};
        }
        categories.forEach(cat => {
            if (!globalCardsData[cat.id]) globalCardsData[cat.id] = { link: "", comment: "" };
        });
        saveGlobalData();
        updateStatsForAllUsers();
    }
    function saveGlobalData() {
        localStorage.setItem(STORAGE_GLOBAL_DATA, JSON.stringify(globalCardsData));
        localStorage.setItem('global_update_flag', Date.now().toString());
        updateStatsForAllUsers();
    }

    window.addEventListener('storage', (e) => {
        if (e.key === 'global_update_flag' || e.key === STORAGE_GLOBAL_DATA) {
            let saved = localStorage.getItem(STORAGE_GLOBAL_DATA);
            if (saved) {
                globalCardsData = JSON.parse(saved);
                if (cardsRendered) updateAllInputsFromData();
                updateStatsForAllUsers();
            }
            refreshOnlineList();
            renderRegisteredUsers();
        }
    });

    function updateAllInputsFromData() {
        categories.forEach(cat => {
            const data = globalCardsData[cat.id] || { link: "", comment: "" };
            const cardDiv = document.querySelector(`.card[data-card-id="${cat.id}"]`);
            if (cardDiv) {
                const linkInput = cardDiv.querySelector(".card-link");
                const commentInput = cardDiv.querySelector(".card-comment");
                if (linkInput && linkInput.value !== data.link) linkInput.value = data.link;
                if (commentInput && commentInput.value !== data.comment) commentInput.value = data.comment;
                if ((data.link?.trim() || data.comment?.trim())) cardDiv.classList.add("completed");
                else cardDiv.classList.remove("completed");
            }
        });
    }

    function saveFieldGlobally(cardId, field, value, cardLabel) {
        if (!globalCardsData[cardId]) globalCardsData[cardId] = { link: "", comment: "" };
        const old = globalCardsData[cardId][field];
        if (old !== value) {
            globalCardsData[cardId][field] = value;
            saveGlobalData();
            if (value && value.trim()) addActivity(cardLabel, field, value.trim());
            else if (old && !value.trim()) addActivity(cardLabel, field, "очистил поле");
            const cardDiv = document.querySelector(`.card[data-card-id="${cardId}"]`);
            if (cardDiv) {
                if ((globalCardsData[cardId].link?.trim() || globalCardsData[cardId].comment?.trim())) cardDiv.classList.add("completed");
                else cardDiv.classList.remove("completed");
            }
        }
    }

    function addActivity(cardLabel, fieldType, preview) {
        if (!currentUser) return;
        const now = new Date();
        const timeStr = `${now.toLocaleDateString()} ${now.toLocaleTimeString()}`;
        let actionText = fieldType === 'link' ? `Ссылка: ${preview.substring(0, 65)}${preview.length>65?'…':''}` : `Комментарий: ${preview.substring(0, 70)}${preview.length>70?'…':''}`;
        activityLogs.unshift({ user: currentUser, card: cardLabel, action: actionText, time: timeStr });
        if (activityLogs.length > 50) activityLogs.pop();
        saveActivityLog(currentUser);
        renderActivityLog();
    }

    function renderActivityLog() {
        const logDiv = document.getElementById("activityLog");
        if (!logDiv) return;
        if (!activityLogs.length) { logDiv.innerHTML = '<div style="text-align:center; opacity:0.7;">✨ Действия появятся здесь</div>'; return; }
        logDiv.innerHTML = '';
        activityLogs.slice(0, 20).forEach(log => {
            const el = document.createElement('div');
            el.className = 'log-item';
            el.innerHTML = `<div class="log-user">👤 ${escapeHtml(log.user)} • ${escapeHtml(log.card)}</div>
                            <div class="log-action">📌 ${escapeHtml(log.action)}</div>
                            <div class="log-time">🕒 ${escapeHtml(log.time)}</div>`;
            logDiv.appendChild(el);
        });
    }

    function renderCards() {
        const grid = document.getElementById("cardsGrid");
        if (!grid) return;
        grid.innerHTML = "";
        categories.forEach(cat => {
            const data = globalCardsData[cat.id] || { link: "", comment: "" };
            const card = document.createElement("div");
            card.className = "card";
            if (data.link?.trim() || data.comment?.trim()) card.classList.add("completed");
            card.setAttribute("data-card-id", cat.id);
            let icon = "📌";
            if (cat.label.includes("Собеседование")) icon = "🎙️";
            else if (cat.label.includes("Тренировка")) icon = "⚡";
            else if (cat.label.includes("Лекции")) icon = "📚";
            else if (cat.label.includes("Эфир")) icon = "📺";
            else if (cat.label.includes("РП ситуация")) icon = "🎭";
            else if (cat.label.includes("Совместная")) icon = "🤝";
            card.innerHTML = `
                <div class="card-header">
                    <div><i>${icon}</i> ${cat.label}</div>
                    <i class="fas fa-check-circle check-icon"></i>
                </div>
                <div class="card-body">
                    <div class="input-field"><label>Ссылка</label><input type="text" class="card-link" placeholder="https://..." value="${escapeHtml(data.link)}"></div>
                    <div class="input-field"><label>Комментарий</label><textarea class="card-comment" rows="2" placeholder="Опишите...">${escapeHtml(data.comment)}</textarea></div>
                </div>
            `;
            const linkInp = card.querySelector(".card-link");
            const commentInp = card.querySelector(".card-comment");
            linkInp.addEventListener("input", (e) => saveFieldGlobally(cat.id, "link", e.target.value, cat.label));
            commentInp.addEventListener("input", (e) => saveFieldGlobally(cat.id, "comment", e.target.value, cat.label));
            grid.appendChild(card);
        });
        cardsRendered = true;
    }

    function escapeHtml(str) { if(!str) return ''; return str.replace(/[&<>]/g, m => ({'&':'&amp;','<':'&lt;','>':'&gt;'}[m])); }

    function getFormattedDate() {
        const picker = document.getElementById("reportDateInput");
        let raw = picker.value;
        if (!raw) {
            const d = new Date();
            raw = `${d.getFullYear()}-${String(d.getMonth()+1).padStart(2,'0')}-${String(d.getDate()).padStart(2,'0')}`;
            picker.value = raw;
        }
        const [y,m,day] = raw.split("-");
        return `${day}. ${m}. ${y.slice(2)}`;
    }

    function generateReport() {
        const date = getFormattedDate();
        let report = `1. Ваш Ник: Ileya_Grinchers\n2. Ваша фракция: Медиацентр temp\n3. Дата: ${date}\n4. Проделанная работа (описание):\n`;
        
        let filledInterviews = 0, filledLives = 0, filledTrainings = 0, hasLectures = false, hasRp = false, hasCommonRp = false;
        for (let i = 1; i <= 4; i++) {
            let d = globalCardsData[`interview${i}`] || {};
            if (d.link?.trim() || d.comment?.trim()) filledInterviews++;
        }
        for (let i = 1; i <= 2; i++) {
            let d = globalCardsData[`live${i}`] || {};
            if (d.link?.trim() || d.comment?.trim()) filledLives++;
        }
        for (let i = 1; i <= 2; i++) {
            let d = globalCardsData[`training${i}`] || {};
            if (d.link?.trim() || d.comment?.trim()) filledTrainings++;
        }
        let lec = globalCardsData["lectures"] || {};
        if (lec.link?.trim() || lec.comment?.trim()) hasLectures = true;
        let rp = globalCardsData["rpSituation"] || {};
        if (rp.link?.trim() || rp.comment?.trim()) hasRp = true;
        let crp = globalCardsData["commonRp"] || {};
        if (crp.link?.trim() || crp.comment?.trim()) hasCommonRp = true;

        let workLines = [];
        if (filledInterviews > 0) workLines.push(`${filledInterviews} собеседование${filledInterviews>1?'ния':'ние'}`);
        if (filledLives > 0) workLines.push(`${filledLives} эфир${filledLives>1?'а':' '}`);
        if (hasLectures) workLines.push(`лекции`);
        if (filledTrainings > 0) workLines.push(`${filledTrainings} тренировк${filledTrainings>1?'и':'а'}`);
        if (hasRp) workLines.push(`рп с составом`);
        if (hasCommonRp) workLines.push(`совместная рп`);
        if (workLines.length === 0) workLines.push("нет заполненных данных");
        report += workLines.join("\n") + "\n";
        
        report += `5. Доказательства:\n`;
        
        let interviewsList = [];
        for (let i = 1; i <= 4; i++) {
            let d = globalCardsData[`interview${i}`] || {};
            if (d.link?.trim() || d.comment?.trim()) {
                let line = `${d.link || "(не указана)"}`;
                if (d.comment?.trim()) line += `\n   ${d.comment}`;
                interviewsList.push(line);
            }
        }
        if (interviewsList.length > 0) { report += `Собеседования:\n`; interviewsList.forEach((it, idx) => report += `${idx+1}. ${it}\n`); }
        
        let livesList = [];
        for (let i = 1; i <= 2; i++) {
            let d = globalCardsData[`live${i}`] || {};
            if (d.link?.trim() || d.comment?.trim()) {
                let line = `${d.link || "(не указана)"}`;
                if (d.comment?.trim()) line += `\n   ${d.comment}`;
                livesList.push(line);
            }
        }
        if (livesList.length > 0) { report += `\nЭфиры:\n`; livesList.forEach((it, idx) => report += `${idx+1}. ${it}\n`); }
        
        let trainingsList = [];
        for (let i = 1; i <= 2; i++) {
            let d = globalCardsData[`training${i}`] || {};
            if (d.link?.trim() || d.comment?.trim()) {
                let line = `${d.link || "(не указана)"}`;
                if (d.comment?.trim()) line += `\n   ${d.comment}`;
                trainingsList.push(line);
            }
        }
        if (trainingsList.length > 0) { report += `\nТренировки:\n`; trainingsList.forEach((it, idx) => report += `${idx+1}. ${it}\n`); }
        
        if (lec.link?.trim() || lec.comment?.trim()) { report += `\nЛекции:\n${lec.link || "(не указана)"}`; if (lec.comment?.trim()) report += `\n   ${lec.comment}`; }
        if (rp.link?.trim() || rp.comment?.trim()) { report += `\n\nРп ситуация:\n${rp.link || "(не указана)"}`; if (rp.comment?.trim()) report += `\n   ${rp.comment}`; }
        if (crp.link?.trim() || crp.comment?.trim()) { report += `\n\nСовместная рп ситуация:\n${crp.link || "(не указана)"}`; if (crp.comment?.trim()) report += `\n   ${crp.comment}`; }
        
        document.getElementById("reportPreview").innerText = report || "Нет данных для отчёта";
    }

    function clearAll() {
        categories.forEach(cat => {
            if (globalCardsData[cat.id]) { globalCardsData[cat.id].link = ""; globalCardsData[cat.id].comment = ""; }
        });
        saveGlobalData();
        updateAllInputsFromData();
        addActivity("Система", "очистка", "Очистил все поля");
        document.getElementById("reportPreview").innerHTML = "🧹 Все данные сброшены";
    }

    // Отображение профиля
    function showProfile(nick) {
        const users = JSON.parse(localStorage.getItem(STORAGE_USERS) || '{}');
        const userData = users[nick];
        if (!userData) return;
        const stats = getUserStats(nick);
        document.getElementById("profileNick").innerText = nick;
        document.getElementById("profileEmail").innerHTML = `<i class="fas fa-envelope"></i> ${userData.email || "email не указан"}`;
        const statsHtml = `
            <div class="stat-item"><span>📋 Собеседования:</span><span>${stats.interviews}</span></div>
            <div class="stat-item"><span>📺 Эфиры:</span><span>${stats.lives}</span></div>
            <div class="stat-item"><span>⚡ Тренировки:</span><span>${stats.trainings}</span></div>
            <div class="stat-item"><span>📚 Лекции:</span><span>${stats.lectures}</span></div>
            <div class="stat-item"><span>🎭 РП ситуации:</span><span>${stats.rpSituations}</span></div>
            <div class="stat-item"><span>🤝 Совместные РП:</span><span>${stats.commonRp}</span></div>
        `;
        document.getElementById("profileStats").innerHTML = statsHtml;
        document.getElementById("profileModal").style.display = "flex";
    }

    function renderRegisteredUsers() {
        const users = JSON.parse(localStorage.getItem(STORAGE_USERS) || '{}');
        const userList = Object.keys(users);
        const container = document.getElementById("registeredUsersList");
        if (container) {
            if (userList.length === 0) container.innerHTML = '<span class="registered-badge">Нет пользователей</span>';
            else {
                container.innerHTML = userList.map(u => `<span class="registered-badge" data-user="${escapeHtml(u)}"><i class="fas fa-user-check"></i> ${escapeHtml(u)}</span>`).join('');
                document.querySelectorAll('.registered-badge[data-user]').forEach(el => {
                    el.addEventListener('click', () => showProfile(el.getAttribute('data-user')));
                });
            }
        }
    }

    function refreshOnlineList() {
        let list = JSON.parse(localStorage.getItem(STORAGE_ONLINE_KEY) || '[]');
        list = [...new Set(list)];
        const container = document.getElementById("onlineList");
        if (container) {
            if (list.length === 0) container.innerHTML = '<span class="online-badge">🌙 никто не в сети</span>';
            else {
                container.innerHTML = list.map(u => `<span class="online-badge"><span class="online-dot"></span> ${escapeHtml(u)}</span>`).join('');
            }
        }
    }
    setInterval(refreshOnlineList, 4000);

    function updateOnlineStatus() {
        if (!currentUser) return;
        let online = JSON.parse(localStorage.getItem(STORAGE_ONLINE_KEY) || '[]');
        if (!online.includes(currentUser)) online.push(currentUser);
        localStorage.setItem(STORAGE_ONLINE_KEY, JSON.stringify(online));
        window.addEventListener('beforeunload', () => {
            let list = JSON.parse(localStorage.getItem(STORAGE_ONLINE_KEY) || '[]');
            let filtered = list.filter(u => u !== currentUser);
            localStorage.setItem(STORAGE_ONLINE_KEY, JSON.stringify(filtered));
        });
        refreshOnlineList();
    }

    function saveActivityLog(nick) { localStorage.setItem(STORAGE_ACTIVITY_PREFIX + nick, JSON.stringify(activityLogs)); }
    function loadActivityLog(nick) {
        const raw = localStorage.getItem(STORAGE_ACTIVITY_PREFIX + nick);
        activityLogs = raw ? JSON.parse(raw) : [];
    }

    // АВТОРИЗАЦИЯ С EMAIL
    function showAuthScreen() {
        const authDiv = document.getElementById("authScreen");
        authDiv.innerHTML = `
            <div class="auth-wrapper"><div class="auth-card">
                <h2>МедиаЦентр Temp</h2>
                <div class="input-group">
                    <label><i class="fas fa-user"></i> Никнейм (Name_Family)</label>
                    <input type="text" id="regNick" placeholder="Ivan_Ivanov">
                </div>
                <div class="input-group">
                    <label><i class="fas fa-envelope"></i> Электронная почта</label>
                    <input type="email" id="regEmail" placeholder="example@mail.ru">
                    <div class="hint-text">Нужна для восстановления пароля</div>
                </div>
                <div class="input-group">
                    <label><i class="fas fa-lock"></i> Пароль (мин. 6 символов)</label>
                    <input type="text" id="regPass" placeholder="пароль">
                    <div class="hint-text"><button type="button" id="genPassBtn" class="gen-password-btn"><i class="fas fa-key"></i> Сгенерировать</button></div>
                </div>
                <div id="authError" class="error-msg"></div>
                <button class="auth-btn" id="doLoginBtn">Войти</button>
                <button class="auth-btn" id="doRegisterBtn" style="background:#372b5a;">Создать аккаунт</button>
                <button class="forgot-password-btn" id="forgotPassBtn"><i class="fas fa-question-circle"></i> Забыли пароль?</button>
            </div></div>
        `;
        document.getElementById("genPassBtn").onclick = () => {
            const chars = 'ABCDEFGHJKLMNPQRSTUVWXYZabcdefghijkmnopqrstuvwxyz23456789!@#$%';
            let pwd = '';
            for (let i = 0; i < 12; i++) pwd += chars[Math.floor(Math.random() * chars.length)];
            document.getElementById("regPass").value = pwd;
            document.getElementById("authError").innerHTML = "✅ Пароль сгенерирован!";
        };
        document.getElementById("forgotPassBtn").onclick = () => {
            const email = prompt("Введите email, на который зарегистрирован аккаунт:");
            if (email) {
                const users = JSON.parse(localStorage.getItem(STORAGE_USERS) || '{}');
                let found = null;
                for (let [nick, data] of Object.entries(users)) {
                    if (data.email === email) { found = nick; break; }
                }
                if (found) alert(`Ваш пароль для ${found}: ${users[found].password}\n(в демо-режиме пароль показан здесь)`);
                else alert("Пользователь с таким email не найден");
            }
        };
        document.getElementById("doLoginBtn").onclick = () => handleAuth('login');
        document.getElementById("doRegisterBtn").onclick = () => handleAuth('register');
    }

    function handleAuth(mode) {
        const nick = document.getElementById("regNick").value.trim();
        const email = document.getElementById("regEmail")?.value.trim() || "";
        const pass = document.getElementById("regPass").value.trim();
        const errDiv = document.getElementById("authError");
        if (!/^[A-Za-z][A-Za-z0-9]*_[A-Za-z][A-Za-z0-9]*$/.test(nick)) {
            errDiv.innerText = "Формат Name_Family, латиница";
            return;
        }
        if (pass.length < 6 || !/^[A-Za-z0-9!@#$%]+$/.test(pass)) {
            errDiv.innerText = "Пароль ≥6 символов, буквы/цифры/!@#$%";
            return;
        }
        let users = JSON.parse(localStorage.getItem(STORAGE_USERS) || '{}');
        for (const [pn, data] of Object.entries(PREREGISTERED_USERS)) {
            if (!users[pn]) users[pn] = { password: data.password, email: data.email };
        }
        if (mode === 'register') {
            if (!email || !email.includes('@')) { errDiv.innerText = "Введите корректный email"; return; }
            if (users[nick]) { errDiv.innerText = "Ник занят"; return; }
            let emailExists = Object.values(users).some(u => u.email === email);
            if (emailExists) { errDiv.innerText = "Email уже используется"; return; }
            users[nick] = { password: pass, email: email };
            localStorage.setItem(STORAGE_USERS, JSON.stringify(users));
            currentUser = nick;
            currentUserEmail = email;
            localStorage.setItem(STORAGE_CURRENT_USER, currentUser);
            afterLogin();
        } else {
            // вход: можно по нику или по email
            let foundUser = null;
            if (users[nick] && users[nick].password === pass) foundUser = nick;
            else {
                for (let [un, data] of Object.entries(users)) {
                    if (data.email === nick && data.password === pass) foundUser = un;
                }
            }
            if (foundUser) {
                currentUser = foundUser;
                currentUserEmail = users[foundUser].email;
                localStorage.setItem(STORAGE_CURRENT_USER, currentUser);
                afterLogin();
            } else { errDiv.innerText = "Неверные данные"; }
        }
    }

    function afterLogin() {
        loadActivityLog(currentUser);
        renderActivityLog();
        document.getElementById("displayNick").innerHTML = currentUser;
        document.getElementById("authScreen").classList.add("hidden");
        document.getElementById("mainInterface").classList.remove("hidden");
        const datePick = document.getElementById("reportDateInput");
        if(datePick && !datePick.value) { let d=new Date(); datePick.value=`${d.getFullYear()}-${String(d.getMonth()+1).padStart(2,'0')}-${String(d.getDate()).padStart(2,'0')}`; }
        renderCards();
        renderRegisteredUsers();
        addActivity("Система", "вход", "Авторизовался");
        updateOnlineStatus();
    }

    document.addEventListener("click", (e) => {
        if (e.target.id === "enterReportBtn" || e.target.closest("#enterReportBtn")) {
            document.getElementById("startSection").classList.add("hidden");
            document.getElementById("reportContent").classList.remove("hidden");
            addActivity("Навигация", "открытие", "Открыл панель");
        }
        if (e.target.id === "myProfileBtn" || e.target.closest("#myProfileBtn")) {
            showProfile(currentUser);
        }
    });
    document.getElementById("logoutBtn")?.addEventListener("click", () => {
        let online = JSON.parse(localStorage.getItem(STORAGE_ONLINE_KEY) || '[]');
        let filtered = online.filter(u => u !== currentUser);
        localStorage.setItem(STORAGE_ONLINE_KEY, JSON.stringify(filtered));
        localStorage.removeItem(STORAGE_CURRENT_USER);
        location.reload();
    });
    document.getElementById("generateReportBtn")?.addEventListener("click", generateReport);
    document.getElementById("clearAllBtn")?.addEventListener("click", clearAll);
    document.querySelector(".close-modal")?.addEventListener("click", () => document.getElementById("profileModal").style.display = "none");
    window.onclick = (e) => { if (e.target === document.getElementById("profileModal")) document.getElementById("profileModal").style.display = "none"; };

    if (localStorage.getItem("theme") === "light") document.body.classList.add("light-theme");
    document.getElementById("themeToggleBtn").addEventListener("click", () => {
        document.body.classList.toggle("light-theme");
        localStorage.setItem("theme", document.body.classList.contains("light-theme") ? "light" : "dark");
    });

    initGlobalData();
    showAuthScreen();
    setInterval(() => { renderRegisteredUsers(); refreshOnlineList(); }, 5000);
</script>
</body>
</html>
