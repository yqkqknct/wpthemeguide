在文章頁面中，通常在文章結束後會顯示文章的作者資訊，也有作者的自我介紹。通常還會附上 Facebook 的個人頁面網址。而這次我們將使用函式來完成這項功能。


## 在控制台個人資訊新增選項

首先，我們可以在控制台 > 個人資訊裡面新增選項，讓作者的 Facebook 網址等等可以直接透過控制台修改。

```
function add_user_porfile( $contactmethods ) {
    $contactmethods['google'] = 'Google+ 個人網址';
    $contactmethods['facebook'] = 'Facebook 個人網址';
    $contactmethods['description_url'] = '個人介紹頁';
    return $contactmethods;
}
add_filter('user_contactmethods','add_user_porfile',1 0,1);

```

WordPress 有一個非常好用的地方，我們可以自己建立一個 function 然後使用 `add_filter()` 函式，如本例，在個人資料（user_contactmethods）就會顯示出更多選項。而這個新增的規則就是 `$contactmethods['ID'] = '選項名稱'`。

## 寫成 function

當然，接下來就要寫成 function 了，一番折磨後像這樣：

```
function article_author(){
    global $post;
?>
<section class="article-author">
    <div class="author-avatar"><?php echo get_avatar( get_the_author_meta('ID'), 100);?></div>
    <div class="author-text">
        <h3 class="author-name"><?php the_author();?></h3>
        <p class="author-description"><?php the_author_meta('description');?></p>
        <div class="author-social">
            <?php if ( get_the_author_meta( 'google' ) ): ?> <a href="<?php the_author_meta('google');?>?rel=author" title="我的 Google+">Google+</a>
            <?php endif; if ( get_the_author_meta( 'facebook' ) ): ?>  | <a href="<?php the_author_meta('facebook');?>" title="我的 Facebook">Facebook</a>
            <?php endif; if ( get_the_author_meta( 'description_url' ) ): ?> | <a href="<?php the_author_meta('description_url');?>" title="<?php the_author();?> 個人介紹">個人介紹</a><?php endif;?>
            </div>
    </div>
</section>
<?php
}

```

在這邊，有幾個函式要說明一下：
- get_avatar － 取得大頭貼，而在迴響的地方我們是用 `$comment`，但在文章裡我們可以直接用作者的 ID 來存取作者的大頭貼，而 100 則是大小。非常方便。
- get_the_author_meta(ID) － 就是存取在控制台個人資訊的選項囉！
- the_author_meta(ID) － 顯示控制台個人資訊的選項。
- the_author_meta('description') － 顯示作者介紹。

## Style

剩下的就是 CSS 的部分囉！希望你在學會之後，還能改出更好的樣式出來 ^__^

```
.article-author {
  width:100%;
  float:left;
  margin:20px 0;
  border-top:1px solid #EEE;
  border-bottom:1px solid #EEE;
  padding:20px 0;
}
.author-avatar {
  width:100px;
  float:left;
}
.author-avatar .avatar {
  border-radius:50%;
}
.author-text {
  float:left;
  width:480px;
  padding-left:20px;
}
.author-social {
  float:right;
  width:100%;
  text-align:right;
}
.author-name,.author-description {
  float:left;
  width:100%;
}
```

接著，你就可以在 single.php 的 `</article>` 前面加上

```
<?php article_author(); ?>
```

就會在文章頁面顯示出作者頭像囉！

![image028](/images/image028.jpg)
