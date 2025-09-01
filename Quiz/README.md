## Quiz 1: Playbook

Tujuan:
1. Membuat konfigurasi ansible.cfg dan inventory untuk mendefinisikan target host.
2. Menulis playbook yang:
    - Menginstal paket-paket penting (Apache2, MariaDB, PHP, PHP-MySQL).
    - Memastikan service Apache2 dan MariaDB berjalan dan otomatis aktif saat boot.
    - Meng-deploy konten web sederhana di /var/www/html/index.php.
3. Menambahkan play kedua untuk melakukan verifikasi dari control node dengan Ansible module uri.
4. Membuktikan bahwa Ansible mampu mengotomatisasi instalasi, konfigurasi, dan pengujian dalam satu eksekusi.

Kegunaan Praktis:
Dengan pendekatan ini, administrator dapat men-setup server LAMP (Linux + Apache + MariaDB + PHP) hanya dengan satu perintah, serta memastikan server berfungsi tanpa harus menguji manual satu per satu.

Implementasi Langkah:

- Membuat direktori kerja
    ```bash
    mkdir quiz-1
    cd quiz-1

- Membuat file ansible.cfg

Isinya: "ansible.cfg"

- Membuat file inventory

Isinya: "inventory"

- Membuat playbook quiz-1_playbook.yml

Isinya: "quiz-1_playbook.yml"

- Eksekusi Playbook
    - Cek syntax:
    ```bash
    ansible-playbook --syntax-check quiz-1_playbook.yml
    ```
    - Jalankan playbook:
    ```bash
    ansible-playbook quiz-1_playbook.yml
    ```

![Screenshot Terminal](Gambar/gambar1.png)

- Verifikasi manual:
    ```bash
    curl pod-sinfang-managed2/index.php
    ```

![Screenshot Terminal](Gambar/gambar2.png)

 
Kesimpulan:
Quiz ini membuktikan bahwa Ansible Playbook dapat digunakan untuk:
1. Mengotomatiskan instalasi LAMP stack.
2. Mengelola service secara konsisten di server target.
3. Melakukan verifikasi otomatis dari control node.
Dengan playbook ini, proses yang biasanya dilakukan manual (instalasi paket, konfigurasi service, menyalin file, pengujian web server) dapat dijalankan secara reproducible, cepat, dan minim error.

## Quiz 2: Variables

Tujuan:
1. Lebih fleksibel → cukup ubah nilai variabel, tidak perlu edit ulang semua task.
2. Lebih konsisten → variabel yang dipakai di banyak tempat tetap sama nilainya.
3. Lebih mudah dikelola → terutama saat daftar paket, nama service, atau path file bisa berubah sesuai kebutuhan.

Konsep Dasar & Kegunaan
1. vars section di Playbook → tempat mendefinisikan variabel.
2. Variabel dipanggil menggunakan format {{ variable_name }}.
Contoh penggunaan:
    - name: "{{ required_Pkg }}" untuk menginstall paket.
    - name: "{{ web_Service }}" untuk mengelola service.
    - content: "{{ content_File }}" dan dest: "{{ dest_File }}" untuk menyalin file.
Dengan cara ini, playbook bisa digunakan kembali untuk banyak skenario dengan hanya mengganti nilai variabel.

Implementasi Langkah:

- Buat direktori kerja
    ```bash
    mkdir quiz-2
    cd quiz-2
    ```

- Buat file ansible.cfg

Isinya: "asnible.cfg"

- Buat file inventory

Isinya: "inventory"

- Buat playbook quiz-2_variables.yml

Isinya: quiz-2_variables.yml

- Eksekusi Playbook
    - Cek syntax:
    ```bash
    ansible-playbook --syntax-check quiz-2_variables.yml
    ```
    Jalankan playbook:
    ```bash
    ansible-playbook quiz-2_variables.yml
    ```

![Screenshot Terminal](Gambar/gambar3.png)

- Verifikasi manual:
    ```bash
    curl pod-sinfang-managed2/index.html
    ```

![Screenshot Terminal](Gambar/gambar4.png)

Kesimpulan:
Quiz ini menunjukkan bahwa penggunaan variabel dalam Ansible membuat playbook lebih modular, efisien, dan reusable.
Hanya dengan mengubah nilai variabel, playbook bisa digunakan ulang di host berbeda tanpa perlu menulis ulang seluruh task.

## Quiz 3: Jinja 2 template