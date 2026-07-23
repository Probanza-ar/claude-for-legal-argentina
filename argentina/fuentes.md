# Fuentes normativas y jurisprudenciales argentinas · mcp-legal-ar

La capa de conectores del sistema es el hub `mcp-legal-ar`: un único conector
MCP que da acceso simultáneo a 14 fuentes jurídicas argentinas. Reemplaza a los
conectores sueltos de la comunidad (que el hub reúne y reensambla en una sola
instalación) y a los conectores originales del repositorio base (Westlaw,
CourtListener, Everlaw) para práctica local.

Los conectores son la segunda capa del sistema. Los perfiles de práctica
funcionan sin ellos. Con el hub, el sistema consulta fuentes primarias
automáticamente sin que el abogado tenga que pegar el texto de la norma o del
fallo en la sesión.

`mcp-legal-ar` es 100% local (transporte stdio, sin servidores intermediarios),
solo lectura y de código abierto auditable. Repositorio:
https://github.com/Probanza-ar/mcp-legal-ar

La instalación no se documenta acá para no duplicarla: está en el README del hub.
Resumen: requiere Node.js, se baja el repo y se agrega un bloque a
`claude_desktop_config.json` apuntando a `build/index.js`. Una sola instalación
deja las 14 fuentes disponibles al mismo tiempo.

---

## Cómo verificar que el hub está activo antes de usarlo

Una sola verificación, no 14:

1. En Claude Desktop: confirmar que `mcp-legal-ar` figura en la lista de
   conectores activos. Si no aparece, revisar `claude_desktop_config.json` y
   reiniciar Claude Desktop desde la bandeja del sistema.
2. Consulta de prueba mínima antes de la consulta real: cualquier
   `*__alcance_fuente` (o `juba__info`) devuelve la cobertura del conector sin
   tocar la web. Si responde, el hub está cargado.

**Si un conector puntual no responde** (la web oficial de esa fuente está caída),
el resto del hub sigue funcionando. No reintentar la misma consulta dos veces:
aplicar el fallback de la tabla y registrar en la sesión que la fuente no estaba
disponible.

Cuando se usa el fallback manual (pegar texto en sesión), indicar siempre al
inicio del texto pegado: fuente, fecha de consulta y URL de origen.

---

## Conectores del hub

| # | Conector | Prefijo de tool | Cobertura | Fallback oficial |
|---|----------|-----------------|-----------|------------------|
| 1 | BORA | `bora__` | Boletín Oficial nacional | boletinoficial.gob.ar |
| 2 | BOPBA | `bopba__` | Boletín Oficial PBA | boletinoficial.gba.gob.ar |
| 3 | InfoLeg | `infoleg__` | Legislación nacional (texto actualizado) | infoleg.gob.ar |
| 4 | Normativa PBA | `normativapba__` | Legislación provincial PBA | normas.gba.gob.ar |
| 5 | JUBA | `juba__` | Jurisprudencia SCBA y cámaras PBA | juba.scba.gov.ar |
| 6 | PTN | `ptn__` | Dictámenes Procuración del Tesoro | busquedadictamenes.ptn.gob.ar |
| 7 | TFN | `tfn__` | Jurisprudencia Tribunal Fiscal de la Nación | tfn.gob.ar |
| 8 | SCBA | `scba__` | Sentencias y resoluciones primera instancia PBA | sentencias.scba.gov.ar |
| 9 | PJN Consulta | `pjn__` | Estado procesal de expedientes federales (HITL) | pjn.gov.ar |
| 10 | SAIJ | `saij__` | Jurisprudencia + legislación + doctrina + dictámenes | saij.gob.ar |
| 11 | PJN Jurisprudencia | `pjnjuris__` | Sumarios de cámaras nacionales y federales (HITL) | pjn.gov.ar |
| 12 | Portal PJN | `portalpjn__` | Feed de novedades del abogado logueado (HITL + SSO) | portalpjn.pjn.gov.ar |
| 13 | JusCABA | `juscaba__` | Expediente Judicial Electrónico CABA (EJE) | eje.juscaba.gob.ar |
| 14 | CSJN | `csjn__` | Sumarios de jurisprudencia CSJN (1863-2026) | sj.csjn.gov.ar |

Cada conector expone `*__alcance_fuente` con su cobertura y límites declarados.
Abajo, el detalle por conector.

---

### 1. BORA — `bora__`

