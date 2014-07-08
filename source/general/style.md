在 style.css 中，我們將設定 WordPress 控制台將擷取的佈景主題各項資訊，如名稱、說明、作者、版號等等。

打開 style.css。

## WordPress 佈景主題資訊

首先，在 style.css 中，加入以下註解，並加以修改：

```
/*
Theme Name: Fundesigner
Theme URI: http://fundesigner.net Description: A Fundesigner Theme.
Author: Yuxin
Author URI: http://fundesigner.net
Version: 1.0
Tags: white, two-columns
License: GNU General Public License v2 or later
License URI: http://www.gnu.org/licenses/gpl-2.0.html
*/
```
這樣，在控制台的地方你就會看到你所設定的新佈景主題。如下圖的左方：

![image013](/images/image013.jpg)


現在可以按啟用。當然，現在啟用網站會是一片空白，我們還沒有做頁面。不過，先來看一下上面的每一行的用意：

- Theme Name: 佈景主題名稱
- Theme URI: 佈景主題網址
- Description: 佈景主題說明
- Author: 佈景主題作者
- Author URI: 佈景主題作者網站
- Version: 佈景主題版本號
- Tags: 佈景主題標籤
- License: 佈景主題授權
- License URI: 佈景主題授權書

## Style.css Reset

一般來說，在開發網站要撰寫 CSS 之前，我們都會先利用將各項元素 reset 掉，以避免各瀏覽器對各元素的初始設定不同。

所以，請在 style.css 內（註解的後面）加入以下 reset CSS 的樣式碼：

```
@import url(http://fonts.googleapis.com/css?family=Open+Sans:300,400);
html,body,div,span,applet,object,iframe,h1,h2,h3,h4,h5,h6,p,blockquote,pre,a,abbr,acronym,address,big,cite,code,del,dfn,em,img,ins,kbd,q,s,samp,small,strike,strong,sub,sup,tt,var,b,u,i,center,dl,dt,dd,ol,ul,li,fieldset,form,label,legend,table,caption,tbody,tfoot,thead,tr,th,td,article,aside,canvas,details,embed,figure,figcaption,footer,header,hgroup,menu,nav,output,ruby,section,summary,time,mark,audio,video {
    border:0;
    font-size:100%;
    font:inherit;
    vertical-align:baseline;
    margin:0;
    padding:0;
}
article,aside,details,figcaption,figure,footer,header,hgroup,menu,nav,section {
    display:block;
}
body {
    line-height:1;
}
ol,ul {
    list-style:none;
}
blockquote,q {
    quotes:none;
}
blockquote:before,blockquote:after,q:before,q:after {
    content:none;
}
table {
    border-collapse:collapse;
    border-spacing:0;
}
```

另外，第一行的 @import 純粹是因為在後面我們會使用到 Open Sans 字體，先把它引入進來。

## 加入一些基本元素樣式

在上面的樣式碼中，我們將全部的元素預設樣式都清掉了，所以我們現在就可以來套上自己希望元素長怎樣的樣式了。如 a, ul, blockquote 等等。將下面的樣式碼加入 style.css（緊接著上面的最後）。

```
a {
  color:#22A2EB;
  text-decoration:none;
}

a:hover {
  text-decoration:underline;
}

img {
  max-width:100%;
  height:auto;
}

ul {
  margin-left:25px;
}

li {
  list-style:square;
  color:#555;
  margin:5px 0;
}

h1 {
  font-size:32px;
  color:#555;
  line-height:1.8;
  font-weight:300;
}

h2 {
  font-size:26px;
  line-height:1.48;
}

h3 {
  font-size:20px;
  line-height:1.48;
  color:#777;
}
```

## 接下來的開發

接下來，只要後面的章節提到 CSS 樣式碼，都是寫在 style.css 中。（寫在上面那段的後面接著寫。）。另外，請注意括號的配對，不要漏掉唷。
