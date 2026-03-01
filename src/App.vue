<script setup>
import * as THREE from "three";
import { OrbitControls } from "three/addons/controls/OrbitControls.js";

let scene, camera, renderer, controls;
function init() {
  // 场景
  scene = new THREE.Scene();
  // 相机
  camera = new THREE.PerspectiveCamera(
    75,
    window.innerWidth / window.innerHeight,
    0.1,
    1000,
  );
  camera.position.z = 5;
  // 渲染器
  renderer = new THREE.WebGLRenderer({
    antialias: true, // 开启抗锯齿
  });
  renderer.setSize(window.innerWidth, window.innerHeight);
  document.body.appendChild(renderer.domElement);
}

// 创建立方体
function createCube() {
  const geometry = new THREE.BoxGeometry(1, 1, 1);
  const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 });
  const cube = new THREE.Mesh(geometry, material);
  scene.add(cube);
}

// 轨道控制器
function controlsCreate() {
  controls = new OrbitControls(camera, renderer.domElement);
}

// 循环渲染
function renderLoop() {
  requestAnimationFrame(renderLoop);
  controls.update();
  renderer.render(scene, camera);
}

init();
controlsCreate();
createCube();
renderLoop();


// const axesHelper = new THREE.AxesHelper(5);
// scene.add(axesHelper);

// function animate(time) {
//   controls.update();
//   renderer.render(scene, camera);
// }
// renderer.setAnimationLoop(animate);

// 让它动起来
// function animate(time) {
//   cube.rotation.x = time / 2000;
//   cube.rotation.y = time / 1000;
//   renderer.render(scene, camera);
// }
// renderer.setAnimationLoop(animate);
</script>

<template></template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
