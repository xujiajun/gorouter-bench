# gorouter-bench
benchmark for  the gorouter

## Benchmarks

> go test -bench=.

### Benchmark System:

* Go Version : go1.11.2 darwin/amd64
* OS:        Mac OS X 10.13.6
* Architecture:   x86_64
* 16 GB 2133 MHz LPDDR3
* CPU: 3.1 GHz Intel Core i7

### Tested routers:

* [beego/mux](https://github.com/beego/mux)
* [go-zoo/bone](https://github.com/go-zoo/bone)
* [go-chi/chi](https://github.com/go-chi/chi)
* [julienschmidt/httprouter](https://github.com/julienschmidt/httprouter)
* [gorilla/mux](https://github.com/gorilla/mux)
* [trie-mux/mux](https://github.com/teambition/trie-mux)
* [xujiajun/gorouter](https://github.com/xujiajun/gorouter)


Thanks the author of httprouter: [@julienschmidt](https://github.com/julienschmidt) give me advise about benchmark [issues/24](https://github.com/xujiajun/gorouter/issues/24)

## Result:

Given some routing matching syntax differences, divide GithubAPI into two groups：

### Using GithubAPI Result：

```
BenchmarkBeegoMuxRouterWithGithubAPI-8   	   10000	    142398 ns/op	  134752 B/op	    1038 allocs/op
BenchmarkBoneRouterWithGithubAPI-8       	    1000	   2104486 ns/op	  720160 B/op	    8620 allocs/op
BenchmarkTrieMuxRouterWithGithubAPI-8    	   20000	     80845 ns/op	   65856 B/op	     537 allocs/op
BenchmarkHttpRouterWithGithubAPI-8       	   50000	     30169 ns/op	   13792 B/op	     167 allocs/op
BenchmarkGoRouter1WithGithubAPI-8        	   30000	     57793 ns/op	   13832 B/op	     406 allocs/op

```
### Using GithubAPI2 Result：

```
BenchmarkGoRouter2WithGithubAPI2-8       	   30000	     57613 ns/op	   13832 B/op	     406 allocs/op
BenchmarkChiRouterWithGithubAPI2-8       	   10000	    143224 ns/op	  104436 B/op	    1110 allocs/op
BenchmarkMuxRouterWithGithubAPI2-8       	     300	   4450731 ns/op	   61463 B/op	     995 allocs/op
```

### All togther Result：

```
➜  gorouter git:(master) go test -bench=.
GithubAPI Routes: 203
GithubAPI2 Routes: 203
   BeegoMuxRouter: 111072 Bytes
   BoneRouter: 100992 Bytes
   ChiRouter: 71512 Bytes
   HttpRouter: 37016 Bytes
   trie-mux: 131128 Bytes
   MuxRouter: 1378496 Bytes
   GoRouter1: 83824 Bytes
   GoRouter2: 85584 Bytes
goos: darwin
goarch: amd64
pkg: github.com/xujiajun/gorouter
BenchmarkBeegoMuxRouterWithGithubAPI-8   	   10000	    142398 ns/op	  134752 B/op	    1038 allocs/op
BenchmarkBoneRouterWithGithubAPI-8       	    1000	   2104486 ns/op	  720160 B/op	    8620 allocs/op
BenchmarkTrieMuxRouterWithGithubAPI-8    	   20000	     80845 ns/op	   65856 B/op	     537 allocs/op
BenchmarkHttpRouterWithGithubAPI-8       	   50000	     30169 ns/op	   13792 B/op	     167 allocs/op
BenchmarkGoRouter1WithGithubAPI-8        	   30000	     57793 ns/op	   13832 B/op	     406 allocs/op
BenchmarkGoRouter2WithGithubAPI2-8       	   30000	     57613 ns/op	   13832 B/op	     406 allocs/op
BenchmarkChiRouterWithGithubAPI2-8       	   10000	    143224 ns/op	  104436 B/op	    1110 allocs/op
BenchmarkMuxRouterWithGithubAPI2-8       	     300	   4450731 ns/op	   61463 B/op	     995 allocs/op
PASS
ok  	github.com/xujiajun/gorouter	15.918s

```

### Conclusions:

* Performance (xujiajun/gorouter,julienschmidt/httprouter and teambition/trie-mux are fast)

* Memory Consumption (xujiajun/gorouter and julienschmidt/httprouter are fewer) 

* Features (julienschmidt/httprouter not supports regexp，but others support it)

> if you want a high performance router which supports regexp, maybe [xujiajun/gorouter](https://github.com/xujiajun/gorouter) is good choice.

> if you want a high performance router which not supports regexp, maybe [julienschmidt/httprouter](https://github.com/julienschmidt/httprouter) is good choice.

In the end, as julienschmidt said `performance can not be the (only) criterion for choosing a router. Play around a bit with some of the routers, and choose the one you like best.`
