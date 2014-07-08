在 sidebar.php 中，我們可以放置一些如相關文章、搜尋等等模組讓訪客有需求時去使用。而 sidebar.php 的寫法非常簡單，甚至在 sidebar.php 中只要三行。不過，我們得另外在 functions.php 中先去註冊模組，這樣你就可以在控制台的外觀 > 模組中去新增模組，之後在 sidebar.php 中被顯示出來。

## 註冊模組

如果你現在去控制台的外觀裡面，你會看不到模組選單。是的，因為我們要先告訴系統我們要使用這個功能，也就是註冊一個模組。所以，請將下面的代碼加入 functions.php。


```
if ( function_exists('register_sidebar') ){
    register_sidebar(array(
        'name' => '側邊欄',
        'id' => 'sidebar',
        'description' => '顯示於每個網頁的右方。',
        'before_widget' => '<section id="%1$s" class="sidebar-right">',
        'after_widget' => '</section>',
        'before_title' => '<h1 class="sidebar-title">',
        'after_title' => '</h1>'
    ));
}
```

函式及參數說明：

- register_sidebar() － 註冊選單之函式。
- 'name' － 模組名稱。
- 'id' － 模組 ID。
- 'description' －模組說明。
- 'before_widget' － 在模組前的標籤。
- 'after_widget' － 模組後的標籤。
- 'before_title' － 模組名稱前的標籤。
- 'after_title' － 模組名稱後的標籤。

## 顯示於 sidebar.php 上

註冊完模組之後，你可以先在裡面新增幾個如最新文章、搜尋，這樣才會東西輸出：


![image020](/images/image020.jpg)

接著，我們在 sidebar.php 加入以下代碼：

```
<aside id="sidebar">
    <?php dynamic_sidebar('sidebar'); ?>
</aside>
```

接著，在 style.css 加入一些樣式碼吧！

```
.sidebar-right {
  background:#FFF;
  margin:30px 0;
  padding:10px 15px;
}
.sidebar-title {
  font-size:24px;
  line-height:1.8;
  color:#666;
  margin:10px 0;
}
```

現在，整個網頁長成這樣：

![image021](/images/image021.jpg)
