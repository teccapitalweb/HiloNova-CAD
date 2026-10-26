# HiloNova CAD

Página de venta de **HiloNova CAD** (el programa de patronaje digital HiloNova Studio) y, dentro de la carpeta `programa/`, el programa ya compilado.

> Rama de trabajo: `dev/conectar-con-studio`. `main` no se toca hasta decidir publicar.
> Historia completa de lo hecho (22–24 de octubre de 2026): en el repositorio `hilonova-studio`, archivo `docs/CAMBIOS-OCT-2026.md`.

## Qué hay aquí

| Archivo / carpeta | Qué es |
|---|---|
| `index.html` | La página de venta: módulos, flujo, exportación, precio ($490 MXN al mes, un solo plan), preguntas frecuentes. Una sola hoja, sin dependencias. Los textos dicen solo lo que el programa hace. |
| `app.html` | Antes era una cáscara vacía; ahora redirige a `programa/auth/signin/`. |
| `assets/img/screen-*.jpg` | Capturas reales del programa que usa la página. |
| `programa/` | El programa (Next.js exportado como sitio estático con la ruta base `/programa`). **Es un archivo generado: no se edita a mano.** |
| `CNAME` | Le dice a GitHub Pages que el sitio vive en **software.hilonovamx.com** (el dominio `hilonovamx.com` lo usa el sitio de formación `hilonova-web`; no tocarlo). |
| `.nojekyll` | Evita que GitHub Pages ignore las carpetas que empiezan con `_` (el programa usa `programa/_next/`). Sin este archivo el programa no carga. |
| `PANEL` | Archivo previo del repositorio, sin uso. |

Los botones de la página («Entrar», «Crear cuenta») llevan a `programa/auth/...`.

## Cómo se regenera `programa/`

Desde el repositorio `hilonova-studio` (con el servidor de desarrollo detenido, comparten la carpeta `.next`):

```bash
node scripts/publicar-en-cad.mjs                       # ruta base /programa (dominio propio)
node scripts/publicar-en-cad.mjs "" /HiloNova-CAD/programa   # si se publica en una carpeta de GitHub Pages
```

Compila con la ruta base indicada, copia el resultado aquí, quita lo que no se usa (video, logo-kit, fotos de la portada) y deja `programa/index.html` redirigiendo a la pantalla de entrar.

## Cómo verlo en local

```bash
python -m http.server 8099 --directory .
# abrir http://localhost:8099/
```

Abrir los archivos con doble clic no funciona: los enlaces y las rutas necesitan un servidor.

## Estado

- Cuentas reales con Firebase (correo/contraseña y Google) y patrones guardados también en la nube.
- **El cobro está apagado**: todas las cuentas entran gratis hasta crear el enlace de pago de Stripe y encender el interruptor (`billing-config.ts` en el programa).
- El DXF está en validación (aún no se prueba en Gerber).
- **Dominio (26 de octubre):** `software.hilonovamx.com` (subdominio; DNS en Spaceship: un registro `CNAME` `software` → `teccapitalweb.github.io`). Ya están el `CNAME` y el `.nojekyll`; falta publicar (pasar a `main`, activar GitHub Pages con ese dominio y autorizar el dominio en Firebase → Authentication → Configuración → Dominios autorizados).
- Pendiente antes de vender: enlaces de pago reales, validación del maestro costurero y revisión legal de términos y privacidad. El guardado en la nube con Firestore real ya se probó.

## Reglas de trabajo

- Cada commit documentado (*Qué / Por qué / Verificación / Archivos*).
- Nada de promesas sin respaldo en la página: si el programa no lo hace, no se escribe.
- Nada se publica sin que el negocio lo pida.