**Fuente:** boletinoficial.gob.ar (Boletín Oficial de la República Argentina).
**Cubre:** normas nacionales, actos administrativos, edictos y avisos publicados
desde 1938. Portada del día, sumario por fecha, texto verbatim de avisos por ID,
nuevas sociedades (Segunda Sección) y licitaciones (Tercera Sección).
**Tools principales:** `bora__obtener_sumario_del_dia`, `bora__buscar_avisos`,
`bora__obtener_detalle_aviso`, `bora__buscar_nuevas_sociedades`,
`bora__buscar_licitaciones_publicas`.

Casos de uso:
- Verificar el texto exacto de un decreto o resolución publicado en una fecha
- Confirmar si una norma fue publicada en el BORA y obtener el PDF firmado
- Rastrear la constitución de una sociedad o una licitación por organismo

Límites:
- Solo BORA nacional; no incluye boletines provinciales (para PBA, conector 2)
- Devuelve la publicación original, no el texto consolidado con modificaciones:
  para vigencia consolidada usar InfoLeg (conector 3)

**Fallback:** boletinoficial.gob.ar acceso directo.

---

### 2. BOPBA — `bopba__`

**Fuente:** boletinoficial.gba.gob.ar (Boletín Oficial de la Provincia de Buenos Aires).
**Cubre:** legislación y actos administrativos provinciales PBA. Búsqueda por
fecha, número de norma y texto libre.
**Tools principales:** `bopba__buscar_boletin`, `bopba__descargar_seccion`,
`bopba__exportar_seccion`.

Casos de uso:
- Verificar la publicación oficial de una norma PBA por fecha y número
- Rastrear la cadena de modificaciones de una ley provincial por sus publicaciones

Límites:
- Solo Boletín Oficial PBA; no cubre BORA nacional ni otras provincias
- Devuelve la publicación original, no el texto consolidado: para el consolidado
  con vigencia usar Normativa PBA (conector 4)

**Fallback:** boletinoficial.gba.gob.ar acceso directo.

---

### 3. InfoLeg — `infoleg__`

**Fuente:** infoleg.gob.ar (InfoLEG - Ministerio de Justicia de la Nación).
**Cubre:** texto actualizado de leyes nacionales, decretos y resoluciones, con
histórico de modificaciones. Es la fuente para verificar el texto y la vigencia
de una norma nacional.
**Tools principales:** `infoleg__buscar_normativa`,
`infoleg__buscar_norma_por_tipo_numero_anio`, `infoleg__obtener_texto_norma`,
`infoleg__obtener_metadatos_norma`, `infoleg__comparar_texto_original_actualizado`.

Casos de uso:
- Confirmar el texto vigente de un artículo del CCCN, LCT, LDC u otra ley nacional
- Verificar si una norma fue modificada o derogada, y por cuál
- Comparar el texto original con el actualizado de una norma

Límites:
- Solo normas nacionales (no provinciales)
- No incluye jurisprudencia
- Nota operativa: InfoLEG suele requerir IP argentina; las consultas corren bien
  desde la máquina del abogado, no desde entornos cloud

**Fallback:** infoleg.gob.ar acceso directo.

---

### 4. Normativa PBA — `normativapba__`

**Fuente:** normas.gba.gob.ar (Sistema de Información Normativa de PBA).
**Cubre:** leyes, decretos, resoluciones y disposiciones PBA desde 1813. Verifica
vigencia, extrae articulado y construye árboles de dependencia normativa.
**Tools principales:** `normativapba__buscar_normativa`,
`normativapba__obtener_texto_norma`, `normativapba__obtener_articulo`,
`normativapba__verificar_vigencia`, `normativapba__relacionar_normativa`,
`normativapba__mapa_normativo_tema`.

Casos de uso:
- Verificar texto y vigencia de normas provinciales PBA
- Obtener el articulado exacto de una ley o decreto PBA para citar
- Construir el mapa normativo de un tema (contratación pública PBA, etc.)

Límites:
- Solo normas provinciales PBA
- **`verificar_vigencia` reproduce el estado cargado en el portal, con sus
  errores.** Caso conocido: la Ley 11.922 (CPP Bonaerense, 1997) figura como
  derogada por una norma de 1978, cuando la relación es inversa. Es un primer
  filtro, no fuente definitiva. Ante derogaciones anómalas, verificar contra el
  Boletín Oficial PBA (conector 2).

**Fallback:** normas.gba.gob.ar acceso directo.

---

### 5. JUBA — `juba__`

