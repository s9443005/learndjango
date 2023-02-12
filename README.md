# learndjango
## W3School學習筆記
### Django Tutorial漿果教學
#### Django漿果家
* 漿果是 a back-end server side web framework
* 漿果是 free, open source and written in Python
* 漿果是 makes it easier to build web pages using Python
* 漿果強調 DRY, Don't Repeat Yourself、資料庫為 CRUD 操作 Create Read Update Delete
#### Djang漿果運作 -- MVT架構(原文為pattern)
* Model -- Database，models.py
* View -- 來自 user 的 request，views.py
* Template -- HTML，在HTML裡嵌入「變數」
* URLs -- urls.py
#### Django漿果啟動--虛擬環境、安裝Django、建立專案、啟用網站
* 以下文字陳述並不完美，步驟或指令或提示，必須要有點想像力...
* 查看版本 ```python --version```，例如```python 3.6.12```
* 查看版本 ```pip --version```，例如```pip 21.2.4 from c:\python39\lib\site-packages\pip (python 3.9)```
* 為每個 Django 專案建立各自的 Virtual Environment 虛擬環境
* 建立虛擬環境 ```py -m venv myworld```，然後```dir/s myworld```一下。```?```己經建立了咋辦
* 啟用環境 ```myworld\Scripts\activate.bat```，會看到提示符號變成了```(myworld)(base)C:\...\myworld\Scripts>```
* 安裝Django```(myworld)(base)C:\...\myworld\Scripts>py -m pip install Django```
* 查看版本```django-admin --version```，例如```4.1.6```
* 回到```myworld```目錄，建立一個新專案```my_tennis_club```，這樣下指令```django-admin startproject my_tennis_club```
* 會自動建立一個目錄系統，用```dir/s```去看看目錄結構
* 厲害了，在```/my_tennis_club目錄```，啟動WEB Server，會看到一些說明...
* 打開瀏覽器，```http://127.0.0.1:8000```，畫面像這樣，[點我](https://www.w3schools.com/django/screenshot_django1.png)
#### 建立 APP(Application)、View，URLs，Template，和Models
* App的意義 -- 在專案裡，APP例如是一個 home page、一個conact form、或是一個member database
* 停止伺服器```用Ctrl-Break```，建立一個APP，指令像這樣```py manage.py startapp members```，注意：要在正確的目錄底下。
* 看看產生的目錄系統。
* 找到在my_tennis_club/members/views.py，用記事本或任何編輯器打開看到：
```
from django.shortcuts import render
# Create your views here.
```
修改成
```
from django.shortcuts import render
from django.http import HttpResponse
def members(request):
    return HttpResponse("Hello world!")
```
以上的例子是伺服器送出回應給瀏覽器，想要執行view的話，還得透過呼叫call a URL。
* 和views.py同一個目錄```my_tennis_club/members/urls.py```，建立urls.py，指定給members（看內容的指定方式），內容如下：
```
from django.urls import path
from . import views

urlpatterns = [
    path('members/', views.members, name='members'),
]
```
＊令人混淆的是（至少旺旺這麼覺得），我們還必須在my_tennis_club（根目錄所在），也建立一個urls.py，先照做。
```my_tennis_club/my_tennis_club/urls.py```
```
from django.contrib import admin
from django.urls import include, path

urlpatterns = [
    path('', include('members.urls')),
    path('admin/', admin.site.urls),
]
```
* 然後到```/my_tennis_club```，執行```py manage.py runserver```啟動WEB Server
* 打開瀏覽器，```http://127.0.0.1:8000/members/```，畫面像這樣，[點我](https://www.w3schools.com/django/screenshot_django_hello_world.png)
