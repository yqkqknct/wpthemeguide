Comments.php 算是整個佈景裡頭有一點複雜的地方，但是做出來一個清爽的迴響介面可是會非常棒呢！

## 需要密碼判斷

首先，我們先寫一個判斷式，為需要密碼才能查看迴響的程式碼。

```
<?php
    if ( post_password_required() ) return;
?>
```

上段程式碼 post_password_required() 就是用來判斷是否需要密碼才能觀看迴響。

## 顯示迴響部分

接下來是顯示迴響的部分，這部分複雜的是在有頗多的判斷式。

```
<h3 class="comment-title"><?php comments_number('沒有迴響', '迴響 (1)', '迴響 (%)' );?></h3>
<?php if ( have_comments() ) : ?>
    <ol class="comment-list">
        <?php wp_list_comments('type=comment&callback=displaycomments'); ?>
    </ol>
    <div class="clearfix"></div>
    <div class="pagenavi">
        <?php paginate_comments_links('prev_text=Prev Comments&next_text=Next Comments');?>
    </div>
    <?php else :  ?>
    <?php if ( comments_open() ) : ?>
        <p>本文還沒有迴響，快來搶頭香！</p>
    <?php else : ?>
        <p class="nocomments">本文不開放迴響。</p>
    <?php endif; ?>
<?php endif; ?>

```

第一行的 comments_number() 是用來顯示迴響數目的函式，而參數分別是沒有迴響時顯示的文字, 一個迴響時顯示的文字, 兩個以上迴響時顯示的文字。
而第二行，有一個 if ( have_comments() ) 的判斷式，而如果成立就會進入第三行到 else 之前的顯示迴響部分。這邊，有兩個要注意的地方：

- wp_list_comments('type=comment&callback=displaycomments'); － 顯示出迴響的函式。在這邊有一個 callback= displaycomments 的參數，我們可以新建 displaycomments 函式來調整迴響的顯示格式。稍後將介紹 displaycomments 自訂函式。
另外 type=comment 的意思是只顯示迴響部分，而 pingback 與 trackback 則不顯示。