**Fuente:** juba.scba.gov.ar (SCBA - Suprema Corte de Buenos Aires).
**Cubre:** jurisprudencia de la SCBA y cámaras de apelación PBA. Búsqueda por
texto libre, fuero, carátula, magistrado, voces jurídicas y período; texto
íntegro de la sentencia.
**Tools principales:** `juba__buscar_jurisprudencia`,
`juba__buscar_jurisprudencia_avanzada`, `juba__buscar_por_caratula`,
`juba__buscar_por_voces_juridicas`, `juba__obtener_sentencia`.

Casos de uso:
- Buscar jurisprudencia SCBA por materia, fuero o período
- Verificar criterio de cámaras PBA antes de citar
- Rastrear evolución jurisprudencial provincial sobre un instituto

Cobertura JUBA (Acuerdo 4011 / Resolución RP 1651/24):
- Desde marzo 2025: cámaras de apelación provinciales y Tribunal de Casación Penal
- Desde junio 2025: juzgados de primera instancia civiles, laborales y CA

Límites:
- Solo jurisprudencia PBA; no cubre fueros nacionales ni CSJN
- Los resultados deben verificarse antes de citar

**Fallback:** juba.scba.gov.ar acceso directo.

---

### 6. PTN — `ptn__`

**Fuente:** busquedadictamenes.ptn.gob.ar (Procuración del Tesoro de la Nación).
**Cubre:** dictámenes de la PTN, fuente principal de doctrina en derecho
administrativo federal: responsabilidad del Estado, empleo público, contratos
administrativos.
**Tools principales:** `ptn__buscar_dictamenes`, `ptn__buscar_por_voz`,
`ptn__buscar_por_ley`, `ptn__obtener_dictamen_texto`, `ptn__localizar_por_cita`.

Casos de uso:
- Buscar doctrina de la PTN sobre responsabilidad del Estado antes de demandar
- Verificar criterio PTN sobre empleo público y contratos administrativos
- Localizar un dictamen por su cita clásica (Tomo:Página)

Límites:
- Solo dictámenes PTN; no cubre jurisprudencia judicial
- No reemplaza a SAIJ (conector 10) para jurisprudencia y doctrina académica

**Fallback:** busquedadictamenes.ptn.gob.ar acceso directo.

---

### 7. TFN — `tfn__`

**Fuente:** tfn.gob.ar (Tribunal Fiscal de la Nación).
**Cubre:** jurisprudencia y resoluciones del TFN en materia impositiva y aduanera.
Filtros por sala, vocalía, competencia, fechas; texto íntegro y PDF; síntesis.
**Tools principales:** `tfn__buscar_resoluciones_tfn`,
`tfn__buscar_por_hechos`, `tfn__buscar_por_sumarios`,
`tfn__obtener_resolucion_tfn`, `tfn__descargar_resolucion_pdf`.

Casos de uso:
- Buscar jurisprudencia TFN por materia (Ganancias, IVA, Bienes Personales, aduanera)
- Verificar criterio de sala o vocalía sobre un instituto tributario antes de recurrir
- Rastrear antecedentes por hechos del caso en lenguaje natural

Límites:
- Solo jurisprudencia TFN; no cubre CNACAF ni CSJN en materia tributaria
- La síntesis es generada por el sistema del TFN; verificar antes de citar

**Fallback:** tfn.gob.ar acceso directo.

---

### 8. SCBA — `scba__`

**Fuente:** sentencias.scba.gov.ar (portal de sentencias PBA, distinto de JUBA).
**Cubre:** sentencias y resoluciones de juzgados de primera instancia PBA, con
texto completo. Búsqueda por organismo, tipo de registro y términos.
**Tools principales:** `scba__buscar_documentos`, `scba__listar_organismos`,
`scba__listar_tipos_registro`, `scba__guardar_documentos_en_disco`.

Casos de uso:
- Buscar resoluciones o sentencias de un juzgado de primera instancia PBA
- Armar un corpus de documentos de un organismo para análisis en sesión
- Complementar a JUBA (conector 5) cuando se necesita texto completo de primera instancia

Límites:
- Solo primera instancia: no cubre SCBA ni cámaras vía JUBA (para eso, conector 5)
- Hay solapamiento parcial con JUBA en primera instancia desde junio 2025: usar
  este cuando se necesite búsqueda por palabra clave dentro del cuerpo del fallo
- Nota TLS: el certificado del portal tiene cadena incompleta; el conector
  desactiva la verificación de forma aislada solo para esta fuente (lectura
  pública, sin credenciales)

