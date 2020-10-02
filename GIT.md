AM/FM Week 2
=============

## Outline

* Pengenalan [**git**](#pengenalan-dengan-git)
  * Install git
  * Command-command di CMD
  * Command-command di git
* Pengenalan [**django**](#pengenalan-dengan-django)
  * Install django
  * cara kerja django
  * cara menggunakan django

Pengenalan dengan Git
=====================

**git** adalah _version control system_ yang digunakan para developer untuk mengembangkan software secara bersama-bersama.
Fungsi utama git yaitu mengatur versi dari source code program anda dengan mengasih tanda baris dan code mana yang ditambah atau diganti.

Website: https://git-scm.com/

Apa itu **repository**?\
Apa itu **remote**?\
Apa itu **gitlab** / **github**? Apa perbedaannya?


## Install git

* Download
  * [Windows 64-bit](https://github.com/git-for-windows/git/releases/download/v2.23.0.windows.1/Git-2.23.0-64-bit.exe)
  * Linux (Ubuntu): `sudo apt install git`
* jalankan installer-nya


## Command-Command di CMD

* `cd` (change directory) : pindah ke luar atau ke dalam suatu folder
* `dir` (directory?) : menampilkan list isi folder di posisi sekarang.
* `mkdir <folder_name>` (make directory) : membuat folder baru
* `del <file_name>` (delete) : menghapus sebuah file
* `rmdir <folder_name>` (remove directory) : menghapus sebuah folder


## Git Commands

Command-command git bisa dijalankan lewat **git bash** (yang baru saja diinstall) atau **command prompt** (cmd).

### git init

Untuk membuat repository pada file lokal yang nantinya ada folder .git

* Buat folder baru, misalkan nama foldernya **gabut**
  ```
  mkdir gituan
  ```
* Lalu masuk ke foldernya
  ```
  cd gituan
  ```
* Buat repository git baru
  ```
  git init
  ```

### git config

Mengatur setting di git

* Masukkan nama
  ```
  git config --global user.name "Nama Lengkap Kamu"
  ```
* Masukkan email
  ```
  git config --global user.email "email.kamu@yang.dipake"
  ```
* Dapat dcek dengan menulis:
  ```
  git config -l
  ```
  Apakah `user.name` dan `user.email` ada disitu?

### git status

Untuk mengetahui status dari repository lokal

* Coba cek status
  ```
  git status
  ```
* **Masukkan sebuah file** di dalam folder tersebut
* Cek status lagi
  ```
  git status
  ```
* Seharusnya ada file berwarna <span style="color: red">merah</span>.
  Artinya ada file berbeda dari keadaan awal.

### git add `<nama_file>`

Menambahkan file baru pada repository yang dipilih.

* Tambahkan file yang berubah untuk dicatat git **satu per satu**
  ```
  git add &lt;nama_file&gt;
  ```
  atau tambahkan **semua** file yang berubah
  ```
  git add .
  ```
* Coba sekarang cek status
  ```
  git status
  ```
* Seharusnya file-filenya sekarang berwarna <span style="color: green">hijau</span>.
  Artinya file sudah di ditandai oleh git.
* File-file yang **belum** di add, disebut <span style="color: red">not staged for commit</span>.
* Sedangkan, file-file yang **sudah** di add, disebut <span style="color: green">staged for commit</span>.

### git commit

Untuk menyimpan perubahan yang dilakukan. Seperti mengambil screenshot dari file-file yang saat commit.

* Cek apakah sudah ada file yang _staged_
  ```
  git status
  ```
* Buat commit baru. Harus memassukan pesan apa yang dicommit (-m)
  ```
  git commit -m "pesan yang sabeb"
  ```
  atau _message_ dapat ditulis di text editor
  ```
  git commit
  ```
  kalau yang terbuka adalah **vim**,
    * pndahhkan kursor dengan **arrow key**
    * tombol `i` untuk menulis
    * selesai menulis tekan `esc`
    * seletah `esc`, tekan `:wq` dan `ENTER` untuk keluar

### git log

Untuk melihat commit-commit yang pernah dilakukan

* Melihat log
  ```
  git log
  ```
* Jika lognya panjang sampai bawah, tekan `q` untuk keluar.

### Beberapa Command Lainnya

* `git branch <nama_branch>` : memuat branch baru di repository
* `git branch` : melihat seluruh branch yang ada pada repository
* `git checkout` : menukar branch yang aktif dengan branchyang dipilih
* `git merge` : untuk menggabungkan branch yang aktif dan branch yang dipilih
* `git push` : untuk mengirimkan perubahan file setelah di commit ke remote repository.
* `git clone` : membuat Salinan repository lokal


## Bahan Belajar

* **https://learngitbranching.js.org/**


Pengenalan dengan Django
========================

## Project Django Pertama

* Buat folder project (misalkan diberi nama **amfm**).
  Akan muncul folder kosong bernama **amfm**.
  Lalu masuk ke folder baru tersebut.
  ```
  mkdir amfm
  cd amfm
  ```
* Kemudian membuat virtual environment (biasanya **env**).
  Akan muncul folder baru bernama **env**.
  ```
  python -m venv env
  ```
* Lalu masuk ke environment yang baru saja dibuat.
  ```
  env\Scripts\activate.bat
  ```
  > Perlu diperhatikan menggunakan _backslash_ (`\` yang di atas `ENTER`), bukan _slash_ (`/`).
* Setelah itu install _package-package_ python yang dibutuhkan dengan pip, seperti django.
  Disini akan menginstall **django**.
  ```
  pip install django
  ```
* Setelah selesai menginstall, kamu akan mencetak apa saja yang diinstall ke file bernama **requirements.txt**.
  Caranya dengan menggunakan pip freeze. Akan muncul file baru bernama requirements.txt.
  ```
  pip freeze > requirements.txt
  ```
* Lalu kamu bisa memulai untuk membuat project django (memakai nama yang sama, yaitu **amfm**)
  ```
  django-admin startproject amfm .
  ```
  hasilnya akan ada file-file seperti ini:
  ```
  ├── env
  │   ├── Scripts
  │   │   ├── activate.bat
  │   │   ├── ...
  │   │   └── ...
  │   ├── ...
  │   └── ...
  ├── manage.py
  ├── requirements.txt
  └── amfm
      ├── __init__.py
      ├── settings.py
      ├── urls.py
      └── wsgi.py
  ```
* Mulai dari sekarang, kamu dapat menjalankan server **django**.
  ```
  python manage.py runserver
  ```
  Server dapat dibuka di browser (misalkan _Firefox_) dengan memasukkan url `localhost:8000` atau `127.0.0.1:8000`.
  Cara menghentikan servernya dengan menekan **CTRL + C**.\
  **Ingat command ini, karena akan sering digunakan.**


## Setup Git

* Inisialisasi repository git
  ```
  git init
  ```
* Membuat config user (kalau tadi belum):
  ```
  git config --global user.name "Nama Lengkap Kamu"
  git config --global user.email "email.kamu@yang.dipake"
  ```
* Membuat file [**.gitignore**](#file-gitignore), yang berfungsi menyembunyikan file-file yang tidak diperlukan agar tidak disimpan di git.\
  **Iya**, file .gitignore **tidak memiliki** ***extension*** seperti (`.txt` atau `.exe`).\
  Buka dan tekan `CTRL-S` di [link .gitignore ini](https://gist.githubusercontent.com/lepiku/a584e98f9d20a08e38e715dbad4a95e3/raw/ddb223ce3481ed3cb9895056f7c663411f40de4c/.gitignore) untuk mendownload filenya.
  Kemudian dimasukkan ke folder paling luar. Seperti ini:
  ```
  ├── env
  │   ├── ...
  │   └── ...
  ├── .gitignore
  ├── manage.py
  └── amfm
      ├── __init__.py
      ├── **pycache**
      ├── settings.py
      ├── urls.py
      └── wsgi.py
  ```
* simpan sebagai commit baru.
  ```
  git add .
  git commit -m "text commit sabeb"
  ```
* Buat [akun Gitlab](https://gitlab.com/users/sign\_in#register-pane) (Kalau belum punya)
* Buatlah [project baru](https://gitlab.com/projects/new) di gitlab.
  Pastikan projectnya diset agar **Public**.
* Kemudian klik tombol **clone** untuk mendapatkan link gitlab yang **https**.
  ![gitlab link](https://imgur.com/ONG7AXM.png)
* Lalu masukkan tulis di terminal link tersebut seperti ini:
  ```
  git remote add origin https://gitlab.com/username_kamu/amfm.git
  ```
* Lalu coba untuk push ke gitlab.
  ```
  git push -u origin master
  ```
  Dia akan meminta username dan password di gitlab.
  Passwordnya **tersembunyi**, jadi coba saja diketik.
* Jika berhasil, kamu bisa liat project django kamu di https://gitlab.com .

## Aplikasi Django Pertama

* Di django, satu project website dapat memiliki banyak **app**. Kamu akan membuat app pertama kamu, misalkan diberi nama **homepage**.
  ```
  python manage.py startapp homepage
  ```
  Akan ada folder bernama **homepage** isinya seperti ini:
  ```
  ├── env
  ├── homepage
  │   ├── admin.py
  │   ├── apps.py
  │   ├── __init__.py
  │   ├── migrations
  │   ├── models.py
  │   ├── tests.py
  │   └── views.py
  ├── manage.py
  └── amfm
      ├── __init__.py
      ├── settings.py
      ├── urls.py
      └── wsgi.py
  ```
* Buka file **amfm/settings.py**, kemudian tambahkan nama app kamu ke `INSTALLED_APPS`, jadi seperti ini:
  ```python
  INSTALLED_APPS = [
      'django.contrib.admin',
      'django.contrib.auth',
      'django.contrib.contenttypes',
      'django.contrib.sessions',
      'django.contrib.messages',
      'django.contrib.staticfiles',
      'homepage',
  ]
  ```
* Buatlah folder baru bernama **templates** di folder **homepage**.
  ```
  mkdir homepage\templates
  ```
* kemudian masukkan file-file html yang kamu buat dari **tugas pertemuan 1** ke folder **homepage/templates/**.
  setelah memasukan file-file html ke folder templates, akan terlihat seperti ini:
  ```
  ├── homepage
  │   ├── __init__.py
  │   ├── admin.py
  │   ├── apps.py
  │   ├── migrations
  │   ├── models.py
  │   ├── tests.py
  │   ├── templates
  │   │   ├── index.html
  │   │   ├── profile.html
  │   │   ├── ... .html
  │   │   └── ... .html
  │   └── views.py
  ```
  > nama file html tidak harus persis sama.
* buka file **homepage/views.py** kemudian buat fungsi baru di dalamnya, misal diberi nama **index(request)** .
  Ganti `nama_file.html` menjadi file sebenarnya.
  Formatnya seperti ini:
  ```python
  def index(request):
      return render(request, 'nama_file.html')
  ```
  Jika punya lebih dari satu html, buatlah isi **homepage/views.py** menjadi seperti ini:
  ```python
  from django.shortcuts import render

  # Create your views here.
  def index(request):
      return render(request, 'index.html')

  def profile(request):
      return render(request, 'profile.html')

  # diteruskan...
  ```
  > Nama fungsinya bebas, tapi perlu diingat nama-namanya.
* Lalu kamu akan mengatur routing url. caranya adalah dengan membuat file baru **homepage/urls.py**. isinya seperti ini:
  ```python
  from django.urls import path
  from . import views

  app_name = 'homepage'

  urlpatterns = [
      path('', views.index, name='index'),
      path('profile/', views.profile, name='profile'),
      # dilanjutkan ...
  ]
  ```
  Format penulisan pathnya adalah `path('url-yang-diinginkan/', views.nama_fungsi, name='nama_fungsi'),`.
  Pastikan **ada satu** url yang string kosong saja (`''`)
* Kemudian membuat mengubah file **amfm/urls.py** kamu akan mengimport **include** dan menambahkan `urlpatterns` baru:
  ```python
  from django.urls import path, include
  from django.contrib import admin

  urlpatterns = [
      path('admin/', admin.site.urls),
      path('', include('homepage.urls')),
  ]
  ```
  Karena dia meng-_include_ `'homepage.urls'` Django akan mencari file **homepage/urls.py**.
* Sekarang coba dijalankan server djangonya.
  ```
  python manage.py runserver
  ```
  Server dapat dibuka di browser dengan memasukkan url `localhost:8000`.
  Apakah bisa berjalan?\
  Apakah **styling atau gambar** sudah muncul? Sepertinya <span style="color: red">**belum**</span>, tapi tidak apa-apa, karena memang <span style="color: green">belum selesai</span> Wkwkwk.
* Sekarang kamu akan memasukkan semua **stylesheet** (\*.css) dan semua **gambar** (\*.jpg, \*.png, \*.svg, dst.) ke project Django kamu.
  Kamu buat folder baru **homepage/static/**
  ```
  mkdir homepage\static\
  ```
* File-file stylesheet dan gambar kamu masukkan ke folder **homepage/static/**.
  Sehingga struktur filenya kira-kira seperti ini:
  ```
  ├── homepage
  │   ├── ...
  │   ├── ...
  │   ├── static
  │   │   ├── style.css
  │   │   ├── ... .css
  │   │   ├── photo.jpg
  │   │   ├── ... .png
  │   │   └── ... .svg
  │   ├── ...
  │   └── ...
  ```
* Lalu kamu harus membuka **semua file html** yang menggunakan css dan gambar untuk menyesuaikan dengan penulisan Django.
  Format dari django menggunakan **static**, jadi harus menambahkan **load static** di semua file yang menggunakan resource dari folder **static/** pada bagian paling atas. Contohnya seperti ini:
  ```html
  <!DOCTYPE html>
  load static
  <html lang="en">
    <head>
      <meta charset="utf-8">
      <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
      ...
    </head>
    ...
  </html>
  ```
* Ubah semua baris html yang menggunakan css atau gambar:
  * CSS:\
    Awalnya:
    ```html
    <link rel="stylesheet" href="nama_file.css">
    ```
    menjadi:
    ```html
    <link rel="stylesheet" href="{% static 'nama_file.css' %}">
    ```
  * Gambar:\
    Awalnya:
    ```html
    <img src="nama_gambar.jpg">
    ```
    menjadi:
    ```html
    <img src="{% static 'nama_gambar.jpg' %}">
    ```
  > Kalau menggunakan inline style, nggak perlu diapa-apain.
* Url-url juga perlu diubah.\
  Awalnya:
  ```html
  <a href="index.html">...</a>
  <a href="profile.html">...</a>
  ```
  menjadi:
  ```html
  <a href="{% url 'homepage:index' %}">...</a>
  <a href="{% url 'homepage:profile' %}">...</a>
  ```
  > `homepage` adalah **app_name** dari **homepage/urls.py**, sedangkan `index` dan `profil` adalah **name** dari path-path yang ada di `urlpatterns`.
* Kalau kamu mencantumkan memasukkan gambar di **file.css**, misalkan\
  Awalnya:
  ```css
  background-image: url('gambar_background.jpg');
  ```
  Kamu harus menambahkan `/static/` menjadi:
  ```css
  background-image: url('/static/gambar_background.jpg');
  ```
  Django secara default memasukkan file-file static ke path url `/static/`.
  Bergantung pada variable `STATIC_ROOT` di **amfm/settings.py**.
* Jalankan server django, dan buka url `localhost:8000` di browser.
  ```bash
  python manage.py runserver
  ```
  Apakah sekarang **styling atau gambar** sudah muncul? Seharusnya <span style="color: green">**sudah**</span>.
* Jangan lupa `git commit` setelah website berjalan.


## Bahan Belajar

* **https://docs.djangoproject.com/en/2.2/intro/tutorial01/**