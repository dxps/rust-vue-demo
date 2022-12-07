# rust-vue-demo

This project demonstrates the integration of npm/vue into a rust axum web-service. The web-service is self-contained, embedding the webui assets into the binary. The webui creates a websocket being used by the web-service to send data to the webui once per second.

## Requirements
* npm/nodes toolchain must be available
* rust toolchain must be available

## Features
* Vue project code is located in folder `webui/`
* The `cargo build` will trigger the vue npm build process ('npm_rs'), the resultin g HTML code will be placed in `webui/dist/`
* The vue JavaScript assets of `webui/dist/` will be embedded into the Rust code (`rust_embed`)
* The binary will be created form Rust code
* The binary will provide a web-service listening at port 3000 (`axum`)
* When connecting with web-browser to service port, eg http://127.0.0.1:3000, a websocket will be established
* The web-service will use the websocket to send data to the webui, cycling once per second.
* The webui provides a button to send data to the webservice, but the message is not processed in web-service.
* If files are modified in `src/` or `webui/src/` the command `cargo build` will update the binary (`build.rs`)

## Usage

Download the project folder from https://github.com/frehberg/rust-vue-demo
```
git clone https://github.com/frehberg/rust-vue-demo
```

Initialize the npm dependencies of the webui frontend
```
cd rust-vue-demo/webui; npm install
```

Build the project
```shell
cd rust-vue-demo/
cargo build
```

Start the web-service
```shell
cd rust-vue-demo/
cargo run
```

Connect with web-browser to http://127.0.0.1:3000

## Developing the Vue Web Frontend

Generate the assets from Vue templates
```shell
cd rust-vue-demo/webui
npm install; npm run build
```
Start the web-service locally listening at port 8080
```shell
cd rust-vue-demo/webui
npm run serve
```

Connect with web-browser to `http://localhost:8080`

Any time the files in folder `rust-vue-demo/webui/src/` are modified, the npm-build-process will be triggered and the browser will perform a reload.



