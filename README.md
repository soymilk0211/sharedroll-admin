# Shared Roll 管理後台

產品負責人自己用的小網頁:發兌換碼、改房間張數。網址是
<https://soymilk0211.github.io/sharedroll-admin/>。

## 這個 repo 是公開的,而它不該讓任何人多做得了一件事

`index.html` 裡有三個常數:Supabase 專案網址、publishable key、Google web client id。三個
**本來就都是公開的**——App 的 `app.json` 裡也是明文,而且跟著安裝檔散到每一支手機上。它們
**識別**專案,不**授權**任何事。

真正的門在資料庫:每一支 admin RPC 第一件事都是問 `is_admin()`,而 `admins` 那張表 RLS 開著
卻一條政策都不給,對 client 角色等於不存在。把這個網址貼給別人,他看到的是一個登入畫面;
登進去之後看到的是「這個帳號還不是管理員」。

**所以這裡絕不可以出現 App Secret、service role key、綠界的 HashKey/HashIV,或任何 `sb_secret_`
開頭的東西。** 那些一旦進來,這個 repo 是公開的這件事就會變成一個真的洞。

## 原始碼在哪裡

主 repo(`soymilk0211/SharedRoll`,私有)的 `admin/index.html` 才是真正的那一份,連同伺服器
那一側的遷移與測試。這個 repo 只是把它推上 GitHub Pages 的地方——**改請改主 repo,再同步過來**,
不要在這裡直接改,不然兩邊會漂開。

相關:主 repo 的 #74(這張票)、#88(同一條平台規則也打到綠界付款頁)。
