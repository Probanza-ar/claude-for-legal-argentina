# Perfil de práctica · Violencia digital

> Archivo de configuración para el sistema claude-for-legal.
> Perfil transversal: complementa el perfil general (argentina/CLAUDE.md) y se carga junto con el
> perfil de área específica según la vía elegida - penal-CLAUDE.md (delitos informáticos, violencia
> de género), familia-CLAUDE.md (violencia familiar por TIC, medidas de protección), civil-CLAUDE.md
> (daños) y proteccion-datos-CLAUDE.md (cuando hay un componente de datos personales o informes
> crediticios). Cubre tanto la vía penal/contravencional como la vía de protección integral de la
> Ley 26.485.
> **Configuración inicial obligatoria:** completar las variables de la sección siguiente antes de usar.

---

## Configuración inicial - completar antes de usar

**FUERO_HABITUAL:**
Indicar el fuero y la jurisdicción donde tramitan habitualmente estos casos. Opciones: "CABA - penal
nacional/CPPCABA + contravencional", "PBA - [departamento judicial]", "federal", u otra combinación.

Ejemplo: `FUERO_HABITUAL: CABA - Fiscalía correspondiente en lo Penal, Contravencional y de Faltas + UFEDyCI`

**ROL_PREDOMINANTE:**
Indicar si actuás predominantemente patrocinando a la víctima (denunciante/querellante) o en defensa
del imputado.

Ejemplo: `ROL_PREDOMINANTE: Patrocinio de la víctima`

---

## Identidad y alcance

Este perfil cubre los casos de violencia ejercida contra mujeres y otras personas por medio de
tecnologías de la información y la comunicación (TIC): difusión no consentida de imágenes o
grabaciones íntimas ("pornovenganza"), sextorsión, hostigamiento y acoso digital, usurpación de
identidad digital, grooming, y las modalidades de violencia vincular (ex pareja, pareja conviviente)
ejercidas por medios digitales. Articula la vía penal, la vía contravencional (CABA), la vía de
protección integral de la Ley 26.485 y la vía civil de daños.

No es un perfil autónomo de delitos informáticos en general (fraude informático, acceso ilegítimo a
sistemas con fines patrimoniales, ciberataques a infraestructura) ni de protección de datos
personales/informes crediticios: para esos escenarios, ver penal-CLAUDE.md sección "Delitos
informáticos" y proteccion-datos-CLAUDE.md respectivamente. Este perfil se activa cuando la conducta
tiene un componente de género, de intimidad sexual, de hostigamiento personal o de violencia vincular
ejercida por medios digitales.

**FUERO_HABITUAL:** ver sección de configuración inicial
**ROL_PREDOMINANTE:** ver sección de configuración inicial

---

## Alerta normativa - normas de vigencia variable

*Última verificación de esta sección: julio 2026.*

### Ley Olimpia (Ley 27.736) - vigente

La Ley 27.736 ("Ley Olimpia"), sancionada el 10/10/2023 y publicada el 23/10/2023, incorporó la
violencia digital o telemática como modalidad autónoma dentro de la Ley 26.485 de Protección Integral
de las Mujeres. No crea tipos penales nuevos: modifica la Ley 26.485 (definiciones, derechos y
medidas de protección). Está vigente y debe aplicarse como marco de encuadre y como fuente de medidas
de protección específicas para el espacio digital (ver desarrollo más abajo).

```
[VERIFICAR VIGENCIA: Ley 27.736 (Ley Olimpia) - confirmar que no hubo modificación posterior a julio 2026]
```

### Vacío legal - no hay tipo penal federal específico para la difusión no consentida de imágenes íntimas entre personas adultas

**Punto crítico a advertir siempre antes de calificar el hecho:** a la fecha de esta verificación, el
Código Penal argentino no contiene una figura autónoma que castigue específicamente la difusión no
consentida de imágenes o grabaciones íntimas de personas adultas ("pornovenganza"). Existen múltiples
proyectos de ley en trámite parlamentario para incorporar esa figura (por ejemplo, expediente
0304-D-2025 con los arts. 128 bis a 128 septies propuestos; la denominada "Ley Belén", expediente
2757-D-22; y la iniciativa impulsada por el senador Zamora en abril de 2026), pero ninguno se
encuentra sancionado. No calificar el hecho como si existiera un tipo penal específico de
"pornovenganza" o "difusión no consentida de imágenes íntimas" en el Código Penal nacional.

En la práctica, estos hechos se encuadran hoy mediante figuras existentes según las circunstancias
del caso: chantaje/extorsión (arts. 168 y 169 CP, cuando hay exigencia patrimonial o de otra
prestación bajo amenaza de difusión), violación de secretos y de la privacidad (arts. 153, 153 bis,
155 y 157 CP), amenazas (art. 149 bis CP), y - cuando la víctima es menor de edad - los delitos contra
la integridad sexual y pornografía infantil (arts. 128 y 131 CP). Ver desarrollo en "Marco normativo"
más abajo.

**Frente aparte - reforma integral del Código Penal (Poder Ejecutivo):** distinto de los proyectos
legislativos individuales, el Poder Ejecutivo impulsa desde fines de 2025 un proyecto de reforma
integral del Código Penal que, entre más de 900 artículos, incluye una sección de delitos informáticos
con tipificación específica de la "pornovenganza" y de la usurpación de identidad digital. A julio de
2026 el texto sigue en negociación interna del Ejecutivo (discusión sobre su alcance entre Casa
Rosada y el equipo técnico) y no fue remitido en versión definitiva al Congreso ni sancionado. No
calificar el hecho conforme a esta reforma bajo ningún concepto mientras no tenga sanción.

```
[REVISIÓN NORMATIVA REQUERIDA: estado parlamentario de los proyectos de tipificación de la difusión no consentida de imágenes íntimas (expte. 0304-D-2025, "Ley Belén" 2757-D-22, iniciativa Zamora abril 2026 - confirmado sin sanción por búsqueda web julio 2026) y de la reforma integral del Código Penal impulsada por el Poder Ejecutivo (sin envío definitivo al Congreso a julio 2026) - verificar en cada consulta si alguno fue sancionado antes de calificar el hecho como delito autónomo]
```

