# Como trabajamos

## Ramas

- `main` — produccion. No se toca.
- `develop` — de aca sale y aca vuelve todo el trabajo.
- `feature/AGRO-12-descripcion-corta` — tu tarea. Un ticket de Jira = una rama = un PR.

Prefijos segun el caso: `feature/`, `bugfix/`, `docs/`, `chore/`.

## Tu dia

```bash
git checkout develop
git pull origin develop                      # arrancar actualizado, siempre
git checkout -b feature/AGRO-12-descripcion

# ...trabajas y commiteas de a poco...
git add .
git commit -m "feat(contacto): agrega formulario"

git push -u origin feature/AGRO-12-descripcion
gh pr create --base develop --fill
```

Despues avisas y el lead lo revisa y lo mergea. **Vos no mergeas.**

## Commits

`tipo(alcance): que hace, en presente y minusculas`

```
feat(hero): agrega seccion hero con CTA
fix(nav): corrige menu movil que no cerraba
docs(readme): documenta como levantar el proyecto
```

Tipos: `feat`, `fix`, `style`, `refactor`, `docs`, `chore`.
Un commit = un cambio con sentido. Nada de "cambios varios".

## Pull Requests

- Titulo con el ticket: `AGRO-12 feat(hero): agrega seccion hero`
- Base: `develop`
- El check de CI tiene que estar en **verde** antes de pedir revision
- PRs chicos. Uno de 2000 lineas no lo revisa nadie de verdad
- Si `develop` avanzo mientras trabajabas: `git pull origin develop` en tu rama y resolves los conflictos ahi

## Reglas que GitHub aplica solo

No se puede pushear directo a `main` ni `develop`, no se puede hacer force push, y el merge lo hace unicamente el lead.
