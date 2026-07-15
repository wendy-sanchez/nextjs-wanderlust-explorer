# SPECS - Wanderlust Explorer MVP

## Objetivo
Construir un explorador de experiencias multipágina con React y Next.js que permita explorar, buscar, filtrar y marcar experiencias como favoritas sin recarga de página.

## Páginas requeridas

### `/` - Home
- Debe incluir una sección hero.
- Debe incluir un botón principal que navegue a `/experiences`.

### `/experiences` - Explorador
- Debe mostrar el listado completo de tarjetas de experiencias.
- Debe incluir una barra de búsqueda.
- Debe incluir al menos dos filtros:
  - Categoría
  - Destino
- La búsqueda y los filtros activos deben reflejarse en la URL como query parameters.
- Al cargar la página, los inputs deben prerrellenarse con los valores presentes en la URL.

### `/experiences/[id]` - Detalle
- Debe mostrar la información completa de una experiencia.
- La experiencia se obtiene desde el dataset local usando su `id`.

### `/favorites` - Favoritos
- Debe mostrar la lista de experiencias marcadas como favoritas por el usuario.
- Los favoritos se manejan en estado de componente por ahora (sin persistencia).

### `/profile` - Perfil
- Página estática con un perfil de usuario simulado.
- Debe incluir un resumen con el número de favoritos guardados.

## Comportamiento de búsqueda y filtros
- La búsqueda filtra por coincidencia en el título de la experiencia.
- Debe usarse regex case-insensitive, por ejemplo: `/term/i`.
- El filtro por categoría y el filtro por destino deben:
  - Funcionar de forma independiente.
  - Combinarse entre sí y con la búsqueda.

## Estado en URL (query params)
- El estado de búsqueda y filtros debe vivir en la URL para permitir vistas compartibles.
- Ejemplo de URL válida:
  - `/experiences?search=vela&category=adventure&destination=Croatia`
- Al abrir un enlace con query params, la vista debe aterrizar prefiltrada con esos valores.

## Dataset
- Generar con IA un array local de 100 objetos de experiencia.
- Guardarlo como un archivo TypeScript local.
- Cada objeto debe incluir como mínimo:
  - `id`
  - `title`
  - `description`
  - `category` (una de: `Adventure`, `Culture`, `Food`, `Wellness`, `Nature`)
  - `destination` (formato ciudad + país)
  - `price`
  - `rating`
  - `imageUrl` (placeholder válido)

## Favoritos
- Cada tarjeta debe tener un icono de corazón para activar/desactivar favorito.
- Los favoritos deben guardarse en un `useState` de nivel superior.
- El estado de favoritos debe pasarse por props a los componentes que lo necesiten.
- No se requiere persistencia en esta fase.

## Criterios de aceptación mínimos
1. Navegación funcional entre todas las páginas requeridas.
2. `/experiences` permite buscar y filtrar por categoría y destino de forma combinada.
3. Query params sincronizados con la UI y restaurados al cargar.
4. `/experiences/[id]` resuelve correctamente una experiencia por `id` desde el dataset local.
5. Corazón de favorito funcional en tarjetas y visible en `/favorites`.
6. `/profile` muestra el conteo de favoritos actualizado.
7. Dataset local TypeScript con 100 experiencias válidas.
