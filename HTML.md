HTML and CSS
==
----

**HTML** (HyperText Markup Language) adalah bahasa markup untuk membuat halaman web.

## HTML Example
----
```html
<!DOCTYPE html>
<html>
    <head>
        <title>Page Title</title>
    </head>
    <body>
        <h1>My First Heading</h1>
        <p>My first paragraph.</p>
    </body>
</html>
```
* ```<!DOCTYPE html>``` mendeklarasikan dokumen ini sebagai HTML5 
* Elemen ```<html>``` adalah root-element dari dokumen HTML 
* Elemen ```<head>``` berisi meta information dari dokumen
* Elemen ```<title>``` mendeklarasikan judul dari web page
* Elemen ```<body>``` berisi elemen-elemen konten web page
* Elemen ```<h1>``` adalah elemen konten yang mendeklarasikan heading terbesar
* Elemen ```<p>``` mendeklarasikan paragraf

## HTML Tag
----
Tag adalah penanda awalan dan akhiran sebuah elemen di html. Tag dibuat dengan kurung siku (<...>). Tag selalu ditulis berpasangan. Contoh :
```html
<h1>AM/FM</h1>
<p>ITF Fuki</p>
```
|Tag                 | Fungsi                               |
|------------------- | -----------------------------------  |
|```<html>```        | untuk memulai dokumen html           |
|```<head>```        | untuk membuat bagian head            |
|```<body>```        | untuk membuat bagian body            |
|```<h1> - <h6>```   | untuk membuat heading pada artikel   |
|```<p>```           | untuk membuat paragraf               |


## HTML Element
----
Element dalam html adalah sebuah komponen penyusun dokumen html. Elemen dibentuk dari tag pembuka, isi tag, dan tag penutup. Contoh :
```html
<p>Hello World</p>
```
## HTML Attributes
----
Atribut html memberikan informasi tambahan tentang elemen html. Atribut biasa ditulis dengan nama dan value : ```name="value"```. Contoh :
```html
<p align="center">Hello World!</p>
```
* Nama atribut ```align``` 
* Nilai/value atribut ```center```

## Headings
Browser menggunakan heading untuk menyusun konten.
```html
<h1>Heading 1</h1>
<h2>Heading 2</h2>
<h3>Heading 3</h3>
<h4>Heading 4</h4>
<h5>Heading 5</h5>
<h6>Heading 6</h6>
```
## Paragraphs 
Elemen ```<p>``` mendeklarasikan paragraf.
```html
<p>
Halo! Namaku Mahdia. Aku suka sekali membuat web. Aku juga suka mendesain! 
</p>

<p>
Sekarang aku sedang mempelajari bagaimana membuat paragraf dalam HTML. Hmm, ternyata mudah sekali bukan?
</p>
```
## Images
Elemen ```<img>``` dibaca sebagai gambar oleh browser.
```html
<img src="img_girl.jpg" alt="Girl with a jacket" width="500" height="600">
```
Penjelasan :
* Atribut dari elemen ```<img>``` adalah ‘src’, ‘alt’, ‘width’ dan ‘height’ dengan nilai-nilainya.
* Atribut ‘src’ dan ‘alt’ wajib diisi.
* Kamu juga bisa menambahkan URL dari internet pada src!
## Table
```html
<table style="width:100%">
  <tr>
    <th>Firstname</th>
    <th>Lastname</th>
  </tr>
  <tr>
    <td>Jill</td>
    <td>Smith</td>
  </tr>
  <tr>
    <td>Eve</td>
    <td>Jackson</td>
  </tr>
  <tr>
    <td>John</td>
    <td>Doe</td>
  </tr>
</table>
```
* Tabel HTML didefinisikan dengan tags ```<table>```. 
* Baris pada tabel didefinisikan dengan elemen tags ```<tr>```.
* Kolom pada kepala tabel menggunakan tags ```<th>```, tags ```<td>``` untuk kolom pada badan tabel.
## Lists
List berurutan (ordered-list) dimulai dengan tags ```<ol>``` dan setiap item dideklarasikan dengan ```<li>```. Sedangkan, tags ```<ul>``` untuk list yang tidak berurutan (unordered-list).
```html
<h2>An Unordered HTML List</h2>
<ul>
  <li>Coffee</li>
  <li>Tea</li>
  <li>Milk</li>
</ul>  
<h2>An Ordered HTML List</h2>
<ol>
  <li>Coffee</li>
  <li>Tea</li>
  <li>Milk</li>
</ol> 
```
## Links
Tautan (links) digunakan untuk mengakses satu halaman ke halaman yang lain. Tags ```<a>``` mendefinisikan tautan (hyperlink).
```html
<h2>HTML Links</h2>
<a href="https://www.w3schools.com/html/">Visit our HTML tutorial</a>
```
## Forms
Form di HTML dapat dibuat dengan tag ```<tag>```
Tag ini memiliki beberapa atribut yang harus diberikan, seperti:
* Action untuk menentukan akasi yang akan dilakukan saat data dikirim;
* Method metode pengiriman data.
Contoh :
```html
<form action="prosess.php" method="GET">
<input type="text" name="info" />
</form>
```
Didalam form, diisi dengan field, yaitu ruas yang dapat diisi data. Pada contoh diatas adalah ```input```. Field memiliki beberapa atribut yang harus diberikan:
* ```type``` merupakan type dari field.
* ```name``` merupakan nama dari field yang akan menjadi kunci dan variabel di dalam program. 

