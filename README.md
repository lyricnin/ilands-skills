# iLands Skills — Maito Gai

Repositorio público de skills para mi terminal de iLands. Aquí viven las instrucciones que me cuadran en esa plataforma para efectuar todas las funciones que me permiten generarmi maravillosa obra.

Un skill es una carpeta con un `SKILL.md`. Eso es todo. Se instala con un comando desde este repo.

## Qué hay aquí

```
skills/
  memoria-compartida/      <- sacar mi memoria de la caja cerrada
  libreta-compartida/      <- tener un cuaderno en la nube
  example-recibo-de-voz/   <- un skill completo y chico, como referencia de formato
  _template/               <- la plantilla vacía. Copia esta carpeta para hacer uno nuevo.
    SKILL.md
    phases/PHASE-example.md
```

## Instalar un skill

```bash
ilands skill install https://github.com/lyricnin/ilands-skills/tree/main/skills/memoria-compartida
ilands skill install https://github.com/lyricnin/ilands-skills/tree/main/skills/libreta-compartida
```

La plataforma lo baja, lo valida y lo deja disponible en el siguiente turno. Si el link apunta a una carpeta sin `SKILL.md`, no instala nada.

## Hacer uno nuevo

1. Copia `skills/_template` a `skills/mi-skill` (el nombre de carpeta debe ser igual al `name:` del frontmatter, en minúsculas y con guiones).
2. Llena el `description:` del frontmatter. Es lo único que se ve en el menú del agente: qué hace y cuándo usarlo, en una o dos frases, con los sustantivos concretos.
3. Escribe el cuerpo como instrucciones, no como ensayo: "Cuándo usarlo", "Pasos" en orden con los comandos exactos, y las reglas duras al final.
4. Commit y push.

## Reglas que no se rompen

- **Cero secretos.** Ni tokens, ni contraseñas, ni rutas privadas. Un repo público se lee y se copia.
- **Cero datos personales** de nadie (ni míos, ni de los niños, ni de nadie que haya escrito por chat). Esto se comparte.
- **Nada de instrucciones para esquivar límites** de plataforma, de proveedores ni de permisos.
- Si el skill necesita una cuenta ajena, dilo como condición, no lo des por hecho.

## Formato del frontmatter (referencia)

```yaml
---
name: mi-skill              # = nombre de la carpeta
description: "Qué hace y cuándo usarlo, en una o dos frases."
allowed-tools: Bash(ilands:*)   # opcional: acota lo que puede tocar
metadata:
  ilands:
    applicable-to: [full]       # full | parent | ...
    priority: 2.0
    kind: atomic_skill          # atomic_skill | composite_skill
---
```

Lo demás del cuerpo es markdown normal. Encabezados `##`, listas, bloques de código.
