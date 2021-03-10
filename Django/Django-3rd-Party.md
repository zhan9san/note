# Django 3rd party

## registration using Custom User model

`django_registration/registration_form.html` is required for `'accounts/register/'` url.
[RegistrationView](https://github.com/ubernostrum/django-registration/blob/3.1/src/django_registration/views.py)

```Python
    path('accounts/register/',
        RegistrationView.as_view(
            form_class=CustomUserForm,
            success_url="/",
        ),
        name='django_registration_register',
    ),
```

## one-step user registration

```Python
    path("accounts/", include("django_registration.backends.one_step.urls")),
```

```Python
    path(
        "register/",
        views.RegistrationView.as_view(),
        name="django_registration_register",
    ),
    path(
        "register/closed/",
        TemplateView.as_view(
            template_name="django_registration/registration_closed.html"
        ),
        name="django_registration_disallowed",
    ),
    path(
        "register/complete/",
        TemplateView.as_view(
            template_name="django_registration/registration_complete.html"
        ),
        name="django_registration_complete",
    ),
```

## built-in auth method

```Python
    path("accounts/", include("django.contrib.auth.urls")),
```

`registration/login.html` is required for `'login/'` url referring to `django/contrib/auth/views.py`

```Python
    path('login/', views.LoginView.as_view(), name='login'),
    path('logout/', views.LogoutView.as_view(), name='logout'),

    path('password_change/', views.PasswordChangeView.as_view(), name='password_change'),
    path('password_change/done/', views.PasswordChangeDoneView.as_view(), name='password_change_done'),

    path('password_reset/', views.PasswordResetView.as_view(), name='password_reset'),
    path('password_reset/done/', views.PasswordResetDoneView.as_view(), name='password_reset_done'),
    path('reset/<uidb64>/<token>/', views.PasswordResetConfirmView.as_view(), name='password_reset_confirm'),
    path('reset/done/', views.PasswordResetCompleteView.as_view(), name='password_reset_complete'),
```

## DRF auth

```Python
    path("api-auth/", include("rest_framework.urls")),
```

```Python
    path('login/', views.LoginView.as_view(template_name='rest_framework/login.html'), name='login'),
    path('logout/', views.LogoutView.as_view(), name='logout'),
```

==Duplicate login method/url between build-in auth and DRF auth?==
