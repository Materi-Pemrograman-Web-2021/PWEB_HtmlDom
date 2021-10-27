# PWEB_HtmlDom
Materi HTML DOM untuk Mata Kuliah PWEB

## 1. Adding Elements

### Append
Menambahkan element ke body.

```js
const body = document.body
body.append("Hello World")
body.append("Hello World", "Bye") // bisa multiple
```

### AppendChild
`Append` berbeda dengan `AppendChild`. Di `Append`, bisa memasukkan sebuah String. Sedangkan `AppendChild`, hanya bisa memasukkan sebuah Node. Dimana maksudnya adalah seperti sebuah elemen `div`, `span`, atau yang lain

```js
const body = document.body
body.appendChild("hehe") 
// error, karena harus berupa element
// hanya bisa nambah 1 item
// Lha terus gimana, kita simak selanjutnya
```

Method ini jarang digunakan. Karena kita biasanya menambahkan element ke halaman web kita, bukan sekedar String saja

## 2. Creating Elements

```js
const body = document.body
const div = document.createElement("div")
```
Nah, kita sudah bisa membuat element. Tapi ketika kita save, kok tidak muncul ? Karena kita sudah membuat elementnya. Tapi belom ditambahkan ke halamannya

Maka, tinggal tambahkan
```js
const body = document.body
const div = document.createElement("div")
body.append(div)
```
Terlihat kosong, karena `div` kita emang belom ada isinya

## 3. Modifying Element Text
Ada dua cara, bisa pakai `innerText` atau `textContent`. Bedanya apa ?

```js
const body = document.body
const div = document.createElement("div")
div.innerText = "Hello World"
div.textContent = "Hello World 2"

body.append(div)
```
Jika kita masukkan seperti diatas, memang terlihat sama. Namun, semisal pada file index.html kita coba tambahkan `span` didalam `div`, 

```html
<div>
    <span>Hello</span>
    <span style="display: none;">World</span>
</div>
```

Lalu, pada file `script.js` kita coba select div nya

```js
const div = document.querySelector('div')
console.log(div.textContent)
console.log(div.innerText)
```

Jadi, bedanya adalah:
1. textContent
Mengembalikan nilai seutuhnya pada HTML. Jadi, indentansi ataupun seluruh text yang ada akan ditampilkan

2. innerText 
Melihat css nya dulu. Apakah ke-display atau enggak

## 4. Modifying Element HTML

```js
const body = document.body
const div = document.createElement("div")

// Tidak ke Bold. Tulisan strong nya malah ke print
div.innerText = "<strong>Hello World</strong>" 
div.textContent = "<strong>Hello World</strong>"

// harus pakai gini
div.innerHTML = "<strong>Hello World</strong>" 

body.append(div)
```
Tapi, katanya innerHTML ini kurang secure karena kita bisa memasukkan command HTML ke sebuah variabel

Alternatif nya adalah
```js
const body = document.body
const div = document.createElement("div")
const strong = document.createElement("strong")
strong.innerText = "Hello Worldddd"
div.append(strong)

body.append(div)
```

Coba tambahkan ke .html nya
```html
<div>
    <span id="hello">Hello</span>
    <span id="world">World</span>
</div>
```

Replace js nya jadi
```js
const body = document.body
const div = document.querySelector('div')
const spanHello = document.querySelector('#hello')
const spanWorld = document.querySelector('#world')
```

## 5. Removing Elements
Semisal kita ingin remove kata `World`

Ada beberapa cara

Cara pertama, pakai `.remove()`
```js
const body = document.body
const div = document.querySelector('div')
const spanHello = document.querySelector('#hello')
const spanWorld = document.querySelector('#world')

spanBye.remove()
// div.append(spanWorld)
```

Cara kedua, kita remove dari parrent nya pakai `.removeChild()`
```js
const body = document.body
const div = document.querySelector('div')
const spanHello = document.querySelector('#hello')
const spanWorld = document.querySelector('#world')

div.removeChild(spanWorld)
```

