
# Point Addition 2

### Test Driven Exercise

#### Add case 3 to the `__add__` method in your library:


```python
from ecc import Point

class Point(Point):

    def __add__(self, other):
        if self.a != other.a or self.b != other.b:
            raise RuntimeError('Points {}, {} are not on the same curve'.format(self, other))
        # Case 0.0: self is the point at infinity, return other
        if self.x is None:
            return other
        # Case 0.1: other is the point at infinity, return self
        if other.x is None:
            return self

        # Case 1: self.x == other.x, self.y != other.y
        # Result is point at infinity
        if self.x == other.x and self.y != other.y:
        # Remember to return an instance of this class:
        # self.__class__(x, y, a, b)
            return self.__class__(None, None, self.a, self.b)
 
        # Case 2: self.x != other.x
        if self.x != other.x:
        # Formula (x3,y3)==(x1,y1)+(x2,y2)
        # s=(y2-y1)/(x2-x1)
            s = (other.y - self.y) / (other.x - self.x)
        # x3=s**2-x1-x2
            x = s**2 - self.x - other.x
        # y3=s*(x1-x3)-y1
            y = s*(self.x-x) - self.y
        # Remember to return an instance of this class:
        # self.__class__(x, y, a, b)
            return self.__class__(x, y, self.a, self.b)

        # Case 3: self.x == other.x, self.y == other.y
        else:
        # Formula (x3,y3)=(x1,y1)+(x1,y1)
        # s=(3*x1**2+a)/(2*y1)
            s = (3*self.x**2 + self.a) / (2*self.y)
        # x3=s**2-2*x1
            x = s**2 - 2*self.x
        # y3=s*(x1-x3)-y1
            y = s*(self.x-x) - self.y
        # Remember to return an instance of this class:
        # self.__class__(x, y, a, b)
            return self.__class__(x, y, self.a, self.b)
```
