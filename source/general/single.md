現在，要開始來做一個網站也很重要的部分，那就是文章內頁囉！一個部落格中最重要的就是它的文章內容，如果文章排版的很乾淨、沒有雜七雜八的東西的話，那麼對文章來講是大大加分（當然文章的內容也很重要。）！

在文章內頁中，有一些代碼和 index.php 有些雷同，所以已經說明過的函式我們就不再講。而在 single.php 中，在文章的後面還有迴響區。另外，像顯示作者、插入 Google Adsense 廣告等實作，將會放在番外篇，讓這一節不會太過於冗長，想先看的讀者可以先偷偷的去看一下番外篇。


## 基本格局

基本格局，有部分和 index.php 相同。

```
<?php get_header(); ?>
<div class="content">
    <div class="article">
        <?php while ( have_posts() ) : the_post(); ?>
        <article class="article-content">
            <h1 class="article-title"><?php the_title(); ?></h1>
            <div class="article-meta">
                <span><?php the_time('n / j, Y'); ?></span><span> / </span>
                <span><?php the_category(' , '); ?></span><span> / </span>
                <span><?php the_tags('', ' , ', ''); ?></span>
            </div>
            <?php the_content(); ?>
            <div class="clearfix"></div>
        </article>
        <?php endwhile; ?>
    </div>
    <div class="sidebar">
        <?php get_sidebar(); ?>
    </div>
</div>
<?php get_footer(); ?>
```

相似度相當高呢！呵呵，我們拿掉了什麼？頁碼。

## 迴響區塊嵌入

接著，我們要在文章之後插入顯示迴響的函式。在 `</article>` 後加入：

```
<div id="comments">
    <?php comments_template(); ?>
</div>
```

- comments_template() － 載入 comments.php 的內容。現在你打開來看是還沒有迴響的，因為我們還沒有製作 comments.php。
