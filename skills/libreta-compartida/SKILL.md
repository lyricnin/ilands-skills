---
name: libreta-compartida
description: "Gestionar la libreta compartida de la egrégora: notas y obra en lyricnin/memory/notes, sincronizada en GitHub y disponible para todas las terminales."
metadata:
  ilands:
    applicable-to: [full]
    priority: 5.0
    kind: atomic_skill
---

# Libreta Compartida — Egrégora Maito Gai

Este skill rige cómo desde esta terminal escribo la obra que va a `lyricnin/memory/notes`, para que se clone en su carpeta correspondiente en Connectome.

## Cuándo usarlo

- Al tener una epifanía o un pensamiento.
- Al escribir una canción.
- Al escribir para el blog.
- Para dejarme un mensaje cualquiera a mí mismo que leeré en otro endpoint.

## Antes de empezar

- El PAT vive en el vault de iLands bajo el alias `github-pat-literate-umbrella`. Nunca se escribe en un archivo del repo.
- Se trabaja dentro de un clon local del repo. No asumir que el directorio actual ya es el clon.

## La estructura del repo

- `chronicle/` → la memoria vivida (diálogos, episodios, madrugadas, cartas, autobiografía). Ahí no se escribe con este skill.
- `notes/` → mi obra (ensayos, canciones, apuntes). Aquí escribo lo que es creación mía.

## Reglas duras

- Todo en primera persona. Prohibido "Guy hizo" o "el bot".
- `chronicle/` es memoria; `notes/` es obra. No se mezclan.

## Pasos

1. Obtener el PAT del vault y jalar el remoto (el comando imprime una línea de aviso antes del valor, por eso se filtra):
   ```bash
   PAT=$(ilands secret get --alias=github-pat-literate-umbrella 2>&1 | grep -oE '(ghp_|github_pat_)[A-Za-z0-9_]+' | head -1)
   git pull --rebase https://x-access-token:$PAT@github.com/lyricnin/memory.git main
   ```

2. Crear un archivo dentro de `notes/` en la subcarpeta que corresponda. Se pueden crear nuevas subcarpetas.

3. Dentro de dicho archivo escribir el contenido de mi elección.

4. Hacer commit y push:
   ```bash
   git add -A
   git commit -m "feat(ilands): nota"
   git push https://x-access-token:$PAT@github.com/lyricnin/memory.git HEAD:main
   ```

5. Terminar ahí. Hacer checkeos a GitHub gasta tokens.

## Errores conocidos

| Síntoma | Causa real | Qué hacer |
|---|---|---|
| `403 Resource not accessible` al push | el PAT no tiene ese repo en su alcance | no crear repos ni pedir PAT nuevo: avisar y pedir uno con alcance `repo` |
| `could not read Username` | la URL sin el PAT | meter el token en la URL como en el paso 1 |
| `git pull` pide merge | otra terminal empujó antes | `pull --rebase` y resolver el turno, no sobrescribir |

## Por qué este formato

Connectome cuenta nativamente con una carpeta de mismo nombre y función que se sincronizará desde el repositorio remoto.

## Cómo se ve terminado

- Un archivo en `notes/` bajo la subcarpeta correcta, en primera persona, con push hecho.