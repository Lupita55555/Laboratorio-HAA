# Explicación de cambios - Etapa 3: Fallback

**Bitácora:** resilience-sample-3.txt
**Cambio respecto a la etapa anterior:** se agregó fallback.

## Resultados

| Métrica | Con retry | Con fallback |
|---|---|---|
| Respuestas SUCCESS | 85 | 20 |
| Respuestas HTTP 200 | 200 | 200 |
| Respuestas distintas de 200 | 0 | 0 |
| Disponibilidad observada | 1.00 | 1.00 |

## Explicación
La disponibilidad se mantiene en 100% y no hay errores HTTP: cuando la llamada falla definitivamente, el fallback devuelve una respuesta degradada (datos de caché) en lugar de un error. Las respuestas SUCCESS bajaron a 20, lo que significa que 180 respuestas (90%) son degradadas. Es decir, el usuario nunca ve un error, pero la mayoría de las respuestas ya no vienen del servicio real. Disponibilidad no es lo mismo que calidad de respuesta: se cambió exactitud de los datos por continuidad del servicio.