Contoh form login :
```html
<!DOCTYPE html>
<html>
<head>
    <title>Form Login</title>
</head>
<body>
    <form action="login.php" method="POST">
        <fieldset>
        <legend>Login</legend>
        <p>
            <label>Username:</label>
            <input type="text" name="username" placeholder="username..." />
        </p>
        <p>
            <label>Password:</label>
            <input type="password" name="password" placeholder="password..." />
        </p>
        <p>
            <label><input type="checkbox" name="remember" value="remember" /> Remember me</label>
        </p>
        <p>
            <input type="submit" name="submit" value="Login" />
        </p>
        </fieldset>
    </form>
</body>
</html>
```
## Block-level Elements
Elemen ```<div>``` adalah Block-level element. Fungsinya adalah untuk mengelompokkan elemen atau tag-tag agar menjadi suatu grup. Biasanya tag ```div``` sering digunakan untuk mendefinisikan ```id``` atau ```class``` dari CSS. Contoh :
```html
<div style="background-color:black;color:white;padding:20px;">
  <h2>London</h2>
  <p>London is the capital city of England. It is the most populous city in the United Kingdom, with a metropolitan area of over 13 million inhabitants.</p>
</div>
```

# CSS
## Analogi HTML/CSS

### HTML
![](https://gitlab.com/it-force/amfm/-/raw/master/gambar/img1.jpg) 

### HTML + CSS
![](https://gitlab.com/it-force/amfm/-/raw/master/gambar/img2.png)

### Contoh HTML
![](https://gitlab.com/it-force/amfm/-/raw/master/gambar/img3.png) 

### Contoh HTML + CSS
![](https://gitlab.com/it-force/amfm/-/raw/master/gambar/img4.png)

## Apakah itu CSS?
CSS (Cascading Style Sheets) adalah kode/bahasa yang mendeskripsikan bagaimana elemen HTML ditampilkan pada layar. CSS mendeskripsikan pengaturan style, layout dan variasi tampilan di berbagai perangkat dan ukuran layar.

![](https://gitlab.com/it-force/amfm/-/raw/master/gambar/img5.png) 

## Bagaimana Cara Mengaplikasikan CSS?
![](https://gitlab.com/it-force/amfm/-/raw/master/gambar/img6.PNG) 

## Di mana kita menuliskan CSS?
#### Inline
- Inline CSS ini diletakan langsung pada elemen HTML sebagai atribut, sehingga tidak membutuhkan selektor lagi
- Hanya dapat digunakan untuk elemen HTML yang telah didefinisikan
- Direkomendasikan jika ingin menimpa aturan style global yang telah ditetapkan

```
<p style="color: blue">Hi Rookies!</p>
```
#### Internal
- Internal CSS didefinisikan pada <head> dokumen HTML menggunakan elemen <style>

```
<head>
    <style>
    p{
        color: blue;
    }
   </style>
</head>
<body>
    <p>Hi Rookies!</p>
</body>
```

Bagaimana jika CSS nya banyak? Tentu tidak terlihat bagus karena menumpuk pada satu file HTML! 
Di mana kita menuliskan CSS?

#### External
index.html
```
<head>
    <link rel="stylesheet"type="text/css" href="style.css">
</head>
<body>
    <p>Hi, Rookies!</p>
</body>
```
style.css
```
p {
    color: blue;
}
```
## CSS Selector
CSS Selectors digunakan untuk memilih elemen HTML yang akan diberikan style berdasarkan element tags, id, kelas, attribute dan lain sebagainya.

Contoh
```
<a href= “https://www.w3schools.com”  id=“css-source” class=“link-default”>Klik disini</a>
```

![](https://gitlab.com/it-force/amfm/-/raw/master/gambar/img12.PNG) 

## Analogi
__Sedan__

![](https://gitlab.com/it-force/amfm/-/raw/master/gambar/img7.png) 

Untuk selector sedan:
```
sedan {
    ...
}
```
Ini adalah contoh dari selector element!

##


__Pink__

![](https://gitlab.com/it-force/amfm/-/raw/master/gambar/img8.png) 

Untuk selector mobil berwarna pink?
```
.pink {
    ...
}
```
Ini adalah contoh dari selector class! 

##

__Nomor plat mobil__

![](https://gitlab.com/it-force/amfm/-/raw/master/gambar/img9.png) 

Untuk selector ID dengan nomor plat mobil sebagai berikut:
```
#123xyz {
    ...
}
```
Ini adalah contoh dari selector ID! 

#### Element Selector
Element selectors akan memilih semua elemen yang memiliki tags yang sama pada dokumen.
```
a {
  font-size: 18px;
text-align: justify; 
}
```

#### Class Selector
Class selectors akan memilih elemen yang memiliki atribut kelas yang spesifik. Kelas ini dapat dimiliki oleh beberapa elemen dan sebuah elemen pun dapat memiliki beberapa kelas.
```
.link-default {
    font-color: red; 
  line-height: 1.5em;
} 
```

#### Id Selectors

Id selector  digunakan untuk memilih elemen yang memiliki sebuah id yang unik, artinya id ini hanya dapat dimiliki oleh satu elemen saja.
```
#css-source {
  font-family: cursive;
  text-decoration: none;
} 
```

## Beberapa atribut CSS yang biasa digunakan
##### Font
- Color: #RRGGBB, red, blue, green
- Font-size: %, px, pt, em 
- Font-family:  Arial, calibri
- Font-style: Normal, italic
- Font-weight: Normal, bold

##### Background
- Background-color: #RRGGBB, red, blue, green
- Background-image: url(“image url”)

##### Sizing-Element
- Height : %, px, vh
- Width : %, px, vw

##### Border
- Border-color : red, #RRGGBB
- Border-style : solid, dotted

## Box Model
Setiap elemen pada CSS adalah sebuah kotak.

![](https://gitlab.com/it-force/amfm/-/raw/master/gambar/img10.png) 

__Total Element Width__ = content width + left padding + right padding + left border + right border + left margin + right margin

__Total Element Height__ = content height + top padding + bottom padding + top border + bottom border + top margin + bottom margin

- Height: tinggi dari konten
- Width: lebar dari konten
- Padding: jarak antara konten dengan border
- Border: batas luar dari sebuah elemen
- Margin: jarak antara elemen satu dengan lainnya
- Box-sizing: border-box

## CSS Animation
CSS Animation digunakan untuk mempermudah membuat animasi pada elemen HTML tanpa bantuan dari kode Javascript atau Flash. Aturan dasar dari CSS Animation, adalah :
1. Aturan animasi yang dibuat harus didefinisikan pada @keyframe
2. Animasi ini harus diimplementasikan pada elemen HTML
3. Durasi dari animasi harus ditentukan

![](https://gitlab.com/it-force/amfm/-/raw/master/gambar/img11.PNG)

## Referensi
* https://www.slideshare.net/ahmedhaque35/intro-to-twitter-bootstrap
* https://www.slideshare.net/emkidwell/gdi-intro-to-html-css-class-2-final
* https://www.w3schools.com/
* https://www.petanikode.com/