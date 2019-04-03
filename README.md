### django-tastypie
---
http://tastypieapi.org/

https://django-tastypie.readthedocs.io/en/latest/api.html

```py
from django.conf.urls import url, include
from tastypie.api import Api
from myapp.api.resources import UserResource, EntryResource

v1_api = Api(api_name='v1')
v1_api.register(UserResource())
v1_api.register(EntryResource())

urlpaterns = [
  url(r'^api/', include(v1_api.urls)),
]



from django.contrib.auth.models import User
from tastypie.authentication import BasicAuthentication
from tastype.resources import ModelResource

class UserResource(ModelResource):
  class Meta:
    queryset = User.objects.all()
    resource_name = 'auth/user'
    excludes = ['email', 'password', 'is_superuser']
    authentication = BasicAuthentication()

```

```
```

```
```


