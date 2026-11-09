# Explicación de cambios - Etapa 4: Circuit Breaker

**Bitácora:** resilience-sample-f.txt
**Cambio respecto a la etapa anterior:** se agregó circuit breaker (configuración completa: timeout + retry + fallback + circuit breaker).

## Resultados

| Métrica | Con fallback | Con circuit breaker |
|---|---|---|
| Respuestas SUCCESS | 20 | 22 |
| Respuestas degradadas (DEGRADED_CACHE) | 180 | 178 |
| Respuestas distintas de 200 | 0 | 0 |
| Disponibilidad observada | 1.00 | 1.00 |

## Explicación
El resultado visible en disponibilidad es casi igual al de la etapa anterior (100%, 0 errores), con una diferencia mínima de 20 a 22 SUCCESS. El aporte del circuit breaker no se ve tanto en el conteo de respuestas como en el comportamiento: cuando detecta una tasa alta de fallos, abre el circuito y deja de llamar al servicio dañado, enviando las solicitudes directamente al fallback. Esto evita saturar el servicio que falla y reduce el tiempo que se pierde en timeouts y reintentos inútiles, lo que permite que el sistema se recupere. Frente a la línea base, la disponibilidad subió de 71.5% a 100% (+28.5 puntos) y los errores HTTP 500 desaparecieron por completo, a cambio de que alrededor de 89% de las respuestas sean degradadas.