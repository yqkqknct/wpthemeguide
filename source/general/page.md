接下來則是和 single.php 有九十五分神似的 page.php 了，page.php 是顯示頁面的檔案，而通常會放如聯絡資訊、關於我們、作品集等等資訊。

在 page.php 中，我們的基本格局和 single.php 幾乎一樣，去掉發表時間、分類與標籤，但不新增迴響樣板。

如果你想讓頁面與文章有不一樣的感覺，你可以自己修改。


## 基本格局

與 single.php 大致相同，但將發表時間、分類與標籤拿掉。（因為頁面沒有分類與標籤，也不需要顯示發表時間）

```
<?php get_header(); ?>
<div class="content">
    <div class="article">
        <?php while ( have_posts() ) : the_post(); ?>
        <article class="article-content">
            <h1 class="article-title"><?php the_title(); ?></h1>
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

完成。現在頁面長得像這樣：

![image022](/images/image022.jpg)