## 6. Modifying Element Attributes
Gimana cara class, atribut, dll ?
Fungsi ini yang paling banyak digunakan

Coba tambahkan ke .html nya
```html
<div>
    <span title = "hello" id="hello">Hello</span>
    <span id="world">World</span>
</div>
```

Di file js coba tambahkan

```js
const body = document.body
const div = document.querySelector('div')
const spanHello = document.querySelector('#hello')
const spanWorld = document.querySelector('#world')

console.log(spanHello.getAttribute('id'))
console.log(spanHello.getAttribute('title'))
// itu sama dengan
console.log(spanHello.id)
console.log(spanHello.title)
```

Sekarang kita coba ubah id dari sebuah atribut
```js
const body = document.body
const div = document.querySelector('div')
const spanHello = document.querySelector('#hello')
const spanWorld = document.querySelector('#world')

console.log(spanHello.setAttribute('id', 'hello_69'))
console.log(spanHello.setAttribute('title', 'title_69'))
// sama dengan
console.log(spanHello.id = 'hello_69')
console.log(spanHello.title = 'hello_69')
```

Kita juga bisa remove attribut
```js
const body = document.body
const div = document.querySelector('div')
const spanHello = document.querySelector('#hello')
const spanWorld = document.querySelector('#world')

spanHello.removeAttribute('title')
```

## 7. Modifying Data Attributes

di html coba ubah jadi
```html
<div>
    <span id="hello" data-test="ini data hello">Hello</span>
    <span id="world">World</span>
</div>
```

Coba kita dapatkan data atrribute, di file js
```js
const body = document.body
const div = document.querySelector('div')
const spanHello = document.querySelector('#hello')
const spanWorld = document.querySelector('#world')

console.log(spanHello.dataset)
```

Kita coba tambahkan data atribut yang lain
```html
<div>
    <span id="hello" data-test="ini data hello" data-hehe-hoho="hehehehe">Hello</span>
    <span id="world">World</span>
</div>
```

Coba kita simpan lagi. Nanti data yang hehe-hoho akan menjadi camelcase

Semisal lebih dari satu data, bisa kita spesifisikan
```js
const body = document.body
const div = document.querySelector('div')
const spanHello = document.querySelector('#hello')
const spanWorld = document.querySelector('#world')

console.log(spanHello.dataset.test)
console.log(spanHello.dataset.heheHoho)
```

Kita juga bisa set atau tambah properti data baru
```js
const body = document.body
const div = document.querySelector('div')
const spanHello = document.querySelector('#hello')
const spanWorld = document.querySelector('#world')

spanHello.dataset.dataBaru = "data baru"
```

## 8. Modifying Element Classes

Pada html, coba kita tambahkan
```html
<div>
    <span id="hello" class="hello1 hello2">Hello</span>
    <span id="world">World</span>
</div>
```

Lalu pada file .js , kita akan menggunakan classList. Untuk method-nya ada banyak, bisa diakses [disini](https://blog.webdevsimplified.com/2020-11/class-list/)

```js
const body = document.body
const div = document.querySelector('div')
const spanHello = document.querySelector('#hello')
const spanWorld = document.querySelector('#world')

// add
spanHello.classList.add("class-baru")

// remove 
spanHello.classList.add("hello1")

// toggle. Jika ada akan di remove, jika belom akan di add
spanHello.classList.toggle("hello3")
spanHello.classList.toggle("hello3", true) // otomatis add
spanHello.classList.toggle("hello3", false) // otomatis remove
```

## 9. Modifying Element Style

```js
const body = document.body
const div = document.querySelector('div')
const spanHello = document.querySelector('#hello')
const spanWorld = document.querySelector('#world')

spanHello.style.color = "red"

// jika style > 2 kata, pakai camelCase
spanHello.style.backgroundColor = "red"
```