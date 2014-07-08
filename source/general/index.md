現在，我們要進行第一個重頭戲。那就是首頁（index.php）的製作。首頁是一個網頁給人的第一印象，所以必須要做得好，訪客留下來閱讀的機會也會增高。

而在 index.php 中，我們會將 header.php, footer.php, sidebar.php 檔案以函式的方式載入。

而這次，我們只做最基本的讓網站文章跑出來，並做出一個好看的頁碼讓訪客能夠進到下一頁繼續看文章。

## 基本格局

首先，我們先把基本格局寫好，把 header.php, footer.php, sidebar.php 分別使用 get_header(), get_footer(), get_sidebar() 函式載入到 index.php。

```
<?php get_header(); ?>
<div class="content">
    <div class="article">
    </div>
    <div class="sidebar">
        <?php get_sidebar(); ?>
    </div>
</div>
<?php get_footer(); ?>
```

接下來，我們為上面的 HTML 標籤加上 CSS，讓網站能夠呈現兩欄的模樣，在 style.css 加入以下樣式碼：

```
.content {
  float:left;
  width:100%;
  margin-top:30px;
}
.article {
  width:70%;
  float:left;
}
.sidebar {
  width:30%;
  float:left;
}
```

現在，你可以打開 http://localhost 看看目前網站長得怎樣了！目前的樣子，大部分是在上一節 header.php 所做出來的樣式。如下圖：

![image015](/images/image015.jpg)

而，如果你想要修改樣式，你可以回到 header.php 及 style.css 進行修改！

## 迴圈輸出網站文章

在上一步的代碼中，.article 是顯示文章的區塊，而 .sidebar 則是顯示側邊欄的區塊。現在，因為是首頁，所以我們要在 .article 裡面一次跑出好幾篇文章，到一定數量即換頁。所以，把下面的代碼放到 .article 裡面，接著再看詳解。

```
<?php while ( have_posts() ) : the_post(); ?>
<article class="article-content">
    <h1 class="article-title">
        <a href="<?php the_permalink(); ?>"><?php the_title(); ?></a>
    </h1>
    <div class="article-meta">
        <span><?php the_time('n / j, Y'); ?></span><span> / </span>
        <span><?php the_category(' , '); ?></span><span> / </span>
        <span><?php the_tags('', ' , ', ''); ?></span>
    </div>
    <?php the_content(); ?>
    <div class="clearfix"></div>
</article>
<?php endwhile; ?>
```

在上面的代碼中，我們用了好幾個還沒出現過的函式，以下是解釋：

