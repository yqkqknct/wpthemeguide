Search.php 會顯示 WordPress 內建的搜尋系統之搜尋解果，當使用者於站內搜尋框搜尋後，將會使用 search.php 來顯示結果。

當然，程式碼與上一章也是非常類似，不過多了一個 have_posts() 來判斷是否有搜尋到文章，沒有的則提示沒有結果，請使用別的關鍵字再搜尋一次。

```
<?php get_header(); ?>
<div class="content">
    <div class="article">
    <?php if ( have_posts() ) : ?>
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

        <?php else : ?>

        <article class="article-content">
            <h1>搜尋結果</h1>
            <p>很抱歉，找不到你所搜尋的文章，你可以試著用其他關鍵字再次搜尋。</p>

            <?php get_search_form(); ?>
        </article>
    <?php endif; ?>
    </div>
    <?php wp_pagenavi(); ?>
    <div class="sidebar">
        <?php get_sidebar(); ?>
    </div>
</div>
<?php get_footer(); ?>

```

-   get_search_form － 顯示迴響表單（searchform.php）。這樣，顯示搜尋結果頁也完成囉！
