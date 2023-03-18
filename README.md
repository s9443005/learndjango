# LEARNING Django漿果學習筆記
## W3School學習筆記
### Django Tutorial漿果教學
#### Django漿果家
* 漿果是 a back-end server side web framework
* 漿果是 free, open source and written in Python
* 漿果是 makes it easier to build web pages using Python
* 漿果強調 DRY, Don't Repeat Yourself、資料庫為 CRUD 操作 Create Read Update Delete
#### Djang漿果運作 -- MVT架構(原文為 MVT pattern)
* Model -- Database以及Table，Model相當於DB裡的Table，在 models.py 裡設定
* View -- 來自 user 的 request，在 views.py 裡設定
* Template -- HTML，在HTML裡嵌入「Django變數」，經「Django解釋」後產生 HTML，由 HttpResponse 傳給瀏覽器。
* URLs -- urls.py
#### Django漿果 
* 設定虛擬環境
* 安裝Django
* 新增專案 C:\...>django-admin startproject XXXproject
* 啟動網站 C:\...>py manage.py runserver <----------------http://127.0.0.1:8000
* 新增專案裡的應用系統 C":\...>py manage.py startapp XXXapp <------------檢視一下目錄結構
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
#### 建立 Django APP(Application)、Django View
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

* 令人混淆的是（至少旺旺這麼覺得），我們還必須在my_tennis_club（根目錄所在），也建立一個urls.py，先照做。

```my_tennis_club/my_tennis_club/urls.py```，不要懷疑，在這個目錄底下
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
* 回顧比較一下，我們到這裡有2次從瀏覽器去連伺服器，分別是

    + ```http://127.0.0.1:8000/```
    + ```http://127.0.0.1:8000/members/```

一個是直接連根目錄，另一個連接叫另外的目錄執行特定的功能，這個叫做render，翻譯有很多種，其中以翻成```渲染```我覺得最有趣。
#### 建立 Django Template，
* 用```dir/s```查看目錄系統，在```my_tennis_club/my_tennis_club/members/template目錄```下建立```myfirst.html```，內容如下
```
<!DOCTYPE html>
<html>
<body>

<h1>Hello World!</h1>
<p>Welcome to my first Django project!</p>

</body>
</html>
```
* 接著要做2個檔案的修改，分別是```my_tennis_club/members/views.py```和```my_tennis_club/my_tennis_club/settings.py```
* 修改```views.py```內容成為：
```
from django.http import HttpResponse
from django.template import loader

def members(request):
  template = loader.get_template('myfirst.html')
  return HttpResponse(template.render())
```
* 修改```settings.py```內容成為：(我的python版本是使用雙引號，W3School範例是單引號，應該沒差；實作時我還單雙混用咧。)
```
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'members'
]
```
* 叫網頁也和前面有一點不同哦

```py manage.py migrate``` 

```py manage.py runserver``` 

* 打開瀏覽器，```http://127.0.0.1:8000/members/```，畫面像這樣，[點我](https://www.w3schools.com/django/screenshot_django_template_myfirst.png)
* 回顧比較一下，我們到這裡有2次從瀏覽器```http://127.0.0.1:8000/members/```去連伺服器，1次是純python程式，1次是使用Template（就myfirst.html檔）。這意味著你可以使用另外的HTML+CSS+JavaScript，運用你原本熟悉的能力。
#### 建立 Django Models
* Django Model是指資料庫database裡的1張表格table
* 找到```my_tennis_club/members/models.py```，修改成：
```
from django.db import models

class Member(models.Model):
  firstname = models.CharField(max_length=255)
  lastname = models.CharField(max_length=255)
```
* 以上內容屬於資料庫管理系統的內容，同學被假定己有一定基礎
* 當我們建立了Django project時，就產生了一個空的 SQLite 資料庫，它位於my_tennis_club根資料夾，其檔名為db.sqlite3，表格會存在裡面
* 以指令```py manage.py makemigrations members```執行後，真正去產生表格。讀一下回饋報表。
* W3School接著去研究了```my_tennis_club/members/migrations/0001_initial.py```，內容也不錯，這裡先跳過。
* 是出爾反爾嗎，還要下一個指令，表格才會真正產生：```py manage.py migrate```。讀一下回饋報表。
* 此時此刻，資料庫裡才有張Member表格。
* 接下來 View SQL，我不太理解
```py manage.py sqlmigrate members 0001```，讀一下回饋報表，看起來是DML新增表格的指令。
#### Django 新增、修改、刪除、查詢
##### 新增
* 新增一筆記錄Record，這過程同學瞭解嗎？或者必須逐行解釋？
```
py manage.py shell
Python 3.9.2 (tags/v3.9.2:1a79785, Feb 19 2021, 13:44:55) [MSC v.1928 64 bit (AMD64)] on win32
Type "help", "copyright", "credits" or "license" for more information.
(InteractiveConsole)
>>>
>>> from members.models import Member
>>> Member.objects.all()
<QuerySet []>
>>> member = Member(firstname='Emil', lastname='Refsnes')
>>> member.save()
>>> Member.objects.all().values()
<QuerySet [{'id': 1, 'firstname': 'Emil', 'lastname': 'Refsnes'}]>
```
* 新增多筆記錄如下，我發現跟傳統的DML還是有點不同的，而且實作畫面和W3School有些許不同
```
>>> member1 = Member(firstname='Tobias', lastname='Refsnes')
>>> member2 = Member(firstname='Linus', lastname='Refsnes')
>>> member3 = Member(firstname='Lene', lastname='Refsnes')
>>> member4 = Member(firstname='Stale', lastname='Refsnes')
>>> member5 = Member(firstname='Jane', lastname='Doe')
>>> members_list = [member1, member2, member3, member4, member5]
>>> for x in members_list:
>>>   x.save()
>>> Member.objects.all().values()
<QuerySet [{'id': 1, 'firstname': 'Emil', 'lastname': 'Refsnes'},
{'id': 2, 'firstname': 'Tobias', 'lastname': 'Refsnes'},
{'id': 3, 'firstname': 'Linus', 'lastname': 'Refsnes'},
{'id': 4, 'firstname': 'Lene', 'lastname': 'Refsnes'},
{'id': 5, 'firstname': 'Stale', 'lastname': 'Refsnes'},
{'id': 6, 'firstname': 'Jane', 'lastname': 'Doe'}]>
```
##### 修改
##### 刪除
#### 修改MODEL
