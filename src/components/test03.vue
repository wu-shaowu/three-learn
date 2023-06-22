<template>
	<div class=""></div>
</template>

<script setup lang='ts'>
import * as THREE from 'three';
import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls'
import { gsap } from 'gsap';
import { render } from 'vue';
import * as dat from 'dat.gui'

//坐标和移动
//创建场景
const scene = new THREE.Scene();
//创建相机
const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000)
//设置相机的位置
camera.position.set(0, 20, 100);
//添加
scene.add(camera)
//设置几何体
const geometry = new THREE.BoxGeometry(1, 1, 1);
//材质
const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 });
//根据几何体和材质构建物体
const cube = new THREE.Mesh(geometry, material);

const gui = new dat.GUI()git branch -M main

cube.position.set(0, 0.0)
//添加
scene.add(cube);
//初始化渲染器
const renderer = new THREE.WebGL1Renderer()
//设置渲染器大小
renderer.setSize(window.innerWidth, window.innerHeight)

document.body.appendChild(renderer.domElement)
//坐标
const axesHelper = new THREE.AxesHelper(20);
scene.add(axesHelper);

//轨道空控制器
const controls = new OrbitControls(camera, renderer.domElement);
controls.enableDamping=true;

controls.update();

const clock = new THREE.Clock()

gsap.to(cube.position, {
	y: 10, duration: 5, ease: "power1.inOut", repeat: 2, 
	onComplete: () => {
		console.log("ok");
	}, onStart: () => {
		console.log("开始");

	}
})
//实时渲染
function animate() {
	// let time = clock.getElapsedTime()	
	// cube.position.x = (time % 5)  *1
	controls.update()
	requestAnimationFrame(animate);



	renderer.render(scene, camera);

}
animate()
//监听窗口事件变化，重新渲染画面
window.addEventListener("resize",()=>{
	//更新摄像头
	camera.aspect = window.innerWidth / window.innerHeight 
	//更新摄像头投影矩阵
	camera.updateProjectionMatrix();
	//更新渲染器
	renderer.setSize(window.innerWidth,window.innerHeight)
	//设置渲染器的像素比
	renderer.setPixelRatio(window.devicePixelRatio)

})
//双击全屏
window.addEventListener("dblclick",()=>{
	const fullScreenElement = document.fullscreenElement

	if(fullScreenElement){
		document.exitFullscreen()
	}
	else{
		renderer.domElement.requestFullscreen()
	}

})


</script>

<style lang="scss" scoped></style>
