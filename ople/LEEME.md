# Entrega de datos OPLE

Archivos para publicarse en la carpeta `ople/` de `jorgelandab/repositorio-ine-datos`. No se suben desde aquí: la rutina de publicación los toma de esta carpeta.

## Archivos

- `manifiesto.json` — esquema 1. Por entidad: `clave` (mismo módulo del plugin: ags, bc, …, zac), `entidad`, `estatus`, `acuerdos`, `corte` (fecha ISO del acuerdo más reciente, con fecha corregida si existe; si ese último año no trae día, solo el año), `sha256` y `bytes` del `<clave>.json.gz`, y `fuentes`. Arriba: `esquema`, `generado`, `total`.
- `indice.json` e `indice.json.gz` — cobertura de las 32 entidades, en el formato que carga el plugin al abrir la página.
- `<clave>.json.gz` — ficha completa de cada entidad.
- `busqueda/<clave>.json.gz` — índice ligero para tarjetas, búsqueda y filtros. El plugin 2.7.8 los necesita; esta entrega los trae ya armados (una versión posterior podría regenerarlos).

## Ficha completa (`<clave>.json.gz`)

`{"modulo","entidad","generado","origenes":[…],"acuerdos":[…]}`

`origenes` es la lista de procedencias. En cada acuerdo, campos como `ko`, `to`, `yo` y `fo` son índices de esa lista.

Campos de un acuerdo (se omiten si van vacíos): `id`, `k` (clave), `ko`, `tm` (título), `to`, `y` (año), `yo`, `u` (URL del PDF), `il`, `ft` (fecha tal cual el listado), `f` (fecha ISO publicada), `fo`, `st`/`sf`/`sx` (sesión), `uf`, `fc` (fecha de captura), `fu`/`fuo` (fuente), `op` (nombre del OPLE), `tp`/`og` (tipo y órgano según el título; etiquetas auxiliares), `pl`, `ax` (anexos), `fci`/`fct`/`fco` (fecha corregida; no sustituyen `ft`/`f`), `rmf`/`rmn` (revisión manual: fecha de la revisión, no del acuerdo).

Las claves, títulos y textos se copian tal como los publica cada OPLE. No se normalizan.

## Índice de búsqueda (`busqueda/<clave>.json.gz`)

`{"v":1,"modulo","entidad","generado","tabla":[textos repetidos],"r":[filas]}`

Cada fila: id (sin el prefijo de entidad), clave, título, año, fecha ISO, índices a `tabla` (fecha textual, tipo, órgano, sesión, OPLE, prefijo de URL), identificador del listado, resto de la URL, número de anexos, banderas (1 = título OCR, 2 = título no disponible) y, si aplica, fecha corregida ISO.

## Estados sin datos

Si un OPLE no tiene acuerdos publicados, su `estatus` en el manifiesto y en el índice es «sin datos publicados», y sus archivos llevan `acuerdos` / `r` vacíos.