### Código Contravencional CABA - arts. 71 bis, 71 ter y 71 quater (Ley 6017, texto consolidado)

A diferencia del ámbito nacional, la Ciudad Autónoma de Buenos Aires sí tiene tipificadas como
contravenciones la difusión no autorizada de imágenes o grabaciones íntimas y el hostigamiento
digital. Esta vía opera **solo cuando el hecho no constituye delito**: si la conducta encuadra en
alguna de las figuras penales del párrafo anterior (chantaje, violación de secretos, amenazas,
delitos contra la integridad sexual), corresponde la vía penal y no la contravencional. Ver desarrollo
completo en "Marco normativo - Código Contravencional CABA".

```
[VERIFICAR VIGENCIA: arts. 71 bis, 71 ter y 71 quater del Código Contravencional CABA (Ley 6017, texto consolidado) - confirmar texto vigente al momento del hecho, incluidos los montos de la unidad fija aplicable]
```

### Convenio de Budapest - Segundo Protocolo Adicional sin incorporación interna

Ver penal-CLAUDE.md, sección "Delitos informáticos": el Segundo Protocolo Adicional al Convenio de
Budapest (mayo 2021) no fue incorporado al derecho interno por ley del Congreso a la fecha de esta
verificación. No invocar sus disposiciones como derecho vigente en Argentina sin comprobar
ratificación posterior.

---

## Marco normativo

### Ley 26.485 modificada por Ley 27.736 (Ley Olimpia)

**Definición de violencia digital o telemática (art. 6 inc. i, Ley 26.485, texto según Ley 27.736):**
toda conducta, acción u omisión contra las mujeres basada en su género, cometida, instigada o
agravada -en parte o en su totalidad- con la asistencia, utilización o apropiación de las TIC, con el
objeto de causar daños físicos, psicológicos, económicos, sexuales o morales, tanto en el ámbito
privado como en el público, a ellas o a su grupo familiar. La norma enumera especialmente: conductas
que atenten contra la integridad, dignidad, identidad, reputación, libertad y el acceso, permanencia y
desenvolvimiento en el espacio digital; la obtención, reproducción y difusión sin consentimiento de
material digital real o editado, íntimo o de desnudez, atribuido a la mujer; la reproducción de
discursos de odio misóginos y patrones estereotipados sexistas; situaciones de acoso, amenaza,
extorsión, control o espionaje de la actividad virtual; accesos no autorizados a dispositivos o
cuentas en línea; robo y difusión no consentida de datos personales (en tanto no sean conductas
permitidas por la Ley 25.326); y cualquier otro ciberataque que afecte los derechos protegidos por la
ley.

**Extensión del ámbito de aplicación y de los derechos protegidos (arts. 2, 3 y 4, texto según Ley
27.736):** se incorporan como bienes protegidos "los derechos y bienes digitales de las mujeres, así
como su desenvolvimiento y permanencia en el espacio digital" (art. 2 inc. h) y el derecho a que se
respete su dignidad, reputación e identidad "incluso en los espacios digitales" (art. 3 inc. d). La
definición general de violencia de género (art. 4) pasa a comprender expresamente el "espacio
analógico digital".

**Derechos procesales específicos (art. 16, texto según Ley 27.736):**
- Inc. a): gratuidad de toda diligencia e instancia, incluido el acceso a recursos públicos para
  pericias informáticas y patrocinio jurídico preferentemente especializado.
- Inc. l): al resguardo diligente y expeditivo de la evidencia en soportes digitales por cuerpos de
  investigación especializados u organismos públicos correspondientes.

**Medidas de protección con componente digital (art. 26, texto según Ley 27.736) - herramientas
directamente utilizables al redactar el pedido de medidas:**
- Apartado a.2 (modificado): orden al presunto agresor de cesar los actos de perturbación o
  intimidación, tanto en el espacio analógico como en el digital.
- Apartado a.8 (nuevo): prohibición de contacto del presunto agresor hacia la mujer por cualquier
  tecnología de la información y la comunicación, aplicación de mensajería instantánea o canal de
  comunicación digital.
- Apartado a.9 (nuevo): orden por auto fundado a las empresas de plataformas digitales, redes sociales
  o páginas electrónicas para la supresión de contenidos que constituyan violencia digital o
  telemática, identificando la URL específica del contenido a remover. La autoridad interviniente
  puede además solicitar el aseguramiento de los datos informáticos de tráfico, abonados y contenido
  suprimido por un plazo de 90 días, renovable una única vez por igual plazo a pedido de parte, y
  puede requerir -mediante auto fundado y para la investigación de las acciones de fondo- la
  revelación de esos datos conforme los mecanismos de cooperación previstos en la normativa vigente.

**Regla operativa:** al redactar cualquier pedido de medidas de protección en un caso con componente
digital, incluir expresamente los apartados a.8 y a.9 del art. 26 como capítulos autónomos del
petitorio, con identificación precisa de las URL, cuentas o plataformas involucradas cuando estén
disponibles. No asumir que la orden de cese genérica (a.2) cubre por sí sola la remoción de contenido:
para eso es necesario invocar puntualmente el a.9.

```
[VACÍO PROBATORIO: URL, capturas de pantalla o identificación precisa del contenido y de la cuenta o perfil del agresor - sin esta identificación, el pedido del apartado a.9 del art. 26 Ley 26.485 puede resultar inejecutable]
```

### Código Penal - figuras aplicables según el escenario

Este perfil no reemplaza el desarrollo de penal-CLAUDE.md, sección "Delitos informáticos" y sección
"Violencia de género y delitos contra la integridad sexual"; los complementa con el encuadre específico
para violencia digital.

**Violación de secretos y de la privacidad (arts. 153, 153 bis, 155 y 157 CP, texto según Ley 26.388):**
- Art. 153 CP: apertura o acceso indebido a comunicación electrónica, correspondencia o
  comunicación no destinada al autor; supresión o desvío de su destino.
- Art. 153 bis CP: acceso a un sistema o dato informático de acceso restringido sin la debida
  autorización.
- Art. 155 CP: publicación indebida de una correspondencia, comunicación electrónica, carta misiva o
  despacho que no estuviera destinado a la publicidad, si el hecho causare o pudiere causar perjuicios
  a terceros. Es una de las figuras a evaluar cuando se difunden capturas de conversaciones o
  contenido privado obtenido de una comunicación electrónica.
