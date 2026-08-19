# Libreta de Fiscalización — V25.3.0 FINAL

## Alcance de esta versión
V25.3.0 integra las correcciones de persistencia y recuperación de V25, restaura y mantiene funcional Construcciones, corrige la navegación Fotografías → Fiscalización y aplica los ajustes finales de interfaz y Gestión solicitados.

## Protección de expedientes al actualizar
- Se conserva la base `LibretaValoracionCR`.
- El esquema permanece en **DB_VERSION 6**; V25.3 no introduce una migración adicional para usuarios de V25.2.x.
- No se usa `indexedDB.deleteDatabase`, `localStorage.clear` ni `deleteObjectStore`.
- Gestión utiliza los mismos registros de `cases`; actualizar archivos del repositorio no reinicia ni vacía Gestión.
- Las migraciones desde esquemas anteriores mantienen respaldo interno de expedientes, fotografías y documentos en las tiendas `recovery*`.

## Construcciones
- Módulo `view-construction` presente y funcional.
- Agregar, editar, guardar y retirar unidades con respaldo recuperable.
- Estado general, paredes exteriores, techo, estructura del techo, cielo raso, piso e instalación eléctrica son controles de selección.
- **Detalles adicionales** es campo de texto abierto.
- Croquis, vértices, distancias y controles tienen una presentación más compacta.

## Fotografías
- Existe un único botón azul **Siguiente**.
- Avanza siempre a **Fiscalización**.
- La transición `field → resolution` solo se registra una vez.
- Si el expediente ya está en Gestión/resolución o finalizado, puede volver a Fotografías y continuar sin error de etapa.

## Gestión — respaldo completo
Los botones principales ahora permiten:
- **Descargar todos**: genera `Gestion_Completa_FECHA.zip`.
- **Cargar todos**: restaura ese mismo paquete.

El ZIP contiene:
- `manifest.json`
- `expedientes.json`
- `gestiones.json`
- `construcciones.json`
- `adjuntos.json`
- carpetas `fotografias/`, `documentos/` y `firmas/` cuando existen archivos.

Al cargar, los expedientes existentes se combinan por ID o número de trámite y no se duplican. Los datos locales no vacíos se conservan mediante la lógica de fusión segura.

## Interfaz compacta
- Botones generales reducidos.
- Botones de importación y Gestión reducidos.
- Textos explicativos de importación Excel/PDF resumidos.
- Sección de vértices y distancias compactada.
- Se eliminó la tarjeta redundante **Identificación del informe de campo** del módulo Informe.

## Informe tamaño Carta
- PDF / impresión: `@page size: Letter` (8.5 × 11 in).
- Vista previa: proporción Carta.
- DOCX: `12240 × 15840` twips, equivalente a Carta.

## Publicación segura en GitHub Pages
1. Antes de publicar, use **Gestión → Descargar todos** para guardar una copia ZIP completa.
2. Reemplace únicamente los archivos de la aplicación en el mismo repositorio/origen.
3. No borre datos del sitio desde el navegador.
4. Mantenga el mismo dominio/origen de GitHub Pages para que IndexedDB continúe siendo la misma base.
5. Después de publicar, compruebe Base local, Gestión, Construcciones, Fotografías e Informe.

## Versión
- Aplicación: **25.3.0-FINAL**
- IndexedDB: **V6**
- Service Worker: **v25.3.0-final-build-1**
