<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <!-- Hapus user-scalable=no untuk aksesibilitas -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bank Sampah ARAS - Dompet Digital</title>
    <!-- Tambahkan Favicon -->
    <link rel="icon" href="img/favicon.png" type="image/png">
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
        .modal-content { position: relative; background: white; padding: 30px; border-radius: 20px; width: 90%; max-width: 350px; text-align: center; box-shadow: 0 20px 40px rgba(0,0,0,0.3); animation: zoomIn 0.3s ease-out; max-height: 90vh; overflow-y: auto; } /* Added max-height and overflow */
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
        .modal-form input, .modal-form select, .modal-form textarea { padding: 10px; border: 1px solid #ddd; border-radius: 8px; font-size: 14px; width: 100%; } /* Added textarea */
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
        /* CSS untuk leaderboard */
        .leaderboard-list {
            list-style: none;
            padding: 0;
            margin: 0;
            text-align: left;
        }
        .leaderboard-item {
            display: flex;
            align-items: center;
            padding: 12px;
            margin-bottom: 8px;
            background: #f0f8ff; /* Light blue background */
            border-radius: 10px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.05);
            transition: transform 0.2s ease;
        }
        .leaderboard-item:hover {
            transform: translateY(-2px);
        }
        .leaderboard-rank {
            font-size: 18px;
            font-weight: bold;
            color: #2ecc71; /* Green for rank */
            width: 30px;
            text-align: center;
            margin-right: 15px;
        }
        .leaderboard-name {
            font-weight: 600;
            color: #333;
            flex-grow: 1;
        }
        .leaderboard-value {
            font-weight: bold;
            color: #f39c12; /* Orange for value */
        }
        .leaderboard-note {
            font-size: 12px;
            color: #7f8c8d;
            text-align: center;
            margin-top: 15px;
        }

        /* Loading Spinner CSS */
        .loading-spinner {
            border: 4px solid rgba(0, 0, 0, 0.1);
            border-left-color: #2ecc71;
            border-radius: 50%;
            width: 24px;
            height: 24px;
            animation: spin 1s linear infinite;
            margin: 10px auto;
        }
        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        /* Admin/Operator specific CSS for forms/lists */
        .admin-form-item {
            margin-bottom: 15px;
            border: 1px solid #eee;
            padding: 10px;
            border-radius: 8px;
            background: #f9f9f9;
        }
        .admin-form-item input, .admin-form-item select {
            margin-top: 5px;
        }
        .admin-form-actions {
            display: flex;
            gap: 10px;
            margin-top: 10px;
        }
        .admin-form-actions button {
            flex: 1;
        }
        .admin-list-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px 0;
            border-bottom: 1px solid #eee;
        }
        .admin-list-item:last-child {
            border-bottom: none;
        }
        .admin-list-item-name {
            font-weight: 600;
            flex-grow: 1;
        }
        .admin-list-item-value {
            color: #666;
            margin-right: 10px;
        }
        .admin-list-item-actions button {
            background: #3498db;
            color: white;
            border: none;
            padding: 5px 10px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 12px;
        }
        .admin-list-item-actions button.delete {
            background: #e74c3c;
        }
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
                    <button class="balance-btn" onclick="showSetorSampah()">🗑️ Setor Sampah</button>
                    <button class="balance-btn" onclick="showTarikSaldo()"> 💵 Tarik Saldo</button>
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
                <div class="feature-item" id="admin-operator-tools" style="display: none;" onclick="showAdminOperatorPanel()">
                    <div class="feature-icon">⚙️</div><div class="feature-text">Admin/Operator</div>
                </div>
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
    // Pastikan versi Firebase SDK yang Anda gunakan konsisten dan terbaru.
    // Anda bisa cek versi terbaru di dokumentasi Firebase: https://firebase.google.com/docs/web/setup
    import { initializeApp } from "https://www.gstatic.com/firebasejs/9.22.1/firebase-app.js";
    import { getAnalytics } from "https://www.gstatic.com/firebasejs/9.22.1/firebase-analytics.js";
    import { getAuth, onAuthStateChanged, createUserWithEmailAndPassword, signInWithEmailAndPassword, signOut, sendPasswordResetEmail } from "https://www.gstatic.com/firebasejs/9.22.1/firebase-auth.js";
    import { getFirestore, doc, setDoc, updateDoc, arrayUnion, arrayRemove, serverTimestamp, onSnapshot, collection, query, orderBy, limit, getDocs, deleteDoc, addDoc, getDoc } from "https://www.gstatic.com/firebasejs/9.22.1/firebase-firestore.js"; 

    // Konfigurasi Firebase Anda
    // >>>>>>> PENTING: GANTI API KEY INI DENGAN API KEY PROYEK FIREBASE ANDA SENDIRI <<<<<<<
    const firebaseConfig = {
      apiKey: "AIzaSyCxAYtwTyqgal3LkMmoO7k2AZG4PbSKTnY", // GANTI INI!
      authDomain: "bank-sampah-aras.firebaseapp.com",
      projectId: "bank-sampah-aras",
      storageBucket: "bank-sampah-aras.firebasestorage.app",
      messagingSenderId: "1038502551432",
      appId: "1:1038502551432:web:e3bcd68910f0669be0243d",
      measurementId: "G-365NW7GG75"
    };

    // Inisialisasi Firebase
    const app = initializeApp(firebaseConfig);
    const analytics = getAnalytics(app); // eslint-disable-line no-unused-vars
    const auth = getAuth(app);
    const db = getFirestore(app);
    console.log("Firebase successfully initialized!");

    // ====================================================================
    // STATE MANAGEMENT & DATA GLOBAL
    // ====================================================================
    // Data statis aplikasi (harga sampah, reward, dll.) - NOW FETCHED FROM FIRESTORE
    let wastePrices = {}; 
    let pointsPerKg = 0; // Will be fetched from Firestore settings
    let rewards = []; 

    // Data default untuk pengguna tamu (belum login)
    const guestData = {
        name: "Tamu", activeDays: 0, totalWasteKg: 0, balance: 0, points: 0, transactions: [], role: 'guest'
    };
    let currentUserData = guestData; 
    let unsubscribeFromUserData = null; // Untuk menyimpan fungsi unsubscribe onSnapshot (listener real-time)

    // ====================================================================
    // HELPER FUNCTIONS (Fungsi Pembantu)
    // ====================================================================

    // Fungsi untuk memformat objek Date atau Firestore Timestamp ke string yang mudah dibaca
    function formatDate(date) {
        if (!date) return '-';
        if (date.toDate) { // Check if it's a Firestore Timestamp
            date = date.toDate();
        } else if (!(date instanceof Date)) { // Fallback if not Date or Firestore Timestamp
            date = new Date(date);
        }
        const options = { year: 'numeric', month: 'short', day: 'numeric', hour: '2-digit', minute: '2-digit' };
        return date.toLocaleDateString('id-ID', options);
    }

    // Fungsi untuk mengecek apakah dua tanggal berada di hari yang sama (mengabaikan waktu)
    function isSameDay(d1, d2) {
        if (!d1 || !d2) return false;
        if (d1.toDate) d1 = d1.toDate(); // Convert Firestore Timestamp to Date
        if (d2.toDate) d2 = d2.toDate(); // Convert Firestore Timestamp to Date

        return d1.getFullYear() === d2.getFullYear() &&
               d1.getMonth() === d2.getMonth() &&
               d1.getDate() === d2.getDate();
    }

    // Fungsi untuk menampilkan modal (pop-up) dengan konten dinamis
    function createModal(icon, title, content, buttonText = "Tutup", buttonAction = closeModal) {
        const modal = document.getElementById('modal');
        const modalIcon = document.getElementById('modalIcon');
        const modalTitle = document.getElementById('modalTitle');
        const modalBody = document.getElementById('modalBody');
        const modalBtn = document.getElementById('modalBtn');

        modalIcon.textContent = icon;
        modalTitle.textContent = title;
        modalBody.innerHTML = content;
        modalBtn.textContent = buttonText;
        modalBtn.onclick = buttonAction;
        modal.style.display = 'flex';
    }

    // Fungsi untuk menutup modal
    window.closeModal = () => { // Make it global for inline onclick
        document.getElementById('modal').style.display = 'none';
    }

    // Fungsi untuk menampilkan spinner loading di dalam tombol atau elemen tertentu
    function showLoading(elementId) {
        const element = document.getElementById(elementId);
        if (element) {
            element.innerHTML = '<div class="loading-spinner"></div>'; // Membutuhkan CSS untuk .loading-spinner
            element.disabled = true; // Nonaktifkan tombol saat loading
        }
    }

    // Fungsi untuk menyembunyikan spinner loading dan mengembalikan konten asli tombol/elemen
    function hideLoading(elementId, originalContent) {
        const element = document.getElementById(elementId);
        if (element && originalContent) {
            element.innerHTML = originalContent;
            element.disabled = false; // Aktifkan kembali tombol
        }
    }

    // Fungsi untuk mengambil pengaturan aplikasi dari Firestore
    async function fetchAppSettings() {
        try {
            const settingsDocRef = doc(db, "settings", "app_config");
            const docSnap = await getDoc(settingsDocRef);
            
            if (docSnap.exists()) {
                const settings = docSnap.data();
                wastePrices = settings.wastePrices || {};
                pointsPerKg = settings.pointsPerKg || 100; // Default if not set
                console.log("App settings fetched:", wastePrices, pointsPerKg);
            } else {
                console.warn("App config document 'settings/app_config' not found. Initializing with default values.");
                const defaultWastePrices = {
                    "Botol Plastik": 2500,
                    "Kardus": 2000,
                    "Kertas": 1500,
                    "Logam": 5000,
                    "Kaca": 500,
                    "Campuran": 2000,
                };
                const defaultPointsPerKg = 100;

                await setDoc(settingsDocRef, {
                    wastePrices: defaultWastePrices,
                    pointsPerKg: defaultPointsPerKg,
                    lastUpdated: serverTimestamp()
                });
                wastePrices = defaultWastePrices;
                pointsPerKg = defaultPointsPerKg;
            }
            renderWasteTypeOptions(); // Re-render waste type dropdown after fetching
        } catch (error) {
            console.error("Error fetching app settings:", error);
            alert("Gagal memuat pengaturan aplikasi: " + error.message);
        }
    }

    // Fungsi untuk mengambil daftar rewards dari Firestore
    async function fetchRewards() {
        try {
            const rewardsColRef = collection(db, "rewards");
            const q = query(rewardsColRef, orderBy("cost", "asc"));
            const querySnapshot = await getDocs(q);
            rewards = [];
            if (!querySnapshot.empty) {
                querySnapshot.forEach(doc => {
                    rewards.push({ id: doc.id, ...doc.data() });
                });
                console.log("Rewards fetched:", rewards);
            } else {
                console.warn("Rewards collection is empty. Initializing default rewards.");
                const defaultRewards = [
                    { name: 'Pulsa 10rb', cost: 11000, icon: '📱' },
                    { name: 'Minyak Goreng 1L', cost: 25000, icon: '🍳' },
                    { name: 'Paket Sembako', cost: 50000, icon: '🛍️' },
                    { name: 'Voucher Belanja 25rb', cost: 25000, icon: '🛒' }
                ];
                for (const reward of defaultRewards) {
                    await addDoc(rewardsColRef, reward); 
                }
                rewards = defaultRewards; // Set locally immediately for display
            }
        } catch (error) {
            console.error("Error fetching rewards:", error);
            alert("Gagal memuat data reward: " + error.message);
        }
    }

    // ====================================================================
    // FUNGSI UTAMA & AUTHENTICATION
    // ====================================================================
    // Ambil referensi ke elemen-elemen UI utama yang akan sering diupdate
    const userGreetingEl = document.getElementById('user-greeting');
    const userNameEl = document.getElementById('user-name');
    const userDaysEl = document.getElementById('user-days');
    const userWasteEl = document.getElementById('user-waste');
    const balanceEl = document.getElementById('balance');
    const transactionListEl = document.getElementById('transaction-list');
    const authNavItem = document.getElementById('auth-nav-item');
    const authNavIcon = authNavItem.querySelector('.nav-icon');
    const authNavText = authNavItem.querySelector('.nav-text');
    const wasteTypeSelectCalc = document.getElementById('wasteTypeCalc');
    const adminOperatorToolsBtn = document.getElementById('admin-operator-tools');

    // Listener otentikasi Firebase (berjalan setiap kali status login berubah)
    onAuthStateChanged(auth, async (user) => {
        // Unsubscribe dari listener data pengguna sebelumnya jika ada, untuk menghindari duplikasi
        if (unsubscribeFromUserData) {
            unsubscribeFromUserData();
            unsubscribeFromUserData = null;
        }

        if (user) {
            const userDocRef = doc(db, "users", user.uid);
            
            // Atur listener real-time untuk dokumen pengguna (onSnapshot)
            unsubscribeFromUserData = onSnapshot(userDocRef, (docSnap) => {
                if (docSnap.exists()) {
                    currentUserData = { uid: user.uid, email: user.email, ...docSnap.data() };
                    currentUserData.transactions = currentUserData.transactions || [];
                    // Transactions stored in Firestore could be Timestamps, ensure they are Date objects for formatting
                    currentUserData.transactions.forEach(tx => {
                        if (tx.timestamp && tx.timestamp.toDate) {
                            tx.date = formatDate(tx.timestamp.toDate()); // Ensure tx.date is formatted from timestamp
                        }
                    });
                    console.log("User data updated:", currentUserData.name, "Role:", currentUserData.role);
                    renderDashboard(currentUserData);
                    updateUIForAuthState(true);
                } else {
                    console.log("User document does not exist, initializing for:", user.email);
                    initializeNewUserDocument(user);
                }
            }, (error) => {
                console.error("Error listening to user data:", error);
                alert("Gagal memuat data pengguna: " + error.message);
                currentUserData = guestData;
                updateUIForAuthState(false);
                renderDashboard(currentUserData);
            });
        } else {
            currentUserData = guestData;
            console.log("User logged out.");
            updateUIForAuthState(false);
            renderDashboard(currentUserData);
        }
    });

    // Fungsi untuk menginisialisasi dokumen pengguna baru di Firestore
    async function initializeNewUserDocument(user) {
        const userDocRef = doc(db, "users", user.uid);
        try {
            await setDoc(userDocRef, {
                name: user.email.split('@')[0] || "Pengguna Baru",
                email: user.email,
                birthdate: null,
                address: null,
                role: 'member',
                balance: 0,
                points: 0,
                activeDays: 0,
                totalWasteKg: 0,
                transactions: [],
                createdAt: serverTimestamp(),
                lastActiveDate: null
            }, { merge: true });
            console.log("New user document (or merged) initialized for:", user.email);
        } catch (error) {
            console.error("Error initializing new user document:", error);
            alert("Gagal menginisialisasi data pengguna baru: " + error.message);
        }
    }

    // Fungsi untuk memperbarui tampilan UI berdasarkan status login
    function updateUIForAuthState(isLoggedIn) {
        if (isLoggedIn) {
            authNavIcon.textContent = '🔓'; // Icon untuk Logout
            authNavText.textContent = 'Logout';
            userGreetingEl.textContent = 'Selamat datang,';
            
            if (currentUserData.role === 'admin' || currentUserData.role === 'operator') {
                adminOperatorToolsBtn.style.display = 'block';
            } else {
                adminOperatorToolsBtn.style.display = 'none';
            }
        } else {
            authNavIcon.textContent = '🔑'; // Icon untuk Login
            authNavText.textContent = 'Login';
            userGreetingEl.textContent = 'Silakan login';
            transactionListEl.innerHTML = '<p style="text-align:center; color:#999;">Login untuk melihat riwayat transaksi.</p>';
            adminOperatorToolsBtn.style.display = 'none';
        }
    }
    
    // Handler klik tombol Login/Logout di navigasi bawah
    window.handleAuthClick = () => {
        if (currentUserData && currentUserData.uid) {
            signOut(auth).then(() => {
                alert("Anda berhasil logout.");
            }).catch((error) => {
                alert("Gagal logout: " + error.message);
                console.error("Logout error:", error);
            });
        } else {
            showLoginForm();
        }
    }

    // ====================================================================
    // FUNGSI RENDER DASHBOARD (Memperbarui tampilan utama)
    // ====================================================================
    function renderDashboard(data) {
        userNameEl.textContent = data.name;
        userDaysEl.textContent = data.activeDays || 0;
        userWasteEl.textContent = `${(data.totalWasteKg || 0).toLocaleString('id-ID', { maximumFractionDigits: 2 })}kg`;
        balanceEl.textContent = `Rp ${(data.balance || 0).toLocaleString('id-ID')}`;
        
        transactionListEl.innerHTML = '';
        if (data.transactions && data.transactions.length > 0) {
            const sortedTransactions = [...data.transactions].sort((a, b) => {
                const dateA = a.timestamp && a.timestamp.toDate ? a.timestamp.toDate() : new Date(0); // Fallback to epoch if no timestamp
                const dateB = b.timestamp && b.timestamp.toDate ? b.timestamp.toDate() : new Date(0);
                return dateB.getTime() - dateA.getTime();
            });

            const recentTransactions = sortedTransactions.slice(0, 5); 

            if (recentTransactions.length > 0) {
                recentTransactions.forEach(tx => {
                    const amountClass = tx.type;
                    const amountSign = tx.amount > 0 ? '+' : '';
                    const icon = tx.type === 'setor' ? '📥' : (tx.type === 'tarik' ? '📤' : '🎁');
                    const displayAmount = Math.abs(tx.amount).toLocaleString('id-ID');
                    const displayDate = tx.timestamp && tx.timestamp.toDate ? formatDate(tx.timestamp.toDate()) : formatDate(tx.date); // Use formatDate for tx.date too
                    
                    const txItemHTML = `
                        <div class="transaction-item ${tx.type}">
                            <div class="transaction-icon ${tx.type}">${icon}</div>
                            <div class="transaction-info">
                                <div class="transaction-title">${tx.title}</div>
                                <div class="transaction-detail">${tx.detail}</div>
                                <div class="transaction-date">${displayDate}</div>
                            </div>
                            <div class="transaction-amount ${amountClass}">${tx.amount < 0 ? '-' : amountSign}Rp ${displayAmount}</div>
                        </div>
                    `;
                    transactionListEl.insertAdjacentHTML('beforeend', txItemHTML);
                });
            } else {
                transactionListEl.innerHTML = '<p style="text-align:center; color:#999;">Belum ada transaksi terbaru.</p>';
            }
        } else if (currentUserData && currentUserData.uid) {
            transactionListEl.innerHTML = '<p style="text-align:center; color:#999;">Belum ada transaksi.</p>';
        } else {
             transactionListEl.innerHTML = '<p style="text-align:center; color:#999;">Login untuk melihat riwayat transaksi.</p>';
        }

        renderWasteTypeOptions();
    }

    // Fungsi untuk mengisi dropdown jenis sampah di kalkulator dan setor sampah
    function renderWasteTypeOptions() {
        wasteTypeSelectCalc.innerHTML = '<option value="" data-price="0">Pilih Jenis Sampah</option>';
        for (const [name, price] of Object.entries(wastePrices)) {
            wasteTypeSelectCalc.insertAdjacentHTML('beforeend', `<option value="${name}" data-price="${price}">${name} (Rp ${price.toLocaleString('id-ID')}/kg)</option>`);
        }
    }
    
    // ====================================================================
    // FUNGSI MODAL (Interaksi Pop-up)
    // ====================================================================
    // Fungsi-fungsi showModal dan closeModal sudah di refactor ke Helper Functions di atas.

    // ====================================================================
    // FUNGSI LOGIN, REGISTRASI, & PROFIL
    // ====================================================================
    window.showLoginForm = () => {
        const formHTML = `
            <div class="modal-form">
                <input type="email" id="loginEmail" placeholder="Email" required>
                <div class="password-wrapper">
                    <input type="password" id="loginPassword" placeholder="Password" required>
                    <button type="button" class="password-toggle" onclick="togglePasswordVisibility('loginPassword')">👁️</button>
                </div>
                <button class="modal-btn" id="loginBtn" onclick="handleLogin()">Login</button>
                <button class="modal-btn secondary" onclick="showRegistrationForm()">Belum punya akun? Daftar</button>
                <a href="#" class="modal-link" onclick="showResetPassword()">Lupa password?</a>
            </div>
        `;
        createModal('🔑', 'Login Pengguna', formHTML, '', () => {});
    }

    window.handleLogin = async () => {
        const loginBtn = document.getElementById('loginBtn');
        const originalBtnText = loginBtn.innerHTML;
        showLoading('loginBtn');

        const email = document.getElementById('loginEmail').value;
        const password = document.getElementById('loginPassword').value;
        
        if (!email || !password) {
            alert("Email dan password harus diisi.");
            hideLoading('loginBtn', originalBtnText);
            return;
        }

        try {
            await signInWithEmailAndPassword(auth, email, password);
            closeModal();
            alert(`Selamat datang kembali!`);
        } catch (error) {
            alert("Login Gagal: " + error.message);
            console.error("Login error:", error);
        } finally {
            hideLoading('loginBtn', originalBtnText);
        }
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
                    <button type="button" class="password-toggle" onclick="togglePasswordVisibility('regPassword')">👁️</button>
                </div>
                
                <label for="regBirthdate">Tanggal Lahir (Opsional)</label>
                <input type="date" id="regBirthdate">
                
                <label for="regAddress">Alamat (Opsional)</label>
                <input type="text" id="regAddress" placeholder="Contoh: Dusun Citambal RT 01/RW 01">
                
                <button class="modal-btn" id="registerBtn" onclick="handleRegistration()">Daftar Sekarang</button>
                <button class="modal-btn secondary" onclick="showLoginForm()">Sudah punya akun? Login</button>
            </div>
        `;
        createModal('📝', 'Daftar Akun Baru', formHTML, '', () => {});
    };

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
            alert("Nama, Email, dan Password wajib diisi!");
            hideLoading('registerBtn', originalBtnText);
            return;
        }
        if (password.length < 6) {
            alert("Password minimal 6 karakter.");
            hideLoading('registerBtn', originalBtnText);
            return;
        }

        try {
            const userCredential = await createUserWithEmailAndPassword(auth, email, password);
            const user = userCredential.user;
            
            await setDoc(doc(db, "users", user.uid), {
                name: name,
                email: email,
                birthdate: birthdate || null,
                address: address || null,
                role: 'member',
                balance: 0,
                points: 0,
                activeDays: 0,
                totalWasteKg: 0,
                transactions: [],
                createdAt: serverTimestamp(),
                lastActiveDate: null 
            });
            closeModal();
            alert("Pendaftaran berhasil! Anda akan otomatis login.");
        } catch (error) {
            alert("Pendaftaran Gagal: " + error.message);
            console.error("Registration error:", error);
        } finally {
            hideLoading('registerBtn', originalBtnText);
        }
    };

    window.showProfil = () => {
        if (!currentUserData || !currentUserData.uid) {
            createModal('👤', 'Profil Pengguna', '<p class="modal-text">Silakan login untuk melihat profil Anda.</p>');
            return;
        }
        const profileHTML = `
            <div class="profile-data-item"><strong>Nama:</strong> ${currentUserData.name || '-'}</div>
            <div class="profile-data-item"><strong>Email:</strong> ${currentUserData.email || '-'}</div>
            <div class="profile-data-item"><strong>Tgl Lahir:</strong> ${currentUserData.birthdate || '-'}</div>
            <div class="profile-data-item"><strong>Alamat:</strong> ${currentUserData.address || '-'}</div>
            <button class="modal-btn secondary" id="resetPassBtn" onclick="showResetPassword()" style="margin-top: 20px;">Ganti Password</button>
        `;
        createModal('👤', 'Profil Pengguna', profileHTML);
    }
    
    window.showResetPassword = () => {
        const email = currentUserData && currentUserData.uid ? currentUserData.email : '';
        const formHTML = `
            <div class="modal-form">
                <label for="resetEmail">Email Anda</label>
                <input type="email" id="resetEmail" value="${email}" placeholder="Masukkan email terdaftar" required>
                <button class="modal-btn" id="sendResetBtn" onclick="handleResetPassword()">Kirim Link Reset Password</button>
            </div>
        `;
        createModal('🔑', 'Reset Password', formHTML, 'Kembali', showLoginForm);
    };

    window.handleResetPassword = async () => {
        const sendResetBtn = document.getElementById('sendResetBtn');
        const originalBtnText = sendResetBtn.innerHTML;
        showLoading('sendResetBtn');

        const email = document.getElementById('resetEmail').value;
        if (!email) {
            alert("Email harus diisi.");
            hideLoading('sendResetBtn', originalBtnText);
            return;
        }
        try {
            await sendPasswordResetEmail(auth, email);
            alert(`Email untuk reset password telah dikirim ke ${email}. Silakan cek kotak masuk Anda.`);
            closeModal();
        } catch (error) {
            alert("Gagal mengirim email: " + error.message);
            console.error("Reset password error:", error);
        } finally {
            hideLoading('sendResetBtn', originalBtnText);
        }
    };

    // ====================================================================
    // FUNGSI FITUR-FITUR BARU & INTERAKSI DATA
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
        createModal('⭐', 'Event & Reward', contentHTML, 'Tutup');
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
        createModal('🏞️', 'Citambal Nu Urang', contentHTML, 'Tutup');
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
        createModal('🏪', 'Daftar UMKM Citambal', umkmHTML, 'Kembali', showCnuMenu);
    };

    window.showAirBersihMenu = () => {
        const airHTML = `
            <p class="modal-text">Layanan pengelolaan Air Bersih Gunung Tumpeng. Pembayaran bisa menggunakan saldo tabungan sampah.</p>
            <button class="modal-btn" onclick="alert('Fitur Pendaftaran Air Bersih akan segera tersedia.')">📝 Daftar Sambungan Baru</button>
            <button class="modal-btn" onclick="alert('Fitur Bayar Tagihan Air akan segera tersedia.')">💳 Bayar Tagihan Air</button>
            <button class="modal-btn secondary" onclick="alert('Fitur Riwayat Pembayaran akan segera tersedia.')">📊 Lihat Riwayat</button>
        `;
        createModal('💧', 'Air Bersih Gunung Tumpeng', airHTML, 'Kembali', showCnuMenu);
    };
    
    // ====================================================================
    // FUNGSI TRANSAKSI & POIN (Implementasi Nyata)
    // ====================================================================

    window.showTukarPoin = () => {
        if (!currentUserData || !currentUserData.uid) { 
            createModal('⚠️', 'Akses Ditolak', '<p class="modal-text">Silakan login untuk menukar poin Anda.</p>');
            return; 
        }
        
        let rewardItemsHTML = '';
        if (rewards.length === 0) {
            rewardItemsHTML = '<p style="text-align:center; color:#999;">Belum ada reward yang tersedia.</p>';
        } else {
            rewards.forEach(reward => {
                const canRedeem = (currentUserData.points || 0) >= reward.cost;
                rewardItemsHTML += `
                    <div class="reward-item">
                        <div class="reward-item-icon">${reward.icon}</div>
                        <div class="reward-item-info">
                            <div class="reward-item-name">${reward.name}</div>
                            <div class="reward-item-cost">${reward.cost.toLocaleString('id-ID')} Poin</div>
                        </div>
                        <button class="reward-item-btn" id="redeem-${reward.id}" onclick="processRedeem('${reward.id}', this)" ${!canRedeem ? 'disabled' : ''}>Tukar</button>
                    </div>
                `;
            });
        }

        const tukarPoinHTML = `
            <div class="points-balance">Poin Anda Saat Ini: <br> <span id="current-points">${(currentUserData.points || 0).toLocaleString('id-ID')} Poin</span></div>
            <div class="reward-list">${rewardItemsHTML}</div>
        `;
        createModal('🎁', 'Tukar Poin Reward', tukarPoinHTML, 'Selesai');
    }

    window.processRedeem = async (rewardId, buttonElement) => {
        if (!currentUserData || !currentUserData.uid) {
            alert("Anda harus login untuk menukar poin.");
            return;
        }

        const originalBtnText = buttonElement ? buttonElement.innerHTML : 'Tukar';
        if (buttonElement) showLoading(buttonElement.id);

        const reward = rewards.find(r => r.id === rewardId);
        if (!reward) {
            alert("Reward tidak ditemukan.");
            if (buttonElement) hideLoading(buttonElement.id, originalBtnText);
            return;
        }

        if ((currentUserData.points || 0) < reward.cost) {
            alert("Poin Anda tidak cukup untuk menukar reward ini.");
            if (buttonElement) hideLoading(buttonElement.id, originalBtnText);
            return;
        }

        if (!confirm(`Apakah Anda yakin ingin menukar ${reward.cost.toLocaleString('id-ID')} Poin untuk ${reward.name}?`)) {
            if (buttonElement) hideLoading(buttonElement.id, originalBtnText);
            return;
        }

        try {
            const userDocRef = doc(db, "users", currentUserData.uid);
            
            let newActiveDays = currentUserData.activeDays || 0;
            let lastActiveDate = currentUserData.lastActiveDate; // Firestore Timestamp object
            const today = new Date(); // Current date for comparison

            // Check if last active date is not today, then increment active days
            const lastActiveDateObj = lastActiveDate ? lastActiveDate.toDate() : null;
            if (!lastActiveDateObj || !isSameDay(lastActiveDateObj, today)) {
                newActiveDays++;
            }

            const newTransaction = {
                type: 'reward',
                title: `Penukaran Poin: ${reward.name}`,
                detail: `Poin berkurang ${reward.cost.toLocaleString('id-ID')}`,
                amount: -reward.cost, // Amount is negative for a debit
                timestamp: serverTimestamp(),
            };

            await updateDoc(userDocRef, {
                points: (currentUserData.points || 0) - reward.cost,
                transactions: arrayUnion(newTransaction),
                activeDays: newActiveDays,
                lastActiveDate: serverTimestamp() // Update last active date to now (server time)
            });
            
            alert(`Berhasil menukar ${reward.name}!`);
            closeModal();
        } catch (error) {
            console.error("Error redeeming points:", error);
            alert("Gagal menukar poin: " + error.message);
        } finally {
            if (buttonElement) hideLoading(buttonElement.id, originalBtnText);
        }
    }

    window.showSetorSampah = () => {
        if (!currentUserData || !currentUserData.uid) { 
            createModal('⚠️', 'Akses Ditolak', '<p class="modal-text">Silakan login untuk mencatat setoran sampah Anda.</p>');
            return; 
        }

        let wasteOptions = '';
        for (const [name, price] of Object.entries(wastePrices)) {
            wasteOptions += `<option value="${name}" data-price="${price}">${name} (Rp ${price.toLocaleString('id-ID')}/kg)</option>`;
        }
        if (Object.keys(wastePrices).length === 0) {
             wasteOptions += '<option value="" disabled>Belum ada jenis sampah tersedia</option>';
        }

        const formHTML = `
            <div class="modal-form">
                <label for="setorWasteType">Jenis Sampah</label>
                <select id="setorWasteType" required>${wasteOptions}</select>
                
                <label for="setorWasteWeight">Berat (kg)</label>
                <input type="number" id="setorWasteWeight" placeholder="Masukkan berat sampah (kg)" step="0.1" min="0.1" required>
                
                <button class="modal-btn" id="setorBtn" onclick="processSetorSampah()">Catat Setoran</button>
            </div>
        `;
        createModal('🗑️', 'Setor Sampah', formHTML, '', () => {});
    };

    window.processSetorSampah = async () => {
        if (!currentUserData || !currentUserData.uid) {
            alert("Anda harus login untuk mencatat setoran.");
            return;
        }

        const setorBtn = document.getElementById('setorBtn');
        const originalBtnText = setorBtn.innerHTML;
        showLoading('setorBtn');

        const wasteTypeSelect = document.getElementById('setorWasteType');
        const wasteWeightInput = document.getElementById('setorWasteWeight');

        const selectedWasteType = wasteTypeSelect.value;
        const wasteWeight = parseFloat(wasteWeightInput.value);

        if (!selectedWasteType || !wasteWeight || wasteWeight <= 0) {
            alert("Mohon pilih jenis sampah dan masukkan berat yang valid (minimal 0.1 kg).");
            hideLoading('setorBtn', originalBtnText);
            return;
        }

        const wastePricePerKg = wastePrices[selectedWasteType];
        if (!wastePricePerKg) {
            alert("Jenis sampah tidak valid atau harganya belum ditentukan.");
            hideLoading('setorBtn', originalBtnText);
            return;
        }

        const earnedAmount = wasteWeight * wastePricePerKg;
        const earnedPoints = wasteWeight * pointsPerKg;

        if (!confirm(`Anda akan menyetorkan ${wasteWeight} kg ${selectedWasteType}.\nEstimasi Saldo: Rp ${earnedAmount.toLocaleString('id-ID')}\nEstimasi Poin: ${earnedPoints.toLocaleString('id-ID')} Poin\n\nLanjutkan?`)) {
            hideLoading('setorBtn', originalBtnText);
            return;
        }

        try {
            const userDocRef = doc(db, "users", currentUserData.uid);
            
            let newActiveDays = currentUserData.activeDays || 0;
            let lastActiveDate = currentUserData.lastActiveDate;
            const today = new Date(); // Current date for comparison
            const lastActiveDateObj = lastActiveDate ? lastActiveDate.toDate() : null;
            if (!lastActiveDateObj || !isSameDay(lastActiveDateObj, today)) {
                newActiveDays++;
            }

            const newBalance = (currentUserData.balance || 0) + earnedAmount;
            const newPoints = (currentUserData.points || 0) + earnedPoints;
            const newTotalWasteKg = (currentUserData.totalWasteKg || 0) + wasteWeight;

            const newTransaction = {
                type: 'setor',
                title: `Setor Sampah: ${selectedWasteType}`,
                detail: `${wasteWeight} kg`,
                amount: earnedAmount,
                timestamp: serverTimestamp(),
            };

            await updateDoc(userDocRef, {
                balance: newBalance,
                points: newPoints,
                totalWasteKg: newTotalWasteKg,
                activeDays: newActiveDays,
                lastActiveDate: serverTimestamp(), // Update last active date to now (server time)
                transactions: arrayUnion(newTransaction)
            });

            alert(`Setoran berhasil dicatat!`);
            closeModal();
        } catch (error) {
            console.error("Error processing waste deposit:", error);
            alert("Gagal mencatat setoran: " + error.message);
        } finally {
            hideLoading('setorBtn', originalBtnText);
        }
    };

    window.showTarikSaldo = () => {
        if (!currentUserData || !currentUserData.uid) { 
            createModal('⚠️', 'Akses Ditolak', '<p class="modal-text">Silakan login untuk melakukan penarikan saldo.</p>');
            return; 
        }

        const formHTML = `
            <div class="modal-form">
                <label for="withdrawAmount">Jumlah Penarikan (Rp)</label>
                <input type="number" id="withdrawAmount" placeholder="Min. Rp 10.000" step="1000" min="10000" required>
                
                <p class="modal-text" style="text-align: center; margin-top: 10px;">Saldo Anda Saat Ini: <strong>Rp ${(currentUserData.balance || 0).toLocaleString('id-ID')}</strong></p>

                <button class="modal-btn" id="withdrawBtn" onclick="processTarikSaldo()">Tarik Saldo</button>
            </div>
        `;
        createModal('💵', 'Tarik Saldo', formHTML, '', () => {});
    };

    window.processTarikSaldo = async () => {
        if (!currentUserData || !currentUserData.uid) {
            alert("Anda harus login untuk melakukan penarikan.");
            return;
        }

        const withdrawBtn = document.getElementById('withdrawBtn');
        const originalBtnText = withdrawBtn.innerHTML;
        showLoading('withdrawBtn');

        const withdrawAmountInput = document.getElementById('withdrawAmount');
        const amount = parseFloat(withdrawAmountInput.value);

        if (isNaN(amount) || amount <= 0) {
            alert("Jumlah penarikan tidak valid.");
            hideLoading('withdrawBtn', originalBtnText);
            return;
        }
        if (amount < 10000) {
            alert("Jumlah penarikan minimal adalah Rp 10.000.");
            hideLoading('withdrawBtn', originalBtnText);
            return;
        }
        if (amount > currentUserData.balance) {
            alert("Saldo Anda tidak cukup untuk penarikan ini.");
            hideLoading('withdrawBtn', originalBtnText);
            return;
        }

        if (!confirm(`Apakah Anda yakin ingin menarik saldo sebesar Rp ${amount.toLocaleString('id-ID')}?`)) {
            hideLoading('withdrawBtn', originalBtnText);
            return;
        }

        try {
            const userDocRef = doc(db, "users", currentUserData.uid);
            
            let newActiveDays = currentUserData.activeDays || 0;
            let lastActiveDate = currentUserData.lastActiveDate;
            const today = new Date(); // Current date for comparison
            const lastActiveDateObj = lastActiveDate ? lastActiveDate.toDate() : null;
            if (!lastActiveDateObj || !isSameDay(lastActiveDateObj, today)) {
                newActiveDays++;
            }

            const newBalance = currentUserData.balance - amount;

            const newTransaction = {
                type: 'tarik',
                title: `Penarikan Saldo`,
                detail: `Tunai`,
                amount: -amount, // Amount is negative for a debit
                timestamp: serverTimestamp(),
            };

            await updateDoc(userDocRef, {
                balance: newBalance,
                transactions: arrayUnion(newTransaction),
                activeDays: newActiveDays,
                lastActiveDate: serverTimestamp() // Update last active date to now (server time)
            });

            alert(`Penarikan berhasil dicatat!`);
            closeModal();
        } catch (error) {
            console.error("Error processing withdrawal:", error);
            alert("Gagal mencatat penarikan: " + error.message);
        } finally {
            hideLoading('withdrawBtn', originalBtnText);
        }
    };


    // ====================================================================
    // FUNGSI LAINNYA & LEADERBOARD DINAMIS
    // ====================================================================
    
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

    // Fungsi Kalkulator Harga Sampah
    window.calculateWaste = () => {
        const wasteTypeSelect = document.getElementById("wasteTypeCalc");
        const wasteWeightInput = document.getElementById("wasteWeight");
        const calculatorResultEl = document.getElementById("calculatorResult");
        const estimatedPriceEl = document.getElementById("estimatedPrice");

        const selectedOption = wasteTypeSelect.options[wasteTypeSelect.selectedIndex];
        const pricePerKg = parseFloat(selectedOption.getAttribute("data-price"));
        const wasteWeight = parseFloat(wasteWeightInput.value);

        calculatorResultEl.style.display = "block";

        if (isNaN(pricePerKg) || pricePerKg === 0 || isNaN(wasteWeight) || wasteWeight <= 0) {
            calculatorResultEl.style.background = "rgba(231, 76, 60, 0.5)"; // Merah untuk error
            estimatedPriceEl.textContent = "Pilih jenis & isi berat yang valid";
            return;
        }

        const estimatedPrice = pricePerKg * wasteWeight;
        calculatorResultEl.style.background = "rgba(255,255,255,0.1)"; // Kembali normal
        estimatedPriceEl.textContent = `Rp ${estimatedPrice.toLocaleString("id-ID")}`;
    }

    // Fungsi untuk mengatur navigasi aktif di bottom bar
    window.setActiveNav=(el)=>{
        document.querySelectorAll(".nav-item").forEach(item=>item.classList.remove("active"));
        el.classList.add("active");
    }

    // Fungsi untuk menampilkan modal Hubungi Admin
    window.showContactAdmin=()=>{
        const contentHTML = `<p class="modal-text">Jika Anda memiliki pertanyaan atau kendala, silakan hubungi admin kami melalui WhatsApp.</p><a href="https://wa.me/6281322355056?text=Halo%20Admin%20Bank%20Sampah%20ARAS" target="_blank" class="contact-link">💬 Hubungi via WhatsApp</a><p class="modal-text" style="font-size: 12px; text-align: center; margin-top: 15px;">Jam Operasional Admin: 08:00 - 17:00 WIB</p>`;
        createModal("📞","Hubungi Admin",contentHTML);
    }

    // Fungsi placeholder untuk Transfer (perlu implementasi lebih lanjut jika dibutuhkan)
    window.showTransfer=()=>{
        if(!currentUserData || !currentUserData.uid){createModal("⚠️","Akses Ditolak",'<p class="modal-text">Silakan login untuk melakukan transfer.</p>'); return};
        createModal("💸","Transfer & Tarik Saldo",'<p class="modal-text">Anda dapat mentransfer saldo tabungan sampah Anda ke rekening bank atau menariknya secara tunai di lokasi Bank Sampah ARAS. Hubungi petugas untuk melakukan transaksi.</p>')
    }

    // Fungsi placeholder untuk Isi Saldo (saldo otomatis bertambah dari setor sampah)
    window.showIsiSaldo=()=>{
        createModal("➕","Cara Mengisi Saldo",'<p class="modal-text">Saldo Anda bertambah setiap kali Anda menyetorkan sampah yang memiliki nilai jual. Semakin banyak sampah yang Anda setor, semakin besar saldo tabungan Anda!</p>')
    }
    
    // Fungsi untuk melihat riwayat aktivitas lengkap
    window.showActivityHistory = () => {
        if (!currentUserData || !currentUserData.uid) {
            createModal("⚠️", "Akses Ditolak", '<p class="modal-text">Silakan login untuk melihat riwayat aktivitas.</p>');
            return;
        }
        let transactionsHtml = '<p style="text-align:center; color:#999;">Belum ada riwayat aktivitas.</p>';
        if (currentUserData.transactions && currentUserData.transactions.length > 0) {
            const sortedTransactions = [...currentUserData.transactions].sort((a, b) => {
                const dateA = a.timestamp && a.timestamp.toDate ? a.timestamp.toDate() : new Date(0);
                const dateB = b.timestamp && b.timestamp.toDate ? b.timestamp.toDate() : new Date(0);
                return dateB.getTime() - dateA.getTime();
            });
            transactionsHtml = sortedTransactions.map(tx => {
                const amountClass = tx.type;
                const amountSign = tx.amount > 0 ? '+' : '';
                const icon = tx.type === 'setor' ? '📥' : (tx.type === 'tarik' ? '📤' : '🎁');
                const displayAmount = Math.abs(tx.amount).toLocaleString('id-ID');
                const displayDate = tx.timestamp && tx.timestamp.toDate ? formatDate(tx.timestamp.toDate()) : formatDate(tx.date);
                return `
                    <div class="transaction-item ${tx.type}">
                        <div class="transaction-icon ${tx.type}">${icon}</div>
                        <div class="transaction-info">
                            <div class="transaction-title">${tx.title}</div>
                            <div class="transaction-detail">${tx.detail}</div>
                            <div class="transaction-date">${displayDate}</div>
                        </div>
                        <div class="transaction-amount ${amountClass}">${tx.amount < 0 ? '-' : amountSign}Rp ${displayAmount}</div>
                    </div>
                `;
            }).join('');
        }
        createModal("📊","Riwayat Aktivitas",`<div id="modal-activity-list" style="max-height: 300px; overflow-y: auto;">${transactionsHtml}</div>`);
    }

    // Fungsi untuk menampilkan daftar harga sampah
    window.showHarga=()=>{
        let contentHTML = "Daftar harga sampah saat ini (per kg):\n\n";
        if (Object.keys(wastePrices).length === 0) {
            contentHTML += "Belum ada data harga sampah yang tersedia.";
        } else {
            for(const [type, price] of Object.entries(wastePrices)) {
                contentHTML += `• ${type}: Rp ${price.toLocaleString("id-ID")}\n`;
            }
        }
        contentHTML += "\n*Harga dapat berubah sewaktu-waktu.";
        createModal("💰","Daftar Harga Sampah",`<p class="modal-text">${contentHTML}</p>`);
    }

    // Fungsi untuk menampilkan jadwal operasional
    window.showJadwal=()=>{
        createModal("📅","Jadwal Operasional",'<p class="modal-text">Bank Sampah ARAS beroperasi pada:\n\n• Hari: Selasa & Jumat\n• Jam: 08:00 - 16:00 WIB\n\nUntuk permintaan pickup, hubungi pengurus H-1.</p>')
    }

    // Fungsi untuk menampilkan panduan (placeholder)
    window.showPanduan = () => {
        createModal('📖', 'Panduan Penggunaan', '<p class="modal-text">Panduan lengkap penggunaan aplikasi Bank Sampah ARAS akan segera tersedia di sini. Silakan login atau hubungi admin untuk informasi lebih lanjut.</p>');
    };
    
    // Fungsi untuk menampilkan Leaderboard
    window.showLeaderboard = async () => {
        let leaderboardHtml = '';
        try {
            createModal("🏆","Memuat Leaderboard...", '<div class="loading-spinner"></div>', '', () => {});

            const usersRef = collection(db, "users");
            const q = query(usersRef, orderBy("totalWasteKg", "desc"), limit(10)); 
            const querySnapshot = await getDocs(q);

            const leaderboardData = [];
            querySnapshot.forEach((doc) => {
                const data = doc.data();
                leaderboardData.push({
                    id: doc.id,
                    name: data.name,
                    totalWasteKg: data.totalWasteKg || 0,
                    isCurrentUser: currentUserData && doc.id === currentUserData.uid
                });
            });

            if (leaderboardData.length === 0) {
                leaderboardHtml = '<p class="modal-text">Belum ada data leaderboard.</p>';
            } else {
                leaderboardHtml += '<ul class="leaderboard-list">';
                leaderboardData.forEach((user, index) => {
                    const rank = index + 1;
                    const highlightClass = user.isCurrentUser ? ' style="background-color: #e0ffe0; border-color: #2ecc71;"' : ''; 
                    leaderboardHtml += `
                        <li class="leaderboard-item"${highlightClass}>
                            <span class="leaderboard-rank">#${rank}</span>
                            <span class="leaderboard-name">${user.name}</span>
                            <span class="leaderboard-value">${user.totalWasteKg.toLocaleString('id-ID', { maximumFractionDigits: 2 })} kg</span>
                        </li>
                    `;
                });
                leaderboardHtml += '</ul>';
                
                if (currentUserData && currentUserData.uid && currentUserData.role === 'member' && !leaderboardData.some(u => u.isCurrentUser)) {
                    leaderboardHtml += `<p class="leaderboard-note">Anda belum masuk Top 10. Terus setorkan sampah Anda! (<span style="font-weight: bold;">Anda: ${currentUserData.totalWasteKg.toLocaleString('id-ID', { maximumFractionDigits: 2 })} kg</span>)</p>`;
                } else if (!currentUserData || !currentUserData.uid) {
                    leaderboardHtml += `<p class="leaderboard-note">Login untuk melihat peringkat Anda.</p>`;
                }
            }

            createModal("🏆","Leaderboard Nasabah", leaderboardHtml);

        } catch (error) {
            console.error("Error fetching leaderboard data:", error);
            createModal("⚠️","Gagal Memuat Leaderboard", '<p class="modal-text">Terjadi kesalahan saat memuat data leaderboard. Silakan coba lagi nanti.</p>');
        }
    };
    
    // ====================================================================
    // ADMIN / OPERATOR FUNGSI
    // ====================================================================

    window.showAdminOperatorPanel = () => {
        if (!currentUserData || (currentUserData.role !== 'admin' && currentUserData.role !== 'operator')) {
            alert("Akses ditolak. Anda bukan Admin atau Operator.");
            return;
        }

        let contentHTML = `
            <p class="modal-text">Selamat datang, ${currentUserData.name} (${currentUserData.role}).</p>
            <div class="modal-menu-grid">
                <div class="feature-item" onclick="showManagePricesModal()">
                    <div class="feature-icon">💸</div>
                    <div class="feature-text">Kelola Harga Sampah</div>
                </div>
                <div class="feature-item" onclick="showManageRewardsModal()">
                    <div class="feature-icon">🎁</div>
                    <div class="feature-text">Kelola Reward</div>
                </div>
        `;
        if (currentUserData.role === 'admin') {
            contentHTML += `
                <div class="feature-item" onclick="showManageUsersModal()">
                    <div class="feature-icon">👥</div>
                    <div class="feature-text">Kelola Pengguna</div>
                </div>
            `;
        }
        contentHTML += `</div>`;
        createModal('⚙️', 'Panel Admin/Operator', contentHTML, 'Tutup');
    };

    window.showManagePricesModal = () => {
        if (!currentUserData || (currentUserData.role !== 'admin' && currentUserData.role !== 'operator')) {
            alert("Akses ditolak.");
            return;
        }

        let pricesHtml = '<div class="modal-form">';
        for (const [type, price] of Object.entries(wastePrices)) {
            pricesHtml += `
                <div class="admin-form-item">
                    <label for="price-${type}">Jenis: ${type}</label>
                    <input type="number" id="price-${type}" value="${price}" min="0" step="100">
                    <div class="admin-form-actions">
                        <button class="modal-btn secondary delete" id="delete-price-${type}" onclick="deleteWasteType('${type}')">Hapus</button>
                    </div>
                </div>
            `;
        }
        pricesHtml += `
            <hr style="margin: 20px 0;">
            <h3>Tambah Jenis Sampah Baru</h3>
            <label for="newWasteType">Nama Jenis Sampah</label>
            <input type="text" id="newWasteType" placeholder="Nama Jenis Sampah">
            <label for="newWastePrice">Harga (Rp/kg)</label>
            <input type="number" id="newWastePrice" placeholder="Harga per kg" min="0" step="100">
            <button class="modal-btn" id="addPriceBtn" onclick="addWasteType()">Tambah Jenis</button>
            <button class="modal-btn" id="savePricesBtn" onclick="saveWastePrices()">Simpan Perubahan</button>
            </div>
        `;
        createModal('💸', 'Kelola Harga Sampah', pricesHtml, 'Kembali', showAdminOperatorPanel);
    };

    window.addWasteType = async () => {
        const newType = document.getElementById('newWasteType').value.trim();
        const newPrice = parseFloat(document.getElementById('newWastePrice').value);

        if (!newType || isNaN(newPrice) || newPrice < 0) {
            alert("Nama jenis sampah dan harga harus valid.");
            return;
        }
        if (wastePrices[newType]) {
            alert(`Jenis sampah "${newType}" sudah ada. Gunakan 'Simpan Perubahan' untuk mengeditnya.`);
            return;
        }

        // Add to local state first for immediate display
        wastePrices[newType] = newPrice;
        document.getElementById('newWasteType').value = '';
        document.getElementById('newWastePrice').value = '';
        // No need to call savePrices here, it will be done explicitly via savePricesBtn
        showManagePricesModal(); // Re-render modal to show new item
    };

    window.deleteWasteType = (typeToDelete) => {
        if (confirm(`Apakah Anda yakin ingin menghapus jenis sampah "${typeToDelete}"?`)) {
            delete wastePrices[typeToDelete]; // Delete from local state
            showManagePricesModal(); // Re-render modal to reflect deletion
        }
    };

    window.saveWastePrices = async () => {
        const saveBtn = document.getElementById('savePricesBtn');
        const originalBtnText = saveBtn.innerHTML;
        showLoading('savePricesBtn');

        const updatedPrices = {};
        // Get prices from the currently displayed modal form (includes existing and newly added unsaved ones)
        const priceInputs = document.querySelectorAll('.admin-form-item input[id^="price-"]');
        priceInputs.forEach(input => {
            const type = input.id.replace('price-', '');
            const price = parseFloat(input.value);
            if (!isNaN(price) && price >= 0) {
                updatedPrices[type] = price;
            }
        });
        
        try {
            await setDoc(doc(db, "settings", "app_config"), { 
                wastePrices: updatedPrices,
                pointsPerKg: pointsPerKg, // Make sure pointsPerKg is preserved
                lastUpdated: serverTimestamp() 
            }, { merge: true }); // Use merge:true to update only wastePrices and lastUpdated without overwriting other settings
            wastePrices = updatedPrices; // Update global local state after successful save
            alert("Harga sampah berhasil diperbarui!");
            closeModal();
            renderDashboard(currentUserData); // Refresh dashboard to update calculator options
        } catch (error) {
            console.error("Error saving waste prices:", error);
            alert("Gagal menyimpan harga sampah: " + error.message);
        } finally {
            hideLoading('savePricesBtn', originalBtnText);
        }
    };

    window.showManageRewardsModal = () => {
        if (!currentUserData || (currentUserData.role !== 'admin' && currentUserData.role !== 'operator')) {
            alert("Akses ditolak.");
            return;
        }

        let rewardsHtml = '<div class="modal-form">';
        rewards.forEach(reward => {
            rewardsHtml += `
                <div class="admin-form-item" id="reward-item-${reward.id}">
                    <label for="reward-name-${reward.id}">Nama Reward</label>
                    <input type="text" id="reward-name-${reward.id}" value="${reward.name}">
                    <label for="reward-cost-${reward.id}">Poin Diperlukan</label>
                    <input type="number" id="reward-cost-${reward.id}" value="${reward.cost}" min="0" step="100">
                    <label for="reward-icon-${reward.id}">Icon</label>
                    <input type="text" id="reward-icon-${reward.id}" value="${reward.icon}" maxlength="2" placeholder="Ex: 🎁">
                    <div class="admin-form-actions">
                        <button class="modal-btn secondary" id="update-reward-${reward.id}" onclick="updateReward('${reward.id}')">Update</button>
                        <button class="modal-btn secondary delete" id="delete-reward-${reward.id}" onclick="deleteReward('${reward.id}')">Hapus</button>
                    </div>
                </div>
            `;
        });
        rewardsHtml += `
            <hr style="margin: 20px 0;">
            <h3>Tambah Reward Baru</h3>
            <label for="newRewardName">Nama Reward</label>
            <input type="text" id="newRewardName" placeholder="Contoh: Voucher Belanja">
            <label for="newRewardCost">Poin Diperlukan</label>
            <input type="number" id="newRewardCost" placeholder="Poin" min="0" step="100">
            <label for="newRewardIcon">Icon</label>
            <input type="text" id="newRewardIcon" placeholder="Ex: 🛍️" maxlength="2">
            <button class="modal-btn" id="addRewardBtn" onclick="addReward()">Tambah Reward</button>
            </div>
        `;
        createModal('🎁', 'Kelola Reward', rewardsHtml, 'Kembali', showAdminOperatorPanel);
    };

    window.addReward = async () => {
        const name = document.getElementById('newRewardName').value.trim();
        const cost = parseFloat(document.getElementById('newRewardCost').value);
        const icon = document.getElementById('newRewardIcon').value.trim();

        if (!name || isNaN(cost) || cost < 0 || !icon) {
            alert("Nama, poin, dan icon reward harus valid.");
            return;
        }

        const addBtn = document.getElementById('addRewardBtn');
        const originalBtnText = addBtn.innerHTML;
        showLoading('addRewardBtn');

        try {
            await addDoc(collection(db, "rewards"), { name, cost, icon });
            await fetchRewards(); // Re-fetch all rewards to update local state
            showManageRewardsModal(); // Re-render modal
            alert("Reward berhasil ditambahkan!");
        } catch (error) {
            console.error("Error adding reward:", error);
            alert("Gagal menambahkan reward: " + error.message);
        } finally {
            hideLoading('addRewardBtn', originalBtnText);
        }
    };

    window.updateReward = async (rewardId) => {
        const name = document.getElementById(`reward-name-${rewardId}`).value.trim();
        const cost = parseFloat(document.getElementById(`reward-cost-${rewardId}`).value);
        const icon = document.getElementById(`reward-icon-${rewardId}`).value.trim();

        if (!name || isNaN(cost) || cost < 0 || !icon) {
            alert("Nama, poin, dan icon reward harus valid.");
            return;
        }

        const updateBtnId = `update-reward-${rewardId}`;
        const updateBtn = document.getElementById(updateBtnId);
        const originalBtnText = updateBtn ? updateBtn.innerHTML : 'Update';
        if (updateBtn) showLoading(updateBtnId);

        try {
            await updateDoc(doc(db, "rewards", rewardId), { name, cost, icon });
            await fetchRewards(); // Re-fetch all rewards to update local state
            alert("Reward berhasil diperbarui!");
            // Re-render modal might be jarring, just alert and let user close or re-open
            // showManageRewardsModal(); 
        } catch (error) {
            console.error("Error updating reward:", error);
            alert("Gagal memperbarui reward: " + error.message);
        } finally {
            if (updateBtn) hideLoading(updateBtnId, originalBtnText);
        }
    };

    window.deleteReward = async (rewardId) => {
        if (!confirm("Apakah Anda yakin ingin menghapus reward ini?")) {
            return;
        }

        const deleteBtnId = `delete-reward-${rewardId}`;
        const deleteBtn = document.getElementById(deleteBtnId);
        const originalBtnText = deleteBtn ? deleteBtn.innerHTML : 'Hapus';
        if (deleteBtn) showLoading(deleteBtnId);

        try {
            await deleteDoc(doc(db, "rewards", rewardId));
            await fetchRewards(); // Re-fetch all rewards to update local state
            showManageRewardsModal(); // Re-render modal to reflect deletion
            alert("Reward berhasil dihapus!");
        } catch (error) {
            console.error("Error deleting reward:", error);
            alert("Gagal menghapus reward: " + error.message);
        } finally {
            if (deleteBtn) hideLoading(deleteBtnId, originalBtnText);
        }
    };
    
    window.showManageUsersModal = async () => {
        if (!currentUserData || currentUserData.role !== 'admin') {
            alert("Akses ditolak. Fitur ini hanya untuk Admin.");
            return;
        }

        createModal("👥", "Memuat Pengguna...", '<div class="loading-spinner"></div>', '', () => {});

        try {
            const usersColRef = collection(db, "users");
            const q = query(usersColRef, orderBy("name", "asc"));
            const querySnapshot = await getDocs(q);

            let usersHtml = '<div class="modal-form">';
            if (querySnapshot.empty) {
                usersHtml += '<p class="modal-text">Belum ada pengguna terdaftar.</p>';
            } else {
                querySnapshot.forEach(userDoc => {
                    const userData = userDoc.data();
                    const userId = userDoc.id;
                    if (userId === currentUserData.uid) return; // Don't allow editing self role via this panel
                    usersHtml += `
                        <div class="admin-form-item">
                            <label>Nama: ${userData.name}</label>
                            <label>Email: ${userData.email}</label>
                            <label for="user-role-${userId}">Role:</label>
                            <select id="user-role-${userId}">
                                <option value="member" ${userData.role === 'member' ? 'selected' : ''}>Member</option>
                                <option value="operator" ${userData.role === 'operator' ? 'selected' : ''}>Operator</option>
                                <option value="admin" ${userData.role === 'admin' ? 'selected' : ''}>Admin</option>
                            </select>
                            <label for="user-balance-${userId}">Saldo (Rp):</label>
                            <input type="number" id="user-balance-${userId}" value="${userData.balance || 0}" step="1">
                            <label for="user-points-${userId}">Poin:</label>
                            <input type="number" id="user-points-${userId}" value="${userData.points || 0}" step="1">
                            <div class="admin-form-actions">
                                <button class="modal-btn secondary" id="update-user-${userId}" onclick="updateUser('${userId}')">Update User</button>
                            </div>
                        </div>
                    `;
                });
            }
            usersHtml += '</div>';
            createModal('👥', 'Kelola Pengguna', usersHtml, 'Kembali', showAdminOperatorPanel);

        } catch (error) {
            console.error("Error fetching users:", error);
            createModal("⚠️", "Gagal Memuat Pengguna", '<p class="modal-text">Terjadi kesalahan saat memuat daftar pengguna.</p>', 'Kembali', showAdminOperatorPanel);
        }
    };

    window.updateUser = async (userId) => {
        if (!currentUserData || currentUserData.role !== 'admin') {
            alert("Akses ditolak.");
            return;
        }
        const userDocRef = doc(db, "users", userId);
        const newRole = document.getElementById(`user-role-${userId}`).value;
        const newBalance = parseFloat(document.getElementById(`user-balance-${userId}`).value);
        const newPoints = parseFloat(document.getElementById(`user-points-${userId}`).value);

        if (isNaN(newBalance) || isNaN(newPoints)) {
            alert("Saldo dan Poin harus berupa angka.");
            return;
        }

        const updateBtnId = `update-user-${userId}`;
        const updateBtn = document.getElementById(updateBtnId);
        const originalBtnText = updateBtn ? updateBtn.innerHTML : 'Update User';
        if (updateBtn) showLoading(updateBtnId);

        try {
            await updateDoc(userDocRef, {
                role: newRole,
                balance: newBalance,
                points: newPoints
            });
            alert(`Pengguna ${userId} berhasil diperbarui.`);
            // No need to re-render all users, Firestore listener will update the modal if it's open.
            // showManageUsersModal(); // Uncomment if you want to force re-render the whole list
        } catch (error) {
            console.error("Error updating user:", error);
            alert("Gagal memperbarui pengguna: " + error.message);
        } finally {
            if (updateBtn) hideLoading(updateBtnId, originalBtnText);
        }
    };


    // ====================================================================
    // INISIALISASI APLIKASI
    // ====================================================================
    // Pastikan DOM sudah dimuat sebelum memanipulasi elemen-elemennya
    document.addEventListener('DOMContentLoaded', async () => {
        await fetchAppSettings();
        await fetchRewards();

        renderDashboard(currentUserData); 
    });
    </script>
</body>
</html>
