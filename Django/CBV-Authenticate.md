# CBV Authenticate

```Python
from rest_framework.views import APIView
from rest_framework import exceptions


class MyAuthentication:
    def authenticate(self, request):
        token = request._request.GET.get('token')
        if not token:
            raise exceptions.AuthenticationFailed('Authentication failed')

    def authenticate_header(self, val):
        pass

class DogView(APIView):
    authentication_classes = [MyAuthentication, ]

    def get(self, *args, **kwargs):
        ret = {
            'code': 10000,
            'asg': 'xxx'
        }
        return HTTPResponse(json.dumps(ret), status=201)
```

URL -> DogView.as_view -> APIView.as_view -> csrf_exempt(view) -> View.dispatch