- while ( have_posts() ) － have_posts() 為判斷是否在資料庫中有文章，若有則回傳 true，並進入 while 迴圈中。
- the_post() － 載入文章相關函式，如需使用下面幾個跟文章資料有關的函式必須先加入 the_post() 函式，才會正常。
- the_title() － 輸出文章標題。
- the_time(' n / j, Y') － 輸出文章發表的時間，參數為顯示時間的格式。n / j, Y 表示格式為 月 / 日, 年，詳細輸出格式可參考：[WP Codex－Format Date & Time](http://codex.wordpress.org/Formatting_Date_and_Time)
- the_category(' , ') － 輸出文章所在分類。參數為分類與分類間的分隔符號。如 分類一, 分類二。
- the_tags('', ' , ', '') － 輸出文章之標籤。第一個參數為在輸出標籤前的文字，假設為 '標籤：' 則整個函式會輸出「標籤：標籤 1, 標籤 2」。第二個參數為標籤與標籤之間的分隔符號。第三個參數為在輸出標籤後的文字，假設為
'<br>' 則輸出文字後將會直接換行。
- the_content() － 輸出文章內容。
- the_permalink() － 輸出文章網址

接下來，我們為上面那些標籤加上稍微好看又清爽的 CSS 樣式：

```
.article-content {
  background:#FFF;
  margin:30px;
  padding:20px;
}
.article-content p {
  font:15px/1.7 "Open Sans", sans-serif;
  color:#565656;
  margin:15px 0;
}
.article-title {
  font-size:32px;
  color:#555;
  line-height:1.8;
  font-weight:300;
}
.article-meta span {
  color:#888;
  font-size:13px;
  margin-right:7px;
}
.article-meta span a {
  color:#888;
  text-decoration:none;
}
.article-meta span a:hover {
  text-decoration:underline;
}
.clearfix {
  content:".";
  display:block;
  height:0;
  clear:both;
  visibility:hidden;
}
```

截至目前，佈景主題長成這樣：

![image016](/images/image016.jpg)

## 繼續閱讀字樣美化

現在，我覺得繼續閱讀的文字和其他文字除了顏色以外沒有差異性，所以我想要來做一點樣式美化它：你會發現，在之前寫的代碼中完全沒有繼續閱讀這四個字。沒錯，因為繼續閱讀是在 the_content() 函式中被顯示的，所以你不會看到他在你寫的代碼中。不過，利用 Chrome 的 Developer Tools 的檢查元素之後，我們會發現繼續閱讀那四個字的 CSS class 是 more-link。所以，我們就幫繼續閱讀那四個字做美化吧。

```
.more-link {
  float:right;
  color:#666;
  background:#EFEFEF;
  text-decoration:none;
  padding:7px 10px;
}
.more-link:hover {
  background:#888;
  color:#FFF;
}
```

![image017](/images/image017.jpg)

另外，上面所提到的檢查元素，只要你在 Chrome 中，將滑鼠游標移至繼續閱讀四個字上，然後按右鍵，點檢查元素，就會看到那一段的原始碼了！


## 精緻頁碼製作

接著，我們要為文章列表加上一個有點精緻的簡單頁碼了，讓訪客能夠換下一頁繼續閱讀。而頁碼我們用數字的方式呈現，另外還需在 functions.php 內加入一個輸出頁碼的函式。所以，我們先在 functions.php 內加入頁碼函式：

```
function wp_pagenavi() {
    global $wp_query;
    $max = $wp_query->max_num_pages;
    if ( !$current = get_query_var('paged') ) $current = 1;
    $args['base'] = str_replace(999999999, '%#%', get_pagenum_link(999999999));  $args['total'] = $max;
    $args['current'] = $current;
    $args['prev_text'] = '<';  $args['next_text'] = '>';
    if ( $max > 1 ){
        $pages = '<div class="wp-pagenavi"><span class="pages">共 ' . $max . ' 頁</span>';
        echo $pages . paginate_links($args) . '</div>';
    }
}
```

我們做出頁碼的方法是利用 WordPress 內建的 `paginate_links()` 函式，來跑出頁碼。而由於 `paginate_links()` 函式預設的顯示方法不合我們的需求，所以我們要利用一些參數讓顯示能夠達到我們要的效果。（[WP_Codex paginate_links](http://codex.wordpress.org/Function_Reference/paginate_links)）

- `$wp_query` － 用意在之後的 `$wp_query->max_num_page` －用來取得總頁數，因為我們是寫在函式裡面，所以必須要把 `$wp_query` 令為全域變數。
- `get_query_var('paged')` － 取得目前所在的頁數。
接著，有一個 `$arg` 的陣列，裡面存放的資料會在下面的 `paginate_links($args)` 當作參數傳給系統。
- `$args['base']` － 用來避免第一頁頁碼會沒有連結的問題，這樣可以確保每一個頁碼都有連結可以點。（除了目前所在頁面的頁數）。
- `$args['total']` － 總頁數。
- `$args['current']` － 目前所在頁數
- `$args['prev_text']` － 上一頁顯示之文字
- `$args['next_text']` － 下一頁顯示之文字

接著，來加入一些讓頁碼更好看的 CSS 樣式囉：

```
.wp-pagenavi {
  background:#FFF;
  margin:30px;
  padding:20px;
}
.pages {
  color:#888;
  margin-right:13px;
}
.page-numbers {
  color:#FFF;
  background:#888;
  text-decoration:none;
  padding:5px 10px;
}
.page-numbers:hover,.page-numbers.current {
  color:#FFF;
  background:#666;
}
```

接著，你就可以在 index.php 的 `</div><div class="sidebar">` 之前加入呼叫函式：

```
<?php wp_pagenavi(); ?>
```

這樣，就可以做出好看又有點精緻的頁碼囉。做好之後如下圖：

![image018](/images/image018.jpg)
