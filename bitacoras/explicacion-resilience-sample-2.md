# Explicación de cambios - Etapa 2: Retry

**Bitácora:** resilience-sample-2.txt
**Cambio respecto a la etapa anterior:** se agregó retry.

## Resultados

| Métrica | Con timeout | Con retry |
|---|---|---|
| Respuestas SUCCESS | 65 | 85 |
| Respuestas HTTP 200 | 65 | 200 |
| Respuestas distintas de 200 | 135 | 0 |
| Disponibilidad observada | 0.325 | 1.00 |

## Explicación
Con retry, las llamadas que fallaban o excedían el timeout se reintentan, y como los fallos son intermitentes, muchos reintentos tienen éxito: los SUCCESS subieron de 65 a 85. Los errores pasaron de 135 a 0 y la disponibilidad llegó a 100%. Sin embargo, solo 85 de las 200 respuestas fueron SUCCESS reales; el resto (115) corresponde a respuestas alternativas, es decir, el servicio sigue fallando para una parte de las solicitudes aun con reintentos. El costo de reintentar es mayor tiempo de respuesta en las peticiones que necesitan más de un intento.