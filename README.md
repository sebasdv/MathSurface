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
3. Haz clic en "Generar Superficie" o selecciona un ejemplo predefinido.
4. Usa los controles para rotar, hacer zoom y ajustar la visualización.
5. Exporta la superficie como archivo STL para impresión 3D.

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
2. Enter your equation in the "Ecuación z = f(x, y)" field. Example:
   ```
   -0.25*x^3 - 0.25*y^3 + 0.5*x^2 + 0.5*y^2 - 0.25*x^2*y^2
   ```
3. Click "Generar Superficie" (Generate Surface) or pick a preset example.
4. Use the mouse to rotate, zoom, and adjust the visualization.
5. Export the surface as an STL file for 3D printing.

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
