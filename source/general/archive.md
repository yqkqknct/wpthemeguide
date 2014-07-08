Archive.php 是用來顯示彙整的文章，如列出標籤為某標籤的所有文章，分類為某分類的全部文章，也可以用依年分顯示文章。

有些佈景是將標籤、分類另外獨立出 tag.php 與 category.php 兩個檔案，而在這邊，我們只用 archive.php 來達成，比較方便一點。

## 基本格局

其實也是跟前面顯示文章的地方相當類似：

```
<?php get_header(); ?>
<div class="content">
    <div class="article">
    <?php while ( have_posts() ) : the_post(); ?>
        <article class="article-content">
            <h1 class="article-title"><a href="<?php the_permalink(); ?>"><?php the_title(); ?></a></h1>
            <div class="article-meta">
                <span><?php the_time('n / j, Y'); ?></span><span> / </span>
                <span><?php the_category(' , '); ?></span><span> / </span>
                <span><?php the_tags('', ' , ', ''); ?></span>
            </div>
            <?php the_content(); ?>
            <div class="clearfix"></div>
        </article>
    <?php endwhile; ?>
    <?php wp_pagenavi(); ?>
    </div>
    <div class="sidebar">
        <?php get_sidebar(); ?>
    </div>
</div>
<?php get_footer(); ?>

```

而要怎麼讓使用者知道這是一個彙整的頁面？在後面 breadcrumb 的地方會再進行補充的動作。