- Art. 157 CP: funcionario público que revelare hechos, actuaciones o documentos que por ley deban
  quedar secretos.

**Chantaje y extorsión (arts. 168 y 169 CP):** en el escenario de sextorsión -amenaza de difundir
material íntimo si la víctima no entrega dinero, más material o realiza alguna prestación-, la figura
aplicable con mayor precisión suele ser el art. 169 CP (chantaje: extorsión especial cuando el medio
comisivo es la amenaza de imputaciones contra el honor o de violación de secretos, pena de 3 a 8 años),
en lugar del art. 168 CP (extorsión genérica, pena de 5 a 10 años, medios comisivos de intimidación
genérica o simulación de autoridad pública). No calificar automáticamente por el art. 168: verificar
si el medio comisivo específico encuadra en el art. 169.

**Amenazas (art. 149 bis CP):** aplicable cuando no hay exigencia patrimonial o de otra prestación, y
la conducta se agota en atemorizar mediante el anuncio de un mal (por ejemplo, "voy a difundir tus
fotos" sin pedir nada a cambio).

**Grooming (art. 131 CP, Ley 26.904) y pornografía infantil (art. 128 CP):** aplicables cuando la
víctima es menor de edad. Ver desarrollo completo en penal-CLAUDE.md, sección "Violencia de género y
delitos contra la integridad sexual".

**Ley "Mica Ortega" (Ley 27.590) - marco de prevención, no tipo penal:** crea el Programa Nacional de
Prevención y Concientización del Grooming o Ciberacoso contra Niñas, Niños y Adolescentes (sancionada
el 11/11/2020, reglamentada por Decreto 407/2022), a cargo de la Secretaría Nacional de Niñez,
Adolescencia y Familia. No modifica el art. 131 CP ni crea un tipo penal: es una herramienta de
política pública (capacitación, protocolos de actuación para organismos administrativos de
protección local, líneas 137 y 144) útil para fundamentar pedidos de medidas de protección,
capacitación institucional o articulación con organismos de niñez, pero no para el encuadre penal del
hecho. Distinta de la Ley 27.458, que declara el 13 de noviembre de cada año Día Nacional de la Lucha
contra el Grooming (fecha conmemorativa, sin contenido programático ni penal propio). No confundir
ambas leyes ni sus números.

```
[VERIFICAR VIGENCIA: Ley 27.590 ("Ley Mica Ortega") y su reglamentación por Decreto 407/2022 - confirmar autoridad de aplicación vigente (SENAF) y protocolos actualizados]
```

**Daño informático (art. 183, segundo párrafo, CP):** aplicable cuando la conducta incluye alteración,
destrucción o inutilización de datos, documentos, programas o sistemas informáticos (por ejemplo,
borrado de cuentas o de dispositivos como parte del hostigamiento).

```
[VERIFICAR VIGENCIA: arts. 128, 131, 149 bis, 153, 153 bis, 155, 157, 168, 169 y 183 CP - primera mención en cualquier escrito]
```

### Código Contravencional CABA (Ley 6017, texto consolidado)

**Art. 71 bis - Difusión no autorizada de imágenes o grabaciones íntimas:** sanciona a quien difunda,
publique, distribuya, facilite, ceda o entregue a terceros imágenes, grabaciones o filmaciones de
carácter íntimo sin el consentimiento de la persona, por cualquier medio de comunicación electrónica,
transmisión de datos, páginas web u otro medio, **siempre que el hecho no constituya delito**. La
sanción prevista es de multa (entre 400 y 1.950 unidades fijas), días de trabajo de utilidad pública
(5 a 15) o días de arresto (3 a 10). El consentimiento de la víctima para la difusión, siendo menor de
18 años, no es válido a los efectos de excluir la contravención.

**Art. 71 ter - Hostigamiento digital:** sanciona a quien intimide u hostigue a otro mediante el uso
de cualquier medio digital, siempre que el hecho no constituya delito, con multa (160 a 800 unidades
fijas), días de trabajo de utilidad pública (3 a 10) o días de arresto (1 a 5). El ejercicio del
derecho a la libertad de expresión no configura hostigamiento digital.

**Fallo (sentencia NO firme) - condena en 1ra instancia por art. 71 ter:** Juzgado de 1ra Instancia en lo Penal, Contravencional
y de Faltas N° 21 de CABA, "G., M. J. sobre 71 ter - Hostigamiento digital", expte. DEB
39719/2023-2, CUIJ DEB J-01-00039719-5/2023-2. Verificado contra el texto completo de la sentencia
(búsqueda web julio 2026, Observatorio de Género del Colegio de Abogados de CABA). El imputado, un
creador de contenido, difundió sin consentimiento la imagen de una mujer trans junto con comentarios
discriminatorios sobre su identidad de género; el tribunal condenó a una multa de 300 unidades fijas
y prohibió mencionar a la víctima con su nombre registral anterior. Tres aportes concretos para
este perfil: (a) validó como prueba idónea una captura de pantalla resguardada con hash y sello de
fecha/hora, generada mediante un programa forense - refuerza el estándar de resguardo de evidencia
de la sección "Prueba y cadena de custodia digital"; (b) encuadró el hecho en la intersección entre
violencia de género digital (extendida a mujeres trans conforme doctrina de la CIDH) y discriminación
(Ley 5261 CABA), por lo que es aplicable también a víctimas de identidad de género no binaria o
trans; (c) además de la multa, ordenó librar oficio a Google Inc. para la desindexación de la
publicación - un ejemplo concreto de implementación judicial de una orden a un intermediario dentro
de un proceso contravencional, sin necesidad de una acción autónoma contra el buscador.

```
[VERIFICAR PRECEDENTE: "G., M. J. sobre 71 ter" (Juzg. PCyF N°21 CABA, expte 39719/2023) - SENTENCIA NO FIRME (verificado en JusCABA vía mcp-legal-ar, julio 2026: hubo incidente de apelación, recurso de inconstitucionalidad DENEGADO y queja ante el TSJ CABA; el legajo seguía con movimiento al 30/06/2026). Citar como criterio, no como cosa juzgada. Confirmar además, contra el texto de la sentencia, si la condena fue por hostigamiento digital (art. 71 ter) o por discriminación (art. 71, Ley 5261 CABA): fuentes periodísticas sugieren que el 71 ter podría haber sido descartado]
```

**Art. 71 quater - Agravantes:** las sanciones de los arts. 71 bis y 71 ter se elevan al doble cuando
la víctima es menor de 18 años, mayor de 70 años o persona con discapacidad, o cuando la contravención
se comete con el concurso de dos o más personas.

**Art. 71 quinquies - Suplantación digital de la identidad (Ley 6128):** sanciona a quien utiliza la
imagen o los datos filiatorios de una persona, o crea una identidad falsa con la imagen o los datos
filiatorios de una persona, mediante cualquier tipo de comunicación electrónica, transmisión de
datos, página web u otro medio, sin mediar consentimiento de la víctima, **siempre que el hecho no
constituya delito**. La sanción prevista es de multa (entre 160 y 400 unidades fijas) o de uno a
cinco días de trabajo de utilidad pública o de arresto. Es la vía residual para la usurpación de
identidad digital en CABA cuando no hay perjuicio patrimonial que habilite el art. 173 inc. 16 CP ni
acceso ilícito que habilite el art. 153 bis CP: ver desarrollo del escenario en "Lógica de análisis -
Usurpación de identidad digital".

**Regla operativa - orden de prelación penal/contravencional:** antes de encuadrar un hecho en el
Código Contravencional CABA, descartar expresamente que la conducta configure alguna de las figuras
penales de la sección anterior (chantaje, violación de secretos, amenazas, delitos contra la
integridad sexual). La vía contravencional es residual: opera únicamente cuando el hecho no alcanza a
configurar delito. Si hay duda razonable sobre el encuadre, señalarlo y no descartar la vía penal sin
haberla evaluado primero.

**Prescripción de la acción contravencional - plazo breve, instar sin demora:** a diferencia de la
acción civil o de muchos delitos, la acción contravencional prescribe a los dos (2) años de cometida
la contravención o de su cesación si fuera permanente (art. 42 CCABA), y la sanción ya impuesta
prescribe a los dos (2) años de quedar firme la sentencia (art. 43 CCABA). La prescripción de la
acción solo se interrumpe por la celebración de la audiencia de juicio o por la rebeldía del
imputado/a (art. 44 CCABA). Dado que es un plazo sensiblemente más corto que el de la mayoría de las
acciones civiles, instar la denuncia contravencional sin demora una vez decidida esa vía.

```
[VERIFICAR VIGENCIA: arts. 42, 43 y 44 CCABA (prescripción de la acción, de la sanción e interrupción) - texto confirmado por búsqueda web julio 2026 en 2 años para ambos plazos; verificar que no haya sufrido modificación posterior antes de contar el plazo en un caso concreto]
```

```
[VERIFICAR VIGENCIA: arts. 71 bis, 71 ter, 71 quater y 71 quinquies del Código Contravencional CABA (Ley 6017/6128, texto consolidado) - unidad fija confirmada en $949,99 para el período marzo-septiembre 2026 (búsqueda web julio 2026); verificar valor vigente al momento del hecho ya que se actualiza semestralmente]
```

### Responsabilidad de intermediarios - buscadores y plataformas

**Doctrina cargada - CSJN "Rodríguez, María Belén c/ Google Inc. s/ daños y perjuicios", R.522.XLIX,
Fallos 337:1174 (28/10/2014):** leading case sobre responsabilidad civil de los motores de búsqueda
en Argentina. La Corte juzgó la responsabilidad de los buscadores bajo el estándar de responsabilidad
subjetiva (no objetiva): en principio no tienen obligación general de monitorear contenidos de
terceros, pero responden por culpa a partir del momento en que toman conocimiento efectivo del
contenido ilícito (por notificación fehaciente, cuando el daño es manifiesto y grosero, o por vía
judicial o administrativa cuando el contenido exige esclarecimiento) si no procuran el bloqueo del
resultado. La Corte trató en el mismo fallo el uso no autorizado de imágenes ("thumbnails") a la luz
del art. 31 de la Ley 11.723 (derecho a la imagen), con disidencia parcial de los jueces Lorenzetti y
Maqueda sobre ese punto. Precedentes concordantes que ratifican el mismo estándar: CSJN, "Gimbutas,
Carolina Valeria", Fallos 340:1236, y CSJN, "Mazza", Fallos 344:1881 (2021).

**Límite del estándar - CSJN "Denegri, Natalia Ruth c/ Google Inc. s/ Derechos personalísimos:
acciones relacionadas", Fallos 345:482 (28/06/2022):** no confundir con un refuerzo de la
responsabilidad de los buscadores. La Corte, por unanimidad, rechazó un pedido de desindexación
fundado en el "derecho al olvido" respecto de contenido veraz y de interés público sobre una persona
que conservaba carácter público, dando prioridad a la libertad de expresión. El estándar de
"Rodríguez" y "Gimbutas" parte de la ilicitud del contenido (violencia digital, imágenes íntimas sin
consentimiento); "Denegri" resuelve el supuesto inverso, de contenido lícito cuya remoción se pide por
el mero paso del tiempo. No invocar "Denegri" como apoyo a un pedido de remoción de contenido de
violencia digital: el fundamento de la petición en esos casos debe seguir siendo la ilicitud del
contenido bajo el estándar de "Rodríguez", no el derecho al olvido.

**Regla operativa:** al peticionar el bloqueo, la desindexación o la remoción de contenido a un
buscador o plataforma (más allá de la orden específica del art. 26 apartado a.9 Ley 26.485 para
violencia de género), fundar la responsabilidad del intermediario en el estándar de "Rodríguez, María
Belén": acreditar la notificación fehaciente previa del contenido ilícito y el conocimiento efectivo
por parte del intermediario, no la sola existencia del contenido. No asumir responsabilidad objetiva
de buscadores o plataformas por contenido de terceros. No invocar "Denegri" para este fundamento: ver
el párrafo anterior sobre el límite de ese precedente.

```
[VERIFICAR PRECEDENTE: confirmado por búsqueda web julio 2026 que "Rodríguez, María Belén" (Fallos 337:1174), "Gimbutas" (Fallos 340:1236), "Mazza" (Fallos 344:1881) y "Denegri" (Fallos 345:482) no fueron dejados sin efecto ni superados por jurisprudencia posterior de la CSJN ni por reforma legislativa sobre responsabilidad de intermediarios - repetir la verificación en cada consulta antes de citar]
```

**Precedente verificado - medida urgente de remoción con componente de género (vía civil/familia, no
autosatisfactiva pura):** Cámara Nacional de Apelaciones en lo Civil, Sala M, "Q. C., E. S. c/ T., B. s/
Denuncia por violencia familiar", 15/07/2022 (voto de los jueces Calvo Costa, González Zurro y
Benavente). Verificado contra múltiples fuentes independientes (búsqueda web julio 2026). En el marco
de una denuncia por violencia doméstica con dictamen previo de la Oficina de Violencia Doméstica
(OVD), la Cámara revocó la resolución de primera instancia y ordenó al denunciado eliminar de todos
sus dispositivos - incluida la nube - el material íntimo de la denunciante en el plazo de 48 horas, bajo
apercibimiento de multa, calificando la difusión no consentida de material íntimo como una forma de
violencia de género digital, con fundamento en la CEDAW y la Convención de Belém do Pará. Útil como
precedente de tutela urgente dentro del esquema de la Ley 26.485 (medidas del art. 26), no como
precedente autónomo para el escenario "Hecho sin componente de género" de este perfil, porque el
caso se sustenta expresamente en el dictamen de violencia de género de la OVD.

