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
El interruptor **Revolución** revoluciona `r = f(x)` en torno al eje X. Con solo el radio exterior es el **método del disco**; agregando un radio interior `g(x)` es el **método de la arandela**.

El panel de volumen muestra dos números que se calculan por caminos independientes:

- `π ∫ f² dx` (o `π ∫ (f²−g²) dx`) por regla de Simpson sobre el intervalo — el valor exacto de la curva.
- El volumen de la malla generada, por el teorema de la divergencia.

Que converjan valida la malla; la diferencia que queda es el error de facetado y se encoge al subir los pasos angulares. El slider **n de Riemann** dibuja los n discos o arandelas que la integral está sumando, para ver la convergencia.

Verificado contra diez sólidos con volumen de forma cerrada (esfera, cono, paraboloide, cuerno `1/x`, `sin(x)`, `x²`, y tres arandelas): la integral acierta al 0.0000% y la malla queda entre −0.15% y −0.21% con 64 pasos angulares, siempre cerrada y con normales hacia afuera.

El sólido se exporta acostado sobre el eje X; si lo quieres imprimir de pie, rótalo en el slicer.

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
The **Revolution** switch revolves `r = f(x)` about the X axis. With only an outer radius that is the **disk method**; adding an inner radius `g(x)` makes it the **washer method**.

The volume panel shows two numbers reached by independent routes:

- `π ∫ f² dx` (or `π ∫ (f²−g²) dx`) by Simpson's rule over the interval — the exact value for the curve.
- The volume of the generated mesh, by the divergence theorem.

Their agreement validates the mesh; the remaining gap is faceting error and shrinks as the angular steps rise. The **Riemann n** slider draws the n disks or washers the integral is summing, so the convergence is visible.

Verified against ten solids with closed-form volumes (sphere, cone, paraboloid, `1/x` horn, `sin(x)`, `x²`, and three washers): the integral is exact to 0.0000% and the mesh lands between −0.15% and −0.21% at 64 angular steps, always closed and outward-facing.

The solid exports lying along the X axis; rotate it in your slicer to print it standing up.

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
