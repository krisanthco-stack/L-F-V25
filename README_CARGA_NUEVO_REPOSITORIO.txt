LIBRETA DE FISCALIZACIÓN — VERSIÓN 22.05 PRUEBA R2

BASE FUNCIONAL: V22.0.4
DESTINO: REPOSITORIO NUEVO E INDEPENDIENTE

CORRECCIONES DE ESTA PRUEBA
- Base Local: filtro USO AGRO visible como botón de filtro rápido, con contador y marca USO AGRO en cada tarjeta detectada.
- La detección agro se realiza únicamente desde Observaciones del expediente y reconoce agro/agropecuario, agrícola/agricultura, pecuario, ganadero, cultivo, siembra, plantación, pastizal y producción primaria, sin distinguir tildes ni mayúsculas.
- Terreno y entorno: Servicios 1 y Servicios 2 se presentan como opciones de selección visibles (radio), no como listas desplegables.
- Construcciones: Tipo de construcción se presenta como 5 opciones rápidas visibles + Otro; Otro abre un campo para escribir.
- Expediente: se eliminó el campo manual Número de inspección.
- Informe: muestra Expediente / trámite y Número de inspección de campo.
- El Número de inspección de campo se genera automáticamente al registrar la firma del inspector de campo, con formato INS-AÑO-####.
- El consecutivo se calcula de forma transaccional en IndexedDB para evitar duplicados entre pestañas del mismo dispositivo y reinicia en 0001 al cambiar el año.
- Se conserva compatibilidad interna con números de inspección existentes de versiones anteriores.
- Se conserva el resto de V22.0.4: Base Local, buscador/filtros, Gestión, Excel de Gestión, PDF, informes, almacenamiento local, sincronización y operación offline.

CARGA EN GITHUB
1. Cree un repositorio NUEVO, por ejemplo: L-FISCALIZACION-V22-05-R2
2. Descomprima este ZIP.
3. Suba LOS ARCHIVOS INTERNOS directamente a la raíz del repositorio; no suba el ZIP como único archivo.
4. En Settings > Pages seleccione Deploy from a branch.
5. Branch: main. Folder: /(root).
6. Save.
7. Abra únicamente la URL Pages del repositorio nuevo.

ARCHIVOS PRINCIPALES
- index.html
- manifest.webmanifest
- sw.js
- .nojekyll
- iconos PWA

IMPORTANTE
Esta es una prueba independiente basada en V22.0.4. No modifica el repositorio o versión productiva anterior.