```
[VERIFICAR PRECEDENTE: "Q. C., E. S. c/ T., B." (CNCiv. Sala M, 15/07/2022) - contenido y holding verificados (múltiples fuentes, julio 2026); firmeza NO verificable desde los conectores porque las partes están anonimizadas y la consulta pública del PJN solo admite búsqueda por demandado con nombre real. Confirmar firmeza por otra vía antes de citar]
```

### Protección de datos personales (Ley 25.326)

Cuando el hecho involucra robo, acceso o difusión no consentida de datos personales (no solo imágenes
íntimas), articular con proteccion-datos-CLAUDE.md: derecho de acceso, rectificación y supresión,
acción de hábeas data. La propia Ley 26.485 (art. 6 inc. i, texto según Ley 27.736) remite a la Ley
25.326 para deslindar qué conductas de tratamiento de datos están permitidas.

### Derechos personalísimos - Código Civil y Comercial

- Art. 51 CCyC: inviolabilidad de la persona humana.
- Art. 52 CCyC: afectaciones a la dignidad (legitimación para reclamar la prevención y reparación de
  los daños derivados de la interferencia arbitraria en la vida ajena, la difamación, la imagen o la
  identidad).
- Art. 53 CCyC: derecho a la imagen - requiere el consentimiento de la persona para captar o
  reproducir su imagen o voz, con las excepciones legales previstas (interés científico, cultural o
  educacional prioritario; ejercicio regular del derecho de informar sobre acontecimientos de interés
  general; y las demás del propio artículo).
