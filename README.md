# learndjango
## W3School學習筆記 D
### Django Tutorial漿果教學
#### Django家
* 漿果是 a back-end server side web framework
* 漿果是 free, open source and written in Python
* 漿果是 makes it easier to build web pages using Python
* 漿果強調 DRY, Don't Repeat Yourself、資料庫為 CRUD 操作 Create Read Update Delete
#### Djang運作 -- MVT架構(pattern)漿果
* Model -- Database，models.py
* View -- 來自 user 的 request，views.py
* Template -- HTML，在HTML裡嵌入「變數」
* URLs -- urls.py
#### Django啟動
* 查看版本 ```python --version```，例如```python 3.6.12```
* 查看版本 ```pip --version```，例如```pip 21.2.4 from c:\python39\lib\site-packages\pip (python 3.9)```
* 為每個 Django 專案建立各自的 Virtual Environment 虛擬環境
* 建立專案 ```py -m venv myworld```，然後```dir/s myworld```一下。```?```己經建立了咋辦
* 啟用環境 ```myworld\Scripts\activate.bat```，會看到提示符號變成了```(myworld)(base)C:\...\myworld\Scripts>```
* 安裝Django```(myworld)(base)C:\...\myworld\Scripts>py -m pip install Django```
* 查看版本```django-admin --version```，例如```4.1.6```
* 回到```myworld```目錄，建立一個新專案```my_tennis_club```，這樣下指令``````
