# Catálogo de Minecraft

Proyecto de Lenguajes de Marcas: una web en español sobre los Mobs (criaturas) de Minecraft, usando datos reales de una API pública gratuita. 

## La API que he elegido

- **Nombre:** Astroworld API 
- **Qué ofrece:** Esta API nos ofrece datos de Minecraft (criaturas, biomas, objetos, versiones...) en formato JSON
- **De dónde sale:** Esta la encontramos en un repositorio donde hay lista de Publics APIs, en la categoría *Games & Comics*
- **Quién la mantiene:** Astroworld MC [Git de Astroworld](https://github.com/astroworld-mc)
- **Documentación:** [Enlace API](https://api.astroworldmc.com)
- **Auth:** no necesita clave y tiene **HTTPS:**

## Condiciones de uso

- Es gratis y no requiere registro.
- Límite de 100 peticiones por minuto por IP.
- Exige un enlace visible en las páginas que usan sus datos: [Powered by Astroworld API](https://api.astroworldmc.com) — lo llevará el pie de todas las páginas.
- El **código** de la API está publicado como software libre con **licencia MIT**, basicamente la podemos leer y reutilizar en su GitHub. Los **datos** que uso se amoldan a las condiciones de arriba. 

## Peticiones que he hecho

- `GET /api/v1/mobs`  La lista completa: 76 criaturas
- `GET /api/v1/mobs/creeper`  Los datos de la ficha del Creeper
- `GET /api/v1/mobs/axolotl`  Los datos de la ficha del Axolotl
- `GET /api/v1/mobs/ender-dragon`  Los datos de la ficha del Ender Dragon
- `GET /api/v1/versions`  Las fechas de lanzamiento de cada versión

Todas las respuestas están guardadas tal cual llegaron de la API en la carpeta `datos/`, y es de ahí de donde sale todo el contenido del sitio web.

## Tabla de campos de una criatura

| Campo del JSON | Tipo | Qué es para el lector |
|---|---|---|
| `name` | texto | El título de la ficha y el texto del enlace del catálogo |
| `id` | texto | Identifica la criatura; decide el nombre de su ficha |
| `type` | texto cerrado | Agrupa el catálogo: pacíficos, neutrales, hostiles, jefes |
| `hp` | número | La salud; se lee «Salud: 20» y es columna de la comparativa |
| `damage.easy` / `normal` / `hard` | números | El daño que causa según la dificultad del juego |
| `xpDrop.min` / `max` | números | La experiencia que da al matarlo |
| `drops[]` | lista de objetos | Tabla de botín: objeto, cantidad y % de probabilidad |
| `spawnBiomes[]` | lista de textos | Los biomas donde aparece |
| `spawnConditions` | texto largo | En qué condiciones aparece |
| `behavior` | texto largo | Cómo se comporta; será el párrafo principal de su ficha |
| `weaknesses[]` | lista de textos | Contra qué es débil |
| `tameable` + `tamingMethod` | booleano + texto | Si se puede domar, y con qué se consigue |
| `breedable` + `breedingItem` | booleano + texto | Si se puede criar, y con qué comida |
| `versionAdded` | texto | La versión del juego en la que apareció |
| `notes` | texto largo | Curiosidades y datos extra |

Cabe recalcar que esta tabla es para poder ver de forma más ordenada todos los datos que nos ofrece la API cuando solicitamos información de una criatura, pero no hemos usado todos los campos, solamente los que resaltaban como información más valiosa. 

## Contenido del proyecto

- [x] README con la API y la tabla de campos
- [x] carpeta `datos/` con los JSON descargados de la API
- [x] `index.html` (portada)
- [x] `catalogo.html` (catálogo)
- [x] `fichas/` (3 fichas con la misma estructura)
- [x] `comparativa.html` (tabla comparando 8 criaturas)
- [x] `sobre-los-datos.html` (explicación de la API)
- [x] `propuesta.html` (formulario)
- [x] `assets/img/` (las imágenes de las criaturas)
- [x] validación de las 8 páginas con el W3C

## Contenido de cada página (8)

- **index.html**: La portada donde se habla de qué es el sitio, de dónde salen los datos (con enlace a la API y su atribución), 3 criaturas destacadas (una hostil, una pacífica y un jefe) con su imagen y datos, y el tráiler oficial del juego insertado desde YouTube.
- **catalogo.html**: Catálogo donde vemos las 15 criaturas, agrupadas según su campo `type` en cuatro secciones (pacíficos, neutrales, hostiles y jefes), cada una con su imagen, su nombre y tres datos clave (salud, daño y experiencia). Las tres que tienen ficha llevan el enlace a ellas.
- **fichas/axolotl.html, fichas/creeper.html, fichas/ender-dragon.html**:Son las plantillas completas de cada criatura: datos clave como lista de definición (salud, daño por dificultad, experiencia, si se puede domar o criar), tabla de botines cuando los hay, biomas y condiciones de aparición, comportamiento, debilidades y curiosidades con la versión en que apareció. Las tres fichas tienen exactamente la misma estructura.
- **comparativa.html**: Una tabla con `caption` que compara 8 criaturas en 4 datos (tipo, salud, daño normal y XP máximo), con cabeceras de fila y de columna identificadas con `scope` y una fila de resumen (`tfoot`) con las medias y el máximo.
- **sobre-los-datos.html**: La ficha de la API: qué es, quién la mantiene, su licencia y condiciones, las atribuciones, las peticiones que hice y la transformación real: un fragmento del JSON junto al HTML en el que se convirtió, con su tabla-puente donde se ve de forma más ordenada.
- **propuesta.html**: El formulario para proponer una criatura nueva: 16 campos agrupados en 4 bloques (`fieldset` con su `legend`) según la tabla de campos, con cada control adaptado al tipo de su dato (lista cerrada para el tipo, números con rango, URL, áreas de texto…) y la validación del navegador (obligatorios marcados con asterisco, longitudes y rangos).
- **datos/**: Las respuestas reales de la API: `mobs.json`, `mob-creeper.json`, `mob-axolotl.json`, `mob-ender-dragon.json` y `versions.json`. De aquí sale todo el texto del sitio.
- **assets/img/**: Las imágenes de las criaturas, guardadas en minúsculas y sin espacios, con su `alt`.

## Decisiones de marcado

1. **Los datos «nombre: valor» van en listas de definición, no en tablas.** Dudé entre presentarlos como `dl` o como tabla. Me quedé con la lista (`dl`/`dt`/`dd`) porque cada dato es un par único; las tablas las reservé para cuando hay varios objetos con los mismos campos: la tabla de botines de las fichas y la comparativa.
2. **Botines vacíos: párrafo en vez de tabla.** El axolotl y el Ender Dragon no sueltan botines (el campo `drops` llega vacío del JSON). En su ficha puse un párrafo en lugar de una tabla vacía, y pasa exactamente lo mismo con el Ender Dragon.
3. **En las fichas la navegación no lleva `aria-current`.** En las páginas de la raíz, el enlace de la página actual va marcado, pero las fichas no están en el menú y he decidido no utilizar `aria-current` porque en el caso de haberlo utilizado, marcaría en cualquiera de las fichas como "página actual" o "catálogo" cuando realmente no es así. 
4. **Los nombres: traducidos con criterio.** Traducí al español los nombres de las criaturas (vaca, oveja, camello...), excepto los que la comunidad usa en inglés (Creeper, Enderman, Warden, Wither, Ender Dragon...).

## Validación

He pasado las 8 páginas del sitio por el validador HTML del W3C ([validator.w3.org](https://validator.w3.org)), subiendo cada fichero desde el disco local.

| Página | Resultado |
|---|---|
| index.html | sin errores |
| catalogo.html | sin errores |
| comparativa.html | sin errores |
| propuesta.html | sin errores |
| sobre-los-datos.html | sin errores |
| fichas/creeper.html | sin errores |
| fichas/axolotl.html | sin errores |
| fichas/ender-dragon.html | sin errores |

Hubo un único aviso en el index.html que se ha corregido con éxito total.

## Créditos y atribución

- **Datos de criaturas:** [Powered by Astroworld API](https://api.astroworldmc.com) — enlace visible en el pie de todas las páginas.
- **Imágenes del juego:** Mojang, vía [minecraft.wiki](https://minecraft.wiki).
- **Tráiler de la portada:** el oficial del canal *Minecraft* de Mojang en YouTube.
- Minecraft y sus contenidos son de Mojang Synergies / Microsoft.

