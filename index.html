<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>貓貓收容所 - 雲端即時同步</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Noto+Sans+TC:wght@400;700&display=swap');
        body { font-family: 'Noto Sans TC', sans-serif; background-color: #0f172a; color: white; }
        .status-btn { transition: all 0.1s; border: 1px solid rgba(255,255,255,0.05); }
        .active-status { border: 2px solid #fbbf24 !important; background-color: #fbbf24 !important; color: #000 !important; font-weight: bold; }
        
        /* 狀態顏色定義 */
        .bg-正常 { background-color: #6366f1; } .bg-開船 { background-color: #0ea5e9; } 
        .bg-駐艇 { background-color: #3b82f6; } .bg-值更 { background-color: #10b981; }
        .bg-碼巡 { background-color: #14b8a6; } .bg-洽公 { background-color: #06b6d4; }
        .bg-幫廚 { background-color: #f43f5e; } .bg-補眠 { background-color: #8b5cf6; }
        .bg-放假班 { background-color: #f59e0b; } .bg-輪休 { background-color: #ef4444; }
        .bg-慰休 { background-color: #ec4899; } .bg-喪假 { background-color: #57534e; } 
        .bg-事假 { background-color: #78716c; } .bg-病假 { background-color: #1c1917; }
        .bg-空員 { background-color: #334155; }
    </style>
</head>
<body class="min-h-screen pb-20">
    <div class="max-w-4xl mx-auto px-3 pt-6">
        <div class="bg-slate-800 rounded-3xl p-5 shadow-2xl mb-4 border border-slate-700 sticky top-4 z-50">
            <div class="flex justify-between items-start mb-4">
                <div>
                    <h1 id="cloud-status" class="text-slate-500 text-[10px] font-bold mb-1 tracking-widest uppercase italic tracking-tighter">正在連線至 GitHub 雲端...</h1>
                    <div class="flex items-baseline gap-1 text-amber-400">
                        <span id="present-count" class="text-5xl font-black">0</span>
                        <span class="text-lg text-slate-500">/ 17</span>
                    </div>
                </div>
                <div class="text-right flex flex-col items-end gap-1">
                    <span class="bg-orange-500 text-[10px] px-2 py-1 rounded-md font-bold text-white shadow-sm">貓貓收容所 🐾</span>
                    <span id="update-timer" class="text-[9px] text-slate-500">自動同步中</span>
                </div>
            </div>
            <div id="category-board" class="grid grid-cols-2 sm:grid-cols-3 gap-2 mt-2 pt-3 border-t border-slate-700/50"></div>
        </div>

        <div class="space-y-2" id="app"></div>
    </div>

    <script>
        // --- 雲端設定連線區 ---
        const BIN_ID = "69f8acda36566621a8237f6f"; 
        const MASTER_KEY = "$2a$10$79/LnHKJxNsioXirnRhFKuTloIn5Fd3v7GSFct59XZWMIXWJuc9C2"; 

        const statuses = ['正常', '開船', '駐艇', '值更', '碼巡', '洽公', '幫廚', '補眠', '放假班', '輪休', '慰休', '喪假', '事假', '病假', '空員'];
        let memberStates = {};

        function initApp() {
            const app = document.getElementById('app');
            for (let i = 1; i <= 17; i++) {
                const id = i.toString().padStart(2, '0');
                memberStates[id] = '正常';
                const card = document.createElement('div');
                card.id = `card-${id}`;
                card.className = "bg-slate-800/80 p-3 rounded-2xl border border-slate-700/50 transition-all";
                card.innerHTML = `
                    <div class="flex justify-between items-center mb-2 px-1">
                        <div class="flex items-center gap-2">
                            <span class="w-6 h-6 flex items-center justify-center rounded bg-slate-900 text-slate-400 font-mono text-xs font-bold">${id}</span>
                            <span id="tag-${id}" class="px-2 py-0.5 rounded text-[9px] font-bold bg-正常 text-white">正常</span>
                        </div>
                    </div>
                    <div class="grid grid-cols-5 gap-1">
                        ${statuses.map(s => `<button onclick="updateStatus('${id}', '${s}')" id="btn-${id}-${s}" class="status-btn py-1.5 rounded-md text-[9px] bg-slate-900/40 text-slate-400">${s}</button>`).join('')}
                    </div>`;
                app.appendChild(card);
            }
        }

        async function fetchCloud() {
            try {
                const res = await fetch(`https://api.jsonbin.io/v3/b/${BIN_ID}/latest`, {
                    headers: { 'X-Master-Key': MASTER_KEY }
                });
                const data = await res.json();
                if (data.record && Object.keys(data.record).length > 0) {
                    memberStates = data.record;
                    Object.keys(memberStates).forEach(id => updateUI(id, memberStates[id]));
                    calculate();
                    document.getElementById('cloud-status').innerText = "● 雲端連線正常 (GitHub)";
                    document.getElementById('cloud-status').className = "text-green-500 text-[10px] font-bold mb-1 tracking-widest uppercase italic";
                }
            } catch (e) {
                document.getElementById('cloud-status').innerText = "○ 連線暫時中斷";
                document.getElementById('cloud-status').className = "text-red-500 text-[10px] font-bold mb-1 tracking-widest uppercase italic";
            }
        }

        async function saveCloud() {
            try {
                await fetch(`https://api.jsonbin.io/v3/b/${BIN_ID}`, {
                    method: 'PUT',
                    headers: {
                        'Content-Type': 'application/json',
                        'X-Master-Key': MASTER_KEY
                    },
                    body: JSON.stringify(memberStates)
                });
            } catch (e) { console.error("同步失敗"); }
        }

        function updateStatus(id, s) {
            memberStates[id] = s;
            updateUI(id, s);
            calculate();
            saveCloud();
        }

        function updateUI(id, s) {
            const tag = document.getElementById(`tag-${id}`);
            const card = document.getElementById(`card-${id}`);
            if(!tag) return;
            tag.textContent = s;
            tag.className = `px-2 py-0.5 rounded text-[9px] font-bold bg-${s} text-white`;
            document.querySelectorAll(`[id^="btn-${id}-"]`).forEach(b => b.classList.remove('active-status'));
            const btn = document.getElementById(`btn-${id}-${s}`);
            if(btn) btn.classList.add('active-status');
            card.style.opacity = (s === '空員') ? "0.3" : "1";
        }

        function calculate() {
            let p = 0; const g = {};
            statuses.forEach(s => g[s] = []);
            Object.keys(memberStates).forEach(id => {
                const s = memberStates[id];
                if(s === '正常') p++;
                g[s].push(id);
            });
            document.getElementById('present-count').textContent = p;
            const board = document.getElementById('category-board');
            board.innerHTML = statuses.slice(1, -1).filter(s => g[s].length > 0).map(s => `
                <div class="bg-slate-900/60 p-2 rounded-lg border border-slate-700/50">
                    <div class="text-[9px] text-slate-500 font-bold mb-0.5">${s}</div>
                    <div class="text-[11px] font-bold text-amber-500 font-mono tracking-tight">${g[s].join(',')}</div>
                </div>`).join('');
        }

        window.onload = () => {
            initApp();
            fetchCloud();
            // 每 15 秒同步一次，這對 JSONBin 免費版最穩定
            setInterval(fetchCloud, 15000); 
        };
    </script>
</body>
</html>
