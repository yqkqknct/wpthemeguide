最近，Facebook 等社群網站的分享越來越頻繁，而如果要 Facebook 轉貼連結時顯示的文章縮圖、描述正確的話，就必須使用`<meta property="og:title" ….>` 等標籤，這麼一來你就可以控制 Facebook 顯示的縮圖和描述，換句話說就是能讓 Facebook 抓的資料正確。

另外，下面這些代碼最初是由就是教不落的阿湯分享出來的，後來經過一些小修改。

其實原理很簡單，還記得我們在 header.php 中提到的 wp_head(); 嗎？我們就要利用這個地方，讓 function 在這裡插入一些 og 標籤。

只要將這個 function 加入到 functions.php 就可以了。

```
function insert_fb_in_head() {
    global $post;
    if ( is_home() ) {
        echo '<meta property="fb:admins" content="管理員的 Facebook 帳號 ID" />';
        echo "\n";
        echo '<meta property="fb:app_id" content="網站 Facebook APP 的 ID" />';
        echo "\n";
        echo '<meta property="og:type" content="website"/>';
        echo "\n";
        echo '<meta property="og:title" content="' . get_bloginfo('name') . '"/>';
        echo "\n";
        echo '<meta property="og:description" content="' . get_bloginfo('description'). '"/>';
        echo "\n";
        echo '<meta property="og:url" content="' . get_bloginfo('url'). '"/>';
        echo "\n";
        echo '<meta property="og:site_name" content="'. get_bloginfo('name'). '"/>';
        echo "\n";
        echo '<meta property="og:locale" content="zh_tw">';
        echo "\n";
    }
    if ( !is_singular() ) return;
    $post_excerpt =  ( $post->post_excerpt ) ?
    $post->post_excerpt : trim( str_replace( "\r\n", ' ', strip_tags( $post->post_content ) ) );
    $description = mb_substr( $post_excerpt, 0, 160, 'UTF-8' );
    $description .= ( mb_strlen( $post_excerpt, 'UTF-8' ) > 160 ) ? '…' : '';         echo "\n";
    echo '<meta property="fb:admins" content="管理員的 Facebook 帳號 ID" />';
    echo "\n";
    echo '<meta property="fb:app_id" content="網站 Facebook APP 的 ID" />';
    echo "\n";
    echo '<meta property="og:title" content="' . get_the_title() . '"/>';
    echo "\n";
    echo '<meta property="og:description" content="' . $description . '"/>';
    echo "\n";
    echo '<meta property="og:type" content="article"/>';
    echo "\n";
    echo '<meta property="og:url" content="' . get_permalink() . '"/>';
    echo "\n";
    echo '<meta property="og:site_name" content="' . get_bloginfo('name'). '"/>';
    echo "\n";
    echo '<meta property="og:image" content="'.$img.'" />' ;
    echo "\n";
    echo '<link rel="image_src" type="image/jpeg" href="'.get_feature_image().'" />' ;
    echo "\n";
    echo '<meta property="og:locale" content="zh_tw">';
    echo "\n";
}
add_action( 'wp_head', 'insert_fb_in_head', 10 );
```

新增完以後，你要先去 [Facebook Developer APP](https://developers.facebook.com/apps) 新增一個屬於你的網站的 APP，然後再把 APP ID 替換「網站 Facebook APP 的 ID」，你的 Facebook 帳號 ID 替換「管理員的 Facebook 帳號 ID」。（共四處）

- add_action( 'wp_head', 'insert_fb_in_head', 10 );

add_action() 這個函式可以說是 WordPress 廣為流行的原因之一，它可以讓開發者在佈景內、控制台內新增非常多的自定義選項、文字。第一個參數 wp_head 就是插入到哪個 WordPress 哪個函式中，insert_fb_in_head 就是我們自己新增的函式，會被 wp_head 拿去用。後面的 10 是重要程度，數字越小越重要。

