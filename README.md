# 《编写高质量代码——改善Python程序的91个建议》

[幕布读书笔记](https://share.mubu.com/doc/3XgcyfK0sf)

## 基本原则

### 7. 将常量集中到一个文件

方案二代码

const.py
```python
class _const:
    class ConstError(TypeError): pass
    class ConstCaseError(ConstError): pass

    def __setattr__(self, key, value):
        if key in self.__dict__:
            raise self.ConstError("Can't change const.{key}".format(key=key))
        if not key.isupper():
            raise self.ConstCaseError(
                'const name "{key}" is not all uppercase'.format(key=key))
        self.__dict__[key] = value


import sys
sys.modules[__name__] = _const()
```

定义常量的地方

```python
import const

const.LANGUAGE = "Python"
```
