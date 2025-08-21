# Countdown-to-our-anniversary
Countdown to our anniversary
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>我们的纪念日倒计时</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            margin: 0;
            padding: 20px;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            color: white;
            position: relative;
        }

        .container {
            max-width: 1200px;
            width: 100%;
        }

        h1 {
            text-align: center;
            font-size: 2.5em;
            margin-bottom: 40px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }

        .countdown-section {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 30px;
            margin-bottom: 30px;
            box-shadow: 0 8px 32px rgba(0,0,0,0.1);
            border: 1px solid rgba(255, 255, 255, 0.2);
        }

        .event-title {
            font-size: 1.8em;
            text-align: center;
            margin-bottom: 20px;
            color: #ffeb3b;
            text-shadow: 1px 1px 2px rgba(0,0,0,0.5);
        }

        .countdown-display {
            display: flex;
            justify-content: center;
            gap: 20px;
            flex-wrap: wrap;
        }

        .time-unit {
            background: rgba(255, 255, 255, 0.2);
            border-radius: 15px;
            padding: 20px;
            text-align: center;
            min-width: 100px;
            backdrop-filter: blur(5px);
            border: 1px solid rgba(255, 255, 255, 0.3);
        }

        .time-number {
            font-size: 2.5em;
            font-weight: bold;
            display: block;
            text-shadow: 1px 1px 2px rgba(0,0,0,0.3);
        }

        .time-label {
            font-size: 1em;
            opacity: 0.9;
            margin-top: 5px;
        }

        .anniversary-info {
            text-align: center;
            margin-top: 15px;
            font-size: 1.1em;
            opacity: 0.9;
        }

        /* 弹窗样式 */
        .anniversary-popup {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.8);
            display: none;
            justify-content: center;
            align-items: center;
            z-index: 1000;
            backdrop-filter: blur(5px);
        }

        .popup-content {
            background: linear-gradient(135deg, #ff6b6b, #ee5a24, #ff9ff3, #54a0ff);
            border-radius: 25px;
            padding: 40px;
            text-align: center;
            max-width: 500px;
            width: 90%;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
            position: relative;
            overflow: hidden;
            animation: popupAppear 0.8s ease-out;
        }

        @keyframes popupAppear {
            0% {
                transform: scale(0.3) rotate(-10deg);
                opacity: 0;
            }
            50% {
                transform: scale(1.05) rotate(2deg);
            }
            100% {
                transform: scale(1) rotate(0deg);
                opacity: 1;
            }
        }

        .popup-title {
            font-size: 2.5em;
            margin-bottom: 20px;
            color: white;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
            animation: titleGlow 2s ease-in-out infinite alternate;
        }

        @keyframes titleGlow {
            from { text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3); }
            to { text-shadow: 2px 2px 20px rgba(255, 255, 255, 0.8); }
        }

        .popup-message {
            font-size: 1.3em;
            line-height: 1.6;
            color: white;
            margin-bottom: 30px;
            text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.3);
        }

        .close-popup {
            background: rgba(255, 255, 255, 0.2);
            border: 2px solid white;
            color: white;
            padding: 12px 30px;
            border-radius: 25px;
            font-size: 1.1em;
            cursor: pointer;
            transition: all 0.3s ease;
            backdrop-filter: blur(10px);
        }

        .close-popup:hover {
            background: rgba(255, 255, 255, 0.3);
            transform: scale(1.05);
        }

        /* 爱心飘落动画 */
        .hearts-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 999;
            display: none;
        }

        .heart {
            position: absolute;
            font-size: 20px;
            color: #ff69b4;
            animation: heartFall 4s linear infinite;
            opacity: 0.8;
        }

        @keyframes heartFall {
            0% {
                transform: translateY(-100px) rotate(0deg);
                opacity: 1;
            }
            100% {
                transform: translateY(100vh) rotate(360deg);
                opacity: 0;
            }
        }

        /* 烟花效果 */
        .firework {
            position: fixed;
            pointer-events: none;
            z-index: 998;
        }

        .firework-particle {
            position: absolute;
            width: 4px;
            height: 4px;
            background: #fff;
            border-radius: 50%;
            animation: fireworkExplode 1.5s ease-out forwards;
        }

        @keyframes fireworkExplode {
            0% {
                opacity: 1;
                transform: scale(1);
            }
            100% {
                opacity: 0;
                transform: scale(0);
            }
        }

        @media (max-width: 768px) {
            .countdown-display {
                gap: 10px;
            }
            
            .time-unit {
                min-width: 80px;
                padding: 15px;
            }
            
            .time-number {
                font-size: 2em;
            }
            
            h1 {
                font-size: 2em;
            }
            
            .event-title {
                font-size: 1.5em;
            }

            .popup-content {
                padding: 30px 20px;
                margin: 20px;
            }

            .popup-title {
                font-size: 2em;
            }

            .popup-message {
                font-size: 1.1em;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>💕 我们的纪念日倒计时 💕</h1>
        
        <!-- 第一次见面纪念日 -->
        <div class="countdown-section">
            <div class="event-title">🌟 第一次见面纪念日</div>
            <div class="countdown-display" id="firstMeet">
                <div class="time-unit">
                    <span class="time-number" id="firstMeetYears">0</span>
                    <div class="time-label">年</div>
                </div>
                <div class="time-unit">
                    <span class="time-number" id="firstMeetMonths">0</span>
                    <div class="time-label">月</div>
                </div>
                <div class="time-unit">
                    <span class="time-number" id="firstMeetDays">0</span>
                    <div class="time-label">天</div>
                </div>
                <div class="time-unit">
                    <span class="time-number" id="firstMeetHours">0</span>
                    <div class="time-label">小时</div>
                </div>
                <div class="time-unit">
                    <span class="time-number" id="firstMeetMinutes">0</span>
                    <div class="time-label">分钟</div>
                </div>
                <div class="time-unit">
                    <span class="time-number" id="firstMeetSeconds">0</span>
                    <div class="time-label">秒</div>
                </div>
            </div>
            <div class="anniversary-info" id="firstMeetInfo">
                距离下一个纪念日还有 <span id="firstMeetNextDays">0</span> 天
            </div>
        </div>

        <!-- 决定在一起纪念日 -->
        <div class="countdown-section">
            <div class="event-title">💖 决定在一起纪念日</div>
            <div class="countdown-display" id="together">
                <div class="time-unit">
                    <span class="time-number" id="togetherYears">0</span>
                    <div class="time-label">年</div>
                </div>
                <div class="time-unit">
                    <span class="time-number" id="togetherMonths">0</span>
                    <div class="time-label">月</div>
                </div>
                <div class="time-unit">
                    <span class="time-number" id="togetherDays">0</span>
                    <div class="time-label">天</div>
                </div>
                <div class="time-unit">
                    <span class="time-number" id="togetherHours">0</span>
                    <div class="time-label">小时</div>
                </div>
                <div class="time-unit">
                    <span class="time-number" id="togetherMinutes">0</span>
                    <div class="time-label">分钟</div>
                </div>
                <div class="time-unit">
                    <span class="time-number" id="togetherSeconds">0</span>
                    <div class="time-label">秒</div>
                </div>
            </div>
            <div class="anniversary-info" id="togetherInfo">
                距离下一个纪念日还有 <span id="togetherNextDays">0</span> 天
            </div>
        </div>

        <!-- 登记结婚纪念日 -->
        <div class="countdown-section">
            <div class="event-title">💍 登记结婚纪念日</div>
            <div class="countdown-display" id="marriage">
                <div class="time-unit">
                    <span class="time-number" id="marriageYears">0</span>
                    <div class="time-label">年</div>
                </div>
                <div class="time-unit">
                    <span class="time-number" id="marriageMonths">0</span>
                    <div class="time-label">月</div>
                </div>
                <div class="time-unit">
                    <span class="time-number" id="marriageDays">0</span>
                    <div class="time-label">天</div>
                </div>
                <div class="time-unit">
                    <span class="time-number" id="marriageHours">0</span>
                    <div class="time-label">小时</div>
                </div>
                <div class="time-unit">
                    <span class="time-number" id="marriageMinutes">0</span>
                    <div class="time-label">分钟</div>
                </div>
                <div class="time-unit">
                    <span class="time-number" id="marriageSeconds">0</span>
                    <div class="time-label">秒</div>
                </div>
            </div>
            <div class="anniversary-info" id="marriageInfo">
                距离下一个纪念日还有 <span id="marriageNextDays">0</span> 天
            </div>
        </div>

        <!-- 婚礼纪念日 -->
        <div class="countdown-section">
            <div class="event-title">💒 婚礼纪念日</div>
            <div class="countdown-display" id="wedding">
                <div class="time-unit">
                    <span class="time-number" id="weddingYears">0</span>
                    <div class="time-label">年</div>
                </div>
                <div class="time-unit">
                    <span class="time-number" id="weddingMonths">0</span>
                    <div class="time-label">月</div>
                </div>
                <div class="time-unit">
                    <span class="time-number" id="weddingDays">0</span>
                    <div class="time-label">天</div>
                </div>
                <div class="time-unit">
                    <span class="time-number" id="weddingHours">0</span>
                    <div class="time-label">小时</div>
                </div>
                <div class="time-unit">
                    <span class="time-number" id="weddingMinutes">0</span>
                    <div class="time-label">分钟</div>
                </div>
                <div class="time-unit">
                    <span class="time-number" id="weddingSeconds">0</span>
                    <div class="time-label">秒</div>
                </div>
            </div>
            <div class="anniversary-info" id="weddingInfo">
                距离下一个纪念日还有 <span id="weddingNextDays">0</span> 天
            </div>
        </div>
    </div>

    <!-- 纪念日弹窗 -->
    <div class="anniversary-popup" id="anniversaryPopup">
        <div class="popup-content">
            <div class="popup-title" id="popupTitle">🎉 特别的日子 🎉</div>
            <div class="popup-message" id="popupMessage">今天是我们的特殊纪念日！</div>
            <button class="close-popup" onclick="closePopup()">关闭</button>
        </div>
    </div>

    <!-- 爱心飘落容器 -->
    <div class="hearts-container" id="heartsContainer"></div>

    <script>
        // 设置重要日期
        const firstMeetDate = new Date('2024-01-17T00:00:00');
        const togetherDate = new Date('2024-01-21T00:00:00');
        const marriageDate = new Date('2024-10-22T00:00:00');
        const weddingDate = new Date('2025-06-28T00:00:00');

        // 浪漫话术配置
        const anniversaryMessages = {
            firstMeet: [
                "还记得那个美好的1月17日吗？✨\n那一天，命运让我们相遇，\n从此我的世界有了你的色彩。\n愿我们的爱情如初见时般美好！💕",
                "时光荏苒，初次相遇的美好依然历历在目 🌟\n感谢那个1月17日，让我遇见了最好的你。\n每一个纪念日都是我们爱情故事的续章！💖"
            ],
            together: [
                "1月21日，我们决定携手同行 💑\n从那一刻起，我们就是彼此的唯一。\n感谢你选择了我，也感谢我选择了你。\n愿我们永远相爱如初！💕",
                "这个特别的日子提醒着我们 💖\n爱情不只是心动的瞬间，\n更是相守一生的约定。\n谢谢你让我的生命如此完整！✨"
            ],
            marriage: [
                "10月22日，我们成为了法律意义上的一家人 💍\n从此以后，无论风雨，我们都在一起。\n这不只是一纸证书，更是我们永恒的约定！💒",
                "还记得那个激动人心的10月22日吗？💕\n我们在民政局许下了此生最重要的诺言。\n从那天起，你就是我的丈夫/妻子，我的一切！💖"
            ],
            wedding: [
                "6月28日，我们在众人的祝福中成为夫妻 💒\n那是我们人生中最美好的时刻之一。\n感谢所有见证我们爱情的人！\n愿我们的婚姻像那天一样幸福美满！💕",
                "婚礼那天的每一个细节都深深印在我心里 ✨\n你穿着婚纱/西装的样子美得让我心动。\n6月28日不只是我们的婚礼，\n更是我们新生活的开始！💖"
            ]
        };

        let hasShownTodaysPopup = {};

        function calculateTimeDifference(startDate) {
            const now = new Date();
            const diff = now - startDate;
            
            const years = Math.floor(diff / (365.25 * 24 * 60 * 60 * 1000));
            const months = Math.floor((diff % (365.25 * 24 * 60 * 60 * 1000)) / (30.44 * 24 * 60 * 60 * 1000));
            const days = Math.floor((diff % (30.44 * 24 * 60 * 60 * 1000)) / (24 * 60 * 60 * 1000));
            const hours = Math.floor((diff % (24 * 60 * 60 * 1000)) / (60 * 60 * 1000));
            const minutes = Math.floor((diff % (60 * 60 * 1000)) / (60 * 1000));
            const seconds = Math.floor((diff % (60 * 1000)) / 1000);
            
            return { years, months, days, hours, minutes, seconds };
        }

        function calculateNextAnniversary(startDate) {
            const now = new Date();
            const currentYear = now.getFullYear();
            
            let thisYearAnniversary = new Date(startDate);
            thisYearAnniversary.setFullYear(currentYear);
            
            if (now > thisYearAnniversary) {
                thisYearAnniversary.setFullYear(currentYear + 1);
            }
            
            const diffToNext = thisYearAnniversary - now;
            const daysToNext = Math.ceil(diffToNext / (24 * 60 * 60 * 1000));
            
            return daysToNext;
        }

        function isAnniversaryToday(anniversaryDate) {
            const now = new Date();
            const today = new Date(now.getFullYear(), now.getMonth(), now.getDate());
            const anniversary = new Date(now.getFullYear(), anniversaryDate.getMonth(), anniversaryDate.getDate());
            
            return today.getTime() === anniversary.getTime();
        }

        function showAnniversaryPopup(type, title) {
            const popup = document.getElementById('anniversaryPopup');
            const popupTitle = document.getElementById('popupTitle');
            const popupMessage = document.getElementById('popupMessage');
            
            const messages = anniversaryMessages[type];
            const randomMessage = messages[Math.floor(Math.random() * messages.length)];
            
            popupTitle.textContent = title;
            popupMessage.textContent = randomMessage;
            
            popup.style.display = 'flex';
            
            // 启动特效
            createHearts();
            createFireworks();
            
            // 标记今天已显示过弹窗
            const today = new Date().toDateString();
            hasShownTodaysPopup[type + today] = true;
        }

        function closePopup() {
            document.getElementById('anniversaryPopup').style.display = 'none';
            document.getElementById('heartsContainer').style.display = 'none';
            // 清除烟花
            const fireworks = document.querySelectorAll('.firework');
            fireworks.forEach(firework => firework.remove());
        }

        function createHearts() {
            const container = document.getElementById('heartsContainer');
            container.style.display = 'block';
            container.innerHTML = '';
            
            for (let i = 0; i < 20; i++) {
                setTimeout(() => {
                    const heart = document.createElement('div');
                    heart.className = 'heart';
                    heart.textContent = Math.random() > 0.5 ? '💕' : '💖';
                    heart.style.left = Math.random() * 100 + '%';
                    heart.style.animationDuration = (Math.random() * 3 + 2) + 's';
                    heart.style.animationDelay = Math.random() * 2 + 's';
                    container.appendChild(heart);
                    
                    setTimeout(() => {
                        if (container.contains(heart)) {
                            container.removeChild(heart);
                        }
                    }, 6000);
                }, i * 200);
            }
        }

        function createFireworks() {
            const colors = ['#ff6b6b', '#4ecdc4', '#45b7d1', '#feca57', '#ff9ff3', '#54a0ff'];
            
            for (let i = 0; i < 5; i++) {
                setTimeout(() => {
                    const firework = document.createElement('div');
                    firework.className = 'firework';
                    firework.style.left = Math.random() * window.innerWidth + 'px';
                    firework.style.top = Math.random() * window.innerHeight + 'px';
                    
                    for (let j = 0; j < 12; j++) {
                        const particle = document.createElement('div');
                        particle.className = 'firework-particle';
                        particle.style.background = colors[Math.floor(Math.random() * colors.length)];
                        
                        const angle = (j * 30) * Math.PI / 180;
                        const distance = Math.random() * 100 + 50;
                        const x = Math.cos(angle) * distance;
                        const y = Math.sin(angle) * distance;
                        
                        particle.style.transform = `translate(${x}px, ${y}px)`;
                        firework.appendChild(particle);
                    }
                    
                    document.body.appendChild(firework);
                    
                    setTimeout(() => {
                        if (document.body.contains(firework)) {
                            document.body.removeChild(firework);
                        }
                    }, 2000);
                }, i * 800);
            }
        }

        function checkAnniversaries() {
            const today = new Date().toDateString();
            
            if (isAnniversaryToday(firstMeetDate) && !hasShownTodaysPopup['firstMeet' + today]) {
                setTimeout(() => showAnniversaryPopup('firstMeet', '🌟 第一次见面纪念日快乐！'), 1000);
            }
            
            if (isAnniversaryToday(togetherDate) && !hasShownTodaysPopup['together' + today]) {
                setTimeout(() => showAnniversaryPopup('together', '💖 在一起纪念日快乐！'), 1000);
            }
            
            if (isAnniversaryToday(marriageDate) && !hasShownTodaysPopup['marriage' + today]) {
                setTimeout(() => showAnniversaryPopup('marriage', '💍 结婚纪念日快乐！'), 1000);
            }
            
            if (isAnniversaryToday(weddingDate) && !hasShownTodaysPopup['wedding' + today]) {
                setTimeout(() => showAnniversaryPopup('wedding', '💒 婚礼纪念日快乐！'), 1000);
            }
        }

        function updateCountdown() {
            // 更新第一次见面倒计时
            const firstMeetTime = calculateTimeDifference(firstMeetDate);
            document.getElementById('firstMeetYears').textContent = firstMeetTime.years;
            document.getElementById('firstMeetMonths').textContent = firstMeetTime.months;
            document.getElementById('firstMeetDays').textContent = firstMeetTime.days;
            document.getElementById('firstMeetHours').textContent = firstMeetTime.hours;
            document.getElementById('firstMeetMinutes').textContent = firstMeetTime.minutes;
            document.getElementById('firstMeetSeconds').textContent = firstMeetTime.seconds;
            
            const firstMeetNextDays = calculateNextAnniversary(firstMeetDate);
            document.getElementById('firstMeetNextDays').textContent = firstMeetNextDays;

            // 更新决定在一起倒计时
            const togetherTime = calculateTimeDifference(togetherDate);
            document.getElementById('togetherYears').textContent = togetherTime.years;
            document.getElementById('togetherMonths').textContent = togetherTime.months;
            document.getElementById('togetherDays').textContent = togetherTime.days;
            document.getElementById('togetherHours').textContent = togetherTime.hours;
            document.getElementById('togetherMinutes').textContent = togetherTime.minutes;
            document.getElementById('togetherSeconds').textContent = togetherTime.seconds;
            
            const togetherNextDays = calculateNextAnniversary(togetherDate);
            document.getElementById('togetherNextDays').textContent = togetherNextDays;

            // 更新结婚倒计时
            const marriageTime = calculateTimeDifference(marriageDate);
            document.getElementById('marriageYears').textContent = marriageTime.years;
            document.getElementById('marriageMonths').textContent = marriageTime.months;
            document.getElementById('marriageDays').textContent = marriageTime.days;
            document.getElementById('marriageHours').textContent = marriageTime.hours;
            document.getElementById('marriageMinutes').textContent = marriageTime.minutes;
            document.getElementById('marriageSeconds').textContent = marriageTime.seconds;
            
            const marriageNextDays = calculateNextAnniversary(marriageDate);
            document.getElementById('marriageNextDays').textContent = marriageNextDays;

            // 更新婚礼倒计时
            const weddingTime = calculateTimeDifference(weddingDate);
            document.getElementById('weddingYears').textContent = weddingTime.years;
            document.getElementById('weddingMonths').textContent = weddingTime.months;
            document.getElementById('weddingDays').textContent = weddingTime.days;
            document.getElementById('weddingHours').textContent = weddingTime.hours;
            document.getElementById('weddingMinutes').textContent = weddingTime.minutes;
            document.getElementById('weddingSeconds').textContent = weddingTime.seconds;
            
            const weddingNextDays = calculateNextAnniversary(weddingDate);
            document.getElementById('weddingNextDays').textContent = weddingNextDays;
        }

        // 初始化
        updateCountdown();
        checkAnniversaries();
        
        // 每秒更新一次
        setInterval(updateCountdown, 1000);
        
        // 每小时检查一次纪念日（以防错过）
        setInterval(checkAnniversaries, 3600000);
    </script>
</body>
</html>