**Fallback:** sentencias.scba.gov.ar acceso directo.

---

### 9. PJN Consulta — `pjn__`

**Fuente:** pjn.gov.ar (consulta pública de expedientes del Poder Judicial de la Nación).
**Cubre:** estado procesal de expedientes federales y actuaciones. Flujo HITL: las
consultas corren dentro de un navegador real y el captcha lo resuelve el usuario.
**Tools principales:** `pjn__iniciar_hitl_browser`, `pjn__consultar_expediente`,
`pjn__buscar_expediente_por_parte`, `pjn__continuar_tras_captcha`,
`pjn__obtener_actuaciones`, `pjn__exportar_expediente`.

Casos de uso:
- Consultar el estado y las actuaciones de un expediente federal por número
- Buscar expedientes por parte (límite del portal público: solo por DEMANDADO)

Límites:
- Es consulta de estado procesal, no de jurisprudencia (para fallos, conector 11)
- Requiere sesión HITL con captcha resuelto a mano; no corre en cloud
- Búsqueda por parte limitada a demandado por restricción del portal

**Fallback:** pjn.gov.ar acceso directo.

---

### 10. SAIJ — `saij__`

**Fuente:** saij.gob.ar (Sistema Argentino de Información Jurídica - Min. de Justicia).
**Cubre:** más de 330.000 documentos entre jurisprudencia federal, nacional y
provincial, legislación, doctrina y dictámenes. Navegación de grafo legal y
resolución de citas textuales.
**Tools principales:** `saij__search_jurisprudencia`, `saij__search_legislacion`,
`saij__search_doctrina`, `saij__search_dictamenes`, `saij__get_document`,
`saij__resolve_citation`, `saij__get_related_documents`.

Casos de uso:
- Buscar jurisprudencia, doctrina y dictámenes en una sola fuente
- Resolver una cita textual ("Ley 24.240") al documento exacto
- Navegar la red de citas entre un fallo y las normas que aplica (y viceversa)
- Acceder a jurisprudencia histórica en PDF escaneado con OCR

Límites:
- Es la única vía del hub para **doctrina**: si la consulta es doctrinaria, este es el conector
- No reemplaza a InfoLeg (conector 3) para el texto oficial consolidado de normas nacionales
- Los resultados deben verificarse antes de citar

**Fallback:** saij.gob.ar acceso directo.

---

### 11. PJN Jurisprudencia — `pjnjuris__`

**Fuente:** sj.pjn.gov.ar (Sistema de Jurisprudencia del Consejo de la Magistratura).
**Cubre:** sumarios de fallos de cámaras nacionales y federales. Búsqueda por
texto libre, carátula, expediente, cámara y magistrado. Flujo HITL con captcha.
**Tools principales:** `pjnjuris__buscar_jurisprudencia_fed`,
`pjnjuris__pjn_buscar_jurisprudencia_por_caratula`,
`pjnjuris__pjn_buscar_jurisprudencia_por_expediente`, `pjnjuris__obtener_sumario`,
`pjnjuris__listar_camaras`.

Casos de uso:
- Buscar jurisprudencia federal y nacional por materia antes de redactar un escrito
- Verificar criterio de una cámara o sala sobre un instituto
- Recuperar el sumario íntegro de un fallo por su ID

Límites:
- Solo jurisprudencia federal/nacional PJN; no cubre PBA (conector 5) ni CSJN directa (conector 14)
- Requiere sesión HITL con captcha; no corre en cloud
- Los fallos de la CSJN viven en otro portal (usar conector 14)

**Fallback:** pjn.gov.ar acceso directo.

---

### 12. Portal PJN — `portalpjn__`

**Fuente:** api.pjn.gov.ar / portalpjn.pjn.gov.ar (portal del abogado logueado).
**Cubre:** feed de novedades del estudio: despachos (D) y cédulas de notificación
(N) de todas las causas del abogado, con descarga del PDF de cada evento. Login
siempre del usuario (HITL por SSO).
**Tools principales:** `portalpjn__iniciar_hitl_browser`,
`portalpjn__obtener_novedades`, `portalpjn__parte_diario`,
`portalpjn__descargar_pdf_evento`.

Casos de uso:
- Armar el parte diario de novedades agrupado por expediente
- Descargar el PDF de un despacho o cédula de notificación

