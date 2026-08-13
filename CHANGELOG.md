# Changelog

Formato basado en [Keep a Changelog](https://keepachangelog.com/es-ES/1.1.0/).
Las versiones se marcan con tags de git: `git tag -l`.

---

## [2.0] — 2026-08-13

La aplicación pasa de un modo a dos. Además de graficar superficies `z = f(x, y)`,
ahora genera sólidos de revolución por los tres métodos del cálculo integral y
reporta sus propiedades de masa.

Cada magnitud nueva está verificada contra formas cerradas conocidas, y los
sólidos contra integración por fuerza bruta independiente de las fórmulas.

### Añadido

- **Modo revolución** con los tres métodos: disco, arandela (eje X) y cáscara
  (eje Y). El intervalo, los pasos axiales y los angulares son propios del modo.
- **Panel de volumen** que compara la integral exacta contra el volumen de la
  malla que generó. Que converjan valida la malla; la diferencia restante es
  error de facetado.
- **Longitud de arco, centroide y momentos de inercia** (densidad 1), respecto al
  eje de revolución y a un eje transversal por el centroide.
- **Rebanadas de Riemann** con slider de n: discos o arandelas en modo disco,
  cáscaras cilíndricas en modo cáscara.
- Dos grupos de presets: **Sólidos clásicos** (volumen) y **Propiedades
  clásicas** (arco, centroide, inercia). Cada botón anuncia su forma cerrada.
- **Hasta cuatro superficies a la vez** con **curvas de intersección** calculadas
  por marching squares sobre el campo diferencia.
- **Base plana imprimible** como alternativa a la cáscara desplazada, con aviso
  cuando esta última se auto-atraviesa.
- **Exportación PNG** a 2× el tamaño en pantalla.
- **Soporte táctil**: arrastrar para rotar y pellizcar para hacer zoom.
- **Subresource Integrity** (SHA-512) en Three.js y Math.js.
- Detección de WebGL ausente y de librerías que no cargan, con mensaje en vez de
  pantalla en blanco.

### Cambiado

- **STL binario en vez de ASCII**: ~4× más pequeño para la misma geometría (un
  ejemplo pasó de 6.2 MB a 1.5 MB).
- **La app abre en una placa imprimible** de 80 × 80 × 43 mm. El polinomio que
  venía por defecto medía 80 × 80 × 1043 mm.
- El **área de superficie** ahora incluye las caras planas. Antes omitía las tapas
  de un cilindro, la base de un cono y la pared de una cáscara.
- **Longitud de arco y área** se calculan sumando cuerdas, no con `∫√(1+f'²)`.
  Esa forma diverge donde la tangente es vertical: la semicircunferencia salía
  4.18% larga.
- Cada modo muestra **solo los controles que lee**, sin sliders inertes.
- El panel móvil deriva su posición del layout en vez de asumir una cabecera de
  52 px.

### Corregido

- Fugas de memoria GPU: la geometría y los materiales descartados no se liberaban.
- Acumulación de reconstrucciones al arrastrar sliders.
- El **método de la arandela con curvas que se cruzan** producía una malla abierta
  y un volumen que se cancelaba a cero.
- Los presets de disco heredaban el eje activo y reportaban el volumen del sólido
  equivocado.
- El cosido de la malla quedaba hacia adentro; el STL salía bien solo por un
  efecto secundario del intercambio de ejes.
- La grilla en mm y sus etiquetas no coincidían.
- Los colores de los ejes contradecían el panel de dimensiones.
- El cambio de idioma destruía el marcado del modal de ayuda.
- Reiniciar no restauraba el zoom.
- `[hidden]` no ocultaba nada donde una clase definía `display`.
- El overlay de dimensiones se solapaba con el botón flotante en móvil.

### Seguridad

- Los scripts de CDN se rechazan si su hash no coincide. Los digests están
  confirmados contra los que publica cdnjs.
- Los mensajes del parser se insertan con `textContent`, no `innerHTML`.

---

## [1.0] — 2026-04-17

Primera versión pública.

- Superficie `z = f(x, y)` con ecuación libre evaluada por Math.js.
- Parámetros ajustables `A`, `f`, `φ` y `a1`…`a5`.
- Exportación STL con grilla en milímetros y escala configurable.
- Interfaz bilingüe EN/ES y modal de ayuda.
- Diseño responsive con panel colapsable en móvil.
