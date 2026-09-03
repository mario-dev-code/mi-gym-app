# FORJA — Mis Rutinas de Gym

## Qué hace la app

Es una app web (marca: "Forja") con tres secciones, accesibles por pestañas arriba:

1. **Rutinas**: crear rutinas (por ejemplo "Pierna" o "Pecho y tríceps"), añadir ejercicios a cada una con peso, series/reps y notas, marcar variantes del mismo ejercicio (por ejemplo si se hace en otro gimnasio o con otra máquina), y marcar qué rutinas se completaron cada semana. También tiene un panel de **copia de seguridad** (exportar/importar) para descargar todos los datos como un archivo `.json` y poder restaurarlos en otro navegador o dispositivo.
2. **Proteína**: calculadora de macros. Tiene una base de datos de ~100 alimentos cotidianos (pollo, atún, arroz, huevo, legumbres, frutas, verduras, lácteos, suplementos, etc.) con proteína/carbohidratos/grasas/calorías por 100 g. Se busca un alimento, se añade con una ración por defecto (editable en gramos) y se suma automáticamente a un resumen del día, comparado con un objetivo de proteína calculado a partir del peso del usuario y un ratio g/kg elegido.
3. **Ejercicios**: biblioteca de ~40 ejercicios recomendados, organizados por grupo muscular (Pecho, Espalda, Pierna, Hombro, Bíceps, Tríceps, Core, Glúteo) con series/reps sugeridas y un consejo de ejecución. Cada ejercicio se puede añadir con un clic directamente a una de las rutinas ya creadas.

Todos los datos se guardan localmente en el navegador (`localStorage`), no hay servidor ni base de datos externa. Las comidas del día de la calculadora se reinician solas cada día nuevo (se guardan bajo la clave `gym-nutricion`, junto con la fecha). Por eso los datos solo persisten en el mismo navegador/dispositivo (no se sincronizan entre varios); para eso está la copia de seguridad exportable.

## Estilo visual

Pensado para parecer un producto real, no un prototipo:

- Fondo oscuro con varias capas: un degradado de base, 3 "manchas" de color (naranja/ámbar/violeta) animadas muy lentamente de fondo (`.orb-1/2/3`), una rejilla sutil y un grano/ruido muy ligero. Todo desactivable automáticamente si el usuario tiene activado "reducir movimiento" en su sistema.
- Color de acento: naranja (con un segundo tono ámbar de apoyo para degradados).
- Tarjetas con fondo semitransparente + `backdrop-filter: blur()` (efecto "glass").
- Tipografía en mayúsculas y negrita para títulos y nombres de rutina/ejercicio (fuente Oswald); el cuerpo de texto usa Inter.
- Sección "hero" al principio de cada pestaña con título grande, texto de apoyo y estadísticas rápidas.
- Avisos flotantes ("toasts") abajo en vez de `alert()` del navegador.
- Anillo de progreso circular (SVG) para la proteína del día.

## Archivos principales

- `entreno.html` es el archivo principal de la app (todo el HTML, CSS y JS está en ese único archivo).
- `index.html` existe solo para redirigir automáticamente a `entreno.html` en cuanto se abre (así el link raíz del proyecto lleva directo a la app).

## Modo "mis datos" (oculto en la versión pública)

El botón para cargar las rutinas/ejercicios personales del usuario (`SAMPLE_ROUTINES_DATA` en el JS) está oculto por defecto porque la app está pensada para publicarse/compartirse y ese botón no debe verlo cualquier visitante.

- Para verlo: abrir la app añadiendo `#misdatos` al final de la URL (ej. `entreno.html#misdatos`). Queda activado también en futuras visitas (se guarda en `localStorage` bajo la clave `gym-dev-mode`).
- Para volver a ocultarlo: abrir la app con `#publico` al final de la URL.

## Despliegue (Vercel)

La app está publicada en: **https://mi-gym-app-inky.vercel.app**

- Proyecto de Vercel: `mario-dev1/mi-gym-app` (cuenta de Vercel iniciada con Google).
- El repositorio de GitHub (`mario-dev-code/mi-gym-app`) está conectado al proyecto de Vercel (se instaló la GitHub App "Vercel" con acceso a ese repo desde `github.com/settings/installations`). Esto significa que **cada `git push` a la rama `main` despliega solo, automáticamente** — no hace falta ejecutar ningún comando de despliegue a mano.
- Este equipo tiene instalados Node.js y el CLI de Vercel (`npm install -g vercel`) por si algún día hiciera falta desplegar manualmente (`vercel deploy --prod`), aunque con el repo conectado no debería ser necesario.
- La carpeta `.vercel/` (config local del CLI) está en `.gitignore` y no se sube al repositorio.

## Sobre mí (el usuario)

Soy principiante total en programación. Las explicaciones deben ser sencillas, paso a paso, y sin dar por hecho conocimientos previos (ni de programación en general ni de términos técnicos).

## Recordatorio de flujo de trabajo

Después de cualquier cambio en este proyecto, hay que hacer commit y push a GitHub (rama `main`). Con el repo conectado a Vercel, ese push ya despliega la app publicada solo — no hace falta ningún paso manual extra.
