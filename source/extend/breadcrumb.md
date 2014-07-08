第一次看到 Breadcrumb 的人一定會有個疑問：這能吃嗎？

Breadcrumb 其實顯示出來就是類似 「首頁 > 程式設計 > WordPress 介紹」這樣，可以讓使用者知道目前所在的網頁位置。算是個不起眼但不可缺乏的小設計。
而我們這次要將 Breadcrumb 的功能寫成函式，方便每個檔案都能輕鬆使用。

```
function breadcrumb_init(){
    global $post;
?>
<ul class="breadcrumb">
    <li itemscope itemtype="http://data-vocabulary.org/Breadcrumb"><a href="<?php bloginfo('url');?>" itemprop="url" title="<?php bloginfo('name');?>">
        <span itemprop="title"><?php bloginfo('name');?></span></a>
    </li>
    <?php
    if( is_single() ) {
        foreach ( get_the_category() as $category) {
            echo '<li itemscope itemtype="http://data-vocabulary.org/Breadcrumb">';
            echo '<span class="divider">›</span> <a href="' . get_category_link($category -> term_id) . '" itemprop="url" title=' . $category -> cat_name . '> <span itemprop="title">' . $category -> cat_name . '</span></a>';
            echo '</li>';
        }
    } else { ?>
        <li itemscope itemtype="http://data-vocabulary.org/Breadcrumb" class="active">
            <span class="divider">›</span>
            <span itemprop="title">
            <?php
            if ( is_category() ) {     echo single_cat_title();    } elseif ( is_tag() ) {
            echo single_tag_title( '', true);
            } elseif ( is_day() ) {
            the_time( get_option('date_format') );
            } elseif ( is_month() ) {     the_time( 'F, Y' );    } elseif ( is_year() ) {     the_time( 'Y' );
            } elseif ( is_page() ) {     the_title();
            } ?></span>
        </li>
    <?php } ?>
</ul>
<?php
}

```

這部分使用到的函式比較多是 is_ 開頭的，都是用來判斷目前使用者所在的頁面來顯示不同的文字。
再來，再加上一點 CSS：

```
.breadcrumb {
  overflow:hidden;
  white-space:nowrap;
  background:transparent;
  font-size:13px;
  color:#999;
  margin:0 0 0 50px;
  padding:0;
}
.breadcrumb li {
  display:inline-block;
  text-shadow:0 1px 0 #FFF;
  margin:0;
}
.breadcrumb i {
  vertical-align:middle;
  opacity:0.5;
  margin:0 4px 0 0;
}
.breadcrumb a {
  color:#999;
}
.breadcrumb .divider {
  color:#ccc;
  padding:0 5px;
}
```

之後，如果要顯示出 Breadcrumb 可以直接使用此函式：`breadcrumb_init();`。
如，你可以在 archive.php 、 single.php、 page.php 的 `<div class="article">` 之後加入

```
<?php breadcrumb_init(); ?>
```

之後就可以顯示出麵包屑囉！

![image027](/images/image027.jpg)
