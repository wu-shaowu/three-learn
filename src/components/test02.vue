<template>
  <div class=""></div>
</template>

<script setup lang='ts'>
import * as THREE from 'three';
import {OrbitControls} from 'three/examples/jsm/controls/OrbitControls'

//坐标和移动
//创建场景
const scene = new THREE.Scene();
//创建相机
const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000)
//设置相机的位置
camera.position.set( 0, 20, 100 );
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
//坐标
const axesHelper = new THREE.AxesHelper( 5 );
scene.add( axesHelper );

//轨道空控制器
const controls = new OrbitControls( camera, renderer.domElement );

controls.update();
//实时渲染
function animate() {

	requestAnimationFrame( animate );

	// required if controls.enableDamping or controls.autoRotate are set to true
	controls.update();

	renderer.render( scene, camera );

}
animate()
</script>

<style lang="scss" scoped></style>
