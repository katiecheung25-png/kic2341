<!DOCTYPE html>
<html lang="zh-Hant">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>韓國雙城 8 天 7 夜導航手冊</title>
<script src="https://cdn.tailwindcss.com"></script>
<style>
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+TC:wght@300;400;600;800&display=swap');
body {
    font-family: 'Noto Sans TC', sans-serif;
    background-color: #FAF9F6;
    color: #2C2C2C;
}
.hide-scroll::-webkit-scrollbar {
    display: none;
}
.hide-scroll {
    -ms-overflow-style: none;
    scrollbar-width: none;
}
.btn-active {
    background-color: #D4A373;
    color: white;
    border-color: #D4A373;
}
.btn-inactive {
    background-color: transparent;
    color: #6B705C;
    border-color: #E3D5CA;
}
.btn-nav {
    display: inline-flex;
    align-items: center;
    background-color: #6B705C;
    color: white;
    padding: 6px 14px;
    border-radius: 8px;
    font-size: 0.85rem;
    font-weight: 600;
    text-decoration: none;
    transition: opacity 0.2s;
}
.btn-nav:hover {
    opacity: 0.85;
}
</style>
<!-- Chosen Palette: Warm Earth Neutrals (Beige, Terracotta, Sage Green) -->
<!-- Application Structure Plan: The SPA is structured as an interactive dashboard. The left panel now focuses exclusively on navigation (Day Selectors) and essential tips. The right panel dynamically displays the selected day's detailed itinerary. This streamlined version removes the statistical overview to provide a cleaner, more direct navigation experience for the user on the move. -->
<!-- Visualization & Content Choices: 
1. Goal: Organize Daily Itinerary -> Viz: Interactive List/Tabs -> Interaction: Click day to filter details -> Justification: Prevents information overload by chunking content by day. 
2. Goal: Direct Action -> Viz: Linked Action Buttons -> Interaction: Click opens Naver Map -> Justification: Translates static text into actionable navigation steps directly supporting the trip.
CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
<!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
</head>
<body class="antialiased min-h-screen pb-12">

    <header class="bg-[#6B705C] text-[#FAF9F6] py-10 px-6 shadow-md border-b-4 border-[#D4A373]">
        <div class="max-w-5xl mx-auto">
            <h1 class="text-3xl md:text-4xl font-extrabold tracking-tight mb-2">🇰🇷 韓國雙城導航手冊</h1>
            <p class="text-lg opacity-90 font-light">釜山首爾 8 天 7 夜互動行程表 (5/9 - 5/16)</p>
        </div>
    </header>

    <main class="max-w-5xl mx-auto px-4 sm:px-6 mt-8">
        
        <section class="mb-10 bg-white p-6 md:p-8 rounded-2xl shadow-sm border border-[#E3D5CA]">
            <h2 class="text-xl font-bold mb-4 text-[#D4A373]">📌 關於本指南</h2>
            <p class="text-base leading-relaxed text-[#555555]">
                本互動指南將您的釜山與首爾行程轉化為易於探索的數位儀表板。您可以點擊左側的日期選單來動態切換右側的詳細行程。所有主要景點與餐廳均已內建 Naver Map 導航連結，確保您在旅途中能快速獲取路線資訊。首段行程將聚焦於釜山的 Visit Busan Pass (VBP) 體驗。
            </p>
        </section>

        <div class="grid grid-cols-1 md:grid-cols-12 gap-8">
            
            <div class="md:col-span-4 flex flex-col space-y-6">
                
                <section class="bg-white p-6 rounded-2xl shadow-sm border border-[#E3D5CA]">
                    <h3 class="text-lg font-bold mb-4 text-[#6B705C]">📅 選擇日期</h3>
                    <div class="flex flex-row md:flex-col gap-3 overflow-x-auto hide-scroll pb-2 md:pb-0" id="daySelectors">
                    </div>
                </section>
                
                <section class="bg-[#FFF9F0] p-6 rounded-2xl shadow-sm border border-[#F4E4BA]">
                    <h3 class="text-lg font-bold mb-3 text-[#D4A373]">💡 導航小叮嚀</h3>
                    <ul class="space-y-3 text-sm text-[#555555]">
                        <li class="flex items-start">
                            <span class="mr-2 text-lg">🎟️</span>
                            <span><strong>Visit Busan Pass:</strong> 48小時券請精確計算好使用時間，以發揮最大效益。</span>
                        </li>
                        <li class="flex items-start">
                            <span class="mr-2 text-lg">🗺️</span>
                            <span><strong>Naver Map App:</strong> 建議在手機下載該應用程式，並將語言設定為「中文」，配合本系統的按鈕使用最佳。</span>
                        </li>
                    </ul>
                </section>

            </div>

            <div class="md:col-span-8">
                <section id="detailPanel" class="bg-white p-6 md:p-8 rounded-2xl shadow-sm border border-[#E3D5CA] min-h-[500px]">
                </section>
            </div>

        </div>
    </main>

