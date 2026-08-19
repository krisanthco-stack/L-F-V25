# AUDITORÍA PROFUNDA Y COMPARACIÓN EJECUTIVA — V22.06.2-AUDITADA

Fecha: 2026-08-18

## 1. Hallazgo crítico

Se confirmó una **regresión real** en V22.06-OFFLINE-FIRST respecto de V22.0.4:

- V22.0.4 ya había eliminado completamente la **firma de la fiscalización de campo/inspector**.
- V22.06-OFFLINE-FIRST volvió a introducir:
  - canvas `fieldSignatureCanvas`;
  - botón `clearFieldSignatureBtn`;
  - propiedad `report.fieldSignature`;
  - generación de `fieldInspectionNumber` condicionada a la firma;
  - auditoría de firma de campo;
  - firma de campo en HTML/Word;
  - exportación JSON de `fieldSignature`.
- Esto contradice directamente el requerimiento aprobado: **eliminar la firma del inspector y conservar únicamente Responsable y Puesto**.

## 2. Segunda regresión

V22.06-OFFLINE-FIRST también volvió a introducir un mecanismo de **Número de inspección de campo** ligado a la firma del inspector.

V22.0.4 no tenía ese mecanismo.

En V22.06.2-AUDITADA se eliminaron sus referencias funcionales y de presentación. Los campos legacy se limpian durante normalización/importación para impedir que una firma antigua vuelva a aparecer.

## 3. Servicios 1 y 2

### V22.0.4
- `Servicios 1`: `<select>`
- `Servicios 2`: `<select>`
- Las opciones ONT ya estaban definidas correctamente.

### V22.06-OFFLINE-FIRST
Se modificó la interfaz a tarjetas/radios (`choice-card`), aunque el requerimiento pedía selección.

Además, permanecieron textos explicativos que el usuario posteriormente indicó eliminar.

### V22.06.2-AUDITADA
Restaurado:
- `Servicios 1` como **select**.
- `Servicios 2` como **select**.
- Se eliminaron los textos explicativos.
- Se conservaron las opciones ONT.
- No se agregan factores de cálculo.

## 4. Construcciones

Los catálogos y la función `cSelect/cSelectOther` confirman que los campos solicitados siguen siendo controles de selección:

- Estado general.
- Paredes exteriores.
- Techo.
- Estructura del techo.
- Cielo raso.
- Piso o acabado del suelo.
- Instalación eléctrica.

Se verificó que las opciones solicitadas por el usuario están presentes en los catálogos.

`Detalles adicionales` continúa como texto libre, tal como fue solicitado.

## 5. Firma que SÍ permanece

La **firma de quien avala la resolución** se conserva.

Esto es correcto porque el requerimiento fue eliminar la firma del inspector/fiscalización de campo, no la firma de quien avala la resolución.

## 6. Finalización

Se detectó otra diferencia regresiva:

- V22.0.4: botón **Finalización**.
- V22.06-OFFLINE-FIRST: botón **Finalizar**.

Se restauró **Finalización**, conservando el flujo existente.

## 7. Comparación ejecutiva

| Elemento | V22.0.4 | V22.06 Offline | V22.06.2 Auditada |
|---|---|---|---|
| Firma inspector/campo | Eliminada | **Reintroducida — REGRESIÓN** | **Eliminada** |
| Número ligado a firma inspector | No existe | **Reintroducido — REGRESIÓN** | **Eliminado** |
| Firma de aval | Sí | Sí | Sí |
| Servicios 1 | Select | Radio/tarjetas | **Select** |
| Servicios 2 | Select | Radio/tarjetas | **Select** |
| Textos explicativos Servicios 1/2 | Presentes | Presentes | **Eliminados** |
| Campos construcción solicitados | Selección | Catálogos preservados | **Selección verificada** |
| Finalización | Finalización | Finalizar | **Finalización** |
| IndexedDB/offline | Base existente | Reforzado | **Conservado** |
| JSON/adjuntos | Existente | Reforzado | **Conservado** |
| Firma de aval en JSON | Sí | Sí | **Sí** |
| Firma inspector en JSON | No | **Sí — regresión** | **No funcional** |

## 8. Criterio de corrección

No se sustituyó V22.06-OFFLINE-FIRST por V22.0.4 completa, porque eso habría eliminado las mejoras offline-first.

Se hizo una corrección selectiva:

**V22.06-OFFLINE-FIRST**
→ conservar arquitectura offline, IndexedDB, sincronización, import/export y gestión existente

**+**
→ recuperar las decisiones correctas de V22.0.4 donde hubo regresión

**−**
→ eliminar únicamente lo que contradice los requerimientos aprobados.

## 9. Validación

- `fieldSignatureCanvas`: 0
- `clearFieldSignatureBtn`: 0
- `ensureFieldInspectionNumber`: 0
- `fieldInspectionNumber(...)`: 0
- `Firma de la fiscalización de campo`: 0
- `Servicios 1`: select
- `Servicios 2`: select
- Firma de aval: conservada
- `Finalización`: restaurada
- Catálogos constructivos requeridos: verificados
- Sintaxis JavaScript: **OK con Node.js**

Los únicos campos legacy relacionados con `fieldSignature`/`fieldInspectionNumber` que permanecen son operaciones internas de **limpieza de datos antiguos**, no controles, firmas, cálculos ni salidas visibles. Esto evita que una versión anterior vuelva a contaminar un expediente al importarlo.

## 10. Versión resultante

**V22.06.2-AUDITADA**

Esta versión debe utilizarse como base para la siguiente etapa y no debe volver a incorporar cambios eliminados previamente.
