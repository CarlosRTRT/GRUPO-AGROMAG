# Guia de trabajo — GRUPO-AGROMAG

Equipo de 4. Lead: **@CarlosRTRT** (unico que puede mergear a `main` y `develop`).

## 1. Ramas (Git Flow)

| Rama | Para que sirve | Quien la toca |
|---|---|---|
| `main` | Version en produccion. Solo recibe releases y hotfix. | Solo el lead, via PR |
| `develop` | Rama de integracion. De aqui sale todo el trabajo diario. | Todos, via PR |
| `feature/*` | Una tarea de Jira = una rama. Sale de `develop`, vuelve a `develop`. | Cada quien la suya |
| `release/*` | Congelar version para probar antes de `main`. | Lead |
| `hotfix/*` | Bug urgente en produccion. Sale de `main`, vuelve a `main` **y** `develop`. | Lead |

**Nombre de la rama:** `feature/AGRO-12-formulario-de-contacto`
`tipo/CLAVE-JIRA-descripcion-corta-en-kebab-case`.
Tipos validos: `feature`, `bugfix`, `hotfix`, `release`, `chore`, `docs`.

## 2. Flujo de una tarea (esto es lo que haces cada dia)

```bash
git checkout develop
git pull origin develop                      # siempre arrancar actualizado
git checkout -b feature/AGRO-12-descripcion  # tu rama

# ...trabajas, y vas commiteando de a poco...
git add .
git commit -m "feat(contacto): agrega formulario con validacion"

git push -u origin feature/AGRO-12-descripcion
gh pr create --base develop --fill           # o abrir el PR desde GitHub
```

Despues del PR: **no se mergea solo**. El lead revisa, comenta y mergea.
Cuando ya se mergeo:

```bash
git checkout develop
git pull origin develop
git branch -d feature/AGRO-12-descripcion    # borrar rama local ya integrada
```

## 3. Commits (Conventional Commits)

Formato: `tipo(alcance): descripcion en presente y minusculas`

```
feat(hero): agrega seccion hero con CTA
fix(nav): corrige menu movil que no cerraba
style(footer): ajusta espaciado en mobile
refactor(servicios): extrae tarjeta a componente
docs(readme): documenta como levantar el proyecto
chore(deps): actualiza astro a 5.x
```

Tipos: `feat`, `fix`, `style`, `refactor`, `docs`, `test`, `chore`.

Reglas simples:
- Un commit = un cambio con sentido. No `cambios varios`.
- En presente: "agrega", no "agregado" ni "agregue".
- Si el commit cierra un ticket, mencionalo: `feat(hero): agrega CTA (AGRO-12)`.

## 4. Pull Requests

- **Titulo:** `AGRO-12 feat(hero): agrega seccion hero`
- **Base:** siempre `develop` (salvo hotfix, que va a `main`).
- Llena la plantilla del PR (se carga sola).
- PRs chicos. Un PR de 2000 lineas no lo revisa nadie de verdad.
- Antes de pedir review: `npm run build` tiene que pasar.
- Si `develop` avanzo mientras trabajabas:
  ```bash
  git checkout feature/mi-rama
  git pull origin develop      # resolves conflictos aca, no en el PR
  ```

## 5. Reglas del repo (configuradas en GitHub, no son opcionales)

- No se puede pushear directo a `main` ni a `develop`. Todo entra por PR.
- Todo PR necesita **1 aprobacion del lead** (CODEOWNERS).
- No se puede forzar push (`--force`) ni borrar esas ramas.
- El merge lo hace **solo el lead**.

## 6. Convencion de Jira

- Un ticket = una rama = un PR.
- El estado del ticket lo mueve quien lo trabaja: `To Do` → `In Progress` → `In Review` (al abrir el PR) → `Done` (cuando se mergea).
- Si una tarea te toma mas de 2 dias, probablemente son dos tickets.

## 7. Comandos del proyecto

```bash
npm install      # instalar dependencias
npm run dev      # servidor local (http://localhost:4321)
npm run build    # build de produccion -> dist/
npm run preview  # ver el build ya compilado
```
