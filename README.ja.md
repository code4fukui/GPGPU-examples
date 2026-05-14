# GPGPU-examples

WebGL2を用いたGPGPU（General-Purpose Graphics Processing Unit）の実装例を集めたリポジトリです。

## デモ
- [demo](https://code4fukui.github.io/GPGPU-examples/)
- [simple](https://code4fukui.github.io/GPGPU-examples/simple.html)

## 特徴
- WebGL2のTransform Feedbackを活用したGPGPU計算
- GPGPUの機能を示す様々なサンプルアプリケーションを収録
- プロジェクトへ簡単に組み込める再利用可能な `GPGPU` クラスを提供

## 使い方
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

## 依存関係
- [eggl の GPGPU.js および glutil](https://github.com/code4fukui/eggl/)
- [glMatrix](https://glmatrix.net/)

## ライセンス
MIT License — 詳細は [LICENSE](LICENSE) をご覧ください。
