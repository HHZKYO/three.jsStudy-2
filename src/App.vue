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
  const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 });
  cube = new THREE.Mesh(geometry, material);
  scene.add(cube);
}
function controlsCreate() {
  controls = new OrbitControls(camera, renderer.domElement);
  controls.enableDamping = true; // 启用阻尼效果
  // controls.autoRotate = true; // 启用自动旋转
  // 限制垂直旋转角度
  // controls.maxPolarAngle = Math.PI / 2;
  // controls.minPolarAngle = 0;
  // // 限制水平旋转角度
  // controls.maxAzimuthAngle = Math.PI / 2;
  // controls.minAzimuthAngle = 0;
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
function moveCube() {
  cube.position.x = 5; 
  cube.rotation.x = Math.PI / 4; // 方向是逆时针旋转的
  cube.scale.set(1, 1, 2)
}


// 初始化
init();
// 轨道控制器
controlsCreate();
// 创建坐标轴
createAxiosHelper();
// 创建立方体
createCube();
// 变换立方体
moveCube()
// 适配窗口大小
renderResize();
// 循环渲染
renderLoop();

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
