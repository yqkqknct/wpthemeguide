在許多部落格、網站上，其文章列表的每一個文章旁邊，通常都會有一張在那篇文章之中的圖片。而這個功能最簡單可以利用 WordPress 內建的「特色圖片」（在編輯文章右側），直接去抓取圖片並且顯示出來。

另外，有些佈景主題會去自動抓取文章中第一張圖片作為特色圖片，其方法也會在本章中介紹。

有一個問題，如果抓取出來每一篇圖片大小不一，排版很醜，用 HTML width 控制圖片又會變得很醜，怎麼辦？我們有兩種方法，第一種是使用 Timthumb，第二種是使用 WordPress 內建的 Crop 功能。不過目前較多佈景是使用
Timthumb，和 WordPress 內建的 Crop 功能差異就是儲存的地方一個是佈景內，另一個是 /wp-content/uploads。

## 開啟特色圖片功能

這個特色圖片的功能預設是沒有開啟的，現在我們要把他打開。

```
if ( function_exists( 'add_theme_support'  ) ) {
    add_theme_support( 'post-thumbnails' );
}
```

語法很簡單，就是 add_theme_support 增加佈景支援功能→post-thumbnails 中譯特色圖片。接著你就會看到他出現了：

![image029](/images/image029.jpg)

## 取得特色圖片圖片網址

取得特色圖片 WordPress （[WP Codex－Post Thumbnails](http://codex.wordpress.org/Post_Thumbnails)）有內建函式，首先是判斷有沒有特色圖片：

```
if ( has_post_thumbnail() ) { /*有特色圖片執行這裡*/ }
```

取得特色圖片：（含 `<img src … >`）

```
$img = get_the_post_thumbnail();
```

顯示特色圖片：（含 `<img src … >`）

```
the_post_thumbnail();
// 相當於 echo get_the_post_thumbnail()

```

取得特色圖片圖片網址：（只有圖片路徑）

```
wp_get_attachment_url( get_post_thumbnail_id() );
```

## 抓取文章第一張圖片

而抓取文章第一張圖片的方式，也非常簡單，只要寫成一個函式就可以達成。另外，這個函式會先判斷目前有沒有設定特色圖片，沒有設定才會去抓第一張圖片，有設定就會直接回傳特色圖片路徑。

```
function get_feature_image(){  global $post, $posts;  $first_img = '';
    if ( has_post_thumbnail() ) {
        $first_img  = wp_get_attachment_url( get_post_thumbnail_id() );
    } else {
        ob_start();
        ob_end_clean();
        $output = preg_match('/<*img[^>]*src*=*["\']?([^"\']*)/i', $post->post_content, $matches);
        $first_img = $matches[1];
    }
    return $first_img;
}

```

而抓取第一張圖片的方式其實很簡單，我們只要用 PHP 的 preg_match 用正規表達式去比對就可以了。另外，因為我們只要第一張圖片，所以不使用 preg_match_all。

## 使用 Timthumb 裁切圖片


Timthumb 是一個非常好用的圖片裁切工具，他可以依照你所給的圖片尺寸去做裁切。而要使用 Timthumb 之前，你需要先去下載 [Timthumb.php](http://timthumb.googlecode.com/svn/trunk/timthumb.php)。 下載回來後，不要對 Timthumb.php 做修改，你可以放到佈景目錄裡頭。

另外，要新增一個資料夾名為 cache，提供給 Timthumb 放置裁切後的圖片。

接著，如果你要在佈景的任何地方使用，你只要使用下面這一行語法：


```
<img src="<?php bloginfo('template_url') ?>/timthumb.php?src=<?php echo get_feature_image() ?>&w=裁切後寬度&h=裁切後高度&zc=1" />
```

再來，你只要把「裁切後寬度」和「裁切後高度」這兩個地方改成你要的大小即可。（不必加 px）。另外，zc=1 代表要裁切，預設從圖片中間開始裁切。


