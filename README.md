# MathSurface

**Autor / Author:** Sebastián Duarte Villanueva ([@sebasdv](https://github.com/sebasdv))  
**Co-author:** Claude.ai  
**Live demo:** https://sebasdv.github.io/MathSurface/

---

## Español

Generador interactivo de superficies matemáticas 3D para impresión 3D. Visualiza y exporta funciones z = f(x, y) como archivos STL listos para imprimir, usando Three.js y Math.js.

### ¿Cómo usar?
1. Abre la [demo](https://sebasdv.github.io/MathSurface/) en tu navegador.
2. Escribe tu ecuación en el campo "Ecuación z = f(x, y)". Ejemplo:
   ```
   -0.25*x^3 - 0.25*y^3 + 0.5*x^2 + 0.5*y^2 - 0.25*x^2*y^2
   ```
3. Haz clic en "Generar" o selecciona un ejemplo predefinido.
4. Con "+ Agregar superficie" puedes graficar hasta cuatro ecuaciones a la vez. Donde dos se cruzan se dibuja automáticamente la **curva de intersección**.
5. Arrastra para rotar, scroll o pellizco para hacer zoom. El botón ⏸ del encabezado pausa la rotación automática.
6. Exporta como STL binario para impresión 3D (todas las superficies visibles, cada una como un cuerpo), o como PNG si solo quieres la imagen.

El STL se escribe en **binario**, no ASCII: alrededor de un cuarto del tamaño para la misma geometría (el ejemplo de cáscara pasa de 6.2 MB a 1.5 MB) y lo lee cualquier slicer actual. Verificado parseando el binario de vuelta y comparándolo con el ASCII equivalente: mismo número de triángulos, mismo volumen, ambos cerrados, y las normales guardadas concuerdan con el cosido.

### Controles por modo
Cada modo muestra solo los controles que realmente lee, para que no haya sliders que no hagan nada:

| Control | Superficies | Revolución |
|---|---|---|
| Resolución | sí | no — usa pasos axiales/angulares |
| Escala Z | sí | no se aplica a un radio |
| Grosor, cara inferior, intersecciones | sí | no |
| Intervalo, Riemann, panel de volumen | no | sí |
| `A`, `f`, `φ`, `a1`…`a5`, opacidad, mm/unidad | sí | sí |

Los coeficientes `a1`…`a5` son parámetros reales en ambos modos, así que se quedan visibles; lo que cambia son sus etiquetas — el sufijo `· x³` / `· y³` describe el polinomio por defecto de superficies, no los coeficientes en sí. En revolución aparecen como `a1`…`a5` a secas, porque las ecuaciones ahí solo aceptan `x`. El slider de rango pasa a llamarse "rango de grilla" en revolución, que es lo único que hace ahí.

### Sólidos de revolución
El interruptor **Revolución** ofrece los tres métodos del cálculo integral:

| Eje | Entradas | Método | Volumen |
|---|---|---|---|
| X | radio exterior `f(x)` | disco | `π ∫ f² dx` |
| X | radios exterior e interior | arandela | `π ∫ \|f²−g²\| dx` |
| Y | curva superior e inferior | cáscara | `2π ∫ x(f−g) dx` |

En modo cáscara el radio **es** x, así que el intervalo debe partir en 0 o más; la app lo rechaza si no. Dejar la segunda entrada vacía significa "la región entre la curva y el eje".

Las dos curvas se toman como máximo y mínimo punto a punto, no según en qué casilla las escribiste. Eso importa: si se cruzan — "la región limitada por y=x e y=2−x" es una arandela de libro — confiar en las etiquetas deja el radio interior por fuera del exterior y la malla se abre.

El panel de volumen muestra dos números que se calculan por caminos independientes:

- `π ∫ f² dx` (o `π ∫ (f²−g²) dx`) por regla de Simpson sobre el intervalo — el valor exacto de la curva.
- El volumen de la malla generada, por el teorema de la divergencia.

Que converjan valida la malla; la diferencia que queda es el error de facetado y se encoge al subir los pasos angulares. El slider **n de Riemann** dibuja los n discos o arandelas que la integral está sumando, para ver la convergencia.

### Propiedades de curva y masa
Una segunda fila del panel muestra, con densidad 1 como asumen los textos de cálculo:

| Magnitud | Fórmula |
|---|---|
| Longitud de arco | de las curvas que escribiste (no del eje) |
| Centroide | disco `x̄ = (π/V)∫x(f²−g²)dx` · cáscara `ȳ` con el mismo integrando |
| I respecto al eje de revolución | disco `(π/2)∫(f⁴−g⁴)dx` · cáscara `2π∫x³(f−g)dx` |
| I centroidal | respecto a un eje transversal por el centroide |

Dos de las tres coordenadas del centroide se anulan por simetría rotacional, así que solo se muestra la que sobrevive, la que va sobre el eje de revolución.

El acordeón **Propiedades clásicas** trae ocho presets elegidos porque cada uno tiene una forma cerrada memorable para una de estas magnitudes, así que puedes leer el panel contra una respuesta conocida:

| Preset | Curva e intervalo | Eje | Magnitud | Forma cerrada | Valor |
|---|---|---|---|---|---|
| Catenaria | `cosh(x)` en [−1, 1] | X | longitud de arco | `2·sinh 1` | 2.350 |
| Potencia 3/2 | `(2/3)*x^(3/2)` en [0, 3] | X | longitud de arco | `14/3` | 4.667 |
| Semiesfera | `sqrt(4 - x^2)` en [0, 2] | X | centroide `x̄` | `3r/8` | 0.750 |
| Paraboloide | `sqrt(x)` en [0, 4] | X | centroide `x̄` | `2h/3` | 2.667 |
| Cono desde la base | `2 - x` en [0, 2] | Y | centroide `ȳ` | `h/4` | 0.500 |
| Esfera | `sqrt(4 - x^2)` en [−2, 2] | X | `I` eje | `⅖MR²` | 53.62 |
| Cilindro | `2` en [0, 5] | X | `I` eje | `½MR²` | 125.66 |
| Cono | `x` en [0, 3] | X | `I` eje | `³⁄₁₀MR²` | 76.34 |

Los valores están en unidades de escena: `u` para la longitud de arco y el centroide, `u⁵` para los momentos. Pulsa el preset y el panel debe mostrar exactamente esa cifra.

Algunos reutilizan un sólido de la lista de arriba a propósito: una misma forma con varias propiedades es justamente el punto. El de cáscara declara su eje, porque un preset lleva el eje con el que se calculó su forma cerrada.

La longitud de arco y el área **no** usan `∫√(1+f'²)`. Esa forma necesita `f'`, y donde la tangente es vertical —los polos de `√(4−x²)`, lo más probable que alguien escriba aquí— el integrando diverge en el extremo y Simpson se pasa: la semicircunferencia salía 4.18% larga y el área de la esfera 0.23% alta. En su lugar se suman cuerdas del muestreo, cuya revolución es un tronco de cono de área exacta `π(r₁+r₂)·cuerda`. La misma semicircunferencia queda dentro del 0.0001%.

Verificado contra veinte sólidos con volumen de forma cerrada (esfera, cono, paraboloide, cuerno `1/x`, `sin(x)`, `x²`, tres arandelas, y diez casos de cáscara incluyendo cambio de signo y curvas que se cruzan): la integral acierta al 0.0000% y la malla queda dentro del 0.21% con 64 pasos angulares, siempre cerrada y con normales hacia afuera.

Cuando la región se cierra a nada en un punto **interior**, el sólido se toca a sí mismo en un círculo. Eso es geometría fiel, no un error, pero deja una arista no-manifold que algunos slicers marcan; la app avisa cuántos puntos así encontró.

En modo disco/arandela el sólido se exporta acostado sobre el eje X. En modo cáscara sale de pie, con base circular plana — mejor para imprimir directamente.

### Cara inferior: base plana o cáscara
El selector **Cara inferior** decide cómo se cierra el modelo por abajo:

- **Base plana** (por defecto): un solo plano bajo todo el modelo, en `min(z) − grosor`. Apoya en la cama de impresión, y no puede auto-intersectarse nunca.
- **Cáscara desplazada**: la superficie trasladada recto hacia abajo, de grosor constante. Gasta mucho menos material, pero no tiene base plana y **se atraviesa a sí misma** donde la caída entre muestras vecinas supera el grosor. La app detecta esa condición y avisa con los números concretos.

Con varias superficies el plano base es **común a todas**, para que la exportación apoye como una sola pieza en vez de dejar un cuerpo flotando; las alturas relativas se conservan, que es de lo que dependen las curvas de intersección.

La base se cierra con un abanico desde el centro al perímetro, no con una retícula completa: a resolución 100 son 400 triángulos en vez de 20.000 coplanares, y cada uno de ellos terminaría en el STL exportado (21.200 facetas contra 40.800).

Verificado: el volumen de la malla coincide con la integral doble `∫∫(z − z_base) dA` al 0.0000% en cuatro superficies distintas, los 4·n triángulos de la base tienen normal exactamente hacia abajo, y no queda ningún vértice bajo el plano.

### Superficies múltiples e intersecciones
Los parámetros `A`, `f`, `phi` y `a1`…`a5` son **compartidos** entre todas las superficies: mover un slider mueve toda la familia, que es justamente lo útil al compararlas. Cada superficie tiene solo su propia ecuación, color y visibilidad.

La curva de intersección es el conjunto de nivel cero del campo diferencia `d = z₁ − z₂`, calculado con marching squares sobre la misma malla con la que se teselan las superficies (sin evaluaciones extra ni librerías de geometría).

### Funciones soportadas
`sin` `cos` `tan` `exp` `log` `sqrt` `abs` y operadores `+ - * / ^`

### Variables y parámetros
- Variables: `x`, `y`
- Parámetros ajustables con sliders: `A`, `f`, `phi`, `a1`…`a5`

---

## English

Interactive 3D math surface generator for 3D printing. Visualize and export z = f(x, y) equations as print-ready STL files, powered by Three.js and Math.js.

### How to use
1. Open the [live demo](https://sebasdv.github.io/MathSurface/) in your browser.
2. Enter your equation in the "Equation z = f(x, y)" field. Example:
   ```
   -0.25*x^3 - 0.25*y^3 + 0.5*x^2 + 0.5*y^2 - 0.25*x^2*y^2
   ```
3. Click "Generate" or pick a preset example.
4. "+ Add surface" plots up to four equations at once. Where two of them cross, the **intersection curve** is drawn automatically.
5. Drag to rotate, scroll or pinch to zoom. The ⏸ button in the header pauses the auto-rotation.
6. Export as binary STL for 3D printing (every visible surface, each as its own body), or as PNG if you just want the image.

The STL is written in **binary**, not ASCII: roughly a quarter the size for the same geometry (the shell example drops from 6.2 MB to 1.5 MB) and every current slicer reads it. Verified by parsing the binary back and comparing against the equivalent ASCII: same triangle count, same volume, both closed, and the stored normals agree with the winding.

### Mode-specific controls
Each mode shows only the controls it actually reads, so no slider sits there doing nothing:

| Control | Surfaces | Revolution |
|---|---|---|
| Resolution | yes | no — uses axial/angular steps |
| Z scale | yes | not applied to a radius |
| Thickness, underside, intersections | yes | no |
| Interval, Riemann, volume panel | no | yes |
| `A`, `f`, `φ`, `a1`…`a5`, opacity, mm/unit | yes | yes |

The `a1`…`a5` coefficients are real parameters in both modes, so they stay visible; what changes is their labels — the `· x³` / `· y³` suffix describes the default surface polynomial, not the coefficients themselves. In revolution they read as plain `a1`…`a5`, because equations there take only `x`. The range slider becomes "grid range" in revolution, which is all it does there.

### Solids of revolution
The **Revolution** switch covers all three integral-calculus methods:

| Axis | Inputs | Method | Volume |
|---|---|---|---|
| X | outer radius `f(x)` | disk | `π ∫ f² dx` |
| X | outer and inner radii | washer | `π ∫ \|f²−g²\| dx` |
| Y | upper and lower curves | shell | `2π ∫ x(f−g) dx` |

In shell mode the radius **is** x, so the interval must start at 0 or above; the app refuses it otherwise. Leaving the second input empty means "the region between the curve and the axis".

The two curves are taken as the pointwise max and min, not according to which box you typed them in. That matters: if they cross — "the region bounded by y=x and y=2−x" is a textbook washer — trusting the labels puts the inner radius outside the outer one and the mesh comes apart.

The volume panel shows two numbers reached by independent routes:

- `π ∫ f² dx` (or `π ∫ (f²−g²) dx`) by Simpson's rule over the interval — the exact value for the curve.
- The volume of the generated mesh, by the divergence theorem.

Their agreement validates the mesh; the remaining gap is faceting error and shrinks as the angular steps rise. The **Riemann n** slider draws the n disks or washers the integral is summing, so the convergence is visible.

### Curve and mass properties
A second row of the panel reports, at unit density as calculus texts assume:

| Quantity | Formula |
|---|---|
| Arc length | of the curves you typed (not of the axis) |
| Centroid | disk `x̄ = (π/V)∫x(f²−g²)dx` · shell `ȳ` from the same integrand |
| I about the axis of revolution | disk `(π/2)∫(f⁴−g⁴)dx` · shell `2π∫x³(f−g)dx` |
| I centroidal | about a transverse axis through the centroid |

Two of the three centroid coordinates vanish by rotational symmetry, so only the surviving one — the one along the axis of revolution — is shown.

The **Classic Properties** accordion holds eight presets chosen because each has a memorable closed form for one of these quantities, so the panel can be read against a known answer:

| Preset | Curve and interval | Axis | Quantity | Closed form | Value |
|---|---|---|---|---|---|
| Catenary | `cosh(x)` on [−1, 1] | X | arc length | `2·sinh 1` | 2.350 |
| Power 3/2 | `(2/3)*x^(3/2)` on [0, 3] | X | arc length | `14/3` | 4.667 |
| Hemisphere | `sqrt(4 - x^2)` on [0, 2] | X | centroid `x̄` | `3r/8` | 0.750 |
| Paraboloid | `sqrt(x)` on [0, 4] | X | centroid `x̄` | `2h/3` | 2.667 |
| Cone from base | `2 - x` on [0, 2] | Y | centroid `ȳ` | `h/4` | 0.500 |
| Sphere | `sqrt(4 - x^2)` on [−2, 2] | X | `I` axis | `⅖MR²` | 53.62 |
| Cylinder | `2` on [0, 5] | X | `I` axis | `½MR²` | 125.66 |
| Cone | `x` on [0, 3] | X | `I` axis | `³⁄₁₀MR²` | 76.34 |

Values are in scene units: `u` for arc length and centroid, `u⁵` for the moments. Click the preset and the panel should read exactly that figure.

Some reuse a solid from the list above on purpose: one shape carrying several properties is the point. The shell one states its axis, because a preset carries the axis its closed form was computed for.

Arc length and area do **not** use `∫√(1+f'²)`. That form needs `f'`, and where the tangent is vertical — the poles of `√(4−x²)`, the most likely thing anyone types here — the integrand is unbounded at the endpoint and Simpson overshoots: the semicircle came out 4.18% long and the sphere's area 0.23% high. Chords of the sampling are summed instead, and each chord's revolution is a truncated cone whose lateral area is exactly `π(r₁+r₂)·chord`. The same semicircle lands within 0.0001%.

Verified against twenty solids with closed-form volumes (sphere, cone, paraboloid, `1/x` horn, `sin(x)`, `x²`, three washers, and ten shell cases including sign changes and crossing curves): the integral is exact to 0.0000% and the mesh lands within 0.21% at 64 angular steps, always closed and outward-facing.

Where the region closes to nothing at an **interior** point, the solid genuinely touches itself along a circle. That is faithful geometry rather than an error, but it leaves a non-manifold edge some slicers flag, so the app reports how many such points it found.

In disk/washer mode the solid exports lying along the X axis. In shell mode it comes out standing up, with a flat circular base — better for printing as-is.

### Underside: flat base or offset shell
The **Underside** selector decides how the model closes at the bottom:

- **Flat base** (default): one plane under the whole model, at `min(z) − thickness`. It sits on the print bed, and it can never self-intersect.
- **Offset shell**: the surface translated straight down, constant thickness. Far less material, but no flat base, and it **passes through itself** wherever the drop between neighbouring samples exceeds the thickness. The app detects that and warns with the actual numbers.

With several surfaces the base plane is **shared**, so an export sits on the bed as one piece rather than leaving a body floating; relative heights survive, which is what the intersection curves depend on.

The base closes with a fan from the centre to the perimeter rather than a full lattice: at resolution 100 that is 400 triangles instead of 20,000 coplanar ones, and every one of them would land in the exported STL (21,200 facets against 40,800).

Verified: the mesh volume matches the double integral `∫∫(z − z_base) dA` to 0.0000% across four different surfaces, all 4·n base triangles have a normal pointing exactly straight down, and no vertex is left below the plane.

### Multiple surfaces and intersections
The `A`, `f`, `phi` and `a1`…`a5` parameters are **shared** across all surfaces: moving one slider moves the whole family, which is the point when you are comparing them. Each surface only owns its equation, colour and visibility.

The intersection curve is the zero level set of the difference field `d = z₁ − z₂`, computed with marching squares over the same lattice the surfaces are tessellated on — no extra evaluations and no geometry library.

### Supported functions
`sin` `cos` `tan` `exp` `log` `sqrt` `abs` and operators `+ - * / ^`

### Variables and parameters
- Variables: `x`, `y`
- Slider-controlled parameters: `A`, `f`, `phi`, `a1`…`a5`

---

## Integridad de dependencias
Los dos scripts de CDN llevan **Subresource Integrity** (SHA-512) más `crossorigin="anonymous"`: si el archivo servido no coincide con su hash, el navegador se niega a ejecutarlo, y la app muestra su mensaje de error en vez de romperse a medias.

Los digests se calcularon desde los bytes descargados y se confirmaron contra los que publica cdnjs:

```bash
curl -s https://api.cdnjs.com/libraries/three.js/r128?fields=sri
curl -s https://api.cdnjs.com/libraries/mathjs/11.11.0?fields=sri
```

**Si actualizas la versión de Three.js o Math.js hay que recalcular el hash**, o la app deja de cargar.

La hoja de estilos de Google Fonts va **sin** `integrity` a propósito: Google la genera por petición y varía las reglas `@font-face` según el User-Agent, así que un hash fijo fallaría en algunos navegadores. Si no llega, la página cae a `system-ui` y sigue funcionando.

## Stack
- [Three.js r128](https://threejs.org/)
- [Math.js v11](https://mathjs.org/)
- Vanilla JS, no build tools

## Dependency integrity
Both CDN scripts carry **Subresource Integrity** (SHA-512) plus `crossorigin="anonymous"`: if the served file does not match its hash the browser refuses to run it, and the app shows its error message instead of half-breaking.

The digests were computed from the downloaded bytes and confirmed against the ones cdnjs publishes:

```bash
curl -s https://api.cdnjs.com/libraries/three.js/r128?fields=sri
curl -s https://api.cdnjs.com/libraries/mathjs/11.11.0?fields=sri
```

**Bumping the Three.js or Math.js version means recomputing the hash**, or the app stops loading.

The Google Fonts stylesheet deliberately has **no** `integrity`: Google generates it per request, varying the `@font-face` rules by User-Agent, so a pinned hash would fail on some browsers. If it never arrives the page falls back to `system-ui` and keeps working.

## License
MIT © Sebastián Duarte Villanueva
