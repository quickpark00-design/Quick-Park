<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ParkMaster Pro | 20 Slot Management</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
    <style>
        .glass { background: rgba(15, 23, 42, 0.9); backdrop-filter: blur(12px); }
        .slot-card { transition: all 0.2s ease-in-out; }
        .slot-card:hover:not(.occupied) { transform: translateY(-4px); border-color: #3b82f6; }
        /* Scrollbar styling for large grids */
        #slot-grid { max-height: 500px; overflow-y: auto; padding-right: 10px; }
        #slot-grid::-webkit-scrollbar { width: 6px; }
        #slot-grid::-webkit-scrollbar-thumb { background: #334155; border-radius: 10px; }
    </style>
</head>
<body class="bg-slate-950 text-slate-100 min-h-screen font-sans">

    <div id="auth-page" class="flex items-center justify-center min-h-screen p-4">
        <div class="glass p-8 rounded-3xl border border-slate-800 w-full max-w-md shadow-2xl">
            <div id="login-form">
                <div class="text-center mb-8">
                    <i class="fas fa-parking text-5xl text-blue-500 mb-4"></i>
                    <h2 class="text-3xl font-black tracking-tight text-white">Login</h2>
                </div>
                <input type="email" id="login-email" placeholder="Email" class="w-full mb-4 p-4 bg-slate-900 border border-slate-700 rounded-xl outline-none focus:ring-2 focus:ring-blue-500">
                <input type="password" id="login-pass" placeholder="Password" class="w-full mb-6 p-4 bg-slate-900 border border-slate-700 rounded-xl outline-none focus:ring-2 focus:ring-blue-500">
                <button onclick="handleLogin()" class="w-full bg-blue-600 hover:bg-blue-700 py-4 rounded-xl font-bold text-lg transition">Login</button>
                <p class="text-center mt-6 text-slate-400">Don't have an account <span onclick="toggleAuth(true)" class="text-blue-400 cursor-pointer hover:underline">Register</span></p>
            </div>

            <div id="register-form" class="hidden">
                <h2 class="text-3xl font-black mb-8 text-center text-emerald-400">Register</h2>
                <input type="text" id="reg-name" placeholder="Full Name" class="w-full mb-4 p-4 bg-slate-900 border border-slate-700 rounded-xl outline-none focus:ring-2 focus:ring-emerald-500">
                <input type="email" id="reg-email" placeholder="Email" class="w-full mb-4 p-4 bg-slate-900 border border-slate-700 rounded-xl outline-none focus:ring-2 focus:ring-emerald-500">
                <input type="password" id="reg-pass" placeholder="Password" class="w-full mb-6 p-4 bg-slate-900 border border-slate-700 rounded-xl outline-none focus:ring-2 focus:ring-emerald-500">
                <button onclick="handleRegister()" class="w-full bg-emerald-600 hover:bg-emerald-700 py-4 rounded-xl font-bold text-lg transition">Register Now</button>
                <p class="text-center mt-6 text-slate-400">Do you already have an account? <span onclick="toggleAuth(false)" class="text-emerald-400 cursor-pointer hover:underline">Login</span></p>
            </div>
        </div>
    </div>

    <div id="dashboard-page" class="hidden min-h-screen">
        <nav class="p-4 border-b border-slate-800 flex justify-between items-center glass sticky top-0 z-50">
            <div class="flex items-center gap-2">
                <div class="bg-blue-600 p-2 rounded-lg"><i class="fas fa-car-side text-white"></i></div>
                <h1 class="text-xl font-bold tracking-tighter uppercase">Parking<span class="text-blue-500">Master</span></h1>
            </div>
            <div class="flex items-center gap-4">
                <span id="user-display" class="text-sm font-medium text-slate-400"></span>
                <button onclick="logout()" class="text-xs bg-red-500/10 text-red-500 px-3 py-2 rounded-lg border border-red-500/20 hover:bg-red-500 hover:text-white transition">Logout</button>
            </div>
        </nav>

        <main class="max-w-7xl mx-auto p-6 grid grid-cols-1 lg:grid-cols-12 gap-8">
            <div class="lg:col-span-8">
                <div class="flex justify-between items-center mb-6">
                    <h2 class="text-2xl font-bold">Parking Grid (20 Slots)</h2>
                    <div class="flex gap-4">
                        <div class="bg-slate-900 px-3 py-1 border border-slate-800 rounded-full text-[10px] text-slate-400">1-10: Standard</div>
                        <div class="bg-slate-900 px-3 py-1 border border-amber-900/30 rounded-full text-[10px] text-amber-500">11-20: Premium</div>
                    </div>
                </div>
                <div id="slot-grid" class="grid grid-cols-2 sm:grid-cols-4 gap-4"></div>
                <div class="mt-4 bg-slate-900/50 p-4 rounded-xl border border-slate-800 flex justify-between text-xs text-slate-400">
                    <span>Total Slots: 20</span>
                    <span>Available: <span id="free-stat" class="text-green-400 font-bold">0</span></span>
                </div>
            </div>

            <div class="lg:col-span-4 space-y-6">
                <div class="glass p-6 rounded-2xl border border-slate-800 shadow-xl">
                    <h3 class="text-lg font-bold mb-4 border-b border-slate-800 pb-2 text-blue-400">Vehicle Details</h3>
                    <div id="details-view" class="hidden space-y-3 p-4 bg-slate-950 rounded-xl border border-blue-500/20 mb-4">
                        <div><p class="text-[10px] text-slate-500 font-bold uppercase">Driver</p><p id="v-name" class="font-bold"></p></div>
                        <div><p class="text-[10px] text-slate-500 font-bold uppercase">Plate</p><p id="v-plate" class="font-mono text-blue-400 text-lg"></p></div>
                        <div><p class="text-[10px] text-slate-500 font-bold uppercase">Model</p><p id="v-car" class="font-bold"></p></div>
                    </div>
                    <div id="booking-form" class="space-y-4">
                        <input type="text" id="in-name" placeholder="Driver Name" class="w-full p-3 bg-slate-900 border border-slate-700 rounded-xl outline-none focus:border-blue-500">
                        <input type="text" id="in-plate" placeholder="Plate No (e.g. MH12AB1234)" class="w-full p-3 bg-slate-900 border border-slate-700 rounded-xl outline-none focus:border-blue-500">
                        <input type="text" id="in-car" placeholder="Car Model" class="w-full p-3 bg-slate-900 border border-slate-700 rounded-xl outline-none focus:border-blue-500">
                    </div>
                </div>

                <div class="glass p-6 rounded-2xl border border-slate-800 shadow-xl">
                    <h3 class="text-lg font-bold mb-4 text-green-400">Plan & Payment</h3>
                    <select id="price-plan" class="w-full bg-slate-900 border border-slate-700 p-3 rounded-xl mb-4 text-sm" onchange="updatePrice()">
                        <option value="5">Hourly ($5.00)</option>
                        <option value="40">Daily ($40.00)</option>
                        <option value="120">Monthly ($120.00)</option>
                    </select>
                    <div class="flex justify-between items-center mb-6 p-3 bg-slate-950 rounded-lg">
                        <span class="text-sm font-bold text-slate-400">Final Price:</span>
                        <span id="final-price" class="text-2xl font-black text-green-400">$0.00</span>
                    </div>
                    <button id="main-btn" onclick="handleAction()" class="w-full bg-blue-600 hover:bg-blue-700 py-4 rounded-xl font-bold shadow-lg transition transform active:scale-95">Confirm & Book</button>
                </div>
            </div>
        </main>
    </div>

    <script>
        let registeredUser = null;
        let isLoggedIn = false;
        let selectedId = null;

        // UPDATED DATABASE: 10 Standard (1-10) and 10 Premium (11-20)
        let slots = Array.from({ length: 20 }, (_, i) => ({
            id: i + 1, 
            type: (i + 1) > 10 ? 'Premium' : 'Standard',
            status: 'available', 
            driver: '', 
            plate: '', 
            car: ''
        }));

        function toggleAuth(isReg) {
            document.getElementById('login-form').classList.toggle('hidden', isReg);
            document.getElementById('register-form').classList.toggle('hidden', !isReg);
        }

        function handleRegister() {
            const name = document.getElementById('reg-name').value;
            const email = document.getElementById('reg-email').value;
            const pass = document.getElementById('reg-pass').value;
            if (!name || !email || !pass) { alert("Sari details bharein!"); return; }
            registeredUser = { name, email, pass };
            alert("Registration Successful!");
            toggleAuth(false);
        }

        function handleLogin() {
            const email = document.getElementById('login-email').value;
            const pass = document.getElementById('login-pass').value;
            if (!registeredUser) { alert("Pehle Register karein!"); return; }
            if (email === registeredUser.email && pass === registeredUser.pass) {
                isLoggedIn = true;
                document.getElementById('user-display').innerText = "Hello, " + registeredUser.name;
                document.getElementById('auth-page').classList.add('hidden');
                document.getElementById('dashboard-page').classList.remove('hidden');
                renderSlots();
            } else { alert("Invalid Credentials!"); }
        }

        function logout() {
            isLoggedIn = false;
            document.getElementById('dashboard-page').classList.add('hidden');
            document.getElementById('auth-page').classList.remove('hidden');
            document.querySelectorAll('input').forEach(i => i.value = '');
        }

        function renderSlots() {
            const grid = document.getElementById('slot-grid');
            grid.innerHTML = '';
            let free = 0;
            slots.forEach(slot => {
                if(slot.status === 'available') free++;
                const isOcc = slot.status === 'occupied';
                const div = document.createElement('div');
                div.className = `slot-card p-4 rounded-2xl border-2 cursor-pointer flex flex-col items-center justify-center h-28 
                    ${isOcc ? 'bg-red-500/10 border-red-500/40' : 'bg-slate-900 border-slate-800'} 
                    ${selectedId === slot.id ? 'border-blue-500 bg-blue-500/10 scale-105 shadow-lg shadow-blue-500/20' : ''}`;
                
                div.innerHTML = `
                    <span class="text-[9px] ${slot.type==='Premium'?'text-amber-500 font-bold':'text-slate-500'} uppercase tracking-tighter">${slot.type}</span>
                    <span class="text-2xl font-black">${slot.id}</span>
                    <i class="fas ${isOcc ? 'fa-car text-red-500' : 'fa-check-circle text-green-500/50'} text-xs mt-1"></i>
                `;
                div.onclick = () => selectSlot(slot);
                grid.appendChild(div);
            });
            document.getElementById('free-stat').innerText = free;
        }

        function selectSlot(slot) {
            selectedId = slot.id;
            renderSlots();
            const form = document.getElementById('booking-form');
            const view = document.getElementById('details-view');
            const btn = document.getElementById('main-btn');

            if(slot.status === 'occupied') {
                form.classList.add('hidden');
                view.classList.remove('hidden');
                document.getElementById('v-name').innerText = slot.driver;
                document.getElementById('v-plate').innerText = slot.plate;
                document.getElementById('v-car').innerText = slot.car;
                btn.innerText = "Release Slot";
                btn.className = "w-full bg-red-600 hover:bg-red-700 py-4 rounded-xl font-bold transition text-white";
            } else {
                form.classList.remove('hidden');
                view.classList.add('hidden');
                btn.innerText = "Confirm & Book";
                btn.className = "w-full bg-blue-600 hover:bg-blue-700 py-4 rounded-xl font-bold transition text-white";
                document.getElementById('in-name').value = registeredUser.name;
            }
            updatePrice();
        }

        function updatePrice() {
            const base = parseFloat(document.getElementById('price-plan').value);
            const slot = slots.find(s => s.id === selectedId);
            const mult = (slot && slot.type === 'Premium') ? 1.5 : 1;
            document.getElementById('final-price').innerText = "$" + (base * mult).toFixed(2);
        }

        function handleAction() {
            if (!isLoggedIn) { alert("Please login first!"); return; }
            if(!selectedId) { alert("Select a slot!"); return; }
            const slot = slots.find(s => s.id === selectedId);

            if(slot.status === 'available') {
                const n = document.getElementById('in-name').value;
                const p = document.getElementById('in-plate').value;
                const c = document.getElementById('in-car').value;
                if(!n || !p || !c) { alert("Fill all details!"); return; }
                slot.status = 'occupied'; slot.driver = n; slot.plate = p.toUpperCase(); slot.car = c;
                alert("Slot " + slot.id + " Booked!");
            } else {
                slot.status = 'available'; slot.driver = ''; slot.plate = ''; slot.car = '';
                alert("Slot " + slot.id + " Released!");
            }
            renderSlots();
            selectSlot(slot);
        }
    </script>
</body>
</html>
