# Character Encoding

> Character encoding is the process of assigning numbers to graphical characters, especially the written characters of
> human language, allowing them to be stored, transmitted, and transformed using digital computers.
>
> \- [Wikipedia](https://en.wikipedia.org/wiki/Character_encoding)

## ASCII

ASCII (American Standard Code for Information Interchange) is one of the most common character encoding schema. It
encodes 128 specified characters into 7-bit integers. The specified characters include both printable (e.g. digits and
alphabets) and non-printable (e.g. tab and line feed) characters.

Later on, the extended ASCII was defined. It extends the original schema by using 8-bit for encoding. Therefore, the
extended ASCII encodes 256 characters in total.

## Unicode

Unicode itself is **NOT** a character encoding scheme. Unicode is a standard to map the characters into the "code points",
which could be encoded into the binary format by different character encoding schemes.

A code point is represented by a leading "U+" and the subsequent hexadecimal value from 0000 to 10FFFF. The code points
are then devided into 10 (in hex), or 17 (in decimal) code planes.

```
  U+0000 -   U+FFFF
 U+10000 -  U+1FFFF
         .
         .
         .
 U+F0000 -  U+FFFFF
U+100000 - U+10FFFF
```

### UTF-8

UTF-8 (Unicode Transformation Format – 8-bit) is the most common encoding on the web. It encodes the unicode characters
(i.e. unicode code points) into 1 - 4 bytes of binary data.

Since the first 128 unicode code points represent the ASCII characters, and are encoded as 1 byte in UTF-8, any ASCII
text is eventually a UTF-8 text.
