# Proyecto Academia

Todo lo necesario para una academia de programación **libre, gratuita y de código abierto** que funciona como un juego con DLC: la plataforma es el juego y cada curso es una expansión que se instala, se actualiza sin perder el progreso y que cualquiera puede crear. Todo gratis: la academia y los cursos.

Esta carpeta **solo agrupa proyectos**. Cada proyecto de dentro es independiente y tiene su propio repositorio de Git, su `CLAUDE.md`, su plan y su estado. La propia carpeta es un repositorio pequeño que guarda solo la planificación común (este `README.md`, `CLAUDE.md`, `PLAN.md`, `ESTADO.md` y `Cursos/CLAUDE.md`).

## Estructura

```
Proyecto Academia/                ← planificación común (este repositorio)
├── README.md, CLAUDE.md, PLAN.md, ESTADO.md
├── Academia/                     ← proyecto: la web de la academia
└── Cursos/                       ← agrupa todo lo de los cursos
    ├── CLAUDE.md                 ← reglas comunes a todos los cursos
    ├── kit-cursos/               ← proyecto: formato y herramientas para escribir y verificar cursos
    ├── curso-inicial/            ← proyecto: el curso común que hace todo alumno
    ├── curso-java/               ← proyecto: Java de 0 a experto
    └── curso-…/                  ← un proyecto por curso
```

Hoy solo existe la planificación. Los proyectos se crean en el orden de [`PLAN.md`](PLAN.md#7-orden-de-trabajo); dónde estamos, en [`ESTADO.md`](ESTADO.md).

## Cómo se relacionan

- **Los cursos usan el kit** desde `../kit-cursos/`: una mejora del kit llega a todos los cursos.
- **La academia instala cada curso** (como un DLC) desde una versión fija de `../Cursos/<curso>/` con su importador y guarda la copia en su carpeta de contenido, fuera de Git. Nunca lee los cursos en directo.
- **Cada `CLAUDE.md` añade lo suyo** a los de las carpetas superiores: una sesión abierta en `Cursos/curso-sql/` lee las reglas generales, las de cursos y las de SQL; una abierta en `Academia/` no carga las de cursos.

## Dónde abrir cada sesión

Cada proyecto se trabaja abriendo Claude Code en su carpeta:

| Para… | Abre Claude Code en |
|---|---|
| Planificar en general, el orden, el contrato de formato o crear un proyecto nuevo | `Proyecto Academia/` |
| Trabajar en el kit | `Cursos/kit-cursos/` |
| Escribir un curso | `Cursos/curso-xxx/` |
| Trabajar en la academia | `Academia/` |

- Una sesión en un curso carga el `CLAUDE.md` de la raíz, el de `Cursos/` y el del curso; una sesión en `Academia/` carga el de la raíz y el suyo.
- **Crear un proyecto nuevo** (crear su carpeta o clonar el original) se hace desde la sesión de la raíz. En cuanto existe con su `CLAUDE.md`, se cierra esa sesión y se abre otra dentro de la carpeta del proyecto.
- **Al terminar algo importante** en un proyecto (por ejemplo, un curso publicado), se actualiza también el `ESTADO.md` de la raíz desde una sesión en `Proyecto Academia/`.

## Normas para que la carpeta se pueda copiar entera

1. **Ninguna ruta absoluta** en scripts ni documentos (nada de `/home/...`). Todo es relativo al proyecto o a esta carpeta.
2. **Lo que depende de cada máquina** (rutas de programas, claves) va en variables de entorno o en ficheros locales que no se suben a Git, nunca en el código.
3. **Lo importante vive escrito en los repositorios** (`PLAN.md`, `ESTADO.md`, `CLAUDE.md`), no solo en la memoria de una sesión. La memoria de Claude y de engram depende de la ruta de la carpeta y no viaja con ella.

Un curso suelto, copiado fuera de esta carpeta, no funciona sin `kit-cursos/` al lado: se copia siempre la carpeta entera.

## De dónde sale

Del aprendizaje de dos proyectos anteriores, que se quedan donde están como archivo y **no se modifican**:

- **Curso Java Completo** (`../Curso Java Completo/`): 21 fases, 199 módulos y 14 etapas, terminado y revisado el 6 de noviembre de 2026. De él salen el método y las herramientas (el kit), parte del curso inicial y la base de `curso-java/`.
- **Code Academy** (`../Code Academy/`): la academia construida a medida de ese curso. Es la base de `Academia/`.

Esas dos rutas relativas solo se usan para crear los proyectos nuevos; cuando estén creados, nada de aquí depende de ellas.
