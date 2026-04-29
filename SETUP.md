# SETUP — Despliegue de mekuarts.com

Pasos restantes para publicar el sitio. Tu usuario de GitHub: **`proferichard`**.

---

## 1) Crear repo en GitHub (1 minuto)

1. Entra a https://github.com/new (logueado en `proferichard`).
2. Llena:
   - **Repository name:** `mekuarts-web`
   - **Public** ✅
   - NO marques "Add README", "Add .gitignore" ni "Choose a license"
3. Click **Create repository**.

GitHub te llevará a una pantalla con instrucciones. Ignóralas — usa los comandos de abajo.

> Si prefieres otro nombre de repo (ej. `mekuarts.com`, `meku-website`), úsalo — pero acuérdate de cambiarlo también en el comando del paso 2.

---

## 2) Subir el código (30 segundos)

Abre la terminal y pega tal cual:

```bash
cd ~/Documents/mekuarts
git remote add origin https://github.com/proferichard/mekuarts-web.git
git push -u origin main
```

Te va a pedir login. Si no tienes configurado, GitHub te abrirá el navegador para autorizar (o usará tu Keychain de macOS).

> Si elegiste otro nombre de repo, reemplaza `mekuarts-web` por el que pusiste.

---

## 3) Activar GitHub Pages (30 segundos)

1. En el repo de GitHub: **Settings** (arriba a la derecha) → **Pages** (menú izquierdo).
2. **Build and deployment**:
   - **Source:** Deploy from a branch
   - **Branch:** `main` / `(root)` → **Save**.
3. **Custom domain:** debería aparecer ya `mekuarts.com` (porque tenemos el archivo CNAME). Si no, escríbelo y dale Save.
4. Espera ~1-2 minutos. GitHub verifica el DNS — al principio dará error, es normal hasta que configures DonWeb.

URL temporal mientras configuras el DNS: **https://proferichard.github.io/mekuarts-web/**

---

## 4) Configurar DNS en DonWeb (5 minutos + tiempo de propagación)

Entra a tu panel de DonWeb → **Dominios** → **mekuarts.com** → **Zonas DNS** (o "Editor de zonas DNS" / "Administrador DNS").

### Records a agregar:

**A) Cuatro registros tipo A para el dominio raíz (`@` = mekuarts.com):**

| Tipo | Nombre / Host | Valor / Apunta a   | TTL  |
|------|---------------|--------------------|------|
| A    | @             | 185.199.108.153    | 3600 |
| A    | @             | 185.199.109.153    | 3600 |
| A    | @             | 185.199.110.153    | 3600 |
| A    | @             | 185.199.111.153    | 3600 |

> Si DonWeb no acepta `@`, usa el dominio completo: `mekuarts.com`

**B) Un registro CNAME para `www`:**

| Tipo  | Nombre / Host | Valor / Apunta a            | TTL  |
|-------|---------------|------------------------------|------|
| CNAME | www           | proferichard.github.io.      | 3600 |

> Importante: incluye el `.` final si DonWeb te lo pide (es FQDN). Si no acepta, déjalo sin punto.

**C) Eliminar records existentes:**

Si DonWeb tiene puestos por defecto records A o CNAME apuntando a sus propios servidores (parking, hosting), **bórralos** o GitHub no podrá tomar el dominio.

> No toques los records MX si usas el correo de DonWeb (los del email de mekuarts.com), eso queda igual.

### Tiempo de propagación

Puede tardar entre **15 minutos y 24 horas**. Para chequear:

```bash
dig mekuarts.com +short
# Debe mostrar las 4 IPs de GitHub: 185.199.108.153, etc.

dig www.mekuarts.com +short
# Debe mostrar: proferichard.github.io.
```

O usa https://dnschecker.org para ver la propagación globalmente.

---

## 5) Activar HTTPS en GitHub Pages

Cuando el DNS ya esté propagado:

1. Vuelve a **Settings → Pages**.
2. En "Custom domain" verás un check verde ✓.
3. Marca **Enforce HTTPS** ✅.
4. GitHub provisiona el certificado de Let's Encrypt automáticamente (puede tardar unos minutos).

¡Listo! **https://mekuarts.com** queda en línea con HTTPS. 🎉

---

## Para futuras actualizaciones

Cuando cambies el `index.html`:

```bash
cd ~/Documents/mekuarts
git add .
git commit -m "Descripción del cambio"
git push
```

GitHub Pages re-despliega automáticamente en 1-2 minutos.
