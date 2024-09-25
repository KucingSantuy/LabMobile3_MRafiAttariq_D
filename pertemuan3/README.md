# Penjelasan Kode Flutter App

## main.dart

1. **Inisialisasi dan Pengecekan Login:**
   ```dart
   void main() async {
     WidgetsFlutterBinding.ensureInitialized();
     SharedPreferences prefs = await SharedPreferences.getInstance();
     bool isLoggedIn = prefs.getBool('isLoggedIn') ?? false;
     runApp(MyApp(isLoggedIn: isLoggedIn));
   }
   ```
   - Fungsi ini menginisialisasi aplikasi.
   - Menggunakan `SharedPreferences` untuk memeriksa status login pengguna.
   - Menjalankan aplikasi dengan status login yang telah ditentukan.

2. **Definisi Routes:**
   ```dart
   class Routes {
     static const String login = '/login';
     static const String home = '/home';
   }
   ```
   - Mendefinisikan konstanta untuk route aplikasi.

3. **Kelas MyApp:**
   ```dart
   class MyApp extends StatelessWidget {
     final bool isLoggedIn;
     // ...
   }
   ```
   - Widget utama aplikasi.
   - Menerima status login sebagai parameter.
   - Mengatur tema aplikasi dan menentukan route awal berdasarkan status login.

## login_screen.dart

1. **Struktur Widget:**
   - Menggunakan `StatefulWidget` karena perlu mengelola state untuk proses login.

2. **UI Login:**
   - Menggunakan `TextField` untuk input username dan password.
   - Tombol login dengan indikator loading.

3. **Proses Login:**
   ```dart
   void _login(BuildContext context) async {
     // ...
     if (_usernameController.text == 'admin' && _passwordController.text == 'password') {
       SharedPreferences prefs = await SharedPreferences.getInstance();
       await prefs.setBool('isLoggedIn', true);
       Navigator.of(context).pushReplacementNamed(Routes.home);
     } else {
       // Tampilkan pesan error
     }
   }
   ```
   - Memeriksa kredensial (hardcoded untuk demo).
   - Menyimpan status login ke `SharedPreferences`.
   - Navigasi ke home screen jika login berhasil.

## home_screen.dart

1. **AppBar dan Drawer:**
   - AppBar dengan tombol logout.
   - Drawer dengan menu navigasi.

2. **Body Home Screen:**
   - Menampilkan pesan selamat datang dan ikon.

3. **Fungsi Logout:**
   ```dart
   void _logout(BuildContext context) async {
     SharedPreferences prefs = await SharedPreferences.getInstance();
     await prefs.setBool('isLoggedIn', false);
     Navigator.of(context).pushReplacementNamed(Routes.login);
   }
   ```
   - Mengubah status login di `SharedPreferences`.
   - Navigasi kembali ke login screen.

Aplikasi ini mendemonstrasikan alur dasar autentikasi, manajemen state sederhana, dan navigasi antar halaman dalam Flutter.

# Screenshot
