# ZAPEL Frame

Programa web para el análisis de **pórticos y vigas 2D por el método de los elementos finitos**, con soporte de **fundación elástica tipo Winkler**. Se dibuja la estructura directamente en pantalla, se asignan apoyos, cargas y propiedades, y se calculan desplazamientos, reacciones y diagramas, con una forma de trabajo parecida a la de Robot Structural Analysis.

Es una actualización gráfica del programa Fortran **ZAPEL77P** (vigas sobre fundación elástica con módulo de suelo variable).

- **Autor del programa original (ZAPEL77P):** Dr. Bernardo Deschapelles
- **Actualizado por:** Prof. Raymond Rosa Ávila

## Demostración

Una vez publicado en GitHub Pages, el programa queda disponible en:

`https://TU-USUARIO.github.io/NOMBRE-DEL-REPOSITORIO/`

No requiere instalación: es un único archivo `index.html` que corre en el navegador, sin servidor ni dependencias externas.

## Características

- Dibujo interactivo de barras sobre una malla con ajuste (snap) a nodos y a la cuadrícula.
- Dos sistemas de unidades: **SI (kN · m)** e **Imperial (kip · ft)**, intercambiables en cualquier momento.
- Cotas con la longitud de cada barra.
- Apoyos: empotrado, articulado, rodillo en Y y rodillo en X.
- Cargas nodales (Fx, Fy, Mz) y carga distribuida con variación lineal a lo largo de la barra.
- Articulaciones (liberación de momento) en el inicio o en el final de cada barra.
- Fundación elástica Winkler con módulo de balasto **ks** variable linealmente entre el inicio y el final de la barra.
- Subdivisión de cada barra en varios elementos finitos.
- Resultados: deformada (con el valor máximo por barra), momento flector, cortante, axial y reacción del suelo.
- Tabla de reacciones, valores máximos globales y comprobación del equilibrio vertical.

## Uso

1. **Dibujar barra:** haz clic para iniciar y clic en cada nodo siguiente. Termina con clic derecho, `Esc` o volviendo a pulsar sobre el último nodo.
2. **Seleccionar:** elige un nodo o una barra para editar sus datos en el panel derecho.
   - Nodo: tipo de apoyo y cargas.
   - Barra: ancho `b`, canto `h`, módulo `E`, carga `w` al inicio y al final, `ks` al inicio y al final, subdivisiones y articulaciones.
3. **Eliminar:** borra el nodo o la barra seleccionados (también con `Supr`).
4. **▶ Calcular:** ejecuta el análisis. Después puedes alternar entre *Deformada*, *Momento*, *Cortante*, *Axial* y *Suelo*.
5. Rueda del ratón para acercar o alejar. Arrastra en un espacio vacío, con la herramienta *Seleccionar*, para desplazar la vista. **Encuadrar** ajusta la vista al modelo.

Se incluyen dos ejemplos: una viga sobre suelo y un pórtico.

## Convenciones

| Magnitud | Convención |
|---|---|
| Ejes globales | X hacia la derecha, Y hacia arriba |
| Fx, Fy | Positivas hacia +X y hacia +Y |
| Mz | Positivo en sentido antihorario |
| Carga distribuida `w` | Positiva hacia abajo (gravedad), por unidad de longitud de la barra |
| Momento flector | Se dibuja del lado de la tracción; positivo cuando la fibra inferior está en tracción |
| Axial | Positivo en tracción |
| Reacción del suelo | Positiva hacia arriba |

## Formulación

- Elemento de pórtico 2D con 3 grados de libertad por nodo (u, v, θ), teoría de Euler-Bernoulli.
- Matriz de rigidez de la fundación Winkler integrada con cuadratura de Gauss y funciones de forma de Hermite. El coeficiente de la fundación por unidad de longitud es `ks · b`.
- Carga distribuida lineal convertida en fuerzas nodales equivalentes.
- Articulaciones mediante condensación estática.
- Sistema de ecuaciones global resuelto con eliminación gaussiana con pivoteo parcial. Si detecta un mecanismo, avisa de que la estructura es inestable.
- Diagramas de M, V y N obtenidos integrando el equilibrio a lo largo de cada elemento, incluyendo la reacción del suelo. La deformada se interpola con funciones de Hermite.

## Limitaciones

- Análisis lineal elástico en 2D.
- Sección rectangular (`b × h`) de propiedades constantes en cada barra.
- El módulo de suelo varía solo linealmente; la ley exponencial de ZAPEL77P no está incluida.
- No incluye lectura de archivos `.DAT` de ZAPEL, resortes nodales, asentamientos impuestos ni exportación a Excel.
- Para vigas sobre suelo conviene subdividir las barras en varios elementos para obtener buena precisión.

Se recomienda verificar los resultados con casos de solución conocida antes de usarlos en un proyecto real.

## Créditos

- Programa original **ZAPEL77P** (2005, actualizado en 2010): Dr. Bernardo Deschapelles.
- Versión web gráfica: Prof. Raymond Rosa Ávila.
