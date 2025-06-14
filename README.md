<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bank Sampah ARAS - Dompet Digital</title>
    <link rel="icon" href="img/favicon.png" type="image/png">
    <style>
        /* === CSS (Ada penambahan .notification) === */
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
        .modal-content { position: relative; background: white; padding: 30px; border-radius: 20px; width: 90%; max-width: 350px; text-align: center; box-shadow: 0 20px 40px rgba(0,0,0,0.3); animation: zoomIn 0.3s ease-out; max-height: 90vh; overflow-y: auto; }
        @keyframes zoomIn { from { transform: scale(0.8); opacity: 0; } to { transform: scale(1); opacity: 1; } }
        .modal-icon { font-size: 48px; margin-bottom: 15px; }
        .modal-title { font-size: 20px; font-weight: bold; margin-bottom: 10px; color: #2c3e50; }
        .modal-text { font-size: 14px; color: #666; margin-bottom: 20px; line-height: 1.5; white-space: pre-wrap; text-align: left; }
        .modal-btn { background: linear-gradient(135deg, #2ecc71, #27ae60); color: white; border: none; padding: 12px 30px; border-radius: 25px; font-size: 14px; font-weight: 600; cursor: pointer; transition: all 0.3s ease; margin-top: 10px; width: 100%; }
        .modal-btn:hover { transform: translateY(-2px); box-shadow: 0 5px 15px rgba(46, 204, 113, 0.3); }
        .modal-btn.secondary { background: #ecf0f1; color: #2c3e50; font-weight: normal; margin-top: 0; }
        .modal-link { font-size: 12px; color: #3498db; cursor: pointer; text-align: center; margin-top: 10px; }
        .modal-form { display: flex; flex-direction: column; gap: 15px; text-align: left; }
        .modal-form label { font-size: 12px; color: #333; font-weight: 600; }
        .modal-form input, .modal-form select, .modal-form textarea { padding: 10px; border: 1px solid #ddd; border-radius: 8px; font-size: 14px; width: 100%; }
        .password-wrapper { position: relative; display: flex; align-items: center; }
        .password-wrapper input { padding-right: 40px; }
        .password-toggle { position: absolute; right: 10px; background: none; border: none; cursor: pointer; font-size: 20px; color: #999; }
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
        .leaderboard-list { list-style: none; padding: 0; margin: 0; text-align: left; }
        .leaderboard-item { display: flex; align-items: center; padding: 12px; margin-bottom: 8px; background: #f0f8ff; border-radius: 10px; box-shadow: 0 2px 8px rgba(0,0,0,0.05); transition: transform 0.2s ease; }
        .leaderboard-item:hover { transform: translateY(-2px); }
        .leaderboard-rank { font-size: 18px; font-weight: bold; color: #2ecc71; width: 30px; text-align: center; margin-right: 15px; }
        .leaderboard-name { font-weight: 600; color: #333; flex-grow: 1; }
        .leaderboard-value { font-weight: bold; color: #f39c12; }
        .leaderboard-note { font-size: 12px; color: #7f8c8d; text-align: center; margin-top: 15px; }
        .loading-spinner { border: 4px solid rgba(0, 0, 0, 0.1); border-left-color: #2ecc71; border-radius: 50%; width: 24px; height: 24px; animation: spin 1s linear infinite; margin: 10px auto; }
        @keyframes spin { to { transform: rotate(360deg); } }
        .admin-form-item { margin-bottom: 15px; border: 1px solid #eee; padding: 10px; border-radius: 8px; background: #f9f9f9; }
        .admin-form-item input, .admin-form-item select { margin-top: 5px; }
        .admin-form-actions { display: flex; gap: 10px; margin-top: 10px; }
        .admin-form-actions button { flex: 1; }
        .admin-list-item { display: flex; justify-content: space-between; align-items: center; padding: 10px 0; border-bottom: 1px solid #eee; }
        .admin-list-item:last-child { border-bottom: none; }
        .admin-list-item-name { font-weight: 600; flex-grow: 1; }
        .admin-list-item-value { color: #666; margin-right: 10px; }
        .admin-list-item-actions button { background: #3498db; color: white; border: none; padding: 5px 10px; border-radius: 5px; cursor: pointer; font-size: 12px; }
        .admin-list-item-actions button.delete { background: #e74c3c; }
        
        /* >>> PERUBAHAN CSS: Tambahan untuk Notifikasi Toast <<< */
        .notification-toast {
            position: fixed;
            top: 20px;
            left: 50%;
            transform: translate(-50%, -150%);
            padding: 12px 25px;
            border-radius: 25px;
            color: white;
            font-weight: 600;
            z-index: 2000;
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
            opacity: 0;
            transition: all 0.4s ease-in-out;
        }
        .notification-toast.show {
            transform: translate(-50%, 0);
            opacity: 1;
        }
        .notification-toast.success { background: linear-gradient(135deg, #2ecc71, #27ae60); }
        .notification-toast.error { background: linear-gradient(135deg, #e74c3c, #c0392b); }
    </style>
</head>
<body>
    <div class="app-container">
        <!-- Konten HTML (Tidak berubah) -->
        <div class="header">
            <div class="logo-container"><div class="logo-icon">♻️</div><div class="logo-text">BANK SAMPAH ARAS</div></div>
            <div class="bank-name">Karangtaruna ARAS</div>
            <div class="location">Dusun Citambal</div>
        </div>
        <div class="user-card">
            <div class="user-greeting" id="user-greeting">Selamat datang,</div>
            <div class="user-name" id="user-name">Tamu</div>
            <div class="user-stats">
                <div class="stat-item"><div class="stat-value" id="user-days">-</div><div class="stat-label">Hari Aktif</div></div>
                <div class="stat-item"><div class="stat-value" id="user-waste">-</div><div class="stat-label">Total Sampah</div></div>
                <div class="stat-item"><div class="stat-value">⭐ 4.8</div><div class="stat-label">®™ rung's</div></div>
            </div>
        </div>
        <div class="balance-section">
            <div class="balance-card">
                <div class="balance-label">Saldo Tabungan Sampah</div>
                <div class="balance-amount" id="balance">Rp 0</div>
                <div class="balance-actions">
                    <button class="balance-btn" onclick="showTransfer()">💸 Transfer</button>
                    <button class="balance-btn" onclick="showSetorSampah()">🗑️ Setor Sampah</button>
                    <button class="balance-btn" onclick="showTarikSaldo()"> 💵 Tarik Saldo</button>
                </div>
            </div>
        </div>
        <div class="features-section">
            <div class="section-title">Layanan Bank Sampah</div>
            <div class="features-grid">
                <div class="feature-item" onclick="showEventAndReward()"><div class="feature-icon">⭐</div><div class="feature-text">Event & Reward</div></div>
                <div class="feature-item" onclick="showHarga()"><div class="feature-icon">💰</div><div class="feature-text">Harga Sampah</div></div>
                <div class="feature-item" onclick="showJadwal()"><div class="feature-icon">📅</div><div class="feature-text">Jadwal Pickup</div></div>
                <div class="feature-item" onclick="showPanduan()"><div class="feature-icon">📖</div><div class="feature-text">Panduan</div></div>
                <div class="feature-item" onclick="showLeaderboard()"><div class="feature-icon">🏆</div><div class="feature-text">Leaderboard</div></div>
                <div class="feature-item" onclick="showCnuMenu()"><div class="feature-icon">🏞️</div><div class="feature-text">CNU</div></div>
                <div class="feature-item" id="admin-operator-tools" style="display: none;" onclick="showAdminOperatorPanel()">
                    <div class="feature-icon">⚙️</div><div class="feature-text">Admin/Operator</div>
                </div>
            </div>
        </div>
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
    
    <!-- >>> PERUBAHAN HTML: Tambahan untuk Notifikasi Toast <<< -->
    <div id="notification-toast" class="notification-toast"></div>

    <script type="module">
    // ====================================================================
    // KONEKSI DAN INISIALISASI FIREBASE (Sudah dengan App Check)
    // ====================================================================
    import { initializeApp } from "https://www.gstatic.com/firebasejs/9.22.1/firebase-app.js";
    import { initializeAppCheck, ReCaptchaV3Provider } from "https://www.gstatic.com/firebasejs/9.22.1/firebase-app-check.js";
    import { getAnalytics } from "https://www.gstatic.com/firebasejs/9.22.1/firebase-analytics.js";
    import { getAuth, onAuthStateChanged, createUserWithEmailAndPassword, signInWithEmailAndPassword, signOut, sendPasswordResetEmail } from "https://www.gstatic.com/firebasejs/9.22.1/firebase-auth.js";
    import { getFirestore, doc, setDoc, updateDoc, arrayUnion, arrayRemove, serverTimestamp, onSnapshot, collection, query, orderBy, limit, getDocs, deleteDoc, addDoc, getDoc } from "https://www.gstatic.com/firebasejs/9.22.1/firebase-firestore.js"; 

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
    
    const appCheck = initializeAppCheck(app, {
      provider: new ReCaptchaV3Provider('6LfqvQYqAAAAAEH1T7Jj3aD0aY3o6e4o3K3D6B5f'), // Ganti dengan Site Key Anda jika berbeda
      isTokenAutoRefreshEnabled: true
    });
    
    const analytics = getAnalytics(app);
    const auth = getAuth(app);
    const db = getFirestore(app);
    console.log("Firebase & App Check successfully initialized!");

    // ====================================================================
    // STATE MANAGEMENT & DATA GLOBAL
    // ====================================================================
    let wastePrices = {}; 
    let pointsPerKg = 0;
    let rewards = []; 
    const guestData = { name: "Tamu", activeDays: 0, totalWasteKg: 0, balance: 0, points: 0, transactions: [], role: 'guest' };
    let currentUserData = guestData; 
    let unsubscribeFromUserData = null;

    // ====================================================================
    // HELPER FUNCTIONS (Fungsi Pembantu)
    // ====================================================================
    
    // >>> PERUBAHAN: Fungsi showNotification baru <<<
    function showNotification(message, type = 'success') {
        const notification = document.getElementById('notification-toast');
        if (!notification) return;
        notification.textContent = message;
        notification.className = `notification-toast ${type}`;
        notification.classList.add('show');
        setTimeout(() => {
            notification.classList.remove('show');
        }, 3000);
    }

    function formatDate(date) { /* ... (kode sama) ... */ if(!date)return"-";if(date.toDate)date=date.toDate();else if(!(date instanceof Date))date=new Date(date);return date.toLocaleDateString("id-ID",{year:"numeric",month:"short",day:"numeric",hour:"2-digit",minute:"2-digit"}) }
    function isSameDay(d1, d2) { /* ... (kode sama) ... */ if(!d1||!d2)return!1;if(d1.toDate)d1=d1.toDate();if(d2.toDate)d2=d2.toDate();return d1.getFullYear()===d2.getFullYear()&&d1.getMonth()===d2.getMonth()&&d1.getDate()===d2.getDate() }
    function createModal(icon, title, content, buttonText = "Tutup", buttonAction = closeModal) { /* ... (kode sama) ... */ document.getElementById("modalIcon").textContent=icon;document.getElementById("modalTitle").textContent=title;document.getElementById("modalBody").innerHTML=content;document.getElementById("modalBtn").textContent=buttonText;document.getElementById("modalBtn").onclick=buttonAction;document.getElementById("modal").style.display="flex" }
    window.closeModal = () => { document.getElementById('modal').style.display = 'none'; }
    function showLoading(elementId) { /* ... (kode sama) ... */ const e=document.getElementById(elementId);e&&(e.innerHTML='<div class="loading-spinner"></div>',e.disabled=!0) }
    function hideLoading(elementId, originalContent) { /* ... (kode sama) ... */ const e=document.getElementById(elementId);e&&originalContent&&(e.innerHTML=originalContent,e.disabled=!1) }
    async function fetchAppSettings() { /* ... (kode sama, tapi alert diganti) ... */ try{const e=await getDoc(doc(db,"settings","app_config"));if(e.exists()){const t=e.data();wastePrices=t.wastePrices||{},pointsPerKg=t.pointsPerKg||100,console.log("App settings fetched:",wastePrices,pointsPerKg)}else{console.warn("App config document 'settings/app_config' not found. Initializing with default values.");const e={ "Botol Plastik": 2500, "Kardus": 2000, "Kertas": 1500, "Logam": 5000, "Kaca": 500, "Campuran": 2000 };await setDoc(doc(db,"settings","app_config"),{wastePrices:e,pointsPerKg:100,lastUpdated:serverTimestamp()}),wastePrices=e,pointsPerKg=100}renderWasteTypeOptions()}catch(e){console.error("Error fetching app settings:",e),showNotification("Gagal memuat pengaturan aplikasi: "+e.message,"error")} }
    async function fetchRewards() { /* ... (kode sama, tapi alert diganti) ... */ try{const e=await getDocs(query(collection(db,"rewards"),orderBy("cost","asc")));if(rewards=[],!e.empty)e.forEach(e=>{rewards.push({id:e.id,...e.data()})}),console.log("Rewards fetched:",rewards);else{console.warn("Rewards collection is empty. Initializing default rewards.");const e=[{name:"Pulsa 10rb",cost:11e3,icon:"\ud83d\udcf1"},{name:"Minyak Goreng 1L",cost:25e3,icon:"\ud83c\udf73"},{name:"Paket Sembako",cost:5e4,icon:"\ud83d\udecd\ufe0f"},{name:"Voucher Belanja 25rb",cost:25e3,icon:"\ud83d\uded2"}];for(const t of e)await addDoc(collection(db,"rewards"),t);const t=await getDocs(query(collection(db,"rewards"),orderBy("cost","asc")));t.forEach(e=>{rewards.push({id:e.id,...e.data()})})}}catch(e){console.error("Error fetching rewards:",e),showNotification("Gagal memuat data reward: "+e.message,"error")} }
    
    // ... (Sisa fungsi helper dan fungsi utama tidak perlu disalin ulang karena panjang, logikanya di bawah ini yang diubah) ...
    // ====================================================================
    // FUNGSI UTAMA & AUTHENTICATION (Sama, tidak berubah)
    // ====================================================================
    const userGreetingEl=document.getElementById("user-greeting"),userNameEl=document.getElementById("user-name"),userDaysEl=document.getElementById("user-days"),userWasteEl=document.getElementById("user-waste"),balanceEl=document.getElementById("balance"),transactionListEl=document.getElementById("transaction-list"),authNavItem=document.getElementById("auth-nav-item"),authNavIcon=authNavItem.querySelector(".nav-icon"),authNavText=authNavItem.querySelector(".nav-text"),wasteTypeSelectCalc=document.getElementById("wasteTypeCalc"),adminOperatorToolsBtn=document.getElementById("admin-operator-tools");onAuthStateChanged(auth,async e=>{unsubscribeFromUserData&&unsubscribeFromUserData(),e?unsubscribeFromUserData=onSnapshot(doc(db,"users",e.uid),t=>{t.exists()?(currentUserData={uid:e.uid,email:e.email,...t.data()},currentUserData.transactions=currentUserData.transactions||[],currentUserData.transactions.forEach(e=>{e.timestamp&&e.timestamp.toDate&&(e.date=formatDate(e.timestamp.toDate()))}),console.log("User data updated:",currentUserData.name,"Role:",currentUserData.role),renderDashboard(currentUserData),updateUIForAuthState(!0)):(console.log("User document does not exist for UID:",e.uid,"initializing with default data."),initializeNewUserDocument(e))},(e)=>{console.error("Error listening to user data:",e),currentUserData=guestData,updateUIForAuthState(!1),renderDashboard(currentUserData),showNotification("Gagal memuat data pengguna: "+e.message,"error")}):(currentUserData=guestData,console.log("User logged out."),updateUIForAuthState(!1),renderDashboard(currentUserData))});async function initializeNewUserDocument(e){const t=doc(db,"users",e.uid);try{await setDoc(t,{name:e.displayName||e.email.split("@")[0]||"Pengguna Baru",email:e.email,birthdate:null,address:null,role:"member",balance:0,points:0,activeDays:0,totalWasteKg:0,transactions:[],createdAt:serverTimestamp(),lastActiveDate:null},{merge:!0}),console.log("New user document (or merged) initialized for:",e.email)}catch(e){console.error("Error initializing new user document:",e),showNotification("Gagal inisialisasi pengguna: "+e.message,"error")}}function updateUIForAuthState(e){e?(authNavIcon.textContent="\ud83d\udd13",authNavText.textContent="Logout",userGreetingEl.textContent="Selamat datang,","admin"!==currentUserData.role&&"operator"!==currentUserData.role?adminOperatorToolsBtn.style.display="none":adminOperatorToolsBtn.style.display="flex"):(authNavIcon.textContent="\ud83d\udd11",authNavText.textContent="Login",userGreetingEl.textContent="Silakan login",transactionListEl.innerHTML='<p style="text-align:center; color:#999;">Login untuk melihat riwayat transaksi.</p>',adminOperatorToolsBtn.style.display="none")}
    
    // >>> PERUBAHAN: handleAuthClick menggunakan showNotification <<<
    window.handleAuthClick = () => {
        if (currentUserData && currentUserData.uid) {
            signOut(auth).then(() => {
                showNotification("Anda berhasil logout.");
            }).catch((error) => {
                showNotification("Gagal logout: " + error.message, "error");
                console.error("Logout error:", error);
            });
        } else {
            showLoginForm();
        }
    }
    
    // ... (Fungsi renderDashboard sama, tidak perlu disalin ulang) ...
    function renderDashboard(e){userNameEl.textContent=e.name,userDaysEl.textContent=e.activeDays||0,userWasteEl.textContent=`${(e.totalWasteKg||0).toLocaleString("id-ID",{maximumFractionDigits:2})}kg`,balanceEl.textContent=`Rp ${(e.balance||0).toLocaleString("id-ID")}`,transactionListEl.innerHTML="",e.transactions&&e.transactions.length>0?([...e.transactions].sort((e,t)=>{const o=e.timestamp&&e.timestamp.toDate?e.timestamp.toDate():new Date(0),a=t.timestamp&&t.timestamp.toDate?t.timestamp.toDate():new Date(0);return a.getTime()-o.getTime()}).slice(0,5).forEach(e=>{const t="setor"===e.type?"\ud83d\udce5":"tarik"===e.type?"\ud83d\udce4":"\ud83c\udf81",o=Math.abs(e.amount).toLocaleString("id-ID"),a=e.timestamp&&e.timestamp.toDate?formatDate(e.timestamp.toDate()):"Tanggal Tidak Diketahui",s=`\n                        <div class="transaction-item ${e.type}">\n                            <div class="transaction-icon ${e.type}">${t}</div>\n                            <div class="transaction-info">\n                                <div class="transaction-title">${e.title}</div>\n                                <div class="transaction-detail">${e.detail}</div>\n                                <div class="transaction-date">${a}</div>\n                            </div>\n                            <div class="transaction-amount ${e.type}">${e.amount<0?"-":"+"}Rp ${o}</div>\n                        </div>\n                    `;transactionListEl.insertAdjacentHTML("beforeend",s)}),0):currentUserData&¤tUserData.uid?transactionListEl.innerHTML='<p style="text-align:center; color:#999;">Belum ada transaksi.</p>':transactionListEl.innerHTML='<p style="text-align:center; color:#999;">Login untuk melihat riwayat transaksi.</p>',renderWasteTypeOptions()}function renderWasteTypeOptions(){wasteTypeSelectCalc.innerHTML='<option value="" data-price="0">Pilih Jenis Sampah</option>';for(const[e,t]of Object.entries(wastePrices))wasteTypeSelectCalc.insertAdjacentHTML("beforeend",`<option value="${e}" data-price="${t}">${e} (Rp ${t.toLocaleString("id-ID")}/kg)</option>`)}

    // >>> PERUBAHAN: Semua fungsi di bawah ini sekarang menggunakan showNotification, dan loading spinner di dalam try...finally
    window.showLoginForm = () => createModal('🔑', 'Login Pengguna', `<div class="modal-form"><input type="email" id="loginEmail" placeholder="Email" required><div class="password-wrapper"><input type="password" id="loginPassword" placeholder="Password" required><button type="button" class="password-toggle" onclick="togglePasswordVisibility('loginPassword')">👁️</button></div><button class="modal-btn" id="loginBtn" onclick="handleLogin()">Login</button><button class="modal-btn secondary" onclick="showRegistrationForm()">Belum punya akun? Daftar</button><a href="#" class="modal-link" onclick="showResetPassword()">Lupa password?</a></div>`, '', () => {});
    
    window.handleLogin = async () => {
        const loginBtn = document.getElementById('loginBtn');
        const originalBtnText = loginBtn.innerHTML;
        showLoading('loginBtn');

        const email = document.getElementById('loginEmail').value;
        const password = document.getElementById('loginPassword').value;
        
        if (!email || !password) {
            showNotification("Email dan password harus diisi.", "error");
            hideLoading('loginBtn', originalBtnText);
            return;
        }

        try {
            await signInWithEmailAndPassword(auth, email, password);
            closeModal();
            showNotification(`Selamat datang kembali!`);
        } catch (error) {
            showNotification("Login Gagal: " + error.code, "error");
            console.error("Login error:", error);
        } finally {
            hideLoading('loginBtn', originalBtnText);
        }
    }

    window.showRegistrationForm = () => createModal('📝', 'Daftar Akun Baru', `<div class="modal-form"><label for="regName">Nama Lengkap</label><input type="text" id="regName" placeholder="Contoh: Budi Santoso" required><label for="regEmail">Email</label><input type="email" id="regEmail" placeholder="contoh@email.com" required><label for="regPassword">Password</label><div class="password-wrapper"><input type="password" id="regPassword" placeholder="Minimal 6 karakter" required><button type="button" class="password-toggle" onclick="togglePasswordVisibility('regPassword')">👁️</button></div><label for="regBirthdate">Tanggal Lahir (Opsional)</label><input type="date" id="regBirthdate"><label for="regAddress">Alamat (Opsional)</label><input type="text" id="regAddress" placeholder="Contoh: Dusun Citambal RT 01/RW 01"><button class="modal-btn" id="registerBtn" onclick="handleRegistration()">Daftar Sekarang</button><button class="modal-btn secondary" onclick="showLoginForm()">Sudah punya akun? Login</button></div>`, '', () => {});
    
    window.handleRegistration = async () => {
        const registerBtn = document.getElementById('registerBtn');
        const originalBtnText = registerBtn.innerHTML;
        showLoading('registerBtn');

        const name = document.getElementById('regName').value;
        const email = document.getElementById('regEmail').value;
        const password = document.getElementById('regPassword').value;
        const birthdate = document.getElementById('regBirthdate').value;
        const address = document.getElementById('regAddress').value;

        if (!name || !email || !password) {
            showNotification("Nama, Email, dan Password wajib diisi!", "error");
            hideLoading('registerBtn', originalBtnText); return;
        }
        if (password.length < 6) {
            showNotification("Password minimal 6 karakter.", "error");
            hideLoading('registerBtn', originalBtnText); return;
        }

        try {
            const userCredential = await createUserWithEmailAndPassword(auth, email, password);
            const user = userCredential.user;
            await setDoc(doc(db, "users", user.uid), { name, email, birthdate: birthdate || null, address: address || null, role: 'member', balance: 0, points: 0, activeDays: 0, totalWasteKg: 0, transactions: [], createdAt: serverTimestamp(), lastActiveDate: null }, { merge: true });
            closeModal();
            showNotification("Pendaftaran berhasil! Anda otomatis login.");
        } catch (error) {
            showNotification("Pendaftaran Gagal: " + error.code, "error");
            console.error("Registration error:", error);
        } finally {
            hideLoading('registerBtn', originalBtnText);
        }
    };

    window.showProfil = () => { /* ... (fungsi sama, tidak perlu notifikasi) ... */ if(!currentUserData||!currentUserData.uid)return void createModal("\ud83d\udc64","Profil Pengguna",'<p class="modal-text">Silakan login untuk melihat profil Anda.</p>');const e=`\n            <div class="profile-data-item"><strong>Nama:</strong> ${currentUserData.name||"-"}</div>\n            <div class="profile-data-item"><strong>Email:</strong> ${currentUserData.email||"-"}</div>\n            <div class="profile-data-item"><strong>Tgl Lahir:</strong> ${currentUserData.birthdate||"-"}</div>\n            <div class="profile-data-item"><strong>Alamat:</strong> ${currentUserData.address||"-"}</div>\n            <button class="modal-btn secondary" id="resetPassBtn" onclick="showResetPassword()" style="margin-top: 20px;">Ganti Password</button>\n        `;createModal("\ud83d\udc64","Profil Pengguna",e) };

    window.showResetPassword = () => { /* ... (fungsi sama, tidak perlu notifikasi) ... */ const e=currentUserData&¤tUserData.uid?currentUserData.email:"",t=`\n            <div class="modal-form">\n                <label for="resetEmail">Email Anda</label>\n                <input type="email" id="resetEmail" value="${e}" placeholder="Masukkan email terdaftar" required>\n                <button class="modal-btn" id="sendResetBtn" onclick="handleResetPassword()">Kirim Link Reset Password</button>\n            </div>\n        `;createModal("\ud83d\udd11","Reset Password",t,"Kembali",showLoginForm) };
    
    window.handleResetPassword = async () => {
        const sendResetBtn = document.getElementById('sendResetBtn');
        const originalBtnText = sendResetBtn.innerHTML;
        showLoading('sendResetBtn');

        const email = document.getElementById('resetEmail').value;
        if (!email) {
            showNotification("Email harus diisi.", "error");
            hideLoading('sendResetBtn', originalBtnText); return;
        }
        try {
            await sendPasswordResetEmail(auth, email);
            showNotification(`Email reset password telah dikirim ke ${email}.`);
            closeModal();
        } catch (error) {
            showNotification("Gagal mengirim email: " + error.code, "error");
            console.error("Reset password error:", error);
        } finally {
            hideLoading('sendResetBtn', originalBtnText);
        }
    };
    
    // ... (Sisa fungsi lain tidak perlu disalin ulang karena panjang, logikanya sama, hanya alert diganti notifikasi)
    // Misalnya: processRedeem, processSetorSampah, processTarikSaldo, dll.
    // Prinsipnya sama: ganti `alert(...)` dengan `showNotification(...)`
    // dan pastikan `showLoading`/`hideLoading` ada di dalam `try...finally`.
    // Di bawah ini contoh untuk satu fungsi lagi sebagai referensi
    
    window.processSetorSampah = async () => {
        if (!currentUserData || !currentUserData.uid) {
            showNotification("Anda harus login untuk mencatat setoran.", "error"); return;
        }

        const setorBtn = document.getElementById('setorBtn');
        const originalBtnText = setorBtn.innerHTML;
        showLoading('setorBtn');

        try {
            const wasteTypeSelect = document.getElementById('setorWasteType');
            const wasteWeightInput = document.getElementById('setorWasteWeight');
            const selectedWasteType = wasteTypeSelect.value;
            const wasteWeight = parseFloat(wasteWeightInput.value);

            if (!selectedWasteType || !wasteWeight || wasteWeight <= 0) {
                showNotification("Pilih jenis sampah dan masukkan berat yang valid.", "error");
                // `finally` akan menangani hideLoading
                return;
            }

            // ... (sisa logika sama)
            const wastePricePerKg = wastePrices[selectedWasteType];
            const earnedAmount = wasteWeight * wastePricePerKg;
            const earnedPoints = wasteWeight * pointsPerKg;

            if (!confirm(`Anda akan menyetorkan ${wasteWeight} kg ${selectedWasteType}.\nEstimasi Saldo: Rp ${earnedAmount.toLocaleString('id-ID')}\nLanjutkan?`)) {
                 // `finally` akan menangani hideLoading
                return;
            }

            const userDocRef = doc(db, "users", currentUserData.uid);
            let newActiveDays = currentUserData.activeDays || 0;
            if (!currentUserData.lastActiveDate || !isSameDay(currentUserData.lastActiveDate.toDate(), new Date())) {
                newActiveDays++;
            }
            const newBalance = (currentUserData.balance || 0) + earnedAmount;
            const newPoints = (currentUserData.points || 0) + earnedPoints;
            const newTotalWasteKg = (currentUserData.totalWasteKg || 0) + wasteWeight;
            const newTransaction = { type: 'setor', title: `Setor Sampah: ${selectedWasteType}`, detail: `${wasteWeight} kg`, amount: earnedAmount, timestamp: serverTimestamp() };

            await updateDoc(userDocRef, { balance: newBalance, points: newPoints, totalWasteKg: newTotalWasteKg, activeDays: newActiveDays, lastActiveDate: serverTimestamp(), transactions: arrayUnion(newTransaction) });
            
            closeModal();
            showNotification(`Setoran berhasil! Saldo +Rp ${earnedAmount.toLocaleString('id-ID')}`);
        } catch (error) {
            showNotification("Gagal mencatat setoran: " + error.message, "error");
            console.error("Error processing waste deposit:", error);
        } finally {
            hideLoading('setorBtn', originalBtnText);
        }
    };
    
    // Sisa fungsi lainnya seperti processTarikSaldo, processRedeem, dll, juga telah saya perbaiki dengan logika yang sama
    // Saya tidak menempelkannya di sini agar respons tidak terlalu panjang, tapi prinsipnya sama.
    // Jika Anda ingin melihat versi lengkapnya, beri tahu saya.
    
    // ... (sisa kode dari file asli Anda bisa ditempel di sini, karena tidak ada perubahan signifikan)
    // Saya akan menempelkan kode sisanya agar lengkap
    window.showEventAndReward=()=>{createModal("\u2b50","Event & Reward",'<p class="modal-text">Pilih layanan yang ingin Anda lihat.</p><div class="modal-menu-grid"><div class="feature-item" onclick="showNotification(\'Belum ada event saat ini. Pantau terus ya!\', \'success\')"><div class="feature-icon">\ud83c\udf89</div><div class="feature-text">Lihat Event</div></div><div class="feature-item" onclick="showTukarPoin()"><div class="feature-icon">\ud83c\udf81</div><div class="feature-text">Tukar Poin</div></div></div>',"Tutup")};window.showCnuMenu=()=>{createModal("\ud83c\udfde\ufe0f","Citambal Nu Urang",'<p class="modal-text">Citambal Nu Urang (CNU) adalah program pemberdayaan masyarakat lokal. Pilih layanan yang Anda butuhkan.</p><div class="modal-menu-grid"><div class="feature-item" onclick="showUmkmList()"><div class="feature-icon">\ud83c\udfea</div><div class="feature-text">UMKM</div></div><div class="feature-item" onclick="showAirBersihMenu()"><div class="feature-icon">\ud83d\udca7</div><div class="feature-text">Air Bersih</div></div></div>',"Tutup")};window.showUmkmList=()=>{createModal("\ud83c\udfea","Daftar UMKM Citambal",'<div class="modal-text">\n                Dukung usaha lokal kita! Hubungi langsung untuk pemesanan.<br><br>\n                <strong>1. Warung Seblak Teh Popon</strong><br>\n                Produk: Seblak, Baso Aci<br>\n                Telp: <a href="tel:081234567890">0812-3456-7890</a><br><br>\n                <strong>2. Rengginang Mang Ujang</strong><br>\n                Produk: Rengginang Aneka Rasa<br>\n                Telp: <a href="tel:089876543210">0898-7654-3210</a><br><br>\n                <strong>3. Keripik Kaca Bi Iis</strong><br>\n                Produk: Keripik Kaca Pedas<br>\n                Telp: <a href="tel:085567891234">0855-6789-1234</a>\n            </div>',"Kembali",showCnuMenu)};window.showAirBersihMenu=()=>{createModal("\ud83d\udca7","Air Bersih Gunung Tumpeng",'<p class="modal-text">Layanan pengelolaan Air Bersih Gunung Tumpeng. Pembayaran bisa menggunakan saldo tabungan sampah.</p><button class="modal-btn" onclick="showNotification(\'Fitur Pendaftaran Air Bersih akan segera tersedia.\')">\ud83d\udcdd Daftar Sambungan Baru</button><button class="modal-btn" onclick="showNotification(\'Fitur Bayar Tagihan Air akan segera tersedia.\')">\ud83d\udcb3 Bayar Tagihan Air</button><button class="modal-btn secondary" onclick="showNotification(\'Fitur Riwayat Pembayaran akan segera tersedia.\')">\ud83d\udcca Lihat Riwayat</button>',"Kembali",showCnuMenu)};window.showTukarPoin=()=>{if(!currentUserData||!currentUserData.uid)return void createModal("\u26a0\ufe0f","Akses Ditolak",'<p class="modal-text">Silakan login untuk menukar poin Anda.</p>');let e="";e=0===rewards.length?'<p style="text-align:center; color:#999;">Belum ada reward yang tersedia.</p>':rewards.map(e=>`\n                    <div class="reward-item">\n                        <div class="reward-item-icon">${e.icon}</div>\n                        <div class="reward-item-info">\n                            <div class="reward-item-name">${e.name}</div>\n                            <div class="reward-item-cost">${e.cost.toLocaleString("id-ID")} Poin</div>\n                        </div>\n                        <button class="reward-item-btn" id="redeem-${e.id}" onclick="processRedeem('${e.id}', this)" ${!((currentUserData.points||0)>=e.cost)?"disabled":""}>Tukar</button>\n                    </div>\n                `).join("");const t=`\n            <div class="points-balance">Poin Anda Saat Ini: <br> <span id="current-points">${(currentUserData.points||0).toLocaleString("id-ID")} Poin</span></div>\n            <div class="reward-list">${e}</div>\n        `;createModal("\ud83c\udf81","Tukar Poin Reward",t,"Selesai")};window.processRedeem=async(e,t)=>{if(!currentUserData||!currentUserData.uid)return void showNotification("Anda harus login untuk menukar poin.","error");const o=t?t.innerHTML:"Tukar";t&&showLoading(t.id);const a=rewards.find(t=>t.id===e);if(!a)return showNotification("Reward tidak ditemukan.","error"),void(t&&hideLoading(t.id,o));if((currentUserData.points||0)<a.cost)return showNotification("Poin Anda tidak cukup untuk menukar reward ini.","error"),void(t&&hideLoading(t.id,o));if(confirm(`Apakah Anda yakin ingin menukar ${a.cost.toLocaleString("id-ID")} Poin untuk ${a.name}?`))try{const e=doc(db,"users",currentUserData.uid),t={type:"reward",title:`Penukaran Poin: ${a.name}`,detail:`Poin berkurang ${a.cost.toLocaleString("id-ID")}`,amount:-a.cost,timestamp:serverTimestamp()};await updateDoc(e,{points:(currentUserData.points||0)-a.cost,transactions:arrayUnion(t),lastActiveDate:serverTimestamp()}),showNotification(`Berhasil menukar ${a.name}!`,"success"),closeModal()}catch(e){console.error("Error redeeming points:",e),showNotification("Gagal menukar poin: "+e.message,"error")}finally{t&&hideLoading(t.id,o)}else t&&hideLoading(t.id,o)};window.showTarikSaldo=()=>{if(!currentUserData||!currentUserData.uid)return void createModal("\u26a0\ufe0f","Akses Ditolak",'<p class="modal-text">Silakan login untuk melakukan penarikan saldo.</p>');const e=`\n            <div class="modal-form">\n                <label for="withdrawAmount">Jumlah Penarikan (Rp)</label>\n                <input type="number" id="withdrawAmount" placeholder="Min. Rp 10.000" step="1000" min="10000" required>\n                \n                <p class="modal-text" style="text-align: center; margin-top: 10px;">Saldo Anda Saat Ini: <strong>Rp ${(currentUserData.balance||0).toLocaleString("id-ID")}</strong></p>\n\n                <button class="modal-btn" id="withdrawBtn" onclick="processTarikSaldo()">Tarik Saldo</button>\n            </div>\n        `;createModal("\ud83d\udcb5","Tarik Saldo",e,"",()=>{})};window.processTarikSaldo=async()=>{if(!currentUserData||!currentUserData.uid)return void showNotification("Anda harus login untuk melakukan penarikan.","error");const e=document.getElementById("withdrawBtn"),t=e.innerHTML;showLoading("withdrawBtn");try{const o=document.getElementById("withdrawAmount"),a=parseFloat(o.value);if(isNaN(a)||a<=0)return void showNotification("Jumlah penarikan tidak valid.","error");if(a<1e4)return void showNotification("Jumlah penarikan minimal adalah Rp 10.000.","error");if(a>currentUserData.balance)return void showNotification("Saldo Anda tidak cukup untuk penarikan ini.","error");if(confirm(`Apakah Anda yakin ingin menarik saldo sebesar Rp ${a.toLocaleString("id-ID")}?`)){const e=doc(db,"users",currentUserData.uid),t={type:"tarik",title:"Penarikan Saldo",detail:"Tunai",amount:-a,timestamp:serverTimestamp()};await updateDoc(e,{balance:currentUserData.balance-a,transactions:arrayUnion(t),lastActiveDate:serverTimestamp()}),showNotification(`Penarikan berhasil! Saldo Anda sekarang: Rp ${(currentUserData.balance-a).toLocaleString("id-ID")}`,"success"),closeModal()}}catch(e){console.error("Error processing withdrawal:",e),showNotification("Gagal mencatat penarikan: "+e.message,"error")}finally{hideLoading("withdrawBtn",t)}};window.togglePasswordVisibility=e=>{const t=document.getElementById(e);t.type="password"===t.type?"text":"password",t.nextElementSibling.textContent="password"===t.type?"\ud83d\udc41\ufe0f":"\ud83d\ude48"};window.calculateWaste=()=>{const e=document.getElementById("wasteTypeCalc"),t=document.getElementById("wasteWeight"),o=document.getElementById("calculatorResult"),a=document.getElementById("estimatedPrice"),s=parseFloat(e.options[e.selectedIndex].getAttribute("data-price")),n=parseFloat(t.value);if(o.style.display="block",isNaN(s)||0===s||isNaN(n)||n<=0)return o.style.background="rgba(231, 76, 60, 0.5)",void(a.textContent="Pilih jenis & isi berat yang valid");o.style.background="rgba(255,255,255,0.1)",a.textContent=`Rp ${(s*n).toLocaleString("id-ID")}`};window.setActiveNav=e=>{document.querySelectorAll(".nav-item").forEach(e=>e.classList.remove("active")),e.classList.add("active")};window.showContactAdmin=()=>{createModal("📞","Hubungi Admin",'<p class="modal-text">Jika Anda memiliki pertanyaan atau kendala, silakan hubungi admin kami melalui WhatsApp.</p><a href="https://wa.me/6281322355056?text=Halo%20Admin%20Bank%20Sampah%20ARAS" target="_blank" class="contact-link">💬 Hubungi via WhatsApp</a><p class="modal-text" style="font-size: 12px; text-align: center; margin-top: 15px;">Jam Operasional Admin: 08:00 - 17:00 WIB</p>')};window.showTransfer=()=>{currentUserData&¤tUserData.uid?createModal("\ud83d\udcb8","Transfer & Tarik Saldo",'<p class="modal-text">Anda dapat mentransfer saldo tabungan sampah Anda ke rekening bank atau menariknya secara tunai di lokasi Bank Sampah ARAS. Hubungi petugas untuk melakukan transaksi.</p>'):createModal("\u26a0\ufe0f","Akses Ditolak",'<p class="modal-text">Silakan login untuk melakukan transfer.</p>')};window.showIsiSaldo=()=>{createModal("\u2795","Cara Mengisi Saldo",'<p class="modal-text">Saldo Anda bertambah setiap kali Anda menyetorkan sampah yang memiliki nilai jual. Semakin banyak sampah yang Anda setor, semakin besar saldo tabungan Anda!</p>')};window.showActivityHistory=()=>{if(!currentUserData||!currentUserData.uid)return void createModal("\u26a0\ufe0f","Akses Ditolak",'<p class="modal-text">Silakan login untuk melihat riwayat aktivitas.</p>');let e='<p style="text-align:center; color:#999;">Belum ada riwayat aktivitas.</p>';currentUserData.transactions&¤tUserData.transactions.length>0&&(e=[...currentUserData.transactions].sort((e,t)=>{const o=e.timestamp&&e.timestamp.toDate?e.timestamp.toDate():new Date(0),a=t.timestamp&&t.timestamp.toDate?t.timestamp.toDate():new Date(0);return a.getTime()-o.getTime()}).map(e=>{const t="setor"===e.type?"\ud83d\udce5":"tarik"===e.type?"\ud83d\udce4":"\ud83c\udf81",o=Math.abs(e.amount).toLocaleString("id-ID"),a=e.timestamp&&e.timestamp.toDate?formatDate(e.timestamp.toDate()):"Tanggal Tidak Diketahui";return`\n                    <div class="transaction-item ${e.type}">\n                        <div class="transaction-icon ${e.type}">${t}</div>\n                        <div class="transaction-info">\n                            <div class="transaction-title">${e.title}</div>\n                            <div class="transaction-detail">${e.detail}</div>\n                            <div class="transaction-date">${a}</div>\n                        </div>\n                        <div class="transaction-amount ${e.type}">${e.amount<0?"-":"+"}Rp ${o}</div>\n                    </div>\n                `}).join("")),createModal("\ud83d\udcca","Riwayat Aktivitas",`<div id="modal-activity-list" style="max-height: 300px; overflow-y: auto;">${e}</div>`)};window.showHarga=()=>{let e="Daftar harga sampah saat ini (per kg):\n\n";e+=0===Object.keys(wastePrices).length?"Belum ada data harga sampah yang tersedia.":Object.entries(wastePrices).map(([e,t])=>`• ${e}: Rp ${t.toLocaleString("id-ID")}`).join("\n"),e+="\n*Harga dapat berubah sewaktu-waktu.",createModal("\ud83d\udcb0","Daftar Harga Sampah",`<p class="modal-text">${e}</p>`)};window.showJadwal=()=>{createModal("\ud83d\udcc5","Jadwal Operasional",'<p class="modal-text">Bank Sampah ARAS beroperasi pada:\n\n• Hari: Selasa & Jumat\n• Jam: 08:00 - 16:00 WIB\n\nUntuk permintaan pickup, hubungi pengurus H-1.</p>')};window.showPanduan=()=>{createModal("\ud83d\udcd6","Panduan Penggunaan",'<p class="modal-text">Panduan lengkap penggunaan aplikasi Bank Sampah ARAS akan segera tersedia di sini. Silakan login atau hubungi admin untuk informasi lebih lanjut.</p>')};window.showLeaderboard=async()=>{let e="";try{createModal("\ud83c\udfc6","Memuat Leaderboard...",'<div class="loading-spinner"></div>',"",()=>{});const t=collection(db,"users"),o=query(t,orderBy("totalWasteKg","desc"),limit(10)),a=await getDocs(o),s=[];if(a.forEach(e=>{const t=e.data();s.push({id:e.id,name:t.name,totalWasteKg:t.totalWasteKg||0,isCurrentUser:currentUserData&&e.id===currentUserData.uid})}),0===s.length)e='<p class="modal-text">Belum ada data leaderboard.</p>';else{e+='<ul class="leaderboard-list">';s.forEach((t,o)=>{const a=o+1,s=t.isCurrentUser?' style="background-color: #e0ffe0; border-color: #2ecc71;"':"";e+=`\n                        <li class="leaderboard-item"${s}>\n                            <span class="leaderboard-rank">#${a}</span>\n                            <span class="leaderboard-name">${t.name}</span>\n                            <span class="leaderboard-value">${t.totalWasteKg.toLocaleString("id-ID",{maximumFractionDigits:2})} kg</span>\n                        </li>\n                    `});e+="</ul>";!currentUserData||!currentUserData.uid||"member"!==currentUserData.role||s.some(e=>e.isCurrentUser)?currentUserData&¤tUserData.uid||(e+='<p class="leaderboard-note">Login untuk melihat peringkat Anda.</p>'):e+=`<p class="leaderboard-note">Anda belum masuk Top 10. Terus setorkan sampah Anda! (<span style="font-weight: bold;">Anda: ${currentUserData.totalWasteKg.toLocaleString("id-ID",{maximumFractionDigits:2})} kg</span>)</p>`}createModal("\ud83c\udfc6","Leaderboard Nasabah",e)}catch(t){console.error("Error fetching leaderboard data:",t),createModal("\u26a0\ufe0f","Gagal Memuat Leaderboard",'<p class="modal-text">Terjadi kesalahan saat memuat data leaderboard. Silakan coba lagi nanti.</p>')}};window.showAdminOperatorPanel=()=>{if(!currentUserData||"admin"!==currentUserData.role&&"operator"!==currentUserData.role)return void showNotification("Akses ditolak. Anda bukan Admin atau Operator.","error");let e=`\n            <p class="modal-text">Selamat datang, ${currentUserData.name} (${currentUserData.role}).</p>\n            <div class="modal-menu-grid">\n                <div class="feature-item" onclick="showManagePricesModal()">\n                    <div class="feature-icon">\ud83d\udcb8</div>\n                    <div class="feature-text">Kelola Harga Sampah</div>\n                </div>\n                <div class="feature-item" onclick="showManageRewardsModal()">\n                    <div class="feature-icon">\ud83c\udf81</div>\n                    <div class="feature-text">Kelola Reward</div>\n                </div>\n        `;"admin"===currentUserData.role&&(e+=`\n                <div class="feature-item" onclick="showManageUsersModal()">\n                    <div class="feature-icon">\ud83d\udc65</div>\n                    <div class="feature-text">Kelola Pengguna</div>\n                </div>\n            `),e+="</div>",createModal("\u2699\ufe0f","Panel Admin/Operator",e,"Tutup")};window.showManagePricesModal=()=>{if(!currentUserData||"admin"!==currentUserData.role&&"operator"!==currentUserData.role)return void showNotification("Akses ditolak.","error");let e='<div class="modal-form">';for(const[t,o]of Object.entries(wastePrices))e+=`\n                <div class="admin-form-item">\n                    <label for="price-${t}">Jenis: ${t}</label>\n                    <input type="number" id="price-${t}" value="${o}" min="0" step="100">\n                    <div class="admin-form-actions">\n                        <button class="modal-btn secondary delete" id="delete-price-${t}" onclick="deleteWasteType('${t}')">Hapus</button>\n                    </div>\n                </div>\n            `;e+='\n            <hr style="margin: 20px 0;">\n            <h3>Tambah Jenis Sampah Baru</h3>\n            <label for="newWasteType">Nama Jenis Sampah</label>\n            <input type="text" id="newWasteType" placeholder="Nama Jenis Sampah">\n            <label for="newWastePrice">Harga (Rp/kg)</label>\n            <input type="number" id="newWastePrice" placeholder="Harga per kg" min="0" step="100">\n            <button class="modal-btn" id="addPriceBtn" onclick="addWasteType()">Tambah Jenis</button>\n            <button class="modal-btn" id="savePricesBtn" onclick="saveWastePrices()">Simpan Perubahan</button>\n            </div>\n        ',createModal("\ud83d\udcb8","Kelola Harga Sampah",e,"Kembali",showAdminOperatorPanel)};window.addWasteType=async()=>{const e=document.getElementById("newWasteType").value.trim(),t=parseFloat(document.getElementById("newWastePrice").value);if(!e||isNaN(t)||t<0)return void showNotification("Nama jenis sampah dan harga harus valid.","error");if(wastePrices[e])return void showNotification(`Jenis sampah "${e}" sudah ada. Gunakan 'Simpan Perubahan' untuk mengeditnya.`,"error");wastePrices[e]=t,document.getElementById("newWasteType").value="",document.getElementById("newWastePrice").value="",showManagePricesModal()};window.deleteWasteType=e=>{confirm(`Apakah Anda yakin ingin menghapus jenis sampah "${e}"?`)&&(delete wastePrices[e],showManagePricesModal())};window.saveWastePrices=async()=>{const e=document.getElementById("savePricesBtn"),t=e.innerHTML;showLoading("savePricesBtn");const o={};document.querySelectorAll('.admin-form-item input[id^="price-"]').forEach(e=>{const t=e.id.replace("price-",""),a=parseFloat(e.value);!isNaN(a)&&a>=0&&(o[t]=a)});for(const[e,t]of Object.entries(wastePrices))e in o||(o[e]=t);try{await setDoc(doc(db,"settings","app_config"),{wastePrices:o,pointsPerKg:pointsPerKg,lastUpdated:serverTimestamp()},{merge:!0}),wastePrices=o,showNotification("Harga sampah berhasil diperbarui!","success"),closeModal(),renderDashboard(currentUserData)}catch(e){console.error("Error saving waste prices:",e),showNotification("Gagal menyimpan harga sampah: "+e.message,"error")}finally{hideLoading("savePricesBtn",t)}};window.showManageRewardsModal=()=>{if(!currentUserData||"admin"!==currentUserData.role&&"operator"!==currentUserData.role)return void showNotification("Akses ditolak.","error");let e='<div class="modal-form">';0===rewards.length?e+='<p class="modal-text" style="text-align: center;">Belum ada reward. Tambahkan yang baru!</p>':rewards.forEach(t=>{e+=`\n                    <div class="admin-form-item" id="reward-item-${t.id}">\n                        <label for="reward-name-${t.id}">Nama Reward</label>\n                        <input type="text" id="reward-name-${t.id}" value="${t.name}">\n                        <label for="reward-cost-${t.id}">Poin Diperlukan</label>\n                        <input type="number" id="reward-cost-${t.id}" value="${t.cost}" min="0" step="100">\n                        <label for="reward-icon-${t.id}">Icon</label>\n                        <input type="text" id="reward-icon-${t.id}" value="${t.icon}" maxlength="2" placeholder="Ex: \ud83c\udf81">\n                        <div class="admin-form-actions">\n                            <button class="modal-btn secondary" id="update-reward-${t.id}" onclick="updateReward('${t.id}')">Update</button>\n                            <button class="modal-btn secondary delete" id="delete-reward-${t.id}" onclick="deleteReward('${t.id}')">Hapus</button>\n                        </div>\n                    </div>\n                `});e+='\n            <hr style="margin: 20px 0;">\n            <h3>Tambah Reward Baru</h3>\n            <label for="newRewardName">Nama Reward</label>\n            <input type="text" id="newRewardName" placeholder="Contoh: Voucher Belanja">\n            <label for="newRewardCost">Poin Diperlukan</label>\n            <input type="number" id="newRewardCost" placeholder="Poin" min="0" step="100">\n            <label for="newRewardIcon">Icon</label>\n            <input type="text" id="newRewardIcon" placeholder="Ex: \ud83d\uded2" maxlength="2">\n            <button class="modal-btn" id="addRewardBtn" onclick="addReward()">Tambah Reward</button>\n            </div>\n        ',createModal("\ud83c\udf81","Kelola Reward",e,"Kembali",showAdminOperatorPanel)};window.addReward=async()=>{const e=document.getElementById("newRewardName").value.trim(),t=parseFloat(document.getElementById("newRewardCost").value),o=document.getElementById("newRewardIcon").value.trim();if(!e||isNaN(t)||t<0||!o)return void showNotification("Nama, poin, dan icon reward harus valid.","error");const a=document.getElementById("addRewardBtn"),s=a.innerHTML;showLoading("addRewardBtn");try{await addDoc(collection(db,"rewards"),{name:e,cost:t,icon:o}),await fetchRewards(),showManageRewardsModal(),showNotification("Reward berhasil ditambahkan!","success")}catch(e){console.error("Error adding reward:",e),showNotification("Gagal menambahkan reward: "+e.message,"error")}finally{hideLoading("addRewardBtn",s)}};window.updateReward=async e=>{const t=document.getElementById(`reward-name-${e}`).value.trim(),o=parseFloat(document.getElementById(`reward-cost-${e}`).value),a=document.getElementById(`reward-icon-${e}`).value.trim();if(!t||isNaN(o)||o<0||!a)return void showNotification("Nama, poin, dan icon reward harus valid.","error");const s=`update-reward-${e}`,n=document.getElementById(s),i=n?n.innerHTML:"Update";n&&showLoading(s);try{await updateDoc(doc(db,"rewards",e),{name:t,cost:o,icon:a}),await fetchRewards(),showNotification("Reward berhasil diperbarui!","success")}catch(e){console.error("Error updating reward:",e),showNotification("Gagal memperbarui reward: "+e.message,"error")}finally{n&&hideLoading(s,i)}};window.deleteReward=async e=>{if(!confirm("Apakah Anda yakin ingin menghapus reward ini?"))return;const t=`delete-reward-${e}`,o=document.getElementById(t),a=o?o.innerHTML:"Hapus";o&&showLoading(t);try{await deleteDoc(doc(db,"rewards",e)),await fetchRewards(),showManageRewardsModal(),showNotification("Reward berhasil dihapus!","success")}catch(e){console.error("Error deleting reward:",e),showNotification("Gagal menghapus reward: "+e.message,"error")}finally{o&&hideLoading(t,a)}};window.showManageUsersModal=async()=>{if(!currentUserData||"admin"!==currentUserData.role)return void showNotification("Akses ditolak. Fitur ini hanya untuk Admin.","error");createModal("\ud83d\udc65","Memuat Pengguna...",'<div class="loading-spinner"></div>',"",()=>{});try{const e=collection(db,"users"),t=query(e,orderBy("name","asc")),o=await getDocs(t);let a='<div class="modal-form">';o.empty?a+='<p class="modal-text">Belum ada pengguna terdaftar.</p>':o.forEach(e=>{const t=e.data(),o=e.id;o!==currentUserData.uid&&(a+=`\n                        <div class="admin-form-item">\n                            <label>Nama: <strong>${t.name}</strong></label>\n                            <label>Email: ${t.email}</label>\n                            <label for="user-role-${o}">Role:</label>\n                            <select id="user-role-${o}">\n                                <option value="member" ${"member"===t.role?"selected":""}>Member</option>\n                                <option value="operator" ${"operator"===t.role?"selected":""}>Operator</option>\n                                <option value="admin" ${"admin"===t.role?"selected":""}>Admin</option>\n                            </select>\n                            <label for="user-balance-${o}">Saldo (Rp):</label>\n                            <input type="number" id="user-balance-${o}" value="${t.balance||0}" step="1">\n                            <label for="user-points-${o}">Poin:</label>\n                            <input type="number" id="user-points-${o}" value="${t.points||0}" step="1">\n                            <div class="admin-form-actions">\n                                <button class="modal-btn secondary" id="update-user-${o}" onclick="updateUser('${o}')">Update User</button>\n                            </div>\n                        </div>\n                    `)});a+="</div>",createModal("\ud83d\udc65","Kelola Pengguna",a,"Kembali",showAdminOperatorPanel)}catch(e){console.error("Error fetching users:",e),createModal("\u26a0\ufe0f","Gagal Memuat Pengguna",'<p class="modal-text">Terjadi kesalahan saat memuat daftar pengguna.</p>',"Kembali",showAdminOperatorPanel)}};window.updateUser=async e=>{if(!currentUserData||"admin"!==currentUserData.role)return void showNotification("Akses ditolak.","error");const t=doc(db,"users",e),o=document.getElementById(`user-role-${e}`).value,a=parseFloat(document.getElementById(`user-balance-${e}`).value),s=parseFloat(document.getElementById(`user-points-${e}`).value);if(isNaN(a)||isNaN(s))return void showNotification("Saldo dan Poin harus berupa angka.","error");const n=`update-user-${e}`,i=document.getElementById(n),r=i?i.innerHTML:"Update User";i&&showLoading(n);try{await updateDoc(t,{role:o,balance:a,points:s}),showNotification(`Pengguna ${e} berhasil diperbarui.`,"success")}catch(e){console.error("Error updating user:",e),showNotification("Gagal memperbarui pengguna: "+e.message,"error")}finally{i&&hideLoading(n,r)}};

    // ====================================================================
    // INISIALISASI APLIKASI
    // ====================================================================
    document.addEventListener('DOMContentLoaded', async () => {
        await fetchAppSettings();
        await fetchRewards();
        console.log("App initialized. Waiting for Firebase Auth state...");
    });
    </script>
</body>
</html>
