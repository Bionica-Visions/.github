# Guía de contribución

Esta guía aplica a todos los repositorios de Biónica Visions que no tengan su propio
`CONTRIBUTING.md`. Si un repositorio tiene reglas adicionales (por ejemplo, cómo levantar el
entorno local), están en su README.

## Ramas

| Rama | Uso |
| --- | --- |
| `main` | Lo que está en producción. Protegida: solo se cambia por pull request. |
| `dev` | Integración y pruebas antes de pasar a `main` (en los repositorios que la usan). |
| `feat/<descripcion-corta>` | Funcionalidad nueva. |
| `fix/<descripcion-corta>` | Corrección de un error. |
| `chore/<descripcion-corta>` | Mantenimiento: dependencias, configuración, CI. |
| `docs/<descripcion-corta>` | Solo documentación. |

Usa minúsculas y guiones: `feat/agendamiento-recordatorios`, `fix/login-redirect-localhost`.

## Commits

Seguimos [Conventional Commits](https://www.conventionalcommits.org/es/v1.0.0/):

```text
<tipo>(<alcance opcional>): <descripción en imperativo>

feat(afiliaciones): agregar descarga del certificado en PDF
fix(auth): corregir la redirección al cerrar sesión
chore(deps): actualizar Django a 6.1.2
```

Tipos: `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `build`, `ci`, `chore`, `revert`.

- Un commit = un cambio lógico.
- Si el cambio rompe compatibilidad, agrega `!` después del tipo (`feat!:`) y explícalo en el
  cuerpo del mensaje.

## Pull requests

1. Crea tu rama desde `dev` (o desde `main` si el repositorio no usa `dev`).
2. Mantén el PR pequeño y enfocado. Si pasa de unas 400 líneas, considera dividirlo.
3. Completa la plantilla del PR: qué cambia, por qué y cómo se probó.
4. El CI debe pasar (lint, formato, pruebas y build) antes de pedir revisión.
5. Se necesita **al menos una aprobación** de otra persona del equipo.
6. Quien abre el PR lo fusiona después de la aprobación, usando **squash and merge** salvo que el
   repositorio indique otra cosa.

## Revisión de código

Al revisar, prioriza en este orden:

1. **Seguridad y datos personales:** permisos, validación de entradas, secretos, exposición de
   datos de afiliados.
2. **Corrección:** ¿hace lo que dice? ¿qué pasa en los casos límite?
3. **Pruebas:** ¿cubren el cambio?
4. **Claridad y mantenimiento.**
5. **Estilo:** de eso se encargan los linters, no la revisión.

Comenta con respeto y explica el porqué. Marca las sugerencias opcionales como `nit:`.

## Estándares de código

| Stack | Herramientas |
| --- | --- |
| Python / Django | `ruff`, `black`, `pytest`; sin migraciones pendientes (`makemigrations --check`). |
| TypeScript / React | `eslint`, `tsc` (incluido en `npm run build`), pruebas con `npm test`. |
| Contenedores | Imágenes publicadas en GHCR desde el CI; nunca desde una máquina local. |

## Secretos y datos

- **Nunca** subas archivos `.env`, credenciales, llaves ni tokens. Usa `.env.example` con valores
  ficticios y los *secrets* de GitHub Actions.
- **Nunca** uses datos reales de afiliados en pruebas, fixtures, capturas de pantalla ni issues.
- Si subiste un secreto por error, avísale al equipo de inmediato y rótalo: borrarlo del
  historial no basta.

## Issues

Usa las plantillas de **Reportar un error** o **Solicitar una funcionalidad**. Las
vulnerabilidades de seguridad **no** van en issues: sigue la [política de seguridad](SECURITY.md).
