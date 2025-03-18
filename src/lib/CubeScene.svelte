<script lang="ts">
import * as THREE from 'three';
import { OrbitControls } from 'three/addons/controls/OrbitControls.js';

const starsTexture = '/stars.jpg';

const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera( 75, window.innerWidth / window.innerHeight, 0.1, 1000 );


const renderer = new THREE.WebGLRenderer();
renderer.setSize( window.innerWidth, window.innerHeight );
document.body.appendChild( renderer.domElement );
const oribt = new OrbitControls(camera, renderer.domElement);
const textureLoader = new THREE.TextureLoader();

const geometry = new THREE.SphereGeometry(5, 100, 100);
const material = new THREE.MeshStandardMaterial( { color: 0x03fc98, wireframe: true } );
const cube = new THREE.Mesh( geometry, material );
scene.add( cube );
cube.position.set(0, 2, 0)

camera.position.set(0, 0, 5);
oribt.update();

const directionalLight = new THREE.DirectionalLight(0xFFFFFF, 1);
scene.add(directionalLight);


const ambientLight = new THREE.AmbientLight(0x333333);
scene.add(ambientLight)


const gridHelper = new THREE.GridHelper(10);
gridHelper.add(gridHelper);
scene.add(gridHelper);


const cubeTextureLoader = new THREE.CubeTextureLoader();
scene.background = cubeTextureLoader.load([
    starsTexture,
    starsTexture,
    starsTexture,
    starsTexture,
    starsTexture,
    starsTexture
]);


function animate() {
  requestAnimationFrame( animate );

  renderer.render( scene, camera );
}

animate();
</script>