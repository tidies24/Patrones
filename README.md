# 🕵️ Guía rápida para GMs  
**Cómo usar el panel de patrones para detectar posibles cheats**

| Sección del panel | ¿Qué muestra? | ¿Por qué importa? |
|-------------------|---------------|-------------------|
| **Lista de Intervalos** | Cada intervalo (en ms) de la acción seleccionada. | Permite ver si el ritmo es constante, errático o con picos de lag. |
| **CantidadDeIntervalos** | Nº de muestras acumuladas (máx. 20). | Las métricas se calculan solo cuando hay **≥ 10** intervalos. |
| **Mínimo / Máximo / Media / Desv. Estándar** | Estadísticas básicas del historial. |  - **Media** ≈ ritmo  en su intervalo<br>- **Desv. Estándar** grande = mucha variación |
| **Ratio** (`σ / μ`) | Variabilidad relativa del patrón. | Si supera el *Threshold* (0.30) el ritmo es muy irregular. |
| **Patrón dentro… / ¡ALERTA!** | Resumen en verde/rojo según el ratio. | Verde = normal · Rojo = posible macro / lag anómalo. |
| **Score** | Suma de 5 métricas (CV alto, flip‑rate, spikes, monotónico, drift). | **Score ≥ Umbral** dispara alerta; verde = dentro de límites. |
| **Métricas activas** | Lista de reglas que sumaron puntos. | Explica **por qué** se marcó (“Spikes, Flip‑Rate”,"Drift", etc.). |
| **Umbral dinámico (effTh)** | (0.3 + 0.2 × incompletitud). | Evita falsos positivos cuando el historial está a medio llenar.|
| **Baseline µ** | Media de referencia personal (EWMA). | Se ajusta al estilo del jugador; sirve para detectar cambios sospechosos a largo plazo.
| **Drift ** | Diferencia absoluta entre la media recién medida (µ) y la Baseline µ que el sistema fue aprendiendo de ese mismo jugador. |  --- |

## 🛑 ¿Drift?
| Indicador | Valor | **Accion** |
|-----------|---------------|------------------|
| ≤ 10 ms      | totalmente normal| Nada..
| ≈ 20‑30 ms   | puede ser adaptación natural (lag, cansancio, nuevo teclado) | Revise sólo si coincide con otras métricas.|
| > 2 · σ      | Anti natural | cambio brusco y sostenido: posible macro o script.|

## 🛑 ¿Cuándo es sospechoso?

| Indicador | Valor honesto | **Bandera roja** |
|-----------|---------------|------------------|
| **Ratio** | ≤ 0.30 | > 0.30 |
| **Score** | 0 – 1 | **≥ 2** |
| **Spikes** | 0 – 1 en 20 muestras | ≥ 2 |
| **Flip‑Rate** | ≤ 3 cambios de tendencia | > 35 % flips |

> **Regla práctica:** Si cualquier fila está en rojo **y** el jugador mantiene ese estado varios ciclos consecutivos, procede a investigar o sancionar.

---

## Pasos rápidos para el GM

1. Selecciona en la lista el timer a revisar (p. ej. `UseItemWithDblClick`).
2. Observa el color del resumen:  
   - Verde → patrón normal.  
   - Rojo → mira el **Score**.
3. Si **Score ≥ 2** y “Métricas activas” apunta a macro (CV, Flip) o spikes:  
   - Pulsa **Solicitar** otra vez para refrescar.  
   - Si sigue rojo durante ~30 s (3 refrescos), toma nota del usuario.
4. Examina la **Lista de Intervalos**:  
   - Números casi idénticos → posible macro.  
   - Picos aislados → podría ser lag; verifica ping antes de sancionar.
5. Usa el chat de GM o comando interno para advertir, registrar o expulsar.

---

## ✅ Checklist final antes de actuar

- [ ] ¿Hay **≥ 10** intervalos?  
- [ ] ¿Ratio > 0.30?  
- [ ] **Score ≥ 2** marcado en rojo.  
- [ ] “Métricas activas” indican *macro* (CV, Flip) o *lag* (Spikes).  

---

### 📑 Métricas activas — ¿qué significa cada bandera?

| Métrica | Qué detecta | Interpretación rápida |
|---------|-------------|-----------------------|
| **CV Alto** | Coeficiente de variación (σ/μ) supera el umbral. | Ritmo con **demasiada dispersión** → posible auto‑click irregular o lag fuerte. |
| **Flip‑Rate** | > 35 % de cambios de tendencia entre intervalos. | Patrón **muy errático**; suele indicar spam de teclas con scripts. |
| **Spikes** | 2 o más intervalos > 2·σ fuera de la media. | **Picos aislados**: lag extremo o manipulación de paquetes. |
| **Monótono** | Serie siempre creciente o decreciente. | Ritmo **súper constante**; típico de macros “perfectos”. |
| **Drift** | Media actual se aleja > 2·σ de su baseline personal. | Cambio **sostenido** en la velocidad (puede ser macro recién activado o nueva latencia). |


