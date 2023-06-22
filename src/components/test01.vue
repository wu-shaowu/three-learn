<script setup>
import * as THREE from 'three';

//创建场景
const scene = new THREE.Scene();
//创建相机
const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000)
//设置相机的位置
camera.position.set(0, 0, 10)
//添加
scene.add(camera)
//设置几何体
const geometry = new THREE.BoxGeometry(1, 1, 1);
//材质
const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 });
//根据几何体和材质构建物体
const cube = new THREE.Mesh(geometry, material);
//添加
scene.add(cube);
//初始化渲染器
const renderer = new THREE.WebGL1Renderer()
//设置渲染器大小
renderer.setSize(window.innerWidth, window.innerHeight)

document.body.appendChild(renderer.domElement)
//使用渲染器渲染相机场景
renderer.render(scene,camera)
</script>

<template>
  <div>
    111
  </div>
</template>

<style scoped></style>
