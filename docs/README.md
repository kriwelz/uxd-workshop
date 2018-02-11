![Logo](_media/uxd.jpg)

# Pengenalan

Halo, selamat bergabung di **UXD | PHP Indonesia** sebuah komunitas di bawah naungan PHP Indonesia yang berfokus pada tema UI / UX & Frontend Developer. Hari ini Minggu (12 / 01) 2018 adalah pertama kalinya komunitas **UXD | PHP Indonesia** mengadakan workshop. 

Sebelumnya perkenalkan nama saya **Muhibbudin Suretno** founder dan admin group **UXD | PHP Indonesia**, saat ini saya bekerja sebagai Sr. Frontend Developer di sebuah marketplace perhiasan online di Jakarta.

Dan pada workshop pertama ini saya akan membawakan materi mengenai **Design To HTML**, dengan fokus pada pembuatan struktur template dan responsive web design.

##### Tentang Tema

Di desain kali ini saya membawa sebuah ide mengenai Studio Foto bernama **The Photograph** yang pada dasarnya adalah hasil research saya pada seorang teman yang memiliki usaha di bidang Photo Studio dan saya cukup banyak mendapatkan insight darinya terutama fitur apa saja yang biasa–nya orang butuhkan pada sebuah studio foto.

#### Daftar Isi

- [Pengenalan](?id=pengenalan)
- [Daftar Isi](?id=daftar-isi)
- [Inisialisasi proyek](?id=inisialisasi-proyek)
- [Memahami struktur proyek](?id=memahami-struktur-proyek)
- [Berkenalan dengan SASS / SCSS](?id=berkenalan-dengan-sass-scss)
- [Membuat Navbar](?id=membuat-navbar)
- [Membuat Section Hero](?id=membuat-section-hero)
- [Membuat Section Introduction](?id=membuat-section-introduction)
- [Membuat Section Services](?id=membuat-section-services)
- [Membuat Section Promotion](?id=membuat-section-promotion)
- [Membuat Section Prices](?id=membuat-section-prices)
- [Membuat Section Client Says](?id=membuat-section-client-says)
- [Membuat Section Footer](?id=membuat-section-footer)
- [Membuat Copyright](?id=membuat-copyright)
- [Kesimpulan](?id=kesimpulan)
- [Penutup](?id=penutup)

#### Inisialisasi proyek

Sebelum memulai anda di wajibkan menyiapkan environment dan software yang akan kita butuhkan, diantaranya seperti di bawah ini :

