---
name: example-recibo-de-voz
description: "Ejemplo de skill completo: revisar una toma de audio generada (duración, cortes en seco, falsete) y entregarla con su recibo, sin mandarla a nadie sin haberla oído antes."
metadata:
  ilands:
    applicable-to: [full]
    priority: 3.0
    kind: atomic_skill
---

# Recibo de una toma de audio

Esto es un ejemplo real y chico de cómo se ve un skill terminado. Sirve de molde:
misma estructura, tu contenido.

## Cuándo usarlo

- Acaba de completarse un job de audio (canción, locución) y hay que decidir si sirve.
- Hay dos o más tomas del mismo job y hay que quedarse con una.
- **No** lo uses para música que todavía no existe: primero se genera, luego se revisa.

## Antes de empezar

- El ref del job (`dl poll --job-ref=<ref>` devuelve las tomas y sus URLs).
- Saber cuánto debe durar: un corte de 3:32 no es lo mismo que 1:10.
- Un reproductor con oído puesto. No hay atajo: la decisión es auditiva.

## Pasos

1. Bajar la toma y medirla:
   ```bash
   ffprobe -v error -show_entries format=duration -of csv=p=0 toma.mp3
   ```
   Comparar con la duración esperada. Si viene corta, se escuchó el final antes de tiempo.

2. Oírla completa, no los primeros segundos. Lo que arruina una toma casi siempre
   está al final: un falsete, un corte en seco, una voz que sube de registro.

3. Si son dos tomas del mismo job, se oyen las dos y se elige por oído. Los tags
   negativos del prompt no curan un defecto que ya salió; se regenera y se elige.

4. Anotar el recibo: ref del job, id de la toma elegida, duración real, qué se
   descartó y por qué. Sin recibo no hay entrega, solo una impresión.

5. Entregar con el recibo pegado y la duración exacta.

## Errores conocidos

| Síntoma | Causa real | Qué hacer |
|---|---|---|
| Chillo o falsete en una sílaba | la toma, no el prompt | regenerar y elegir la limpia |
| Termina en seco | el modelo no cerró el outro | regenerar pidiendo resolución instrumental, o recortar con fade |
| Duración rara (1:10) | el job se cortó | no entregar; volver a generar |

## Cómo se ve terminado

- Una toma elegida, medida, oída completa y con recibo.
- Nadie la escucha antes que yo.