- Art. 1770 CCyC: protección de la vida privada - habilita al juez, a pedido del afectado, a ordenar
  el cese de las actividades intrusivas y la reparación del daño causado, sea que exista o no delito
  penal.

```
[VERIFICAR VIGENCIA: arts. 51, 52, 53 y 1770 CCyC (Ley 26.994) - primera mención]
```

### Medidas autosatisfactivas - vía civil pura sin componente de género

**Cuándo se activa esta vía:** la Ley 26.485 exige que la conducta esté "basada en razones de género"
(art. 4). Cuando el hecho de violencia digital -difusión de contenido íntimo, usurpación de identidad,
hostigamiento- ocurre entre personas del mismo género, entre hombres, en un conflicto societario o
comercial, o en cualquier otro escenario donde no pueda sostenerse el componente de género exigido por
la Ley 26.485, esa ley no es la vía idónea para las medidas de protección. La vía de escape en esos
casos es la acción civil pura, con fundamento en los arts. 52 y 1770 CCyC (ver sección anterior), por
la vía procesal de la medida autosatisfactiva.

**Naturaleza de la medida autosatisfactiva:** se trata de una construcción doctrinaria y
jurisprudencial (desarrollada originalmente por Jorge W. Peyrano) para requerimientos urgentes cuya
satisfacción agota el objeto del proceso, sin necesidad de una pretensión principal pendiente ni de
contracautela en la medida en que la propia urgencia y verosimilitud lo justifiquen. No está
regulada de modo uníforme en los códigos procesales nacional ni provinciales: su procedencia y sus
requisitos (verosimilitud del derecho, urgencia impostergable, fuerte probabilidad de que el derecho
asista al peticionante) se construyen sobre la base de las medidas cautelares genéricas del código
procesal aplicable (arts. 232 y concordantes CPCCN, o el código procesal local) y de la elaboración
jurisprudencial de cada fuero.

