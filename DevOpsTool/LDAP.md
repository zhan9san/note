# LDAP

```Bash
export DJANGO_SECRET_KEY='xxx'

export AUTH_LDAP_SERVER_URI='ldap://x.x.x.x:636'

export AUTH_LDAP_BIND_DN='CN=xxx,OU=xxx,OU=xxx,DC=xxx,DC=xxx,DC=com'
export AUTH_LDAP_BIND_PASSWORD='xxx'

export AUTH_LDAP_USER_SEARCH_BASE_DN='DC=xxx,DC=xxx,DC=xxx'
export AUTH_LDAP_USER_SEARCH_FILTER='(&(!(userAccountControl=xxx))(objectCategory=xxx)(objectClass=xxx)(sAMAccountName=%(user)s))'

export AUTH_LDAP_GROUP_SEARCH_BASE_DN='OU=xxx,DC=xx,DC=xxx,DC=com'
export AUTH_LDAP_GROUP_SEARCH_FILTER='(objectClass=group)'
```

```Python
# Baseline configuration.
AUTH_LDAP_SERVER_URI = env("AUTH_LDAP_SERVER_URI")

AUTH_LDAP_BIND_DN = env("AUTH_LDAP_BIND_DN")
AUTH_LDAP_BIND_PASSWORD = env("AUTH_LDAP_BIND_PASSWORD")

AUTH_LDAP_USER_SEARCH_BASE_DN = env("AUTH_LDAP_USER_SEARCH_BASE_DN")
AUTH_LDAP_USER_SEARCH_FILTER = env("AUTH_LDAP_USER_SEARCH_FILTER")

AUTH_LDAP_USER_SEARCH = LDAPSearch(
    AUTH_LDAP_USER_SEARCH_BASE_DN,
    ldap.SCOPE_SUBTREE,
    AUTH_LDAP_USER_SEARCH_FILTER,
)

AUTH_LDAP_GROUP_SEARCH_BASE_DN = env("AUTH_LDAP_GROUP_SEARCH_BASE_DN")
AUTH_LDAP_GROUP_SEARCH_FILTER = env("AUTH_LDAP_GROUP_SEARCH_FILTER")
# Set up the basic group parameters.
AUTH_LDAP_GROUP_SEARCH = LDAPSearch(
    AUTH_LDAP_GROUP_SEARCH_BASE_DN,
    ldap.SCOPE_SUBTREE,
    AUTH_LDAP_GROUP_SEARCH_FILTER,
)

AUTH_LDAP_GROUP_TYPE = GroupOfNamesType(name_attr='cn')

AUTH_LDAP_MIRROR_GROUPS = True

# Populate the Django user from the LDAP directory.
AUTH_LDAP_USER_ATTR_MAP = {
    'first_name': 'givenName',
    'last_name': 'sn',
    'email': 'mail',
}

AUTH_LDAP_ALWAYS_UPDATE_USER = True

# Use LDAP group membership to calculate group permissions.
AUTH_LDAP_FIND_GROUP_PERMS = True

# Cache distinguished names and group memberships for an hour to minimize
# LDAP traffic.
AUTH_LDAP_CACHE_TIMEOUT = 3600

LOGGING = {
    "version": 1,
    "disable_existing_loggers": False,
    "handlers": {"console": {"class": "logging.StreamHandler"}},
    "loggers": {"django_auth_ldap": {"level": "DEBUG", "handlers": ["console"]}},
}
```
