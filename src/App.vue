<script setup>
import * as THREE from "three";
import { OrbitControls } from "three/addons/controls/OrbitControls.js";

let scene, camera, renderer, controls, cube;
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
  camera.position.x = 5;
  camera.position.y = 5;
  camera.position.z = 5;
  // 渲染器
  renderer = new THREE.WebGLRenderer({
    antialias: true, // 开启抗锯齿
  });
  renderer.setSize(window.innerWidth, window.innerHeight);
  document.body.appendChild(renderer.domElement);
}
function createCube() {
  const geometry = new THREE.BoxGeometry(1, 1, 1);
  const cubeInfoArr = [];
  for (let i = 0; i < 5; i++) {
    cubeInfoArr.push({
      color: Math.random() * 0xffffff,
      w: Math.floor(Math.random() * (3 - 1 + 1)) + 1,
      h: Math.floor(Math.random() * (3 - 1 + 1)) + 1,
      d: Math.floor(Math.random() * (3 - 1 + 1)) + 1,
      x: Math.floor(Math.random() * (5 - -5 + 1)) - 5,
      y: Math.floor(Math.random() * (5 - -5 + 1)) - 5,
      z: Math.floor(Math.random() * (5 - -5 + 1)) - 5,
    });
  }
  console.log(cubeInfoArr);
  cubeInfoArr.forEach((item) => {
    const material = new THREE.MeshBasicMaterial({ color: item.color });
    const geometry = new THREE.BoxGeometry(item.w, item.h, item.d);
    const cube = new THREE.Mesh(geometry, material);
    cube.position.set(item.x, item.y, item.z);
    scene.add(cube);
  });
}
function controlsCreate() {
  controls = new OrbitControls(camera, renderer.domElement);
  controls.enableDamping = true; // 启用阻尼效果
}
function renderLoop() {
  requestAnimationFrame(renderLoop);
  controls.update();
  renderer.render(scene, camera);
}
function createAxiosHelper() {
  const axesHelper = new THREE.AxesHelper(5);
  scene.add(axesHelper);
}
function renderResize() {
  window.addEventListener("resize", () => {
    // 1. 更新相机的宽高比
    camera.aspect = window.innerWidth / window.innerHeight;

    // 2. 更新相机的投影矩阵（必须调用）
    camera.updateProjectionMatrix();

    // 3. 更新渲染器的尺寸
    renderer.setSize(window.innerWidth, window.innerHeight);

    // 4. （可选）如果使用了像素比，确保在移动端横竖屏切换时也更新
    // renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
  });
}

// 初始化
init();
// 轨道控制器
controlsCreate();
// 创建坐标轴
createAxiosHelper();
// 创建立方体
createCube();
// 适配窗口大小
renderResize();
// 循环渲染
renderLoop();
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
