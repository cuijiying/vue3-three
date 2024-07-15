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

// 创建几何体
const geometry = new THREE.BoxGeometry(1, 1, 1);

// 创建材质
const parentMaterial = new THREE.MeshBasicMaterial({ color: 0x00ffff });
parentMaterial.wireframe = true
const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 });


const parent = new THREE.Mesh(geometry, parentMaterial);
parent.position.set(-2, 0, 0)
// parent.scale.set(2, 2, 2)
// 创建网格
const cube = new THREE.Mesh(geometry, material);
cube.position.set(2, 0, 0)
cube.rotation.set(Math.PI / 4, 0, 0)
// 缩放
cube.scale.set(2, 2, 2)
parent.rotation.set(Math.PI / 4, 0, 0)
parent.add(cube)

// 添加到场景
scene.add(parent)

// 坐标辅助器
const axesHelper = new THREE.AxesHelper(5);
scene.add(axesHelper);

// 轨道控制器
const controls = new OrbitControls(camera, renderer.domElement);
controls.enableDamping = true;  // 启用阻尼
controls.dampingFactor = 0.05;  // 阻尼系数

// 窗口大小改变自动调整
window.addEventListener('resize', () => {
  camera.aspect = window.innerWidth / window.innerHeight;
  camera.updateProjectionMatrix();
  renderer.setSize(window.innerWidth, window.innerHeight);
});

// 点击按钮全屏
let fullScreen = document.createElement('button');
fullScreen.innerHTML = '全屏';
document.body.appendChild(fullScreen);
fullScreen.onclick = () => {
  const fullScreenEL = document.fullscreenElement;
  if (!fullScreenEL) {
    fullScreen.innerHTML = '退出全屏';
    document.body.requestFullscreen();
  } else {
    document.exitFullscreen();
    fullScreen.innerHTML = '全屏';
  }
}

// gui
const gui = new GUI();
const obj = {
  isFullScreen: false,
 
  // 位置
}
gui.add(obj, 'isFullScreen').onChange(() => {
  if (obj.isFullScreen) {
    fullScreen.click();
  } else {
    fullScreen.click();
  }
});
gui.addColor(parentMaterial, 'color').onChange(() => {
  parentMaterial.color.set(parentMaterial.color);
});
gui.add(parent.position, 'x', -5, 5);
// gui.add(cube.position, 'y').min(-5).max(5);
gui.add(parent.position, 'y').min(-5).max(5);
gui.add(parent.position, 'z').min(-5).max(5).name("z轴").step(0.1);
// 设置线框模式
gui.add(parentMaterial, 'wireframe').name("是否线框材质").onChange((value) => {
  parentMaterial.wireframe = value;
});


function animate(){
  controls.update();  // 更新轨道控制器
  requestAnimationFrame(animate);
  renderer.render(scene, camera);  // 渲染场景
}

animate();
</script>

<template>
</template>
