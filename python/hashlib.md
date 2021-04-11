## hashlib

- hashlib是一个提供字符串加密功能的模块，包含MD5和SHA的算法，MD5和SHA是摘要算法。

- md5是最常见的摘要算法，速度快，加密强度不高，生成的结果是固定的128bit字节，通常用一个32位的16进制字符串表示。

- 也称哈希算法，离散算法。通过一个函数将任意长度的数据转化为一个长度固定的数据串，摘要函数是一个单向函数，计算f(data)很容易，但是通过digest反推data非常困难。

    - 生成了一个md5对象
    
    - 对数据进行编码，否则报错
    
    - 获取digest