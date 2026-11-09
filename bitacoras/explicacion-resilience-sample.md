# Explicación de cambios - Etapa 1: Timeout

**Bitácora:** resilience-sample.txt
**Cambio respecto a la etapa anterior:** se agregó timeout a la llamada.

## Resultados

| Métrica | Baseline | Con timeout |
|---|---|---|
| Respuestas HTTP 200 (SUCCESS) | 143 | 65 |
| Respuestas distintas de 200 | 57 | 135 |
| Disponibilidad observada | 0.715 | 0.325 |

## Explicación
La disponibilidad empeoró: bajó de 71.5% a 32.5% y los errores subieron de 57 a 135. El timeout por sí solo no corrige los fallos; solo limita cuánto espera el servicio. Las peticiones lentas que antes terminaban respondiendo con éxito ahora se cortan al superar el límite y se convierten en error. Su beneficio es que el cliente ya no queda esperando indefinidamente (los hilos y recursos se liberan antes), pero necesita patrones complementarios (retry y fallback) para que esos cortes no lleguen como error al usuario.