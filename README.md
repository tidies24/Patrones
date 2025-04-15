# Control de Patrones en Timers

## Estructura del Código

### Constantes
- **MaxHistory**: Número máximo de intervalos que se almacenarán para cada timer.  
- **PatternThreshold**: Umbral de sensibilidad que determina cuándo un patrón se considera “sospechoso” en función de la variabilidad.  
- **MinInterval**: Intervalo mínimo aceptable. Cualquier intervalo menor o igual a este valor se “ignora” por considerarse imposible o muy rápido.  
- **MaxInterval**: Intervalo máximo aceptable. Si un intervalo supera este valor, se “resetea” el historial, asumiendo que ha habido una pausa demasiado grande.

> **Nota**: Estos parámetros pueden configurarse de forma **global** o de manera **específica** para cada timer.

### Clase `clsTimerPattern`
- **Propósito**: Manejar los intervalos asociados a un **solo** timer (por ejemplo, “Attack”, “UseItem”, etc.).  
- **Métodos**:
  - `Initialize(size)`: Configura el tamaño del array que almacena los intervalos (hasta `MaxHistory`).
  - `ShiftIntervals()`: Desplaza los intervalos cuando el historial está lleno, liberando espacio para el más reciente.
  - `Reset()`: Limpia todos los valores almacenados, reiniciando el historial de intervalos.


### Diccionario `TimerPatterns`
- **Descripción**: Un `Dictionary` que mapea el **índice** de cada timer (TimerIndex) con su instancia correspondiente de `clsTimerPattern`.
- **Finalidad**: Permitir acceso rápido al historial de intervalos para cada timer.  
  - Por ejemplo, `TimerPatterns("3")` podría manejar los intervalos del timer “UseItemWithU”.


## Funciones y Subrutinas

- **`InitializePatterns`**
  - Inicializa el diccionario con instancias de `clsTimerPattern`.
  - Cada instancia se configura para manejar un máximo de `MaxHistory` intervalos.

- **`DeInitializePatterns`**
  - Libera los recursos del diccionario.

- **`AddIntervalToHistory`**
  - Agrega un nuevo intervalo al historial de un timer específico.
  - Si el historial está lleno, utiliza `ShiftIntervals` para hacer espacio.

- **`IsPatternSuspicious`**
  - Evalúa si el patrón de un timer es sospechoso.
  - Calcula la media y la desviación estándar de los intervalos.
  - Compara la desviación estándar con `PatternThreshold`.

- **`CalculatePatternMetrics`**
  - Calcula la media y la desviación estándar de los intervalos.
  - Usa la fórmula estándar para la desviación estándar.

- **`GetPatternInfo`**
  - Muestra la **media**, **desviación estándar** y **rango** de intervalos con su tiempo.

- **`ResetAllPatterns`**
  - ...

## Explicación de los Cálculos

- **Media (Mean)**: Calcula el promedio de todos los intervalos registrados. Es una medida de tendencia central que ayuda a entender cuál es el intervalo típico o esperado.
  
  
    - mean = sum / tp.Count
  

- **Desviación Estándar (Standard Deviation)**: Mide la cantidad de variación o dispersión de los intervalos respecto a la media. Una desviación estándar alta indica que los intervalos varían mucho, mientras que una baja sugiere que están más agrupados alrededor de la media.
  
  
     - stdDev = Sqr((sumSq - (sum ^ 2) / tp.Count) / (tp.Count - 1))
  

Estas métricas permiten comparar el comportamiento actual de los intervalos con lo que se considera normal. Si la variabilidad (desviación estándar) es excesiva en comparación con la media, puede ser un indicativo de que algo inusual está ocurriendo, como un intento de manipulación o trampa.

## Ejemplo de Uso

- **Inicialización**: Llama a `InitializePatterns` con el número de timers.
- **Agregar Intervalos**: Usa `AddIntervalToHistory` para registrar cada nuevo intervalo.
- **Detección de Patrones**: Llama a `IsPatternSuspicious` para verificar si un patrón es anómalo.

## Consideraciones

- **Flexibilidad**: Puedes ajustar `PatternThreshold` para cambiar la sensibilidad del sistema.
- **Mantenimiento**: La estructura modular facilita la extensión y mantenimiento del código.

Este sistema permite detectar comportamientos sospechosos basados en la variabilidad de los intervalos de tiempo, proporcionando un mecanismo efectivo para el control de trampas en juegos o aplicaciones similares.
