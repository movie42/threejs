# Basic Scene

threejs를 배우고 싶어서 threejs journey 수강 신청했다. 아직 기본 단계지만 하루에 한개씩 꾸준하게 듣다가 정리를 하고 넘어가야할 것 같아서 작성한다. 기본 큐브는 아래처럼 그릴 수 있다. Threejs Document를 보고 정리했다. 몇 번 반복하다보니까 그냥 뭐가 필요한지 대강은 알 것 같다.

- scene를 그린다. scene는 기본이다. 에펙에 컴포지션(?)같은 건가보다.
- geometray와 meteral은 mesh에 포함되어야하고 mesh는 scene에 추가해야한다.
- camera도 선언한뒤 scene에 추가해야한다.
- renderer는 canvas를 object로 받을 수 있고 canvas에 지금까지 그린 scene를 랜더링한다.
- renderer는 property로 setSize, render가 있는데 둘다 함수다.
- render에는 scene와 camera를 지정해주고 setSize에는 넓이와 높이를 지정해주면 canvas의 넢이와 높이가 된다.
- 그리고 나면 검은 화면만 나오는데 camera가 object에 너무 가까이 있어서 그렇다. position.z를 키워주면 카메라가 멀리 물러나면서 object를 보여준다.

# 기본 모형을 그리기 위해서 필요한 생성자들.

다음은 기본 모형을 그리는데 필요한 생성자들을 정리했다. 사실 정리가 아니라 그냥 ThreeJS Documentation에서 퍼왔다.

## Scene

Scenes allow you to set up what and where is to be rendered by three.js. This is where you place objects, lights and cameras.

```jsx
const scene = new THREE.Scene();
```

## **[BoxGeometry(width : Float, height : Float, depth : Float, widthSegments : Integer, heightSegments : Integer, depthSegments : Integer)](https://threejs.org/docs/index.html#api/en/geometries/BoxGeometry)**

```jsx
const geometry = new THREE.BoxGeometry(1, 1, 1);
const material = new THREE.MeshBasicMaterial({ color: `ff00ff` });
const cube = new THREE.Mesh(geometry, material);
scene.add(cube);
```

## [MeshBasicMater](https://threejs.org/docs/#api/en/materials/MeshBasicMaterial)ial(parameters :Object)

A material for drawing geometries in a simple shaded (flat or wireframe) way.

```jsx
const material = new THREE.MeshBasicMaterial({ color: `ff00ff` });
```

parameters(optional) an object with one or more properties defining the material's appearance. Any property of the material (including any property inherited from Material) can be passed in here.

## [Mesh](https://threejs.org/docs/index.html#api/en/objects/Mesh)(**geometry : BufferGeometry, material : Material)**

Class representing triangular [polygon mesh](https://en.wikipedia.org/wiki/Polygon_mesh) based objects. Also serves as a base for other classes such as SkinnedMesh.

### Constructor

- Mesh( geometry : BufferGeometry, material : Material )
  geometry — (optional) an instance of BufferGeometry. Default is a new BufferGeometry.material — (optional) a single or an array of Material. Default is a new MeshBasicMaterial

```tsx
const geometry = new THREE.BoxGeometry(1, 1, 1);
const material = new THREE.MeshBasicMaterial({ color: 0xffff00 });
const mesh = new THREE.Mesh(geometry, material);
scene.add(mesh);
```

## **[PerspectiveCamera](https://threejs.org/docs/index.html#api/en/cameras/PerspectiveCamera)(fov : Number, aspect : Number, near : Number, far : Number)**

fov — Camera frustum vertical field of view.

aspect — Camera frustum aspect ratio.

near — Camera frustum near plane.

far — Camera frustum far plane.

Camera that uses [perspective projection](<https://en.wikipedia.org/wiki/Perspective_(graphical)>).

This projection mode is designed to mimic the way the human eye sees. It is the most common projection mode used for rendering a 3D scene.

```tsx
const camera = new THREE.PerspectiveCamera(45, width / height, 1, 1000);
scene.add(camera);
```

## **[WebGLRenderer](https://threejs.org/docs/index.html#api/en/renderers/WebGLRenderer)( parameters : Object )**

The WebGL renderer displays your beautifully crafted scenes using [WebGL](https://en.wikipedia.org/wiki/WebGL).

parameters
 - (optional) object with properties defining the renderer's behaviour. The constructor also accepts no parameters at all. In all cases, it will assume sane defaults when parameters are missing. The following are valid parameters:

**canvas**
 - A [canvas](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/canvas) where the renderer draws its output. This corresponds to the domElement property below. If not passed in here, a new canvas element will be created.

```tsx
const canvas = document.querySelector(".canvas");
const renderer = new THREE.WebGLRenderer({
  canvas
});
renderer.setSize(sizes.width, sizes.height);
renderer.render(scene, camera);
```

**.setSize ( width : Integer, height : Integer, updateStyle : Boolean ) : undefined**

Resizes the output canvas to (width, height) with device pixel ratio taken into account, and also sets the viewport to fit that size, starting in (0, 0). Setting updateStyle to false prevents any style changes to the output canvas.

**.render ( scene : Object3D, camera : Camera ) : undefined**

Render a scene or another type of object using a camera. The render is done to a previously specified renderTarget set by calling .setRenderTarget or to the canvas as usual. By default render buffers are cleared before rendering but you can prevent this by setting the property autoClear to false. If you want to prevent only certain buffers being cleared you can set either the autoClearColor, autoClearStencil or autoClearDepth properties to false. To forcibly clear one ore more buffers call .clear.
