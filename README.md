# ZAPEL Frame

Programa web para el análisis de **pórticos y vigas planos (2D)** por el **método de los elementos finitos**, con soporte de **fundación elástica tipo Winkler**. Se dibuja la estructura directamente en pantalla, se asignan apoyos, cargas y propiedades, y se obtienen deformada, reacciones y diagramas de esfuerzos, con una forma de trabajo parecida a la de Robot Structural Analysis.

Es una actualización gráfica del programa Fortran **ZAPEL77P** (vigas sobre fundación elástica).

> Es un único archivo HTML autocontenido: no requiere instalación, servidor, base de datos ni conexión a internet para funcionar.

## Instalación

### Opción A: publicarlo como página web con GitHub Pages

1. Crea una cuenta en [github.com](https://github.com) si aún no tienes una.
2. Pulsa **New repository**, ponle un nombre (por ejemplo `zapel-frame`) y déjalo en **Public**.
3. Sube los archivos a la **raíz** del repositorio con **Add file → Upload files**:
   - `index.html` (el programa)
   - `README.md`
   - `LICENSE` (ver la sección *Licencia*)

   Pulsa **Commit changes**.
4. Ve a **Settings → Pages**. En *Build and deployment* elige **Deploy from a branch**, la rama **main** y la carpeta **/ (root)**, y pulsa **Save**.
5. Espera uno o dos minutos. El programa quedará en:

   `https://TU-USUARIO.github.io/zapel-frame/`

**Si ves un error 404:** comprueba que el archivo se llame exactamente `index.html` (en minúsculas, sin `.html.html`), que esté en la raíz y no dentro de una carpeta, y que en la pestaña **Actions** el despliegue *pages build and deployment* tenga el check verde. Recarga con Ctrl+F5.

**Para actualizar:** sube el archivo nuevo con el mismo nombre y reemplaza el anterior. La página se actualiza sola en uno o dos minutos.

### Opción B: usarlo en tu computadora, sin internet

1. Descarga `index.html`, con **Code → Download ZIP** o descargando el archivo directamente.
2. Haz doble clic en el archivo para abrirlo con cualquier navegador moderno (Chrome, Edge, Firefox, Safari).

### Opción C: desde la terminal

```bash
git clone https://github.com/TU-USUARIO/zapel-frame.git
cd zapel-frame
# abre index.html en tu navegador
```

## Características

- Dibujo interactivo de barras sobre malla, con ajuste a nodos y a la cuadrícula.
- Unidades **SI (kN · m)** e **Imperial (kip · ft)**, intercambiables en cualquier momento.
- Cotas con la longitud de cada barra.
- Apoyos: empotrado, articulado, rodillo en Y y rodillo en X.
- Cargas nodales (Fx, Fy, Mz).
- Cargas distribuidas por barra, con valor al inicio y al final:
  - de gravedad (`w`, positiva hacia abajo);
  - laterales (`wx`, positiva hacia +X), por ejemplo sobre columnas.
- Articulaciones (liberación de momento) en el inicio o en el final de cada barra.
- Subdivisión de cada barra en varios elementos finitos.
- Fundación Winkler con módulo de balasto `ks` variable linealmente entre el inicio y el final de la barra.
- Resultados:
  - deformada, con el valor máximo por barra y animación;
  - momento flector, cortante, axial y reacción del suelo;
  - tabla de reacciones, valores máximos y comprobación del equilibrio vertical.
- Funciona en el teléfono: pellizca con dos dedos para hacer zoom, o usa los botones **＋** y **－**.

## Uso básico

1. Elige **Dibujar barra** y haz clic en cada nodo. Termina con clic derecho o `Esc`.
2. Con **Seleccionar**, elige un nodo (apoyo y cargas) o una barra (sección, material, cargas, suelo, articulaciones y subdivisiones) y edítalos en el panel derecho.
3. Pulsa **▶ Calcular** y alterna entre *Deformada*, *Momento*, *Cortante*, *Axial* y *Suelo*.
4. Pulsa **▶ Animar** para ver la deformada en movimiento.

El botón **Encuadrar** ajusta la vista al modelo. La rueda del ratón hace zoom, y arrastrar sobre un espacio vacío con «Seleccionar» desplaza el dibujo. Hay dos ejemplos cargados: una viga sobre suelo y un pórtico.

## Convenciones

| Magnitud | Convención |
|---|---|
| Ejes globales | X hacia la derecha, Y hacia arriba |
| Fx, Fy | Positivas hacia +X y hacia +Y |
| Mz | Positivo en sentido antihorario |
| Carga `w` | Positiva hacia abajo, por unidad de longitud de la barra |
| Carga `wx` | Positiva hacia +X, por unidad de longitud de la barra |
| Momento flector | Se dibuja del lado de la tracción |
| Axial | Positivo en tracción |
| Reacción del suelo | Positiva hacia arriba |

## Limitaciones

- Análisis lineal elástico en 2D, sin efectos de segundo orden.
- Sección rectangular (`b × h`) de propiedades constantes en cada barra.
- El módulo de suelo varía solo linealmente; la ley exponencial de ZAPEL77P no está incluida.
- No incluye lectura de archivos `.DAT` de ZAPEL, resortes nodales ni asentamientos impuestos.
- Para vigas sobre suelo conviene subdividir las barras en varios elementos para obtener buena precisión.

> Los resultados deben verificarse con casos de solución conocida antes de usarse en un proyecto real. El software se ofrece sin garantía de ningún tipo.

## Licencia

Este trabajo se distribuye bajo la licencia **Creative Commons Atribución-CompartirIgual 4.0 Internacional (CC BY-SA 4.0)**.

[![CC BY-SA 4.0](https://licensebuttons.net/l/by-sa/4.0/88x31.png)](https://creativecommons.org/licenses/by-sa/4.0/deed.es)

**Qué significa:**

- **Compartir:** puedes copiar y redistribuir el material en cualquier medio o formato.
- **Adaptar:** puedes remezclar, transformar y construir a partir del material, incluso con fines comerciales.
- **Atribución:** debes dar crédito a los autores, incluir un enlace a la licencia e indicar si hiciste cambios.
- **CompartirIgual (SA, *ShareAlike*):** si adaptas o transformas el material, debes distribuir tus contribuciones bajo **la misma licencia** que el original.

Texto completo de la licencia: <https://creativecommons.org/licenses/by-sa/4.0/legalcode.es>

**Cómo añadir el archivo `LICENSE` al repositorio:** en GitHub pulsa **Add file → Create new file**, escribe `LICENSE` como nombre y pulsa **Choose a license template**. Elige *Creative Commons Attribution Share Alike 4.0 International* y confirma con **Commit changes**. También puedes copiar el texto desde el enlace anterior.

## Créditos

- Programa original **ZAPEL77P**: Dr. Bernardo Deschapelles.
- Versión web gráfica (ZAPEL Frame): actualizada por el Prof. Raymond Rosa Ávila.

Al reutilizar este trabajo, conserva estos créditos, enlaza la licencia e indica los cambios que hagas.
