# Estado del Proyecto Academia

> Actualízalo al terminar cada paso del plan. Es la memoria entre sesiones: lo que no esté aquí o en `PLAN.md` no lo sabrá la sesión siguiente.

## Dónde estamos

**9 de noviembre de 2026.** Paso 0 terminado (contrato en `Cursos/kit-cursos/FORMATO.md`, versión 1). La academia se llama **MyOpenAcademy**; existe la organización `myopenacademy` en GitHub (vacía). Se trabaja en **tres sesiones a la vez**, una por proyecto, coordinadas por el autor con los bloques 📣 que prepara cada sesión:

| Proyecto | Dónde va | Dónde sigue |
|---|---|---|
| `Cursos/kit-cursos/` | Hecho todo lo que el curso inicial necesita hasta su fase 5: `formato_academia.py`, índice, chuleta, Mermaid (con la versión de la academia), el verificador de código con la terminal de Docker (Ubuntu en español, Git como en Ubuntu, bash 3.2), `reemplazar.py` y `declarar_ejercicios.py`. Pendientes: `curl` con servidor local (fase 6 del curso), comparar CSV con JSON (reto de la fase 4) y ampliar el curso de ejemplo para la academia | Su `ESTADO.md` y `PLAN.md` |
| `Cursos/curso-inicial/` | **Fases 1 y 2 aprobadas por el autor** (con segunda opinión de la sesión de la raíz). Fase 3 (la primera con bash) en escritura | Su `ESTADO.md` y `PLAN-CURSO.md` |
| `Academia/` | Prueba de importación de la fase 1 hecha (el formato encaja; el trabajo está en el importador). **Plan nuevo** con los hitos H6 a H11 hasta el pack base 1.0 (unos 20 días). **H7 en marcha** (cursos como DLC), en la rama `feat/h7-cursos-dlc` | Su `ESTADO.md` y `PLAN.md` |

## Siguiente paso

Seguir con los tres proyectos en paralelo hasta el **pack base 1.0** (la academia más el DLC del curso inicial, publicado en GitHub); después, el curso de Java como primer DLC. Lo que queda en la raíz: anotar aquí lo que valga para todo el proyecto (guía de estilo común en `Cursos/CLAUDE.md`, decisiones generales en `PLAN.md`) y revisar cada fase del curso antes que el autor si lo pide.

Reglas para que no se pisen: `FORMATO.md` solo se cambia desde el kit; ninguna sesión toca el repositorio de otra; lo que una necesite de otra se anota en su `ESTADO.md` y se avisa al autor con un bloque 📣. ⚠️ La academia no se arranca a la vez que el Code Academy original (mismo puerto); el autor estudia Java en el original mientras tanto.

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

## Decisiones del curso inicial que valen para todo el proyecto

Tomadas el 8 de noviembre de 2026 en la sesión del curso inicial y anotadas aquí (`PLAN.md`, apartado 10, decisiones 8 a 10):

- **Nombre público del curso inicial:** «Fundamentos para programar».
- **Bash para todos**, con Git Bash en Windows y WSL como alternativa; **en macOS, solo lo que funciona en bash 3.2** (su versión), avisando de los comandos que cambian entre macOS y Linux. **Salidas en español** y **rama `main`** en Git. **Afecta al curso de Java**: al adaptarlo, pasar de PowerShell y bash lado a lado a solo bash, enlazando al inicial (`PLAN.md`, apartado 6.3).
- **Cinco normas sobre el uso de la IA para toda la academia** (`PLAN.md`, decisión 10).

## Hecho

| Fecha | Qué |
|---|---|
| 2026-11-08 | Planificación con el autor: catálogo, curso inicial, curso de Java nuevo (opción A), academia, estructura de carpetas y orden de trabajo. Resultado en `PLAN.md`. |
| 2026-11-08 | Revisión del plan con el autor. Proyecto libre, gratuito y de código abierto, de uso propio y para portfolio; academia como «juego» y cursos como «DLC» que se instalan con su versión; acceso libre con recomendaciones y roadmaps; varios usuarios con roles y configuración; diseñada para internet aunque se use en local; los cursos se hacen para la academia; versiones de cursos; retos opcionales al final de cada fase; pack base 1.0 primero; trabajo en paralelo según la gente disponible. Se revisó Code Academy (hitos H1 a H5 hechos) y otras academias (The Odin Project, Exercism, freeCodeCamp, roadmap.sh, Full Stack Open, MoureDev, midudev, Píldoras Informáticas) en busca de ideas. Resultado en `PLAN.md` y `Cursos/CLAUDE.md`. |
| 2026-11-08 | **Paso 0: contrato de formato.** Estudiados, solo leyendo, la estructura del curso de Java original y el manifiesto, el importador y la actualización de Code Academy. Escrito `FORMATO.md` (versión 1) y resueltas con el autor las decisiones 1 a 7 del apartado 10 del plan (ver «Decisiones del paso 0»). |
| 2026-11-09 | Guía de estilo común en `Cursos/CLAUDE.md`: «fichero» y teclas con `<kbd>`. **Fase 2 del curso inicial aprobada** tras la segunda opinión (tres precisiones). La academia: prueba de importación hecha, plan nuevo H6 a H11 (unos 20 días, anotado en el apartado 9 del plan general) y H7 empezado, con un único curso de ejemplo en el kit. |
| 2026-11-08 | **Fase 1 del curso inicial aprobada por el autor** tras la revisión de conjunto, los recortes y una segunda opinión completa. Creada `Academia/` clonando Code Academy con su historial (sin remoto), con su `CLAUDE.md` y su `ESTADO.md`, para la prueba de importación. |
| 2026-11-08 | Anotadas en la raíz las decisiones 8 a 10 del curso inicial (nombre público, bash para todos, normas sobre la IA). |
| 2026-11-08 | **Paso 1 empezado:** creados `Cursos/kit-cursos/` (con `FORMATO.md` movido desde la raíz) y `Cursos/curso-inicial/` (con su plan y el temario de 31 módulos con la ruta de origen de cada módulo adaptado), cada uno con su repositorio, `CLAUDE.md`, plan, `ESTADO.md`, `README.md` y `.gitignore`. |

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
