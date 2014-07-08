在 header.php 中，我們將撰寫要在網頁頂部顯示的介面。此外，header.php 也是載入 CSS、Javascript 的地方，以及各項 meta 標籤。

`<head>` 頭部標籤同樣會放在這個檔案裡。

```
<!DOCTYPE html>
<html <?php language_attributes(); ?>>
    <head>
    <meta charset="<?php bloginfo('charset');?>" />
    <title><?php if (is_home()) { bloginfo('name'); echo ' - ';
                        bloginfo('description');
                    } else {
                        wp_title(' - ', true, 'right');
                        bloginfo('name');
                } ?>
    </title>
    </head>
<body>
```

從上面的程式碼中，你可能會看到幾個你不認識的函式：

- language_attributes() － 取得網站的語系。如 zh_tw。
- bloginfo() － 網站各項重要資料，如填入 'charset' 則輸出網站編碼，填入 'url' 則輸出網站的網址，'name' 則輸出網站名稱，'description'則輸出網站描述 。官方詳細參數：[WP Codex – bloginfo()](http://codex.wordpress.org/Function_Reference/bloginfo)
- wp_title() － 網站當前頁面名稱。官方詳細參數：[WP Codex – wp_title()](http://codex.wordpress.org/Function_Reference/wp_title)

## <head> 內標籤 － <meta>, <link>

接著，我們要開始加入跟佈景有相關性的標籤了。另外，你也可以加入自己需要的，如 jQuery Plugin 等等。在這裡僅加入較基本的幾項標籤。請加在 </title> 之後。

```
<?php wp_head(); ?>
<meta name="viewport" content="width=device-width, initial-scale=1" />
<link rel="pingback" href="<?php bloginfo( 'pingback_url' ); ?>" />
<link href="<?php bloginfo('template_directory') ?>/style.css" media="screen" rel="stylesheet" type="text/css" />
```

新函式說明：
- wp_head() － WordPress 頭部的 Hook。某些外掛會利用此處將外掛需要的 Javascript 檔案載入，我們也可以利用此處載入需要載入的檔案。
- bloginfo('pingback_url') － 網站 Pingback 的網址。
- bloginfo('template_directory') － 網站套用中佈景之路徑，如「http://網址/wp-content/themes/fundesigner」

## 網站頂部介面 － 選單、Logo 及其他

接著，我們要開始來寫會真正顯示在網站上的東西了！是不是很期待呢？其實也不用太期待，接下來的東西，並不只是複製貼上就完成了，除了複製貼上之外，你還要自己針對自己想要的樣式下去做修改、調整，讓佈景有你的風格，是你想要見到的。而我們將在 header.php 中製作選單、Logo 及整體介面上半部。首先，在 header.php 的 <body> 後面加入以下代碼：

```
<div class="container">
    <header class="header">
        <h1 class="title"><a href="<?php bloginfo('url'); ?>">樂在設計</a></h1>
        <nav>
        <?php wp_nav_menu( array( 'theme_location' => 'primary-menu' ) ); ?>
        </nav>
    </header>
```

為什麼我現在去開網站沒有任何東西？因為現在 WordPress 讀取的是index.php，而我們還沒有在 index.php 內將 header.php 嵌入進來，所以還沒有東西。不過先別急，我們先把這部分完成，到了 index.php 你就能一覽廬山真面目了。

等等！我們還沒有介紹 wp_nav_menu() 這個函式。這個函式說穿了就是把在控制台→外觀→選單中所設定的選單叫出來。'theme_location' 則是告訴系統要的是哪一個選單。因為我們還沒有定義出 'primary-menu' 這個選單，所以我們打開 functions.php 並加入以下函式：

```
<?php
    register_nav_menus( array(
      'primary-menu' => __( '主選單' )
     )
    );
?>
```

這樣，你在控制台→外觀→選單中應該就會看到能夠設定的選項，如下圖，而你可以新增幾個項目進去：（注意佈景主題位置→主選單必須被設定。）


![image014](/images/image014.jpg)

再來，我們要為之前的 HTML 標籤做 CSS 樣式美化。將以下的 CSS 樣式碼加入 style.css：

```
body {
    background:#FAFAFA;
    font-family:"Open Sans", sans-serif;
}
.container {
    width:1000px;
    margin:0 auto;
}
.header {
    width:100%;
    text-align:center;
}
.title {
    margin:60px 0;
}
.title a {
    font-size:60px;
    color:#666;
    text-decoration:none;
}
.menu li {
    display:inline-block;
    padding:5px 10px;
}
.menu li a {
    background:#FFF;
    color:#888;
    font-family:"Open Sans", sans-serif;
    font-weight:300;
    text-decoration:none;
    padding:8px 15px;
}
.menu li a:hover {
    background:#AAA;
    color:#FFF;
}
```

這樣，header.php 就算完成囉！請接著下一章 index.php 看，就能夠看到 header.php 的效果了！
