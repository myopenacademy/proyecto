# Estado del Proyecto Academia

> Actualízalo al terminar cada paso del plan. Es la memoria entre sesiones: lo que no esté aquí o en `PLAN.md` no lo sabrá la sesión siguiente.

## Dónde estamos

**8 de noviembre de 2026:** planificación revisada y **paso 0 terminado**: el contrato de formato está en [`FORMATO.md`](FORMATO.md) (versión 1), en esta carpeta hasta que exista `Cursos/kit-cursos/`. La academia se llama **MyOpenAcademy**. Existe la organización `myopenacademy` en GitHub (vacía). Ningún proyecto creado todavía en `Academia/` ni en `Cursos/`.

## Siguiente paso

**Paso 1 del plan: el kit mínimo y la fase 1 del curso inicial** ([`PLAN.md`, apartados 7 y 8.2](PLAN.md#82-paso-1-el-kit-de-herramientas)). Meta final: el **pack base 1.0** (la academia más el DLC del curso inicial) publicado en GitHub; el curso de Java, como primer DLC.

1. **Desde una sesión en esta carpeta:** crear `Cursos/kit-cursos/` con su repositorio de Git, su `CLAUDE.md`, su plan y su `ESTADO.md`, y mover allí `FORMATO.md`. Después, cerrar la sesión y abrir otra dentro de `Cursos/kit-cursos/`.
2. **En el kit:** sacar del curso de Java original (solo comandos de Git de lectura) lo genérico de `herramientas/`, las plantillas (incluidos `curso.json`, `retos.md`, `LICENSE`, `CONTRIBUTING.md` y `CHANGELOG.md`) y escribir `formato_academia.py`, que comprueba `FORMATO.md`. Lo justo para el curso inicial.
3. **Desde una sesión en esta carpeta:** crear `Cursos/curso-inicial/` con su repositorio y sus ficheros; después, sesión dentro de él para cerrar con el autor el temario (31 módulos, con sus identificadores y retos de fase), escribir la fase 1 y parar para que la revise.
4. **Prueba de importación** de esa fase 1 en una copia de la academia (paso 2 del orden de trabajo).

## Decisiones del paso 0

Todas del 8 de noviembre de 2026, aprobadas por el autor. El contrato completo está en `FORMATO.md`.

- **La identidad la guarda el curso, no la academia.** Hoy Code Academy inventa los identificadores al importar (`java-03.06` sale del número del módulo; los ejercicios se reconocen por su título exacto y los nuevos reciben el siguiente número libre), y los guarda en su propio manifiesto. Con varias instalaciones y versiones eso da identificadores distintos para lo mismo. Por eso cada curso lleva un **`curso.json`** en su raíz, fuente de verdad de su estructura (id, versión, partes, fases, módulos, ejercicios, etapas y equivalencias), con **identificadores sin números** (`java.polimorfismo`), para que renumerar, mover o cambiar un título no rompa nada. Se edita a mano o con el kit, y el kit lo comprueba (la lista de `generar_indice.py` del curso de Java pasa a este fichero). El manifiesto de la academia pasa a ser interno y se genera desde `curso.json`: **hay que rehacer la parte de identidad del importador** de Code Academy. Se puede elegir el esquema ahora porque la academia empieza sin alumnos. Así la academia y los cursos solo comparten el contrato (`FORMATO.md` y el esquema de `curso.json`), con versión.
- **Enlaces entre cursos con la dirección completa de GitHub** (`https://github.com/myopenacademy/curso-inicial/blob/main/<fichero>.md#ancla`), a cualquier curso. Funcionan en GitHub; el kit los traduce a la carpeta hermana (`../curso-inicial/`) y comprueba fichero y ancla; la academia los convierte en enlace a la lección si ese curso está instalado y, si no, deja el de GitHub. Riesgo anotado: si un curso renombra un fichero, se rompen los enlaces que otros cursos tengan hacia él; el kit debería poder comprobar todos los cursos a la vez.
- **Preguntas de repaso** en «## 7. Preguntas de repaso», detrás de la chuleta (no se renumera nada en los módulos ya escritos), cada una con su respuesta en `<details>`. **Obligatorias en los cursos nuevos**; el curso de Java las declara en el campo `transicion` de `curso.json` y el kit solo avisa mientras se añaden poco a poco.
- **«Requisitos previos» pasa a «Conviene saber antes»** en la cabecera de cada módulo, porque son recomendaciones. En Java es un cambio mecánico al adaptarlo.
- **Retos de fase** en un fichero `retos.md` por fase, con su código en `codigo/retos/`. Conviene que toda fase los tenga (el kit avisa si faltan).
- **Licencias:** **MIT** para la academia, el kit y el código de los cursos; **CC BY-SA 4.0** para el texto de los cursos.
- **El curso inicial usa pseudocódigo**, no un lenguaje real. Sus retos de fase son sobre todo de herramientas, que el kit puede verificar: Git, Markdown, JSON, YAML y terminal. Idea para más adelante: un pseudocódigo ejecutable (PSeInt).
- **Nombre: MyOpenAcademy.** «Open» dice que es libre y de código abierto; «My», que es tu propia academia y se aprende por tu cuenta. No se registra la marca. Va con un subtítulo que diga que es de programación. Se descartaron Code Academy, MyCodeAcademy y academy.dev (se confunden con Codecademy o son demasiado genéricos) y CursoCode y MyCursoCode (mezclan idiomas y suenan a un solo curso).
- **Repositorios en GitHub.** Cada proyecto, su propio repositorio y su propio Git:
  - **La academia**, en la cuenta personal del autor, `santi-cast/myopenacademy` (su portfolio; comprobado libre). Es lo único de MyOpenAcademy que aparece en su perfil.
  - **Los cursos y el kit**, en la organización **`myopenacademy`** (`myopenacademy/curso-inicial`, `myopenacademy/curso-java`, `myopenacademy/kit-cursos`…), porque pertenecen a la academia. El autor la creó el 8 de noviembre de 2026 (plan gratuito, sin miembros); se gestiona desde su cuenta. La planificación común, si se sube, también ahí.
  - El **README de la academia** enlaza a todo: cursos disponibles (DLC), «Crea tu propio curso» con el kit y `FORMATO.md`, hoja de ruta y diagrama. La organización tendrá su portada con enlace de vuelta.
  - Se descartó meter los cursos dentro del repositorio de la academia (repositorio enorme, versiones mezcladas, choca con «un repositorio por proyecto» y con la idea de DLC).

## Hecho

| Fecha | Qué |
|---|---|
| 2026-11-08 | Planificación con el autor: catálogo, curso inicial, curso de Java nuevo (opción A), academia, estructura de carpetas y orden de trabajo. Resultado en `PLAN.md`. |
| 2026-11-08 | Revisión del plan con el autor. Proyecto libre, gratuito y de código abierto, de uso propio y para portfolio; academia como «juego» y cursos como «DLC» que se instalan con su versión; acceso libre con recomendaciones y roadmaps; varios usuarios con roles y configuración; diseñada para internet aunque se use en local; los cursos se hacen para la academia; versiones de cursos; retos opcionales al final de cada fase; pack base 1.0 primero; trabajo en paralelo según la gente disponible. Se revisó Code Academy (hitos H1 a H5 hechos) y otras academias (The Odin Project, Exercism, freeCodeCamp, roadmap.sh, Full Stack Open, MoureDev, midudev, Píldoras Informáticas) en busca de ideas. Resultado en `PLAN.md` y `Cursos/CLAUDE.md`. |
| 2026-11-08 | **Paso 0: contrato de formato.** Estudiados, solo leyendo, la estructura del curso de Java original y el manifiesto, el importador y la actualización de Code Academy. Escrito `FORMATO.md` (versión 1) y resueltas con el autor las decisiones 1 a 7 del apartado 10 del plan (ver «Decisiones del paso 0»). |

## Ajustes pedidos por el autor

- Mientras planifica, **solo contestar**: no lanzar comandos ni guardar o cambiar nada hasta que diga que la planificación ha terminado.
- Todos los cursos con **la misma estructura, nombres y formato**, tomando como modelo el curso de Java original; **los cursos se hacen para la academia**.
- El curso de Java nuevo y la academia se crean **copiando los originales con su historial**; los originales no se tocan.
- El curso de Java y Code Academy fueron el aprendizaje: este proyecto **aprovecha todo** lo que se pueda de ellos.
- **Todo es gratis** (la academia y los cursos): nada de pagos, precios ni partes de pago.
- **Acceso libre**: los requisitos son recomendaciones; nada se bloquea.
- La academia, **para varios usuarios con cuentas** y diseñada **como si fuera a desplegarse en internet**, aunque se use en local.
- Los **retos** van dentro de cada curso, al final de cada fase: opcionales, sin seguimiento y sin bloquear.
- **Se trabaja en paralelo lo que haga falta**: hoy el autor está solo, mañana puede haber más gente.
- Ir publicando en GitHub para que se vea el progreso del proyecto.
- Además de escribirlo aquí, **guardar las decisiones en engram** (el autor permitió `mem_save` y `mem_session_summary`; `mem_judge` sigue sin permiso).

## Pendientes del autor

Ver [`PLAN.md`, apartado 10](PLAN.md#10-decisiones-pendientes-del-autor). Las siete del paso 0 están resueltas; quedan las del curso inicial (nombre público, terminal en Windows, normas sobre la IA), las de la academia y las de más adelante.
