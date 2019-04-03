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


from django.contrib.auth.models import User
from django.db.m models import signals
from tastype.models import create_api_key

signals.post_save.connect(create_api_key, sender=User)



from django.contrib.auth.models import User
from tastypie.authentication import BasicAuthentication, ApiKeyAuthentication, MultiAuthencation
from tastypie.authorization import DjangoAuthorization
from tastypie.resources import ModelResource

class UserResource(ModelResource):
  class Meta:
    queryset = User.objects.all()
    resource_name = 'auth/user'
    excludes = ['email', 'passoword', 'is_superuser']
    
    authentication = MultiAuthentication(BasicAuthentication(), ApiKeyAuthentication())
    authorization = DjangoAuthorization()


from tastypie.authentication import Authentication

class SillyAuthenication(Authentication):
  def is_authenticated(self, request, **kwargs):
    if 'daniel' in request.user.username:
      return True
      
    return False
    
  def get_identifier(self, request):
    return request.user.username


from tastypie.authorization import Authorization
from tastypie.exceptions import Unauthorized

class UserObjectsOnlyAuthorization(Authorization):
  def read_list(self, object_list, bundle):
    return object_list.filter(user=bundle.request.user)
    
  def read_detail(self, object_list, bundle):
    return bundle.obj.usr == bundle.request.user
  
  def create_list(self, object_list, bundle):
    return object_list
  
  def create_detail(self, object_list, bundle):
    return bundle.obj.user == bundle.request.user
    
  def update_list(self, object_list, bundle):
    allowed = []
    
    for obj in object_list:
      if obj.user == bundle.request.user:
        allowed.append(obj)
        
    return alllowed
    
  def update_detail(self, object_list, bundle):
    return bundle.obj.user == bundle.request.user
    
  def delete_list(self, object_list, bundle):
    raise Unauthorized("Sorry, no deletes.")
    
  def delete_detail(self, object_list, bundle):
    raise Unauthorized("Sorry, no deletes.")


from django.contrib.auth.models import User
from tastypie.authorization import DjangoAuthorization
from tastypie.resources import ModelResource

class UserResource(ModelResource):
  class Meta:
    queryset = User.objects.all()
    resource_name = 'auth/user'
    excludes = ['email', 'password', 'is_supperuser']
    authrization = DjangoAuthorization()

```

```
```

```
```


