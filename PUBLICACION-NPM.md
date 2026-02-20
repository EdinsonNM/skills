# Guía de Publicación en NPM

## Paso 1: Crear cuenta en NPM (si no tienes)

1. Ve a https://www.npmjs.com/signup
2. Crea tu cuenta
3. Verifica tu email

## Paso 2: Autenticarte en tu máquina

```bash
npm login
```

Te pedirá:
- Username
- Password
- Email
- One-time password (si tienes 2FA habilitado)

## Paso 3: Verificar autenticación

```bash
npm whoami
```

Debe mostrar tu nombre de usuario.

## Paso 4: Publicar el paquete

Desde la carpeta `skills`:

```bash
cd skills
npm publish --access public
```

**Nota**: El flag `--access public` es necesario para paquetes con scope (@edinsonm/skills).

## Paso 5: Verificar publicación

Visita: https://www.npmjs.com/package/@edinsonm/skills

## Paso 6: Probar instalación

```bash
# Instalar globalmente
npm install -g @edinsonm/skills

# Verificar que funciona
skills --version

# Probar modo no interactivo
npx @edinsonm/skills add vercel-labs/agent-skills --non-interactive --list
```

## Actualizar versión (para futuras publicaciones)

```bash
# Incrementar versión patch (1.4.0 -> 1.4.1)
npm version patch

# Incrementar versión minor (1.4.0 -> 1.5.0)
npm version minor

# Incrementar versión major (1.4.0 -> 2.0.0)
npm version major

# Publicar nueva versión
npm publish --access public
```

## Integración con tu aplicación Tauri

Una vez publicado, actualiza tu código Rust para usar el paquete de npm:

```rust
// En src-tauri/src/installer/skills.rs
// Cambia de:
.arg("skills")

// A:
.arg("@edinsonm/skills")
```

O simplemente usa:

```bash
npx @edinsonm/skills add <repo> --non-interactive
```

## Troubleshooting

### Error: 403 Forbidden

Si obtienes un error 403, verifica:

1. Que estés autenticado: `npm whoami`
2. Que el nombre del paquete no esté tomado
3. Que uses `--access public` para paquetes con scope

### Error: Package name too similar

Si el nombre es muy similar a otro paquete, npm puede rechazarlo. Considera:

- `@edinsonm/agent-skills`
- `@edinsonm/skills-cli`
- `@edinsonm/gravion-skills`

### Cambiar nombre del paquete

Si necesitas cambiar el nombre:

1. Edita `skills/package.json` y cambia el campo `"name"`
2. Ejecuta `npm run build`
3. Ejecuta `npm publish --access public`

## Comandos útiles

```bash
# Ver información del paquete
npm view @edinsonm/skills

# Ver versiones publicadas
npm view @edinsonm/skills versions

# Despublicar versión (solo en las primeras 72 horas)
npm unpublish @edinsonm/skills@1.4.0

# Deprecar versión
npm deprecate @edinsonm/skills@1.4.0 "Use version 1.4.1 instead"
```

## Siguiente paso

Una vez publicado, actualiza tu aplicación para usar:

```bash
npx @edinsonm/skills add <repo> --non-interactive
```

En lugar de depender de `npm link` local.
