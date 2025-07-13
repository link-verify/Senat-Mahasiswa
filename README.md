<?php
session_start();

// Data user statis
$users = [
  ["username" => "ketua", "password" => "1234", "role" => "Ketua"],
  ["username" => "sekretaris", "password" => "1234", "role" => "Sekretaris"],
  ["username" => "bendahara", "password" => "1234", "role" => "Bendahara"],
];

// Logout
if (isset($_GET['logout'])) {
  session_destroy();
  header("Location: organisasi.php");
  exit();
}

// Tangani login
$error = '';
if (isset($_POST['login'])) {
  $username = $_POST['username'] ?? '';
  $password = $_POST['password'] ?? '';

  $found = false;
  foreach ($users as $user) {
    if ($user['username'] === $username && $user['password'] === $password) {
      $_SESSION['user'] = $user;
      $found = true;
      break;
    }
  }

  if (!$found) {
    $error = "Username atau password salah!";
  }
}

// Tangani logout link
if (isset($_GET['logout'])) {
  session_destroy();
  header("Location: organisasi.php");
  exit();
}

// Tampilkan halaman
$user = $_SESSION['user'] ?? null;
?>

<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <title>Organisasi - Sistem Login</title>
  <style>
    body { font-family: Arial, sans-serif; background: #f0f2f5; margin: 0; padding: 0; }
    .container { max-width: 400px; margin: 50px auto; background: #fff; border-radius: 8px; box-shadow: 0 8px 30px rgba(0,0,0,0.1); padding: 30px; }
    h2 { margin-top: 0; color: #0047AB; }
    input { width: 100%; padding: 10px; margin-bottom: 15px; border: 1px solid #ccc; border-radius: 4px; }
    button { width: 100%; padding: 10px; background: #0047AB; color: #fff; border: none; border-radius: 4px; cursor: pointer; }
    button:hover { background: #0066CC; }
    .error { color: red; font-size: 12px; }
    .welcome { text-align: center; }
    .logout { display: inline-block; margin-top: 15px; color: #0047AB; text-decoration: none; }
    .card { background: #f9f9f9; padding: 15px; border-radius: 5px; margin-top: 20px; box-shadow: 0 4px 15px rgba(0,0,0,0.1); }
  </style>
</head>
<body>

<div class="container">
  <?php if (!$user): ?>
    <h2>Login Organisasi</h2>
    <form method="POST">
      <input type="text" name="username" placeholder="Username" required />
      <input type="password" name="password" placeholder="Password" required />
      <?php if($error): ?>
        <div class="error"><?= $error ?></div>
      <?php endif; ?>
      <button type="submit" name="login">Login</button>
    </form>
  <?php else: ?>
    <div class="welcome">
      <h2>Selamat Datang, <?= htmlspecialchars($user['username']); ?>!</h2>
      <p>Peran Anda: <strong><?= $user['role']; ?></strong></p>
      <a class="logout" href="?logout=1">Logout</a>
    </div>

    <div class="card">
      <?php if ($user['role'] == "Ketua"): ?>
        <h3>Menu Ketua</h3>
        <ul>
          <li>Kelola agenda rapat</li>
          <li>Verifikasi laporan keuangan</li>
        </ul>
      <?php elseif ($user['role'] == "Sekretaris"): ?>
        <h3>Menu Sekretaris</h3>
        <ul>
          <li>Input notulen rapat</li>
          <li>Update dokumen organisasi</li>
        </ul>
      <?php elseif ($user['role'] == "Bendahara"): ?>
        <h3>Menu Bendahara</h3>
        <ul>
          <li>Input laporan keuangan</li>
          <li>Lihat laporan kas</li>
        </ul>
      <?php endif; ?>
    </div>
  <?php endif; ?>
</div>

</body>
</html>