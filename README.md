# Basic Rust HTTP Server

A extremely barebones http server with a couple of methods and the ability to attach handlers to routes.

!!! This implementation likely has major security concerns.

NOTE: I did not read the HTTP specification before making this.

## Features

- Status codes
- Get / set headers
- Attach request handlers
- Multithreaded
- Repond with text / media

## Code Example

```rust
use rust_http_server::http;

fn main() -> ! {
    let mut server = http::HTTPServer::new("0.0.0.0", 7878);

    server.post("/", |req: http::Request, _res: &mut http::Response| {
        println!("{:#?}", req.body);
        http::send_string("Hello")
    });

    server.get("/", |_req: http::Request, _res: &mut http::Response| {
        http::send_file("templates/index.html")
    });

    println!("Server starting...");
    server.start();
}
```