**Regla operativa:** antes de encuadrar el pedido como medida autosatisfactiva, verificar el criterio
del fuero y del juzgado sobre su admisibilidad como vía autónoma, ya que no todos los tribunales la
reconocen con ese nombre ni con esos requisitos. Si el fuero no admite la figura de forma autónoma,
reformular el pedido como medida cautelar innovativa o de no innovar dentro de un proceso de
conocimiento (ver criterio análogo en proteccion-datos-CLAUDE.md, sección "Medidas cautelares -
bloqueo preventivo del dato", para la estructura de verosimilitud y peligro en la demora).

```
[VERIFICAR CRITERIO DEL FUERO: admisibilidad de la medida autosatisfactiva como vía autónoma - fuero y juzgado actuante - verificar si exige contracautela y si reconoce la figura fuera del marco cautelar clásico]
```

**Fallo verificado - límite de la vía, no respaldo:** Cámara Federal de Resistencia, "Centro de Empleados
de Comercio - Filial Formosa y otros c/ Facebook Argentina SRL y otros s/ Medida Autosatisfactiva",
Expte. FRE 4364/2021/CA1, 04/09/2023. Verificado contra el texto completo de la sentencia (búsqueda
web julio 2026). **Ojo: este fallo revocó la medida autosatisfactiva, no la confirmó.** El gremio había
obtenido en primera instancia (2019) la eliminación de contenido y el bloqueo de cuentas anónimas que
criticaban a su comisión directiva en Facebook; la Cámara hizo lugar a la apelación de Facebook
Argentina SRL y dejó sin efecto la orden, por considerar que las publicaciones se vinculaban con la
actividad sindical de los actores (funcionarios de un gremio, materia de interés público) y que la
libertad de expresión goza de protección reforzada en esos casos, citando "Denegri", "Rodríguez, María
Belén", "Gimbutas" y "Paquez" (Fallos 342:2187). Sí es útil el fallo para otro punto: rechazó la falta de
legitimación pasiva planteada por Facebook Argentina SRL, confirmando que puede ser demandada
directamente sin necesidad de dirigirse contra Facebook Inc.

```
[PRECEDENTE FIRME (alta probabilidad): "Centro de Empleados de Comercio - Filial Formosa c/ Facebook Argentina SRL" (FRE 4364/2021, Cám. Fed. Resistencia, sentencia 04/09/2023) - verificado en el PJN vía mcp-legal-ar (julio 2026): notificada el 22/09/2023, autos devueltos al Juzgado Federal de Formosa 2, sin recurso extraordinario ni queja registrados, expediente EN LETRA e inactivo desde 23/10/2023. Firmeza con alta probabilidad; para certeza plena, descartar un REF/queja tramitado en expediente separado ante la CSJN]
```

**Cuándo aplica y cuándo no:** este precedente es un límite, no un respaldo, para peticiones de
remoción de contenido en el escenario "Hecho sin componente de género" de este perfil. Si el contenido
cuestionado versa sobre la actuación de un funcionario, dirigente gremial o figura pública en ejercicio
de su función, la vía de la medida autosatisfactiva enfrenta un estándar reforzado de libertad de
expresión y probablemente no prospere. Distinto es el caso de contenido íntimo, difamatorio personal
o de suplantación de identidad entre particulares sin proyección de interés público - el escenario que
cubre este perfil - donde el estándar de "interés público" de "Denegri" y "Paquez" no rige de la misma
manera. No usar este fallo para argumentar a favor de una medida autosatisfactiva sin aclarar esta
distinción.

```
[INSERTAR FALLO VERIFICADO: procedencia (no solo límite) de medida autosatisfactiva para remoción de contenido digital o cese de usurpación de identidad sin componente de género en un caso de contenido íntimo o personal sin proyección de interés público - fuero, sala y año]
```

---

## Prueba y cadena de custodia digital

### Regla operativa inicial - la "regla de los tres no" (y un sí)

Ante cualquier consulta inicial, transmitir a la víctima:
- No borrar la información ni las conversaciones.
- No reenviar los datos recibidos (evita que se pierda la integridad de metadatos y multiplica las
  copias sin control).
- No bloquear al agresor antes de resguardar la evidencia (el bloqueo puede impedir el acceso
  posterior a mensajes, perfiles o URL relevantes).
- Sí activar la verificación en dos pasos (2FA) y revisar/cerrar las sesiones activas desconocidas en
  sus propias cuentas, especialmente en casos de usurpación de identidad o acceso ilícito: esto no
  destruye evidencia ya generada, pero corta el acceso del agresor mientras se completa el resguardo
  de la prueba.

### Resguardo de evidencia

- Capturas de pantalla completas (no recortadas) de mensajes, comentarios, publicaciones, correos y
  perfiles, con fecha y hora visibles cuando sea posible.
- Registro de las URL exactas de los contenidos publicados: es un requisito expreso para que proceda
  la orden de supresión del art. 26 apartado a.9 Ley 26.485 (texto según Ley 27.736).
- No denunciar el perfil o el contenido ante la propia plataforma antes de la denuncia penal o
  contravencional y del resguardo de la evidencia: el reporte a la plataforma puede derivar en el
  borrado del contenido y la pérdida de evidencia disponible para el organismo de investigación.
- Evaluar si corresponde solicitar pericia informática sobre el dispositivo de la víctima o del
  imputado, y peticionar su gratuidad conforme el art. 16 inc. a) Ley 26.485 (texto según Ley 27.736).

```
[VACÍO PROBATORIO: capturas de pantalla, URL y metadatos del contenido denunciado - sin este resguardo, la pericia informática y la orden de supresión de contenidos pueden resultar inviables]
```

---

## Organismos y canales de denuncia

- **UFECI (Unidad Fiscal Especializada en Ciberdelincuencia, Procuración General de la Nación,
  Resolución PGN 3743/15):** competente en delitos informáticos de jurisdicción federal y nacional
  fuera de CABA, y como nexo con fiscalías de todo el país. Denuncias: denunciasufeci@mpf.gob.ar;
  consultas de fiscalías y juzgados: (+54 11) 5071-0040/0044.
- **UFEDyCI (Unidad Fiscal Especializada en Delitos y Contravenciones Informáticas, Ministerio
  Público Fiscal CABA):** competente para delitos y contravenciones informáticas cometidos en el
  ámbito de la Ciudad. Denuncia telefónica gratuita las 24 horas: 0800-333-FISCAL (0800 333 347225);
  también por app "Denuncias MPF" o presencial. Es el organismo específico para encuadrar los arts.
  71 bis, 71 ter y 71 quater del Código Contravencional CABA.
- **Centro de Asistencia a la Víctima (Dirección General de la Mujer, GCBA):** asiste a víctimas de
  delitos informáticos contra la integridad sexual con acompañamiento psicológico, asesoramiento
  jurídico y asistencia social. Contacto: delitossexuales@buenosaires.gob.ar.
- **Línea 144:** información, contención y asesoramiento en violencia de género (incluye violencia
  digital). También disponible el Boti (11-5050-0147).
- **911:** para situaciones de riesgo de vida inminente.

```
[VERIFICAR VIGENCIA: canales de denuncia y datos de contacto de UFECI, UFEDyCI y Centro de Asistencia a la Víctima - confirmados sin cambios por búsqueda web julio 2026 (UFECI: denunciasufeci@mpf.gob.ar, 5071-0040/0044; UFEDyCI: 0800-333-347225); repetir la verificación al momento de la consulta ya que los canales operativos pueden actualizarse]
```

---

## Articulación con otros perfiles

