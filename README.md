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
