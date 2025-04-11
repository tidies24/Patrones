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

## Ejemplo de Uso

- **Inicialización**: Llama a `InitializePatterns` con el número de timers.
- **Agregar Intervalos**: Usa `AddIntervalToHistory` para registrar cada nuevo intervalo.
- **Detección de Patrones**: Llama a `IsPatternSuspicious` para verificar si un patrón es anómalo.

## Consideraciones

- **Flexibilidad**: Puedes ajustar `PatternThreshold` para cambiar la sensibilidad del sistema.
- **Mantenimiento**: La estructura modular facilita la extensión y mantenimiento del código.

Este sistema permite detectar comportamientos sospechosos basados en la variabilidad de los intervalos de tiempo, proporcionando un mecanismo efectivo para el control de trampas en juegos o aplicaciones similares.
