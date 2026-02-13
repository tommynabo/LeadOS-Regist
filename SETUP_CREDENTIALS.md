# 🔐 Setup de Credenciales - Email Discovery Pipeline

Guía paso a paso para configurar TODAS las credenciales que necesitas para el pipeline de descubrimiento de emails en cascada.

**Tiempo total**: ~30-45 minutos  
**Coste**: $0 (TODO GRATIS)

---

## 📋 Credenciales Necesarias

| Credencial | ¿Ya tienes? | Coste | Tiempo Setup |
|------------|-------------|-------|--------------|
| ✅ Apify API Token | SÍ | $0 (créditos) | Ya hecho |
| ❌ Google Cloud Project + Custom Search | NO | $0 | 15 mins |
| ✅ OpenAI API Key | SÍ (mencionado) | $0.001/request | 5 mins |
| ❌ Custom Search Engine ID | NO | $0 | 5 mins |
| ✅ WHOIS APIs | SÍ (públicas) | $0 | 0 mins |
| ✅ SMTP Validation | SÍ (local) | $0 | 0 mins |
| ✅ Twitter/Apify | SÍ | Incluido | 0 mins |

---

## 🚀 PASO 1: Google Cloud Project (15 mins)

### Objetivo
Crear un proyecto en Google Cloud para poder usar **Google Custom Search API** (100 búsquedas/día GRATIS).

### Pasos

**1.1 Ir a Google Cloud Console**
```
1. Ve a https://console.cloud.google.com/
2. Si no tienes cuenta, crea una (puedes usar tu Gmail actual)
3. Click en "Select a Project" (arriba a la izquierda)
4. Click en "NEW PROJECT"
```

**1.2 Crear nuevo proyecto**
```
Nombre: LeadOS-EmailDiscovery
(o algo así, el nombre no importa)

ID del proyecto: Se genera automático (ej: leadosos-123456)
Location: Sin cambios (dejar por defecto)

Espera ~30 segundos a que se cree el proyecto
```

**1.3 Habilitar Custom Search API**

```
1. En la consola, ve a: Apis y servicios → Biblioteca
   (O directamente: https://console.cloud.google.com/apis/library)

2. Busca: "Custom Search API"

3. Click en "Custom Search API"

4. Click en botón azul "HABILITAR"

5. Espera a que cargue (30 segundos)
```

**1.4 Crear credenciales (API Key)**

```
1. Ve a: Apis y servicios → Credenciales
   (O: https://console.cloud.google.com/apis/credentials)

2. Click en "CREATE CREDENTIALS"

3. Selecciona "API Key"

4. Se abrirá un popup con tu API Key:

   COPIAR ESTE VALOR (es algo como: AIzaSy...)
   
5. Haz click en "CLOSE"

6. Guarda el valor en un lugar seguro (pronto lo necesitarás)
```

**RESULTADO**: Tienes tu `GOOGLE_API_KEY` ✅

---

## 🔎 PASO 2: Google Custom Search Engine (5 mins)

### Objetivo
Crear el buscador personalizado que harás búsquedas. Necesitas crear **al menos 1** (recomiendo 2 si tienes 2 proyectos).

### Pasos

**2.1 Ir a Programmable Search Console**
```
Ve a: https://programmablesearchengine.google.com/
(o busca "Google Programmable Search Engine")

Sign in con tu cuenta Google (la misma del paso anterior)
```

**2.2 Crear primer Custom Search Engine**

```
1. Click en "Create"

2. Rellena:
   Name: "LeadOS-Project1-Search"
   
   Sites to search: 
   Deja el campo vacío o pon: *.com *.es
   
   (Esto busca en TODO internet, no solo sitios específicos)

3. Click en "CREATE"

4. Se abrirá el editor de tu Custom Search Engine

5. IMPORTANTE: En la barra de arriba, busca tu ID:
   
   Debería ser algo como: 12345678901234567:abc123def456
   
   CÓPIALO (es tu GOOGLE_CUSTOM_SEARCH_ENGINE_ID #1)
```

**2.3 (OPCIONAL) Crear segundo Custom Search Engine para Proyecto 2**

```
Repite 2.1-2.2 pero con nombre:
"LeadOS-Project2-Search"

Así cada proyecto tiene su propio buscador con 100 búsquedas/día
```

**RESULTADO**: Tienes tu `GOOGLE_CUSTOM_SEARCH_ENGINE_ID` ✅

---

## 🤖 PASO 3: Verificar OpenAI API Key (5 mins)

### Objetivo
Confirmar que tienes acceso a OpenAI para GPT-4o-mini (que YA usas en el código).

### Pasos

**3.1 Ve a OpenAI**
```
https://platform.openai.com/api/keys

Sign in con tu cuenta OpenAI
(Si no tienes, crea una en https://openai.com/api/)
```

**3.2 Copiar API Key existente o crear una nueva**

```
Si ves items en "API keys":
└─ Click en un item existente
└─ Copia el valor (starts with sk-...)
└─ Este es tu VITE_OPENAI_API_KEY

Si no hay ninguna:
└─ Click en "+ Create new secret key"
└─ Nombre: "leadosos-email-discovery"
└─ Copia el valor (aparece una sola vez)
```

**3.3 Verificar que funciona**

