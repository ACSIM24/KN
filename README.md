# KN — Análisis y predicción de incidentes de mantención

Notebook de Google Colab que toma el export de tickets de **Fractal** (`EXPORTFRACTAL*.csv` o `.xlsx`) y genera estadísticas y alertas predictivas para mejorar el SLA de Kuehne + Nagel.

## Uso
1. Abrir `KN_Analisis_Incidentes.ipynb` en [Google Colab](https://colab.research.google.com/) (`Archivo → Subir notebook`, o `Abrir desde GitHub`).
2. `Entorno de ejecución → Ejecutar todo`.
3. Subir el archivo exportado cuando la primera celda lo pida.
4. Al final se descarga `KN_resultados_incidentes.xlsx` con todas las tablas.

## Qué responde
| Pregunta | Resultado |
|---|---|
| ¿Dónde están los mayores incidentes? | Tickets por sede y área, mapa de calor sede × problema, día × hora |
| ¿Activos más recurrentes? | Ranking de activos y pares *activo + problema* repetidos |
| ¿Problemas más recurrentes? | Clasificación automática por palabras clave (baños, iluminación, eléctrico, puertas, etc.) |
| ¿Cuánto cuesta? | Costo (columna *Cost Avoidance*) por sede, problema, activo y mes, y un Pareto |
| ¿Cuánto demoramos? | Horas de resolución (mediana, promedio, P90) y % SLA por sede, problema, técnico y prioridad |
| ¿Quién levanta más tickets? | Ranking de solicitantes con % cancelados/duplicados, y carga por técnico |
| **Predictivo** | Pronóstico semanal por sede · activos con falla probable (MTBF) · riesgo de incumplir SLA en tickets abiertos · problemas en alza |

## Parámetros
En la celda **0. Configuración**: `SLA_HORAS`, `TOP_N`, `SEMANAS_PRONOSTICO`, `DIAS_ALERTA_ACTIVOS`, `MIN_INCIDENTES_ACTIVO`, `EXCLUIR_CANCELADOS`.
Las categorías de problemas se ajustan en el diccionario `CATEGORIAS` (celda 2).

## Notas sobre los datos
- El export de Fractal tiene los encabezados **corridos una columna** desde *Clasificación 2* (ej. *Clasificación 2* trae la prioridad y *Email del solicitante* trae el técnico). El notebook lo detecta y lo corrige automáticamente.
- Se excluyen de los análisis los tickets de prueba, los duplicados y los cancelados (configurable).
- Los archivos de datos (`*.csv`, `*.xlsx`) no se versionan porque contienen nombres y correos del personal.
