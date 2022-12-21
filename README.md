# A microservice for sales tax rate lookup

## Build

```bash
cargo build --target wasm32-wasi --release
```

## Run

```bash
wasmedge target/wasm32-wasi/release/sales_tax_rate_lookup.wasm
```

## Test

Run the following from another terminal.

```bash
$ curl http://localhost:8001/find_rate -X POST -d "78701"
0.0825

$ curl http://localhost:8001/find_rate -X POST -d "54921"
0.055
```

If the zip code is not in the source CSV file, the microservice will return an HTTP 404 response.

```bash
$ curl -v http://localhost:8001/find_rate -X POST -d "12345"

*   Trying 127.0.0.1:8001...
* TCP_NODELAY set
* Connected to localhost (127.0.0.1) port 8001 (#0)
> POST /find_rate HTTP/1.1
> Host: localhost:8001
> User-Agent: curl/7.68.0
> Accept: */*
> Content-Length: 5
> Content-Type: application/x-www-form-urlencoded
>
* upload completely sent off: 5 out of 5 bytes
* Mark bundle as not supporting multiuse
< HTTP/1.1 404 Not Found
< content-length: 0
< date: Wed, 21 Dec 2022 04:01:52 GMT
<
* Connection #0 to host localhost left intact
```
