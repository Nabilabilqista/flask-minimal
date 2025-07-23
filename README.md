# Setup Manual & Reboot Service Flask
Untuk menjalankan aplikasi Flask secara otomatis di latar belakang, termasuk saat terminal ditutup atau server direboot, ikuti langkah-langkah berikut:

## Langkah-langkah:
1. Connect ke EC2
2. Ketik
   ```bash
   ls
   cd flask-minimal
   ```
3. Buat file service systemd:
   ```bash
   sudo nano /etc/systemd/system/flaskapp.service
   ```
4. Salin dan tempel konfigurasi berikut:
   ```bash
   [Unit]
   Description=Flask Minimal App
   After=network.target

   [Service]
   User=ubuntu
   WorkingDirectory=/home/ubuntu/flask-minimal
   ExecStart=/home/ubuntu/flask-minimal/venv/bin/python app.py
   Restart=always

   [Install]
   WantedBy=multi-user.target
   ```
5. Reload systemd dan daftarkan servicenya:
   ```bash
   sudo systemctl daemon-reexec
   sudo systemctl daemon-reload
   sudo systemctl enable flaskapp.service
   sudo systemctl start flaskapp.service
   ```
6. Cek status untuk memastikan service berjalan dengan baik:
   ```bash
   sudo systemctl status flaskapp.service
   ```

## Langkah Terakhir
Salin ip public dan tempel di browser, jangan lupa tambahkan :5000 di belakang

## Hasil Akhir
Setelah mengikuti langkah di atas, aplikasi Flask akan:
Berjalan di latar belakang (background)
Otomatis menyala ulang jika terjadi crash
Tetap berjalan secara otomatis setiap kali server direboot
Kamu tidak perlu menjalankan ulang aplikasi secara manual setiap kali login ke server!

## Otomatisasi
Kalau kamu reboot server sekarang (sudo reboot), aplikasi Flask akan tetap berjalan tanpa kamu harus menjalankannya lagi. Kamu hanya perlu cek statusnya:
```bash
   sudo systemctl status flaskapp.service
```
