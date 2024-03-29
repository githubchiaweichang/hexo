---
title: Code review
date: 2018-07-31 00:30:19
tags:
---




# 代碼格式方面
很多公司都有 coding style guideline。大家的約定俗成，避免公司的代碼風格不一致，也避免一些不不要的為了「要不要把閉括號另起一行」而無謂地爭論，除非是不小心，通常大家都不會弄錯。但是新員工往往會在這方面還不太熟悉。這一類問題也比較容易指出。

# 代碼可讀性方面
這包括一個函數不要太長，太長就 break down。所有的變量名盡量能夠說明它的用意和類型。比如 hosting_address_hash，一看就知道是房東地址，而且是個 hash 類型。不要有嵌套太多層的條件語句或者循環語句。不要有一個太長的 boolean 判斷語句。如果一個函數，別人需要看你的長篇註釋才能明白，那這個函數就一定有重構的空間。另外，如果不可避免有一些註釋，則一定要保證註釋準確且與代碼完全一致。

幫代碼作者想想他/她有沒有漏掉任何 corner case
很多時候這是業務邏輯相關的，尤其需要比較老的工程師幫助指出需要處理的所有情況。

# Error handling
這是最常見也是代碼審核最容易幫別人看出的問題。舉個例子，下面一段簡單到不能再簡單的代碼就至少有三個潛在的問題：params 裡面需要 validate 是不是有 user_id 和 new_name 這兩個 key；能不能找到這個 user_id 對應的 user；save 的時候會不會有 DB level 的 exception，應該怎麼處理。


# 測試例和防坑
測試例不用說了，每段代碼都應該有測試例。但是對於一些你能預見如果別人改動代碼會引起可能問題的情況，一定要額外的加測試例防止這種事情的發生。這一點沒有例子參考也不太好說。怎麼寫好測試例，本身就值得寫一篇文章了。

# 小架構
什麼意思呢，就是一個文件或者類內部的代碼組織。比如如果有重複的代碼段，就應該提取出來公用。不要在代碼裡隨意設常數，所有的常數都應該文件頂部統一定義。哪些應該是 private，等等

# 大架構
這個就更廣了。包括文件組織，函數是不是應該抽像到 lib 或者 helper 文件裡；是不是應該使用繼承類；是不是和整個代碼庫的風格一致，等等。

當然，視具體情況可能還有很多別的需要在 code review 中註意的。但是如果按照這個 checklist 過一遍，一些明顯的問題就可以避免個八九不離十了。

另外，代碼 review 和寫代碼是我們每個工程師都應該致力的兩個方面，缺一不可。可能在工作中的某個階段或者某個項目裡，你會花更多的時間在某一面，但長久看來，兩個技能缺一不可。

# 代碼審核是工作，不要抱有情緒化
我曾經幹過一件事，一個外組同事的代碼，別人已經 stamp 了，可是我覺得有問題，於是把 stamp revert 掉了，在 comments 裡寫了為什麼有問題，和建議的改法。當時心裡還有點覺得好像怪得罪人的。可是後來發現同事反而很客氣地接受並道謝了。心裡也是很感激有這樣的工作環境。

另外，經常會遇到有些 review 的 comments 裡出現不同意見，其實是兩個人在編程習慣和約定俗成上沒有共識。如果在不違背公司 style guideline 的情況下，沒必要一定讓對方和你有一樣的習慣。如果你真的覺得這樣更好，通常我也只會寫「I personally would prefer A over B, but no strong opinion.」或者「How about change it to A, since … However, this is not a merge blocker.」

人都有不周到的時候。多幾雙眼睛一起幫你看一遍，就可以很大程度地減少代碼裡的錯誤。另外， 相互 review 的過程中還能從彼此那裡學到很多編程的小技巧和好習慣 。細想來，很多 Java 和 Ruby 的特別好用的 feature，我都是在 code review 的過程中學到的。



[Airbnb 資深工程師分享：怎樣才是正確、有效的 code review]:https://buzzorange.com/techorange/2016/08/16/airbnb-code-review/
[美國碼農加班少很多、卻能開發出厲害的產品？讓亞馬遜工程師告訴你：會議就是生產力]:https://www.inside.com.tw/2018/05/03/amazon-sde-process