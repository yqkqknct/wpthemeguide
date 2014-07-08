footer.php 這一個檔案通常是拿來放一些版權資訊等等不屬於主要內容的資訊。而這個檔案同樣要把整個 HTML 標籤還尚未關閉的做一個適當的關閉，如 .container，要在 footer.php 將它關閉。

## 基本格式 － 將未關閉的標籤關閉

在 header.php 中，有些標籤是還沒有關閉的。而這些標籤我們要在 footer.php 將它關閉，這樣才算一份語法正確又好的網頁。在 footer.php 加入以下代碼：

```
        <footer class="footer">
        </footer>
    </div>
    <?php wp_footer(); ?>
</body>
</html>

```

- bloginfo() － 參數若為 url 則輸出網站網址；若為 name 則輸出網站名稱。
- wp_footer() － 若有登入，在網站中每個頁面的最上面都會有一條黑色的控制條。此函式即為載入該條之函式。最後，我們將 body 與 html 一同關閉。

## 加入版權資訊

另外，在網頁底部幾乎每個網站都會放置版權資訊，有時候也有放聯絡資料。而
在這邊我們會在 footer.php 放上網站的版權資訊。在 footer.php 的 `<footer class="footer">` 後加上：

```
<div class="copyright">Copyright © 2013 <a href="<?php bloginfo("url"); ?>"><?php bloginfo("name"); ?></a></div>
```

接著，為這些 HTML 標籤加上一些 CSS 吧！

```

.footer {
  float:left;
  margin:0 30px 15px;
  padding:20px;
}

.copyright {
  color:#888;
  font-size:13px;
}

.copyright a {
  color:#666;
  text-decoration:none;
}

.copyright a:hover {
  color:#666;
  text-decoration:underline;
}
```

最後，打開瀏覽器 localhost，你會看到 footer 乖乖的在網站的最底部！

![image019](/images/image019.jpg)
