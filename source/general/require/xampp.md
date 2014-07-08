
在佈景開發過程中，我們可以有兩種方式：一是將 WordPress 裝在虛擬主機中，然後製作佈景的時候會一直不斷將檔案使用 FTP 上傳至虛擬主機；二是直接在自己的電腦中裝設 WordPress，這樣不但不需要每次都使用 FTP 上傳，而且只要打開瀏覽器輸入 http://localhost/ 就可以看到目前的開發狀態。之後開發完成後，再統一上傳到自己的虛擬主機就可以了。

沒錯，我們這次要使用的就是將 WordPress 安裝在自己的電腦，在自己的電腦中建立佈景主題，進行 WordPress 佈景主題世紀終極大開發。

我們要利用的工具是 XAMPP。XAMPP 是一個結合 Apache、PHP、PERL、 MySQL 的軟體，相當方便。

## XAMPP 基本介紹

- 正體中文首頁：http://www.apachefriends.org/zh_tw/index.html
- 分類下載頁面：http://www.apachefriends.org/zh_tw/xampp.html
- Windows 下載頁：http://www.apachefriends.org/zh_tw/xampp-windows.html
- Mac OSX 下載頁：http://www.apachefriends.org/zh_tw/xampp-macosx.html
- Linux 下載頁：http://www.apachefriends.org/zh_tw/xampp-linux.html

## Windows 安裝說明

進到 Windows 下載頁。如下圖，你可以點擊「自動安裝程式」、「ZIP」或「7zip」進行 XAMPP 的下載。如果你對免安裝程式不熟悉，推薦你使用「自動安裝程式」版本；若您熟悉，推薦選擇「7zip」版本，下載快且不留痕跡。

![image003](/images/image003.jpg)

打開你安裝 XAMPP 的目錄。往下拉，你會看到一個「xampp-control.exe」，將它打開，你會看到管理各項服務開啟的介面。

> 注意：如果你使用的是 ZIP 或 7-zip 版本，在開啟 xampp-control.exe 之前請先執行 setup_xampp.bat，再開啟 xampp-control.exe，才能正常開啟各項服務。

![image005](/images/image005.jpg)

開啟 xampp-control.exe 之後，要安裝 WordPress，我們必須將 Apache 及 MySQL 這兩項服務開啟，只要按一下 Start 即可。如下圖，為開啟狀態。

![image006](/images/image006.jpg)

> 注意：某些程式可能會擋住 Apache 使用的 80port，如 Skype，若發生請關掉占用 80port 的程式或修改其設定。

## XAMPP 網站目錄

XAMPP 存放網站檔案的地方在「htdocs」資料夾。

你現在可以打開瀏覽器，並且輸入「http://localhost」或「http://127.0.0.1」，你講會看到以下頁面：

![image008](/images/image008.jpg)

現在，你可以看一下關於 XAMPP 的各項資訊。或者，你可以打開 htdocs 目錄，開始安裝 WordPress。安裝步驟與一般安裝方式一樣，你需要先打開phpMyAdmin （http://localhost/phpmyadmin），並新增資料庫。如下圖：

![image009](/images/image009.jpg)

接著，你需要到 WordPress 官網下載最新的 WordPress。下載完後，將完整檔案放至 htdocs 資料夾內。如下圖：

![image010](/images/image010.jpg)

接著，打開 http://localhost/wordpress/ 即可開始安裝。另外，安裝過程中的資料庫帳號及密碼，帳號預設為 root，密碼預設為空。（有修改請填你修改後的）。資料庫名稱請填上一張圖片中新建數據庫你填的資料庫名稱。

最後安裝成功後會進到 WordPress 的控制台。如果你能夠進去，這樣初始的本機開發環境就算完成了，恭喜完成成就十分之一。

