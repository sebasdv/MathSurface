# Generador 3D de Ecuaciones Matemáticas / 3D Mathematical Equation Generator

**Autor / Author:** Sebastián Duarte Villanueva  
**Coautor / Co-author:** Claude.ai  
**Organización / Organization:** Universidad Adolfo Ibañez, Design Engineering Center

## Español

Este proyecto permite visualizar y generar modelos 3D de funciones matemáticas de dos variables (x, y) de manera interactiva usando Three.js y Math.js. Puedes ingresar tu propia ecuación en el campo correspondiente y ajustar parámetros como amplitud, frecuencia, fase, rango, resolución y más.

### ¿Cómo usar?
1. Abre el archivo `index.html` en tu navegador.
2. Escribe tu ecuación en el campo "Ecuación z = f(x, y)". Ejemplo:
   ```
   -0.25*x^3 - 0.25*y^3 + 0.5*x^2 + 0.5*y^2 - 0.25*x^2*y^2
   ```
3. Haz clic en "Generar Superficie" o selecciona un ejemplo.
4. Usa los controles para rotar, hacer zoom y ajustar la visualización.
5. Puedes exportar la superficie como archivo STL para impresión 3D.

### Ejemplo de función avanzada
Para graficar la función f(x, y) del análisis de extremos:
```
f(x, y) = -1/4 x³ - 1/4 y³ + 1/2 x² + 1/2 y² - 1/4 x²y²
```
Ingresa:
```
-0.25*x^3 - 0.25*y^3 + 0.5*x^2 + 0.5*y^2 - 0.25*x^2*y^2
```

## English

This project allows you to visualize and generate 3D models of mathematical functions of two variables (x, y) interactively using Three.js and Math.js. You can enter your own equation and adjust parameters such as amplitude, frequency, phase, range, resolution, and more.

### How to use?
1. Open the `index.html` file in your browser.
2. Enter your equation in the "Ecuación z = f(x, y)" field. Example:
   ```
   -0.25*x^3 - 0.25*y^3 + 0.5*x^2 + 0.5*y^2 - 0.25*x^2*y^2
   ```
3. Click "Generar Superficie" (Generate Surface) or select an example.
4. Use the controls to rotate, zoom, and adjust the visualization.
5. You can export the surface as an STL file for 3D printing.

### Advanced function example
To plot the function f(x, y) from the extrema analysis:
```
f(x, y) = -1/4 x³ - 1/4 y³ + 1/2 x² + 1/2 y² - 1/4 x²y²
```
Enter:
```
-0.25*x^3 - 0.25*y^3 + 0.5*x^2 + 0.5*y^2 - 0.25*x^2*y^2
``` 