# ๐ Pointillism
<br/>

![10](https://user-images.githubusercontent.com/84780174/139401901-8f5b53ba-8c76-4682-b53b-9fcdda230ba0.jpg)

![doc](https://user-images.githubusercontent.com/84780174/139401824-3c289d8e-0ebe-4569-93cf-e0a590edd53e.jpg)

<br/>


<a href="https://limhyejeong.github.io/pointillism/" target="_black">https://limhyejeong.github.io/pointillism/</a>

<br/><br/>

# โณ๏ธ ์ ์ ์๋

์ ๋ฌํ๋ ์ ์ ์ฐ์ด์ ๊ทธ๋ฆผ์ ๊ทธ๋ฆฌ๋ ํ๋ฒ์ผ๋ก, ํ๋์ค์ ํ๊ฐ ์กฐ๋ฅด์ฃผ ์ ๋ผ๊ฐ ๊ฐ๋ฐํ ํ๋ฒ์ด๋ค.

์กฐ๋ฅด์ฃผ ์ ๋ผ์ ๋ํ์ ์ธ ๊ทธ๋ฆผ '๊ทธ๋๋์ํธ ์ฌ์ ์ผ์์ผ ์คํ'๋ฅผ

p5.js์ ์ด๋ฏธ์ง ์ ๋ณด๋ฅผ ์ป๋ ๋ฐฉ๋ฒ์ผ๋ก ํฝ์ํํด๋ณด์๋ค.
<br/><br/><br/>

# ๐งฉ ์ธํฐ๋์

- ๋ง์ฐ์ค ๋๋๊ทธ์ ํ ๋ก ์ (ํฝ์)์ ์ฌ์ด์ฆ ๋ณ๊ฒฝ

<br/><br/>

# ๐จ ๊ตฌํ ๋ฐฉ๋ฒ & ์ฝ๋
<br/>

## 1. ์ฌ์ง ๋ถ๋ฌ์ค๊ธฐ

```jsx
function preload() {
   img = loadImage('seurat.jpg');
}
```

preload()๋ setup()์ด ์คํ๋๊ธฐ ์ ์ ํธ์ถ๋๋ ํจ์์ด๋ฉฐ,

์ธ๋ถ ํ์ผ์ ๋น๋๊ธฐ ๋ถ๋ฌ์ค๊ธฐ๋ฅผ ์ฐจ๋จํ๊ธฐ ์ํด ์ฌ์ฉ๋๋ค.

<br/><br/><br/>

## 2. ์ด๋ฏธ์ง ํฝ์ํ

```jsx
function draw() {
   background(0);

   // ์ด๋ฏธ์ง์ ํฝ์ ์ ๋ณด ์ ๊ทผ
   for (let col = 0; col < img.width; col += size) {
      for (let row = 0; row < img.height; row += size) {
         let c = img.get(col, row);
         stroke(color(c));
         strokeWeight(size);
         point(col, row);
      }
   }
}
```

img.get์ผ๋ก ์ด๋ฏธ์ง ์ ๋ณด๋ฅผ ๋ถ๋ฌ์จ ํ, ํ๊ณผ ์ด์ ๋ง๊ฒ ํฝ์์ ๋ฐฐ์นํ์๋ค.

point๊ฐ ์๋ rect ๋ฑ์ ๋ค๋ฅธ ๋ํ ํจ์๋ฅผ ์ฐ๋ฉด ๋ค๋ฅธ ๋ชจ์์ ํฝ์์ด ๋๋ค.

<br/><br/><br/>

## 3. ๋ง์ฐ์ค ์ด๋ฒคํธ

```jsx
// ๋ง์ฐ์ค ๋๋๊ทธ ์ด๋ฒคํธ
function mouseDragged() {
   // ์ด๋ฏธ์ง ์์ ์ปค์๊ฐ ์๋์ง ํ์คํธ
   if(
      mouseX > 0 && mouseX < img.width &&
      mouseY > 0 && mouseY < img.height
   ) {
      // ์๋๋ก ๋์ด๋ด๋ฆฌ๋ฉด size ์ถ์
      if (mouseY < y) {
         if (size > minSize) {
            size -= 1;
         }
      }
      // ์๋ก ๋์ด์ฌ๋ฆฌ๋ฉด size ํ๋
      else {
         if (size < maxSize) {
            size += 1;
         }
      }
   }
}
```

```jsx
// ๋ง์ฐ์ค ํ  ์ด๋ฒคํธ
function mouseWheel(e) {
   // ์ด๋ฏธ์ง ์์ ์ปค์๊ฐ ์๋์ง ํ์คํธ
   if(
      mouseX > 0 && mouseX < img.width &&
      mouseY > 0 && mouseY < img.height
   ) {
      // ํ ์ ์ฌ๋ฆฌ๊ณ  ์๋ค๋ฉด deltaY๊ฐ์ด ์์
      if (e.deltaY < 0) {
         if (size > minSize) {
            size -= 1;
         }
      }
      // ํ ์ ๋ด๋ฆฌ๊ณ  ์๋ค๋ฉด deltaY๊ฐ์ด ์์
      else {
         if (size < maxSize) {
            size += 1;
         }
      }
   }
}
```

๋ง์ฐ์ค ๋๋๊ทธ์ ํ ๋ก ํฝ์์ ์ฌ์ด์ฆ๋ฅผ ๋ณ๊ฒฝํ  ์ ์๊ฒ ํ์๋ค.

๋ ํจ์์ ์ค๋ณต๋๋ ๋ถ๋ถ์ resize ํจ์๋ฅผ ์์ฑํ์ฌ ๋ฆฌํฉํ ๋งํ์๋ค.

```jsx
function resize(low, high) {
   // ์ด๋ฏธ์ง ์์ ์ปค์๊ฐ ์๋์ง ํ์คํธ
   if(
      mouseX > 0 && mouseX < img.width &&
      mouseY > 0 && mouseY < img.height
   ) {
      if (low < high) {
         if (size > minSize) {
            size -= 1;
         }
      }
      else {
         if (size < maxSize) {
            size += 1;
         }
      }
   }
}
```
