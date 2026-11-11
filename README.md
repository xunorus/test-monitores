# Test de monitores

Herramienta web de una sola página (sin dependencias, Web Audio API) para verificar que dos monitores de estudio estén **balanceados en volumen** y bien alineados.

👉 **Usar online:** https://xunorus.github.io/test-monitores/

## Qué permite probar

| Sección | Para qué |
|---|---|
| **1 · Nivel por canal** | Ruido rosa por canal (L / ambos / R), alternancia automática cada 2 s para leer el SPL sin tocar nada, y **trims independientes ±12 dB** (se guardan en `localStorage`) para emparejar los niveles. Medidores L/R de salida. |
| **2 · Paneo** | Slider manual y barrido automático (2–16 s por ciclo): el centro debe quedar en el medio físico, sin saltos ni huecos. |
| **3 · Fase y polaridad** | Tono de 100 Hz en ambos canales, con inversión de fase de un canal: fuera de fase el grave debe casi desaparecer. Si se cae *en fase*, hay un cable invertido. |
| **4 · Barrido** | Barrido senoidal 20 Hz → 20 kHz (5/10/20/30 s) y tonos fijos de 40 Hz a 16 kHz para detectar baches de crossover, resonancias y sibilancias. |

Atajos: `espacio` parar · `L` izquierda · `R` derecha · `B` ambos.

## Procedimiento rápido

1. Fijá el volumen de salida de la interfaz y no lo toques más. Dejá el balance del sistema centrado.
2. App de SPL en el celular (Decibel X, NIOSH SLM), ponderación **C o Z**, respuesta **Slow**, en el punto de escucha y sin moverlo entre mediciones.
3. Ruido rosa → **Izquierda**, anotá dB → **Derecha**, anotá dB. Con *Alternar* no debería saltar más de ±1 dB.
4. Bajá con el trim el canal que mide más fuerte hasta quedar dentro de 1 dB.
5. Si hace falta más de 3 dB de corrección, el problema es ubicación / toe-in / simetría de la sala, no el nivel.
6. Verificá con el barrido de paneo y el barrido de frecuencia.

## Notas

- El navegador no puede distinguir L de R con el micrófono interno (es mono), por eso la medición absoluta se hace con un SPL externo; la página genera la señal y aplica los trims.
- El audio arranca recién con el primer clic o tecla (política de autoplay). Empezá con el volumen maestro bajo.
- Todo corre local: no hay backend, ni red, ni telemetría.
