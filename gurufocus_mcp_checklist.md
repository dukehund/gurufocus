# Checklist: Conectar MCP de GuruFocus en OpenCode

Objetivo: conectar el MCP de GuruFocus (`https://api.gurufocus.com/mcp`) desde OpenCode usando la API key, **sin comprometerla** (sin escribirla en archivos).

## Pasos

### [ ] Paso 0 — Obtener la API key
- [ ] Obtener la API key de GuruFocus desde la cuenta.

### [ ] Paso 1 — Guardar la key en variable de entorno
- [ ] Añadir a `~/.bashrc` o `~/.zshrc`:
  ```sh
  export MCP_API_KEY="skg-..."
  ```
- [ ] Recargar la shell o exportarla en la sesión actual.

### [ ] Paso 2 — Agregar el servidor MCP
- [ ] `opencode mcp add gurufocus --url https://api.gurufocus.com/mcp --global`
- [ ] Editar `~/.config/opencode/opencode.json`:
  ```jsonc
  {
    "$schema": "https://opencode.ai/config.json",
    "mcp": {
      "servers": {
        "gurufocus": {
          "type": "remote",
          "url": "https://api.gurufocus.com/mcp",
          "oauth": false,
          "headers": {
            "Authorization": "Bearer {env:MCP_API_KEY}"
          }
        }
      }
    }
  }
  ```

### [ ] Paso 3 — Verificar la conexión
- [ ] Ejecutar: `opencode mcp list`
- [ ] Confirmar estado: `✓ gurufocus connected`

### [ ] Paso 4 — Usar el MCP
- [ ] Iniciar sesión de OpenCode.
- [ ] Ejecutar `/mcps` para revisar estado/conexión.
- [ ] Probar con un pedido tipo: "dame el perfil y valuation de Apple".

### [ ] Paso 5 — Verificar tools disponibles
- [ ] Confirmar que las tools se listan (fundamentals, rankings, valuations, dividends, news, etc.).
- [ ] Recordar: con tier gratuito, algunas tools pueden no estar disponibles o devolver menos datos.

## Seguridad (API key)

- [ ] Nunca escribir la API key literal en `opencode.json` ni en archivos del repo.
- [ ] Usar siempre la sustitución `{env:MCP_API_KEY}`.
- [ ] No commitear archivos de config con secrets.

## Referencias

- GuruFocus MCP doc: `./gurumcp.md`
- OpenCode MCP docs: <https://opencode.ai/v2/docs/mcp-servers>
