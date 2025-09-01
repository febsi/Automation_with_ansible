## Managing Roles

Tujuan:
1. Mempelajari konsep roles pada Ansible sebagai cara modularisasi konfigurasi.
2. Membuat role myvhost untuk mengonfigurasi Apache2 Virtual Host secara otomatis.
3. Menggunakan template Jinja2 untuk membangun file konfigurasi virtual host.
4. Memastikan web server dapat berjalan dengan dua vhost berbeda pada dua managed server.
5. Memahami penggunaan pre_tasks dan post_tasks dalam playbook.

Langakh Pengerjaan:

- Membuat direktori kerja:
    ```bash
    mkdir role-create
    cd role-create
    ```

- Buat file konfigurasi Ansible:
    - ansible.cfg   "ansible.cfg"
    - inventory     "inventory1"

- Membuat dirictory role
    ```bash
    mkdir roles
    cd roles
    ansible-galaxy init myvhost
    rm -rvf myvhost/{defaults,vars,tests}
    cd ..
    ```

- Tambahkan direktori untuk HTML:
    ```bash
    mkdir -p roles/myvhost/files/html-1
    mkdir -p roles/myvhost/files/html-2
    echo 'simple index vhost1 : pod-sinfang' > roles/myvhost/files/html-1/index.html
    echo 'simple index vhost2 : pod-sinfang' > roles/myvhost/files/html-2/index.html
    ```

- isi directory roles
    - Membuat tasks
        
        Isinya: roles/tasks/main.yml

    - Membuat handlers

        Isinya: roles/handlers/main.yml

    - Membuat template

        Isinya: roles/templates/vhost-1.conf.j2
        Isinya: roles/templates/vhost-2.conf.j2

Role = cara modularisasi playbook.
tasks/ = isi utama langkah-langkah otomatisasi.
handlers/ = aksi khusus (misalnya restart service).
templates/ = file dinamis dengan variabel (pakai Jinja2).

- Membuat playbook

    Isinya: use-vhost-role.yml


- Syntax check:
    ```bash
    ansible-playbook use-vhost-role.yml --syntax-check
    ```

- Jalankan playbook:
    ```bash
    ansible-playbook use-vhost-role.yml
    ```

- Verifikasi
    Cek hasil konfigurasi vhost di masing-masing managed server:
    ```bash
    curl -H "Host: vhost-1.student" http://pod-username-managed1
    curl -H "Host: vhost-2.student" http://pod-username-managed1
    curl -H "Host: vhost-1.student" http://pod-username-managed2
    curl -H "Host: vhost-2.student" http://pod-username-managed2
    ```
    ![Screenshot Terminal](Gambar/gambar1.png)

Kesimpulan:
1. Roles memudahkan strukturisasi konfigurasi Ansible sehingga lebih modular dan reusable.
2. Konfigurasi Apache2 dengan 2 Virtual Host berhasil di-deploy secara otomatis ke seluruh webserver.
3. Menggunakan template Jinja2 memungkinkan konfigurasi yang dinamis sesuai variabel Ansible.

## Managing Secrets
