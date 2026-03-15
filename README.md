# GPGPU-examples

> 日本語のREADMEはこちらです: [README.ja.md](README.ja.md)

A collection of examples demonstrating the use of GPGPU (General-Purpose Graphics Processing Unit) with WebGL2.

## Demo
- [demo](https://code4fukui.github.io/GPGPU-examples/)
- [simple](https://code4fukui.github.io/GPGPU-examples/simple.html)

## Features
- Utilizes WebGL2 transform feedback for GPGPU calculations
- Includes various example applications showcasing GPGPU capabilities
- Provides a reusable `GPGPU` class for easy integration into projects

## Usage
```javascript
import { GPGPU } from "https://code4fukui.github.io/GPGPU-examples/GPGPU.js";

const vstf = `#version 300 es
in float position;
out float vPosition;

void main() {
  vPosition = sin(position);
}
`;

const len = 10000 * 10000;
const position = new Float32Array(len);
for (let i = 0; i < len; i++) {
  position[i] = i;
}

const vPosition = new Float32Array(position.length);

const gl = document.createElement("canvas").getContext("webgl2");
const gpu = new GPGPU(gl, vstf, { position }, { vPosition });

const st1 = performance.now();
const res1 = gpu.calc();
const dt1 = performance.now() - st1;

console.log(gpu.inv.position, gpu.outv.vPosition);
result.innerHTML = `GPU: ${dt1.toFixed(1)}msec`;
```

## Dependencies
- [GPGPU.js and glutil of eggl](https://github.com/code4fukui/eggl/)
- [glMatrix](https://glmatrix.net/)

## License
MIT License