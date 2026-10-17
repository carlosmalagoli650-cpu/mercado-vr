
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Supermercado VR 3D</title>
</head>
<body>
  <h1>Supermercado VR</h1>
  <script type="module">
    import * as THREE from
      'https://cdn.jsdelivr.net/npm/three@0.160.0/build/three.module.js';

    const cena = new THREE.Scene();
    cena.background = new THREE.Color(0xb8cbd0);

    const camera = new THREE.PerspectiveCamera(
      75, innerWidth / innerHeight, 0.1, 100
    );
    camera.position.set(0, 1.7, 8);

    const renderizador = new THREE.WebGLRenderer({ antialias: true });
    renderizador.setSize(innerWidth, innerHeight);
    renderizador.xr.enabled = true;
    document.body.appendChild(renderizador.domElement);

    cena.add(new THREE.HemisphereLight(0xffffff, 0x666666, 2));

    function criarCaixa(largura, altura, profundidade,
                        cor, x, y, z) {
      const objeto = new THREE.Mesh(
        new THREE.BoxGeometry(largura, altura, profundidade),
        new THREE.MeshStandardMaterial({ color: cor })
      );
      objeto.position.set(x, y, z);
      cena.add(objeto);
      return objeto;
    }

    // Piso do supermercado
    criarCaixa(30, 0.2, 30, 0xc5c5bd, 0, -0.1, 0);

    // Prateleiras
    for (const z of [-7, 0, 7]) {
      for (const x of [-6, 0, 6]) {
        criarCaixa(3, 2.5, 0.7, 0x687579, x, 1.25, z);
      }
    }

    function animar() {
      renderizador.setAnimationLoop(() => {
        renderizador.render(cena, camera);
      });
    }
    animar();
  </script>
</body>
</html>

