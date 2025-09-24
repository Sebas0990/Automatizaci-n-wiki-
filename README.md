# Sistema de Alarmas para Tanque de Agua

## Descripción del Problema
Se pide realizar un sistema de alarmas para un tanque de agua.  
El sistema cuenta con:
- 3 sensores (B1, B2, B3) que miden el nivel del agua.  
- 5 alarmas (H1, H2, H3, H4, H5):  
  - 4 alarmas para indicar niveles de agua.  
  - 1 alarma para detectar errores de activación.  

Condición: Solo puede haber una alarma activa a la vez.  
Un error ocurre cuando los sensores no se activan en orden secuencial (ejemplo: se activa B3 sin que B1 y B2 estén activos).  

## Tabla de Verdad

| B1 | B2 | B3 | H1 | H2 | H3 | H4 | H5 |
|----|----|----|----|----|----|----|----|
| 0  | 0  | 0  | 0  | 0  | 1  | 0  | 0  |
| 1  | 0  | 0  | 1  | 0  | 0  | 0  | 0  |
| 1  | 1  | 0  | 0  | 1  | 0  | 0  | 0  |
| 1  | 1  | 1  | 0  | 0  | 0  | 1  | 0  |
| 0  | 1  | 0  | 0  | 0  | 0  | 0  | 1  |
| 0  | 0  | 1  | 0  | 0  | 0  | 0  | 1  |
| 0  | 1  | 1  | 0  | 0  | 0  | 0  | 1  |
| 1  | 0  | 1  | 0  | 0  | 0  | 0  | 1  |

## Implementación en CODESYS
- Entradas: interruptores de palanca (B1, B2, B3).  
- Salidas: luces de alarma (H1–H5).  
- Uso de bobinas tipo SET y RESET para asegurar que solo una salida esté activa a la vez.  
- Los errores se implementaron con lógica combinacional usando configuraciones AND–OR.  
- Se probó con simulación, confirmando la activación correcta de las alarmas según la tabla de verdad.  

## Implementación en OpenPLC
- Declaración de variables BOOL para entradas y salidas.  
- Asignación de entradas/salidas digitales en un Arduino Uno.  
- Dada la limitación de pines, la alarma de error se representa activando todas las salidas simultáneamente.  
- Conexiones en serie (para sensores) y en paralelo (para alarmas).  

## Implementación Física
- Sensores: simulados con cables a VCC conectados a las entradas.  
- Alarmas: 4 LEDs de colores distintos según el nivel de agua.  
- La configuración reproduce el comportamiento descrito en la tabla de verdad.  

## Tecnologías Utilizadas
- Codesys (programación en lógica Ladder).  
- OpenPLC (Arduino Uno).  
- Hardware físico: LEDs, cableado, protoboard, resistencias.  