Límites:
- Requiere login del abogado (HITL + SSO); no corre en cloud ni sin sesión
- No presenta escritos por diseño: solo lectura del feed
- Es gestión de causas propias, no investigación de jurisprudencia

**Fallback:** portalpjn.pjn.gov.ar acceso directo (con login del abogado).

---

### 13. JusCABA — `juscaba__`

**Fuente:** eje.juscaba.gob.ar (Expediente Judicial Electrónico de la Justicia CABA).
**Cubre:** consulta de causas por parte, número o CUIJ: encabezado, ficha, fuero,
partes, actuaciones, verificación de sentencia y descarga de PDF. Acceso público,
sin login ni captcha.
**Tools principales:** `juscaba__buscar_causas`, `juscaba__obtener_ficha`,
`juscaba__obtener_encabezado`, `juscaba__listar_actuaciones`,
`juscaba__tiene_sentencia`, `juscaba__descargar_pdf`.

Casos de uso:
- Consultar el estado y las actuaciones de una causa CABA por parte o CUIJ
- Verificar si una causa tiene sentencia y descargar su PDF

Límites:
- Es consulta de expedientes CABA (fuero CAyT, PCyF), no jurisprudencia indexada
- Cubre la Justicia de la Ciudad, no fueros nacionales con sede en CABA ni PBA

**Fallback:** eje.juscaba.gob.ar acceso directo.

---

### 14. CSJN — `csjn__`

**Fuente:** sjconsulta.csjn.gov.ar (CSJN - Secretaría de Jurisprudencia, base de Sumarios).
**Cubre:** sumarios de jurisprudencia de la Corte Suprema, 1863-2026. Búsqueda por
texto libre, carátula, fecha y tomo:página de Fallos. El detalle trae el análisis
documental (competencia, recurso, sentido, remisión, voces, normas, ministros,
votos), los sumarios del fallo y el enlace al PDF. Acceso público sin login.
**Tools principales:** `csjn__buscar_sumarios`, `csjn__obtener_documento`,
`csjn__alcance_fuente`.

Casos de uso:
- Buscar leading cases de la CSJN por materia, con cita de Fallos verificable
- Obtener el análisis documental y el PDF de un fallo para citar en un recurso
- Rastrear la evolución del criterio de la Corte sobre un instituto

Límites:
- Solo base de SUMARIOS de la CSJN; no cubre instancias inferiores
- El análisis documental (campo `normasConsideradas`) a veces viene vacío en
  origen. `obtener_documento` con `incluirCuerpo=true` (defecto) agrega un bloque
  `cuerpoFallo` con normas y votos **extraídos del PDF**, etiquetado como
  extracción automática best-effort y separado del análisis documental. En fallos
  escaneados el OCR puede corromper dígitos (un tomo de Fallos) y las firmas son
  ilegibles: nada de `cuerpoFallo` se cita sin verificar contra el PDF
- La cita autoritativa es la del sumario más el PDF, no la extracción automática

**Fallback:** sj.csjn.gov.ar acceso directo.

---

## Tabla de decisión - qué tool del hub usar

| Necesidad | Conector / tool | Fallback oficial |
|---|---|---|
| Texto y vigencia de una norma nacional | 3 InfoLeg · `infoleg__obtener_texto_norma` | infoleg.gob.ar |
| Texto y vigencia de una norma provincial PBA | 4 Normativa PBA · `normativapba__obtener_texto_norma` + `verificar_vigencia` | normas.gba.gob.ar |
| Publicación oficial de una norma nacional (verbatim/PDF) | 1 BORA · `bora__obtener_detalle_aviso` | boletinoficial.gob.ar |
| Publicación oficial de una norma PBA | 2 BOPBA · `bopba__buscar_boletin` | boletinoficial.gba.gob.ar |
| Jurisprudencia PBA (SCBA y cámaras) | 5 JUBA · `juba__buscar_jurisprudencia` | juba.scba.gov.ar |
| Sentencias de primera instancia PBA (texto completo) | 8 SCBA · `scba__buscar_documentos` | sentencias.scba.gov.ar |
| Jurisprudencia federal/nacional (cámaras) | 11 PJN Juris · `pjnjuris__buscar_jurisprudencia_fed` | pjn.gov.ar |
| Fallos de la CSJN | 14 CSJN · `csjn__buscar_sumarios` → `csjn__obtener_documento` | sj.csjn.gov.ar |
| Jurisprudencia + legislación + dictámenes (general) | 10 SAIJ · `saij__search_jurisprudencia` | saij.gob.ar |
| **Doctrina** | 10 SAIJ · `saij__search_doctrina` | saij.gob.ar |
| Dictámenes administrativos federales (PTN) | 6 PTN · `ptn__buscar_dictamenes` | busquedadictamenes.ptn.gob.ar |
| Jurisprudencia tributaria/aduanera (TFN) | 7 TFN · `tfn__buscar_resoluciones_tfn` | tfn.gob.ar |
| Estado procesal de un expediente federal | 9 PJN Consulta · `pjn__consultar_expediente` (HITL) | pjn.gov.ar |
| Estado de una causa CABA (EJE) | 13 JusCABA · `juscaba__buscar_causas` | eje.juscaba.gob.ar |
| Novedades de las causas propias (despachos, cédulas) | 12 Portal PJN · `portalpjn__parte_diario` (HITL + SSO) | portalpjn.pjn.gov.ar |
| Resolver una cita textual a documento | 10 SAIJ · `saij__resolve_citation` | saij.gob.ar |

