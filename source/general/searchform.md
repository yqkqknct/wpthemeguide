Searchform.php 顧名思義就是搜尋的表單，沒錯，我們現在就要來製作搜尋的表單囉！

由於 WordPress 內建的搜尋表單不是很好，在搜尋框之前還有一個「搜尋：」，不是很好看，所以我們可以使用 searchform.php 來更換搜尋表單的格式。

這是原本 WordPress 內建的搜尋表單：

![image024](/images/image024.jpg)

使用 searchform.php 修改之後：

![image025](/images/image025.jpg)

是不是變得比較好看了呢？要達成這樣的效果，就在 searchform.php 加入下面的代碼就可以了：

```
<form role="search" method="get" id="searchform" action="<?php echo home_url( '/' ); ?>">     <input type="text" value="" name="s" id="s" placeholder="搜尋..." />
    <input type="submit" id="searchsubmit" value="搜尋" />
</form>
```

其中，placeholder 就是在上圖的表單中提示搜尋… 的字樣那個。
這樣，搜尋表單就完成囉！
