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
6. Exporta como STL para impresión 3D (todas las superficies visibles, cada una como un cuerpo), o como PNG si solo quieres la imagen.

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

Verificado contra veinte sólidos con volumen de forma cerrada (esfera, cono, paraboloide, cuerno `1/x`, `sin(x)`, `x²`, tres arandelas, y diez casos de cáscara incluyendo cambio de signo y curvas que se cruzan): la integral acierta al 0.0000% y la malla queda dentro del 0.21% con 64 pasos angulares, siempre cerrada y con normales hacia afuera.

Cuando la región se cierra a nada en un punto **interior**, el sólido se toca a sí mismo en un círculo. Eso es geometría fiel, no un error, pero deja una arista no-manifold que algunos slicers marcan; la app avisa cuántos puntos así encontró.

En modo disco/arandela el sólido se exporta acostado sobre el eje X. En modo cáscara sale de pie, con base circular plana — mejor para imprimir directamente.

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
6. Export as STL for 3D printing (every visible surface, each as its own body), or as PNG if you just want the image.

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

Verified against twenty solids with closed-form volumes (sphere, cone, paraboloid, `1/x` horn, `sin(x)`, `x²`, three washers, and ten shell cases including sign changes and crossing curves): the integral is exact to 0.0000% and the mesh lands within 0.21% at 64 angular steps, always closed and outward-facing.

Where the region closes to nothing at an **interior** point, the solid genuinely touches itself along a circle. That is faithful geometry rather than an error, but it leaves a non-manifold edge some slicers flag, so the app reports how many such points it found.

In disk/washer mode the solid exports lying along the X axis. In shell mode it comes out standing up, with a flat circular base — better for printing as-is.

### Multiple surfaces and intersections
The `A`, `f`, `phi` and `a1`…`a5` parameters are **shared** across all surfaces: moving one slider moves the whole family, which is the point when you are comparing them. Each surface only owns its equation, colour and visibility.

The intersection curve is the zero level set of the difference field `d = z₁ − z₂`, computed with marching squares over the same lattice the surfaces are tessellated on — no extra evaluations and no geometry library.

### Supported functions
`sin` `cos` `tan` `exp` `log` `sqrt` `abs` and operators `+ - * / ^`

### Variables and parameters
- Variables: `x`, `y`
- Slider-controlled parameters: `A`, `f`, `phi`, `a1`…`a5`

---

## Stack
- [Three.js r128](https://threejs.org/)
- [Math.js v11](https://mathjs.org/)
- Vanilla JS, no build tools

## License
MIT © Sebastián Duarte Villanueva
