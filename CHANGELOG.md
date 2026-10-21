# Changelog

Registro de cambios del modelo de riesgo de crédito.

## [Sin publicar]

## [1.1.0] - 2026-10-20

### Agregado
- Robot guardián con GitHub Actions y Python 3.12: entrenamiento, quality gate de AUC y reporte de errores.
- Artefacto `modelo-riesgo` con el modelo, preprocesamiento y métricas; output `auc-test` para comunicar el AUC entre jobs.
- Eventos de push con filtros de ramas y rutas, validación de PR y ejecución manual.
- Despliegue simulado desde `main`, con secretos y aprobación manual del entorno `produccion`.
- Semillas fijas (`random_state=42`) en la separación train/test y el Random Forest, y balanceo de clases (`class_weight="balanced"`), recuperados de la sesión 3.

### Cambiado
- Búsqueda de hiperparámetros reducida de cuatro combinaciones a una: 50 árboles, profundidad máxima 6 y mínimo de 100 muestras por hoja.

### Corregido
- Cálculo del AUC con la probabilidad de la clase positiva (`y_pred[:,1]`).

### Validación
- Base previa al grid reducido: dos ejecuciones locales con Python 3.13.9 y dependencias fijadas dieron AUC train `0.7616229854900092` y test `0.7322540496315074`; GitHub Actions con Python 3.12 reprodujo esas métricas.
- Modelo con grid reducido: AUC test `0.7317`, superior al umbral `AUC_MIN=0.70`; `model-ci` completó en 51 segundos en la ejecución del PR #3.
- Sabotaje controlado: AUC test `0.2683`, quality gate fallido, reporte de error ejecutado y PR bloqueado. La corrección en la misma rama activó CI y permitió integrar los cambios.
- Artefacto descargado y verificado con `best_model.pickle` y métricas en la misión 3.
- El despliegue a producción de esta release queda pendiente de revisión, integración del PR hacia `main` y aprobación manual.
