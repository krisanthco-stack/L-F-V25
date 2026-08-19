# Libreta de Fiscalización — V22.06 OFFLINE-FIRST

## Alcance implementado
- Flujo: Terreno → Construcciones/Croquis → Fiscalización → Gestión → Excel.
- IndexedDB como fuente local de verdad; fotografías y PDF permanecen como `Blob` local.
- Cola de sincronización pendiente por expediente, estado visual y reintentos con backoff exponencial.
- Resolución de conflictos basada en la versión más reciente + conservación de valores no vacíos; cambios posteriores durante sincronización vuelven a estado `pending`.
- Exportación/importación JSON del expediente con fotografías, PDF y firmas en Base64/data URL.
- Esquema JSON `FiscalizacionBIExport`, versión `2.0`.
- Administración local de registros de correo institucional: crear, editar, eliminar con rol Administrador, respaldo previo y confirmación explícita.
- Servicios 1 y 2 conservan las opciones reales existentes del proyecto: selección visible mediante radio.
- Al finalizar Fiscalización: primero se genera y guarda el informe; después se traslada a Gestión; finalmente se genera el Excel consolidado.
- Excel de Gestión incluye propietario, terreno, vía/servicios y detalle constructivo.
- Informe no muestra campos constructivos vacíos ni anexos fotográficos sin fotografías reales.

## Esquema JSON
```json
{
  "schema": "FiscalizacionBIExport",
  "schemaVersion": "2.0",
  "appVersion": "22.06-OFFLINE-FIRST",
  "exportedAt": "ISO-8601",
  "exportedBy": "usuario",
  "case": {},
  "attachments": {
    "photos": [],
    "documents": []
  },
  "signatures": {
    "fieldSignature": "data:image/...",
    "resolutionSignature": "data:image/..."
  }
}
```

## Nota de seguridad
El control de rol de correo es local/offline. Para seguridad institucional fuerte debe complementarse con autenticación y autorización del servidor central al sincronizar. La aplicación nunca solicita ni almacena contraseñas de Gmail/Microsoft.

## Análisis UX: módulo Fiscalización reducido
No se recomienda duplicar el módulo. El flujo existente ya separa claramente captura, resolución y Gestión. Una segunda pantalla reducida generaría duplicidad y riesgo de inconsistencias. Para consulta rápida basta con el estado, resumen y acciones del expediente dentro de Gestión.
