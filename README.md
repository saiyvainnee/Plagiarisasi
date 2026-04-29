```
PHP
// Koneksi database sederhana (Rentan SQLi)
$username = $_POST['username'];
$password = $_POST['password'];

// Query langsung digabungkan dengan input pengguna
$query = "SELECT * FROM users WHERE username = '$username' AND password = '$password'";
$result = mysqli_query($conn, $query);

if (mysqli_num_rows($result) > 0) {
echo "Login Berhasil!";
} else {
echo "Login Gagal!";
}
```

```
PHP
// Perbaikan dengan Prepared Statements
$stmt = $pdo->prepare('SELECT * FROM users WHERE username = :username AND password = :password');
$stmt->execute(['username' => $username, 'password' => $password]);
$user = $stmt->fetch();

if ($user) {
echo "Login Berhasil!";
} else {
echo "Login Gagal!";
}
```
Dengan perubahan ini, input ' OR '1'='1 tidak akan berpengaruh, karena database tidak akan membaca karakter tersebut sebagai logika perintah, melainkan sebagai bagian dari string nama pengguna.
