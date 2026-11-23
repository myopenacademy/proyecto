# Reglas comunes a todos los cursos

Se suman a las de `../CLAUDE.md`. Cada curso añade las suyas (lenguaje, versiones, herramientas) en su propio `CLAUDE.md`.

Mientras no exista `kit-cursos/`, la referencia de todo lo que se dice aquí es el curso de Java original: su `PLAN-CURSO.md` (plantilla en el apartado 4, progresión y ejercicios en el 4.1, forma de trabajo en el 8) y sus herramientas, en `../../Curso Java Completo/`. Cuando exista el kit, la referencia pasa a ser `kit-cursos/` y su `FORMATO.md`.

## Reglas que no se pueden saltar

- Cada curso es la obra de referencia del autor: **la calidad y la exactitud van por delante de la velocidad**.
- Se escribe para un **principiante absoluto** en lo que trata el curso (el curso inicial no da nada por sabido; los demás dan por sabido el curso inicial y lo que digan sus requisitos).
- **No recortes**: cada módulo tiene la extensión que el tema necesite.
- **Estructura común a todos los cursos**: mismas carpetas, mismos nombres y mismo formato (`fase-NN-nombre/`, `NN-nombre.md`, `codigo/` por fase, `proyecto/` si hay proyecto evolutivo, `00-indice.md` con «## Fase NN — Título»…). Lo fija el `FORMATO.md` del kit, que sale del curso de Java original y de lo que exige la academia.
- Todos los módulos siguen la **plantilla de módulo**: Qué aprenderás · Teoría · Ejemplos · Errores típicos · Buenas prácticas · Ejercicios prácticos resueltos · Chuleta.
- Teoría, ejemplos y ejercicios van **de menor a mayor complejidad**, con **casos reales**, y los ejercicios en **cuatro niveles** (básico, intermedio, avanzado y caso real), con **soluciones completas, comentadas y explicadas**. En la sección «Ejercicios prácticos resueltos», cada ejercicio es «Ejercicio N · Título» y su solución va en `<details>` (lo exige el importador de la academia).
- **Vocabulario común:** «fichero» en todo el texto (no «archivo»), salvo en los nombres que aparecen en pantalla («Explorador de archivos», el menú «Archivo»), que se escriben tal cual. Al presentarlo por primera vez, se avisa de que son sinónimos (decidido el 9 de noviembre de 2026 en el curso inicial; es la primera regla de la guía de estilo común).
- **Teclas y atajos de teclado** con `<kbd>` (`<kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>T</kbd>`), como propone `FORMATO.md` (apartado 10.5): la academia los muestra como teclas. El curso de Java, que usa negrita, lo cambia al adaptarse (decidido el 9 de noviembre de 2026; segunda regla de la guía de estilo común).
- **Verifica versiones y APIs** contra la documentación oficial antes de escribir. Nunca inventes APIs.
- **Compila y ejecuta todo el código** antes de incluirlo. Cada programa completo se guarda en `codigo/` de su fase, enlazado desde el módulo con «📁 Código», y la verificación del kit debe pasar antes de cada commit. Las pruebas sueltas que no se publican van en `.verificacion/`, fuera de Git.
- **Nombres estables**: el temario y los nombres de fichero se cierran antes de escribir. La academia identifica cada lección por un identificador permanente; renombrar o mover un módulo es una excepción que se anota.
- Verifica **el módulo** al terminarlo y **la fase entera** al cerrarla (o si cambia algo compartido). Al cerrar cada fase: verificación entera **del último commit, como la recibirá el alumno** (`verificar_codigo.py --commit`, con Docker), enlaces de todo el curso, Mermaid, y apuntarlo en `ESTADO.md` (decidido el 9 de noviembre de 2026: en el disco del autor pueden pasar cosas que fallan en un clon, como CRLF, carpetas vacías o permisos).
- **Las verificaciones que se anotan se hacen con una copia limpia de una versión etiquetada del kit** (`git -C ../kit-cursos archive <etiqueta>` a una carpeta temporal), nunca con lo que haya en el disco de `../kit-cursos/`, que puede estar en una rama a medias. Lo que el kit aún no ha publicado espera a su versión etiquetada; una prueba con una rama del kit no cuenta como verificación (decidido por el autor el 23 de noviembre de 2026, después de que el curso de Java anotara cifras con el kit 1.1.0 a medio hacer).
- **Un commit por módulo**, y `ESTADO.md` al día al terminar cada uno.
- **Después de cada módulo, actualiza toda la documentación** del curso: índice, chuleta global, enlaces, diagramas, `ESTADO.md`, la documentación de las herramientas que cambien, plan, portada, roadmaps, módulos anteriores y proyecto, si les afecta.
- **Para al terminar cada fase** para que el autor la revise.
- **Los cursos se hacen para la academia**: si un curso necesita algo que la academia no admite, no se hace un apaño en el curso; primero se amplía la academia y `FORMATO.md` (desde sus proyectos) y después lo usa el curso.
- **Retos al final de cada fase**: opcionales, para afianzar lo aprendido mezclando varios módulos, con solución en `<details>` verificada como el resto del código. Sin seguimiento y sin bloquear nada. Su formato exacto lo fija `FORMATO.md`.
- Cada módulo dice **qué conviene saber antes**, con enlaces (aunque sean de otro curso), y termina con **preguntas de repaso**; los ejercicios llevan **pistas** plegadas antes de la solución. Su formato exacto lo fija `FORMATO.md`.
- Todo curso tiene un **proyecto para el portfolio del alumno**, aunque sea pequeño.
- Cada repositorio de curso lleva **licencia, `CONTRIBUTING.md` y `CHANGELOG.md`**, y cada versión publicada se etiqueta en Git.
- **Se trabaja en paralelo lo que haga falta**: un curso, una sola sesión o persona a la vez. Los cambios en el kit o en `FORMATO.md` se hacen solo desde `kit-cursos/`.
