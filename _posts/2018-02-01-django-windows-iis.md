---
layout: default
title:  "django on windows with IIS"
date:   2018-02-01 15:12:16 -0700
categories: www
---

### 0. setup
Install ananconda to be the easiest, then
```
pip install wfastcgi
pip install django
wfastcgi-enable.exe
```

### 1. create the sherlock project
```
django-admin startproject sherlock
```

### 2. unlock the handlers
```
%windir%\system32\inetsrv\appcmd unlock config -section:system.webServer/handlers
```

### 3. set the physical path
```
%windir%\system32\inetsrv\appcmd set vdir "Default Web Site/" -physicalPath:"e:\www\sherlock"
```

### 4. create the views.py
```
from django.http import HttpResponse
def home(request):
    html = "<html><body>Elementary!</body></html>"
    return HttpResponse(html)

```

### 5. update urls.py
```
from django.conf.urls import url
import sherlock.views

urlpatterns = [
    url(r'^$', sherlock.views.home),
]
```

### 6. update web.config
create one if not existed yet
```
<configuration>
 <appSettings>
   <add key="WSGI_HANDLER" value="django.core.wsgi.get_wsgi_application()" />
   <add key="PYTHONPATH" value="e:\www\sherlock" />
   <add key="DJANGO_SETTINGS_MODULE" value="sherlock.settings" />
 </appSettings>
 <system.webServer>
   <handlers>
       <add name="Python FastCGI" path="*" verb="*" modules="FastCgiModule" scriptProcessor="e:\anaconda3\python.exe|e:\anaconda3\Lib\site-packages\wfastcgi.py" resourceType="Unspecified" />
   </handlers>
 </system.webServer>
</configuration>
```

### Last but not least
Mind the permission settings of the www folder and also the django package folder, ensure IIS_IUSER has both read and execute access.



[1]: https://docs.microsoft.com/en-us/azure/virtual-machines/windows/classic/python-django-web-app?toc=%2Fazure%2Fvirtual-machines%2Fwindows%2Fclassic%2Ftoc.json
