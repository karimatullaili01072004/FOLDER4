<?php
// File tempat data disimpan
$dataFile = 'data.txt';

// Membaca data yang ada dalam file
$data = file_exists($dataFile) ? unserialize(file_get_contents($dataFile)) : [
    'dosen' => [],
    'mahasiswa' => [],
    'mata_kuliah' => [],
    'perkuliahan' => []
];

// Menambahkan data baru
if ($_SERVER['REQUEST_METHOD'] === 'POST' && isset($_POST['nama'])) {
    $tipe = $_POST['tipe'];
    $nama = $_POST['nama'];
    $kode = $_POST['kode'];

    // Menambahkan data ke tipe yang sesuai
    $data[$tipe][] = ['nama' => $nama, 'kode' => $kode];

    // Menyimpan data ke file
    file_put_contents($dataFile, serialize($data));

    // Redirect untuk mencegah form duplikat pengiriman
    header("Location: index.php");
    exit;
}

// Menghapus data
if (isset($_GET['hapus'])) {
    $tipe = $_GET['tipe'];
    $index = $_GET['hapus'];

    // Menghapus data dari array
    array_splice($data[$tipe], $index, 1);

    // Menyimpan data ke file
    file_put_contents($dataFile, serialize($data));

    header("Location: index.php");
    exit;
}

// Mengedit data
if (isset($_POST['edit_index'])) {
    $tipe = $_POST['tipe'];
    $index = $_POST['edit_index'];
    $nama = $_POST['edit_nama'];
    $kode = $_POST['edit_kode'];

    // Mengupdate data pada index yang dipilih
    $data[$tipe][$index] = ['nama' => $nama, 'kode' => $kode];

    // Menyimpan data ke file
    file_put_contents($dataFile, serialize($data));

    header("Location: index.php");
    exit;
}
?>

<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Aplikasi Perkuliahan</title>
</head>
<body>
    <div>
        <h1>Manajemen Data Perkuliahan</h1>

        <!-- Form tambah data -->
        <div>
            <h3>Tambah Data</h3>
            <form method="POST" action="index.php">
                <label for="tipe">Tipe Data:</label>
                <select name="tipe" id="tipe" required>
                    <option value="dosen">Dosen</option>
                    <option value="mahasiswa">Mahasiswa</option>
                    <option value="mata_kuliah">Mata Kuliah</option>
                    <option value="perkuliahan">Perkuliahan</option>
                </select>
                <br>
                <label for="nama">Nama:</label>
                <input type="text" name="nama" id="nama" required>
                <br>
                <label for="kode">Kode / NIP / NIM:</label>
                <input type="text" name="kode" id="kode">
                <br>
                <button type="submit">Tambah</button>
            </form>
        </div>

        <!-- Menampilkan data -->
        <h3>Data</h3>
        <div>
            <?php
            foreach ($data as $tipe => $items) {
                echo "<h4>" . ucfirst($tipe) . "</h4>";
                foreach ($items as $index => $item) {
                    echo "<div>
                        <strong>{$tipe}:</strong> {$item['nama']} ({$item['kode']})
                        <a href='?hapus=$index&tipe=$tipe'>Hapus</a>
                        <form method='POST' action='index.php'>
                            <input type='hidden' name='tipe' value='$tipe'>
                            <input type='hidden' name='edit_index' value='$index'>
                            <input type='text' name='edit_nama' value='{$item['nama']}'>
                            <input type='text' name='edit_kode' value='{$item['kode']}'>
                            <button type='submit'>Edit</button>
                        </form>
                    </div>";
                }
            }
            ?>
        </div>
    </div>
</body>
</html>
