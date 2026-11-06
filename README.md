# Catálogo de Minecraft

Proyecto de Lenguajes de Marcas: una web en español sobre los Mobs (criaturas) de Minecraft, usando datos reales de una API pública gratuita. 

## La API que he elegido

- **Nombre:** Astroworld API 
- **Qué ofrece:** Esta API nos ofrece datos de Minecraft (criaturas, biomas, objetos, versiones...) en formato JSON
- **De dónde sale:** Esta la encontramos en un repositorio donde hay lista de Publics APIs, en la categoría *Games & Comics*
- **Quién la mantiene:** Astroworld MC [Git de Astroworld](github.com/astroworld-mc)
- **Documentación:** [Enlace API](https://api.astroworldmc.com)
- **Auth:** no necesita clave y tiene **HTTPS:**

## Condiciones de uso

- Es gratis y no requiere registro.
- Límite de 100 peticiones por minuto por IP.
- Exige un enlace visible en las páginas que usan sus datos: [Powered by Astroworld API](https://api.astroworldmc.com) — lo llevará el pie de todas las páginas.

## Peticiones que he hecho

- `GET /api/v1/mobs` — la lista completa: 76 criaturas
- `GET /api/v1/mobs/creeper` — ficha 1
- `GET /api/v1/mobs/axolotl` — ficha 2
- `GET /api/v1/mobs/ender-dragon` — ficha 3
- `GET /api/v1/versions` — fechas de lanzamiento de cada versión

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

## Contenido del proyecto

- [x] README con la API y la tabla de campos
- [ ] carpeta `datos/` con los JSON descargados de la API
- [ ] `index.html` (portada)
- [ ] `catalogo.html` (catálogo)
- [ ] `fichas/` (3 fichas con la misma estructura)
- [ ] `comparativa.html` (tabla comparando 8 criaturas)
- [ ] `sobre-los-datos.html` (explicación de la API)
- [ ] `propuesta.html` (formulario)
