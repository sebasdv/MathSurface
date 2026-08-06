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
