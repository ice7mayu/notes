# Base64

[Original Post](https://stackabuse.com/encoding-and-decoding-base64-strings-in-python/)

## Encoding Strings with Python

Python 3 provides a base64 module that allows us to easily encode and decode information. We first convert the string into a bytes-like object. Once converted, we can use the base64 module to encode it.

In a new file encoding_text.py, enter the following:

```python
import base64

message = "Python is fun"
message_bytes = message.encode('ascii')
base64_bytes = base64.b64encode(message_bytes)
base64_message = base64_bytes.decode('ascii')

print(base64_message)
```

In the code above, we first imported the base64 module. The message variable stores our input string to be encoded. We convert that to a bytes-like object using the string's encode method and store it in message_bytes. We then Base64 encode message_bytes and store the result in base64_bytes using the base64.b64encode method. We finally get the string representation of the Base64 conversion by decoding the base64_bytes as ASCII.

## Decoding Strings with Python

Decoding a Base64 string is essentially a reverse of the encoding process. We decode the Base64 string into bytes of unencoded data. We then convert the bytes-like object into a string.

In a new file called decoding_text.py, write the following code:

```python
import base64

base64_message = 'UHl0aG9uIGlzIGZ1bg=='
base64_bytes = base64_message.encode('ascii')
message_bytes = base64.b64decode(base64_bytes)
message = message_bytes.decode('ascii')

print(message)
```

Once again, we need the base64 module imported. We then encode our message into a bytes-like object with encode('ASCII'). We continue by calling the base64.b64decode method to decode the base64_bytes into our message_bytes variable. Finally, we decode message_bytes into a string object message, so it becomes human readable.

Run this file to see the following output:

```bash
$ python3 decoding_text.py
Python is fun
```

Now that we can encode and decode string data, let's try to encode binary data.
