# Libreta de Fiscalización V25.0.0 — Base + Gestión con recuperación

## Persistencia
- IndexedDB es la fuente local de verdad.
- DB schema V5.
- Al actualizar desde un esquema anterior, V25 crea automáticamente una copia recuperable de expedientes, fotografías y documentos antes de completar la migración.
- Los expedientes retirados manualmente de Base local también se respaldan antes de eliminarse de la vista activa.

## Recuperación
- Base local: botón **Recuperar eliminados**.
- Gestión: botón **Recuperar eliminados**.
- La restauración conserva el expediente y sus adjuntos cuando existen en el respaldo.
- Un expediente finalizado se restaura lógicamente en Gestión; uno activo vuelve a Base local.

## Paquetes
- Base/Expediente/Gestión: importar y exportar paquete completo `.zip`.
- El usuario selecciona el ZIP directamente; no necesita descomprimirlo.
- Incluye JSON, fotografías, documentos/PDF y firma de resolución cuando existe.

## Regresión crítica cubierta
La actualización no debe crear una base vacía ni perder expedientes existentes. La migración V5 crea el respaldo de recuperación dentro de IndexedDB antes de continuar.
