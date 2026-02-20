# Solución: Error 403 - Two-Factor Authentication

## El problema

NPM requiere autenticación de dos factores (2FA) para publicar paquetes.

## Solución 1: Habilitar 2FA en tu cuenta (Recomendado)

### Paso 1: Habilitar 2FA en npmjs.com

1. Ve a https://www.npmjs.com/settings/[tu-usuario]/tfa
2. Haz clic en "Enable 2FA"
3. Elige "Authorization and Publishing" (recomendado) o "Authorization Only"
4. Escanea el código QR con tu app de autenticación (Google Authenticator, Authy, etc.)
5. Ingresa el código de 6 dígitos para confirmar

### Paso 2: Publicar con 2FA

```bash
cd skills
npm publish --access public --otp=123456
```

Reemplaza `123456` con el código de 6 dígitos de tu app de autenticación.

## Solución 2: Usar Access Token (Alternativa)

### Paso 1: Crear un Access Token

1. Ve a https://www.npmjs.com/settings/[tu-usuario]/tokens
2. Haz clic en "Generate New Token"
3. Selecciona "Automation" (permite bypass de 2FA)
4. Copia el token generado (solo se muestra una vez)

### Paso 2: Configurar el token

```bash
npm config set //registry.npmjs.org/:_authToken TU_TOKEN_AQUI
```

### Paso 3: Publicar

```bash
cd skills
npm publish --access public
```

## Solución 3: Usar .npmrc local (Más seguro)

### Paso 1: Crear archivo .npmrc en la carpeta skills

```bash
cd skills
echo "//registry.npmjs.org/:_authToken=TU_TOKEN_AQUI" > .npmrc
```

**IMPORTANTE**: Agrega `.npmrc` a tu `.gitignore` para no subir el token a GitHub.

### Paso 2: Publicar

```bash
npm publish --access public
```

## Recomendación

**Usa la Solución 1 (2FA)** porque es más segura y es el estándar de npm.

## Comando completo con 2FA

```bash
# 1. Asegúrate de estar en la carpeta correcta
cd skills

# 2. Verifica que el build esté actualizado
npm run build

# 3. Obtén el código OTP de tu app de autenticación

# 4. Publica con el código OTP
npm publish --access public --otp=CODIGO_DE_6_DIGITOS
```

## Verificar publicación

```bash
# Ver el paquete en npm
npm view @edinsonm/skills

# Probar instalación
npx @edinsonm/skills --version
```

## Troubleshooting

### Error: OTP expired
El código OTP expira cada 30 segundos. Genera uno nuevo y vuelve a intentar.

### Error: Invalid OTP
Verifica que estés usando la app correcta y que el reloj de tu dispositivo esté sincronizado.

### Error: Token invalid
Si usas un token, verifica que:
1. El token sea de tipo "Automation"
2. El token no haya expirado
3. El token esté correctamente configurado en .npmrc

## Siguiente paso

Una vez publicado exitosamente, ejecuta:

```bash
# Probar el paquete
npx @edinsonm/skills add vercel-labs/agent-skills --non-interactive --list

# Probar en tu aplicación
npm run tauri dev
```
