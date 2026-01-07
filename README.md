# Pemesanan-makanan-
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pemesanan Makanan</title>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600&display=swap" rel="stylesheet">
    <script type="text/javascript" src="https://cdn.jsdelivr.net/npm/@emailjs/browser@3/dist/email.min.js"></script>
    <script type="text/javascript">
        emailjs.init('u5oCRLoB6lKqLNVrh');
    </script>
    <style>
        body {
            font-family: 'Poppins', sans-serif;
            max-width: 600px;
            margin: 2rem auto;
            padding: 0 1rem;
            background-image: url('quality_restoration_20260107123637895.jpg');
            background-size: cover;
            background-position: center;
            background-repeat: no-repeat;
            overflow-x: hidden;
        }
        h1 {
            font-weight: 600;
            color: #d63384;
            text-align: center;
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-bottom: 0.5rem;
        }
        .tagline {
            text-align: center;
            color: #6c757d;
            margin-top: 0;
            margin-bottom: 1.5rem;
            font-size: 0.9rem;
        }
        .menu-info {
            font-weight: 500;
            color: #495057;
            text-align: center;
            font-size: 1.1rem;
            background-color: #fff3cd;
            padding: 0.8rem;
            border-radius: 8px;
            margin-bottom: 1.5rem;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
        }
        .form-group {
            margin-bottom: 1.2rem;
        }
        label {
            display: block;
            margin-bottom: 0.5rem;
            font-weight: 500;
            color: #212529;
            font-size: 0.95rem;
        }
        input, textarea, select {
            width: 100%;
            padding: 0.7rem;
            border: 1px solid #ddd;
            border-radius: 4px;
            box-sizing: border-box;
            font-family: 'Poppins', sans-serif;
            font-size: 0.9rem;
            transition: border-color 0.3s ease, box-shadow 0.3s ease;
        }
        input:focus, textarea:focus, select:focus {
            outline: none;
            border-color: #d63384;
            box-shadow: 0 0 0 2px rgba(214, 51, 132, 0.1);
        }
        button {
            background-color: #d63384;
            color: white;
            padding: 0.8rem 1.5rem;
            border: none;
            border-radius: 4px;
            font-size: 1rem;
            cursor: pointer;
            font-family: 'Poppins', sans-serif;
            font-weight: 500;
            text-transform: uppercase;
            letter-spacing: 1px;
            width: 100%;
            transition: background-color 0.3s ease, transform 0.2s ease;
            box-shadow: 0 3px 6px rgba(214, 51, 132, 0.2);
        }
        button:hover {
            background-color: #c22576;
            transform: translateY(-2px);
        }
        button:active {
            transform: translateY(0);
        }
        .radio-group, .menu-check-group {
            display: flex;
            gap: 1.5rem;
            align-items: center;
            padding: 0.5rem 0;
        }
        .menu-item {
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }
        /* Tambahan untuk input jumlah per menu */
        .menu-quantity {
            width: 60px;
            padding: 0.3rem;
            margin-left: 0.5rem;
        }
        .order-card {
            background-color: rgba(255, 255, 255, 0.7);
            padding: 1.5rem 2rem;
            border-radius: 12px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.08);
        }
    </style>