<script>
const tripData = {
    "5/9": {
        title: "5/9 (週六) - 入住海雲台與 VBP 啟動",
        location: "釜山",
        items: [
            { icon: "🏨", time: "抵達", name: "海雲台 W Apartment", desc: "行李寄存與辦理入住手續。", link: "https://naver.me/IMRnF9mF" },
            { icon: "🥣", time: "早上", name: "密陽聖代豬肉湯 (釜山總店)", desc: "享用釜山道地特色早餐。", link: "https://naver.me/FpM2S6Wf" },
            { icon: "🐠", time: "下午", name: "釜山水族館 Sea Life", desc: "正式開啟 Visit Busan Pass (48小時) 效期。", link: "https://naver.me/FoENALrx" },
            { icon: "🥩", time: "傍晚", name: "晚餐 A: 味贊王鹽烤肉", desc: "海雲台周邊人氣烤肉選擇。", link: "https://naver.me/G99R1hbe" },
            { icon: "🥩", time: "傍晚", name: "晚餐 B: 83烤肉", desc: "廣安里周邊人氣烤肉選擇。", link: "https://naver.me/xyT8I7oR" },
            { icon: "🛥️", time: "晚上", name: "鑽石灣遊艇夜景", desc: "使用 Visit Busan Pass 欣賞絕美夜景 (需預約)。", link: "https://naver.me/x7ndUL9U" }
        ]
    },
    "5/10": {
        title: "5/10 (週日) - 機張郡動感行程",
        location: "釜山",
        items: [
            { icon: "🏎️", time: "白天", name: "Skyline Luge 釜山", desc: "體驗刺激的斜坡滑車 (Visit Busan Pass 景點)。", link: "https://naver.me/F36XzC0j" },
            { icon: "🎡", time: "下午", name: "釜山樂天世界", desc: "探索大型主題遊樂園 (Visit Busan Pass 景點)。", link: "https://naver.me/xk6vW3wO" }
        ]
    },
    "5/11": {
        title: "5/11 (週一) - 景觀與汗蒸幕",
        location: "釜山",
        items: [
            { icon: "🏙️", time: "下午", name: "釜山 X the SKY", desc: "前往高空觀景台俯瞰海景 (Visit Busan Pass 景點)。", link: "https://naver.me/5vI6fO8z" },
            { icon: "♨️", time: "晚上", name: "Spa Land 汗蒸幕", desc: "新世界百貨內的高級汗蒸幕放鬆身心 (Visit Busan Pass 景點)。", link: "https://naver.me/FfMWpYvN" }
        ]
    }
};

let currentDay = "5/9";

function initApp() {
    renderSelectors();
    renderDetails(currentDay);
}

function renderSelectors() {
    const container = document.getElementById('daySelectors');
    container.innerHTML = '';
    
    Object.keys(tripData).forEach(day => {
        const btn = document.createElement('button');
        const isActive = day === currentDay;
        
        btn.className = `flex-shrink-0 w-32 md:w-full text-left px-5 py-4 rounded-xl border-2 font-bold transition-all duration-200 ${isActive ? 'btn-active shadow-md transform scale-[1.02]' : 'btn-inactive hover:bg-[#F5EBE4]'}`;
        btn.innerHTML = `<span class="block text-lg">${day}</span><span class="block text-xs font-normal opacity-80 mt-1">${tripData[day].location}</span>`;
        
        btn.onclick = () => {
            currentDay = day;
            renderSelectors();
            renderDetails(day);
        };
        container.appendChild(btn);
    });
}

function renderDetails(day) {
    const container = document.getElementById('detailPanel');
    const data = tripData[day];
    
    let html = `
        <div class="border-b-2 border-[#E3D5CA] pb-4 mb-6">
            <span class="inline-block px-3 py-1 bg-[#D4A373] text-white text-xs font-bold rounded-full mb-3">${data.location}</span>
            <h2 class="text-2xl font-extrabold text-[#2C2C2C]">${data.title}</h2>
        </div>
        <div class="space-y-6">
    `;
    
    data.items.forEach(item => {
        html += `
            <div class="flex flex-col sm:flex-row sm:items-start bg-[#FAF9F6] p-5 rounded-xl border border-[#E3D5CA] hover:shadow-md transition-shadow">
                <div class="flex items-center sm:items-start mb-3 sm:mb-0 sm:w-1/4 sm:pr-4">
                    <span class="text-3xl mr-3">${item.icon}</span>
                    <span class="text-sm font-bold text-[#D4A373] bg-[#FFF0E6] px-2 py-1 rounded-md">${item.time}</span>
                </div>
                <div class="sm:w-3/4 flex flex-col items-start">
                    <h4 class="text-lg font-bold text-[#2C2C2C] mb-1">${item.name}</h4>
                    <p class="text-sm text-[#666666] mb-3 leading-relaxed">${item.desc}</p>
                    <a href="${item.link}" target="_blank" class="btn-nav">
                        📍 開啟 Naver Map
                    </a>
                </div>
            </div>
        `;
    });
    
    html += `</div>`;
    container.innerHTML = html;
}

document.addEventListener('DOMContentLoaded', initApp);
</script>
</body>
</html>
