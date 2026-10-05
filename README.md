<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Prototipe Sistem Pengajuan Cuti Online - Kelompok 6 USG</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Alpine.js CDN -->
    <script defer src="https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
</head>
<body class="bg-slate-100 font-sans text-slate-800" x-data="appState()">

    <!-- TOP NAVIGATION BAR / ROLE SWITCHER SIMULATOR -->
    <header class="bg-slate-900 text-white shadow-md sticky top-0 z-50">
        <div class="max-w-7xl mx-auto px-4 py-3 flex flex-col sm:flex-row justify-between items-center gap-3">
            <div class="flex items-center gap-3">
                <div class="bg-blue-600 p-2 rounded-lg text-white font-bold text-lg">
                    <i class="fa-solid fa-calendar-days"></i>
                </div>
                <div>
                    <h1 class="font-bold text-base sm:text-lg">Sistem Pengajuan Cuti Online</h1>
                    <p class="text-xs text-slate-400">Universitas Sunan Gresik • Kelompok 6 (Studi Kasus)</p>
                </div>
            </div>
            
            <!-- Role Switcher Panel for Evaluation -->
            <div class="flex items-center gap-2 bg-slate-800 p-1.5 rounded-lg border border-slate-700">
                <span class="text-xs text-slate-400 px-2 font-medium hidden md:inline">Simulasi Peran:</span>
                <button @click="currentRole = 'login'" :class="currentRole === 'login' ? 'bg-blue-600 text-white' : 'text-slate-300 hover:bg-slate-700'" class="px-3 py-1.5 rounded text-xs font-semibold transition">Login</button>
                <button @click="currentRole = 'karyawan'" :class="currentRole === 'karyawan' ? 'bg-blue-600 text-white' : 'text-slate-300 hover:bg-slate-700'" class="px-3 py-1.5 rounded text-xs font-semibold transition">1. Karyawan</button>
                <button @click="currentRole = 'atasan'" :class="currentRole === 'atasan' ? 'bg-blue-600 text-white' : 'text-slate-300 hover:bg-slate-700'" class="px-3 py-1.5 rounded text-xs font-semibold transition">2. Atasan</button>
                <button @click="currentRole = 'hr'" :class="currentRole === 'hr' ? 'bg-blue-600 text-white' : 'text-slate-300 hover:bg-slate-700'" class="px-3 py-1.5 rounded text-xs font-semibold transition">3. HR</button>
            </div>
        </div>
    </header>

    <!-- MAIN CONTAINER -->
    <main class="max-w-7xl mx-auto px-4 py-8">

        <!-- ================= PAGE 1: LOGIN & AUTENTIKASI ================= -->
        <div x-show="currentRole === 'login'" class="max-w-md mx-auto bg-white rounded-2xl shadow-xl overflow-hidden border border-slate-200 my-10">
            <div class="bg-gradient-to-r from-blue-700 to-indigo-800 p-6 text-white text-center">
                <div class="w-16 h-16 bg-white/10 rounded-full flex items-center justify-center mx-auto mb-3 text-2xl backdrop-blur-sm">
                    <i class="fa-solid fa-lock"></i>
                </div>
                <h2 class="text-xl font-bold">Portal Autentikasi Sistem</h2>
                <p class="text-xs text-blue-200 mt-1">Silakan pilih hak akses peran pengguna</p>
            </div>
            <div class="p-6 space-y-4">
                <div>
                    <label class="block text-xs font-semibold text-slate-600 uppercase mb-1">Pilih Hak Akses Role</label>
                    <select x-model="selectedRoleLogin" class="w-full px-3 py-2 border border-slate-300 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-blue-500">
                        <option value="karyawan">Karyawan (Diana Muchibbatul Chabibah - 25120040)</option>
                        <option value="atasan">Atasan / Manager (Bapak Ahmad, S.T.)</option>
                        <option value="hr">HR / Personalia (Ibu Siska, M.M.)</option>
                    </select>
                </div>
                <div>
                    <label class="block text-xs font-semibold text-slate-600 uppercase mb-1">Email / NIP</label>
                    <input type="text" value="diana.25120040@student.usg.ac.id" readonly class="w-full px-3 py-2 bg-slate-50 border border-slate-200 rounded-lg text-sm text-slate-500">
                </div>
                <div>
                    <label class="block text-xs font-semibold text-slate-600 uppercase mb-1">Kata Sandi</label>
                    <input type="password" value="********" readonly class="w-full px-3 py-2 bg-slate-50 border border-slate-200 rounded-lg text-sm text-slate-500">
                </div>
                <button @click="currentRole = selectedRoleLogin" class="w-full bg-blue-600 hover:bg-blue-700 text-white font-medium py-2.5 rounded-lg transition text-sm shadow-md">
                    Masuk ke Sistem <i class="fa-solid fa-arrow-right ml-1"></i>
                </button>
            </div>
        </div>

        <!-- ================= PAGE 2: DASHBOARD KARYAWAN ================= -->
        <div x-show="currentRole === 'karyawan'" class="space-y-6">
            <!-- Welcome Banner -->
            <div class="bg-gradient-to-r from-blue-600 to-cyan-600 rounded-2xl p-6 text-white shadow-lg flex flex-col md:flex-row justify-between items-start md:items-center gap-4">
                <div>
                    <span class="bg-blue-500/50 text-white text-xs px-2.5 py-1 rounded-full font-medium">Dashboard Karyawan</span>
                    <h2 class="text-2xl font-bold mt-2">Selamat Datang, Diana Muchibbatul Chabibah</h2>
                    <p class="text-blue-100 text-sm">NIM/ID: 25120040 | Ajukan permohonan cuti Anda dengan mudah dan pantau statusnya secara real-time.</p>
                </div>
                <div class="bg-white/10 backdrop-blur-md px-4 py-3 rounded-xl border border-white/20 text-center min-w-[160px]">
                    <span class="text-xs text-blue-100 block">Sisa Saldo Cuti</span>
                    <span class="text-3xl font-extrabold text-white" x-text="sisaCuti"></span> <span class="text-xs">Hari</span>
                </div>
            </div>

            <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
                <!-- Form Pengajuan Cuti -->
                <div class="bg-white rounded-2xl p-6 shadow-sm border border-slate-200 lg:col-span-1">
                    <h3 class="font-bold text-slate-800 text-base mb-4 flex items-center gap-2">
                        <i class="fa-solid fa-file-pen text-blue-600"></i> Form Pengajuan Cuti Baru
                    </h3>
                    <form @submit.prevent="submitCuti()" class="space-y-4">
                        <div>
                            <label class="block text-xs font-semibold text-slate-600 mb-1">Jenis Cuti</label>
                            <select x-model="newCuti.jenis" class="w-full px-3 py-2 border border-slate-300 rounded-lg text-sm focus:ring-2 focus:ring-blue-500">
                                <option value="Cuti Tahunan">Cuti Tahunan</option>
                                <option value="Cuti Sakit">Cuti Sakit (Dengan Surat Dokter)</option>
                                <option value="Cuti Keperluan Penting">Cuti Keperluan Penting</option>
                            </select>
                        </div>
                        <div class="grid grid-cols-2 gap-2">
                            <div>
                                <label class="block text-xs font-semibold text-slate-600 mb-1">Tanggal Mulai</label>
                                <input type="date" x-model="newCuti.mulai" required class="w-full px-3 py-2 border border-slate-300 rounded-lg text-sm">
                            </div>
                            <div>
                                <label class="block text-xs font-semibold text-slate-600 mb-1">Tanggal Selesai</label>
                                <input type="date" x-model="newCuti.selesai" required class="w-full px-3 py-2 border border-slate-300 rounded-lg text-sm">
                            </div>
                        </div>
                        <div>
                            <label class="block text-xs font-semibold text-slate-600 mb-1">Alasan Cuti</label>
                            <textarea x-model="newCuti.alasan" rows="3" placeholder="Tuliskan alasan pengajuan cuti..." required class="w-full px-3 py-2 border border-slate-300 rounded-lg text-sm"></textarea>
                        </div>
                        <button type="submit" class="w-full bg-blue-600 hover:bg-blue-700 text-white font-medium py-2 rounded-lg transition text-sm shadow">
                            Kirim Pengajuan Cuti
                        </button>
                    </form>
                </div>

                <!-- Riwayat & Status Pengajuan -->
                <div class="bg-white rounded-2xl p-6 shadow-sm border border-slate-200 lg:col-span-2">
                    <h3 class="font-bold text-slate-800 text-base mb-4 flex items-center gap-2">
                        <i class="fa-solid fa-clock-rotate-left text-blue-600"></i> Riwayat & Status Pengajuan Cuti
                    </h3>
                    <div class="overflow-x-auto">
                        <table class="w-full text-left border-collapse text-sm">
                            <thead>
                                <tr class="bg-slate-50 border-b border-slate-200 text-slate-600 text-xs uppercase">
                                    <th class="p-3">Jenis</th>
                                    <th class="p-3">Tanggal</th>
                                    <th class="p-3">Durasi</th>
                                    <th class="p-3">Alasan</th>
                                    <th class="p-3">Status</th>
                                </tr>
                            </thead>
                            <tbody class="divide-y divide-slate-100">
                                <template x-for="item in daftarCuti" :key="item.id">
                                    <tr>
                                        <td class="p-3 font-medium text-slate-800" x-text="item.jenis"></td>
                                        <td class="p-3 text-slate-600 text-xs" x-text="item.mulai + ' s.d ' + item.selesai"></td>
                                        <td class="p-3 text-slate-600" x-text="item.durasi + ' Hari'"></td>
                                        <td class="p-3 text-slate-600 text-xs" x-text="item.alasan"></td>
                                        <td class="p-3">
                                            <span class="px-2.5 py-1 rounded-full text-xs font-semibold"
                                                :class="{
                                                    'bg-amber-100 text-amber-700': item.status === 'Pending (Menunggu Atasan)',
                                                    'bg-emerald-100 text-emerald-700': item.status === 'Disetujui',
                                                    'bg-rose-100 text-rose-700': item.status === 'Ditolak'
                                                }" x-text="item.status"></span>
                                        </td>
                                    </tr>
                                </template>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>

        <!-- ================= PAGE 3: DASHBOARD ATASAN ================= -->
        <div x-show="currentRole === 'atasan'" class="space-y-6">
            <div class="bg-gradient-to-r from-indigo-700 to-purple-800 rounded-2xl p-6 text-white shadow-lg flex justify-between items-center">
                <div>
                    <span class="bg-indigo-500/50 text-white text-xs px-2.5 py-1 rounded-full font-medium">Dashboard Atasan / Manager</span>
                    <h2 class="text-2xl font-bold mt-2">Persetujuan Cuti Bawahan</h2>
                    <p class="text-indigo-100 text-sm">Evaluasi, berikan catatan, atau gunakan fitur *One-Click Approval* untuk percepat proses.</p>
                </div>
                <div class="hidden sm:block text-right">
                    <span class="text-xs text-indigo-200">Pending Review</span>
                    <span class="text-3xl font-extrabold block" x-text="daftarCuti.filter(i => i.status.includes('Pending')).length"></span>
                </div>
            </div>

            <div class="bg-white rounded-2xl p-6 shadow-sm border border-slate-200">
                <div class="flex justify-between items-center mb-4">
                    <h3 class="font-bold text-slate-800 text-base">Daftar Permohonan Masuk</h3>
                    <span class="text-xs text-slate-500 bg-slate-100 px-3 py-1 rounded-lg">Menampilkan semua bawahan</span>
                </div>

                <div class="space-y-4">
                    <template x-for="item in daftarCuti" :key="item.id">
                        <div class="border border-slate-200 rounded-xl p-4 flex flex-col md:flex-row justify-between items-start md:items-center gap-4 bg-slate-50/50">
                            <div class="space-y-1">
                                <div class="flex items-center gap-2">
                                    <span class="font-bold text-slate-800" x-text="item.nama"></span>
                                    <span class="text-xs bg-slate-200 text-slate-700 px-2 py-0.5 rounded" x-text="item.nim"></span>
                                    <span class="text-xs font-semibold px-2 py-0.5 rounded"
                                        :class="{
                                            'bg-amber-100 text-amber-700': item.status.includes('Pending'),
                                            'bg-emerald-100 text-emerald-700': item.status === 'Disetujui',
                                            'bg-rose-100 text-rose-700': item.status === 'Ditolak'
                                        }" x-text="item.status"></span>
                                </div>
                                <p class="text-xs text-slate-600"><strong class="text-slate-700">Jenis:</strong> <span x-text="item.jenis"></span> | <strong class="text-slate-700">Durasi:</strong> <span x-text="item.mulai + ' s.d ' + item.selesai"></span> (<span x-text="item.durasi"></span> Hari)</p>
                                <p class="text-xs text-slate-600"><strong class="text-slate-700">Alasan:</strong> <span x-text="item.alasan"></span></p>
                            </div>

                            <div class="flex items-center gap-2 w-full md:w-auto justify-end">
                                <template x-if="item.status.includes('Pending')">
                                    <div class="flex gap-2 w-full md:w-auto">
                                        <button @click="setujuiCuti(item.id)" class="flex-1 md:flex-initial bg-emerald-600 hover:bg-emerald-700 text-white px-3 py-1.5 rounded-lg text-xs font-medium transition shadow-sm">
                                            <i class="fa-solid fa-check mr-1"></i> Setujui (One-Click)
                                        </button>
                                        <button @click="tolakCuti(item.id)" class="flex-1 md:flex-initial bg-rose-600 hover:bg-rose-700 text-white px-3 py-1.5 rounded-lg text-xs font-medium transition shadow-sm">
                                            <i class="fa-solid fa-xmark mr-1"></i> Tolak
                                        </button>
                                    </div>
                                </template>
                                <template x-if="!item.status.includes('Pending')">
                                    <span class="text-xs text-slate-400 italic">Sudah diproses</span>
                                </template>
                            </div>
                        </div>
                    </template>
                </div>
            </div>
        </div>

        <!-- ================= PAGE 4: DASHBOARD HR ================= -->
        <div x-show="currentRole === 'hr'" class="space-y-6">
            <div class="bg-gradient-to-r from-slate-800 to-slate-900 rounded-2xl p-6 text-white shadow-lg flex justify-between items-center">
                <div>
                    <span class="bg-blue-600 text-white text-xs px-2.5 py-1 rounded-full font-medium">Dashboard HR / Administrator</span>
                    <h2 class="text-2xl font-bold mt-2">Pengelolaan & Rekapitulasi Data Cuti</h2>
                    <p class="text-slate-300 text-sm">Monitor seluruh data cuti karyawan, verifikasi akhir, dan analisis bottleneck persetujuan.</p>
                </div>
                <button @click="alert('Mengunduh laporan rekapitulasi cuti (.CSV / PDF)...')" class="bg-blue-600 hover:bg-blue-700 text-white text-xs px-4 py-2.5 rounded-xl font-medium transition shadow flex items-center gap-2">
                    <i class="fa-solid fa-download"></i> Unduh Laporan
                </button>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                <div class="bg-white p-5 rounded-xl border border-slate-200 shadow-sm">
                    <span class="text-xs text-slate-500 font-semibold uppercase">Total Pengajuan Bulan Ini</span>
                    <h3 class="text-2xl font-bold text-slate-800 mt-1">12 Kasus</h3>
                </div>
                <div class="bg-white p-5 rounded-xl border border-slate-200 shadow-sm">
                    <span class="text-xs text-slate-500 font-semibold uppercase">Rata-Rata Respon Atasan</span>
                    <h3 class="text-2xl font-bold text-amber-600 mt-1">1.8 Hari <span class="text-xs font-normal text-slate-500">(Perlu Auto-Reminder)</span></h3>
                </div>
                <div class="bg-white p-5 rounded-xl border border-slate-200 shadow-sm">
                    <span class="text-xs text-slate-500 font-semibold uppercase">Sistem Status</span>
                    <h3 class="text-2xl font-bold text-emerald-600 mt-1 flex items-center gap-2">
                        <span class="w-3 h-3 bg-emerald-500 rounded-full inline-block animate-pulse"></span> Normal
                    </h3>
                </div>
            </div>

            <!-- Tabel Manajemen HR -->
            <div class="bg-white rounded-2xl p-6 shadow-sm border border-slate-200">
                <h3 class="font-bold text-slate-800 text-base mb-4">Master Data & Log Cuti Karyawan</h3>
                <div class="overflow-x-auto">
                    <table class="w-full text-left border-collapse text-sm">
                        <thead>
                            <tr class="bg-slate-50 border-b border-slate-200 text-slate-600 text-xs uppercase">
                                <th class="p-3">Nama Karyawan</th>
                                <th class="p-3">Jenis Cuti</th>
                                <th class="p-3">Tanggal</th>
                                <th class="p-3">Saldo Cuti Tersisa</th>
                                <th class="p-3">Status Akhir</th>
                            </tr>
                        </thead>
                        <tbody class="divide-y divide-slate-100">
                            <template x-for="item in daftarCuti" :key="item.id">
                                <tr>
                                    <td class="p-3 font-medium text-slate-800" x-text="item.nama"></td>
                                    <td class="p-3 text-slate-600" x-text="item.jenis"></td>
                                    <td class="p-3 text-slate-600 text-xs" x-text="item.mulai"></td>
                                    <td class="p-3 text-slate-600" x-text="item.sisaSaldoBefore + ' Hari'"></td>
                                    <td class="p-3">
                                        <span class="px-2.5 py-1 rounded-full text-xs font-semibold"
                                            :class="{
                                                'bg-amber-100 text-amber-700': item.status.includes('Pending'),
                                                'bg-emerald-100 text-emerald-700': item.status === 'Disetujui',
                                                'bg-rose-100 text-rose-700': item.status === 'Ditolak'
                                            }" x-text="item.status"></span>
                                    </td>
                                </tr>
                            </template>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>

    </main>

    <!-- FOOTER -->
    <footer class="text-center py-6 text-xs text-slate-500 border-t border-slate-200 mt-12">
        <p>Prototipe Sistem Informasi Cuti Online &bull; Dikembangkan untuk Tugas Analisis dan Perancangan Sistem Informasi</p>
        <p class="mt-1">Universitas Sunan Gresik &copy; 2026</p>
    </footer>

    <!-- SCRIPT LOGIC -->
    <script>
        function appState() {
            return {
                currentRole: 'login',
                selectedRoleLogin: 'karyawan',
                sisaCuti: 10,
                newCuti: {
                    jenis: 'Cuti Tahunan',
                    mulai: '',
                    selesai: '',
                    alasan: ''
                },
                daftarCuti: [
                    { id: 1, nama: 'Diana Muchibbatul Chabibah', nim: '25120040', jenis: 'Cuti Tahunan', mulai: '2026-10-10', selesai: '2026-10-12', durasi: 3, alasan: 'Keperluan keluarga mendadak', status: 'Pending (Menunggu Atasan)', sisaSaldoBefore: 10 },
                    { id: 2, nama: 'Misliana', nim: '251200XX', jenis: 'Cuti Sakit', mulai: '2026-09-15', selesai: '2026-09-16', durasi: 2, alasan: 'Demam dan beristirahat total', status: 'Disetujui', sisaSaldoBefore: 8 },
                    { id: 3, nama: 'Dewangga Wisnu Madya', nim: '25120056', jenis: 'Cuti Keperluan Penting', mulai: '2026-09-01', selesai: '2026-09-01', durasi: 1, alasan: 'Mengurus dokumen penting', status: 'Disetujui', sisaSaldoBefore: 11 }
                ],
                submitCuti() {
                    if (this.newCuti.durasi > this.sisaCuti) {
                        alert('Gagal: Pengajuan melebihi sisa saldo cuti Anda!');
                        return;
                    }
                    const newEntry = {
                        id: Date.now(),
                        nama: 'Diana Muchibbatul Chabibah',
                        nim: '25120040',
                        jenis: this.newCuti.jenis,
                        mulai: this.newCuti.mulai,
                        selesai: this.newCuti.selesai,
                        durasi: 2, // Simulasi durasi hitung otomatis
                        alasan: this.newCuti.alasan,
                        status: 'Pending (Menunggu Atasan)',
                        sisaSaldoBefore: this.sisaCuti
                    };
                    this.daftarCuti.unshift(newEntry);
                    this.sisaCuti -= 2;
                    alert('Pengajuan cuti berhasil dikirim ke Atasan!');
                    this.newCuti.alasan = '';
                },
                setujuiCuti(id) {
                    const item = this.daftarCuti.find(i => i.id === id);
                    if (item) {
                        item.status = 'Disetujui';
                        alert('Pengajuan cuti berhasil disetujui (Fitur One-Click Approval Aktif)!');
                    }
                },
                tolakCuti(id) {
                    const item = this.daftarCuti.find(i => i.id === id);
                    if (item) {
                        item.status = 'Ditolak';
                        alert('Pengajuan cuti telah ditolak.');
                    }
                }
            }
        }
    </script>
</body>
</html>
