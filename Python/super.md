# super

```Python
class A:
    def a(self):
        print('A-a')

    def b(self):
        self.a()

class B(A):
    def a(self):
        super(B, self).a()
        print('B-a')

    def b(self):
        super(B, self).b()
        self.a()

b = B()
b.b()

# Output:
# A-a
# B-a
# A-a
# B-a
```
