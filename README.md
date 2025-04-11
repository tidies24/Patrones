# Control de Patrones en Timers

## Estructura del Código

### Constantes
- **MaxHistory**: Define el número máximo de intervalos que se almacenarán para cada timer.
- **PatternThreshold**: Umbral que determina si un patrón es sospechoso.

### Clase `clsTimerPattern`
- **Propósito**: Manejar los intervalos de cada timer.
- **Métodos**:
  - `Initialize`: Configura el array de intervalos.
  - `ShiftIntervals`: Desplaza los intervalos cuando el historial está lleno.

### Diccionario `TimerPatterns`
- Almacena instancias de `clsTimerPattern` para cada timer.

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
