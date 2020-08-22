[The Mr.Charles](https://www.linkedin.com/in/themrcharles/), building FOSSGIS@[Kartoza](https://kartoza.com).

<svg fill="none" viewBox="0 0 800 400" width="800" height="400" xmlns="http://www.w3.org/2000/svg">
  <foreignObject width="100%" height="100%">
    <div xmlns="http://www.w3.org/1999/xhtml">
      <script src="./three.min.js"></script>
      <script src="./OBJLoader.js"></script>
      <script src="./MTLLoader.js"></script>
      <style>
        .container {
          color: white;
          background: #0f0f0f;
          width: 100%;
          height: 384px;
          text-align: center;
          display: flex;
          flex-direction: column;
          align-items: center;
          justify-content: center;
          margin: 0;
          border-radius: 12px;
        }
      </style>
      <div class="container">
        <h1>Like a ninja, only not as good...</h1>
        <canvas id="canvas" style="width: 256px; height: 256px; border-radius: 12px;"></canvas>
      </div>
      <script>
        let trefoil;

        const scene = new THREE.Scene();

        const light = new THREE.DirectionalLight('#ffffff', 0.9);
        light.position.set(-20, 0, 100);
        scene.add(light);

        const camera = new THREE.PerspectiveCamera(45, 1, 1, 1000);
        camera.position.z = 8;

        const canvas = document.getElementById("canvas");
        const renderer = new THREE.WebGLRenderer({ canvas: canvas, antialias: true });

        const objLoader = new THREE.OBJLoader();
        objLoader.setPath('./')

        const mtlLoader = new THREE.MTLLoader();
        mtlLoader.setPath('./')

        new Promise((resolve) => {
          mtlLoader.load('trefoil.mtl', (materials) => {
            resolve(materials);
          })
        })
        .then((materials) => {
          materials.preload();
          objLoader.setMaterials(materials);
          objLoader.load('trefoil.obj', (object) => {
            trefoil = object;
            scene.add(object);
          });
        })

        function render() {
          if (trefoil) {
            trefoil.rotation.x += 0.005;
            trefoil.rotation.y += 0.005;
          }
          requestAnimationFrame(render);
          renderer.render(scene, camera);
        }

        render();

      </script>
    </div>
  </foreignObject>
</svg>

<!--
**zacharlie/zacharlie** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

### Hi there 👋

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->
