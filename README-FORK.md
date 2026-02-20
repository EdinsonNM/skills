# Skills CLI - Fork con Modo No Interactivo

Este es un fork del CLI de skills de Vercel Labs con soporte para modo no interactivo.

## Cambios Implementados

### Nuevos Flags

- `--non-interactive`: Activa el modo no interactivo (también se activa automáticamente con `CI=true`)
- `--scope project|global`: Especifica el alcance de instalación
- `--method symlink|copy`: Especifica el método de instalación

### Comportamiento en Modo No Interactivo

Cuando el modo no interactivo está activo:
- **Agentes**: Selecciona todos los agentes detectados (o todos disponibles si no hay ninguno)
- **Skills**: Selecciona todos los skills descubiertos
- **Scope**: Usa "Project" por defecto
- **Method**: Usa "Symlink" por defecto
- **Confirmación**: Se omite automáticamente

## Uso Local

### Instalación Local

```bash
# Desde el directorio skills/
pnpm install
pnpm run build

# Enlazar globalmente para desarrollo
npm link
```

### Uso en tu Aplicación

```bash
# Modo no interactivo básico
npx skills add vercel-labs/agent-skills --non-interactive

# Con flags explícitos
npx skills add vercel-labs/agent-skills --non-interactive --scope project --method symlink

# Con skill específico
npx skills add vercel-labs/agent-skills --skill my-skill --non-interactive
```

## Integración con Rust/Tauri

El código Rust en `src-tauri/src/installer/skills.rs` ya está configurado para usar estos flags:

```rust
command
    .arg("skills")
    .arg("add")
    .arg(repository)
    .arg("--non-interactive")
    .arg("--scope")
    .arg("project")
    .arg("--method")
    .arg("symlink");
```

## Testing

Para probar que funciona correctamente:

```bash
# Test básico
cd skills
node src/cli.ts add vercel-labs/agent-skills --non-interactive --list

# Test con instalación real (en un directorio de prueba)
mkdir /tmp/test-skills
cd /tmp/test-skills
node /path/to/skills/src/cli.ts add vercel-labs/agent-skills --non-interactive
```

## Publicación (Opcional)

Si quieres publicar tu fork a npm:

```bash
# Cambiar el nombre del paquete en package.json
# "name": "@tu-usuario/skills"

# Publicar
npm publish --access public
```

O usar como dependencia de GitHub:

```json
{
  "dependencies": {
    "skills": "github:tu-usuario/skills#main"
  }
}
```
