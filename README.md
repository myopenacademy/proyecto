# Proyecto Academia

Todo lo necesario para la academia online de programación: la web de la academia y los cursos que publica.

Esta carpeta **solo agrupa proyectos**. Cada proyecto de dentro es independiente y tiene su propio repositorio de Git, su `CLAUDE.md`, su plan y su estado. La propia carpeta es un repositorio pequeño que guarda solo la planificación común (este `README.md`, `CLAUDE.md`, `PLAN.md`, `ESTADO.md` y `Cursos/CLAUDE.md`).

## Estructura

```
Proyecto Academia/                ← planificación común (este repositorio)
├── README.md, CLAUDE.md, PLAN.md, ESTADO.md
├── Academia/                     ← proyecto: la web de la academia
└── Cursos/                       ← agrupa todo lo de los cursos
    ├── CLAUDE.md                 ← reglas comunes a todos los cursos
    ├── kit-cursos/               ← proyecto: herramientas internas para escribir y verificar cursos
    ├── curso-inicial/            ← proyecto: el curso común que hace todo alumno
    ├── curso-java/               ← proyecto: Java de 0 a experto
    └── curso-…/                  ← un proyecto por curso
```

Hoy solo existe la planificación. Los proyectos se crean en el orden de [`PLAN.md`](PLAN.md#7-orden-de-trabajo); dónde estamos, en [`ESTADO.md`](ESTADO.md).

## Cómo se relacionan

- **Los cursos usan el kit** desde `../kit-cursos/`: una mejora del kit llega a todos los cursos.
- **La academia importa cada curso** desde un commit fijo de `../Cursos/<curso>/` con su importador y guarda la copia en su carpeta de contenido. Nunca lee los cursos en directo.
- **Cada `CLAUDE.md` añade lo suyo** a los de las carpetas superiores: una sesión abierta en `Cursos/curso-sql/` lee las reglas generales, las de cursos y las de SQL; una abierta en `Academia/` no carga las de cursos.

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
