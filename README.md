<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>Bank Sampah ARAS - Dompet Digital</title>
    <style>
        /* === CSS (Tidak ada perubahan signifikan, tetap sama) === */
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background: linear-gradient(135deg, #f0f4f8 0%, #d9e2ec 100%); color: #333; min-height: 100vh; overflow-x: hidden; }
        .app-container { max-width: 414px; margin: 0 auto; background: #f8f9fa; min-height: 100vh; box-shadow: 0 0 20px rgba(0,0,0,0.1); position: relative; padding-bottom: 70px; }
        .header { background: linear-gradient(135deg, #2ecc71 0%, #27ae60 100%); color: white; padding: 25px 20px 30px; text-align: center; position: relative; overflow: hidden; border-bottom-left-radius: 20px; border-bottom-right-radius: 20px;}
        .header::before { content: ''; position: absolute; top: -50%; right: -20%; width: 100px; height: 100px; background: radial-gradient(circle, rgba(255,255,255,0.1) 0%, transparent 70%); border-radius: 50%; animation: float 6s ease-in-out infinite; }
        @keyframes float { 0%, 100% { transform: translateY(0px) rotate(0deg); } 50% { transform: translateY(-20px) rotate(180deg); } }
        .logo-container { display: flex; align-items: center; justify-content: center; margin-bottom: 10px; }
        .logo-icon { font-size: 32px; margin-right: 10px; }
        .logo-text { font-size: 24px; font-weight: bold; }
        .bank-name { font-size: 16px; opacity: 0.9; margin-bottom: 5px; }
        .location { font-size: 12px; opacity: 0.8; }
        .user-card { background: linear-gradient(135deg, #3498db 0%, #2980b9 100%); margin: -15px 20px 20px; padding: 20px; border-radius: 20px; color: white; box-shadow: 0 10px 30px rgba(52, 152, 219, 0.3); position: relative; overflow: hidden; }
        .user-card::before { content: '♻️'; position: absolute; top: 10px; right: 15px; font-size: 40px; opacity: 0.2; }
        .user-greeting { font-size: 14px; opacity: 0.9; margin-bottom: 5px; }
        .user-name { font-size: 20px; font-weight: bold; margin-bottom: 15px; }
        .user-stats { display: flex; justify-content: space-between; align-items: center; }
        .stat-item { text-align: center; }
        .stat-value { font-size: 18px; font-weight: bold; }
        .stat-label { font-size: 10px; opacity: 0.8; }
        .balance-section { padding: 0 20px; margin-bottom: 25px; }
        .balance-card { background: linear-gradient(135deg, #e74c3c 0%, #c0392b 100%); padding: 25px; border-radius: 20px; color: white; text-align: center; box-shadow: 0 10px 30px rgba(231, 76, 60, 0.3); position: relative; overflow: hidden; }
        .balance-card::before { content: '💰'; position: absolute; top: -10px; right: -10px; font-size: 60px; opacity: 0.1; transform: rotate(15deg); }
        .balance-label { font-size: 14px; opacity: 0.9; margin-bottom: 8px; }
        .balance-amount { font-size: 32px; font-weight: bold; margin-bottom: 15px; }
        .balance-actions { display: flex; gap: 10px; }
        .balance-btn { flex: 1; background: rgba(255,255,255,0.2); border: none; color: white; padding: 10px; border-radius: 10px; font-size: 12px; cursor: pointer; transition: all 0.3s ease; backdrop-filter: blur(10px); }
        .balance-btn:hover { background: rgba(255,255,255,0.3); transform: translateY(-2px); }
        .features-section { padding: 0 20px; margin-bottom: 25px; }
        .section-title { font-size: 18px; font-weight: bold; color: #2c3e50; margin-bottom: 15px; display: flex; align-items: center; }
        .section-title::before { content: '🌱'; margin-right: 8px; }
        .features-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 15px; margin-bottom: 20px; }
        .feature-item { background: white; border-radius: 15px; padding: 20px 10px; text-align: center; box-shadow: 0 5px 15px rgba(0,0,0,0.08); cursor: pointer; transition: all 0.3s ease; border: 2px solid transparent; }
        .feature-item:hover { transform: translateY(-5px); box-shadow: 0 10px 25px rgba(0,0,0,0.15); border-color: #2ecc71; }
        .feature-icon { font-size: 28px; margin-bottom: 8px; display: block; }
        .feature-text { font-size: 12px; color: #2c3e50; font-weight: 600; }
        .waste-calculator { background: linear-gradient(135deg, #f39c12 0%, #e67e22 100%); margin: 0 20px 20px; padding: 20px; border-radius: 15px; color: white; position: relative; overflow: hidden; }
        .waste-calculator::before { content: '⚖️'; position: absolute; top: 10px; right: 15px; font-size: 35px; opacity: 0.3; }
        .calculator-title { font-size: 16px; font-weight: bold; margin-bottom: 15px; }
        .calculator-row { display: flex; align-items: center; margin-bottom: 10px; }
        .calculator-input { flex: 1; background: rgba(255,255,255,0.2); border: none; color: white; padding: 8px 12px; border-radius: 8px; margin-right: 10px; font-size: 14px; }
        .calculator-input::placeholder { color: rgba(255,255,255,0.7); }
        .calculator-btn { background: rgba(255,255,255,0.2); border: none; color: white; padding: 8px 15px; border-radius: 8px; cursor: pointer; font-size: 12px; transition: all 0.3s ease; }
        .calculator-btn:hover { background: rgba(255,255,255,0.3); }
        .calculator-result { background: rgba(255,255,255,0.1); padding: 10px; border-radius: 8px; margin-top: 10px; text-align: center; font-weight: bold; }
        .transactions-section { padding: 0 20px; margin-bottom: 20px; }
        #transaction-list {}
        .transaction-item { background: white; border-radius: 12px; padding: 15px; margin-bottom: 10px; box-shadow: 0 3px 10px rgba(0,0,0,0.05); display: flex; align-items: center; border-left: 4px solid; transition: all 0.3s ease; }
        .transaction-item:hover { transform: translateX(5px); box-shadow: 0 5px 15px rgba(0,0,0,0.1); }
        .transaction-item.setor { border-left-color: #27ae60; } .transaction-item.tarik { border-left-color: #e74c3c; } .transaction-item.reward { border-left-color: #f39c12; }
        .transaction-icon { width: 45px; height: 45px; border-radius: 50%; display: flex; align-items: center; justify-content: center; margin-right: 15px; font-size: 20px; color: white; }
        .transaction-icon.setor { background: linear-gradient(135deg, #27ae60, #2ecc71); } .transaction-icon.tarik { background: linear-gradient(135deg, #e74c3c, #c0392b); } .transaction-icon.reward { background: linear-gradient(135deg, #f39c12, #e67e22); }
        .transaction-info { flex: 1; }
        .transaction-title { font-weight: 600; color: #2c3e50; margin-bottom: 3px; }
        .transaction-detail { font-size: 12px; color: #7f8c8d; margin-bottom: 2px; }
        .transaction-date { font-size: 10px; color: #95a5a6; }
        .transaction-amount { font-weight: bold; font-size: 14px; text-align: right; }
        .transaction-amount.setor { color: #27ae60; } .transaction-amount.tarik { color: #e74c3c; } .transaction-amount.reward { color: #f39c12; }
        .bottom-nav { position: fixed; bottom: 0; left: 50%; transform: translateX(-50%); width: 100%; max-width: 414px; background: white; border-top: 1px solid #e0e0e0; display: flex; padding: 10px 0; box-shadow: 0 -5px 15px rgba(0,0,0,0.1); z-index: 99; }
        .nav-item { flex: 1; text-align: center; padding: 10px; cursor: pointer; transition: all 0.3s ease; color: #7f8c8d; }
        .nav-item.active { color: #2ecc71; }
        .nav-icon { font-size: 20px; margin-bottom: 3px; }
        .nav-text { font-size: 10px; font-weight: 500; }
        .modal { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.5); z-index: 1000; backdrop-filter: blur(5px); align-items: center; justify-content: center; }
        .modal-content { position: relative; background: white; padding: 30px; border-radius: 20px; width: 90%; max-width: 350px; text-align: center; box-shadow: 0 20px 40px rgba(0,0,0,0.3); animation: zoomIn 0.3s ease-out; }
        @keyframes zoomIn { from { transform: scale(0.8); opacity: 0; } to { transform: scale(1); opacity: 1; } }
        .modal-icon { font-size: 48px; margin-bottom: 15px; }
        .modal-title { font-size: 20px; font-weight: bold; margin-bottom: 10px; color: #2c3e50; }
        .modal-text { font-size: 14px; color: #666; margin-bottom: 20px; line-height: 1.5; white-space: pre-wrap; text-align: left; }
        .modal-btn { background: linear-gradient(135deg, #2ecc71, #27ae60); color: white; border: none; padding: 12px 30px; border-radius: 25px; font-size: 14px; font-weight: 600; cursor: pointer; transition: all 0.3s ease; margin-top: 10px; width: 100%; }
        .modal-btn:hover { transform: translateY(-2px); box-shadow: 0 5px 15px rgba(46, 204, 113, 0.3); }
        .modal-form { display: flex; flex-direction: column; gap: 15px; text-align: left; }
        .modal-form label { font-size: 12px; color: #333; font-weight: 600; }
        .modal-form input, .modal-form select { padding: 10px; border: 1px solid #ddd; border-radius: 8px; font-size: 14px; width: 100%; }
        .password-wrapper { position: relative; display: flex; align-items: center; }
        .password-wrapper input { padding-right: 40px; }
        .password-toggle { position: absolute; right: 10px; background: none; border: none; cursor: pointer; font-size: 20px; color: #999; }
        .modal-btn.secondary { background: #ecf0f1; color: #2c3e50; font-weight: normal; margin-top: 0; }
        .modal-link { font-size: 12px; color: #3498db; cursor: pointer; text-align: center; margin-top: 10px; }
        .points-balance { background: #fdf3e6; border: 1px solid #f39c12; padding: 10px; border-radius: 10px; margin-bottom: 15px; }
        .points-balance span { font-weight: bold; color: #f39c12; font-size: 18px; }
        .reward-list { max-height: 250px; overflow-y: auto; text-align: left; }
        .reward-item { display: flex; align-items: center; padding: 10px; border: 1px solid #eee; border-radius: 10px; margin-bottom: 10px; }
        .reward-item-icon { font-size: 24px; margin-right: 15px; }
        .reward-item-info { flex: 1; }
        .reward-item-name { font-weight: 600; }
        .reward-item-cost { font-size: 12px; color: #e74c3c; }
        .reward-item-btn { background: #2ecc71; color: white; border: none; padding: 8px 12px; font-size: 12px; border-radius: 8px; cursor: pointer; }
        .reward-item-btn:disabled { background: #bdc3c7; cursor: not-allowed; }
        a.contact-link { display: block; background: #25D366; color: white !important; text-decoration: none; padding: 12px; border-radius: 8px; font-weight: bold; text-align: center; margin-top: 10px; }
        .modal-menu-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 15px; margin-top: 15px; }
        .profile-data-item { text-align: left; margin-bottom: 12px; font-size: 14px; }
        .profile-data-item strong { color: #2c3e50; }
    </style>
</head>
<body>
    <div class="app-container">
        <!-- Header -->
        <div class="header">
            <div class="logo-container"><div class="logo-icon">♻️</div><div class="logo-text">BANK SAMPAH ARAS</div></div>
            <div class="bank-name">Karangtaruna ARAS</div>
            <div class="location">Dusun Citambal</div>
        </div>

        <!-- User Card -->
        <div class="user-card">
            <div class="user-greeting" id="user-greeting">Selamat datang,</div>
            <div class="user-name" id="user-name">Tamu</div>
            <div class="user-stats">
                <div class="stat-item"><div class="stat-value" id="user-days">-</div><div class="stat-label">Hari Aktif</div></div>
                <div class="stat-item"><div class="stat-value" id="user-waste">-</div><div class="stat-label">Total Sampah</div></div>
                <div class="stat-item"><div class="stat-value">⭐ 4.8</div><div class="stat-label">®™ rung's</div></div>
            </div>
        </div>

        <!-- Balance Section -->
        <div class="balance-section">
            <div class="balance-card">
                <div class="balance-label">Saldo Tabungan Sampah</div>
                <div class="balance-amount" id="balance">Rp 0</div>
                <div class="balance-actions">
                    <button class="balance-btn" onclick="showTransfer()">💸 Transfer</button>
                    <button class="balance-btn" onclick="showRincianSaldo()">🧾 Rincian Saldo</button>
                    <button class="balance-btn" onclick="showIsiSaldo()">➕ Cara Isi Saldo</button>
                </div>
            </div>
        </div>

        <!-- Features Section (DIUBAH) -->
        <div class="features-section">
            <div class="section-title">Layanan Bank Sampah</div>
            <div class="features-grid">
                <div class="feature-item" onclick="showEventAndReward()"><div class="feature-icon">⭐</div><div class="feature-text">Event & Reward</div></div>
                <div class="feature-item" onclick="showHarga()"><div class="feature-icon">💰</div><div class="feature-text">Harga Sampah</div></div>
                <div class="feature-item" onclick="showJadwal()"><div class="feature-icon">📅</div><div class="feature-text">Jadwal Pickup</div></div>
                <div class="feature-item" onclick="showPanduan()"><div class="feature-icon">📖</div><div class="feature-text">Panduan</div></div>
                <div class="feature-item" onclick="showLeaderboard()"><div class="feature-icon">🏆</div><div class="feature-text">Leaderboard</div></div>
                <div class="feature-item" onclick="showCnuMenu()"><div class="feature-icon">🏞️</div><div class="feature-text">CNU</div></div>
            </div>
        </div>
        
        <!-- Sisa Konten -->
        <div class="waste-calculator">
            <div class="calculator-title">Kalkulator Harga Sampah</div>
            <div class="calculator-row"><select class="calculator-input" id="wasteTypeCalc"><option value="" data-price="0">Pilih Jenis Sampah</option></select></div>
            <div class="calculator-row"><input type="number" class="calculator-input" id="wasteWeight" placeholder="Berat (kg)" step="0.1"><button class="calculator-btn" onclick="calculateWaste()">Hitung</button></div>
            <div class="calculator-result" id="calculatorResult" style="display: none;">Estimasi Harga: <span id="estimatedPrice"></span></div>
        </div>
        <div class="transactions-section">
            <div class="section-title">Aktivitas Terbaru</div>
            <div id="transaction-list"><p style="text-align:center; color:#999;">Login untuk melihat riwayat transaksi.</p></div>
        </div>

        <!-- Bottom Nav (DIUBAH) -->
        <div class="bottom-nav">
            <div class="nav-item active" onclick="setActiveNav(this)"><div class="nav-icon">🏠</div><div class="nav-text">Beranda</div></div>
            <div class="nav-item" onclick="setActiveNav(this); showContactAdmin()"><div class="nav-icon">💬</div><div class="nav-text">Hubungi Admin</div></div>
            <div class="nav-item" onclick="setActiveNav(this); showActivityHistory()"><div class="nav-icon">📊</div><div class="nav-text">Riwayat</div></div>
            <div class="nav-item" onclick="setActiveNav(this); showProfil()"><div class="nav-icon">👤</div><div class="nav-text">Profil</div></div>
            <div class="nav-item" id="auth-nav-item" onclick="handleAuthClick()"><div class="nav-icon">🔑</div><div class="nav-text">Login</div></div>
        </div>
    </div>
    
    <!-- Modal (Pop-up) -->
    <div id="modal" class="modal" onclick="closeModal()">
        <div class="modal-content" onclick="event.stopPropagation()">
            <div class="modal-icon" id="modalIcon">♻️</div>
            <h3 class="modal-title" id="modalTitle"></h3>
            <div id="modalBody"></div>
            <button class="modal-btn" id="modalBtn" onclick="closeModal()">Tutup</button>
        </div>
    </div>

    <script type="module">
    // ====================================================================
    // KONEKSI DAN INISIALISASI FIREBASE
    // ====================================================================
    import { initializeApp } from "https://www.gstatic.com/firebasejs/9.22.1/firebase-app.js";
    import { getAnalytics } from "https://www.gstatic.com/firebasejs/9.22.1/firebase-analytics.js";
    import { getAuth, onAuthStateChanged, createUserWithEmailAndPassword, signInWithEmailAndPassword, signOut, sendPasswordResetEmail } from "https://www.gstatic.com/firebasejs/9.22.1/firebase-auth.js";
    import { getFirestore, doc, setDoc, getDoc, serverTimestamp } from "https://www.gstatic.com/firebasejs/9.22.1/firebase-firestore.js";

    const firebaseConfig = {
      apiKey: "AIzaSyCxAYtwTyqgal3LkMmoO7k2AZG4PbSKTnY",
      authDomain: "bank-sampah-aras.firebaseapp.com",
      projectId: "bank-sampah-aras",
      storageBucket: "bank-sampah-aras.firebasestorage.app",
      messagingSenderId: "1038502551432",
      appId: "1:1038502551432:web:e3bcd68910f0669be0243d",
      measurementId: "G-365NW7GG75"
    };

    const app = initializeApp(firebaseConfig);
    const analytics = getAnalytics(app);
    const auth = getAuth(app);
    const db = getFirestore(app);
    console.log("Firebase successfully initialized!");

    // ====================================================================
    // STATE MANAGEMENT & DATA GLOBAL
    // ====================================================================
    let currentUserData = null; // Akan diisi dengan data pengguna yang login
    const staticData = {
        wastePrices: { "Botol Plastik": 2500, "Kardus": 2000, "Kertas": 1500, "Logam": 5000, "Kaca": 500, "Campuran": 2000, },
        rewards: [
            { id: 'pulsa10k', name: 'Pulsa 10rb', cost: 11000, icon: '📱' },
            { id: 'minyak1l', name: 'Minyak Goreng 1L', cost: 25000, icon: '🍳' },
            { id: 'sembako', name: 'Paket Sembako', cost: 50000, icon: '🛍️' },
            { id: 'voucher25k', name: 'Voucher Belanja 25rb', cost: 25000, icon: '🛒' }
        ],
        guestData: {
            name: "Tamu", activeDays: 0, totalWasteKg: 0, balance: 0, points: 0, transactions: []
        }
    };

    // ====================================================================
    // FUNGSI UTAMA & AUTHENTICATION
    // ====================================================================
    onAuthStateChanged(auth, async (user) => {
        if (user) {
            // Pengguna sedang login
            const userDocRef = doc(db, "users", user.uid);
            const userDocSnap = await getDoc(userDocRef);
            if (userDocSnap.exists()) {
                currentUserData = { uid: user.uid, email: user.email, ...userDocSnap.data() };
            } else {
                // Dokumen tidak ditemukan, mungkin pengguna baru atau data error
                currentUserData = { uid: user.uid, email: user.email, ...staticData.guestData, name: "Pengguna Baru" };
            }
            console.log("User logged in:", currentUserData.name);
            updateUIForAuthState(true);
            renderDashboard(currentUserData);
        } else {
            // Pengguna logout
            currentUserData = null;
            console.log("User logged out.");
            updateUIForAuthState(false);
            renderDashboard(staticData.guestData);
        }
    });

    function updateUIForAuthState(isLoggedIn) {
        const authNavItem = document.getElementById('auth-nav-item');
        const authNavIcon = authNavItem.querySelector('.nav-icon');
        const authNavText = authNavItem.querySelector('.nav-text');

        if (isLoggedIn) {
            authNavIcon.textContent = '🔓';
            authNavText.textContent = 'Logout';
            document.getElementById('user-greeting').textContent = 'Selamat datang,';
        } else {
            authNavIcon.textContent = '🔑';
            authNavText.textContent = 'Login';
            document.getElementById('user-greeting').textContent = 'Silakan login';
            document.getElementById('transaction-list').innerHTML = '<p style="text-align:center; color:#999;">Login untuk melihat riwayat transaksi.</p>';
        }
    }
    
    window.handleAuthClick = () => {
        if (currentUserData) {
            signOut(auth).then(() => {
                alert("Anda berhasil logout.");
            }).catch((error) => {
                alert("Gagal logout: " + error.message);
            });
        } else {
            showLoginForm();
        }
    }

    // ====================================================================
    // FUNGSI RENDER DASHBOARD
    // ====================================================================
    function renderDashboard(data) {
        document.getElementById('user-name').textContent = data.name;
        document.getElementById('user-days').textContent = data.activeDays || '-';
        document.getElementById('user-waste').textContent = `${data.totalWasteKg || 0}kg`;
        document.getElementById('balance').textContent = `Rp ${(data.balance || 0).toLocaleString('id-ID')}`;
        
        const transactionList = document.getElementById('transaction-list');
        transactionList.innerHTML = '';
        if (data.transactions && data.transactions.length > 0) {
            data.transactions.forEach(tx => {
                const amountClass = tx.type;
                const amountSign = tx.amount > 0 ? '+' : '';
                const icon = tx.type === 'setor' ? '📥' : (tx.type === 'tarik' ? '📤' : '🎁');
                const txItemHTML = `<div class="transaction-item ${tx.type}"><div class="transaction-icon ${tx.type}">${icon}</div><div class="transaction-info"><div class="transaction-title">${tx.title}</div><div class="transaction-detail">${tx.detail}</div><div class="transaction-date">${tx.date}</div></div><div class="transaction-amount ${amountClass}">${amountSign}Rp ${Math.abs(tx.amount).toLocaleString('id-ID')}</div></div>`;
                transactionList.insertAdjacentHTML('beforeend', txItemHTML);
            });
        } else if (currentUserData) {
            transactionList.innerHTML = '<p style="text-align:center; color:#999;">Belum ada transaksi.</p>';
        }

        const wasteTypeSelect = document.getElementById('wasteTypeCalc');
        if (wasteTypeSelect.options.length <= 1) { // Hanya isi jika belum ada
            for (const [name, price] of Object.entries(staticData.wastePrices)) {
                wasteTypeSelect.insertAdjacentHTML('beforeend', `<option value="${name}" data-price="${price}">${name} (Rp ${price.toLocaleString('id-ID')}/kg)</option>`);
            }
        }
    }

    // ====================================================================
    // FUNGSI MODAL
    // ====================================================================
    const modal = document.getElementById('modal');
    const modalIcon = document.getElementById('modalIcon');
    const modalTitle = document.getElementById('modalTitle');
    const modalBody = document.getElementById('modalBody');
    const modalBtn = document.getElementById('modalBtn');
    
    window.showModal = (icon, title, content, buttonText = "Tutup", buttonAction = closeModal) => {
        modalIcon.textContent = icon;
        modalTitle.textContent = title;
        modalBody.innerHTML = content;
        modalBtn.textContent = buttonText;
        modalBtn.onclick = buttonAction;
        modal.style.display = 'flex';
    }
    window.closeModal = () => { modal.style.display = 'none'; }

    // ====================================================================
    // FUNGSI LOGIN, REGISTRASI, & PROFIL
    // ====================================================================
    window.showLoginForm = () => {
        const formHTML = `
            <div class="modal-form">
                <input type="email" id="loginEmail" placeholder="Email" required>
                <div class="password-wrapper">
                    <input type="password" id="loginPassword" placeholder="Password" required>
                    <button class="password-toggle" onclick="togglePasswordVisibility('loginPassword')">👁️</button>
                </div>
                <button class="modal-btn" onclick="handleLogin()">Login</button>
                <button class="modal-btn secondary" onclick="showRegistrationForm()">Belum punya akun? Daftar</button>
            </div>
        `;
        showModal('🔑', 'Login Pengguna', formHTML);
        modalBtn.style.display = 'none';
    }

    window.handleLogin = () => {
        const email = document.getElementById('loginEmail').value;
        const password = document.getElementById('loginPassword').value;
        if (!email || !password) {
            alert("Email dan password harus diisi.");
            return;
        }
        signInWithEmailAndPassword(auth, email, password)
            .then((userCredential) => {
                closeModal();
                alert(`Selamat datang kembali!`);
            })
            .catch((error) => {
                alert("Login Gagal: " + error.message);
            });
    }

    window.showRegistrationForm = () => {
        const formHTML = `
            <div class="modal-form">
                <label for="regName">Nama Lengkap</label>
                <input type="text" id="regName" placeholder="Contoh: Budi Santoso" required>
                
                <label for="regEmail">Email</label>
                <input type="email" id="regEmail" placeholder="contoh@email.com" required>
                
                <label for="regPassword">Password</label>
                <div class="password-wrapper">
                    <input type="password" id="regPassword" placeholder="Minimal 6 karakter" required>
                    <button class="password-toggle" onclick="togglePasswordVisibility('regPassword')">👁️</button>
                </div>
                
                <label for="regBirthdate">Tanggal Lahir</label>
                <input type="date" id="regBirthdate" required>
                
                <label for="regAddress">Alamat</label>
                <input type="text" id="regAddress" placeholder="Contoh: Dusun Citambal RT 01/RW 01" required>
                
                <button class="modal-btn" onclick="handleRegistration()">Daftar Sekarang</button>
                <button class="modal-btn secondary" onclick="showLoginForm()">Sudah punya akun? Login</button>
            </div>
        `;
        showModal('📝', 'Daftar Akun Baru', formHTML);
        modalBtn.style.display = 'none';
    };

    window.handleRegistration = () => {
        const name = document.getElementById('regName').value;
        const email = document.getElementById('regEmail').value;
        const password = document.getElementById('regPassword').value;
        const birthdate = document.getElementById('regBirthdate').value;
        const address = document.getElementById('regAddress').value;

        if (!name || !email || !password || !birthdate || !address) {
            alert("Semua kolom wajib diisi!");
            return;
        }

        createUserWithEmailAndPassword(auth, email, password)
            .then(async (userCredential) => {
                const user = userCredential.user;
                // Simpan data tambahan ke Firestore
                await setDoc(doc(db, "users", user.uid), {
                    name: name,
                    email: email,
                    birthdate: birthdate,
                    address: address,
                    role: 'member',
                    balance: 0,
                    points: 0,
                    activeDays: 0,
                    totalWasteKg: 0,
                    transactions: [],
                    createdAt: serverTimestamp()
                });
                closeModal();
                alert("Pendaftaran berhasil! Anda akan otomatis login.");
            })
            .catch((error) => {
                alert("Pendaftaran Gagal: " + error.message);
            });
    };

    window.showProfil = () => {
        if (!currentUserData) {
            showModal('👤', 'Profil Pengguna', '<p class="modal-text">Silakan login untuk melihat profil Anda.</p>');
            return;
        }
        const profileHTML = `
            <div class="profile-data-item"><strong>Nama:</strong> ${currentUserData.name}</div>
            <div class="profile-data-item"><strong>Email:</strong> ${currentUserData.email}</div>
            <div class="profile-data-item"><strong>Tgl Lahir:</strong> ${currentUserData.birthdate}</div>
            <div class="profile-data-item"><strong>Alamat:</strong> ${currentUserData.address}</div>
            <button class="modal-btn secondary" onclick="handleChangePassword()" style="margin-top: 20px;">Ganti Password</button>
        `;
        showModal('👤', 'Profil Pengguna', profileHTML);
    }
    
    window.handleChangePassword = () => {
        if (!currentUserData) return;
        sendPasswordResetEmail(auth, currentUserData.email)
            .then(() => {
                alert(`Email untuk reset password telah dikirim ke ${currentUserData.email}. Silakan cek kotak masuk Anda.`);
            })
            .catch((error) => {
                alert("Gagal mengirim email: " + error.message);
            });
    };


    // ====================================================================
    // FUNGSI FITUR-FITUR BARU
    // ====================================================================

    window.showEventAndReward = () => {
        const contentHTML = `
            <p class="modal-text">Pilih layanan yang ingin Anda lihat.</p>
            <div class="modal-menu-grid">
                <div class="feature-item" onclick="alert('Belum ada event saat ini. Pantau terus ya!')">
                    <div class="feature-icon">🎉</div>
                    <div class="feature-text">Lihat Event</div>
                </div>
                <div class="feature-item" onclick="showTukarPoin()">
                    <div class="feature-icon">🎁</div>
                    <div class="feature-text">Tukar Poin</div>
                </div>
            </div>
        `;
        showModal('⭐', 'Event & Reward', contentHTML, 'Tutup');
    }

    window.showCnuMenu = () => {
        const contentHTML = `
            <p class="modal-text">Citambal Nu Urang (CNU) adalah program pemberdayaan masyarakat lokal. Pilih layanan yang Anda butuhkan.</p>
            <div class="modal-menu-grid">
                <div class="feature-item" onclick="showUmkmList()">
                    <div class="feature-icon">🏪</div>
                    <div class="feature-text">UMKM</div>
                </div>
                <div class="feature-item" onclick="showAirBersihMenu()">
                    <div class="feature-icon">💧</div>
                    <div class="feature-text">Air Bersih</div>
                </div>
            </div>
        `;
        showModal('🏞️', 'Citambal Nu Urang', contentHTML, 'Tutup');
    };

    window.showUmkmList = () => {
        const umkmHTML = `
            <div class="modal-text">
                Dukung usaha lokal kita! Hubungi langsung untuk pemesanan.<br><br>
                <strong>1. Warung Seblak Teh Popon</strong><br>
                Produk: Seblak, Baso Aci<br>
                Telp: <a href="tel:081234567890">0812-3456-7890</a><br><br>
                <strong>2. Rengginang Mang Ujang</strong><br>
                Produk: Rengginang Aneka Rasa<br>
                Telp: <a href="tel:089876543210">0898-7654-3210</a><br><br>
                <strong>3. Keripik Kaca Bi Iis</strong><br>
                Produk: Keripik Kaca Pedas<br>
                Telp: <a href="tel:085567891234">0855-6789-1234</a>
            </div>
        `;
        showModal('🏪', 'Daftar UMKM Citambal', umkmHTML, 'Kembali', showCnuMenu);
    };

    window.showAirBersihMenu = () => {
        const airHTML = `
            <p class="modal-text">Layanan pengelolaan Air Bersih Gunung Tumpeng. Pembayaran bisa menggunakan saldo tabungan sampah.</p>
            <button class="modal-btn" onclick="alert('Fitur Pendaftaran Air Bersih akan segera tersedia.')">📝 Daftar Sambungan Baru</button>
            <button class="modal-btn" onclick="alert('Fitur Bayar Tagihan Air akan segera tersedia.')">💳 Bayar Tagihan Air</button>
            <button class="modal-btn secondary" onclick="alert('Fitur Riwayat Pembayaran akan segera tersedia.')">📊 Lihat Riwayat</button>
        `;
        showModal('💧', 'Air Bersih Gunung Tumpeng', airHTML, 'Kembali', showCnuMenu);
    };
    
    // ====================================================================
    // FUNGSI LAINNYA (Telah Disesuaikan)
    // ====================================================================
    window.showTukarPoin = () => {
        if (!currentUserData) { alert("Silakan login untuk menukar poin."); return; }
        
        let rewardItemsHTML = '';
        staticData.rewards.forEach(reward => {
            const canRedeem = currentUserData.points >= reward.cost;
            rewardItemsHTML += `<div class="reward-item"><div class="reward-item-icon">${reward.icon}</div><div class="reward-item-info"><div class="reward-item-name">${reward.name}</div><div class="reward-item-cost">${reward.cost.toLocaleString('id-ID')} Poin</div></div><button class="reward-item-btn" onclick="processRedeem('${reward.id}')" ${!canRedeem ? 'disabled' : ''}>Tukar</button></div>`;
        });

        const tukarPoinHTML = `<div class="points-balance">Poin Anda Saat Ini: <br> <span id="current-points">${currentUserData.points.toLocaleString('id-ID')} Poin</span></div><div class="reward-list">${rewardItemsHTML}</div>`;
        showModal('🎁', 'Tukar Poin Reward', tukarPoinHTML, 'Selesai');
    }

    window.processRedeem = (rewardId) => {
        // Logika ini perlu diintegrasikan dengan update data ke Firestore nantinya
        alert("Fitur penukaran poin sedang dalam pengembangan untuk terhubung ke database.");
    }
    
    window.togglePasswordVisibility = (inputId) => {
        const passwordInput = document.getElementById(inputId);
        const toggleButton = passwordInput.nextElementSibling;
        if (passwordInput.type === 'password') {
            passwordInput.type = 'text';
            toggleButton.textContent = '🙈';
        } else {
            passwordInput.type = 'password';
            toggleButton.textContent = '👁️';
        }
    }

    window.calculateWaste=()=>{const t=document.getElementById("wasteTypeCalc"),e=document.getElementById("wasteWeight"),o=document.getElementById("calculatorResult"),a=document.getElementById("estimatedPrice"),d=t.options[t.selectedIndex],n=parseFloat(d.getAttribute("data-price")),i=parseFloat(e.value);if(o.style.display="block",0===n||isNaN(i)||i<=0)return o.style.background="rgba(231, 76, 60, 0.5)",void(a.textContent="Pilih jenis & isi berat");const s=n*i;o.style.background="rgba(255,255,255,0.1)",a.textContent=`Rp ${s.toLocaleString("id-ID")}`}
    window.setActiveNav=(el)=>{document.querySelectorAll(".nav-item").forEach(item=>item.classList.remove("active"));el.classList.add("active");}
    window.showContactAdmin=()=>{const t=`<p class="modal-text">Jika Anda memiliki pertanyaan atau kendala, silakan hubungi admin kami melalui WhatsApp.</p><a href="https://wa.me/6281322355056?text=Halo%20Admin%20Bank%20Sampah%20ARAS" target="_blank" class="contact-link">💬 Hubungi via WhatsApp</a><p class="modal-text" style="font-size: 12px; text-align: center; margin-top: 15px;">Jam Operasional Admin: 08:00 - 17:00 WIB</p>`;showModal("📞","Hubungi Admin",t)}
    window.showTransfer=()=>{if(!currentUserData){alert("Silakan login untuk melakukan transfer.");return};showModal("💸","Transfer & Tarik Saldo",'<p class="modal-text">Anda dapat mentransfer saldo tabungan sampah Anda ke rekening bank atau menariknya secara tunai di lokasi Bank Sampah ARAS. Hubungi petugas untuk melakukan transaksi.</p>')}
    window.showRincianSaldo=()=>{if(!currentUserData){alert("Silakan login untuk melihat rincian saldo.");return};let t="Ini adalah catatan keuangan lengkap Anda:\n\n";(currentUserData.transactions||[]).forEach(e=>{const o=e.amount>0?"+":"";t+=`• (${e.type}) ${o}Rp ${Math.abs(e.amount).toLocaleString("id-ID")} - ${e.title}\n`}),showModal("🧾","Rincian Saldo (Mutasi Keuangan)",`<p class="modal-text">${t}</p>`)}
    window.showIsiSaldo=()=>{showModal("➕","Cara Mengisi Saldo",'<p class="modal-text">Saldo Anda bertambah setiap kali Anda menyetorkan sampah yang memiliki nilai jual. Semakin banyak sampah yang Anda setor, semakin besar saldo tabungan Anda!</p>')}
    window.showActivityHistory=()=>{if(!currentUserData){alert("Silakan login untuk melihat riwayat aktivitas.");return};showModal("📊","Riwayat Aktivitas",'<p class="modal-text">Fitur riwayat aktivitas lengkap sedang dalam pengembangan.</p>')}
    window.showHarga=()=>{let t="Daftar harga sampah saat ini (per kg):\n\n";for(const[e,o]of Object.entries(staticData.wastePrices))t+=`• ${e}: Rp ${o.toLocaleString("id-ID")}\n`;t+="\n*Harga dapat berubah sewaktu-waktu.",showModal("💰","Daftar Harga Sampah",`<p class="modal-text">${t}</p>`)}
    window.showJadwal=()=>{showModal("📅","Jadwal Operasional",'<p class="modal-text">Bank Sampah ARAS beroperasi pada:\n\n• Hari: Selasa & Jumat\n• Jam: 08:00 - 16:00 WIB\n\nUntuk permintaan pickup, hubungi pengurus H-1.</p>')}
    window.showPanduan=()=>{showModal("📖","Panduan Memilah Sampah",'<p class="modal-text">• KERTAS: Koran, HVS, majalah.\n• PLASTIK: Botol, gelas, & kresek.\n• LOGAM: Kaleng minuman/makanan.\n• KACA: Botol sirup, botol kecap.</p>')}
    window.showLeaderboard=()=>{showModal("🏆","Leaderboard Nasabah",'<p class="modal-text">Peringkat setoran terbanyak bulan ini:\n\n1. Bpk. Sutisna (45.2 kg)\n2. Ibu Aisyah (41.8 kg)\n3. (Data Anda akan muncul di sini setelah login)\n\nTerus tingkatkan setoran Anda!</p>')}
    
    // ====================================================================
    // INISIALISASI APLIKASI
    // ====================================================================
    document.addEventListener('DOMContentLoaded', () => {
        renderDashboard(staticData.guestData); // Tampilkan data tamu saat pertama kali dimuat
    });
    </script>
</body>
</html>
