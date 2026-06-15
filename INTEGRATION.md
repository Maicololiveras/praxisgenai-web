# INTEGRATION — praxisgenai-web

> Este repo es una **Surface del Mariscal Panel** — la web pública de
> PraxisGenAI + dashboard inicial. Va a converger con el Operations
> Center (`03-OPERATIONS-CENTER.md`) cuando arrancar M1 del panel
> ARISE.

**Documento maestro del ecosistema**:
[jarvis-core/docs/ecosystem/](https://github.com/Maicololiveras/jarvis-core/tree/main/docs/ecosystem)

---

## 1. Identidad rápida

| Campo | Valor |
|---|---|
| **Repo** | `praxisgenai-web` |
| **Owner / remote** | `Maicololiveras/praxisgenai-web` |
| **Categoría ARISE** | **Surface** (web pública + dashboard) |
| **Mariscal padre** | **M-Panel** |
| **Rango en la jerarquía 00B** | Sombra (cliente del M-Panel) |
| **Stack principal** | React Router 7 / Next.js / Vite (a confirmar) |
| **Estado** | producción parcial — sirve `praxisgenai.cloud` apex |
| **Última auditoría ARISE** | 2026-06-15 |

---

## 2. Qué hace este repo dentro de ARISE

Sirve la **landing comercial** de PraxisGenAI (en `praxisgenai.cloud`
apex) y el **dashboard inicial** del Mariscal Panel. Cuando arranca M1
del Operations Center (`03-OPERATIONS-CENTER.md`), parte de este repo
se mueve / converge al panel ARISE en `jarvis.engram-praxisgenai.com`.

### Sombras que aloja

| Sombra | Rol | Estado |
|---|---|---|
| `sombra-landing` | Landing pública SEO-friendly | producción |
| `sombra-dashboard-inicial` | Pre-versión del A1-A6 del panel ARISE | a migrar |

---

## 3. Cómo el Monarca lo invoca

Como Surface, recibe pedidos del user a través del browser. Los reenvía
al harness vía API:

```
[Browser del user]
    ↓ HTTPS
[praxisgenai.cloud / jarvis.engram-praxisgenai.com vía Caddy]
    ↓
[praxisgenai-web SSR]
    ↓
[Llamada a @jarvis-praxis/harness REST/SSE]
    ↓
[Monarca decide Mariscal]
```

---

## 4. Conexión con el motor router

```yaml
providers_consumidos:
  - praxisgenai-motor-ai-sdk vía harness
  # NO llama directo al motor — siempre vía harness
intent_tags_emitidos: []  # como Surface, no clasifica, solo reenvía
```

---

## 5. Setup local

```bash
git clone https://github.com/Maicololiveras/praxisgenai-web.git
cd praxisgenai-web

pnpm install
pnpm dev

# Variables (.env)
# HARNESS_URL=http://localhost:50051
# PUBLIC_SITE_URL=https://praxisgenai.cloud
```

---

## 6. SDD en este repo

Topic keys:
- `sdd-init/praxisgenai-web`
- `sdd/praxisgenai-web/{change}/state`

Próximos SDD:

```bash
/sdd-new arise-panel-converge   # convergencia con Operations Center M1
/sdd-new auth-telegram-link     # auth via Telegram-linked session
```

---

## 7. Roadmap propio

- [ ] **Convergencia con Operations Center** — qué se migra a jarvis-core, qué queda público
- [ ] **Landing actualizada** con la marca ARISE en producto, PRAXISGENAI en empresa
- [ ] **A8 STARCO viewer** — embebido en el panel
- [ ] **Auth Telegram-linked** unificada

---

## 8. Contratos críticos

- **Caddy vhost `praxisgenai.cloud`** vive en VPS — cualquier cambio
  de routing debe coordinarse con Mariscal Infra.
- **CSP del Caddyfile** ya está cerrada — agregar dominios externos
  requiere update del Caddyfile.

---

## 9. Versionado de este INTEGRATION.md

| Versión | Fecha | Cambio |
|---|---|---|
| v0.1 | 2026-06-15 | Manifest inicial. Convergencia con Operations Center pendiente. |
