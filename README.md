# Pemrograman Berbasis Framework<br>
Nama : Isna Dewi Malika Arum<br>
Kelas : TI - 2D<br>
NIM : 220102087<br>

**1. Codeigniter4**<br>
=> Kerangka Pengembangan Aplikasi - sebuah toolkit - untuk orang-orang yang membangun situs web menggunakan PHP. <br>
**Basis Data yang Didukung**<br>
=> MySQL melalui MySQLidriver (hanya versi 5.1 ke atas)<br>
=> PostgreSQL melalui Postgredriver (hanya versi 7.4 dan lebih tinggi)<br>
=> SQLite3 melalui SQLite3driver<br>
=> Microsoft SQL Server melalui SQLSRVdriver (hanya versi 2005 dan lebih tinggi)<br>
=> Oracle Database melalui OCI8driver (hanya versi 12.1 dan lebih tinggi)<br>

**2. Installation**<br>
    **a. Composer Installation**
      Teknik pertama buka cmder pada web server, lalu ketikan seperti dibawah<br>
      ```composer create-project codeigniter4/appstarter project-root```<br>
      project-root dapat diganti sesuai nama projek anda<br>
      contohnya <br>
      ![Screenshot 2024-03-18 101407](https://github.com/IsnaDewi/IsnaDewiMalikaArum/assets/134571793/6c42ca1c-a2a5-4daf-81ea-b0ed2399adfb)<br>
      Kemudian untuk menjalankan server ketikan<br>
      ```cd (isikan nama root anda)``` <br>
      lalu ketikan <br>
      ```php spark serve``` <br>
      contohnya<br>
      ![image](https://github.com/IsnaDewi/IsnaDewiMalikaArum/assets/134571793/c3c86f39-5131-4d1b-b00e-7bfe7ff64c5b)<br>

   **3. Build Your First Application** <br>
   Anda akan melewati halaman-halaman berikut:<br>
Pendahuluan, halaman ini, yang memberi Anda gambaran umum tentang apa yang diharapkan dan membuat aplikasi default Anda diunduh dan dijalankan.<br>
 Tutorial ini dimaksudkan untuk memperkenalkan Anda pada framework CodeIgniter4 dan prinsip dasar arsitektur MVC. Ini akan menunjukkan kepada Anda bagaimana aplikasi dasar CodeIgniter dibangun secara langkah demi langkah.<br>
   Tutorial ini terutama akan fokus pada:<br>
      =>Dasar-dasar Model-View-Controller<br>
      =>Dasar-dasar peroutean<br>
      =>Validasi formulir<br>
      =>Melakukan query database dasar menggunakan Model CodeIgniter<br>
**Halaman statis**, yang akan mengajarkan Anda dasar-dasar pengontrol, tampilan, dan peroutean.<br>
      1. Buka file rute yang terletak di app/Config/Routes.php<br>
```
<?php

use CodeIgniter\Router\RouteCollection;

/**
 * @var RouteCollection $routes
 */
$routes->get('/', 'Home::index');
```

contohnya <br>
![image](https://github.com/IsnaDewi/IsnaDewiMalikaArum/assets/134571793/37c0e002-040d-44d5-b98d-17a7d9312895) <br>

Tambahkan baris berikut, setelah arahan rute untuk '/'.<br>
```
use App\Controllers\Pages;

$routes->get('pages', [Pages::class, 'index']);
$routes->get('(:segment)', [Pages::class, 'view']);
```

contohnya <br>
![image](https://github.com/IsnaDewi/IsnaDewiMalikaArum/assets/134571793/f0e3b314-48b7-4f81-a01e-0848caeb9a18) <br>
      2. Buat file di app/Controllers/Pages.php dengan kode berikut. <br>
```
<?php

namespace App\Controllers;

class Pages extends BaseController
{
    public function index()
    {
        return view('welcome_message');
    }

    public function view($page = 'home')
    {
        // ...
    }
}
```

contohnya <br>
![image](https://github.com/IsnaDewi/IsnaDewiMalikaArum/assets/134571793/fbbaedeb-a8e0-40f6-a89f-3e26e7fdfea7)<br>
      3. Buat Tampilan
           a. Buat header di app/Views/templates/header.php dan tambahkan kode berikut: <br>
```
<!doctype html>
<html>
<head>
    <title>CodeIgniter Tutorial</title>
</head>
<body>

    <h1><?= esc($title) ?></h1>
```

contohnya <br>
![image](https://github.com/IsnaDewi/IsnaDewiMalikaArum/assets/134571793/7e200c64-8b4a-43d4-9153-b2eb0f3ed196) <br>
      b. buat footer di app/Views/templates/footer.php yang menyertakan kode berikut: <br>
```
 <em>&copy; 2022</em>
</body>
</html>
```
contohnya <br>
![image](https://github.com/IsnaDewi/IsnaDewiMalikaArum/assets/134571793/5a359536-87ec-4888-be05-4a9696281964) <br>
   4. Menambahkan Logika ke Controller
      a. Buat Home.php dan about.php
      ![image](https://github.com/IsnaDewi/IsnaDewiMalikaArum/assets/134571793/2e24da31-7ec2-4541-b0a3-973e16829476) <br>
![image](https://github.com/IsnaDewi/IsnaDewiMalikaArum/assets/134571793/b8c50c94-ef62-40b2-bea1-d022f8a9bafb) <br>
      b. Halaman Lengkap::view() Metode
```
<?php

namespace App\Controllers;

use CodeIgniter\Exceptions\PageNotFoundException; // Add this line

class Pages extends BaseController
{
    // ...

    public function view($page = 'home')
    {
        if (! is_file(APPPATH . 'Views/pages/' . $page . '.php')) {
            // Whoops, we don't have a page for that!
            throw new PageNotFoundException($page);
        }

        $data['title'] = ucfirst($page); // Capitalize the first letter

        return view('templates/header', $data)
            . view('pages/' . $page)
            . view('templates/footer');
    }
}
```

contohnya <br>
![image](https://github.com/IsnaDewi/IsnaDewiMalikaArum/assets/134571793/0ec1fa08-8a09-46d8-8b25-cb1767ada278) <br>
      5. Menjalankan Aplikasi <br>
      ketikan _php spark serve_ pada cmder <br>
```php spark serve``` <br>
lalu kunjungi **_localhost:8080/home_** <br>
seperti gambar dibawah ini <br>
![image](https://github.com/IsnaDewi/IsnaDewiMalikaArum/assets/134571793/3300938e-c450-4880-a519-09d138618336) <br>
**Bagian Berita** , tempat Anda akan mulai menggunakan model dan melakukan beberapa operasi basis data dasar.<br>
      1. Buat Database dan Tabel pada phpMyAdmin<br>
         membuat database **ci4tutorial** yang dapat digunakan untuk tutorial ini <br>
```
CREATE TABLE news (
    id INT UNSIGNED NOT NULL AUTO_INCREMENT,
    title VARCHAR(128) NOT NULL,
    slug VARCHAR(128) NOT NULL,
    body TEXT NOT NULL,
    PRIMARY KEY (id),
    UNIQUE slug (slug)
);
```
lalu isikan data di table news
```
INSERT INTO news VALUES
(1,'Elvis sighted','elvis-sighted','Elvis was sighted at the Podunk internet cafe. It looked like he was writing a CodeIgniter app.'),
(2,'Say it isn\'t so!','say-it-isnt-so','Scientists conclude that some programmers have a sense of humor.'),
(3,'Caffeination, Yes!','caffeination-yes','World\'s largest coffee shop open onsite nested coffee shop for staff only.');
```

      2. Hubungkan ke Basis Data <br>
         hapus tanda komentar pada file env <br>
         
![image](https://github.com/IsnaDewi/IsnaDewiMalikaArum/assets/134571793/20397655-7136-49f8-a225-ae098719b908) <br>
      3. Buat Model Berita<br>
            a. Buka direktori app/Models dan buat file baru bernama NewsModel.php dan tambahkan kode berikut.<br>
            
```
<?php

namespace App\Models;

use CodeIgniter\Model;

class NewsModel extends Model
{
    protected $table = 'news';
}
```

        
   b. Tambahkan Metode NewsModel::getNews() <br>
   
```
 public function getNews($slug = false)
    {
        if ($slug === false) {
            return $this->findAll();
        }

        return $this->where(['slug' => $slug])->first();
    }
```
contohnya <br>
![image](https://github.com/IsnaDewi/IsnaDewiMalikaArum/assets/134571793/509cf760-c208-40b6-ac08-454f1c248181) <br>
      4. Tampilkan Berita <br>
      - Menambahkan Aturan Perutean <br>
      
```
<?php

// ...

use App\Controllers\News; // Add this line
use App\Controllers\Pages;

$routes->get('news', [News::class, 'index']);           // Add this line
$routes->get('news/(:segment)', [News::class, 'show']); // Add this line

$routes->get('pages', [Pages::class, 'index']);
$routes->get('(:segment)', [Pages::class, 'view']);
```
- Buat Pengontrol Berita <br>
Buat pengontrol baru di app/Controllers/News.php . <br>
      
```
<?php

namespace App\Controllers;

use App\Models\NewsModel;

class News extends BaseController
{
    public function index()
    {
        $model = model(NewsModel::class);

        $data['news'] = $model->getNews();
    }

    public function show($slug = null)
    {
        $model = model(NewsModel::class);

        $data['news'] = $model->getNews($slug);
    }
}
```

- Berita Lengkap::index() Metode <br>
         
```
<?php

namespace App\Controllers;

use App\Models\NewsModel;

class News extends BaseController
{
    public function index()
    {
        $model = model(NewsModel::class);

        $data = [
            'news'  => $model->getNews(),
            'title' => 'News archive',
        ];

        return view('templates/header', $data)
            . view('news/index')
            . view('templates/footer');
    }

    // ...
}
```

- Buat File Tampilan berita/indeks <br>
a. Buat app/Views/news/index.php dan tambahkan potongan kode berikutnya. <br>

            
```
<h2><?= esc($title) ?></h2>

<?php if (! empty($news) && is_array($news)): ?>

    <?php foreach ($news as $news_item): ?>

        <h3><?= esc($news_item['title']) ?></h3>

        <div class="main">
            <?= esc($news_item['body']) ?>
        </div>
        <p><a href="/news/<?= esc($news_item['slug'], 'url') ?>">View article</a></p>

    <?php endforeach ?>

<?php else: ?>

    <h3>No News</h3>

    <p>Unable to find any news for you.</p>

<?php endif ?>
```


b. Berita Lengkap::show()Metode

      
```
<?php

namespace App\Controllers;

use App\Models\NewsModel;
use CodeIgniter\Exceptions\PageNotFoundException;

class News extends BaseController
{
    // ...

    public function show($slug = null)
    {
        $model = model(NewsModel::class);

        $data['news'] = $model->getNews($slug);

        if (empty($data['news'])) {
            throw new PageNotFoundException('Cannot find the news item: ' . $slug);
        }

        $data['title'] = $data['news']['title'];

        return view('templates/header', $data)
            . view('news/view')
            . view('templates/footer');
    }
}
```


-  Buat berita/lihat lihat file<br>
membuat tampilan terkait di app/Views/news/view.php . Letakkan kode berikut di file ini.<br>


```
<h2><?= esc($news['title']) ?></h2>
<p><?= esc($news['body']) ?></p>
```

lalu arahakn pada browser ketik **_localhost:8080/news_**
![image](https://github.com/IsnaDewi/IsnaDewiMalikaArum/assets/134571793/616b7ddb-8ce6-4aff-bc8c-152a9145c0e0) <br>

**Buat item berita** , yang akan memperkenalkan operasi database lebih lanjut dan validasi formulir.<br>
         1. Aktifkan Filter CSRF <br>
         Buka file app/Config/Filters.php dan perbarui $methodsproperti seperti berikut: <br>
```
<?php

namespace Config;

use CodeIgniter\Config\BaseConfig;

class Filters extends BaseConfig
{
    // ...

    public $methods = [
        'post' => ['csrf'],
    ];

    // ...
}
```

contohnya : <br>
![image](https://github.com/IsnaDewi/IsnaDewiMalikaArum/assets/134571793/9bdc28f7-89af-40b0-ae78-1cee0e2bcef4) <br>
      2. Menambahkan Aturan Perutean <br>
            menambahkan aturan tambahan ke file app/Config/Routes.php <br>
```
<?php

// ...

use App\Controllers\News;
use App\Controllers\Pages;

$routes->get('news', [News::class, 'index']);
$routes->get('news/new', [News::class, 'new']); // Add this line
$routes->post('news', [News::class, 'create']); // Add this line
$routes->get('news/(:segment)', [News::class, 'show']);

$routes->get('pages', [Pages::class, 'index']);
$routes->get('(:segment)', [Pages::class, 'view']);
```
contohnya <br>
![image](https://github.com/IsnaDewi/IsnaDewiMalikaArum/assets/134571793/8acd6810-0144-4afd-8330-e83cc3ffbbab) <br>
      3. Buat Formulir<br>
            a. Buat berita/buat lihat file<br>
            Buat tampilan baru di app/Views/news/create.php :<br>
```
<h2><?= esc($title) ?></h2>

<?= session()->getFlashdata('error') ?>
<?= validation_list_errors() ?>

<form action="/news" method="post">
    <?= csrf_field() ?>

    <label for="title">Title</label>
    <input type="input" name="title" value="<?= set_value('title') ?>">
    <br>

    <label for="body">Text</label>
    <textarea name="body" cols="45" rows="4"><?= set_value('body') ?></textarea>
    <br>

    <input type="submit" name="submit" value="Create news item">
</form>
```
contohnya <br>
![image](https://github.com/IsnaDewi/IsnaDewiMalikaArum/assets/134571793/6a8b5b77-359c-4e10-a018-ebedd28498c6) <br>
         b. Pengendali Berita<br>
               => Tambahkan Berita::baru() untuk Menampilkan Formulir<br>
            Pertama, buatlah metode untuk menampilkan form HTML yang telah Anda buat.<br>
```
<?php

namespace App\Controllers;

use App\Models\NewsModel;
use CodeIgniter\Exceptions\PageNotFoundException;

class News extends BaseController
{
    // ...

    public function new()
    {
        helper('form');

        return view('templates/header', ['title' => 'Create a news item'])
            . view('news/create')
            . view('templates/footer');
    }
}
```
<br>
      c. Tambahkan Berita::create() untuk Membuat Item Berita<br>
   Selanjutnya, buat metode untuk membuat item berita dari data yang dikirimkan.<br>
   Anda akan melakukan tiga hal di sini:<br>
   1. memeriksa apakah data yang dikirimkan lolos aturan validasi.<br>
   2. menyimpan item berita ke database.<br>
   3. mengembalikan halaman sukses.<br>
   
```
<?php

namespace App\Controllers;

use App\Models\NewsModel;
use CodeIgniter\Exceptions\PageNotFoundException;

class News extends BaseController
{
    // ...

    public function create()
    {
        helper('form');

        $data = $this->request->getPost(['title', 'body']);

        // Checks whether the submitted data passed the validation rules.
        if (! $this->validateData($data, [
            'title' => 'required|max_length[255]|min_length[3]',
            'body'  => 'required|max_length[5000]|min_length[10]',
        ])) {
            // The validation fails, so returns the form.
            return $this->new();
        }

        // Gets the validated data(Simpan Item Berita)
        $post = $this->validator->getValidated();

        $model = model(NewsModel::class);

        $model->save([
            'title' => $post['title'],
            'slug'  => url_title($post['title'], '-', true),
            'body'  => $post['body'],
        ]);

        return view('templates/header', ['title' => 'Create a news item'])
            . view('news/success')
            . view('templates/footer');
    }
}
```
contohnya <br>
![image](https://github.com/IsnaDewi/IsnaDewiMalikaArum/assets/134571793/065cc802-8155-47f5-8ea4-1899156a9e6c)<br>
         d. Kembalikan Halaman Sukses<br>
            Buat tampilan di app/Views/news/success.php dan tulis pesan sukses. Ini bisa sesederhana:<br>
```
<p>News item created successfully.</p>
```
contohnya <br>
![image](https://github.com/IsnaDewi/IsnaDewiMalikaArum/assets/134571793/22f628fc-9b94-4d6f-ae05-767473328f9a)<br>

      4. Pembaruan Model Berita<br>
            Edit NewsModel untuk memberikannya daftar bidang yang dapat diperbarui di $allowedFields properti.<br>
            
```
<?php

namespace App\Models;

use CodeIgniter\Model;

class NewsModel extends Model
{
    protected $table = 'news';

    protected $allowedFields = ['title', 'slug', 'body'];
}
```
contohnya <br>

![image](https://github.com/IsnaDewi/IsnaDewiMalikaArum/assets/134571793/78829693-65dd-4560-8a00-bd5ba855bae1) <br>

5. Buat Item Berita <br>
arahkan browser Anda ke lingkungan pengembangan lokal tempat Anda menginstal CodeIgniter dan tambahkan /news/new ke URL <br>
contohnya <br>

![image](https://github.com/IsnaDewi/IsnaDewiMalikaArum/assets/134571793/9d57d91f-5ee5-4864-98fb-ebe55c9d80a6)
<br>
      
**3. Codelgniter4 Overview** <br>
      1. **Struktur Aplikasi** <br>
         Untuk mendapatkan hasil maksimal dari CodeIgniter, Anda perlu memahami bagaimana struktur aplikasi, secara default, dan apa yang dapat Anda ubah untuk memenuhi kebutuhan aplikasi Anda. <br>
=> Direktori Default<br>
   ->aplikasi <br>
   ->sistem <br>
   ->publik <br>
   ->dapat ditulis <br>
   ->tes <br>
=>Memodifikasi Lokasi Direktori <br>
   Jika Anda telah memindahkan salah satu direktori utama, Anda dapat mengubah pengaturan konfigurasi di dalam app/Config/Paths.php . <br>
   2. **Model, Views, and Controllers** <br>
   3. **Autoloading Files** <br>
         a. Pemuat Otomatis Codelgniter4 <br>
         b. Konfigurasi <br>
         Konfigurasi awal dilakukan di app/Config/Autoload.php . File ini berisi dua array utama: satu untuk peta kelas, dan satu lagi untuk namespace yang kompatibel dengan PSR-4. <br>
            => Ruang Nama <br>
```
<?php

namespace Config;

use CodeIgniter\Config\AutoloadConfig;

class Autoload extends AutoloadConfig
{
    // ...
    public $psr4 = [
        APP_NAMESPACE => APPPATH, // For custom app namespace
        'Config'      => APPPATH . 'Config',
    ];

    // ...
}
```
contohnya <br>
            ![image](https://github.com/IsnaDewi/IsnaDewiMalikaArum/assets/134571793/926074f6-a567-4ae8-9647-496014f50472) <br>

   4.**Mengonfirmasi Namespace**<br>
      Anda dapat memeriksa konfigurasi namespace dengan perintah:spark namespaces<br>
```
php spark namespaces
```
5. **Ruang Nama Aplikasi**
      Anda dapat mengubah namespace ini dengan mengedit file app/Config/Constants.php dan menetapkan nilai namespace baru di bawah APP_NAMESPACEpengaturan:<br>
```
defined('APP_NAMESPACE') || define('APP_NAMESPACE', 'App');
```

6. **Peta Kelas**
      Classmap digunakan secara luas oleh CodeIgniter untuk meningkatkan kinerja sistem dengan tidak memukul sistem file dengan is_file()panggilan tambahan.<br>
```
<?php

namespace Config;

use CodeIgniter\Config\AutoloadConfig;

class Autoload extends AutoloadConfig
{
    // ...
    public $classmap = [
        'Markdown' => APPPATH . 'ThirdParty/markdown.php',
    ];

    // ...
}
```

7. **Dukungan Komposer**
      Dukungan komposer secara otomatis diinisialisasi secara default. Secara default, ia mencari file autoload Komposer di . Jika Anda perlu mengubah lokasi file tersebut karena alasan apa pun, Anda dapat mengubah nilai yang ditentukan di app/Config/Constants.php . <br>


   
      
      
