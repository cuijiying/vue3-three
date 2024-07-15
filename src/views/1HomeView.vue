<script setup lang="ts">
import * as THREE from 'three';
import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls.js';

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

// 创建几何体
const geometry = new THREE.BoxGeometry(1, 1, 1);

// 创建材质
const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 });

// 创建网格
const cube = new THREE.Mesh(geometry, material);

// 添加到场景
scene.add(cube);

// 坐标辅助器
const axesHelper = new THREE.AxesHelper(5);
scene.add(axesHelper);

// 轨道控制器
// const controls = new OrbitControls(camera, renderer.domElement);
//  document.body 也可以解决轨道控制器跟随问题
const controls = new OrbitControls(camera, document.body);
controls.enableDamping = true;  // 启用阻尼
controls.dampingFactor = 0.05;  // 阻尼系数
controls.autoRotate = true;     // 自动旋转

// 窗口大小调整
window.addEventListener('resize', () => {
  camera.aspect = window.innerWidth / window.innerHeight;
  camera.updateProjectionMatrix();
  renderer.setSize(window.innerWidth, window.innerHeight);
});

function animate(){
  requestAnimationFrame(animate);
  controls.update();  // 更新轨道控制器
  renderer.render(scene, camera);  // 渲染场景
}

animate();
</script>

<template>
</template>