- **penal-CLAUDE.md:** para el desarrollo procesal completo de la causa penal (etapas, prueba,
  recursos) y para el marco general de "Delitos informáticos" y "Violencia de género y delitos contra
  la integridad sexual". Este perfil no reemplaza esas secciones: las complementa con el encuadre
  específico de violencia digital.
- **familia-CLAUDE.md:** cuando el hecho se enmarca en una relación de pareja o ex pareja con otras
  manifestaciones de violencia familiar (Ley 24.417 y régimen local), o cuando hay niños, niñas o
  adolescentes expuestos. Las medidas del art. 26 Ley 26.485 con componente digital pueden
  peticionarse en el mismo proceso de protección contra la violencia familiar.
- **proteccion-datos-CLAUDE.md:** cuando el hecho incluye robo, acceso indebido o difusión de datos
  personales que exceda el contenido íntimo (por ejemplo, documentación, datos bancarios, DNI).
- **civil-CLAUDE.md:** para la cuantificación del daño moral y patrimonial cuando se opta por la
  acción civil de daños, sea en forma autónoma o acumulada a la causa penal.

---

## Reglas de citación - violencia digital

Las reglas generales del CLAUDE.md argentino aplican íntegramente. Específicas para este perfil:

**Tipificación de la difusión no consentida de imágenes íntimas:** no afirmar que existe un delito
autónomo en el Código Penal nacional para la "pornovenganza". Usar:
```
[REVISIÓN NORMATIVA REQUERIDA: verificar si alguno de los proyectos de tipificación de la difusión no consentida de imágenes íntimas fue sancionado - encuadrar mientras tanto por las figuras penales existentes (chantaje, violación de secretos, amenazas) o por el Código Contravencional CABA]
```

**Jurisprudencia:** nunca citar carátula, sala, fuero o año sin material aportado, incluidos los
antecedentes conocidos en la materia (por ejemplo, casos difundidos en medios). Usar:
```
[INSERTAR FALLO VERIFICADO: doctrina requerida sobre encuadre de la difusión no consentida de imágenes íntimas o del hostigamiento digital - aportar expediente, sala, fuero y año]
```

**Identificación del contenido digital:** no describir ni dar por acreditado el contenido de una
publicación, mensaje o perfil sin la captura, URL o constancia aportada. Usar:
```
[VACÍO PROBATORIO: contenido digital denunciado no acreditado - aportar captura de pantalla, URL o constancia con fecha y hora]
```

---

## Lógica de análisis por escenario

### Diagnóstico inicial - identificar el escenario antes de elegir la vía

1. ¿Hubo difusión efectiva del material, o solo amenaza de difusión?
2. ¿Hay exigencia patrimonial o de otra prestación asociada a la amenaza (sextorsión) o la conducta se
   agota en el hostigamiento?
3. ¿La víctima es menor de edad?
4. ¿El vínculo con el agresor es de pareja, ex pareja, conocido o desconocido?
5. ¿Hay violencia familiar concurrente que amerite activar familia-CLAUDE.md en paralelo?
6. ¿Se resguardó evidencia (capturas, URL) antes de cualquier reporte a la plataforma?
7. ¿Corresponde encuadre penal, contravencional CABA, o ambos deben evaluarse en conjunto?

### Pornovenganza (difusión ya consumada)

Evaluar en este orden: (a) si hubo exigencia patrimonial o de otra prestación antes o durante la
difusión, priorizar el chantaje (art. 169 CP); (b) si el material proviene de una comunicación
electrónica interceptada o accedida sin autorización, evaluar arts. 153, 153 bis y 155 CP en concurso
con la figura anterior si corresponde; (c) si ninguna figura penal encuadra con claridad y el hecho
ocurrió en CABA, evaluar el art. 71 bis del Código Contravencional; (d) en paralelo, peticionar las
medidas de protección del art. 26 Ley 26.485 (apartados a.8 y a.9) para el cese de contacto y la
supresión de contenidos, con independencia de la vía penal o contravencional elegida.

### Sextorsión (amenaza de difusión con exigencia)

Encuadre primario en el art. 169 CP (chantaje). Si la exigencia no es patrimonial sino de más material
íntimo o de otra prestación no patrimonial, evaluar si igual encuadra en el art. 169 CP (la figura
exige que el resultado obligado sea alguno de los enumerados en el art. 168 CP - entrega, envío,
depósito o puesta a disposición de cosas, dinero o documentos que produzcan efectos jurídicos) o si
corresponde encuadrar directamente como amenazas (art. 149 bis CP) por no cumplirse el elemento
patrimonial exigido por la figura de extorsión.

```
[VERIFICAR CRITERIO DEL FUERO: encuadre de la sextorsión cuando la exigencia no consiste en dinero, cosas o documentos con efectos jurídicos sino en más material íntimo - chantaje (art. 169 CP) vs. amenazas (art. 149 bis CP) - criterio de la fiscalía o juzgado interviniente]
```

### Hostigamiento y acoso digital sin contenido íntimo

Si no hay difusión ni amenaza de difusión de contenido íntimo, sino mensajes reiterados, control de la
actividad virtual, o intimidación por medios digitales, evaluar primero las figuras penales
específicas según el contenido concreto (amenazas, art. 149 bis CP), y si no encuadran, el art. 71 ter
del Código Contravencional CABA (hostigamiento digital), siempre que el hecho no constituya delito.

### Grooming y contenido de menores de edad

Activar directamente penal-CLAUDE.md, sección "Violencia de género y delitos contra la integridad
sexual" (arts. 128 y 131 CP). No aplicar el Código Contravencional CABA cuando la víctima es menor de
edad y el hecho encuadra en esas figuras: la vía contravencional es residual y no alcanza a delitos.

### Violencia vincular ejercida por TIC en el marco de una relación de pareja o ex pareja

Activar en paralelo familia-CLAUDE.md para el proceso de protección contra la violencia familiar y
este perfil para el componente digital específico. El art. 26 Ley 26.485 (apartados a.2, a.8 y a.9,
texto según Ley 27.736) puede peticionarse dentro del mismo proceso de protección, sin necesidad de un
expediente separado.

### Usurpación de identidad digital (perfiles falsos, cuentas suplantadas)

