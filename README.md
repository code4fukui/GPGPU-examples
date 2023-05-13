# GPGPU-examples
 
- [demo](https://code4fukui.github.io/GPGPU-examples/)
- [simple](https://code4fukui.github.io/GPGPU-examples/simple.html)

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

## dependencies

- [GPGPU.js and glutil of eggl](https://github.com/code4fukui/eggl/)
- [glMatrix](https://glmatrix.net/)
