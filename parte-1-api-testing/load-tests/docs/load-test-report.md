# Reporte de Pruebas de Carga - Escenario 1 150 Usuarios - 2 minutos.

## Objetivo
Evaluar el rendimiento de la API Fake Store bajo carga de 150 usuarios concurrentes durante 2 minutos.
## Entorno de Prueba
Herramienta utilizada: Apache JMeter 5.6
Entorno: API Fake Store pública (https://fakestoreapi.com)

## Configuración de Prueba
- **Usuarios concurrentes:** 150
- **Duración:** 120 segundos
- **Ramp-up:** 0 segundos
- **Endpoints probados:**
  - `GET /products` (Listar productos)
  - `POST /products` (Crear producto)

## Métricas Obtenidas

### Resultados Globales
| Métrica | Valor | Evaluación |
|---------|-------|------------|
| **Total Requests** | 56,809 | Cumple|
| **Throughput** | 471.69 req/seg | Cumple |
| **Error Rate** | 0.00% | Cumple |
| **Avg Response Time** | 633.78 ms | No Cumple |
| **Max Response Time** | 8,446 ms | No Cumple |

##Análisis de hallazgos

#Comportamiento Bajo Carga
**Estabilidad del Sistema:
- La API mantuvo disponibilidad del 100% durante los 2 minutos de prueba
-  Throughput consistente (~471 req/seg) demostrando buena capacidad de procesamiento
-  Cero errores HTTP indica robustez en el manejo de requests concurrentes

**Problemas de Latencia:
-  Latencia promedio de ~950 ms está muy por encima de estándares industry
-  Picos extremos de hasta 8.4 segundos afectarían experiencia de usuario
-  Percentil 95 en 1.3 segundos indica que 5% de usuarios sufriría delays críticos

#Patrones Identificados
**Degradación Gradual:
- Los tiempos de respuesta mostraron aumento progresivo durante la prueba
- Posible acumulación de procesos o consumo de recursos
**Problemas en Ambos Endpoints:
- Al inicio de la prueba el endpoint GET presento latencia de 995ms y el POST de 832ms a partir del minuto 1Tanto GET como POST presentaron latencia de mas o menos 965 ms.
**Ausencia de Errores:
- A pesar de alta latencia, el sistema no generó timeouts o errores

##Anexos
Todas las evidencias técnicas se encuentran disponibles en el repositorio GIT del proyecto.
**Enlace
https://github.com/DanielMerchanQA/prueba-tecnicaDVP-testing-Daniel-Merchan

# Reporte de Pruebas de Carga - Escenario 2 –  Escalado de 100 a 1000 usuarios en intervalos de 150.

## Objetivo
Evaluar el rendimiento, estabilidad y escalabilidad de los endpoints de la API Fake Store bajo carga de 100 usuarios escalándose hasta los 1000 usuarios en intervalos de 150 usuarios. El objetivo es identificar tiempos de respuesta, tasa de errores y posibles cuellos de botella en los endpoints GET /products (consulta) y POST /products (creación).
## Entorno de Prueba
Herramienta utilizada: Apache JMeter 5.6
Entorno: API Fake Store pública (https://fakestoreapi.com)

## Configuración de Prueba
- **Usuarios concurrentes:** 150
- **Duración:** 480 segundos
- **Ramp-up:** 0 segundos
- **Endpoints probados:**
  - `GET /products` (Listar productos)
  - `POST /products` (Crear producto)

## Métricas Obtenidas

### Resultados Globales
| Métrica | Valor | Evaluación |
|---------|-------|------------|
| **Total Requests** | 382694 | Cumple|
| **Throughput** | 576.65 req/seg | Cumple |
| **Error Rate** | 47.63% | Cumple |
| **Avg Response Time** | 1296.18 ms | No Cumple |
| **Max Response Time** | 190806 ms | No Cumple |

##Análisis de hallazgos

#Comportamiento Bajo Carga
**Estabilidad del Sistema:
- La API mantuvo disponibilidad del 100% durante los 8 minutos de prueba
- Throughput consistente (~576 req/seg) demostrando buena capacidad de procesamiento
- Se presentó una tasa de errores del 47.63% lo que indica que la API no tiene capacidad para responder todas las peticiones exitosamente.

**Problemas de Latencia:
-  Latencia promedio de ~1296 ms está muy por encima de estándares industry
-  Picos extremos de hasta 19 segundos afectarían seriamente la experiencia de usuario
-  Percentil 95 en 23 segundos indica que 5% de usuarios sufriría delays críticos

#Patrones Identificados
**Degradación Gradual:
- Los tiempos de respuesta mostraron aumento progresivo durante la prueba
- Posible acumulación de procesos o consumo de recursos
- De acuerdo a la grafica 2 (Transactions per Second) se evidencia que cuando transcurre el minuto 2 se comienzan a evidenciar peticiones con respuestas fallidas, teniendo su pico máximo en el minuto 4 de  la prueba con un aproximado de 390 peticiones fallidas. 
**Problemas en Ambos Endpoints:
- Al inicio de la prueba el endpoint GET presento latencia de 1489ms y el POST de 822ms.
**Errores:
- El porcentaje de peticiones fallidas es superior al 45% lo que indica que el usuario no tendrá una experiencia optima al interactuar con la API.

##Anexos
Todas las evidencias técnicas se encuentran disponibles en el repositorio GIT del proyecto.
**Enlace
https://github.com/DanielMerchanQA/prueba-tecnicaDVP-testing-Daniel-Merchan
