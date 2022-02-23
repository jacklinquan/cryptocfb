# cryptocfb
A Python module to encrypt and decrypt data with AES-128 CFB mode.

## Installation
`pip install cryptocfb`

## Usage
``` python
>>> from cryptocfb import CryptoCFB
>>>
>>> key = b'0123456789abcdef'
>>> iv = bytes(reversed(key))
>>> cfb = CryptoCFB(key, iv)
>>>
>>> plain = b'This is a long message that needs to be encrypted.'
>>> cipher = cfb.encrypt(plain)
>>> cipher
bytearray(b"_#\xbf\x02\xd6\x19\x0c)\xd9\x18\xaf\xb9\xa4{JP\xf6j\xa3\xb2\xb2\xc6b\x9f\xae\x82\xa5\xd4\xaeen\xde\x12\x16\xfb\xf6\x079\x83\xd2\xbdC\'\x93\x9e\xc3\xeb\xc7\x03\x82")
>>> len(plain)
50
>>> len(cipher)
50
>>> cfb.reset_vector()
>>>
>>> cfb.decrypt(cipher)
bytearray(b'This is a long message that needs to be encrypted.')
>>> cfb.reset_vector()
>>>
>>> ba = bytearray(plain)
>>> ba1 = ba[0:16]
>>> ba2 = ba[16:32]
>>> ba3 = ba[32:48]
>>> ba4 = ba[48:64]
>>> cfb.crypt_inplace(ba1)
bytearray(b'_#\xbf\x02\xd6\x19\x0c)\xd9\x18\xaf\xb9\xa4{JP')
>>> cfb.crypt_inplace(ba2)
bytearray(b'\xf6j\xa3\xb2\xb2\xc6b\x9f\xae\x82\xa5\xd4\xaeen\xde')
>>> cfb.crypt_inplace(ba3)
bytearray(b"\x12\x16\xfb\xf6\x079\x83\xd2\xbdC\'\x93\x9e\xc3\xeb\xc7")
>>> cfb.crypt_inplace(ba4)
bytearray(b'\x03\x82')
>>> cfb.reset_vector()
>>>
>>> cfb.crypt_inplace(ba1, False)
bytearray(b'This is a long m')
>>> cfb.crypt_inplace(ba2, False)
bytearray(b'essage that need')
>>> cfb.crypt_inplace(ba3, False)
bytearray(b's to be encrypte')
>>> cfb.crypt_inplace(ba4, False)
bytearray(b'd.')
>>> cfb.reset_vector()
>>>
>>> ba
bytearray(b'This is a long message that needs to be encrypted.')
>>> cfb.crypt_inplace(ba)
bytearray(b"_#\xbf\x02\xd6\x19\x0c)\xd9\x18\xaf\xb9\xa4{JP\xf6j\xa3\xb2\xb2\xc6b\x9f\xae\x82\xa5\xd4\xaeen\xde\x12\x16\xfb\xf6\x079\x83\xd2\xbdC\'\x93\x9e\xc3\xeb\xc7\x03\x82")
>>> len(ba)
50
>>> ba.extend(bytearray(14))
>>> ba
bytearray(b"_#\xbf\x02\xd6\x19\x0c)\xd9\x18\xaf\xb9\xa4{JP\xf6j\xa3\xb2\xb2\xc6b\x9f\xae\x82\xa5\xd4\xaeen\xde\x12\x16\xfb\xf6\x079\x83\xd2\xbdC\'\x93\x9e\xc3\xeb\xc7\x03\x82\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00")
>>> cfb.reset_vector()
>>>
>>> cfb.crypt_inplace(ba, False)
bytearray(b'This is a long message that needs to be encrypted.d\xd5\x99vk\x08\x1c\x82\xf0_\xb8\x8aw\x85')
>>> cfb.reset_vector()
```
