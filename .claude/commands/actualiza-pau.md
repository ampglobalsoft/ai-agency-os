---
description: Actualiza AI Agency OS desde el repo ORIGINAL de pauberenguer (upstream) y lo vuelca en tu fork. Uso — /actualiza-pau
---

# /actualiza-pau

Variante de `/actualiza` para quien trabaja con un **fork**. `/actualiza` y `scripts/update.sh` leen siempre de `origin`; en un fork, `origin` es tu copia y no ve las novedades del autor. Este comando trae primero los cambios del repo original a tu fork y después ejecuta el update normal.

Repo original (solo lectura): `https://github.com/pauberenguer/ai-agency-os.git`

## Proceso

1. Confirmar que estamos en un repo ai-agency-os (existe `vendor/sinapsis/` y `CLAUDE.md` con "AI Agency OS"). Si no, avisar y parar.
2. Comprobar el remoto `upstream`:
   ```bash
   git remote get-url upstream
   ```
   - Si no existe: `git remote add upstream https://github.com/pauberenguer/ai-agency-os.git`
   - Si existe y apunta a otra URL: avisar y preguntar antes de cambiarlo.
3. Comprobar que `origin` NO es el repo de pauberenguer (si lo es, no hay fork: usar `/actualiza` normal y parar).
4. Si hay cambios sin commitear: NO forzar. Explicar qué archivos son y preguntar (sus cosas mandan).
5. Traer lo nuevo y mostrar qué hay:
   ```bash
   git fetch upstream
   git log --oneline HEAD..upstream/main
   ```
   Si no hay commits nuevos → decir "Ya estás al día con el original" y parar.
6. Resumir al usuario los commits nuevos (y `CHANGELOG.md` si existe) y avisar de que vas a incorporarlos y subirlos a su fork.
7. Incorporar a la rama actual, sin forzar nunca:
   ```bash
   git merge --ff-only upstream/main || git merge upstream/main
   ```
   Si hay conflictos: parar, listar los archivos y resolverlos con el usuario uno a uno. No usar `--force`, ni `reset --hard`, ni `checkout --theirs/--ours` en bloque.
8. Subir al fork (es el repo del usuario, pero confirma antes del primer push de la sesión):
   ```bash
   git push origin <rama-actual>
   ```
9. Ejecutar el update normal, que ya preserva `brand-context/`, `context/`, `projects/`, `clients/`, `loops/` y las skills propias:
   ```bash
   bash scripts/update.sh
   ```
   Sin terminal entra en modo no-interactivo: mantiene la versión local ante conflictos y lista "Pendientes de decisión". Resuélvelos con el usuario como indica `/actualiza`.
10. Resumen corto de qué cambió y recordatorio: "Si algo se rompe, di **restaura** y volvemos a la anterior" (`/restaura`; backup en `.backup/`).

## Qué NO hace

- Nunca hace push a `upstream` (es de otra persona).
- Nunca fuerza push ni reescribe historial en el fork.
- No toca tus datos de operador.

## Disparadores en lenguaje natural

"actualiza desde Pau", "actualiza desde el original", "tráete lo de pauberenguer", "sincroniza con upstream".