```
Abre tu .env local y busca:
VITE_OPENAI_API_KEY=sk-...

Si no existe, añádela ahora con el valor de OpenAI
```

**RESULTADO**: Confirmado `VITE_OPENAI_API_KEY` ✅

---

## 🔌 PASO 4: APIs Públicas (0 mins - NO NECESITAN CREDENCIALES)

Estos funcionan sin credenciales adicionales:

### WHOIS Lookups
```
API gratuita: https://whoisjsonapi.com/api/v1/{domain}
NO necesita autenticación
Alternativa: https://api.domainsbot.com/v2/whois
```

### SMTP Validation
```
Validación local usando DNS + SMTP
Se hace por código (no requiere API key)
```

### Twitter/X Scraping
```
Usarás Apify (que YA tienes)
NO requiere credencial extra de Twitter
```

---

## 📝 PASO 5: Guardar todo en .env (10 mins)

### Dónde guardar

Abre el archivo `.env.local` en la raíz del proyecto LeadOS:

```bash
# En la terminal
cd /Users/tomas/Downloads/DOCUMENTOS/LeadOS\ -\ Regist
nano .env.local
# o abre con VS Code
```

### Qué añadir

Busca estas variables y actualiza (o añade si no existen):

```bash
# ═══════════════════════════════════════════════════════════════
# APIFY (Ya deberías tener esto)
# ═══════════════════════════════════════════════════════════════
VITE_APIFY_API_TOKEN=apify_api_...    # (Ya tienes)

# ═══════════════════════════════════════════════════════════════
# GOOGLE CUSTOM SEARCH (NUEVO)
# ═══════════════════════════════════════════════════════════════
GOOGLE_API_KEY=AIzaSyA8jTHMYinq4HWzdnorrd4-Qbcf0nBnLzI              # Del PASO 1.4
GOOGLE_CUSTOM_SEARCH_ENGINE_ID=06fdb20f849ed4c2e                   # Del PASO 2.2

# ═══════════════════════════════════════════════════════════════
# OPENAI (Probablemente ya está)
# ═══════════════════════════════════════════════════════════════
VITE_OPENAI_API_KEY=sk-...            # Verificado en PASO 3

# ═══════════════════════════════════════════════════════════════
# NUEVAS OPCIONALES: Si tienes 2 Custom Search Engines
# ═══════════════════════════════════════════════════════════════
# GOOGLE_CUSTOM_SEARCH_ENGINE_ID_PROJECT2=12345678901234567:xyz789uvw012  # Del PASO 2.3 (opcional)
```

**Guarda el archivo**:
```bash
Press Ctrl+X, then Y, then Enter (en nano)
o Cmd+S en VS Code
```

---

## ✅ CHECKLIST DE VERIFICACIÓN

Antes de empezar a código, verifica que tienes TODO:

```
☐ Google Cloud Project creado
☐ Custom Search API habilitada
☐ API Key de Google generada (GOOGLE_API_KEY)
☐ Custom Search Engine creado (GOOGLE_CUSTOM_SEARCH_ENGINE_ID)
☐ (OPCIONAL) Segundo Custom Search Engine para Proyecto 2
☐ OpenAI API Key activa (VITE_OPENAI_API_KEY)
☐ Archivo .env.local actualizado con todas las claves
☐ Apify tokens en .env.local (ya tienes)
```

---

## 🆘 Si algo va mal

### "Google API Key inválida"
```
1. Ve a https://console.cloud.google.com/apis/credentials
2. Verifica que "Custom Search API" esté HABILITADA
3. Si no, habilítala desde biblioteca
4. Genera una nueva API Key si es necesario
5. Copia exactamente sin espacios
```

### "Custom Search Engine ID no funciona"
```
1. Ve a https://programmablesearchengine.google.com/
2. Click en tu custom search engine
3. En la barra superior, busca el ID (formato: 12345:abc123)
4. Copia EXACTAMENTE
5. Asegúrate que no hay espacios antes/después
```

### "OpenAI API Key rechazada"
```
1. Ve a https://platform.openai.com/api/keys
2. Verifica que la key no esté marcada como "revoked"
3. Si está revoked, crea una nueva
4. Copia sin espacios
5. Verifica que empiece con "sk-"
```

### "No puedo crear Google Cloud Project"
```
- Asegúrate de estar logueado en Google
- Si necesitas verificación, sigue los pasos de Google
- A veces pide tarjeta de crédito (pero no cobra si usas gratis)
```

---

## 💰 RESUMEN DE COSTOS FINALES

```
Google Custom Search:     $0    (100 búsquedas/día GRATIS)
Google API Key:           $0    (sin coste directo)
OpenAI (gpt-4o-mini):     $6/mes (si haces ~100 leads/día)
WHOIS:                    $0    (públicas)
SMTP:                     $0    (local)
Apify:                    $0    (créditos gratis 4 cuentas = $20)

═════════════════════════════════════════════════════════
TOTAL:                    $6/mes MÁXIMO
```

---

## 🎯 Próximos pasos

Una vez tengas TODO en .env.local, avísame y empezaremos a implementar:

1. `EmailDiscoveryPipeline.ts` con los 7 intentos
2. Integración en `SearchService.ts`
3. Load balancing de cuentas Apify
4. Dashboard de stats

¿Ya tienes todo? 🚀
