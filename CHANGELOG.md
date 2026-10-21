# Changelog

Registro de cambios del modelo de riesgo de crédito.

## [Sin publicar]

### Agregado
- Semillas fijas (`random_state=42`) en la separación train/test y en el Random Forest, recuperadas de la sesión 3.
- Balanceo de clases con `class_weight="balanced"`.

### Corregido
- Cálculo del AUC con la probabilidad de la clase positiva (`y_pred[:,1]`).

### Validación local
- Dos ejecuciones completas consecutivas con métricas idénticas: AUC train `0.7616229854900092` y test `0.7322540496315074`.
- Python 3.13.9 y las versiones exactas de `requirements.txt`, instaladas en `.venv`.
- `pip check` sin dependencias incompatibles. La ejecución en GitHub Actions con Python 3.12 se verificará al incorporar el workflow.

