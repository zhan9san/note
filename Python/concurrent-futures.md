# concurrent.futures

Exception will be raised in this kind of snippet.

```Python
with concurrent.futures.ThreadPoolExecutor(max_workers=2) as executor:
    for future in executor.map(load_url, URLS):
        pass
```

Exception will NOT be raised in this kind of snippet.

```Python
with concurrent.futures.ThreadPoolExecutor(max_workers=2) as executor:
    executor.map(load_url, URLS)
```

Another way to wirte it

```Python
with concurrent.futures.ThreadPoolExecutor(max_workers=2) as executor:
    futures = [executor.submit(load_url, item) for item in number_list]
    for future in concurrent.futures.as_completed(futures):
        print(future.exception())
```

<https://python-parallel-programmning-cookbook.readthedocs.io/zh_CN/latest/chapter4/02_Using_the_concurrent.futures_Python_modules.html>
