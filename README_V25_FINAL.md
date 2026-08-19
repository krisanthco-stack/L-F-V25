# Libreta de Fiscalización — V25.2.0 FINAL CORREGIDA

## Base usada y comparación
Esta compilación se construyó comparando:
- **V22.0.3** incluida dentro del repositorio recibido, como referencia de regresión funcional.
- **V22.05-PRUEBA-R2 / L-F-V25-main**, que conserva la pantalla de Construcciones y mejoras visuales, pero identifica incorrectamente la aplicación como V22 y usa esquema IndexedDB V2.
- **V25.0.0 FUNCIONAL BASE GESTIÓN RECUPERACIÓN**, que aporta recuperación y paquetes completos, pero había perdido la vista HTML de Construcciones y aún eliminaba una tienda antigua durante la migración.
- **V25.2.0 FINAL CORREGIDA**, resultado de la integración segura.

## Corrección crítica: Construcciones
- Se restauró `view-construction`, que faltaba en la V25 funcional aunque el menú y el JavaScript seguían apuntando a ese módulo.
- **Agregar construcción** vuelve a funcionar.
- Cada unidad mantiene tipología, unidad de medida, estado, materiales, croquis, área o longitud y observaciones.
- Se conserva el cálculo desde croquis para m² y la medición lineal para ML/km.
- Las fotografías pueden asociarse a la unidad constructiva correspondiente.
- El resumen de cantidad, área total y longitud total vuelve a estar dentro del módulo correcto.
- La fiscalización y los anexos de construcciones siguen alimentándose del mismo expediente.
- Antes de retirar una unidad constructiva se crea un respaldo recuperable del expediente completo.

## Protección al actualizar el repositorio
- Se conserva el mismo nombre de base `LibretaValoracionCR`.
- El esquema es **V6** y una actualización nunca elimina tiendas existentes.
- Antes de una migración se crea una copia recuperable de expedientes, fotografías y PDF.
- No se usa `indexedDB.deleteDatabase`, `localStorage.clear` ni `deleteObjectStore` en V25.2.
- Los trámites en **Gestión** siguen siendo registros de `cases`; cambiar el código del repositorio no los reinicia ni los duplica.
- El Service Worker usa caché propio de V25.2 y navegación de red sin caché obsoleta.

## Recuperación
- Botón **Recuperar eliminados** en Base local y Gestión.
- Retirar un expediente crea primero una copia completa recuperable.
- Retirar un PDF crea primero una copia completa recuperable.
- Retirar una fotografía normal o de anexo crea primero una copia completa recuperable.
- Retirar una unidad constructiva crea primero una copia completa recuperable.
- Se corrigió la restauración/importación: ahora existe `mergeCaseRecords()` y sus auxiliares, que antes eran llamados pero faltaban en la V25 funcional.
- La restauración usa `snapshotId` exacto para no mezclar adjuntos de respaldos históricos distintos.

## Importante sobre archivos ya eliminados por una versión anterior
V25.2 puede recuperar información presente en las tiendas de recuperación, paquetes ZIP/JSON previos o registros que aún existan en IndexedDB. Si una versión anterior eliminó físicamente los bytes de un PDF o fotografía sin crear respaldo, el navegador no puede reconstruir ese archivo de la nada. Desde V25.2 las operaciones de retirada protegidas crean respaldo antes de borrar.

## Publicación segura
1. Haga una copia del ZIP exportado de sus expedientes importantes.
2. Suba **los archivos internos de esta carpeta** directamente a la raíz del mismo repositorio de GitHub Pages.
3. No cambie el dominio/origen donde usa la libreta y no borre los datos del sitio desde el navegador.
4. Después de publicar, abra la aplicación y verifique que Base local y Gestión muestran los expedientes existentes.
5. Abra **Construcciones**, agregue una unidad de prueba, guárdela y vuelva a abrir el expediente.

### Fallos de ejecución reparados
- Se evita el `ReferenceError` de `refreshEmailSendUi` que podía interrumpir el refresco general de V25.
- Se incorporó `bytesToBase64`, necesaria para convertir y restaurar adjuntos de paquetes ZIP.
