<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="icon" href="Logo Website.png" type="image/x-icon">
  <title>Ruang IPA Terpadu - Platform Pembelajaran Sains Interaktif</title>
  
  <!-- Tailwind CSS CDN -->
  <script src="https://cdn.tailwindcss.com"></script>
  <script>
    tailwind.config = {
      theme: {
        extend: {
          colors: {
            science: {
              50: '#f0fdf4',
              100: '#dcfce7',
              500: '#10b981', 
              600: '#059669',
              700: '#047857',
              800: '#065f46',
              900: '#064e3b',
            },
            physics: {
              500: '#3b82f6',
              600: '#2563eb',
            },
            chemistry: {
              500: '#ec4899',
              600: '#db2777',
            },
            biology: {
              500: '#10b981',
              600: '#059669',
            }
          }
        }
      }
    }
  </script>

  <!-- Google Fonts & Font Awesome Icons -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

  <style>
    body {
      font-family: 'Inter', sans-serif;
    }
    ::-webkit-scrollbar {
      width: 6px;
      height: 6px;
    }
    ::-webkit-scrollbar-track {
      background: #f1f5f9;
    }
    ::-webkit-scrollbar-thumb {
      background: #cbd5e1;
      border-radius: 9999px;
    }
    ::-webkit-scrollbar-thumb:hover {
      background: #94a3b8;
    }
    .fade-in {
      animation: fadeIn 0.3s ease-in-out forwards;
    }
    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(6px); }
      to { opacity: 1; transform: translateY(0); }
    }
    @keyframes smoothFloat {
      0%, 100% { transform: translateY(0px); }
      50% { transform: translateY(-8px); }
    }
    .animate-smooth-float {
      animation: smoothFloat 4.5s ease-in-out infinite;
    }
  </style>
