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
```

If the zip code is not in the source CSV file, the microservice will return a default tax rate of 0.08.

```bash
$ curl http://localhost:8001/find_rate -X POST -d "12345"
0.08
```