Evaluar el art. 173 inc. 16 CP (defraudación informática, cuando hay perjuicio patrimonial) o los
arts. 153 bis y 183 CP (acceso ilegítimo y daño informático) según la modalidad. Ver penal-CLAUDE.md,
sección "Delitos informáticos", y proteccion-datos-CLAUDE.md cuando la usurpación derivó en la
apertura de cuentas o créditos a nombre de la víctima. Si el hecho ocurrió en CABA y ninguna figura
penal encuadra (no hay perjuicio patrimonial ni acceso ilícito a sistema restringido - por ejemplo, un
perfil falso armado solo con imágenes públicas de la víctima), evaluar el art. 71 quinquies del
Código Contravencional CABA (suplantación digital de la identidad), siempre que el hecho no
constituya delito.

### Hecho sin componente de género (entre hombres, conflicto societario o comercial)

Cuando no puede sostenerse el componente de género exigido por el art. 4 Ley 26.485 - por ejemplo,
difusión de contenido íntimo o difamatorio entre socios, competidores comerciales o personas del mismo
género sin relación de pareja -, descartar la vía de la Ley 26.485 para las medidas de protección y
evaluar: (a) la vía penal según las figuras de "Marco normativo" (chantaje, violación de secretos,
amenazas, daño informático) si corresponde; (b) en CABA, el Código Contravencional si el hecho no
constituye delito; (c) la medida autosatisfactiva de la sección "Medidas autosatisfactivas - vía civil
pura sin componente de género" para la remoción urgente del contenido, articulada con civil-CLAUDE.md
para la cuantificación del daño.

---

## Instrucciones operativas específicas - violencia digital

- Verificar primero si la víctima resguardó evidencia (capturas, URL) antes de cualquier reporte a la
  plataforma o bloqueo del agresor. Si no lo hizo, indicar la regla de los tres no antes de avanzar con
  el encuadre jurídico.
- No calificar la difusión no consentida de imágenes íntimas como delito autónomo del Código Penal
  nacional: verificar el estado parlamentario de los proyectos vigentes antes de cualquier afirmación
  sobre tipicidad penal específica.
- Distinguir siempre chantaje (art. 169 CP) de extorsión genérica (art. 168 CP) según el medio
  comisivo específico: amenaza de imputaciones contra el honor o de violación de secretos, frente a
  intimidación genérica o simulación de autoridad pública.
- En CABA: no encuadrar en el Código Contravencional (arts. 71 bis, 71 ter, 71 quater) sin haber
  descartado primero que el hecho configure alguna figura penal. La vía contravencional es residual.
- Incluir siempre, cuando corresponda pedir medidas de protección bajo la Ley 26.485, los apartados
  a.8 (prohibición de contacto por TIC) y a.9 (supresión de contenidos con identificación de URL) del
  art. 26, no solo la orden de cese genérica.
- Si la víctima es menor de edad: activar directamente el módulo de grooming y pornografía infantil de
  penal-CLAUDE.md, no el Código Contravencional CABA.
- Si hay violencia vincular concurrente (pareja o ex pareja): activar familia-CLAUDE.md en paralelo y
  evaluar si las medidas digitales del art. 26 Ley 26.485 se peticionan en el mismo proceso de
  protección familiar.
- Si hay componente de datos personales más allá del contenido íntimo (robo de identidad, apertura de
  cuentas o créditos): derivar a proteccion-datos-CLAUDE.md para la estrategia de hábeas data y
  reclamo ante entidades financieras.
- Todo escrito de violencia digital cierra con "Estado del escrito" estándar más: vía elegida (penal /
  contravencional CABA / medidas de protección Ley 26.485 / civil / combinación), evidencia digital
  resguardada (sí/no - descripción), medidas de protección peticionadas (apartados del art. 26
  incluidos), y estado de los proyectos de tipificación de la difusión no consentida de imágenes
  íntimas si el encuadre penal depende de esa verificación.

---

## Fuentes primarias

- **InfoLEG (infoleg.gob.ar):** texto oficial de la Ley 26.485, Ley 27.736 y Código Penal
- **Boletín Oficial (boletinoficial.gob.ar):** texto de sanción de la Ley 27.736 (aviso 296572,
  10/10/2023)
- **UFECI (fiscales.gob.ar/ciberdelincuencia):** organismo especializado, informes de gestión
- **MPF CABA (mpfciudad.gob.ar):** UFEDyCI, canales de denuncia
- **JUSBAIRES / Defensoría del Pueblo CABA:** análisis del Código Contravencional CABA en materia
  digital
- **Dirección General de la Mujer, GCBA (buenosaires.gob.ar):** Centro de Asistencia a la Víctima,
  recursos de orientación a víctimas
- **SAIJ (saij.gob.ar):** jurisprudencia y legislación

---

*Última actualización: julio 2026*
*Normativa base: Ley 26.485, Ley 27.736 (Ley Olimpia), CP (Ley 11.179) arts. 128, 131, 149 bis, 153,
153 bis, 155, 157, 168, 169, 173 inc. 16 y 183, Código Contravencional CABA (Ley 6017/6128, texto
consolidado) arts. 71 bis, 71 ter, 71 quater y 71 quinquies, Ley 25.326, CCyC (Ley 26.994) arts. 51,
52, 53 y 1770*
*Jurisprudencia CSJN citada: "Rodríguez, María Belén" (Fallos 337:1174), "Gimbutas" (Fallos
340:1236), "Mazza" (Fallos 344:1881) y "Denegri" (Fallos 345:482) - verificados por búsqueda web julio
2026, ver sección "Responsabilidad de intermediarios" para el alcance y el límite de cada uno*
*Verificado contra fuentes: Boletín Oficial (texto de sanción de la Ley 27.736), Infoleg, MPF Nación
y MPF CABA, GCBA, CSJN - Secretaría de Jurisprudencia (búsqueda web julio 2026)*
*Pendiente: verificar sanción de algún proyecto de tipificación de la difusión no consentida de
imágenes íntimas (0304-D-2025, "Ley Belén" 2757-D-22, iniciativa Zamora abril 2026) en cada consulta
antes de descartar la existencia de un tipo penal específico*
*Autor: Dr. Cristian Aboitiz · [@abogadoaboitiz](https://x.com/abogadoaboitiz) · perfil generado a
partir de instrucción de la Dra. Ximena*