</head>
<body>
    <div class="order-card">
        <h1>Pemesanan</h1>
        <p class="tagline">Nikmati kelezatan makanan pilihan dengan bumbu spesial!</p>
        
        <div class="menu-info" id="totalDisplay">
            <strong>Total Harga:</strong> Rp 0
        </div>

        <form id="orderForm">
            <!-- Pilihan Menu dengan Checkbox & Jumlah per Menu -->
            <div class="form-group">
                <label>Pilih Menu:</label>
                <div class="menu-check-group" style="flex-direction: column; gap: 1rem; align-items: flex-start;">
                    <!-- Menu Bakso Aci -->
                    <div class="menu-item">
                        <input type="checkbox" id="menuBakso" name="menu[]" value="Bakso Aci" data-price="10000">
                        <label for="menuBakso">Bakso Aci (Rp 10.000/porsi)</label>
                        <input type="number" class="menu-quantity" id="qtyBakso" name="qtyBakso" min="1" value="1" disabled>
                    </div>

                    <!-- Menu Cireng Isi -->
                    <div class="menu-item">
                        <input type="checkbox" id="menuCireng" name="menu[]" value="Cireng Isi (6 buah)" data-price="12000">
                        <label for="menuCireng">Cireng Isi (6 buah) (Rp 12.000/porsi)</label>
                        <input type="number" class="menu-quantity" id="qtyCireng" name="qtyCireng" min="1" value="1" disabled>
                    </div>
                </div>
            </div>

            <!-- Pilihan Uang Pas -->
            <div class="form-group">
                <label>Pilihan Uang Pas:</label>
                <div class="radio-group">
                    <div>
                        <input type="radio" id="uangPasYa" name="uangPas" value="Ya" required>
                        <label for="uangPasYa">Ya</label>
                    </div>
                    <div>
                        <input type="radio" id="uangPasTidak" name="uangPas" value="Tidak">
                        <label for="uangPasTidak">Tidak</label>
                    </div>
                </div>
            </div>

            <!-- Alamat Pengiriman -->
            <div class="form-group">
                <label for="deliveryAddress">Dikirim ke:</label>
                <textarea id="deliveryAddress" name="deliveryAddress" rows="3" placeholder="Contoh: Jl. Merdeka No. 123, Kelurahan Sukamenak, Kecamatan Karawang Barat..." required></textarea>
            </div>

            <!-- Note Tambahan -->
            <div class="form-group">
                <label for="note">Note Tambahan:</label>
                <textarea id="note" name="note" rows="2" placeholder="Contoh: Kurang pedas, tambah bawang merah goreng..."></textarea>
            </div>

            <button type="submit">Kirim Pesanan</button>
        </form>
    </div>

    <script>
        // Ambil semua elemen menu dan input jumlah
        const menuCheckboxes = document.querySelectorAll('input[name="menu[]"]');
        const menuQuantities = document.querySelectorAll('.menu-quantity');
        const totalDisplay = document.getElementById('totalDisplay');

        // Aktifkan/nonaktifkan input jumlah saat checkbox dicentang
        menuCheckboxes.forEach(checkbox => {
            checkbox.addEventListener('change', function() {
                const qtyInput = document.getElementById(`qty${this.id.replace('menu', '')}`);
                qtyInput.disabled = !this.checked;
                calculateTotal(); // Hitung total setiap kali ada perubahan
            });
        });

        // Hitung total harga setiap kali jumlah berubah
        menuQuantities.forEach(input => {
            input.addEventListener('input', function() {
                if (this.value < 1) this.value = 1;
                calculateTotal();
            });
        });

        // Fungsi menghitung total harga
        function calculateTotal() {
            let total = 0;
            menuCheckboxes.forEach(checkbox => {
                if (checkbox.checked) {
                    const price = parseInt(checkbox.dataset.price);
                    const qty = parseInt(document.getElementById(`qty${checkbox.id.replace('menu', '')}`).value);
                    total += price * qty;
                }
            });
            totalDisplay.innerHTML = `<strong>Total Harga:</strong> Rp ${total.toLocaleString('id-ID')}`;
        }

        // Fungsi submit form
        document.getElementById('orderForm').addEventListener('submit', function(e) {
            e.preventDefault();

            // Cek apakah minimal satu menu dipilih
            const selectedMenus = document.querySelectorAll('input[name="menu[]"]:checked');
            if (selectedMenus.length === 0) {
                alert('⚠️ Silakan pilih minimal satu menu terlebih dahulu!');
                return;
            }

            // Siapkan detail pesanan untuk alert dan email
            let orderDetails = '';
            let totalHarga = 0;
            selectedMenus.forEach(checkbox => {
                const menuName = checkbox.value;
                const menuPrice = parseInt(checkbox.dataset.price);
                const menuQty = parseInt(document.getElementById(`qty${checkbox.id.replace('menu', '')}`).value);
                const subtotal = menuPrice * menuQty;
                orderDetails += `- ${menuName}: ${menuQty} porsi (Rp ${menuPrice.toLocaleString('id-ID')}/porsi) → Subtotal: Rp ${subtotal.toLocaleString('id-ID')}\n`;
                totalHarga += subtotal;
            });

            // Kirim data ke Gmail via EmailJS
            emailjs.sendForm('service_uzfu70i', 'template_7ljv484', this)
                .then(() => {
                    alert(`✅ PESANAN BERHASIL TERKIRIM! \n\n📝 Detail Pesanan: \n${orderDetails}\nTotal Harga: Rp ${totalHarga.toLocaleString('id-ID')} \nUang Pas: ${document.querySelector('input[name="uangPas"]:checked').value} \n\n📧 Notifikasi sudah kami kirim ke Gmail. Terima kasih!`);
                    
                    // Reset form setelah berhasil
                    this.reset();
                    menuQuantities.forEach(input => input.disabled = true);
                    totalDisplay.innerHTML = `<strong>Total Harga:</strong> Rp 0`;
                }, (error) => {
                    alert('❌ Maaf, pesanan gagal terkirim. Silakan coba lagi nanti!');
                    console.log('Error:', error);
                });
        });
    </script>
</body>
</html>