- paginate_comments_links('prev_text=Prev Comments&next_text=Next
Comments'); － 這部分則是當迴響超過控制台設定的單頁數目時，會顯示上一頁迴響及下一頁迴響。prev_text 及 next_text 則是可以設定顯示之文字。

接下來 else 之後的程式碼就是當目前該文章沒有迴響時會進來這裡，而沒有迴響有兩種情況，一種是沒有人留言，另外一種是不開放留言。所以我們可以使用
if ( comments_open() ) 來判斷是否有開放迴響，有的話就是沒有人留言，沒有的話就是不開放迴響。最後記得要補上 endif;。


## 新建 displaycomments 函式

先說明一下，displaycomments 函式並不是 WordPress 內建的函式，而是我們自己新增的函式。這個函式的用途是可以自訂每則迴響之顯示格式，我們先在 functions.php 加入以下的程式碼，再來解說。

```
function displaycomments($comment, $args, $depth){
    $GLOBALS['comment'] = $comment;
?>
    <li class="comment-list-box">
        <div class="comment-author">
            <?php echo get_avatar( $comment, 40 ); ?>
        </div>
        <div class="comment-fn">
            <?php printf(__('<span class="fn">%s</span>'), get_comment_author_link()) ?>
        </div>
        <div class="comment-meta">
            <?php printf(__('%1$s @ %2$s'), get_comment_date(),  get_comment_time()) ?> <?php edit_comment_link() ?>
        </div>
        <?php if ($comment->comment_approved == '0') : ?>
            <em class="comment-approved">你的迴響正在審核中。</em>
        <?php endif;?>
        <?php comment_text() ?>
        <?php comment_reply_link(array_merge( $args, array('depth' => $depth, 'max_depth' => $args['max_depth']))) ?>
    </li>
<?php }
```

- `get_avatar( $comment, 40 );` － 這個函式是用來顯示出迴響留言者的大頭貼，而參數 $comment 表示是迴響用的，40 代表大小。
- `printf(__('<span class="fn">%s</span>'), get_comment_author_link())` － 這部分是顯示留言者名稱，如果有網站的話會一併加上連結。
- `<?php printf(__('%1$s @ %2$s'), get_comment_date(),  get_comment_time()) ?> <?php edit_comment_link() ?>` － 這部分是顯示留言時間，%1$s @ %2$s 為格式。而 edit_comment_link() 則是當該留言者是會員時顯示編輯之連結。
- `if ($comment->comment_approved == '0')` 是用來判斷迴響是否有通過審核，若尚未審核則顯示正在審核中。
- `comment_text()` 就是迴響的內容啦！
- `comment_reply_link(array_merge( $args, array('depth' => $depth, 'max_depth' => $args['max_depth'])))` － 這是用來顯示回覆的連結，而後面的參數是為了要讓階層功能正常，不可以省略。

## 留言表單部份

```
<?php comment_form(); ?>
```

由於 WordPress 有內建顯示迴響表單的函式，所以只要一行就能搞定了！

但是預設會顯示這兩句話：「你的電子郵件位址並不會被公開。 必要欄位標記為 *」與「你可以使用這些 HTML 標籤與屬性： ……」，如果不想要顯示的話，可改成這樣：

```
<?php comment_form("comment_notes_after=&comment_notes_before="); ?>
```

這樣就可以讓那兩句話消失。而 comment_notes_before 代表第一句話， comment_notes_after 代表第二句話。

## 迴響樣式碼

迴響樣式碼算是最難寫的部分，不過寫得好的話感覺會很棒。你可以特別去看一下寫法，有使用到 position 的功能。

```
#comments {
  background:#fff;
  margin:30px;
  padding:20px;
}
#comments li {
  list-style:none;
}
#comments li.comment-list-box {
  border-bottom:1px solid #eee;
  position:relative;
  margin:20px 0;
  padding:10px 0 20px 55px;
}
#comments li.comment-list-box .comment-author img {
  position:absolute;
  left:0;
  float:left;
  border-radius:50%;
  border:1px solid #ccc;
  margin:0 10px 5px 0;
}
#comments li.comment-list-box a.comment-reply-link {
  border:1px solid #ddd;
  color:#888;
  border-radius:20px;
  font-size:13px;
  display:inline-block;
  padding:5px 13px;
}
#comments li.comment-list-box a.comment-reply-link:hover {
  background:#eee;
  color:#888;
  text-decoration:none;
}
#comments ul.children {
  margin:0;
  padding:0;
}
#comments ul.children li {
  border-bottom:none;
  margin-bottom:0;
  padding-bottom:0;
}
#comments p {
  line-height:1.48;
  margin:10px 0;
}
#comments input[type="text"] {
  width:30%;
}
#comments .comment-meta {
  font-size:13px;
  line-height:28px;
  color:#999;
}
.cancel-comment-reply {
  line-height:1.48;
}
.comment-list {
  margin:10px 0 40px;
  padding:0;
}
input[type="submit"] {
  border:1px solid #888;
  background:#FFF;
  border-radius:3px;
  font-size:15px;
  cursor:pointer;
  outline:none;
  padding:7px 12px;
}
input[type="submit"]:focus,input[type="submit"]:hover {
  background:#666;
  color:#FFF;
}
input[type="text"] {
  outline:none;
  border-radius:3px;
  border:1px solid #EEE;
  font-size:15px;
  padding:7px 5px;
}
textarea {
  width:95%;
  min-height:160px;
  border:1px solid #EEE;
  border-radius:3px;
  outline:0;
  font-size:15px;
  padding:8px;
}
input[type="text"]:focus,textarea:focus {
  -webkit-transition:border-color .2s ease-in;
  border-color:#A5CFE7;
}
```

另外，我們在這邊順便將 input 與 textarea 的樣式做好。這樣，整個迴響區域就完成囉！恭喜！

目前文章迴響的地方長得像這樣：

![image023](/images/image023.jpg)




