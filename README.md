# [coarse_hash](https://github.com/rtmigo/coarse_hash_py)

Calculates fast coarse hashes from files. Instead of hashing entire files, we take individual bytes, add the size of the file, and calculate the hash from that.

This allows you to get hashes of large files very quickly. However, it
may not display small differences in file content.

# Install

``` bash
$ pip3 install git+https://github.com/rtmigo/coarse_hash_py#egg=coarse_hash
```

# Use

Calculate the checksum based on ten equidistant bytes, and the file size. 
The very first and the very last byte of the file will be among the ten read.

``` python3
from pathlib import Path
from coarse_hash import file_to_hash_equidistant 

print(file_to_hash_equidistant(Path('/path/to/file.dat'), n=10))
```

Calculate the checksum based on the bytes located at an increasing distance from
each other, and the file size. In this case, we will read more bytes from the
file header than from the body.

``` python3
from pathlib import Path
from coarse_hash import file_to_hash_fibonacci

print(file_to_hash_fibonacci(Path('/path/to/file.dat')))
```

### HashAlgo

The optional `HashAlgo` argument allows you to select a hashing algorithm.

| Algorithm         | Digest Size (bytes) |
|-------------------|---------------------|
| `HashAlgo.crc32`  | 4                   |
| `HashAlgo.md5`    | 24                  |
| `HashAlgo.sha256` | 32                  |

```python3
from coarse_hash import file_to_hash_fibonacci, HashAlgo

print(file_to_hash_fibonacci('/path/to/file.dat', algo=HashAlgo.crc32))
```