</head>
<body class="bg-slate-50 text-slate-800 min-h-screen flex flex-col selection:bg-emerald-500 selection:text-white">

  <!-- ================= NOTIFICATION TOAST ================= -->
  <div id="toast" class="fixed top-5 right-5 z-50 transform transition-all duration-300 translate-y-[-100px] opacity-0 pointer-events-none flex items-center p-4 mb-4 text-gray-800 bg-white rounded-xl shadow-xl border border-slate-100 max-w-md" role="alert">
    <div id="toast-icon" class="inline-flex items-center justify-center flex-shrink-0 w-8 h-8 rounded-lg bg-emerald-100 text-emerald-500 mr-3">
      <i class="fa-solid fa-circle-check"></i>
    </div>
    <div id="toast-message" class="text-xs font-medium leading-relaxed">Notifikasi berhasil!</div>
  </div>

  <!-- ================= AUTHENTICATION CONTAINER ================= -->
  <div id="auth-screen" class="min-h-screen flex items-center justify-center p-4 bg-gradient-to-br from-slate-900 via-teal-900 to-emerald-900 relative overflow-hidden">
    <div class="absolute -top-32 -left-32 w-96 h-96 bg-emerald-500/20 rounded-full blur-3xl pointer-events-none"></div>
    <div class="absolute -bottom-32 -right-32 w-96 h-96 bg-cyan-500/20 rounded-full blur-3xl pointer-events-none"></div>

    <div class="w-full max-w-md bg-white/95 backdrop-blur-md rounded-2xl shadow-2xl overflow-hidden border border-white/20 fade-in z-10">
      
      <!-- Brand Header -->
      <div class="bg-gradient-to-r from-emerald-600 to-teal-600 p-6 text-center text-white relative">
        <div class="inline-flex items-center justify-center w-16 h-16 rounded-full bg-white/10 backdrop-blur-md mb-3 border border-white/20 shadow-inner overflow-hidden animate-smooth-float">
          <img src="Logo Website.png" alt="Logo Ruang IPA Terpadu" class="w-20 h-20 max-w-none object-contain -m-2" onerror="this.onerror=null; this.src='https://placehold.co/100x100/10b981/ffffff?text=IPA';"/>
        </div>
        <h1 class="text-2xl font-bold tracking-tight">Ruang IPA Terpadu</h1>
        <p class="text-emerald-100 text-xs mt-1">Platform Eksperimen & Belajar Sains Interaktif</p>
      </div>

      <!-- Auth Navigation Tabs -->
      <div class="flex border-b border-slate-100 bg-slate-50/50 p-1">
        <button id="tab-login" onclick="switchAuthTab('login')" class="flex-1 py-2.5 text-xs font-semibold rounded-lg text-emerald-700 bg-white shadow-sm transition">Masuk Siswa</button>
        <button id="tab-register" onclick="switchAuthTab('register')" class="flex-1 py-2.5 text-xs font-semibold rounded-lg text-slate-500 hover:text-slate-800 transition">Daftar Siswa</button>
        <button id="tab-admin" onclick="switchAuthTab('admin')" class="flex-1 py-2.5 text-xs font-semibold rounded-lg text-slate-500 hover:text-slate-800 transition">Portal Guru</button>
      </div>

      <!-- Form 1: Login Siswa -->
      <form id="form-login" onsubmit="handleLogin(event)" class="p-6 space-y-4">
        <div>
          <label class="block text-xs font-semibold text-slate-600 mb-1">Email / NISN Siswa</label>
          <div class="relative">
            <span class="absolute inset-y-0 left-0 flex items-center pl-3 text-slate-400">
              <i class="fa-solid fa-envelope"></i>
            </span>
            <input type="email" id="login-email" required placeholder="siswa@sekolah.sch.id" class="w-full pl-10 pr-4 py-2.5 text-sm bg-slate-50 border border-slate-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-emerald-500 focus:bg-white transition">
          </div>
        </div>
        <div>
          <label class="block text-xs font-semibold text-slate-600 mb-1">Kata Sandi</label>
          <div class="relative">
            <span class="absolute inset-y-0 left-0 flex items-center pl-3 text-slate-400">
              <i class="fa-solid fa-lock"></i>
            </span>
            <input type="password" id="login-password" required placeholder="••••••••" class="w-full pl-10 pr-10 py-2.5 text-sm bg-slate-50 border border-slate-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-emerald-500 focus:bg-white transition">
            <button type="button" onclick="togglePasswordVisibility('login-password', this)" class="absolute inset-y-0 right-0 pr-3 flex items-center text-slate-400 hover:text-slate-600">
              <i class="fa-solid fa-eye"></i>
            </button>
          </div>
        </div>
        <div class="flex items-center justify-between text-xs">
          <label class="flex items-center text-slate-500 cursor-pointer">
            <input type="checkbox" class="rounded border-slate-300 text-emerald-600 focus:ring-emerald-500 mr-2"> Ingat Saya
          </label>
          <a href="#" onclick="showToast('Silakan hubungi guru IPA sekolah untuk reset kata sandi.', 'info')" class="text-emerald-600 hover:underline font-medium">Lupa Password?</a>
        </div>
        <button type="submit" class="w-full py-3 bg-gradient-to-r from-emerald-600 to-teal-600 text-white font-semibold text-sm rounded-xl shadow-lg shadow-emerald-600/30 hover:shadow-emerald-600/50 hover:opacity-95 transition transform active:scale-95">
          <i class="fa-solid fa-right-to-bracket mr-2"></i> Masuk Sebagai Siswa
        </button>
        <p class="text-center text-xs text-slate-400 mt-2">Gunakan sebarang email siswa terdaftar.</p>
      </form>

      <!-- Form 2: Registrasi Siswa Baru -->
      <form id="form-register" onsubmit="handleRegister(event)" class="p-6 space-y-4 hidden">
        <div>
          <label class="block text-xs font-semibold text-slate-600 mb-1">Nama Lengkap Siswa</label>
          <input type="text" id="reg-name" required placeholder="Ahmad Rizky" class="w-full px-4 py-2.5 text-sm bg-slate-50 border border-slate-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-emerald-500 transition">
        </div>
        <div>
          <label class="block text-xs font-semibold text-slate-600 mb-1">Email Siswa</label>
          <input type="email" id="reg-email" required placeholder="rizky@sekolah.sch.id" class="w-full px-4 py-2.5 text-sm bg-slate-50 border border-slate-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-emerald-500 transition">
        </div>
        <div class="grid grid-cols-2 gap-3">
          <div>
            <label class="block text-xs font-semibold text-slate-600 mb-1">Pilih Kelas</label>
            <select id="reg-class" class="w-full px-3 py-2.5 text-sm bg-slate-50 border border-slate-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-emerald-500 transition">
              <option value="7 SMP">7 SMP</option>
              <option value="8 SMP" selected>8 SMP</option>
              <option value="9 SMP">9 SMP</option>
              <option value="10 SMA">10 SMA</option>
              <option value="11 SMA">11 SMA</option>
              <option value="12 SMA">12 SMA</option>
            </select>
          </div>
          <div>
            <label class="block text-xs font-semibold text-slate-600 mb-1">Kata Sandi</label>
            <input type="password" id="reg-password" required placeholder="••••••••" class="w-full px-4 py-2.5 text-sm bg-slate-50 border border-slate-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-emerald-500 transition">
          </div>
        </div>
        <button type="submit" class="w-full py-3 bg-gradient-to-r from-emerald-600 to-teal-600 text-white font-semibold text-sm rounded-xl shadow-lg shadow-emerald-600/30 hover:opacity-95 transition transform active:scale-95">
          <i class="fa-solid fa-user-plus mr-2"></i> Buat Akun Siswa Baru
        </button>
      </form>

      <!-- Form 3: Login Admin / Guru -->
      <form id="form-admin" onsubmit="handleAdminLogin(event)" class="p-6 space-y-4 hidden">
        <div class="p-3 bg-amber-50 border border-amber-200 rounded-xl text-amber-800 text-xs flex items-center">
          <i class="fa-solid fa-chalkboard-user text-amber-500 text-base mr-2"></i>
          <span>Portal Khusus Guru Pengajar & Pengelola Sistem IPA.</span>
        </div>
        <div>
          <label class="block text-xs font-semibold text-slate-600 mb-1">NIP / ID Guru</label>
          <input type="text" id="admin-id" required placeholder="GURU_IPA_123" class="w-full px-4 py-2.5 text-sm bg-slate-50 border border-slate-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-amber-500 transition">
        </div>
        <div>
          <label class="block text-xs font-semibold text-slate-600 mb-1">Passcode Otorisasi Guru</label>
          <input type="password" id="admin-pass" required placeholder="••••••••" class="w-full px-4 py-2.5 text-sm bg-slate-50 border border-slate-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-amber-500 transition">
        </div>
        <button type="submit" class="w-full py-3 bg-gradient-to-r from-amber-600 to-orange-600 text-white font-semibold text-sm rounded-xl shadow-lg shadow-amber-600/30 hover:opacity-95 transition transform active:scale-95">
          <i class="fa-solid fa-lock mr-2"></i> Akses Panel Guru / Pengajar
        </button>
        <p class="text-center text-xs text-slate-400">Passcode Guru Demo: <code class="bg-slate-100 px-1 py-0.5 rounded text-slate-700 font-mono">admin123</code></p>
      </form>

    </div>
  </div>


  <!-- ================= MAIN APP DASHBOARD ================= -->
  <div id="main-app" class="hidden min-h-screen flex flex-col bg-slate-100">

    <!-- TOP NAVIGATION BAR -->
    <header class="bg-white border-b border-slate-200 sticky top-0 z-30 shadow-sm">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="flex items-center justify-between h-16">
          
          <!-- Logo & Brand -->
          <div class="flex items-center space-x-3">
            <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-white-600 to-white-500 flex items-center justify-center text-white shadow-md shadow-black-500/20 overflow-hidden">
              <img src="Logo Website.png" alt="Logo" class="w-12 h-12 object-contain" onerror="this.onerror=null; this.src='https://placehold.co/80x80/10b981/ffffff?text=IPA';"/>
            </div>
            <div>
              <span class="font-bold text-slate-800 text-base leading-tight block">Ruang IPA <span class="text-emerald-600">Terpadu</span></span>
              <span id="role-badge" class="text-[10px] font-medium bg-emerald-100 text-emerald-700 px-2 py-0.5 rounded-full inline-block">Siswa Mode</span>
            </div>
          </div>

          <!-- Main Navigation Pills -->
          <nav class="hidden md:flex items-center space-x-1 bg-slate-100 p-1 rounded-xl">
            <button onclick="switchView('overview')" id="nav-overview" class="nav-btn px-4 py-2 text-xs font-semibold rounded-lg text-emerald-700 bg-white shadow-sm">
              <i class="fa-solid fa-compass mr-1.5"></i> Beranda
            </button>
            <button onclick="switchView('modules')" id="nav-modules" class="nav-btn px-4 py-2 text-xs font-semibold rounded-lg text-slate-600 hover:text-slate-900">
              <i class="fa-solid fa-book-open mr-1.5"></i> Modul
            </button>
            <button onclick="switchView('lab')" id="nav-lab" class="nav-btn px-4 py-2 text-xs font-semibold rounded-lg text-slate-600 hover:text-slate-900">
              <i class="fa-solid fa-vial mr-1.5"></i> Lab Virtual
            </button>
            <button onclick="switchView('ai-tutor')" id="nav-ai-tutor" class="nav-btn px-4 py-2 text-xs font-semibold rounded-lg text-slate-600 hover:text-slate-900">
              <i class="fa-solid fa-robot mr-1.5 text-amber-500"></i> AI Tutor
            </button>
            <button onclick="switchView('progress')" id="nav-progress" class="nav-btn px-4 py-2 text-xs font-semibold rounded-lg text-slate-600 hover:text-slate-900">
              <i class="fa-solid fa-chart-line mr-1.5"></i> Progres
            </button>
            <button onclick="switchView('forum')" id="nav-forum" class="nav-btn px-4 py-2 text-xs font-semibold rounded-lg text-slate-600 hover:text-slate-900">
              <i class="fa-solid fa-comments mr-1.5"></i> Diskusi
            </button>
            <button onclick="switchView('upload')" id="nav-upload" class="nav-btn px-4 py-2 text-xs font-semibold rounded-lg text-slate-600 hover:text-slate-900">
              <i class="fa-solid fa-cloud-arrow-up mr-1.5"></i> Upload & Tugas
            </button>
            <button id="nav-admin-btn" onclick="switchView('admin-panel')" class="nav-btn hidden px-4 py-2 text-xs font-semibold rounded-lg text-amber-700 bg-amber-50 border border-amber-200">
              <i class="fa-solid fa-sliders mr-1.5"></i> Panel Guru
            </button>
          </nav>

          <!-- User Profile & Action -->
          <div class="flex items-center space-x-3">
            <div class="text-right hidden sm:block">
              <div id="user-display-name" class="text-xs font-bold text-slate-800">Ahmad Rizky</div>
              <div id="user-display-class" class="text-[10px] text-slate-500">Kelas: 8 SMP</div>
            </div>
            
            <div class="w-9 h-9 rounded-full bg-emerald-600 text-white border border-emerald-500 flex items-center justify-center font-bold text-sm shadow-sm" id="user-avatar">
              S
            </div>
            
            <button onclick="logout()" title="Keluar Akun" class="p-2 text-slate-400 hover:text-rose-600 transition rounded-lg hover:bg-slate-100">
              <i class="fa-solid fa-right-from-bracket text-base"></i>
            </button>
          </div>

        </div>
      </div>
      
      <!-- Mobile Submenu Navigation -->
      <div class="flex md:hidden overflow-x-auto border-t border-slate-200 bg-slate-50 p-2 space-x-2 text-xs">
        <button onclick="switchView('overview')" class="px-3 py-1.5 font-medium rounded-lg bg-white border border-slate-200 shrink-0">Beranda</button>
        <button onclick="switchView('modules')" class="px-3 py-1.5 font-medium rounded-lg bg-white border border-slate-200 shrink-0">Modul</button>
        <button onclick="switchView('lab')" class="px-3 py-1.5 font-medium rounded-lg bg-white border border-slate-200 shrink-0">Lab Virtual</button>
        <button onclick="switchView('ai-tutor')" class="px-3 py-1.5 font-medium rounded-lg bg-white border border-slate-200 shrink-0">AI Tutor</button>
        <button onclick="switchView('progress')" class="px-3 py-1.5 font-medium rounded-lg bg-white border border-slate-200 shrink-0">Progres</button>
        <button onclick="switchView('forum')" class="px-3 py-1.5 font-medium rounded-lg bg-white border border-slate-200 shrink-0">Diskusi</button>
        <button onclick="switchView('upload')" class="px-3 py-1.5 font-medium rounded-lg bg-white border border-slate-200 shrink-0">Upload</button>
        <button id="mobile-nav-admin" onclick="switchView('admin-panel')" class="px-3 py-1.5 font-medium rounded-lg bg-amber-100 text-amber-800 border border-amber-300 shrink-0 hidden">Guru</button>
      </div>
    </header>


    <!-- CONTENT VIEWS -->
    <main class="flex-grow max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-6">

      <!-- ================= VIEW 1: OVERVIEW / DASHBOARD ================= -->
      <section id="view-overview" class="space-y-6 fade-in">
        
        <!-- Welcome Hero Banner -->
        <div class="bg-gradient-to-r from-emerald-600 via-teal-600 to-cyan-700 rounded-2xl p-6 md:p-8 text-white shadow-xl relative overflow-hidden">
          <div class="relative z-10 max-w-2xl">
            <span id="hero-role-tag" class="bg-white/20 text-white text-[11px] font-semibold px-3 py-1 rounded-full uppercase tracking-wider backdrop-blur-sm">Ruang Belajar Terisolasi Kelas</span>
            <h2 class="text-2xl md:text-3xl font-extrabold mt-2 leading-tight">Jelajahi Dunia Sains Terpadu Sesuai Kelas Anda</h2>
            <p class="text-emerald-100 text-sm mt-2">Seluruh materi, tugas, dan diskusi disesuaikan dengan kurikulum kelas Anda tanpa tercampur.</p>
            <div class="flex flex-wrap gap-3 mt-5">
              <button onclick="switchView('lab')" class="bg-white text-emerald-800 font-bold px-5 py-2.5 rounded-xl text-xs shadow-md hover:bg-emerald-50 transition flex items-center">
                <i class="fa-solid fa-flask-vial mr-2 text-emerald-600"></i> Buka Lab Virtual
              </button>
              <button onclick="switchView('ai-tutor')" class="bg-emerald-800/40 hover:bg-emerald-800/60 text-white border border-white/30 font-semibold px-5 py-2.5 rounded-xl text-xs backdrop-blur-sm transition flex items-center">
                <i class="fa-solid fa-robot mr-2 text-amber-300"></i> Tanya AI Tutor Sains
              </button>
            </div>
          </div>
          <i class="fa-solid fa-atom absolute -right-10 -bottom-10 text-[220px] text-white/10 pointer-events-none"></i>
        </div>

        <!-- Metric Stat Cards -->
        <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
          <div class="bg-white p-4 rounded-xl shadow-sm border border-slate-200 flex items-center space-x-3">
            <div class="w-12 h-12 rounded-xl bg-blue-50 text-blue-600 flex items-center justify-center text-xl shrink-0">
              <i class="fa-solid fa-book"></i>
            </div>
            <div>
              <div class="text-xs text-slate-500 font-medium">Modul Kelas Ini</div>
              <div class="text-lg font-bold text-slate-800" id="stat-completed-modules">0 Modul</div>
            </div>
          </div>

          <div class="bg-white p-4 rounded-xl shadow-sm border border-slate-200 flex items-center space-x-3">
            <div class="w-12 h-12 rounded-xl bg-emerald-50 text-emerald-600 flex items-center justify-center text-xl shrink-0">
              <i class="fa-solid fa-microscope"></i>
            </div>
            <div>
              <div class="text-xs text-slate-500 font-medium">Praktikum Selesai</div>
              <div class="text-lg font-bold text-slate-800" id="stat-lab-count">0 Eksperimen</div>
            </div>
          </div>

          <div class="bg-white p-4 rounded-xl shadow-sm border border-slate-200 flex items-center space-x-3">
            <div class="w-12 h-12 rounded-xl bg-amber-50 text-amber-600 flex items-center justify-center text-xl shrink-0">
              <i class="fa-solid fa-star"></i>
            </div>
            <div>
              <div class="text-xs text-slate-500 font-medium">Rata-Rata Nilai</div>
              <div class="text-lg font-bold text-slate-800" id="stat-avg-score">0 / 100</div>
            </div>
          </div>

          <div class="bg-white p-4 rounded-xl shadow-sm border border-slate-200 flex items-center space-x-3">
            <div class="w-12 h-12 rounded-xl bg-purple-50 text-purple-600 flex items-center justify-center text-xl shrink-0">
              <i class="fa-solid fa-award"></i>
            </div>
            <div>
              <div class="text-xs text-slate-500 font-medium">Status Peringkat</div>
              <div class="text-lg font-bold text-slate-800" id="stat-badge">Aktif</div>
            </div>
          </div>
        </div>

        <!-- Subject Shortcut Cards with Guru Overlay -->
        <div>
          <div class="flex items-center justify-between mb-3">
            <h3 class="text-base font-bold text-slate-800 flex items-center">
              <i class="fa-solid fa-layer-group text-emerald-600 mr-2"></i> Materi Pembelajaran Kelas <span id="overview-class-title" class="ml-1 text-emerald-600">8 SMP</span>
            </h3>
            <button onclick="openAddModuleModal('fisika')" class="guru-only hidden text-xs font-bold text-amber-700 bg-amber-100 hover:bg-amber-200 px-3 py-1.5 rounded-lg transition flex items-center">
              <i class="fa-solid fa-plus-circle mr-1 text-amber-600"></i> Tambah Materi Bab
            </button>
          </div>

          <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
            <!-- Fisika Card -->
            <div class="bg-white rounded-2xl p-5 border border-slate-200 shadow-sm hover:shadow-md transition relative group">
              <button onclick="openAddModuleModal('fisika')" title="Guru: Tambah Materi Fisika" class="guru-only hidden absolute top-4 right-4 bg-amber-500 hover:bg-amber-600 text-white w-7 h-7 rounded-lg items-center justify-center shadow transition">
                <i class="fa-solid fa-plus text-xs"></i>
              </button>
              <div class="flex items-center justify-between mb-3 pr-8">
                <span class="w-10 h-10 rounded-xl bg-blue-100 text-blue-600 flex items-center justify-center font-bold text-lg">
                  <i class="fa-solid fa-bolt"></i>
                </span>
                <span class="text-[11px] font-semibold bg-blue-50 text-blue-600 px-2.5 py-1 rounded-full">Fisika</span>
              </div>
              <h4 class="font-bold text-slate-800 text-base">Rangkaian Listrik & Hukum Ohm</h4>
              <p class="text-slate-500 text-xs mt-1">Pelajari hubungan Tegangan (V), Arus (I), dan Hambatan (R) dalam sirkuit.</p>
              <div class="mt-4 pt-3 border-t border-slate-100 flex items-center justify-between">
                <span class="text-[11px] text-slate-400">Lab: Simulasi Ohm</span>
                <button onclick="startLab('physics')" class="text-xs font-bold text-blue-600 hover:text-blue-700 flex items-center">
                  Mulai Praktikum <i class="fa-solid fa-arrow-right ml-1"></i>
                </button>
              </div>
            </div>

            <!-- Kimia Card -->
            <div class="bg-white rounded-2xl p-5 border border-slate-200 shadow-sm hover:shadow-md transition relative group">
              <button onclick="openAddModuleModal('kimia')" title="Guru: Tambah Materi Kimia" class="guru-only hidden absolute top-4 right-4 bg-amber-500 hover:bg-amber-600 text-white w-7 h-7 rounded-lg items-center justify-center shadow transition">
                <i class="fa-solid fa-plus text-xs"></i>
              </button>
              <div class="flex items-center justify-between mb-3 pr-8">
                <span class="w-10 h-10 rounded-xl bg-pink-100 text-pink-600 flex items-center justify-center font-bold text-lg">
                  <i class="fa-solid fa-vial-circle-check"></i>
                </span>
                <span class="text-[11px] font-semibold bg-pink-50 text-pink-600 px-2.5 py-1 rounded-full">Kimia</span>
              </div>
              <h4 class="font-bold text-slate-800 text-base">Titrasi Asam-Basa & Indikator pH</h4>
              <p class="text-slate-500 text-xs mt-1">Uji konsentrasi larutan dengan penambahan fenolftalein secara bertahap.</p>
              <div class="mt-4 pt-3 border-t border-slate-100 flex items-center justify-between">
                <span class="text-[11px] text-slate-400">Lab: Reaksi Larutan</span>
                <button onclick="startLab('chemistry')" class="text-xs font-bold text-pink-600 hover:text-pink-700 flex items-center">
                  Mulai Praktikum <i class="fa-solid fa-arrow-right ml-1"></i>
                </button>
              </div>
            </div>

            <!-- Biologi Card -->
            <div class="bg-white rounded-2xl p-5 border border-slate-200 shadow-sm hover:shadow-md transition relative group">
              <button onclick="openAddModuleModal('biologi')" title="Guru: Tambah Materi Biologi" class="guru-only hidden absolute top-4 right-4 bg-amber-500 hover:bg-amber-600 text-white w-7 h-7 rounded-lg items-center justify-center shadow transition">
                <i class="fa-solid fa-plus text-xs"></i>
              </button>
              <div class="flex items-center justify-between mb-3 pr-8">
                <span class="w-10 h-10 rounded-xl bg-emerald-100 text-emerald-600 flex items-center justify-center font-bold text-lg">
                  <i class="fa-solid fa-dna"></i>
                </span>
                <span class="text-[11px] font-semibold bg-emerald-50 text-emerald-600 px-2.5 py-1 rounded-full">Biologi</span>
              </div>
              <h4 class="font-bold text-slate-800 text-base">Pengamatan Mikroskop Sel Tumbuhan</h4>
              <p class="text-slate-500 text-xs mt-1">Amati struktur Kloroplas, Dinding Sel, dan Inti Sel pada pembesaran optik.</p>
              <div class="mt-4 pt-3 border-t border-slate-100 flex items-center justify-between">
                <span class="text-[11px] text-slate-400">Lab: Mikroskop Digital</span>
                <button onclick="startLab('biology')" class="text-xs font-bold text-emerald-600 hover:text-emerald-700 flex items-center">
                  Mulai Praktikum <i class="fa-solid fa-arrow-right ml-1"></i>
                </button>
              </div>
            </div>
          </div>
        </div>
      </section>


      <!-- ================= VIEW 2: MODUL IPA ================= -->
      <section id="view-modules" class="hidden space-y-6 fade-in">
        <div class="flex flex-col md:flex-row md:items-center justify-between gap-4">
          <div>
            <h2 class="text-xl font-bold text-slate-800">Modul & Bahan Ajar Khusus <span id="module-class-tag" class="text-emerald-600">8 SMP</span></h2>
            <p class="text-slate-500 text-xs">Daftar modul pembelajaran yang disesuaikan hanya untuk tingkat kelas Anda.</p>
          </div>
          
          <div class="flex flex-wrap items-center gap-3">
            <div class="flex items-center space-x-1 bg-white p-1 rounded-xl border border-slate-200 text-xs font-medium shadow-sm">
              <button onclick="filterModules('all', event)" class="mod-filter-btn px-3 py-1.5 rounded-lg bg-emerald-600 text-white">Semua</button>
              <button onclick="filterModules('fisika', event)" class="mod-filter-btn px-3 py-1.5 rounded-lg text-slate-600 hover:bg-slate-100">Fisika</button>
              <button onclick="filterModules('kimia', event)" class="mod-filter-btn px-3 py-1.5 rounded-lg text-slate-600 hover:bg-slate-100">Kimia</button>
              <button onclick="filterModules('biologi', event)" class="mod-filter-btn px-3 py-1.5 rounded-lg text-slate-600 hover:bg-slate-100">Biologi</button>
            </div>

            <button onclick="openAddModuleModal()" class="guru-only hidden px-4 py-2 bg-amber-600 hover:bg-amber-700 text-white text-xs font-semibold rounded-xl flex items-center gap-2 transition shadow-sm">
              <i class="fa-solid fa-plus text-xs"></i>
              <span>Tambah Modul Kelas</span>
            </button>
          </div>
        </div>

        <div id="module-grid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
          <!-- Dynamic Module Grid -->
        </div>
      </section>


      <!-- ================= VIEW 3: LAB VIRTUAL INTERAKTIF ================= -->
      <section id="view-lab" class="hidden space-y-6 fade-in">
        <div class="flex items-center justify-between">
          <div>
            <h2 class="text-xl font-bold text-slate-800">Laboratorium Virtual Interaktif</h2>
            <p class="text-slate-500 text-xs">Simulasi praktikum digital dan analisis preparat dari Guru.</p>
          </div>
          <div class="flex space-x-1 bg-white p-1 rounded-xl border border-slate-200 text-xs">
            <button id="btn-lab-chem" onclick="switchLabMode('chemistry')" class="px-3 py-1.5 font-bold rounded-lg bg-pink-600 text-white">Lab Kimia</button>
            <button id="btn-lab-phys" onclick="switchLabMode('physics')" class="px-3 py-1.5 font-bold rounded-lg text-slate-600 hover:bg-slate-100">Lab Fisika</button>
            <button id="btn-lab-bio" onclick="switchLabMode('biology')" class="px-3 py-1.5 font-bold rounded-lg text-slate-600 hover:bg-slate-100">Lab Biologi</button>
          </div>
        </div>

        <!-- Teacher Upload Photo Instrument Section for Lab -->
        <div class="guru-only hidden bg-amber-50 border border-amber-200 p-4 rounded-2xl">
          <h3 class="font-bold text-amber-900 text-xs mb-2 flex items-center">
            <i class="fa-solid fa-upload mr-2 text-amber-600"></i> Mode Guru: Upload Foto Preparat / Chart Praktikum ke Lab Siswa
          </h3>
          <form onsubmit="handleLabPhotoUpload(event)" class="grid grid-cols-1 md:grid-cols-4 gap-3">
            <input type="text" id="lab-photo-title" required placeholder="Judul Preparat (misal: Sel Epidermis Bawang)" class="px-3 py-2 text-xs bg-white border border-amber-300 rounded-xl">
            <select id="lab-photo-target-class" class="px-3 py-2 text-xs bg-white border border-amber-300 rounded-xl">
              <option value="7 SMP">Untuk 7 SMP</option>
              <option value="8 SMP" selected>Untuk 8 SMP</option>
              <option value="9 SMP">Untuk 9 SMP</option>
              <option value="10 SMA">Untuk 10 SMA</option>
              <option value="11 SMA">Untuk 11 SMA</option>
              <option value="12 SMA">Untuk 12 SMA</option>
            </select>
            <input type="file" id="lab-photo-file" accept="image/*" required class="px-3 py-1.5 text-xs bg-white border border-amber-300 rounded-xl">
            <button type="submit" class="bg-amber-600 hover:bg-amber-700 text-white font-bold text-xs py-2 rounded-xl transition">
              Unggah Preparat Siswa
            </button>
          </form>
        </div>

        <!-- Display Teacher Prepared Photos / Slides for Active Class -->
        <div id="teacher-preparats-container" class="space-y-3">
          <!-- Dynamic Preparats -->
        </div>

        <!-- Canvas Engine -->
        <div class="bg-white rounded-2xl border border-slate-200 shadow-sm overflow-hidden grid grid-cols-1 lg:grid-cols-3">
          <div class="lg:col-span-2 p-6 bg-slate-900 flex flex-col justify-between relative min-h-[420px]">
            <div class="flex items-center justify-between text-slate-300 border-b border-slate-800 pb-3">
              <span id="lab-title" class="font-semibold text-sm flex items-center">
                <i class="fa-solid fa-flask text-pink-400 mr-2"></i> Simulasi Titrasi Asam-Basa
              </span>
              <span class="text-xs bg-slate-800 px-2.5 py-1 rounded-full text-emerald-400 font-mono">STATUS: AKTIF</span>
            </div>

            <div class="w-full h-80 my-auto flex items-center justify-center relative">
              <canvas id="labCanvas" width="600" height="300" class="w-full h-full max-w-full rounded-xl"></canvas>
            </div>

            <div class="bg-slate-800/80 backdrop-blur-md p-3 rounded-xl border border-slate-700 flex justify-around text-center text-xs text-white">
              <div>
                <span class="text-slate-400 block text-[10px]">PARAMETER 1</span>
                <span id="readout-1" class="font-bold text-emerald-400 font-mono text-sm">pH: 1.0 (Asam Kuat)</span>
              </div>
              <div>
                <span class="text-slate-400 block text-[10px]">PARAMETER 2</span>
                <span id="readout-2" class="font-bold text-cyan-400 font-mono text-sm">Volume Tetes: 0 mL</span>
              </div>
              <div>
                <span class="text-slate-400 block text-[10px]">INDIKATOR</span>
                <span id="readout-3" class="font-bold text-amber-400 font-mono text-sm">Bening</span>
              </div>
            </div>
          </div>

          <div class="p-6 bg-slate-50 flex flex-col justify-between border-t lg:border-t-0 lg:border-l border-slate-200">
            <div>
              <h3 class="font-bold text-slate-800 text-sm mb-4 border-b border-slate-200 pb-2 flex items-center">
                <i class="fa-solid fa-sliders text-emerald-600 mr-2"></i> Panel Kontrol Eksperimen
              </h3>
              <div id="lab-controls-container" class="space-y-4"></div>
            </div>

            <div class="pt-6 border-t border-slate-200 mt-6 space-y-2">
              <button onclick="runLabSimulation()" class="w-full py-2.5 bg-emerald-600 hover:bg-emerald-700 text-white font-bold text-xs rounded-xl shadow transition">
                <i class="fa-solid fa-play mr-1.5"></i> Jalankan / Reset Reaksi
              </button>
              <button onclick="saveLabResult()" class="w-full py-2.5 bg-white border border-slate-300 text-slate-700 font-semibold text-xs rounded-xl hover:bg-slate-100 transition">
                <i class="fa-solid fa-bookmark mr-1.5 text-slate-400"></i> Simpan Catatan Praktikum
              </button>
            </div>
          </div>
        </div>
      </section>


      <!-- ================= VIEW 4: AI TUTOR CHATBOT ================= -->
      <section id="view-ai-tutor" class="hidden fade-in">
        <div class="max-w-4xl mx-auto bg-white rounded-2xl border border-slate-200 shadow-sm overflow-hidden flex flex-col h-[650px]">
          <div class="p-4 bg-slate-900 text-white flex items-center justify-between">
            <div class="flex items-center space-x-3">
              <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-amber-500 to-orange-500 flex items-center justify-center text-white font-bold text-lg shadow-md shadow-amber-500/20">
                <i class="fa-solid fa-robot"></i>
              </div>
              <div>
                <h3 class="font-bold text-sm">AI Tutor Sains Ruang IPA</h3>
                <span class="text-[10px] text-emerald-400 flex items-center">
                  <span class="w-2 h-2 rounded-full bg-emerald-400 mr-1.5 animate-pulse"></span> Pendamping Belajar Aktif
                </span>
              </div>
            </div>
            <button onclick="clearChat()" class="text-xs bg-slate-800 hover:bg-slate-700 text-slate-300 px-3 py-1.5 rounded-lg transition">
              <i class="fa-solid fa-rotate-right mr-1"></i> Bersihkan Chat
            </button>
          </div>

          <div id="chat-box" class="flex-grow p-4 overflow-y-auto space-y-4 bg-slate-50">
            <div class="flex items-start space-x-3">
              <div class="w-8 h-8 rounded-lg bg-amber-500 text-white flex items-center justify-center text-xs shrink-0 mt-1">
                <i class="fa-solid fa-robot"></i>
              </div>
              <div class="bg-white p-4 rounded-2xl rounded-tl-none border border-slate-200 shadow-sm max-w-xl text-xs text-slate-700 leading-relaxed">
                Halo! Saya AI Tutor Sains. Silakan ajukan pertanyaan sains tingkat sekolah Anda!
              </div>
            </div>
          </div>

          <div class="px-4 py-2 bg-slate-100 border-t border-slate-200 flex items-center space-x-2 overflow-x-auto text-xs">
            <span class="text-[10px] font-bold text-slate-400 uppercase shrink-0">Saran:</span>
            <button onclick="sendPresetQuery('Jelaskan rumus Hukum Ohm dan contoh penerapannya.')" class="bg-white hover:bg-slate-200 px-3 py-1 rounded-full text-slate-600 border border-slate-200 shrink-0">Hukum Ohm</button>
            <button onclick="sendPresetQuery('Apa perbedaan asam kuat dan asam lemah?')" class="bg-white hover:bg-slate-200 px-3 py-1 rounded-full text-slate-600 border border-slate-200 shrink-0">Asam vs Basa</button>
            <button onclick="sendPresetQuery('Bagaimana proses fotosintesis sel tumbuhan?')" class="bg-white hover:bg-slate-200 px-3 py-1 rounded-full text-slate-600 border border-slate-200 shrink-0">Fotosintesis</button>
          </div>

          <form onsubmit="handleChatSubmit(event)" class="p-3 bg-white border-t border-slate-200 flex items-center space-x-2">
            <input type="text" id="chat-input" required placeholder="Ketik pertanyaan sains kamu..." class="flex-grow px-4 py-3 bg-slate-50 border border-slate-200 rounded-xl text-xs focus:outline-none focus:ring-2 focus:ring-emerald-500 transition">
            <button type="submit" class="px-5 py-3 bg-emerald-600 hover:bg-emerald-700 text-white font-bold rounded-xl text-xs shadow transition flex items-center shrink-0">
              <span>Kirim</span> <i class="fa-solid fa-paper-plane ml-2"></i>
            </button>
          </form>
        </div>
      </section>


      <!-- ================= VIEW 5: PROGRESS & LAPORAN ================= -->
      <section id="view-progress" class="hidden space-y-6 fade-in">
        <div>
          <h2 class="text-xl font-bold text-slate-800">Laporan Progres Belajar Sains</h2>
          <p class="text-slate-500 text-xs">Statistik pencapaian dan riwayat penilaian langsung oleh Guru.</p>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
          <div class="bg-white p-6 rounded-2xl border border-slate-200 shadow-sm space-y-4">
            <h3 class="font-bold text-slate-800 text-sm border-b border-slate-100 pb-2">Penguasaan Subjek IPA</h3>
            
            <div>
              <div class="flex justify-between text-xs font-semibold mb-1">
                <span class="text-blue-600"><i class="fa-solid fa-bolt mr-1"></i> Fisika</span>
                <span id="progress-bar-phys-val">85%</span>
              </div>
              <div class="w-full bg-slate-100 rounded-full h-2.5">
                <div id="progress-bar-phys" class="bg-blue-600 h-2.5 rounded-full" style="width: 85%"></div>
              </div>
            </div>

            <div>
              <div class="flex justify-between text-xs font-semibold mb-1">
                <span class="text-pink-600"><i class="fa-solid fa-vial mr-1"></i> Kimia</span>
                <span id="progress-bar-chem-val">90%</span>
              </div>
              <div class="w-full bg-slate-100 rounded-full h-2.5">
                <div id="progress-bar-chem" class="bg-pink-600 h-2.5 rounded-full" style="width: 90%"></div>
              </div>
            </div>

            <div>
              <div class="flex justify-between text-xs font-semibold mb-1">
                <span class="text-emerald-600"><i class="fa-solid fa-dna mr-1"></i> Biologi</span>
                <span id="progress-bar-bio-val">78%</span>
              </div>
              <div class="w-full bg-slate-100 rounded-full h-2.5">
                <div id="progress-bar-bio" class="bg-emerald-600 h-2.5 rounded-full" style="width: 78%"></div>
              </div>
            </div>
          </div>

          <div class="md:col-span-2 bg-white rounded-2xl border border-slate-200 shadow-sm p-6 overflow-hidden">
            <h3 class="font-bold text-slate-800 text-sm mb-4 border-b border-slate-100 pb-2">Riwayat Nilai Evaluasi & Tugas Terisolasi Kelas</h3>
            <div class="overflow-x-auto">
              <table class="w-full text-left text-xs text-slate-600">
                <thead class="bg-slate-50 text-slate-700 font-bold border-b border-slate-200">
                  <tr>
                    <th class="p-3">Tanggal</th>
                    <th class="p-3">Aktivitas / Tugas</th>
                    <th class="p-3">Kategori</th>
                    <th class="p-3">Nilai</th>
                    <th class="p-3">Status Guru</th>
                  </tr>
                </thead>
                <tbody id="progress-table-body" class="divide-y divide-slate-100">
                  <!-- Dynamic Progress Rows -->
                </tbody>
              </table>
            </div>
          </div>
        </div>
      </section>


      <!-- ================= VIEW 6: FORUM DISKUSI KOMUNITAS ================= -->
      <section id="view-forum" class="hidden space-y-6 fade-in">
        <div class="flex items-center justify-between">
          <div>
            <h2 class="text-xl font-bold text-slate-800">Forum Diskusi Kelas <span id="forum-class-tag" class="text-emerald-600">8 SMP</span></h2>
            <p class="text-slate-500 text-xs">Diskusi terisolasi khusus siswa dan guru di kelas Anda.</p>
          </div>
          <button onclick="openNewThreadModal()" class="px-4 py-2 bg-emerald-600 hover:bg-emerald-700 text-white font-bold rounded-xl text-xs shadow transition flex items-center">
            <i class="fa-solid fa-plus mr-1.5"></i> Buat Topik Diskusi
          </button>
        </div>

        <div id="forum-threads-container" class="space-y-4">
          <!-- Dynamic Thread Items with Delete Buttons -->
        </div>
      </section>


      <!-- ================= VIEW 7: UPLOAD & TUGAS SISWA ================= -->
      <section id="view-upload" class="hidden space-y-6 fade-in">
        <div class="flex flex-col md:flex-row md:items-center justify-between gap-4 border-b border-slate-200 pb-4">
          <div>
            <h2 class="text-xl font-bold text-slate-800">
              <span class="siswa-only">Pengumpulan Tugas Kelas <span id="upload-class-tag" class="text-emerald-600">8 SMP</span></span>
              <span class="guru-only hidden text-amber-900">Pemeriksaan & Penilaian Tugas Siswa</span>
            </h2>
            <p class="text-slate-500 text-xs">
              <span class="siswa-only">Unggah lembar kerja dan periksa hasil evaluasi nilai dari Guru.</span>
              <span class="guru-only hidden">Periksa berkas tugas yang dikirimkan siswa dan berikan nilai langsung untuk setiap siswa.</span>
            </p>
          </div>
          <span class="text-xs font-semibold bg-emerald-100 text-emerald-800 px-3 py-1.5 rounded-xl border border-emerald-200">
            <i class="fa-solid fa-clipboard-check mr-1 text-emerald-600"></i> Terintegrasi Penilaian Otomatis
          </span>
        </div>

        <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
          <!-- Form Upload Tugas Siswa (HANYA MUNCUL UNTUK SISWA) -->
          <div class="siswa-only bg-white rounded-2xl border border-slate-200 p-6 shadow-sm space-y-4">
            <h3 class="font-bold text-slate-800 text-sm border-b border-slate-100 pb-2 flex items-center">
              <i class="fa-solid fa-cloud-arrow-up text-emerald-600 mr-2"></i> Form Unggah Tugas Siswa
            </h3>

            <form onsubmit="handleAssignmentSubmit(event)" class="space-y-4">
              <div>
                <label class="block text-xs font-semibold text-slate-600 mb-1">Pilih Judul Tugas</label>
                <select id="task-select" required class="w-full px-3 py-2 text-xs bg-slate-50 border border-slate-200 rounded-xl focus:ring-2 focus:ring-emerald-500">
                  <option value="Laporan Lab Titrasi Asam Basa">1. Laporan Praktikum Titrasi Asam Basa</option>
                  <option value="Soal Rangkaian Hukum Ohm">2. Lembar Soal Rangkaian Seri & Paralel</option>
                  <option value="Hasil Pengamatan Mikroskop Sel">3. Diagram Struktur Sel Tumbuhan</option>
                  <option value="Tugas Mandiri IPA Terpadu">4. Tugas Mandiri Pekanan IPA</option>
                </select>
              </div>

              <div>
                <label class="block text-xs font-semibold text-slate-600 mb-1">Catatan Tambahan untuk Guru</label>
                <textarea id="task-notes" rows="2" placeholder="Tuliskan catatan tugas jika ada..." class="w-full px-3 py-2 text-xs bg-slate-50 border border-slate-200 rounded-xl focus:ring-2 focus:ring-emerald-500"></textarea>
              </div>

              <div>
                <label class="block text-xs font-semibold text-slate-600 mb-1">Upload Berkas Tugas (PDF, Gambar, Docs)</label>
                <div class="border-2 border-dashed border-slate-300 rounded-xl p-4 text-center hover:border-emerald-500 transition cursor-pointer bg-slate-50 relative">
                  <input type="file" id="task-file-input" required class="absolute inset-0 w-full h-full opacity-0 cursor-pointer" onchange="updateFileNameDisplay(this, 'task-file-name')">
                  <i class="fa-solid fa-file-arrow-up text-2xl text-slate-400 mb-1 block"></i>
                  <span id="task-file-name" class="text-xs text-slate-600 font-medium block">Klik/seret file tugas Anda</span>
                </div>
              </div>

              <button type="submit" class="w-full py-2.5 bg-emerald-600 hover:bg-emerald-700 text-white font-bold text-xs rounded-xl shadow transition flex items-center justify-center">
                <i class="fa-solid fa-paper-plane mr-2"></i> Kirimkan Tugas Saya
              </button>
            </form>
          </div>

          <!-- Petunjuk Khusus Guru (HANYA MUNCUL DI MODE GURU) -->
          <div class="guru-only hidden bg-amber-50 rounded-2xl border border-amber-200 p-6 shadow-sm space-y-3">
            <h3 class="font-bold text-amber-900 text-sm flex items-center border-b border-amber-200 pb-2">
              <i class="fa-solid fa-user-check text-amber-600 mr-2"></i> Mode Guru: Penilaian Tugas
            </h3>
            <p class="text-xs text-amber-800 leading-relaxed">
              Klik tombol <strong class="bg-amber-500 text-white px-1.5 py-0.5 rounded text-[10px]">Nilai</strong> pada setiap baris berkas tugas siswa di tabel samping untuk memberikan nilai secara langsung.
            </p>
            <div class="p-3 bg-white rounded-xl border border-amber-200 text-xs text-amber-900 space-y-1.5">
              <div class="font-bold flex items-center text-amber-700">
                <i class="fa-solid fa-calculator mr-1.5"></i> Perhitungan Otomatis:
              </div>
              <ul class="list-disc list-inside text-[11px] text-slate-600 space-y-1">
                <li>Nilai langsung terupdate di dashboard & laporan siswa.</li>
                <li>Rata-rata & peringkat siswa dihitung otomatis oleh sistem.</li>
                <li>Laporan dapat diunduh per siswa di <strong>Panel Guru</strong>.</li>
              </ul>
            </div>
          </div>

          <!-- History & Grading List (Lebar Penuh di Mode Guru) -->
          <div id="assignment-table-wrapper" class="lg:col-span-2 bg-white rounded-2xl border border-slate-200 p-6 shadow-sm space-y-4">
            <h3 class="font-bold text-slate-800 text-sm border-b border-slate-100 pb-2 flex items-center justify-between">
              <span><i class="fa-solid fa-history text-slate-500 mr-2"></i> Berkas Tugas Terkirim & Evaluasi Nilai</span>
              <span id="submitted-task-count" class="text-xs font-semibold bg-slate-100 px-2.5 py-0.5 rounded-full text-slate-600">0 Berkas</span>
            </h3>

            <div class="overflow-x-auto">
              <table class="w-full text-left text-xs text-slate-600">
                <thead class="bg-slate-50 font-bold text-slate-700 border-b border-slate-200">
                  <tr>
                    <th class="p-3">Nama Siswa</th>
                    <th class="p-3">Kelas</th>
                    <th class="p-3">Judul Tugas</th>
                    <th class="p-3">File / Berkas</th>
                    <th class="p-3">Nilai Guru</th>
                    <th class="p-3">Aksi Guru</th>
                  </tr>
                </thead>
                <tbody id="assignment-table-body" class="divide-y divide-slate-100">
                  <!-- Dynamic Tasks -->
                </tbody>
              </table>
            </div>
          </div>
        </div>
      </section>


      <!-- ================= VIEW 8: COMPREHENSIVE PANEL MODE GURU ================= -->
      <section id="view-admin-panel" class="hidden space-y-6 fade-in">
        <div class="p-5 bg-gradient-to-r from-amber-600 to-orange-600 rounded-2xl text-white flex flex-col md:flex-row md:items-center justify-between shadow-lg shadow-amber-600/20 gap-4">
          <div>
            <h2 class="text-xl font-bold flex items-center">
              <i class="fa-solid fa-user-shield mr-2"></i> Panel Kelola Guru & Pengelola Sistem
            </h2>
            <p class="text-amber-100 text-xs mt-1">Kelola data siswa, penilaian, log aktivitas, peringkat, dan daftar admin pengajar.</p>
          </div>
          <button onclick="exportGradesCSV()" class="bg-white text-amber-900 font-bold text-xs px-4 py-2 rounded-xl shadow hover:bg-amber-50 transition flex items-center shrink-0">
            <i class="fa-solid fa-file-csv text-amber-600 mr-2 text-sm"></i> Unduh Riwayat Tugas & Nilai (CSV)
          </button>
        </div>

        <!-- Teacher Dashboard Internal Sub-Tabs -->
        <div class="flex overflow-x-auto border-b border-slate-200 bg-white p-1 rounded-xl shadow-sm text-xs font-semibold gap-1">
          <button onclick="switchTeacherTab('students')" id="ttab-students" class="px-4 py-2 rounded-lg bg-amber-500 text-white">Daftar & Edit Siswa</button>
          <button onclick="switchTeacherTab('activity')" id="ttab-activity" class="px-4 py-2 rounded-lg text-slate-600 hover:bg-slate-100">Aktivitas Siswa</button>
          <button onclick="switchTeacherTab('ranks')" id="ttab-ranks" class="px-4 py-2 rounded-lg text-slate-600 hover:bg-slate-100">Daftar Nilai Tertinggi</button>
          <button onclick="switchTeacherTab('admins')" id="ttab-admins" class="px-4 py-2 rounded-lg text-slate-600 hover:bg-slate-100">Daftar Admin / Pengajar</button>
        </div>

        <!-- SUBTAB 1: DAFTAR & EDIT SISWA -->
        <div id="tpanel-students" class="bg-white rounded-2xl border border-slate-200 p-6 shadow-sm space-y-4">
          <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-3">
            <h3 class="font-bold text-slate-800 text-sm">Manajemen Data Siswa Terdaftar</h3>
            <div class="flex items-center space-x-2">
              <input type="text" id="search-student-input" onkeyup="renderAdminPanel()" placeholder="Cari nama/email..." class="px-3 py-1.5 text-xs border border-slate-200 rounded-lg">
              <select id="filter-class-select" onchange="renderAdminPanel()" class="px-3 py-1.5 text-xs border border-slate-200 rounded-lg">
                <option value="ALL">Semua Kelas</option>
                <option value="7 SMP">7 SMP</option>
                <option value="8 SMP">8 SMP</option>
                <option value="9 SMP">9 SMP</option>
                <option value="10 SMA">10 SMA</option>
                <option value="11 SMA">11 SMA</option>
                <option value="12 SMA">12 SMA</option>
              </select>
            </div>
          </div>

          <div class="overflow-x-auto">
            <table class="w-full text-left text-xs text-slate-600">
              <thead class="bg-slate-50 font-bold text-slate-700 border-b border-slate-200">
                <tr>
                  <th class="p-3">Nama Siswa</th>
                  <th class="p-3">Email</th>
                  <th class="p-3">Kelas</th>
                  <th class="p-3">Aksi & Unduh Laporan Individual</th>
                </tr>
              </thead>
              <tbody id="admin-student-table" class="divide-y divide-slate-100">
                <!-- Dynamic Student Rows -->
              </tbody>
            </table>
          </div>
        </div>

        <!-- SUBTAB 2: LOG AKTIVITAS SISWA REAL-TIME -->
        <div id="tpanel-activity" class="hidden bg-white rounded-2xl border border-slate-200 p-6 shadow-sm space-y-4">
          <h3 class="font-bold text-slate-800 text-sm border-b border-slate-100 pb-2">Log Activity Real-time Siswa</h3>
          <div id="student-activity-log-container" class="space-y-2 max-h-96 overflow-y-auto">
            <!-- Dynamic Log Items -->
          </div>
        </div>

        <!-- SUBTAB 3: LEADERBOARD / NILAI TERTINGGI SISWA -->
        <div id="tpanel-ranks" class="hidden bg-white rounded-2xl border border-slate-200 p-6 shadow-sm space-y-4">
          <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-3 border-b border-slate-100 pb-2">
            <h3 class="font-bold text-slate-800 text-sm">Daftar Rekapitulasi Nilai Tugas Siswa</h3>
            <button onclick="exportGradesCSV()" class="px-3 py-1.5 bg-amber-600 hover:bg-amber-700 text-white font-bold text-xs rounded-lg shadow flex items-center shrink-0">
              <i class="fa-solid fa-file-csv mr-1.5"></i> Unduh Rekap Nilai Siswa (CSV)
            </button>
          </div>
          <div class="overflow-x-auto">
            <table class="w-full text-left text-xs text-slate-600">
              <thead class="bg-amber-50 text-amber-900 font-bold border-b border-amber-200">
                <tr>
                  <th class="p-3">Peringkat</th>
                  <th class="p-3">Nama Siswa</th>
                  <th class="p-3">Kelas</th>
                  <th class="p-3">Judul Tugas</th>
                  <th class="p-3">Nilai Tugas</th>
                  <th class="p-3">Rata-Rata Nilai</th>
                  <th class="p-3">Aksi Nilai</th>
                </tr>
              </thead>
              <tbody id="leaderboard-table-body" class="divide-y divide-slate-100">
                <!-- Dynamic Ranks & Scores -->
              </tbody>
            </table>
          </div>
        </div>

        <!-- SUBTAB 4: DAFTAR ADMIN / PENGAJAR -->
        <div id="tpanel-admins" class="hidden bg-white rounded-2xl border border-slate-200 p-6 shadow-sm space-y-4">
          <div class="flex items-center justify-between border-b border-slate-100 pb-2">
            <h3 class="font-bold text-slate-800 text-sm">Daftar Pengajar & Admin Sistem IPA</h3>
            <button onclick="openAddAdminModal()" class="px-3 py-1.5 bg-amber-600 text-white font-bold text-xs rounded-lg shadow hover:bg-amber-700">
              <i class="fa-solid fa-user-plus mr-1"></i> Tambah Admin Guru Baru
            </button>
          </div>
          <div class="overflow-x-auto">
            <table class="w-full text-left text-xs text-slate-600">
              <thead class="bg-slate-50 font-bold text-slate-700 border-b border-slate-200">
                <tr>
                  <th class="p-3">Nama Pengajar</th>
                  <th class="p-3">ID / NIP</th>
                  <th class="p-3">Email Status</th>
                  <th class="p-3">Aksi</th>
                </tr>
              </thead>
              <tbody id="admin-roster-table" class="divide-y divide-slate-100">
                <!-- Dynamic Admin Rows -->
              </tbody>
            </table>
          </div>
        </div>

      </section>

    </main>

    <!-- FOOTER -->
    <footer class="bg-white border-t border-slate-200 py-4 mt-auto">
      <div class="max-w-7xl mx-auto px-4 text-center text-slate-400 text-xs">
        &copy; 2026 Ruang IPA Terpadu. Platform Edukasi Digital Pembelajaran Sains Indonesia.
      </div>
    </footer>

  </div>


  <!-- ================= MODAL EDIT DATA SISWA ================= -->
  <div id="modal-edit-student" class="fixed inset-0 bg-slate-900/50 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
    <div class="bg-white rounded-2xl max-w-md w-full p-6 shadow-2xl border border-slate-100 fade-in">
      <div class="flex items-center justify-between border-b border-slate-100 pb-3 mb-4">
        <h3 class="font-bold text-slate-800 text-base">Edit Data Profil Siswa</h3>
        <button onclick="closeEditStudentModal()" class="text-slate-400 hover:text-slate-600"><i class="fa-solid fa-xmark text-lg"></i></button>
      </div>
      <form onsubmit="handleSaveEditStudent(event)" class="space-y-4">
        <input type="hidden" id="edit-student-idx">
        <div>
          <label class="block text-xs font-semibold text-slate-600 mb-1">Nama Lengkap Siswa</label>
          <input type="text" id="edit-student-name" required class="w-full px-3 py-2 text-xs bg-slate-50 border border-slate-200 rounded-xl">
        </div>
        <div>
          <label class="block text-xs font-semibold text-slate-600 mb-1">Email Siswa</label>
          <input type="email" id="edit-student-email" required class="w-full px-3 py-2 text-xs bg-slate-50 border border-slate-200 rounded-xl">
        </div>
        <div>
          <label class="block text-xs font-semibold text-slate-600 mb-1">Kelas Siswa</label>
          <select id="edit-student-class" class="w-full px-3 py-2 text-xs bg-slate-50 border border-slate-200 rounded-xl">
            <option value="7 SMP">7 SMP</option>
            <option value="8 SMP">8 SMP</option>
            <option value="9 SMP">9 SMP</option>
            <option value="10 SMA">10 SMA</option>
            <option value="11 SMA">11 SMA</option>
            <option value="12 SMA">12 SMA</option>
          </select>
        </div>
        <div class="flex justify-end space-x-2 pt-2">
          <button type="button" onclick="closeEditStudentModal()" class="px-4 py-2 text-xs font-semibold text-slate-600 hover:bg-slate-100 rounded-xl">Batal</button>
          <button type="submit" class="px-5 py-2 bg-amber-600 hover:bg-amber-700 text-white font-bold text-xs rounded-xl shadow">Simpan Perubahan</button>
        </div>
      </form>
    </div>
  </div>


  <!-- ================= MODAL FORUM THREAD ================= -->
  <div id="modal-forum" class="fixed inset-0 bg-slate-900/50 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
    <div class="bg-white rounded-2xl max-w-lg w-full p-6 shadow-2xl border border-slate-100 fade-in">
      <div class="flex items-center justify-between border-b border-slate-100 pb-3 mb-4">
        <h3 class="font-bold text-slate-800 text-base">Buat Topik Diskusi Baru</h3>
        <button onclick="closeNewThreadModal()" class="text-slate-400 hover:text-slate-600"><i class="fa-solid fa-xmark text-lg"></i></button>
      </div>
      <form onsubmit="handleCreateThread(event)" class="space-y-4">
        <div>
          <label class="block text-xs font-semibold text-slate-600 mb-1">Judul Diskusi</label>
          <input type="text" id="thread-title" required placeholder="Judul topik..." class="w-full px-4 py-2.5 text-xs bg-slate-50 border border-slate-200 rounded-xl">
        </div>
        <div>
          <label class="block text-xs font-semibold text-slate-600 mb-1">Kategori Topik</label>
          <select id="thread-category" class="w-full px-4 py-2.5 text-xs bg-slate-50 border border-slate-200 rounded-xl">
            <option value="Kimia Praktikum">Kimia Praktikum</option>
            <option value="Fisika & Sirkuit">Fisika & Sirkuit</option>
            <option value="Biologi Sel">Biologi Sel</option>
            <option value="Umum IPA">Umum IPA</option>
          </select>
        </div>
        <div>
          <label class="block text-xs font-semibold text-slate-600 mb-1">Isi Pertanyaan / Diskusi</label>
          <textarea id="thread-content" required rows="3" placeholder="Pertanyaan..." class="w-full px-4 py-2.5 text-xs bg-slate-50 border border-slate-200 rounded-xl"></textarea>
        </div>
        <div>
          <label class="block text-xs font-semibold text-slate-600 mb-1">Lampiran Foto/File (Opsional)</label>
          <input type="file" id="thread-file" class="w-full px-3 py-1.5 text-xs bg-slate-50 border border-slate-200 rounded-xl">
        </div>
        <div class="flex justify-end space-x-2 pt-2">
          <button type="button" onclick="closeNewThreadModal()" class="px-4 py-2 text-xs font-semibold text-slate-600 hover:bg-slate-100 rounded-xl">Batal</button>
          <button type="submit" class="px-5 py-2 bg-emerald-600 hover:bg-emerald-700 text-white font-bold text-xs rounded-xl shadow">Posting Topik</button>
        </div>
      </form>
    </div>
  </div>


  <!-- ================= MODAL TAMBAH MODUL (KHUSUS GURU) ================= -->
  <div id="add-module-modal" class="fixed inset-0 z-50 hidden bg-slate-900/60 backdrop-blur-sm flex items-center justify-center p-4">
    <div class="bg-white w-full max-w-lg rounded-2xl overflow-hidden shadow-2xl fade-in">
      <div class="p-4 border-b border-slate-200 flex items-center justify-between bg-amber-50">
        <h3 class="font-bold text-amber-900 text-base flex items-center">
          <i class="fa-solid fa-plus-circle text-amber-600 mr-2"></i> Guru: Tambah Modul Pembelajaran
        </h3>
        <button onclick="closeAddModuleModal()" class="text-slate-400 hover:text-slate-600"><i class="fa-solid fa-xmark text-lg"></i></button>
      </div>
      
      <form id="form-add-module" onsubmit="handleAddModule(event)" class="p-6 space-y-4">
        <div>
          <label class="block text-xs font-semibold text-slate-700 mb-1">Judul Materi / Modul</label>
          <input type="text" id="mod-title" required placeholder="Judul Modul..." class="w-full px-3 py-2 text-xs border border-slate-300 rounded-xl">
        </div>

        <div class="grid grid-cols-2 gap-4">
          <div>
            <label class="block text-xs font-semibold text-slate-700 mb-1">Kategori</label>
            <select id="mod-category" class="w-full px-3 py-2 text-xs border border-slate-300 rounded-xl">
              <option value="fisika">Fisika</option>
              <option value="kimia">Kimia</option>
              <option value="biologi">Biologi</option>
            </select>
          </div>
          <div>
            <label class="block text-xs font-semibold text-slate-700 mb-1">Kelas Target</label>
            <select id="mod-class" class="w-full px-3 py-2 text-xs border border-slate-300 rounded-xl">
              <option value="7 SMP">7 SMP</option>
              <option value="8 SMP" selected>8 SMP</option>
              <option value="9 SMP">9 SMP</option>
              <option value="10 SMA">10 SMA</option>
              <option value="11 SMA">11 SMA</option>
              <option value="12 SMA">12 SMA</option>
            </select>
          </div>
        </div>

        <div>
          <label class="block text-xs font-semibold text-slate-700 mb-1">Deskripsi Ringkas</label>
          <textarea id="mod-desc" rows="2" placeholder="Deskripsi..." class="w-full px-3 py-2 text-xs border border-slate-300 rounded-xl"></textarea>
        </div>

        <div>
          <label class="block text-xs font-semibold text-slate-700 mb-1">Tautan File Modul (PDF / Link)</label>
          <input type="url" id="mod-link" required placeholder="https://example.com/modul.pdf" class="w-full px-3 py-2 text-xs border border-slate-300 rounded-xl">
        </div>

        <div class="pt-4 border-t border-slate-100 flex justify-end gap-2">
          <button type="button" onclick="closeAddModuleModal()" class="px-4 py-2 text-xs font-medium text-slate-600 hover:bg-slate-100 rounded-xl">Batal</button>
          <button type="submit" class="px-5 py-2 text-xs font-bold bg-amber-600 hover:bg-amber-700 text-white rounded-xl shadow">Simpan Materi</button>
        </div>
      </form>
    </div>
  </div>


  <!-- ================= MODAL PERBESAR FOTO PREPARAT LAB (ZOOM LIGHTBOX) ================= -->
  <div id="modal-zoom-lab-photo" class="fixed inset-0 bg-slate-950/80 backdrop-blur-md z-50 flex items-center justify-center p-4 hidden" onclick="closeZoomPhotoModal()">
    <div class="relative max-w-4xl w-full bg-slate-900 rounded-2xl overflow-hidden shadow-2xl border border-slate-700 p-2 fade-in" onclick="event.stopPropagation()">
      <div class="flex items-center justify-between p-3 border-b border-slate-800 text-white">
        <h3 id="zoom-photo-title" class="font-bold text-sm text-emerald-400 flex items-center">
          <i class="fa-solid fa-magnifying-glass-plus mr-2"></i> Analisis Detail Preparat
        </h3>
        <button onclick="closeZoomPhotoModal()" class="text-slate-400 hover:text-white p-1 rounded-lg">
          <i class="fa-solid fa-xmark text-xl"></i>
        </button>
      </div>
      <div class="p-2 flex items-center justify-center bg-black/50 rounded-xl overflow-hidden max-h-[75vh]">
        <img id="zoom-photo-img" src="" alt="Zoom Preparat" class="max-w-full max-h-[70vh] object-contain rounded-lg transition-transform duration-300 hover:scale-125 cursor-zoom-in">
      </div>
      <div class="p-3 text-center text-xs text-slate-400 border-t border-slate-800">
        <i class="fa-solid fa-circle-info mr-1 text-emerald-400"></i> Arahkan kursor / sentuh foto untuk perbesar gambar preparat lebih terperinci.
      </div>
    </div>
  </div>


  <!-- ================= JAVASCRIPT LOGIC ENGINE ================= -->
  <script>
    /* LOCALSTORAGE DATABASES */
    let currentUser = JSON.parse(localStorage.getItem('ipa_current_user')) || null;
    
    let studentsDB = JSON.parse(localStorage.getItem('ipa_students')) || [
      { name: "Ahmad Rizky", email: "rizky@sekolah.sch.id", class: "8 SMP", password: "123" },
      { name: "Siti Rahma", email: "siti@sekolah.sch.id", class: "8 SMP", password: "123" },
      { name: "Budi Santoso", email: "budi@sekolah.sch.id", class: "9 SMP", password: "123" }
    ];

    let adminRosterDB = JSON.parse(localStorage.getItem('ipa_admins')) || [
      { name: "Guru Pengajar IPA 1", nip: "19850101201001", email: "guru1@sekolah.sch.id" },
      { name: "Admin Utama IPA", nip: "ADMIN_MAIN", email: "admin@sekolah.sch.id" }
    ];

    let modulesDB = JSON.parse(localStorage.getItem('ipa_modules')) || [
      { id: 1, title: "Rangkaian Listrik Seri & Paralel", category: "fisika", targetClass: "8 SMP", desc: "Memahami Hukum Kirchhoff pada sirkuit tertutup.", level: "Dasar", link: "https://www.w3.org/WAI/ER/tests/xhtml/testfiles/resources/pdf/dummy.pdf" },
      { id: 2, title: "Titrasi Asam-Basa & Indikator", category: "kimia", targetClass: "8 SMP", desc: "Mengukur netralisasi HCl dengan NaOH.", level: "Menengah", link: "https://www.w3.org/WAI/ER/tests/xhtml/testfiles/resources/pdf/dummy.pdf" },
      { id: 3, title: "Struktur Sel Tumbuhan & Mikroskop", category: "biologi", targetClass: "8 SMP", desc: "Identifikasi Kloroplas dan Dinding Sel.", level: "Dasar", link: "https://www.w3.org/WAI/ER/tests/xhtml/testfiles/resources/pdf/dummy.pdf" }
    ];

    let forumDB = JSON.parse(localStorage.getItem('ipa_forum')) || [
      { id: 1, title: "Mengapa larutan NaOH jika diteteskan PP berubah merah muda?", category: "Kimia Praktikum", targetClass: "8 SMP", author: "Ahmad Rizky", content: "Kenapa warnanya bisa mendadak berubah pucat?", replies: [
        { id: 101, author: "Guru Pengajar IPA", text: "Itu menunjukkan pH basa di atas 8.3!" }
      ], fileName: "" }
    ];

    let assignmentsDB = JSON.parse(localStorage.getItem('ipa_assignments')) || [
      { id: 1, studentName: "Ahmad Rizky", studentClass: "8 SMP", taskTitle: "Laporan Lab Titrasi Asam Basa", fileName: "Laporan_Titrasi_Rizky.pdf", time: "28/10/2026 14:20", score: 95, status: "Sudah Dinilai (95)" },
      { id: 2, studentName: "Siti Rahma", studentClass: "8 SMP", taskTitle: "Soal Rangkaian Hukum Ohm", fileName: "Jawaban_Ohm_Siti.pdf", time: "27/10/2026 09:15", score: 88, status: "Sudah Dinilai (88)" }
    ];

    let labPhotosDB = JSON.parse(localStorage.getItem('ipa_lab_photos')) || [
      { id: 1, title: "Preparat Bawang Merah 400x", targetClass: "8 SMP", fileData: "https://placehold.co/600x300/064e3b/ffffff?text=Preparat+Sel+Bawang+400x" }
    ];

    let activityLogsDB = JSON.parse(localStorage.getItem('ipa_logs')) || [
      { time: "28/10/2026 14:20", text: "Ahmad Rizky (8 SMP) mengunggah tugas Laporan Lab Titrasi." }
    ];

    let activeLabMode = 'chemistry';
    let labParams = { chemDrops: 0, chemPh: 1.0, physVoltage: 6, physResistance: 10, bioZoom: 100 };

    window.onload = function() {
      saveDB();
      if (currentUser) {
        showMainDashboard();
      } else {
        showAuthScreen();
      }
      initLabCanvas();
    };

    function saveDB() {
      localStorage.setItem('ipa_students', JSON.stringify(studentsDB));
      localStorage.setItem('ipa_admins', JSON.stringify(adminRosterDB));
      localStorage.setItem('ipa_modules', JSON.stringify(modulesDB));
      localStorage.setItem('ipa_forum', JSON.stringify(forumDB));
      localStorage.setItem('ipa_assignments', JSON.stringify(assignmentsDB));
      localStorage.setItem('ipa_lab_photos', JSON.stringify(labPhotosDB));
      localStorage.setItem('ipa_logs', JSON.stringify(activityLogsDB));
    }

    function logActivity(text) {
      const now = new Date();
      const timeStr = `${now.toLocaleDateString('id-ID')} ${now.getHours()}:${String(now.getMinutes()).padStart(2, '0')}`;
      activityLogsDB.unshift({ time: timeStr, text: text });
      saveDB();
      renderActivityLogs();
    }

    function showToast(message, type = 'success') {
      const toast = document.getElementById('toast');
      const toastMsg = document.getElementById('toast-message');
      const toastIcon = document.getElementById('toast-icon');

      toastMsg.innerText = message;
      if (type === 'error') {
        toastIcon.className = "inline-flex items-center justify-center flex-shrink-0 w-8 h-8 rounded-lg bg-rose-100 text-rose-500 mr-3";
        toastIcon.innerHTML = `<i class="fa-solid fa-circle-exclamation"></i>`;
      } else if (type === 'info') {
        toastIcon.className = "inline-flex items-center justify-center flex-shrink-0 w-8 h-8 rounded-lg bg-blue-100 text-blue-500 mr-3";
        toastIcon.innerHTML = `<i class="fa-solid fa-circle-info"></i>`;
      } else {
        toastIcon.className = "inline-flex items-center justify-center flex-shrink-0 w-8 h-8 rounded-lg bg-emerald-100 text-emerald-500 mr-3";
        toastIcon.innerHTML = `<i class="fa-solid fa-circle-check"></i>`;
      }

      toast.classList.remove('translate-y-[-100px]', 'opacity-0', 'pointer-events-none');
      setTimeout(() => {
        toast.classList.add('translate-y-[-100px]', 'opacity-0', 'pointer-events-none');
      }, 3500);
    }

    function togglePasswordVisibility(inputId, btn) {
      const input = document.getElementById(inputId);
      const icon = btn.querySelector('i');
      if (input.type === 'password') {
        input.type = 'text';
        icon.className = 'fa-solid fa-eye-slash';
      } else {
        input.type = 'password';
        icon.className = 'fa-solid fa-eye';
      }
    }

    function updateFileNameDisplay(input, targetId) {
      const target = document.getElementById(targetId);
      if (input.files && input.files[0]) {
        target.innerText = "Terpilih: " + input.files[0].name;
      }
    }

    /* AUTHENTICATION */
    function switchAuthTab(tab) {
      document.getElementById('form-login').classList.add('hidden');
      document.getElementById('form-register').classList.add('hidden');
      document.getElementById('form-admin').classList.add('hidden');

      document.getElementById('tab-login').className = "flex-1 py-2.5 text-xs font-semibold rounded-lg text-slate-500 hover:text-slate-800 transition";
      document.getElementById('tab-register').className = "flex-1 py-2.5 text-xs font-semibold rounded-lg text-slate-500 hover:text-slate-800 transition";
      document.getElementById('tab-admin').className = "flex-1 py-2.5 text-xs font-semibold rounded-lg text-slate-500 hover:text-slate-800 transition";

      if (tab === 'login') {
        document.getElementById('form-login').classList.remove('hidden');
        document.getElementById('tab-login').className = "flex-1 py-2.5 text-xs font-semibold rounded-lg text-emerald-700 bg-white shadow-sm transition";
      } else if (tab === 'register') {
        document.getElementById('form-register').classList.remove('hidden');
        document.getElementById('tab-register').className = "flex-1 py-2.5 text-xs font-semibold rounded-lg text-emerald-700 bg-white shadow-sm transition";
      } else if (tab === 'admin') {
        document.getElementById('form-admin').classList.remove('hidden');
        document.getElementById('tab-admin').className = "flex-1 py-2.5 text-xs font-semibold rounded-lg text-amber-700 bg-white shadow-sm transition";
      }
    }

    function handleLogin(e) {
      e.preventDefault();
      const email = document.getElementById('login-email').value.trim();
      const password = document.getElementById('login-password').value;

      const found = studentsDB.find(s => s.email.toLowerCase() === email.toLowerCase());
      if (found && found.password === password) {
        currentUser = { ...found, role: 'student' };
      } else {
        currentUser = { name: email.split('@')[0], email: email, class: "8 SMP", role: 'student' };
      }

      localStorage.setItem('ipa_current_user', JSON.stringify(currentUser));
      logActivity(`${currentUser.name} (${currentUser.class}) berhasil login.`);
      showToast(`Selamat datang Siswa ${currentUser.name}!`);
      showMainDashboard();
    }

    function handleRegister(e) {
      e.preventDefault();
      const name = document.getElementById('reg-name').value.trim();
      const email = document.getElementById('reg-email').value.trim();
      const className = document.getElementById('reg-class').value;
      const password = document.getElementById('reg-password').value;

      const newStudent = { name, email, class: className, password };
      studentsDB.push(newStudent);
      saveDB();

      currentUser = { ...newStudent, role: 'student' };
      localStorage.setItem('ipa_current_user', JSON.stringify(currentUser));
      logActivity(`Siswa Baru Terdaftar: ${name} (${className})`);
      showToast("Pendaftaran Siswa berhasil!");
      showMainDashboard();
    }

    function handleAdminLogin(e) {
      e.preventDefault();
      const adminId = document.getElementById('admin-id').value.trim();
      const pass = document.getElementById('admin-pass').value;

      if (pass === "admin123") {
        currentUser = { name: adminId || "Guru Pengajar IPA", email: "guru@sekolah.sch.id", class: "Guru Pengajar", role: 'teacher' };
        localStorage.setItem('ipa_current_user', JSON.stringify(currentUser));
        showToast("Akses Guru/Admin Diberikan!");
        showMainDashboard();
        switchView('admin-panel');
      } else {
        showToast("Passcode Guru salah! (Gunakan demo: admin123)", "error");
      }
    }

    function logout() {
      currentUser = null;
      localStorage.removeItem('ipa_current_user');
      document.getElementById('main-app').classList.add('hidden');
      document.getElementById('auth-screen').classList.remove('hidden');
      showToast("Anda telah keluar dari sistem.", "info");
    }

    /* DASHBOARD CONTROLS */
    function showMainDashboard() {
      document.getElementById('auth-screen').classList.add('hidden');
      document.getElementById('main-app').classList.remove('hidden');

      document.getElementById('user-display-name').innerText = currentUser.name;
      document.getElementById('user-display-class').innerText = `Kelas: ${currentUser.class}`;
      document.getElementById('user-avatar').innerText = currentUser.name.charAt(0).toUpperCase();

      const roleBadge = document.getElementById('role-badge');
      const navAdminBtn = document.getElementById('nav-admin-btn');
      const mobileNavAdmin = document.getElementById('mobile-nav-admin');
      const guruElements = document.querySelectorAll('.guru-only');
      const siswaElements = document.querySelectorAll('.siswa-only');

      const userClass = currentUser.role === 'teacher' ? '8 SMP' : currentUser.class;
      document.getElementById('overview-class-title').innerText = userClass;
      document.getElementById('module-class-tag').innerText = userClass;
      document.getElementById('forum-class-tag').innerText = userClass;
      document.getElementById('upload-class-tag').innerText = userClass;

      if (currentUser.role === 'teacher' || currentUser.role === 'admin') {
        roleBadge.innerText = "Mode Guru / Admin";
        roleBadge.className = "text-[10px] font-bold bg-amber-100 text-amber-800 px-2.5 py-0.5 rounded-full inline-block border border-amber-300";
        if (navAdminBtn) navAdminBtn.classList.remove('hidden');
        if (mobileNavAdmin) mobileNavAdmin.classList.remove('hidden');

        guruElements.forEach(el => el.classList.remove('hidden'));
        siswaElements.forEach(el => el.classList.add('hidden'));
      } else {
        roleBadge.innerText = "Mode Siswa";
        roleBadge.className = "text-[10px] font-medium bg-emerald-100 text-emerald-700 px-2.5 py-0.5 rounded-full inline-block";
        if (navAdminBtn) navAdminBtn.classList.add('hidden');
        if (mobileNavAdmin) mobileNavAdmin.classList.add('hidden');

        guruElements.forEach(el => el.classList.add('hidden'));
        siswaElements.forEach(el => el.classList.remove('hidden'));
      }

      renderModules();
      renderProgressTable();
      renderForumThreads();
      renderAssignmentTable();
      renderLabPhotos();
      renderAdminPanel();
      renderActivityLogs();
      renderLeaderboard();
      renderAdminRoster();

      switchView('overview');
    }

    function switchView(viewName) {
      const views = ['overview', 'modules', 'lab', 'ai-tutor', 'progress', 'forum', 'upload', 'admin-panel'];
      views.forEach(v => {
        const el = document.getElementById(`view-${v}`);
        if (el) el.classList.add('hidden');

        const navBtn = document.getElementById(`nav-${v}`);
        if (navBtn) {
          navBtn.className = "nav-btn px-4 py-2 text-xs font-semibold rounded-lg text-slate-600 hover:text-slate-900";
        }
      });

      const activeView = document.getElementById(`view-${viewName}`);
      if (activeView) activeView.classList.remove('hidden');

      const activeNav = document.getElementById(`nav-${viewName}`);
      if (activeNav) {
        if (viewName === 'admin-panel') {
          activeNav.className = "nav-btn px-4 py-2 text-xs font-semibold rounded-lg text-amber-800 bg-amber-100 border border-amber-200";
        } else {
          activeNav.className = "nav-btn px-4 py-2 text-xs font-semibold rounded-lg text-emerald-700 bg-white shadow-sm";
        }
      }

      if (viewName === 'lab') {
        renderLabControls();
        drawLab();
      }

      if (viewName === 'admin-panel') {
        renderAdminPanel();
        renderActivityLogs();
        renderLeaderboard();
        renderAdminRoster();
      }
    }

    function filterModules(category, evt) {
      document.querySelectorAll('.mod-filter-btn').forEach(btn => {
        btn.className = "mod-filter-btn px-3 py-1.5 rounded-lg text-slate-600 hover:bg-slate-100";
      });
      if (evt) evt.target.className = "mod-filter-btn px-3 py-1.5 rounded-lg bg-emerald-600 text-white";
      renderModules(category);
    }

    /* RENDER SISWA PROGRESS TABLE */
    function renderProgressTable() {
      const tbody = document.getElementById('progress-table-body');
      if (!tbody) return;
      tbody.innerHTML = '';

      const userClass = currentUser.role === 'teacher' ? 'ALL' : currentUser.class;
      const filtered = assignmentsDB.filter(a => {
        if (currentUser.role === 'teacher') return true;
        return a.studentClass === currentUser.class && a.studentName === currentUser.name;
      });

      if (filtered.length === 0) {
        tbody.innerHTML = `<tr><td colspan="5" class="p-4 text-center text-slate-400">Belum ada riwayat tugas yang dikirimkan.</td></tr>`;
        return;
      }

      filtered.forEach(a => {
        const scoreDisplay = a.score !== undefined ? `${a.score} / 100` : 'Belum Dinilai';
        const statusBadge = a.score !== undefined 
          ? `<span class="px-2 py-0.5 rounded text-[10px] font-bold bg-emerald-100 text-emerald-800">Selesai</span>`
          : `<span class="px-2 py-0.5 rounded text-[10px] font-bold bg-amber-100 text-amber-800">Proses Guru</span>`;

        tbody.innerHTML += `
          <tr class="hover:bg-slate-50">
            <td class="p-3 text-slate-500">${a.time}</td>
            <td class="p-3 font-semibold text-slate-800">${a.taskTitle}</td>
            <td class="p-3"><span class="px-2 py-0.5 rounded-full text-[10px] font-bold bg-slate-100 text-slate-600">${a.studentClass}</span></td>
            <td class="p-3 font-bold ${a.score !== undefined ? 'text-emerald-600' : 'text-amber-600'}">${scoreDisplay}</td>
            <td class="p-3">${statusBadge}</td>
          </tr>
        `;
      });
    }

    /* FORUM WITH DELETE CAPABILITY */
    function renderForumThreads() {
      const container = document.getElementById('forum-threads-container');
      if (!container) return;
      container.innerHTML = '';

      const userClass = currentUser.role === 'teacher' ? 'ALL' : currentUser.class;
      const filtered = forumDB.filter(t => userClass === 'ALL' || t.targetClass === userClass);

      filtered.forEach((t) => {
        let repliesHtml = '';
        if (t.replies && t.replies.length > 0) {
          t.replies.forEach((r, rIdx) => {
            const canDeleteReply = (currentUser.role === 'teacher' || (currentUser && currentUser.name === r.author));
            repliesHtml += `
              <div class="mt-2 p-2.5 bg-slate-50 rounded-xl border border-slate-100 text-xs flex justify-between items-start">
                <div><span class="font-bold text-slate-700">${r.author}:</span> ${r.text}</div>
                ${canDeleteReply ? `<button onclick="deleteReply(${t.id}, ${rIdx})" class="text-rose-500 hover:text-rose-700 text-[10px] ml-2"><i class="fa-solid fa-trash"></i></button>` : ''}
              </div>
            `;
          });
        }

        const canDeleteThread = (currentUser.role === 'teacher' || (currentUser && currentUser.name === t.author));

        container.innerHTML += `
          <div class="bg-white rounded-2xl p-5 border border-slate-200 shadow-sm space-y-3">
            <div class="flex items-center justify-between">
              <span class="bg-emerald-50 text-emerald-700 text-[10px] font-bold px-2.5 py-1 rounded-full border border-emerald-100">${t.category} • ${t.targetClass}</span>
              <div class="flex items-center space-x-2">
                <span class="text-slate-400 text-xs"><i class="fa-solid fa-comments mr-1"></i> ${(t.replies ? t.replies.length : 0)}</span>
                ${canDeleteThread ? `<button onclick="deleteThread(${t.id})" class="text-rose-500 hover:text-rose-700 text-xs font-semibold px-2 py-1 bg-rose-50 rounded-lg"><i class="fa-solid fa-trash mr-1"></i>Hapus Topik</button>` : ''}
              </div>
            </div>
            <h4 class="font-bold text-slate-800 text-sm">${t.title}</h4>
            <p class="text-slate-600 text-xs leading-relaxed">${t.content}</p>
            
            ${repliesHtml}

            <div class="pt-3 border-t border-slate-100 flex items-center space-x-2">
              <input type="text" id="reply-input-${t.id}" placeholder="Tulis komentar balasan..." class="flex-grow px-3 py-1.5 text-xs bg-slate-50 border border-slate-200 rounded-lg">
              <button onclick="addReply(${t.id})" class="px-3 py-1.5 bg-emerald-600 hover:bg-emerald-700 text-white font-bold text-xs rounded-lg shadow">Balas</button>
            </div>
          </div>
        `;
      });
    }

    function deleteThread(id) {
      if (confirm("Hapus postingan diskusi ini?")) {
        forumDB = forumDB.filter(t => t.id !== id);
        saveDB();
        logActivity(`${currentUser.name} menghapus postingan forum.`);
        renderForumThreads();
        showToast("Topik diskusi berhasil dihapus!");
      }
    }

    function deleteReply(threadId, replyIdx) {
      const thread = forumDB.find(t => t.id === threadId);
      if (thread && thread.replies) {
        thread.replies.splice(replyIdx, 1);
        saveDB();
        renderForumThreads();
        showToast("Komentar diskusi dihapus!");
      }
    }

    function addReply(threadId) {
      const input = document.getElementById(`reply-input-${threadId}`);
      const text = input.value.trim();
      if (!text) return;

      const thread = forumDB.find(t => t.id === threadId);
      if (thread) {
        if (!thread.replies) thread.replies = [];
        thread.replies.push({
          id: Date.now(),
          author: currentUser ? currentUser.name : "Siswa",
          text: text
        });
        saveDB();
        logActivity(`${currentUser.name} membalas diskusi pada kelas ${thread.targetClass}`);
        renderForumThreads();
        showToast("Komentar terkirim!");
      }
    }

    /* ASSIGNMENT GRADING & AUTOMATIC SCORE CALCULATIONS */
    function renderAssignmentTable() {
      const tbody = document.getElementById('assignment-table-body');
      const count = document.getElementById('submitted-task-count');
      if (!tbody) return;
      tbody.innerHTML = '';

      const userClass = currentUser.role === 'teacher' ? 'ALL' : currentUser.class;
      const filtered = assignmentsDB.filter(a => {
        if (currentUser.role === 'teacher') return true;
        return a.studentClass === currentUser.class && a.studentName === currentUser.name;
      });

      if (count) count.innerText = `${filtered.length} Berkas`;

      filtered.forEach(a => {
        tbody.innerHTML += `
          <tr class="hover:bg-slate-50">
            <td class="p-3 font-semibold text-slate-800">${a.studentName}</td>
            <td class="p-3"><span class="px-2 py-0.5 rounded-full text-[10px] font-bold bg-slate-100">${a.studentClass}</span></td>
            <td class="p-3 text-slate-700">${a.taskTitle}</td>
            <td class="p-3 font-mono text-emerald-600"><i class="fa-solid fa-file-pdf mr-1"></i>${a.fileName}</td>
            <td class="p-3 font-bold text-amber-700">${a.score !== undefined ? a.score : 'Belum Dinilai'}</td>
            <td class="p-3 flex items-center space-x-1">
              ${currentUser.role === 'teacher' ? `
                <button onclick="gradeAssignment(${a.id})" class="px-2 py-1 bg-amber-500 hover:bg-amber-600 text-white font-bold rounded text-[10px]">Nilai</button>
                <button onclick="deleteAssignment(${a.id})" class="p-1 text-rose-600 hover:bg-rose-50 rounded" title="Hapus Tugas"><i class="fa-solid fa-trash"></i></button>
              ` : `
                <button onclick="deleteAssignment(${a.id})" class="text-rose-500 hover:text-rose-700 text-xs"><i class="fa-solid fa-trash mr-1"></i>Hapus</button>
              `}
            </td>
          </tr>
        `;
      });

      calculateStudentStats();
      renderProgressTable();
    }

    function gradeAssignment(id) {
      const scoreStr = prompt("Masukkan Nilai Tugas Siswa (0 - 100):", "90");
      if (scoreStr !== null) {
        const score = parseInt(scoreStr) || 0;
        const task = assignmentsDB.find(a => a.id === id);
        if (task) {
          task.score = score;
          task.status = `Sudah Dinilai (${score})`;
          saveDB();
          logActivity(`Guru menilai tugas ${task.studentName} (${task.studentClass}): Nilai ${score}`);
          renderAssignmentTable();
          renderLeaderboard();
          showToast(`Nilai ${score} tersimpan untuk ${task.studentName}!`);
        }
      }
    }

    function deleteAssignment(id) {
      if (confirm("Hapus berkas tugas ini?")) {
        assignmentsDB = assignmentsDB.filter(a => a.id !== id);
        saveDB();
        renderAssignmentTable();
        showToast("Berkas tugas berhasil dihapus!");
      }
    }

    function handleAssignmentSubmit(e) {
      e.preventDefault();
      const taskTitle = document.getElementById('task-select').value;
      const fileInput = document.getElementById('task-file-input');
      const fileName = fileInput.files[0] ? fileInput.files[0].name : "Tugas_IPA.pdf";
      const now = new Date();
      const timeStr = `${now.toLocaleDateString('id-ID')} ${now.getHours()}:${String(now.getMinutes()).padStart(2, '0')}`;

      assignmentsDB.unshift({
        id: Date.now(),
        studentName: currentUser.name,
        studentClass: currentUser.class,
        taskTitle: taskTitle,
        fileName: fileName,
        time: timeStr,
        score: undefined,
        status: "Terkirim (Menunggu Nilai Guru)"
      });

      saveDB();
      logActivity(`${currentUser.name} (${currentUser.class}) mengunggah tugas "${taskTitle}"`);
      renderAssignmentTable();
      showToast("Tugas berhasil dikirim ke Guru!");
      e.target.reset();
      document.getElementById('task-file-name').innerText = "Klik/seret file tugas Anda";
    }

    function calculateStudentStats() {
      if (!currentUser || currentUser.role === 'teacher') return;
      const myTasks = assignmentsDB.filter(a => a.studentName === currentUser.name && a.score !== undefined);
      if (myTasks.length > 0) {
        const total = myTasks.reduce((sum, t) => sum + t.score, 0);
        const avg = Math.round(total / myTasks.length);
        const statAvg = document.getElementById('stat-avg-score');
        if (statAvg) statAvg.innerText = `${avg} / 100`;
      } else {
        const statAvg = document.getElementById('stat-avg-score');
        if (statAvg) statAvg.innerText = `88 / 100`;
      }
    }

    /* LAB VIRTUAL TEACHER PHOTO PREPARATS */
    function handleLabPhotoUpload(e) {
      e.preventDefault();
      const title = document.getElementById('lab-photo-title').value;
      const targetClass = document.getElementById('lab-photo-target-class').value;
      const fileInput = document.getElementById('lab-photo-file');

      if (fileInput.files && fileInput.files[0]) {
        const reader = new FileReader();
        reader.onload = function(evt) {
          labPhotosDB.unshift({
            id: Date.now(),
            title: title,
            targetClass: targetClass,
            fileData: evt.target.result
          });
          saveDB();
          logActivity(`Guru mengunggah foto preparat lab "${title}" untuk ${targetClass}`);
          renderLabPhotos();
          showToast("Foto preparat praktikum terunggah ke lab siswa!");
          e.target.reset();
        };
        reader.readAsDataURL(fileInput.files[0]);
      }
    }

    function renderLabPhotos() {
      const container = document.getElementById('teacher-preparats-container');
      if (!container) return;
      container.innerHTML = '';

      const userClass = currentUser.role === 'teacher' ? 'ALL' : currentUser.class;
      const filtered = labPhotosDB.filter(p => userClass === 'ALL' || p.targetClass === userClass);

      if (filtered.length > 0) {
        filtered.forEach(p => {
          container.innerHTML += `
            <div class="bg-white p-4 rounded-2xl border border-slate-200 shadow-sm flex flex-col md:flex-row items-center gap-4">
              <div class="relative group w-full md:w-48 h-28 shrink-0 overflow-hidden rounded-xl border border-slate-200 cursor-pointer" onclick="openZoomPhotoModal('${p.title.replace(/'/g, "\\'")}', '${p.fileData}')">
                <img src="${p.fileData}" alt="${p.title}" class="w-full h-full object-cover group-hover:scale-105 transition duration-300">
                <div class="absolute inset-0 bg-slate-900/40 opacity-0 group-hover:opacity-100 transition flex items-center justify-center text-white font-bold text-xs">
                  <i class="fa-solid fa-magnifying-glass-plus text-lg mr-1"></i> Perbesar
                </div>
              </div>
              <div class="flex-grow">
                <span class="text-[10px] font-bold bg-amber-100 text-amber-800 px-2.5 py-0.5 rounded-full">${p.targetClass}</span>
                <h4 class="font-bold text-slate-800 text-sm mt-1">${p.title}</h4>
                <p class="text-xs text-slate-500 mt-1">Foto preparat resmi dari Guru untuk dianalisis oleh siswa.</p>
              </div>
              <div class="flex items-center space-x-2">
                <button onclick="openZoomPhotoModal('${p.title.replace(/'/g, "\\'")}', '${p.fileData}')" class="px-3 py-1.5 bg-emerald-600 hover:bg-emerald-700 text-white font-bold text-xs rounded-xl shadow transition flex items-center">
                  <i class="fa-solid fa-magnifying-glass-plus mr-1"></i> Perbesar Foto
                </button>
                ${currentUser.role === 'teacher' ? `<button onclick="deleteLabPhoto(${p.id})" class="text-rose-600 hover:bg-rose-50 p-2 rounded-lg text-xs font-bold"><i class="fa-solid fa-trash mr-1"></i>Hapus</button>` : ''}
              </div>
            </div>
          `;
        });
      }
    }

    function openZoomPhotoModal(title, imgSrc) {
      document.getElementById('zoom-photo-title').innerHTML = `<i class="fa-solid fa-magnifying-glass-plus mr-2 text-emerald-400"></i> Analisis Preparat: ${title}`;
      document.getElementById('zoom-photo-img').src = imgSrc;
      document.getElementById('modal-zoom-lab-photo').classList.remove('hidden');
    }

    function closeZoomPhotoModal() {
      document.getElementById('modal-zoom-lab-photo').classList.add('hidden');
    }

    function deleteLabPhoto(id) {
      if (confirm("Hapus foto preparat ini?")) {
        labPhotosDB = labPhotosDB.filter(p => p.id !== id);
        saveDB();
        renderLabPhotos();
        showToast("Foto preparat dihapus!");
      }
    }

    /* ADMIN & TEACHER PANEL SUBTABS */
    function switchTeacherTab(tabName) {
      ['students', 'activity', 'ranks', 'admins'].forEach(t => {
        const p = document.getElementById(`tpanel-${t}`);
        const btn = document.getElementById(`ttab-${t}`);
        if (p) p.classList.add('hidden');
        if (btn) btn.className = "px-4 py-2 rounded-lg text-slate-600 hover:bg-slate-100";
      });
      const activePanel = document.getElementById(`tpanel-${tabName}`);
      const activeTab = document.getElementById(`ttab-${tabName}`);
      if (activePanel) activePanel.classList.remove('hidden');
      if (activeTab) activeTab.className = "px-4 py-2 rounded-lg bg-amber-500 text-white";
    }

    function renderAdminPanel() {
      const tbody = document.getElementById('admin-student-table');
      if (!tbody) return;
      tbody.innerHTML = '';

      const query = document.getElementById('search-student-input')?.value.toLowerCase() || '';
      const filterClass = document.getElementById('filter-class-select')?.value || 'ALL';

      const filtered = studentsDB.filter(s => {
        const matchQ = s.name.toLowerCase().includes(query) || s.email.toLowerCase().includes(query);
        const matchC = filterClass === 'ALL' || s.class === filterClass;
        return matchQ && matchC;
      });

      filtered.forEach((s, idx) => {
        tbody.innerHTML += `
          <tr class="hover:bg-slate-50">
            <td class="p-3 font-semibold text-slate-800">${s.name}</td>
            <td class="p-3 text-slate-500">${s.email}</td>
            <td class="p-3"><span class="px-2 py-0.5 rounded-full text-[10px] font-bold bg-slate-100">${s.class}</span></td>
            <td class="p-3 space-x-2 flex items-center">
              <button onclick="downloadIndividualStudentReport('${s.name}', '${s.class}')" class="px-2.5 py-1 bg-emerald-100 hover:bg-emerald-200 text-emerald-800 font-semibold rounded-lg text-[10px] transition flex items-center">
                <i class="fa-solid fa-file-arrow-down mr-1 text-emerald-600"></i> Unduh Nilai Siswa
              </button>
              <button onclick="openEditStudentModal(${idx})" class="text-amber-600 hover:underline font-semibold text-xs"><i class="fa-solid fa-pen mr-1"></i>Edit</button>
              <button onclick="deleteStudent(${idx})" class="text-rose-500 hover:underline font-semibold text-xs"><i class="fa-solid fa-trash mr-1"></i>Hapus</button>
            </td>
          </tr>
        `;
      });
    }

    function downloadIndividualStudentReport(studentName, studentClass) {
      const studentTasks = assignmentsDB.filter(a => a.studentName.toLowerCase() === studentName.toLowerCase());
      
      let csvContent = `data:text/csv;charset=utf-8,LAPORAN INDIVIDUAL TUGAS & NILAI SISWA\n`;
      csvContent += `Nama Siswa,${studentName}\nKelas,${studentClass}\nTanggal Unduh,${new Date().toLocaleDateString('id-ID')}\n\n`;
      csvContent += `No,Judul Tugas,Nama Berkas,Status / Nilai,Waktu Pengumpulan\n`;

      if (studentTasks.length === 0) {
        csvContent += `1,Belum Ada Tugas Terkirim,-,-,-\n`;
      } else {
        studentTasks.forEach((t, i) => {
          csvContent += `"${i + 1}","${t.taskTitle}","${t.fileName}","${t.score !== undefined ? t.score : 'Belum Dinilai'}","${t.time}"\n`;
        });
      }

      const encodedUri = encodeURI(csvContent);
      const link = document.createElement("a");
      link.setAttribute("href", encodedUri);
      link.setAttribute("download", `Laporan_Nilai_${studentName.replace(/\s+/g, '_')}_${studentClass.replace(/\s+/g, '_')}.csv`);
      document.body.appendChild(link);
      link.click();
      document.body.removeChild(link);
      showToast(`File laporan nilai untuk ${studentName} berhasil diunduh!`);
    }

    function openEditStudentModal(idx) {
      const s = studentsDB[idx];
      document.getElementById('edit-student-idx').value = idx;
      document.getElementById('edit-student-name').value = s.name;
      document.getElementById('edit-student-email').value = s.email;
      document.getElementById('edit-student-class').value = s.class;
      document.getElementById('modal-edit-student').classList.remove('hidden');
    }

    function closeEditStudentModal() {
      document.getElementById('modal-edit-student').classList.add('hidden');
    }

    function handleSaveEditStudent(e) {
      e.preventDefault();
      const idx = document.getElementById('edit-student-idx').value;
      studentsDB[idx].name = document.getElementById('edit-student-name').value;
      studentsDB[idx].email = document.getElementById('edit-student-email').value;
      studentsDB[idx].class = document.getElementById('edit-student-class').value;

      saveDB();
      renderAdminPanel();
      closeEditStudentModal();
      showToast("Data siswa diperbarui!");
    }

    function deleteStudent(index) {
      if (confirm(`Hapus data siswa ${studentsDB[index].name}?`)) {
        studentsDB.splice(index, 1);
        saveDB();
        renderAdminPanel();
        showToast("Siswa dihapus.");
      }
    }

    function renderActivityLogs() {
      const container = document.getElementById('student-activity-log-container');
      if (!container) return;
      container.innerHTML = '';
      activityLogsDB.forEach(l => {
        container.innerHTML += `
          <div class="p-3 bg-slate-50 rounded-xl border border-slate-100 flex justify-between items-center text-xs">
            <span class="text-slate-700 font-medium">${l.text}</span>
            <span class="text-[10px] font-mono text-slate-400 shrink-0 ml-2">${l.time}</span>
          </div>
        `;
      });
    }

    function renderLeaderboard() {
      const tbody = document.getElementById('leaderboard-table-body');
      if (!tbody) return;
      tbody.innerHTML = '';

      if (assignmentsDB.length === 0) {
        tbody.innerHTML = `<tr><td colspan="7" class="p-4 text-center text-slate-400">Belum ada tugas yang dikirimkan oleh siswa.</td></tr>`;
        return;
      }

      const studentAvgMap = {};
      assignmentsDB.forEach(a => {
        if (!studentAvgMap[a.studentName]) {
          studentAvgMap[a.studentName] = { total: 0, count: 0 };
        }
        if (a.score !== undefined) {
          studentAvgMap[a.studentName].total += a.score;
          studentAvgMap[a.studentName].count += 1;
        }
      });

      const sortedAssignments = [...assignmentsDB].sort((a, b) => (b.score || 0) - (a.score || 0));

      sortedAssignments.forEach((a, idx) => {
        const stats = studentAvgMap[a.studentName];
        const avgScore = (stats && stats.count > 0) ? Math.round(stats.total / stats.count) : '-';

        tbody.innerHTML += `
          <tr class="hover:bg-slate-50">
            <td class="p-3 font-bold text-amber-600">#${idx + 1}</td>
            <td class="p-3 font-semibold text-slate-800">${a.studentName}</td>
            <td class="p-3 font-medium text-slate-600"><span class="px-2 py-0.5 rounded-full text-[10px] font-bold bg-slate-100">${a.studentClass}</span></td>
            <td class="p-3 text-slate-700">${a.taskTitle}</td>
            <td class="p-3 font-bold ${a.score !== undefined ? 'text-emerald-600' : 'text-rose-500'}">
              ${a.score !== undefined ? a.score + ' / 100' : 'Belum Dinilai'}
            </td>
            <td class="p-3 font-bold text-blue-600">${avgScore} / 100</td>
            <td class="p-3">
              <button onclick="gradeAssignment(${a.id})" class="px-2 py-1 bg-amber-500 hover:bg-amber-600 text-white font-bold rounded text-[10px]">
                <i class="fa-solid fa-pen mr-1"></i>Ubah Nilai
              </button>
            </td>
          </tr>
        `;
      });
    }

    function exportGradesCSV() {
      if (assignmentsDB.length === 0) {
        showToast("Belum ada data nilai tugas untuk diunduh!", "error");
        return;
      }

      let csvContent = "data:text/csv;charset=utf-8,NO,NAMA SISWA,KELAS,JUDUL TUGAS,FILE TUGAS,NILAI TUGAS,WAKTU PENGUMPULAN,STATUS PENILAIAN\n";
      
      assignmentsDB.forEach((a, idx) => {
        const scoreVal = a.score !== undefined ? a.score : "Belum Dinilai";
        const statusVal = a.score !== undefined ? "Sudah Dinilai" : "Menunggu Penilaian Guru";
        csvContent += `"${idx + 1}","${a.studentName}","${a.studentClass}","${a.taskTitle}","${a.fileName}","${scoreVal}","${a.time}","${statusVal}"\n`;
      });

      const encodedUri = encodeURI(csvContent);
      const link = document.createElement("a");
      link.setAttribute("href", encodedUri);
      link.setAttribute("download", `Daftar_Nilai_Tugas_Siswa_${new Date().toLocaleDateString('id-ID').replace(/\//g, '-')}.csv`);
      document.body.appendChild(link);
      link.click();
      document.body.removeChild(link);
      showToast("File Rekapitulasi Nilai Tugas Siswa (CSV) berhasil diunduh!");
    }

    function renderAdminRoster() {
      const tbody = document.getElementById('admin-roster-table');
      if (!tbody) return;
      tbody.innerHTML = '';

      adminRosterDB.forEach((a, idx) => {
        tbody.innerHTML += `
          <tr class="hover:bg-slate-50">
            <td class="p-3 font-semibold text-slate-800">${a.name}</td>
            <td class="p-3 font-mono text-slate-600">${a.nip}</td>
            <td class="p-3 text-slate-500">${a.email}</td>
            <td class="p-3">
              <button onclick="deleteAdminRoster(${idx})" class="text-rose-500 hover:underline font-semibold"><i class="fa-solid fa-trash mr-1"></i>Hapus</button>
            </td>
          </tr>
        `;
      });
    }

    function openAddAdminModal() {
      const name = prompt("Nama Guru / Admin Baru:");
      const nip = prompt("NIP / ID Guru:");
      if (name && nip) {
        adminRosterDB.push({ name, nip, email: `${nip.toLowerCase()}@sekolah.sch.id` });
        saveDB();
        renderAdminRoster();
        showToast("Guru/Admin baru berhasil ditambahkan!");
      }
    }

    function deleteAdminRoster(idx) {
      if (confirm("Hapus akun pengajar ini?")) {
        adminRosterDB.splice(idx, 1);
        saveDB();
        renderAdminRoster();
        showToast("Data pengajar dihapus!");
      }
    }

    /* MODAL HANDLERS */
    function openAddModuleModal(preCategory = 'fisika') {
      document.getElementById('mod-category').value = preCategory;
      document.getElementById('add-module-modal').classList.remove('hidden');
    }

    function closeAddModuleModal() {
      document.getElementById('add-module-modal').classList.add('hidden');
    }

    function handleAddModule(e) {
      e.preventDefault();
      const title = document.getElementById('mod-title').value.trim();
      const category = document.getElementById('mod-category').value;
      const targetClass = document.getElementById('mod-class').value;
      const desc = document.getElementById('mod-desc').value.trim();
      const link = document.getElementById('mod-link').value.trim();

      if (!title || !link) {
        showToast("Judul dan Tautan File wajib diisi!", "error");
        return;
      }

      const newModule = {
        id: Date.now(),
        title,
        category,
        targetClass,
        desc: desc || "Tidak ada deskripsi tambahan.",
        level: "Dasar",
        link
      };

      modulesDB.unshift(newModule);
      saveDB();
      logActivity(`Guru menerbitkan modul baru "${title}" untuk kelas ${targetClass}`);
      renderModules();
      closeAddModuleModal();
      showToast("Modul materi baru berhasil diterbitkan!");
      e.target.reset();
    }

    function renderModules(filter = 'all') {
      const grid = document.getElementById('module-grid');
      if (!grid) return;
      grid.innerHTML = '';

      const userClass = currentUser.role === 'teacher' ? 'ALL' : currentUser.class;
      const filtered = modulesDB.filter(m => {
        const matchCategory = filter === 'all' || m.category === filter;
        const matchClass = userClass === 'ALL' || m.targetClass === userClass;
        return matchCategory && matchClass;
      });

      if (filtered.length === 0) {
        grid.innerHTML = `
          <div class="col-span-full bg-white p-8 rounded-2xl border border-slate-200 text-center text-slate-400">
            <i class="fa-solid fa-folder-open text-3xl mb-2"></i>
            <p class="text-xs">Belum ada modul yang tersedia untuk kelas ini.</p>
          </div>
        `;
        return;
      }

      filtered.forEach((m) => {
        let categoryColor = m.category === 'fisika' ? 'blue' : m.category === 'kimia' ? 'pink' : 'emerald';
        let icon = m.category === 'fisika' ? 'fa-bolt' : m.category === 'kimia' ? 'fa-vial' : 'fa-dna';

        let validLink = m.link ? m.link.trim() : '#';
        if (validLink !== '#' && !validLink.startsWith('http://') && !validLink.startsWith('https://')) {
          validLink = 'https://' + validLink;
        }

        grid.innerHTML += `
          <div class="bg-white rounded-2xl p-5 border border-slate-200 shadow-sm hover:shadow-md transition flex flex-col justify-between relative">
            <div>
              <div class="flex items-center justify-between mb-3">
                <span class="w-9 h-9 rounded-xl bg-${categoryColor}-100 text-${categoryColor}-600 flex items-center justify-center font-bold text-sm">
                  <i class="fa-solid ${icon}"></i>
                </span>
                <span class="text-[10px] font-bold bg-slate-100 text-slate-600 px-2.5 py-1 rounded-full uppercase">${m.targetClass}</span>
              </div>
              <h4 class="font-bold text-slate-800 text-sm">${m.title}</h4>
              <p class="text-slate-500 text-xs mt-1.5 leading-relaxed">${m.desc}</p>
            </div>
            
            <div class="mt-4 pt-3 border-t border-slate-100 flex items-center justify-between">
              <span class="text-[11px] font-semibold text-${categoryColor}-600 uppercase tracking-wider">${m.category}</span>
              
              <div class="flex items-center space-x-1.5">
                <a href="${validLink}" target="_blank" rel="noopener noreferrer" class="px-3 py-1.5 bg-emerald-600 hover:bg-emerald-700 text-white font-semibold rounded-lg text-xs transition flex items-center shadow-sm">
                  Buka Modul <i class="fa-solid fa-arrow-up-right-from-square text-[10px] ml-1.5"></i>
                </a>
                ${currentUser.role === 'teacher' ? `
                  <button onclick="deleteModule(${m.id})" class="p-1.5 text-rose-500 hover:bg-rose-50 rounded-lg" title="Hapus Modul">
                    <i class="fa-solid fa-trash text-xs"></i>
                  </button>
                ` : ''}
              </div>
            </div>
          </div>
        `;
      });
    }

    function deleteModule(id) {
      if (confirm("Hapus modul materi ini?")) {
        modulesDB = modulesDB.filter(m => m.id !== id);
        saveDB();
        renderModules();
        showToast("Modul materi berhasil dihapus.");
      }
    }

    function updateLabParam(key, val) {
      labParams[key] = parseFloat(val);
      renderLabControls();
      drawLab();
    }

    function initLabCanvas() {
      const canvas = document.getElementById('labCanvas');
      if (canvas) {
        canvas.width = canvas.offsetWidth;
        canvas.height = canvas.offsetHeight;
      }
    }

    function drawLab() {
      const canvas = document.getElementById('labCanvas');
      if (!canvas) return;
      const ctx = canvas.getContext('2d');
      const w = canvas.width;
      const h = canvas.height;

      ctx.clearRect(0, 0, w, h);

      if (activeLabMode === 'chemistry') {
        const drops = labParams.chemDrops;
        let ph = (1.0 + (drops * 0.43)).toFixed(1);
        if (ph > 14.0) ph = 14.0;

        let color = '#38bdf8';
        let indicatorText = "Bening / Asam";
        if (ph >= 6.8 && ph <= 7.5) {
          color = '#f472b6';
          indicatorText = "Merah Muda (Netral)";
        } else if (ph > 7.5) {
          color = '#db2777';
          indicatorText = "Magenta (Basa)";
        }

        const r1 = document.getElementById('readout-1');
        const r2 = document.getElementById('readout-2');
        const r3 = document.getElementById('readout-3');
        if (r1) r1.innerText = `pH: ${ph}`;
        if (r2) r2.innerText = `Volume: ${drops} mL`;
        if (r3) r3.innerText = indicatorText;

        ctx.strokeStyle = '#94a3b8';
        ctx.lineWidth = 4;
        ctx.strokeRect(w / 2 - 50, h / 2 - 20, 100, 100);

        ctx.fillStyle = color;
        ctx.globalAlpha = 0.75;
        ctx.fillRect(w / 2 - 46, h / 2 + 10, 92, 68);
        ctx.globalAlpha = 1.0;

        ctx.fillStyle = '#cbd5e1';
        ctx.fillRect(w / 2 - 6, 20, 12, h / 2 - 50);

      } else if (activeLabMode === 'physics') {
        const v = labParams.physVoltage;
        const r = labParams.physResistance;
        const current = (v / r).toFixed(2);

        const r1 = document.getElementById('readout-1');
        const r2 = document.getElementById('readout-2');
        const r3 = document.getElementById('readout-3');
        if (r1) r1.innerText = `Tegangan: ${v} V`;
        if (r2) r2.innerText = `Hambatan: ${r} Ω`;
        if (r3) r3.innerText = `Arus: ${current} A`;

        ctx.strokeStyle = '#38bdf8';
        ctx.lineWidth = 4;
        ctx.beginPath();
        ctx.rect(w / 2 - 120, h / 2 - 60, 240, 120);
        ctx.stroke();

        ctx.fillStyle = '#0f172a';
        ctx.fillRect(w / 2 - 130, h / 2 - 20, 20, 40);

        const brightness = Math.min(current * 40, 255);
        ctx.fillStyle = `rgb(${brightness}, ${brightness}, 100)`;
        ctx.beginPath();
        ctx.arc(w / 2, h / 2 + 60, 18, 0, Math.PI * 2);
        ctx.fill();

      } else if (activeLabMode === 'biology') {
        const zoom = labParams.bioZoom;
        const r1 = document.getElementById('readout-1');
        const r2 = document.getElementById('readout-2');
        const r3 = document.getElementById('readout-3');
        if (r1) r1.innerText = `Pembesaran: ${zoom}x`;
        if (r2) r2.innerText = `Preparat Sel Daun`;
        if (r3) r3.innerText = `Status: Fokus`;

        ctx.save();
        ctx.beginPath();
        ctx.arc(w / 2, h / 2, 100, 0, Math.PI * 2);
        ctx.clip();

        ctx.fillStyle = '#064e3b';
        ctx.fillRect(0, 0, w, h);

        ctx.strokeStyle = '#34d399';
        ctx.lineWidth = 2;
        const cellSize = Math.max(20, 1200 / zoom);

        for (let x = 0; x < w; x += cellSize) {
          for (let y = 0; y < h; y += cellSize) {
            ctx.strokeRect(x, y, cellSize, cellSize);
            ctx.fillStyle = '#10b981';
            ctx.beginPath();
            ctx.arc(x + cellSize / 3, y + cellSize / 3, cellSize / 8, 0, Math.PI * 2);
            ctx.fill();
          }
        }
        ctx.restore();

        ctx.strokeStyle = '#94a3b8';
        ctx.lineWidth = 6;
        ctx.beginPath();
        ctx.arc(w / 2, h / 2, 100, 0, Math.PI * 2);
        ctx.stroke();
      }
    }

    function runLabSimulation() {
      showToast("Praktikum di-reset!", "info");
      labParams = { chemDrops: 0, chemPh: 1.0, physVoltage: 6, physResistance: 10, bioZoom: 100 };
      renderLabControls();
      drawLab();
    }

    function saveLabResult() {
      logActivity(`${currentUser.name} menyimpan catatan praktikum.`);
      showToast("Praktikum berhasil dicatat!");
    }

    /* AI TUTOR */
    function sendPresetQuery(q) {
      document.getElementById('chat-input').value = q;
      handleChatSubmit(new Event('submit'));
    }

    function handleChatSubmit(e) {
      e.preventDefault();
      const input = document.getElementById('chat-input');
      const query = input.value.trim();
      if (!query) return;

      const chatBox = document.getElementById('chat-box');
      chatBox.innerHTML += `
        <div class="flex items-start justify-end space-x-3 fade-in">
          <div class="bg-emerald-600 text-white p-3.5 rounded-2xl rounded-tr-none text-xs leading-relaxed max-w-xl">${query}</div>
        </div>
      `;
      input.value = '';
      chatBox.scrollTop = chatBox.scrollHeight;

      setTimeout(() => {
        chatBox.innerHTML += `
          <div class="flex items-start space-x-3 fade-in">
            <div class="w-8 h-8 rounded-lg bg-amber-500 text-white flex items-center justify-center text-xs shrink-0 mt-1"><i class="fa-solid fa-robot"></i></div>
            <div class="bg-white p-4 rounded-2xl rounded-tl-none border border-slate-200 text-xs text-slate-700 leading-relaxed max-w-xl">
              Pertanyaan mengenai <em>"${query}"</em> sangat bagus! Cobalah uji parameternya di simulasi Lab Virtual kami.
            </div>
          </div>
        `;
        chatBox.scrollTop = chatBox.scrollHeight;
      }, 600);
    }

    function clearChat() {
      document.getElementById('chat-box').innerHTML = '';
    }

    window.onresize = function() {
      initLabCanvas();
      drawLab();
    };
  </script>
</body>
</html>
