<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ADSPAY ELITE - OFFICIAL</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://unpkg.com/lucide@latest"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;600;900&display=swap');
        body { font-family: 'Outfit', sans-serif; background: #f0f4f8; overflow-x: hidden; }

        .glass { background: rgba(255, 255, 255, 0.8); backdrop-filter: blur(20px); border: 1px solid rgba(255,255,255,0.3); }

        /* Rubber Band Animation */
        @keyframes rubberBand {
            0% { transform: scale(1); }
            30% { transform: scaleX(1.25) scaleY(0.75); }
            40% { transform: scaleX(0.75) scaleY(1.25); }
            50% { transform: scaleX(1.15) scaleY(0.85); }
            100% { transform: scale(1); }
        }
        .haptic-touch:active i, .haptic-touch:active img, .haptic-touch:active div {
            animation: rubberBand 0.6s both;
        }

        /* Tab Transitions */
        .tab-content { display: none; }
        .tab-content.active { 
            display: block; 
            animation: slideIn 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275); 
        }

        @keyframes slideIn {
            from { opacity: 0; transform: translateY(30px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .auth-input { width: 100%; padding: 1.1rem; border-radius: 1.5rem; border: 1.5px solid #e2e8f0; background: #fff; outline: none; transition: 0.3s; font-size: 14px; }
        .auth-input:focus { border-color: #4f46e5; box-shadow: 0 10px 20px -10px rgba(79, 70, 229, 0.2); }
    </style>
</head>
<body class="pb-32">

    <div id="auth-section" class="min-h-screen flex flex-col justify-center p-6 space-y-6">
        
        <div id="login-tab" class="tab-content active space-y-6">
            <div class="text-center space-y-3">
                <div class="w-20 h-20 bg-indigo-600 text-white rounded-[2rem] mx-auto flex items-center justify-center shadow-2xl rotate-6 haptic-touch"><i data-lucide="shield-check" class="w-10 h-10"></i></div>
                <h2 class="text-3xl font-black tracking-tighter">Welcome Back!</h2>
                <p class="text-[10px] font-black text-slate-400 uppercase tracking-widest">Login to continue</p>
            </div>
            <div class="glass p-8 rounded-[3rem] shadow-xl space-y-4">
                <input type="email" id="log-email" placeholder="Gmail Address" class="auth-input">
                <input type="password" id="log-pass" placeholder="Password" class="auth-input">
                <div class="text-right"><button onclick="authTab('reset-tab')" class="text-[10px] font-black text-indigo-500 uppercase">Forgot Password?</button></div>
                <button id="login-btn" onclick="handleLogin()" class="w-full bg-indigo-600 text-white py-4 rounded-[1.5rem] font-black uppercase text-xs haptic-touch">Login Now</button>
            </div>
            <button onclick="authTab('reg-tab')" class="w-full text-xs font-black text-slate-500 uppercase text-center">New member? <span class="text-indigo-600">Register</span></button>
        </div>

        <div id="reg-tab" class="tab-content space-y-6">
            <div class="text-center space-y-2">
                <h2 class="text-3xl font-black tracking-tighter">Create Account</h2>
                <p class="text-[10px] font-black text-slate-400 uppercase tracking-widest text-center">Start your journey today</p>
            </div>
            <div class="glass p-8 rounded-[3rem] shadow-xl space-y-4 max-h-[70vh] overflow-y-auto">
                <input type="text" id="reg-name" placeholder="Full Name" class="auth-input">
                <input type="email" id="reg-email" placeholder="Gmail Address" class="auth-input">
                <input type="password" id="reg-pass" placeholder="Password" class="auth-input">
                <div class="bg-indigo-50 p-4 rounded-3xl border border-indigo-100">
                    <p class="text-[9px] font-black text-indigo-400 uppercase mb-2 ml-1">Refer Code (Optional)</p>
                    <input type="text" id="reg-ref" placeholder="Referral ID" class="w-full bg-transparent outline-none font-black text-sm text-indigo-600">
                </div>
                <button id="reg-btn" onclick="handleRegister()" class="w-full bg-emerald-500 text-white py-4 rounded-[1.5rem] font-black uppercase text-xs haptic-touch">Sign Up Free</button>
            </div>
            <button onclick="authTab('login-tab')" class="w-full text-xs font-black text-slate-500 uppercase text-center">Already registered? <span class="text-indigo-600">Login</span></button>
        </div>

        <div id="reset-tab" class="tab-content space-y-6">
            <div class="text-center space-y-4">
                <div class="w-20 h-20 bg-rose-500 text-white rounded-[2rem] mx-auto flex items-center justify-center shadow-2xl -rotate-6 haptic-touch"><i data-lucide="key-round" class="w-10 h-10"></i></div>
                <h2 class="text-3xl font-black tracking-tighter">Reset Password</h2>
                <p class="text-[10px] font-black text-slate-400 uppercase tracking-widest text-center px-10">পাসওয়ার্ড পরিবর্তনের লিঙ্ক আপনার জিমেইলে পাঠানো হবে</p>
            </div>
            <div class="glass p-8 rounded-[3rem] shadow-xl space-y-5">
                <input type="email" id="reset-email" placeholder="Enter Registered Gmail" class="auth-input">
                <button id="reset-btn" onclick="handlePasswordReset()" class="w-full bg-black text-white py-4 rounded-[1.5rem] font-black uppercase text-xs haptic-touch">Send Reset Link</button>
            </div>
            <button onclick="authTab('login-tab')" class="w-full text-xs font-black text-slate-500 uppercase text-center">Back to Login</button>
        </div>
    </div>

    <div id="main-app" class="hidden">
        <header class="p-6 glass sticky top-0 z-50 flex justify-between items-center rounded-b-[2.5rem] shadow-sm">
            <div class="flex items-center gap-4 haptic-touch">
                <div class="relative">
                    <img id="u-photo" src="https://ui-avatars.com/api/?name=User&background=4f46e5&color=fff" class="w-12 h-12 rounded-2xl shadow-xl border-2 border-white transition-transform">
                    <div id="verify-badge" class="hidden absolute -top-2 -right-2 bg-emerald-500 text-white rounded-full p-1 border-2 border-white animate-bounce">
                        <i data-lucide="check" class="w-3 h-3"></i>
                    </div>
                </div>
                <div>
                    <h3 id="u-name" class="font-black text-sm tracking-tight">Loading...</h3>
                    <p class="text-[8px] font-black text-indigo-500 uppercase tracking-widest">Elite Member</p>
                </div>
            </div>
            <div class="bg-black text-white p-3 px-5 rounded-2xl shadow-2xl active:scale-90 transition-transform">
                <p class="text-[10px] font-bold opacity-50 uppercase">Balance</p>
                <p class="text-lg font-black"><span id="u-balance">0.00</span>৳</p>
            </div>
        </header>

        <main class="p-5 space-y-6">
            <div id="home" class="tab-content active space-y-6">
                <div class="grid grid-cols-2 gap-4">
                    <div class="motion-card bg-white p-6 rounded-[2.5rem] border shadow-sm flex flex-col items-center haptic-touch">
                        <div class="bg-blue-50 text-blue-600 p-4 rounded-3xl mb-3"><i data-lucide="zap" class="w-6 h-6"></i></div>
                        <p class="text-[10px] font-black text-slate-400 uppercase">Tasks</p>
                        <p id="u-task-count" class="text-xl font-black">0</p>
                    </div>
                    <div class="motion-card bg-white p-6 rounded-[2.5rem] border shadow-sm flex flex-col items-center haptic-touch">
                        <div class="bg-emerald-50 text-emerald-600 p-4 rounded-3xl mb-3"><i data-lucide="users" class="w-6 h-6"></i></div>
                        <p class="text-[10px] font-black text-slate-400 uppercase">Refers</p>
                        <p id="u-ref-count" class="text-xl font-black">0</p>
                    </div>
                </div>

                <button onclick="tab('earn')" class="w-full glass p-6 rounded-[2.5rem] flex items-center justify-between haptic-touch shadow-xl">
                    <div class="flex items-center gap-5">
                        <div class="bg-indigo-600 text-white p-5 rounded-3xl"><i data-lucide="play-circle" class="w-7 h-7"></i></div>
                        <div class="text-left"><p class="font-black text-xl">Earn Now</p><p class="text-[10px] font-bold text-slate-400 uppercase tracking-widest">Start Daily Ads Job</p></div>
                    </div>
                    <i data-lucide="chevron-right" class="text-slate-300"></i>
                </button>

                <div class="grid grid-cols-3 gap-3">
                    <button onclick="tab('contact')" class="bg-white p-4 rounded-3xl border shadow-sm haptic-touch">
                        <i data-lucide="phone" class="w-5 h-5 mx-auto text-indigo-600 mb-2"></i>
                        <p class="text-[8px] font-black uppercase">Call</p>
                    </button>
                    <button onclick="tab('policy')" class="bg-white p-4 rounded-3xl border shadow-sm haptic-touch">
                        <i data-lucide="shield-check" class="w-5 h-5 mx-auto text-rose-500 mb-2"></i>
                        <p class="text-[8px] font-black uppercase">Rules</p>
                    </button>
                    <button onclick="tab('about')" class="bg-white p-4 rounded-3xl border shadow-sm haptic-touch">
                        <i data-lucide="info" class="w-5 h-5 mx-auto text-blue-500 mb-2"></i>
                        <p class="text-[8px] font-black uppercase">About</p>
                    </button>
                </div>
            </div>

            <div id="contact" class="tab-content space-y-4">
                <div class="glass p-8 rounded-[3rem] text-center space-y-6">
                    <div class="w-20 h-20 bg-indigo-600 text-white rounded-[2rem] mx-auto flex items-center justify-center shadow-2xl haptic-touch"><i data-lucide="headset" class="w-10 h-10"></i></div>
                    <h2 class="text-2xl font-black tracking-tight">Support</h2>
                    <div class="space-y-3">
                        <a href="tel:01617565066" class="flex items-center gap-4 p-5 bg-white rounded-3xl border haptic-touch"><i data-lucide="phone" class="text-indigo-600"></i> 01617565066</a>
                    </div>
                    <button onclick="tab('home')" class="w-full py-4 text-xs font-black uppercase text-slate-400">Back</button>
                </div>
            </div>
        </main>

        <nav class="fixed bottom-8 left-6 right-6 h-20 glass !rounded-[2.5rem] flex items-center justify-around px-4 shadow-2xl z-50">
            <button onclick="tab('home')" class="p-4 haptic-touch"><i data-lucide="home"></i></button>
            <button onclick="tab('earn')" class="p-4 haptic-touch"><i data-lucide="zap"></i></button>
            <button onclick="tab('wallet')" class="p-4 haptic-touch"><i data-lucide="wallet"></i></button>
            <button onclick="tab('profile')" class="p-4 haptic-touch"><i data-lucide="user"></i></button>
        </nav>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/9.23.0/firebase-app.js";
        import { getAuth, onAuthStateChanged, signInWithEmailAndPassword, createUserWithEmailAndPassword, sendPasswordResetEmail } from "https://www.gstatic.com/firebasejs/9.23.0/firebase-auth.js";
        import { getFirestore, doc, setDoc, onSnapshot } from "https://www.gstatic.com/firebasejs/9.23.0/firebase-firestore.js";

        const firebaseConfig = {
            apiKey: "AIzaSyATr7aDNNsydceq_Z_5SuW4gIyFchPEm4A",
            authDomain: "adspay-hup.firebaseapp.com",
            projectId: "adspay-hup",
            appId: "1:250165529622:web:35f1307b0acafb182bf937"
        };

        const app = initializeApp(firebaseConfig);
        const auth = getAuth(app);
        const db = getFirestore(app);

        // --- AUTH LOGIC ---
        window.authTab = (id) => {
            document.querySelectorAll('#auth-section .tab-content').forEach(t => t.classList.remove('active'));
            document.getElementById(id).classList.add('active');
            lucide.createIcons();
        };

        window.handleLogin = () => {
            const email = document.getElementById('log-email').value;
            const pass = document.getElementById('log-pass').value;
            if(!email || !pass) return alert("Email & Password Required!");
            signInWithEmailAndPassword(auth, email, pass).catch(e => alert(e.message));
        };

        window.handleRegister = async () => {
            const name = document.getElementById('reg-name').value;
            const email = document.getElementById('reg-email').value;
            const pass = document.getElementById('reg-pass').value;
            if(!name || !email || !pass) return alert("Fill all fields!");
            try {
                const cred = await createUserWithEmailAndPassword(auth, email, pass);
                await setDoc(doc(db, "users", cred.user.uid), {
                    uid: cred.user.uid, name, email, balance: 0, taskCompleted: 0, totalInvites: 0
                });
            } catch (e) { alert(e.message); }
        };

        window.handlePasswordReset = () => {
            const email = document.getElementById('reset-email').value;
            if(!email) return alert("Enter Gmail!");
            sendPasswordResetEmail(auth, email).then(() => alert("Reset link sent to Gmail!")).catch(e => alert(e.message));
        };

        // --- DASHBOARD LOGIC ---
        onAuthStateChanged(auth, (user) => {
            if (user) {
                document.getElementById('auth-section').classList.add('hidden');
                document.getElementById('main-app').classList.remove('hidden');
                onSnapshot(doc(db, "users", user.uid), (d) => {
                    const u = d.data();
                    if(u) {
                        document.getElementById('u-name').innerText = u.name;
                        document.getElementById('u-balance').innerText = u.balance.toFixed(2);
                        document.getElementById('u-task-count').innerText = u.taskCompleted;
                        document.getElementById('u-ref-count').innerText = u.totalInvites;
                        document.getElementById('u-photo').src = `https://ui-avatars.com/api/?name=${u.name}&background=4f46e5&color=fff`;
                    }
                });
            } else {
                document.getElementById('auth-section').classList.remove('hidden');
                document.getElementById('main-app').classList.add('hidden');
            }
            lucide.createIcons();
        });

        window.tab = (id) => {
            document.querySelectorAll('#main-app .tab-content').forEach(c => c.classList.remove('active'));
            document.getElementById(id).classList.add('active');
            lucide.createIcons();
        };

        lucide.createIcons();
    </script>
</body>
</html>
