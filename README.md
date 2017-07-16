# Factorial

### Prerequisite

The following parts all require the provided factorial server to be running:

```go
$ go run server/main.go
```


The server takes a GET request with a query parameter of n, where n is the number to generate
the factorial for.

Example:  GET /?n=5  should return 120.

### Part 1

Write a function that sends each factorial number to a channel every ¼ second, starting at n = 0.
The factorial value should be requested from the provided factorial server.

The function can potentially calculate factorials "forever,” but also knows how to stop calculating
more numbers and return when needed.

In the main function, print each number as it receives them. Running the program should show
us the following output.

```go
$ go run series.go
N: 0, A: 1
N: 1, A: 1
N: 2, A: 2
N: 3, A: 6
N: 4, A: 24
N: 5, A: 120
N: 6, A: 720
N: 7, A: 5040
N: 8, A: 40320
N: 9, A: 362880 N: 10, A: 3628800 #...
# later ...
N: 48, A:
12413915592536072670862289047373375038521486354677760000000000
N: 49, A:
608281864034267560872252163321295376887552831379210240000000000
N: 50, A:
30414093201713378043612608166064768844377641568960512000000000000
# and so on ...


```



Stopping the program with "Ctrl­C" must cancel any further numbers from being calculated and
print a friendly "See you later" before terminating *gracefully*. (Do NOT use os.Exit).

### Part 2

Write a function that concurrently calculates the first 10 factorial numbers and sends it to a
channel.The function should utilize the same factorial server provided.

In the main function, print each number as it receives them from the channel. Running the
program multiple times could show us the possible outputs:

```go
 $ go run concurrent.go N: 0, A: 1
N: 5, A: 120
N: 1, A: 1
N: 2, A: 2
N: 3, A: 6
N: 4, A: 24
N: 6, A: 720
N: 8, A: 40320
N: 7, A: 5040
N: 9, A: 362880
$ go run concurrent.go
N: 3, A: 6
N: 4, A: 24
N: 5, A: 120
N: 6, A: 720
N: 7, A: 5040
N: 0, A: 1
N: 8, A: 40320
N: 1, A: 1
N: 2, A: 2
N: 9, A: 362880
$ go run concurrent.go
N: 4, A: 24
N: 3, A: 6
N: 1, A: 1
N: 2, A: 2
N: 0, A: 1
N: 8, A: 40320
N: 6, A: 720
N: 5, A: 120
N: 9, A: 362880
N: 7, A: 5040
```

### Part 3

Write a function that concurrently calculates factorial numbers with four workers from n = 30 to n
= 40 and sends it to a channel. It should utilize the factorial server provided.

Write another function that concurrently sorts the digits in the numbers with two workers using
Quick Sort(use sort.Sort()), and sends it to a channel.

In the main function, print the factorial number and the sorted digits as they are received.
Gracefully terminate all workers and exit after printing the 5th value. Do not use os.Exit().

An example output:

```go
$ go run pipeline.go
N: 32
  A: 263130836933693530167218012160000000
  S: 000000000011111222333333356666678899
N: 33
  A: 8683317618811886495518194401280000000
  S: 0000000011111112334445566678888888899
N: 37
  A: 13763753091226345046315979581580902400000000
  S: 00000000000011112223333344455555666777889999
N: 39
  A: 20397882081197443358640281739902897356800000000
  S: 00000000000011122223333344455667777888888899999
N: 31
  A: 8222838654177922817725562880000000
  S: 0000000112222222345556677778888889
$ go run pipeline.go
N: 33
  A: 8683317618811886495518194401280000000
  S: 0000000011111112334445566678888888899
N: 35
  A: 10333147966386144929666651337523200000000
  S: 00000000011112223333333444556666666778999
N: 36
  A: 371993326789901217467999448150835200000000
  S: 000000000011112223333444556677778889999999
N: 40
  A: 815915283247897734345611269596115894272000000000
  S: 000000000111111222223334444555556667777888899999
N: 34
  A: 295232799039604140847618609643520000000
  S: 000000000001122223334444556666778899999
N: 38
  A: 523022617466601111760007224100074291200000000
  S: 000000000000000011111112222222344456666677779
```

