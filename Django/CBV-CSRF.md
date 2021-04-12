# CBV CSRF

`https://stackoverflow.com/questions/27315592/csrf-exempt-does-not-work-on-generic-view-based-class/38498887`

You need to decorate the dispatch method for csrf_exempt to work. What it does is set an csrf_exempt attribute on the view function itself to True, and the middleware checks for this on the (outermost) view function. If only a few of the methods need to be decorated, you still need to use csrf_exempt on the dispatch method, but you can use csrf_protect on e.g. put(). If a GET, HEAD, OPTIONS or TRACE HTTP method is used it won't be checked whether you decorate it or not.

```Python
class ChromeLoginView(View):
    @method_decorator(csrf_exempt)
    def dispatch(self, request, *args, **kwargs):
        return super(ChromeLoginView, self).dispatch(request, *args, **kwargs)

    def get(self, request):
        return JsonResponse({'status': request.user.is_authenticated()})

    def post(self, request):
        username = request.POST['username']
        password = request.POST['password']
        user = authenticate(username=username, password=password)
        if user is not None:
            if user.is_active:
                login(request, user)
                return JsonResponse({'status': True})
        return JsonResponse({'status': False})
```