---

## Ruteo por pieza de demanda

Regla antes de la tabla: la instrucción dice DÓNDE buscar, no QUÉ dice el fallo o
la norma. El contenido sustantivo lo trae el conector verificado; no se rellena
con conocimiento del modelo. "Para jurisprudencia de Corte, `csjn__`; para
doctrina, `saij__`; para vigencia de la norma, `infoleg__`" es ruteo. "El leading
case en X es Y" sería contenido, y ahí se vuelve a habilitar el relleno con
training. Si el conector no trae el dato, va un marcador, no una afirmación.

| Pieza del escrito | Fuente / tool | Marcador si falta |
|---|---|---|
| Hechos | Material aportado, no conectores. Estado de expediente: `pjn__`, `juscaba__` | `[VACÍO PROBATORIO: ...]` |
| Prueba | Material aportado | `[VACÍO PROBATORIO: ...]` |
| Derecho - norma nacional | `infoleg__obtener_texto_norma` (+ vigencia) | `[VERIFICAR VIGENCIA]` / `[REVISIÓN NORMATIVA REQUERIDA]` |
| Derecho - norma PBA | `normativapba__obtener_texto_norma` + `verificar_vigencia` | íd. |
| Jurisprudencia CSJN | `csjn__buscar_sumarios` → `csjn__obtener_documento` | `[INSERTAR FALLO VERIFICADO: ...]` |
| Jurisprudencia federal/nacional (cámaras) | `pjnjuris__buscar_jurisprudencia_fed` | íd. |
| Jurisprudencia PBA (SCBA/cámaras) | `juba__buscar_jurisprudencia`; 1ª instancia PBA: `scba__buscar_documentos` | íd. |
| Jurisprudencia tributaria | `tfn__buscar_resoluciones_tfn` | íd. |
| Jurisprudencia / expedientes CABA | jurisprudencia: `saij__` (parcial); expediente: `juscaba__buscar_causas` | íd. |
| Doctrina | `saij__search_doctrina`; doctrina administrativa federal: `ptn__buscar_dictamenes` | nota de fuente faltante |
| Vigencia del precedente (criterio no superado) | Sin conector: verificación manual | `[VERIFICAR PRECEDENTE: ...]` |
| Firmeza del propio fallo (¿recurrido?) | Estado procesal vía expediente: `juscaba__`, `pjn__` (HITL), `mev__`, si la causa es ubicable | `[VERIFICAR PRECEDENTE: ...]` si no se ubica |
| Petitorio | Perfil de práctica, no conectores | - |

El detalle de cada tool y sus límites está arriba, en "Conectores del hub".

---

## Verificación de vigencia - dos cosas distintas

No confundir vigencia de la norma con vigencia del precedente. La primera el hub
la resuelve; la segunda, no.

**Vigencia de la NORMA.** `infoleg__` (nacional) y `normativapba__verificar_vigencia`
(PBA) informan si la norma está vigente, fue modificada o derogada. BORA y BOPBA
confirman la publicación original y las modificatorias individuales, pero no
consolidan el texto. Recordar la limitación de `normativapba__verificar_vigencia`
(replica el estado del portal, con sus errores): primer filtro, no definitivo.

**Vigencia del PRECEDENTE.** Los conectores de JURISPRUDENCIA (JUBA, SAIJ, CSJN,
PJN Jurisprudencia) no te dicen si un fallo sigue siendo buen derecho: traen el
precedente, pero no avisan si fue dejado sin efecto o superado. Los endpoints de
citados/citantes no están implementados. Esa verificación -de que el criterio no
fue superado por uno posterior- es manual y obligatoria antes de fundar una
pretensión en un fallo. Marcar en sesión cuando no se pudo confirmar:

```
[VERIFICAR PRECEDENTE: "carátula" o Fallos T:P - confirmar que no fue dejado sin efecto ni superado antes de citar]
```

**Firmeza del propio fallo, vía expediente (sí se puede).** Distinto del criterio:
si lo que se quiere saber es si ESE fallo quedó firme o fue recurrido, los
conectores de EXPEDIENTES lo resuelven cuando la causa está en su portal, leyendo
el estado procesal y los expedientes vinculados (apelación, recurso extraordinario
o de inconstitucionalidad, queja):

- CABA: `juscaba__buscar_causas` por carátula/número/CUIJ. Los legajos vinculados
  muestran los recursos. Ej. real (jul-2026): "G., M. J. sobre 71 ter" tenía un
  recurso de inconstitucionalidad denegado y una queja ante el TSJ CABA -> NO firme.
- Nación/federal: `pjn__buscar_expediente_por_parte` (HITL, solo por demandado con
  nombre real) -> `pjn__obtener_actuaciones`. Si tras la sentencia de cámara los
  autos volvieron al juzgado de origen y no hay recurso extraordinario ni queja
  registrados, el fallo aparece firme (para certeza plena, descartar un REF/queja
  tramitado en expediente separado ante la CSJN). Ej. real: "Centro de Empleados de
  Comercio c/ Facebook" (FRE 4364/2021), devuelto a origen e inactivo -> firme.
- PBA: `mev__` (con login) para expedientes de la Provincia.

Límites: solo si la causa es ubicable. Partes anonimizadas no se buscan por nombre;
el PJN público solo admite demandado. Cuando no se puede ubicar, rige el
[VERIFICAR PRECEDENTE] manual.

---

## Combinaciones recomendadas

- **InfoLeg + JUBA + SAIJ:** flujo completo para escritos en fuero PBA. Norma
  nacional verificada + jurisprudencia PBA + doctrina.
- **InfoLeg + CSJN + PJN Jurisprudencia:** recursos y escritos ante fueros
  nacionales/federales. Norma verificada + Corte + cámaras.
- **InfoLeg + CSJN + SAIJ + previsional-CLAUDE.md:** demanda de reajuste de haberes
  ante el Fuero Federal de la Seguridad Social. InfoLeg verifica la fórmula de
  movilidad de cada período (secuencia 24.241 / 26.417 / 27.426 / 27.541 / 27.609 /
  DNU 274/2024) y la Ley 24.463; CSJN aporta la línea de movilidad y de haber inicial;
  SAIJ y PJN Jurisprudencia, la jurisprudencia del fuero (CFSS). La vigencia del
  precedente de movilidad se verifica a mano (B5).
- **InfoLeg + BORA:** verificación normativa completa. InfoLeg da el texto
  consolidado; BORA confirma la publicación original y la cadena de modificaciones.
- **BORA + societario-CLAUDE.md:** due diligence societario. BORA busca el acto
  constitutivo y las modificaciones; el perfil aporta la lógica de análisis LGS.
- **InfoLeg + TFN:** escritos ante el TFN. InfoLeg verifica la norma; TFN aporta
  los antecedentes del tribunal sobre el instituto.
- **CSJN + TFN:** apelación ante la CNACAF o casación tributaria. CSJN da la
  doctrina de la Corte; TFN el criterio del tribunal sobre el mismo instituto.
- **Normativa PBA + BOPBA:** cobertura normativa PBA completa. NormativaPBA da el
  consolidado con vigencia; BOPBA la publicación original y la cadena por fecha.
- **SAIJ + PTN:** escritos contencioso administrativos federales. PTN aporta la
  doctrina de la Procuración; SAIJ la jurisprudencia y doctrina académica.
- **JUBA + SCBA:** cobertura PBA complementaria. JUBA cubre SCBA y cámaras; SCBA
  cubre primera instancia con texto completo y búsqueda por palabra clave en el cuerpo.

---

## Si dos conectores se contradicen

Los conectores que acceden a fuentes primarias oficiales prevalecen sobre el
conocimiento base del sistema en caso de contradicción. Entre conectores: SCBA
(conector 8) y TFN (conector 7) son scrapers de mayor fragilidad técnica; si sus
resultados contradicen a JUBA, SAIJ o CSJN sobre el mismo documento, verificar
directamente en el portal oficial antes de proceder. Reportar la discrepancia al
abogado con el marcador:

```
[DISCREPANCIA ENTRE FUENTES: el conector [X] indica [A] / la fuente primaria
 indica [B]. Verificar directamente en fuente primaria antes de proceder.]
```

---

## Fuentes primarias oficiales (sin conector)

Acceso directo por el abogado para verificación manual. Son la fuente de verdad
ante cualquier discrepancia con un conector.

| Fuente | URL | Uso principal |
|---|---|---|
| InfoLEG | infoleg.gob.ar | Texto oficial de normas nacionales |
| normas.gba.gob.ar | normas.gba.gob.ar | Texto oficial de normas provinciales PBA |
| SAIJ | saij.gob.ar | Jurisprudencia, doctrina, legislación |
| PJN | pjn.gov.ar | Acordadas y jurisprudencia federal |
| CNACAF | cnacaf.gov.ar | Jurisprudencia CA federal y alzada tributaria |
| SCBA | scba.gov.ar | Jurisprudencia PBA - fuente primaria bonaerense |
| JUBA | juba.scba.gov.ar | Consulta de jurisprudencia PBA |
| Poder Judicial CABA | jusbaires.gob.ar | Jurisprudencia y expedientes fuero local CABA |
| PTN | busquedadictamenes.ptn.gob.ar | Dictámenes - responsabilidad del Estado y empleo público |
| AAIP | argentina.gob.ar/aaip | Disposiciones de datos personales |
| IGJ | igj.gob.ar | Resoluciones societarias CABA |
| DPPJ | gba.gob.ar/dppj | Resoluciones societarias PBA |
| CNV | cnv.gov.ar | Normas mercado de capitales |
| BCRA | bcra.gov.ar | Normativa cambiaria y financiera |
| COMARB | comarb.gov.ar | Convenio Multilateral - Ingresos Brutos |
| TFN | tfn.gob.ar | Jurisprudencia tributaria |
| Boletín Oficial nacional | boletinoficial.gob.ar | Publicaciones oficiales nacionales |
| Boletín Oficial PBA | boletinoficial.gba.gob.ar | Publicaciones oficiales PBA |

---

## Fuentes sin conector todavía (objetivos de integración)

Fuentes relevantes para la práctica argentina sin conector en el hub al momento de
esta actualización. Se documentan como objetivos de desarrollo.

| Nombre tentativo | Fuente | Viabilidad estimada | Estado |
|---|---|---|---|
| TSJ CABA / Cámara CAyT | Jurisprudencia del fuero CABA (no expedientes) | MEDIA | No integrado; usar SAIJ para cobertura parcial CABA |
| dppj | DPPJ PBA - Personas Jurídicas | MEDIA-ALTA (Tramix Web, scraping por legajo) | No integrado |
| bcra-deudores | BCRA - Central de Deudores | BAJA (Cloudflare + reCAPTCHA, bloquea cloud) | No integrado |
| Citados/citantes CSJN | Vigencia de precedentes | MEDIA (endpoints vistos, no mapeados) | No integrado - hueco de verificación de vigencia del precedente |

---

## El hub reúne trabajo de la comunidad

`mcp-legal-ar` no crea fuentes nuevas: unifica conectores desarrollados por la
comunidad argentina de legal tech más desarrollos propios. El crédito de cada
conector de terceros corresponde a sus autores originales.

- **BORA, BOPBA, InfoLeg, Normativa PBA, JUBA, PTN, TFN** - Voftec (MIT). Los
  repositorios originales ya no están públicos; el hub preserva esas integraciones.
  Por eso este archivo ya no lista los conectores sueltos por URL/uvx de la
  comunidad: quedaron obsoletos al despublicarse los repos. El hub es el camino vivo.
- **SCBA** - FacundoEmanuel (MIT).
- **SAIJ** - Joaquin Escalante (MIT).
- **Portal PJN, JusCABA, CSJN** y las reescrituras de PJN Consulta y PJN
  Jurisprudencia - desarrollo propio de [@abogadoaboitiz](https://x.com/abogadoaboitiz),
  sin derivar de código de terceros.

Las licencias y atribuciones completas están en `THIRD_PARTY_NOTICES.md` del repo
del hub.

---

*Última actualización: junio 2026*
*Autor: Dr. Cristian Aboitiz · [@abogadoaboitiz](https://x.com/abogadoaboitiz)*
