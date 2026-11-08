# Formato de los cursos de MyOpenAcademy

> **Borrador para revisión del autor** · versión del formato: **1** · 8 de noviembre de 2026.
> Vive aquí hasta que exista `Cursos/kit-cursos/`, que lo incluirá. Decisiones y su porqué: [`ESTADO.md`](ESTADO.md) y [`PLAN.md`, apartado 8.1](PLAN.md#81-paso-0-el-contrato-de-formato).

Este documento dice **cómo tiene que ser un curso para que MyOpenAcademy lo pueda instalar**. Está escrito para cualquiera que quiera crear un curso, no solo para el autor.

## 1. La idea

MyOpenAcademy funciona como **un juego con DLC**: la academia es el juego y cada curso es una expansión que se instala, se actualiza sin perder el progreso y que cualquiera puede crear. Todo es gratis y de código abierto.

Para que eso funcione, la academia y los cursos solo comparten **este contrato**:

- **Manda la academia.** Este formato recoge lo que la academia necesita para instalar y mostrar un curso, y **todo curso lo cumple**. Si un curso necesita algo que la academia no sabe hacer, no se hace un apaño en el curso: primero se amplía la academia y este formato, y después lo usa el curso.
- **La academia no sabe nada de ningún curso concreto** y **un curso no sabe nada del código de la academia**. Cada uno tiene su repositorio, sus versiones y su ritmo.
- **Un curso se lee también sin la academia**, directamente en GitHub: todo es Markdown con enlaces que funcionan.
- **El formato tiene versión** (el campo `formato` de [`curso.json`](#3-cursojson-la-identidad-del-curso)). Solo se cambia desde el proyecto del kit, y la academia sigue sabiendo leer las versiones anteriores.

En lo que sigue, **«debe»** es obligatorio (la comprobación falla si no se cumple) y **«conviene»** es una recomendación (la comprobación avisa, pero no falla).

## 2. Estructura de un repositorio de curso

```
curso-xxx/
├── curso.json                ← identidad y estructura del curso (apartado 3)
├── README.md                 ← portada: qué es, a quién va, cómo usarlo, versiones, requisitos
├── LICENSE                   ← licencias (apartado 12)
├── CONTRIBUTING.md           ← cómo proponer cambios
├── CHANGELOG.md              ← qué cambia en cada versión
├── 00-indice.md              ← índice completo; se genera desde curso.json
├── 99-chuleta-global.md      ← todas las chuletas; se genera
├── ROADMAP.md                ← ruta de aprendizaje del curso (conviene)
├── RUTA-MINIMA.md            ← ruta mínima, si el curso la tiene (opcional)
├── glosario.md               ← solo en el curso inicial (apartado 9)
├── fase-01-nombre/
│   ├── 01-nombre.md          ← un fichero por módulo
│   ├── 02-nombre.md
│   ├── retos.md              ← retos opcionales de la fase (apartado 6)
│   ├── img/                  ← imágenes de la fase (si hay)
│   └── codigo/               ← código de la fase (apartado 7)
├── fase-02-nombre/
│   └── …
└── proyecto/                 ← etapas del proyecto, si el curso lo hace por etapas (apartado 8)
    ├── 01-nombre.md
    └── codigo/
```

- **Cada curso es su propio repositorio de Git.** Los cursos oficiales viven en la organización [`myopenacademy`](https://github.com/myopenacademy) de GitHub, con el nombre `curso-<nombre>` (`myopenacademy/curso-java`); la academia está en [`santi-cast/myopenacademy`](https://github.com/santi-cast/myopenacademy). Un curso de otra persona puede estar en cualquier cuenta: basta con que cumpla este formato.
- Carpetas y ficheros **numerados** para que aparezcan en orden, con nombres en **minúsculas, sin tildes, sin eñes y sin espacios** (guiones en su lugar).
- **El número y el nombre del fichero no son la identidad del módulo**: la identidad está en `curso.json`. Un fichero se puede renombrar o mover a otra fase; basta con actualizar su ruta en `curso.json`.
- Las herramientas internas de quien escribe el curso (verificación, generadores) no son parte del curso: no se instalan en la academia. Si el curso las guarda en su repositorio, van en `herramientas/`, que la academia ignora.

## 3. `curso.json`: la identidad del curso

Es la **fuente de verdad** de la estructura del curso: qué fases, módulos, ejercicios y etapas tiene, en qué orden, en qué fichero está cada uno y con qué identificador. La academia lo lee para instalar el curso; el índice, la chuleta global y los roadmaps del curso se generan a partir de él. Se edita a mano o con las herramientas del kit, y **el kit lo comprueba siempre**: cambiar el título de un ejercicio o añadir uno nuevo son cosas distintas, y solo quien escribe el curso sabe cuál de las dos ha hecho.

### 3.1. Ejemplo

```json
{
  "formato": 1,
  "tipo": "curso",
  "id": "java",
  "titulo": "Java de 0 a experto",
  "descripcion": "De no saber programar a trabajar con Java y Spring Boot.",
  "version": "2.0.0",
  "idioma": "es",
  "repositorio": "https://github.com/myopenacademy/curso-java",
  "conviene_saber_antes": ["inicial"],
  "partes": [
    {
      "id": "java.parte.lenguaje",
      "titulo": "El lenguaje Java",
      "fases": ["java.fase.fundamentos", "java.fase.poo"]
    }
  ],
  "fases": [
    {
      "id": "java.fase.poo",
      "carpeta": "fase-03-poo",
      "titulo": "Programación orientada a objetos",
      "retos": "fase-03-poo/retos.md",
      "modulos": [
        {
          "id": "java.polimorfismo",
          "fichero": "fase-03-poo/04-polimorfismo.md",
          "titulo": "Polimorfismo",
          "ejercicios": [
            { "id": "java.polimorfismo.compila", "titulo": "¿Compila? ¿Qué pasa al ejecutar?" },
            { "id": "java.polimorfismo.parking", "titulo": "Las tarifas del parking" }
          ]
        }
      ]
    }
  ],
  "proyecto": {
    "tipo": "etapas",
    "titulo": "Mi Biblioteca",
    "etapas": [
      { "id": "java.etapa.consola", "fichero": "proyecto/01-version-consola.md", "titulo": "Versión de consola" }
    ]
  },
  "equivalencias": []
}
```

### 3.2. Campos

| Campo | Qué es |
|---|---|
| `formato` | Versión de este documento que cumple el curso. Hoy, `1`. |
| `tipo` | Tipo de paquete. Hoy solo existe `"curso"`; el campo está para poder añadir otros en el futuro. |
| `id` | Identificador del curso: corto, en minúsculas (`inicial`, `java`, `sql`). Es el prefijo de todos los demás identificadores. No cambia nunca. |
| `titulo`, `descripcion` | Lo que muestra la academia en el catálogo. |
| `version` | Versión del curso (apartado 11). Coincide con la etiqueta de Git que se instala. |
| `idioma` | Idioma del contenido (`es`). |
| `repositorio` | Dirección del repositorio en GitHub. La usan los enlaces entre cursos y el botón «Mejorar esta lección». |
| `conviene_saber_antes` | Cursos que se recomienda haber hecho antes (sus `id`). Son recomendaciones: nada se bloquea. |
| `partes` | Opcional. Tramos con nombre del curso, cada uno con la lista ordenada de sus fases. Sirven para orientarse y como piezas de los roadmaps. Si hay partes, cada fase está exactamente en una. |
| `fases` | Las fases en orden. Cada una con su `id`, su `carpeta`, su `titulo` (el mismo de `00-indice.md`), sus `modulos` en orden y, si tiene retos, la ruta de su `retos.md`. |
| `modulos` | Cada módulo con su `id`, su `fichero`, su `titulo` (el mismo del encabezado del fichero) y sus `ejercicios` en orden. Un módulo todavía sin escribir lleva `"disponible": false` y no tiene fichero. |
| `ejercicios` | Cada ejercicio con su `id` y su `titulo`: el texto exacto que sigue a «Ejercicio N · » en el módulo (apartado 5.4). |
| `proyecto` | El proyecto para el portfolio del alumno (apartado 8). |
| `equivalencias` | Qué fue de los identificadores que ya no existen (apartado 11.2). |
| `transicion` | Opcional. Reglas de este formato que el curso todavía no cumple y que, mientras tanto, la comprobación trata como avisos y no como errores. Solo para cursos escritos antes de este formato. Hoy solo admite `"preguntas-de-repaso"` (el curso de Java lleva `"transicion": ["preguntas-de-repaso"]` mientras las añade). |

### 3.3. Identificadores

- **Forma:** el `id` del curso, un punto y un nombre: `java.polimorfismo`, `java.fase.poo`, `java.etapa.consola`, `java.parte.lenguaje`. Los ejercicios cuelgan de su módulo: `java.polimorfismo.parking`. Solo letras minúsculas sin tildes, cifras, guiones y puntos.
- **Sin números de posición.** El identificador no dice en qué fase ni en qué orden está el módulo, así que moverlo o renumerarlo no lo cambia.
- **Permanentes.** Una vez publicado, un identificador **no cambia ni se reutiliza nunca**: el progreso de los usuarios va unido a él. Cambiar el título de un módulo o de un ejercicio es cambiar su `titulo`, conservando el `id`.
- **Únicos** dentro del curso; con el prefijo del curso, también en toda la academia. Por eso **el `id` del curso tiene que ser único en la academia**: la academia no instala un curso cuyo `id` ya usa otro curso instalado. Quien cree un curso por su cuenta conviene que elija un `id` que no se confunda con los oficiales (por ejemplo, `ana-fotografia` mejor que `fotografia`).
- **Cómo se eligen la primera vez:** del nombre del fichero sin número para los módulos (`04-polimorfismo.md` → `java.polimorfismo`) y del título para los ejercicios (`Las tarifas del parking` → `java.polimorfismo.las-tarifas-del-parking`), en minúsculas, sin tildes y con guiones. Las herramientas del kit los proponen así. Después ya no cambian aunque cambie el fichero o el título.

## 4. Ficheros especiales

- **`README.md`**: portada del curso. Qué es, a quién va dirigido, qué conviene saber antes, cómo usarlo (en orden o por libre), versiones de las herramientas, requisitos de software y licencia.
- **`LICENSE`**, **`CONTRIBUTING.md`** y **`CHANGELOG.md`**: obligatorios (apartados 11 y 12).
- **`00-indice.md`**: el índice completo, con un encabezado `## Fase NN — Título` por fase y enlaces a todos los módulos, con su nivel y su tiempo. Se genera desde `curso.json`; no se edita a mano.
- **`99-chuleta-global.md`**: la sección «Chuleta» de todos los módulos, reunida. Se genera.
- **`ROADMAP.md`** (conviene) y **`RUTA-MINIMA.md`** (opcional): la ruta de aprendizaje del propio curso y, si la hay, la ruta mínima.

## 5. El módulo

### 5.1. Plantilla

Todos los módulos siguen **exactamente** esta estructura, para que el lector sepa siempre dónde buscar y la academia pueda leerlos:

```markdown
# 03.04 Polimorfismo

> **Versiones:** Java 25
> **Conviene saber antes:** [03.03 Herencia](03-herencia.md)
> **Tiempo estimado:** 5 horas
> **Nivel:** Intermedio · Núcleo

## Qué aprenderás

## 1. Teoría

## 2. Ejemplos de código

## 3. Errores típicos

## 4. Buenas prácticas

## 5. Ejercicios prácticos resueltos

## 6. Chuleta

## 7. Preguntas de repaso

---
⬅️ [Anterior: …](…) · 📚 [Índice](../00-indice.md) · ➡️ [Siguiente: …](…)
```

- El **título** es `# NN.NN Título`, con el mismo título que `curso.json`. El número es solo para orientarse.
- Las secciones van **en este orden y con estos nombres exactos**. Dentro de cada una, los subapartados se numeran (`### 1.1.`, `### 1.2.`…).

### 5.2. Cabecera

Las líneas de la cita del principio son los **datos del módulo** que lee la academia:

| Línea | Obligatoria | Qué lleva |
|---|---|---|
| `**Versiones:**` | No | Las versiones de las herramientas que usa el módulo, si aplican. |
| `**Conviene saber antes:**` | Sí | Enlaces a los módulos que se recomienda haber estudiado, de este curso o de otro (apartado 10.2), separados por ` · `. Si no hace falta nada, `Nada`. Son recomendaciones: nada se bloquea. |
| `**Tiempo estimado:**` | Sí | Horas de estudio, incluidos los ejercicios: `5 horas`, `1 hora`, `1,5 horas`. |
| `**Nivel:**` | Sí | `Básico`, `Intermedio` o `Avanzado`, seguido de ` · ` y `Núcleo` (imprescindible) o `Ampliación` (para profundizar más adelante). |

### 5.3. «Qué aprenderás»

Lista de objetivos concretos del módulo. Es lo primero que ve quien entra suelto a un módulo: con esto y con «Conviene saber antes» decide si el módulo es para él.

### 5.4. «Ejercicios prácticos resueltos»

```markdown
## 5. Ejercicios prácticos resueltos

### 🟢 Básico

#### Ejercicio 1 · Las tarifas del parking

Enunciado…

<details>
<summary>Pista 1</summary>

…

</details>

<details>
<summary>Ver solución</summary>

Razonamiento, código, salida y explicación…

</details>
```

- Los ejercicios se agrupan en cuatro niveles, en este orden y con estos encabezados: `### 🟢 Básico`, `### 🟡 Intermedio`, `### 🔴 Avanzado` y `### 🏆 Caso real`.
- Cada ejercicio es `#### Ejercicio N · Título`. El **título** (lo que sigue a «Ejercicio N · ») debe coincidir **exactamente** con el `titulo` de ese ejercicio en `curso.json`, y en el mismo orden. N es solo la posición: no identifica al ejercicio.
- **Pistas** (conviene): cero, una o varias, cada una en su `<details>` con `<summary>Pista N</summary>`, **antes** de la solución.
- **Solución** (obligatoria): un `<details>` con `<summary>Ver solución</summary>`, **después** de las pistas. Completa, comentada y explicada.
- Deja una línea en blanco después de `<summary>…</summary>` y antes de `</details>`, para que el Markdown de dentro se vea bien en GitHub.

### 5.5. «Preguntas de repaso»

```markdown
## 7. Preguntas de repaso

1. ¿Qué diferencia hay entre el tipo de la variable y el tipo del objeto?

   <details>
   <summary>Ver respuesta</summary>

   El tipo de la variable decide qué métodos se pueden llamar… Lo tienes en [1.2. El tipo de la variable y el tipo del objeto](#12-el-tipo-de-la-variable-y-el-tipo-del-objeto).

   </details>

2. …
```

- Una lista numerada de preguntas de autoevaluación, cada una con su respuesta en `<details>` con `<summary>Ver respuesta</summary>`.
- Conviene que cada respuesta **enlace al apartado del módulo** donde se explica.
- Sin nota ni seguimiento: son para que el alumno compruebe si lo ha entendido.
- **Obligatorias** en los cursos nuevos. En los cursos que ya estaban escritos antes de este formato (el de Java), la comprobación **solo avisa** mientras se añaden poco a poco, si el curso lo declara en el campo `transicion` de `curso.json`.

## 6. Los retos de cada fase

Al final de cada fase, un fichero **`retos.md`** con retos **opcionales** para afianzar lo aprendido. Mezclan lo de varios módulos de la fase. **No tienen seguimiento** (la academia no guarda si se han hecho) y **no bloquean nada**.

```markdown
# Retos de la fase 03 — Programación orientada a objetos

> **Conviene saber antes:** los módulos de la fase.
> **Tiempo estimado:** 4 horas

Introducción: qué se practica y cómo abordarlos…

## Reto 1 · El inventario de una ferretería

Enunciado…

<details>
<summary>Pista 1</summary>

…

</details>

<details>
<summary>Ver solución</summary>

…

</details>
```

- El fichero se llama siempre `retos.md` (queda el último de la fase al ordenar) y su ruta se declara en `curso.json`, en el campo `retos` de la fase.
- Cada reto es `## Reto N · Título`, con pistas y solución como los ejercicios (apartado 5.4).
- Su código va en `codigo/retos/reto-NN-nombre/` de la fase y se verifica como el resto.
- No es un módulo: no tiene identificador ni aparece en `modulos`. La academia lo muestra al final de su fase como extra opcional.
- Conviene que **cada fase tenga sus retos**; la comprobación avisa si falta.

## 7. El código

- Cada fase tiene una carpeta `codigo/` con una subcarpeta por módulo, con el **mismo nombre que su fichero** sin `.md`. Dentro, `ejemplos/` y `ejercicios/`.
- **Una carpeta por ejemplo o solución**, nombrada con el número de su apartado y una descripción: `ejemplos/2.1-upcasting/`, `ejercicios/ej02-tarifas-parking/`.
- Solo llevan carpeta los programas **completos**; los fragmentos se quedan en el texto.
- En el módulo, debajo de cada programa completo, el enlace a su carpeta:
  `📁 **Código:** [`codigo/04-polimorfismo/ejemplos/2.1-upcasting/`](codigo/04-polimorfismo/ejemplos/2.1-upcasting/)`
- El bloque del módulo y el fichero de `codigo/` deben ser **idénticos**.
- **Nombres reservados** junto a la solución de cada ejercicio, para la corrección automática futura: `partida/` (código de partida que se da al alumno) y `pruebas/` (pruebas que comprueban su solución). Hoy no los usa nadie, pero no se pueden usar para otra cosa.
- La academia ofrece cada carpeta enlazada como descarga en ZIP.

## 8. El proyecto para el portfolio del alumno

Todo curso **debe** tener un proyecto con el que el alumno termine teniendo algo que enseñar, aunque sea pequeño. Se declara en `curso.json`, en el campo `proyecto`, de una de estas dos formas:

- **Por etapas** (`"tipo": "etapas"`): un proyecto que crece a lo largo del curso, en la carpeta `proyecto/`, con un fichero por etapa y su código en `proyecto/codigo/`. Cada etapa tiene su `id`, su `fichero` y su `titulo`. Las etapas no son módulos: la academia las muestra en su propia sección, con su propio seguimiento.
- **Como un módulo final** (`"tipo": "modulo"`, con `"modulo": "inicial.primer-repositorio"`): un módulo del curso que es el proyecto. Es el caso del curso inicial.

## 9. El glosario

- Hay **un glosario común**, `glosario.md`, en la raíz del **curso inicial**. Los términos se definen una vez y los demás cursos enlazan a la definición en vez de volver a explicarla.
- Un encabezado `## Letra` por letra y un `### Término` por término, en orden alfabético.
- Para enlazar a un término desde otro curso se usa un enlace entre cursos (apartado 10.2): `https://github.com/myopenacademy/curso-inicial/blob/main/glosario.md#api`.

## 10. Enlaces, imágenes y diagramas

### 10.1. Dentro del mismo curso

- Enlaces **relativos**, para que funcionen en cualquier editor y en GitHub: `[03.03 Herencia](03-herencia.md)`, `[el índice](../00-indice.md)`, `[1.2](#12-el-tipo-de-la-variable-y-el-tipo-del-objeto)`.
- Las anclas son las que genera GitHub a partir del encabezado.
- Todo enlace debe llevar a un fichero o carpeta que exista y, si tiene ancla, a un encabezado que exista.

### 10.2. A otro curso

- Con la **dirección completa de GitHub** del fichero, en la rama `main`:
  `[Git: fundamentos](https://github.com/myopenacademy/curso-inicial/blob/main/fase-05-git-y-github/01-git-fundamentos.md#qué-es-un-commit)`
- **Funciona en GitHub tal cual.** El kit la traduce a la carpeta hermana del curso (`../curso-inicial/`) y comprueba que el fichero y el ancla existen. La academia la convierte en un enlace a la lección si ese curso está instalado; si no, deja el enlace a GitHub.
- Se puede enlazar a **cualquier curso**: hacia atrás (lo que conviene saber antes) y hacia delante (por ejemplo, el curso inicial dice qué curso enseña cada pieza de una aplicación). Si la carpeta hermana del curso enlazado no está en la máquina de quien escribe, la comprobación avisa de que no ha podido revisar ese enlace.

### 10.3. Imágenes

- Solo imágenes **PNG, JPG o SVG** guardadas en el propio curso (en la carpeta `img/` de la fase), con enlace relativo y **texto alternativo** que describa la imagen: `![Diagrama de la herencia de Empleado](img/herencia.svg)`.
- Nada de imágenes de otras webs ni incrustadas (`data:`).
- Los SVG, legibles con fondo claro y oscuro.

### 10.4. Diagramas Mermaid

- En bloques ` ```mermaid `, que GitHub y la academia dibujan.
- Sin negrita ni cursiva en las etiquetas, y solo las entidades `&quot;`, `&lt;`, `&gt;` y `&amp;`.
- Sin directivas, *frontmatter*, interacciones, imágenes ni estilos con `url()` o `@import`: la academia muestra esos diagramas como código.
- Conviene acompañar los diagramas importantes de una frase que diga lo mismo en texto, para quien no pueda verlos.

### 10.5. HTML

Solo el HTML que necesita este formato: `<details>` y `<summary>`. El resto se escribe en Markdown (tablas, tachado con `~~texto~~`, imágenes).

- El HTML de formato sin efecto (`<span>`, `<div>`, `<u>`…) la academia lo quita al instalar y deja su texto: es un aviso.
- Scripts, marcos, manejadores de eventos (`onclick`…), imágenes escritas en HTML y atributos desconocidos **hacen fallar la instalación**: es un error.

## 11. Versiones del curso

### 11.1. Versión y registro de cambios

- La `version` de `curso.json` sigue el esquema `MAYOR.MENOR.PARCHE`:
  - **PARCHE** (`2.0.1`): erratas y mejoras de texto o de código, sin cambiar la estructura.
  - **MENOR** (`2.1.0`): contenido nuevo (módulos, ejercicios, retos, etapas) sin quitar ni cambiar identificadores.
  - **MAYOR** (`3.0.0`): cambios de estructura con equivalencias, o una edición nueva del curso.
- Cada versión publicada se **etiqueta en Git** con su número (`v2.1.0`), y esa etiqueta es lo que se instala en la academia.
- `CHANGELOG.md` dice qué cambia en cada versión, de la más nueva a la más antigua.

### 11.2. Equivalencias

Cuando un identificador publicado deja de existir, `curso.json` dice qué fue de él, para que la academia traslade el progreso de los usuarios:

```json
"equivalencias": [
  { "desde": "2.0.0", "antes": "java.colecciones", "ahora": ["java.listas", "java.mapas"] },
  { "desde": "2.0.0", "antes": "java.applets", "ahora": [], "motivo": "Tecnología retirada" }
]
```

- **Dividir** un módulo: `ahora` lleva los nuevos. **Unir** varios: una entrada por cada uno, con el mismo destino. **Retirar**: `ahora` vacío y un `motivo`.
- Las equivalencias no se borran nunca: alguien puede actualizar desde una versión muy antigua.
- Cambiar el título, el fichero, la fase o el orden **no** necesita equivalencia: el identificador no cambia.

## 12. Licencias

Salvo que el curso diga otra cosa en su `LICENSE`, los cursos de MyOpenAcademy usan:

- **CC BY-SA 4.0** para el texto: cualquiera puede usarlo y adaptarlo citando la autoría, y lo que publique a partir de él lo comparte con la misma licencia.
- **MIT** para el código (`codigo/`, `proyecto/codigo/`).

## 13. Comprobación

La comprobación del kit (`formato_academia.py`) revisa que un curso cumple este formato **antes de instalarlo**. Cada error dice el fichero, la línea y qué falta (por ejemplo, «`fase-03-poo/04-polimorfismo.md:1165`: falta la solución del ejercicio 4»). Comprueba:

- `curso.json`: campos, identificadores (forma, unicidad, que no desaparezca ninguno publicado sin equivalencia; para saberlo compara con la última versión etiquetada) y que cada fichero declarado existe y cada fichero de módulo está declarado.
- Cada módulo: título, cabecera, secciones en orden, ejercicios con sus títulos iguales a `curso.json`, solución de cada ejercicio, preguntas de repaso.
- Retos, etapas, glosario y proyecto.
- Enlaces del mismo curso y entre cursos (con sus anclas), imágenes, diagramas y HTML.
- Ficheros obligatorios.

**Errores** (no se instala) frente a **avisos** (se instala, pero conviene corregirlo): lo que este documento dice con «debe» es un error, y lo que dice con «conviene», un aviso.

## 14. Lo que vive en la academia, no en los cursos

Para que los cursos no dependan unos de otros, algunas cosas son de la academia:

- **Roadmaps entre cursos** (por ejemplo, «Backend con Java: inicial → Java → SQL → Git a fondo»): ficheros de datos en el repositorio de la academia, que nombran cursos, partes, fases o módulos por su identificador. Los roadmaps de dentro de un curso siguen en el curso (`ROADMAP.md`).
- **La lista de cursos instalados** y su versión.
- **El curso de ejemplo** que usan las pruebas de la academia y que sirve de modelo para crear un curso nuevo.

## 15. Cambiar este formato

- Se cambia **solo desde el proyecto del kit** (`Cursos/kit-cursos/`), nunca desde un curso ni desde la academia por su cuenta.
- Cada cambio sube la versión del formato (el campo `formato`), se anota qué cursos hay que poner al día y la academia sigue sabiendo leer las versiones anteriores.
- Si un curso necesita algo nuevo, primero se amplía la academia y este formato, y después lo usa el curso.
