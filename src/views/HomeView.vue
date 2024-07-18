<script setup lang="ts">
import * as THREE from 'three';
import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls.js';
// 导入lil.gui
import { GUI } from 'three/examples/jsm/libs/lil-gui.module.min.js';
// 创建场景
const scene = new THREE.Scene();

// 创建相机
const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
camera.position.z = 5;
camera.position.x = 2;
camera.position.y = 2;
camera.lookAt(0, 0, 0);

// 创建渲染器
const renderer = new THREE.WebGLRenderer();
renderer.setSize(window.innerWidth, window.innerHeight);
document.body.appendChild(renderer.domElement);

// 窗口大小改变自动调整
window.addEventListener('resize', () => {
  camera.aspect = window.innerWidth / window.innerHeight;
  camera.updateProjectionMatrix();
  renderer.setSize(window.innerWidth, window.innerHeight);
});

// 坐标辅助器
const axesHelper = new THREE.AxesHelper(5);
scene.add(axesHelper);

// 轨道控制器
const controls = new OrbitControls(camera, renderer.domElement);
controls.enableDamping = true;  // 启用阻尼
controls.dampingFactor = 0.05;  // 阻尼系数

function animate(){
  controls.update();  // 更新轨道控制器
  requestAnimationFrame(animate);
  renderer.render(scene, camera);  // 渲染场景
}

animate();



// 创建几何体
const geometry = new THREE.BufferGeometry();
console.log(geometry, 'geometry');

const vertices = new Float32Array([
  -1.0, -1.0, 0,
  1.0, -1.0, 0,
  1.0, 1.0, 0,
  // 1.0, 1.0, 0,
  -1.0, 1.0, 0,
  // -1.0, -1.0, 0,
]);
geometry.setAttribute('position', new THREE.BufferAttribute(vertices, 3));
const material0 = new THREE.MeshBasicMaterial({ 
  color: 0x00ff00, 
  // wireframe: true,
  side: THREE.DoubleSide
});
const material1 = new THREE.MeshBasicMaterial({ 
  color: 0xff0000, 
  // wireframe: true,
  // side: THREE.DoubleSide
});
// 创建索引
const indices = new Uint16Array([
  0, 1, 2,
  2, 3, 0
]);
geometry.addGroup(0, 3, 0);
geometry.addGroup(3, 3, 1);
geometry.setIndex(new THREE.BufferAttribute(indices, 1));
const cubeMy = new THREE.Mesh(geometry, [material0, material1]);
scene.add(cubeMy);

// // 创建几何体
const cubegeometry = new THREE.BoxGeometry(1, 1, 1);
console.log(cubegeometry);
// // 创建材质
const cubematerial0 = new THREE.MeshBasicMaterial({
  color: 0x00ff00,
  // wireframe: true,
});
const cubematerial1 = new THREE.MeshBasicMaterial({
  color: 0xff0000,
});
const cubematerial2 = new THREE.MeshBasicMaterial({
  color: 0x0000ff,
});
const cubematerial3 = new THREE.MeshBasicMaterial({
  color: 0xffff00,
});
const cubematerial4 = new THREE.MeshBasicMaterial({
  color: 0x00ffff,
});
const cubematerial5 = new THREE.MeshBasicMaterial({
  color: 0xff00ff,
});
const cube = new THREE.Mesh(cubegeometry, [
  cubematerial0,
  cubematerial1,
  cubematerial2,
  cubematerial3,
  cubematerial4,
  cubematerial5,
]);
// console.log(geometry);

cube.position.x = 2;

// 将网格添加到场景中
scene.add(cube);










</script>

<template>
</template>
