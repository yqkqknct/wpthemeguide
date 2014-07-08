很多網站會在文章 More 標記處插入一個或兩個的 Google Adsense 廣告，而實現方法很簡單，我們只要利用拆字串的方法，把 More 標記的 HTML 找出來，在那邊插入廣告代碼就可以了！


```
function adsense_adder_at_more_tag($text) {
    if( is_single()) :
    $ads_text ='請將廣告代碼貼在這裡 ';
    $pos1 = strpos($text, '<span id="more-');
    $pos2 = strpos($text, '</span>', $pos1);
    $text1 = substr($text, 0, $pos2);
    $text2 = substr($text, $pos2); $text = $text1 . $ads_text . $text2; endif; return $text;
}
add_filter('the_content', 'adsense_adder_at_more_tag');
```

新增完，記得將「請將廣告代碼貼在這裡」替換成你的廣告代碼。這樣就完成囉！