- [Git](https://git-scm.com/downloads)
- [Ruby SASS](https://sass-lang.com/install)

> Jika anda belum pernah memakai Ruby sebelumnya, silahkan download & install terlebih dahulu melalui [tautan berikut.](https://www.ruby-lang.org/id/documentation/installation/)

Selanjutnya anda dapat men–download source skeleton yang akan kita gunakan pada proyek ini dengan cara seperti berikut :

- Menggunakan GIT via SSH :
  `$ git clone git@github.com:muhibbudins/uxd-workshop.git`
- Menggunakan GIT via HTTPS :
  `$ git clone https://github.com/muhibbudins/uxd-workshop.git`
- Men-*download* langsung dari *source* :
  [klik disini](https://github.com/muhibbudins/uxd-workshop/archive/master.zip)

Setelah semuanya selesai, silahkan buka skeleton yang sudah di download serta buka **Command prompt / Terminal** pada folder tersebut. Lalu jalankan _Ruby SASS_ dengan command berikut :

``` bash
$ sass --watch scss/main.scss:css/main.css
```

#### Memahami struktur proyek

Berikut adalah struktur folder yang akan kita gunakan pada proyek ini :

![Structure](_media/directory.png)

Pada gambar di atas kita dapat melihat beberapa folder di antaranya **css, img, js, scss** serta beberapa file seperti **.gitignore, LICENSE, README.md** dan **index.html** dengan keterangan sebagai berikut :

- **css** : Folder dimana hasil compile file .scss di simpan _(destination directory)_
- **img** : Folder untuk menyimpan asset file hasil slicing dari desain
- **js** : Folder untuk menyimpan semua script JavaScript yang digunakan pada aplikasi
- **scss** : Folder utama untuk file SASS dengan format .scss
- **index.html** : File utama yang akan di panggil oleh browser

> Hanya file _main.scss_ pada folder **scss** yang akan di compile dan pada folder ini berisi sub folder **components** & **core** yang menjadi tempat kita menyimpan file .scss yang nantinya di panggil pada file main.scss

#### Berkenalan dengan SASS / SCSS

SASS adalah sebuah CSS Preprocessor yang cukup populer saat ini karena kemudahan dalam pengaplikasiannya pada proyek besar maupun kecil, SASS memiliki dua format file yang cukup berbeda secara syntax yaitu **.sass** & **.scss** perbedaan yang cukup mencolok itu adalah syntax **.sass** tidak mendukung penggunaan { bracket } dan ; (semi-colon) seperti bahasa ibunya yaitu Ruby. Namun berbeda dengan syntax **.scss** yang secara struktur 100% sama dengan file CSS pada umumnya, tapi dengan beberapa keunggulan lain yang tidak ada pada bahasa CSS biasa.

Berikut adalah contoh penggunaan SASS dengan syntax (format) **.scss** :

![SCSS](_media/scss.png)

Sangat mirip dengan CSS bukan? bedanya hanya pada bentuk _nesting_. Jika pada syntax CSS kita biasa melakukan _nesting_ seperti ini :

``` scss
.foo {
  color: blue;
}
.foo.bar {
  background-color: red;
}
.foo.bar > p {
  font-size: 16px;
}
```

Maka pada SCSS kita dapat mempersingkatnya menjadi seperti ini :

``` scss
.foo {
  color: blue;

  &.bar {
    background-color: red;

    &> p {
      font-size: 16px;
    }
  }
}
```

Dengan menggunakan SASS / SCSS kita dapat mempersingkat menulis ulang class **.foo** serta child—nya, selain itu masih ada lagi kelebihan lain saat kita menggunakan SASS / SCSS sebagai CSS Pre-processor contohnya :

- [Conditional](http://sass-lang.com/documentation/file.SASS_REFERENCE.html#if)
- [Loop](http://sass-lang.com/documentation/file.SASS_REFERENCE.html#for)
- [Array](http://sass-lang.com/documentation/file.SASS_REFERENCE.html#each-directive)
- [Mixin (Function)](http://sass-lang.com/documentation/file.SASS_REFERENCE.html#mixins)

> Selengkapnya bisa anda pelajari pada [link berikut.](http://sass-lang.com/guide)

Dan pada proyek ini saya telah menambahkan beberapa _helper_ yang akan membantu kita dan yang telah saya simpan pada folder **scss/core**, yaitu diantaranya :

- Animation delay
- Color variable
- Fonts variable
- Responsive utility
- Text utility

#### Membuat Navbar

Selanjutnya yang akan kita buat pertama adalah bagian **navbar**, tapi sebelumnya kita akan coba rubah bagian _body_ pada **main.scss** menjadi seperti berikut :

```scss
...
// global style
body {
  font-family: $quicksand;
  font-size: 16px;
  background-color: $dark;
}
```

Lalu kita coba buat bagian navbar seperti pada gambar di bawah ini.

![Navbar](_media/Navbar.jpg)

Yang kita lakukan pertama kali adalah membuat menunya dahulu, silahkan buka file **index.html** dan replace bagian code berikut :

```html
  <!-- Start your code -->

  <div class="col-6 text-center">
    <h1>Hi, Welcome!</h1>
    <p class="text-secondary">Now write your imagination and think this browser is a canvas.</p>
  </div>

  <!-- End your code -->
```

Menjadi seperti ini :

```html
  <!-- Navbar -->
  <nav class="navbar navbar-expand-lg">  
    <div class="container">
      <a class="navbar-brand" href="#">Brand</a>
      <ul class="navbar-nav ml-auto">
        <li class="nav-item">
          <a class="nav-link" href="#">Home</a>
        </li>
        <li class="nav-item dropdown">
          <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
            Categories
          </a>
          <div class="dropdown-menu" aria-labelledby="navbarDropdown">
            <a class="dropdown-item" href="#">Action</a>
            <a class="dropdown-item" href="#">Another action</a>
          </div>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="#">Gallery</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="#">Team</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="#">About Us</a>
        </li>
      </ul>
    </div>
  </nav>
```

Selanjutnya silahkan buka file index.html pada browser maka hasilnya adalah seperti berikut :

![Navbar before](_media/navbar-before.png)

Sekarang kita coba styling bagian navbar ini agar sama dengan desain yang telah di buat, silahkan tambahkan code berikut pada file **components/_navbar.scss**.

```scss
// Hoverable Mixin
@mixin hoverable() {
  &:hover,
  &:focus,
  &:active {
    color: transparentize($white, 0);
  }
}

// Main navbar
.navbar {
  background-color: $indigo;

  &-brand {
    font-size: 28;
    font-family: $lobster;
    color: transparentize($white, 0.2);

    @include hoverable();
  }
  
  // Navbar item
  .nav {
    &-item {
      padding: 8px 10px;
    }
    &-link {
      font-size: 14px;
      color: transparentize($white, 0.2);
  
      @include hoverable();
    }
  }
}

// Dropdown Arrow
.dropdown-toggle {
  &:after {
    border: 0;
    content: "\f3d0";
    display: inline-block;
    font-family: "Ionicons";
    speak: none;
    font-style: normal;
    font-weight: normal;
    font-variant: normal;
    text-transform: none;
    text-rendering: auto;
    line-height: 1;
    -webkit-font-smoothing: antialiased;
    vertical-align: 0;
  }
}
```

> Pada code di atas pada line awal saya membuat sebuah **mixin** bernama **hoverable** yang berguna untuk membuat pseudo class yang akan di panggil pada beberapa class yaitu _.navbar_brand_ dan _.nav-link_.

Dan hasilnya adalah seperti berikut :

![Navbar before](_media/navbar-after.png)

<!-- Divider -->
<p align="center">:wavy_dash::wavy_dash::wavy_dash::wavy_dash:</p>
<!-- Divider -->


#### Membuat Section Hero

Selanjutnya kita akan membuat bagian hero seperti desain berikut :

![Hero](_media/Hero.jpg)

Silahkan tambahkan code berikut, setelah bagian <~~ Navbar ~~>.

```html
  <!-- Hero -->
  <section class="section section-overlay">
    <div class="section-overlay-inner">
      <img src="img/logo.svg" alt="The Photograph">
      <p>Consequatur eius ullam fugiat illo laborum similique repellat quisquam ut. Aut debitis quam quas <br> voluptatibus, temporibus omnis repudiandae fugiat  reprehenderit nobis eum.</p>
      <div class="section-overlay-button">
        <a href="#" class="btn btn-info">View Gallery</a>
        <a href="#" class="btn btn-outline-white">Call</a>
      </div>
    </div>
  </section>
```

Pada code HTML di atas kita coba membuat sebuah section hero yang berisi ucapan selamat datang, yang jika kalian buka pada browser hasilnya seperti berikut :

![Hero Before](_media/hero-before.png)

Sepertinya masih belum bagus, selanjutnya kita coba tambahkan beberapa style untuk bagian hero ini. Kita buka file **components/_section.scss** dan pertama kita tambahkan adalah style utama untuk bagian section.

Code–nya seperti di bawah ini :

```scss
.section {
  width: 100%;
  min-height: 400px;
  padding: 60px 0;
  color: $white;
}
```

Lalu kita tambahkan sub-class _.section-overlay_ untuk mempercantik bagian hero tersebut, silahkan tambahkan code di bawah ini kedalam class _.section_ :

```scss
.section {

  ...
  &-overlay {
    width: 100%;
    height: calc(100vh - 70px);
    display: flex;
    align-items: center;
    justify-content: center;
    background-image: url(../img/bg-hero.jpeg);
    background-size: cover;
    background-repeat: no-repeat;
    position: relative;
  
    &:before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      bottom: 0;
      right: 0;
      background-color: transparentize($dark, 0.4);
      z-index: 0;
    }
    &-inner {
      z-index: 100;
      text-align: center;
      color: $white;
  
      img {
        width: 390px;
        height: auto
      }
      p {
        margin: 20px 0;
      }
    }
    &-button {
      margin-top: 40px;
  
      .btn {
        margin: 0 5px;
      }
    }
  }
}
```

Selanjutnya untuk bagian button kita tambahkan code berikut pada file **components/_button.scss** :

```scss
// Hoverable Mixin
@mixin hoverable() {
  &:hover,
  &:focus,
  &:active {
    color: $white;
    border: 1px solid $blue;
    background-color: darken($blue, 4%);
  }
}

.btn {
  padding: 10px 32px;
  border-radius: 30px;
  border: 1px solid $blue;

  &-info {
    background-color: $blue;

    @include hoverable();
  }
  &-outline {
    &-info {
      background-color: transparent;
      color: $blue;
  
      @include hoverable();
    }
    &-white {
      background-color: transparent;
      border-color: $white;
      color: $white;
  
      @include hoverable();
    }
  }
}
```

Dan hasilnya adalah seperti bisa kita lihat di bawah ini :

![Hero After](_media/hero-after.png)

Terlihat lebih rapi bukan? Bagian navbar dan hero sudah, selanjutnya kita coba masuk ke bagian **Introduction.** :smile:

<!-- Divider -->
<p align="center">:wavy_dash::wavy_dash::wavy_dash::wavy_dash:</p>
<!-- Divider -->

#### Membuat Section Introduction

Pada bagian ini kita coba membuat intro dari **The Photograph** kira-kira isinya itu hanya title, description serta link menuju sosmed seperti pada gambar di bawah.

![Introduction](_media/Introduction.jpg)

Pertama, silahkan tambahkan code berikut setelah bagian <~~ Hero ~~> 

```html
  <!-- Introduction -->
  <section class="section section-indigo">
    <div class="container">
      <div class="row">
        <div class="col-9 mx-auto text-center">
          <div class="text-xlarge mb-4">The Photograph</div>
          <p class="text">Accusamus quisquam fugit tempora distinctio sint reprehenderit optio quos similique vitae consectetur? Molestiae est aspernatur eos totam consectetur quia sit neque delectus. Iusto iure facere provident doloribus unde excepturi ipsum beatae et distinctio commodi culpa harum ea dolore quibusdam, voluptatibus autem necessitatibus eaque deleniti. Dolores maiores atque necessitatibus sequi laboriosam odit blanditiis, qui recusandae molestiae unde. </p>
          <p class="text">Dolore est minus atque reiciendis ratione quis natus veritatis, nisi. Distinctio asperiores itaque ex. Quam sunt consequatur aut dolorem expedita aliquam, saepe minima vitae in enim, illum harum suscipit voluptatum nostrum quo? Autem consectetur, minima reprehenderit hic, corporis tempore cumque a doloribus! Accusamus, illum sapiente tenetur impedit deleniti! Recusandae qui animi reprehenderit ipsum quo? Dolor suscipit autem dolorem obcaecati inventore perspiciatis atque omnis, id sit. Maiores harum accusamus dolor, sint repudiandae eveniet nam, dolore iusto maxime.</p>
          <nav class="nav justify-content-center">
            <a class="nav-link nav-social text-icon" href="#">
              <i class="ion-social-facebook"></i>
            </a>
            <a class="nav-link nav-social text-icon" href="#">
              <i class="ion-social-instagram"></i>
            </a>
            <a class="nav-link nav-social text-icon" href="#">
              <i class="ion-social-pinterest"></i>
            </a>
            <a class="nav-link nav-social text-icon" href="#">
              <i class="ion-social-twitter"></i>
            </a>
          </nav>
        </div>
      </div>
    </div>
  </section>
```

Selanjutnya kita rubah warna background section tersebut, dengan menambahkan beberapa baris code pada file **components/_section.scss**. Dan tambahkan sebelum code `&-overlay`.

```scss
// _section.scss
  ...
  &-indigo {
    background-color: $indigo;
  }
  ...
```

Maka hasilnya adalah seperti berikut ini :

![Introduction](_media/introduction.png)


<!-- Divider -->
<p align="center">:wavy_dash::wavy_dash::wavy_dash::wavy_dash:</p>
<!-- Divider -->


#### Membuat Section Services

![Services](_media/Services.jpg)

Di bagian ini akan cukup sulit karena kita akan menambahkan lumayan banyak code pada beberapa file terpisah, yang pertama kita coba tambahkan markup HTML untuk bagian ini setelah bagian introduction.

Silahkan tambahkan code pada file **index.html** seperti berikut ini :

```html
  <!-- Services -->
  <section class="section section-service">
    <div class="container-fluid">
      <div class="row">
        <div class="col-9 mx-auto text-center">
          <div class="text-xlarge mb-4">Our Services</div>
        </div>
      </div>
    </div>
    <div class="grid">
      <div class="grid-item">
        <img src="img/service-1.jpeg" alt="Service 1">
        <div class="grid-overlay">
          <div class="grid-title">Wedding Photo</div>
          <div class="grid-description">Consequatur eius ullam fugiat illo laborumsimilique repellat quisquam ut. Aut debitis quam quas  voluptatibus.</div>
          <a href="#" class="btn btn-outline-info">Read More</a>
        </div>
      </div>
      <div class="grid-item">
        <img src="img/service-2.jpeg" alt="Service 2">
        <div class="grid-overlay">
          <div class="grid-title">Family Photo</div>
          <div class="grid-description">Consequatur eius ullam fugiat illo laborumsimilique repellat quisquam ut. Aut debitis quam quas  voluptatibus.</div>
          <a href="#" class="btn btn-outline-info">Read More</a>
        </div>
      </div>
      <div class="grid-item">
        <img src="img/service-3.jpeg" alt="Service 3">
        <div class="grid-overlay">
          <div class="grid-title">Graduation</div>
          <div class="grid-description">Consequatur eius ullam fugiat illo laborumsimilique repellat quisquam ut. Aut debitis quam quas  voluptatibus.</div>
          <a href="#" class="btn btn-outline-info">Read More</a>
        </div>
      </div>
      <div class="grid-item">
        <img src="img/service-4.jpeg" alt="Service 4">
        <div class="grid-overlay">
          <div class="grid-title">Couple Photo</div>
          <div class="grid-description">Consequatur eius ullam fugiat illo laborumsimilique repellat quisquam ut. Aut debitis quam quas  voluptatibus.</div>
          <a href="#" class="btn btn-outline-info">Read More</a>
        </div>
      </div>
      <div class="grid-item">
        <img src="img/service-5.jpeg" alt="Service 5">
        <div class="grid-overlay">
          <div class="grid-title">Milenial Photo</div>
          <div class="grid-description">Consequatur eius ullam fugiat illo laborumsimilique repellat quisquam ut. Aut debitis quam quas  voluptatibus.</div>
          <a href="#" class="btn btn-outline-info">Read More</a>
        </div>
      </div>
      <div class="grid-item">
        <img src="img/service-6.jpeg" alt="Service 6">
        <div class="grid-overlay">
          <div class="grid-title">Exclusive Photo</div>
          <div class="grid-description">Consequatur eius ullam fugiat illo laborumsimilique repellat quisquam ut. Aut debitis quam quas  voluptatibus.</div>
          <a href="#" class="btn btn-outline-info">Read More</a>
        </div>
      </div>
    </div>
  </section>
```

Untuk styling-nya pertama kita ubah bagian background service, dengan menambahkan code berikut setelah **&-indigo** pada file **components/_section.scss**.

```scss
  &-service {
    background-color: $black;
    padding-bottom: 0;
  }
```

Lalu pada tambahkan code berikut pada file **components/_grid.scss** yang berguna untuk membuat grid card.

```scss
.grid {
  width: 100%;
  display: flex;
  flex-wrap: wrap;

  &-item {
    width: calc(100% / 3);
    height: 300px;
    position: relative;
    overflow: hidden;

    img {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translateX(-50%) translateY(-50%);
      width: 100%;
      height: auto;
      transition: all 0.8s ease;
    }
    &:hover > .grid-overlay {
      opacity: 1;
    }
    &:hover > img {
      filter: grayscale(100);
      transform: scale(1.2) translateX(-40%) translateY(-40%);
    }
  }
  &-overlay {
    position: absolute;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
    background-color: transparentize($black, 0.4);
    z-index: 10;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    text-align: center;
    padding: 0 60px;
    opacity: 0;
    transition: opacity 0.3s ease;
  }
  &-title {
    font-size: 28px;
  }
  &-description {
    font-size: 14px;
    margin: 20px 0;
  }
}
```

> Pada beberapa class di atas saya menambahkan property transition yang berguna untuk membuat animasi pada setiap item card

Dan hasilnya adalah seperti berikut ini.

![Service](_media/service.png)

<!-- Divider -->
<p align="center">:wavy_dash::wavy_dash::wavy_dash::wavy_dash:</p>
<!-- Divider -->


#### Membuat Section Promotion

![Promotion](_media/Promotion.jpg)

#### Membuat Section Prices

![Prices](_media/Prices.jpg)

#### Membuat Section Client Says

![ClientSays](_media/ClientSays.jpg)

#### Membuat Section Footer

![Footer](_media/Footer.jpg)

#### Membuat Copyright

![Copyright](_media/Copyright.jpg)

#### Kesimpulan

![Full Page](_media/Desktop.jpg)

#### Penutup
