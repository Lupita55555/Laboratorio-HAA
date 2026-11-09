# Explicación de cambios - Etapa 0: Línea base (sin patrones)

**Bitácora:** availability-baseline.txt
**Configuración:** servicio sin patrones de resiliencia (sin timeout, retry, fallback ni circuit breaker).

## Resultados

| Métrica | Valor |
|---|---|
| Solicitudes totales | 200 |
| Respuestas HTTP 200 (SUCCESS) | 143 |
| Respuestas distintas de 200 | 57 |
| Disponibilidad observada | 0.715 (71.5%) |

## Explicación
Esta etapa es el punto de referencia. El servicio dependiente falla de forma intermitente y, al no existir ningún mecanismo de protección, cada fallo llega directamente al cliente como error. Casi 3 de cada 10 solicitudes (28.5%) terminaron fallando. Todas las etapas siguientes se comparan contra este 71.5% de disponibilidad.