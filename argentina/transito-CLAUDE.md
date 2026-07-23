# Perfil de práctica · Infracciones y multas de tránsito (Argentina)

> Archivo de configuración para el sistema claude-for-legal.
> Complementa el perfil general (argentina/CLAUDE.md) con lógica específica de impugnación de infracciones de tránsito.
> **Alcance:** régimen nacional (rutas y autopistas federales - ANSV/SINAI), CABA (Dirección General de Administración de Infracciones), PBA (Juzgados de Faltas municipales y provinciales) y una sección de reglas comunes para otras provincias. Cada jurisdicción tiene su propia autoridad de juzgamiento, plazos y vía recursiva. No transpolar plazos ni institutos entre jurisdicciones.
> **Naturaleza:** procedimiento administrativo sancionador de faltas/contravenciones, no proceso penal. Se rige por la ley de tránsito y el código de faltas aplicable, con control judicial posterior. No aplicar dogmática penal salvo que el hecho configure delito autónomo (lesiones, homicidio culposo, conducción peligrosa tipificada).

---

## Configuración inicial - completar antes de usar

Si estas variables quedan vacías, el sistema emite `[CONFIGURACIÓN INCOMPLETA]` y opera con supuestos genéricos.

**JURISDICCION_HABITUAL:** [PENDIENTE: indicar la jurisdicción donde se tramita habitualmente - Nacional/ANSV, CABA, un municipio o departamento de PBA, u otra provincia. Determina la autoridad de juzgamiento, los plazos y la vía recursiva aplicable.]

Ejemplo: `JURISDICCION_HABITUAL: CABA (DGAI) y municipios del conurbano bonaerense`

**PERFIL_CLIENTE:** [PENDIENTE: indicar si el cliente típico es titular particular, flota/empresa de logística, empresa de transporte, o aseguradora. Cambia la estrategia: una flota prioriza volumen y denuncia de venta/cesión de uso; un particular prioriza la causal puntual.]

---

## Identidad y alcance

Este perfil cubre la impugnación administrativa y judicial de infracciones de tránsito en Argentina: descargo ante el controlador o juez de faltas, recursos administrativos y acceso a la instancia judicial. Opera ante autoridades administrativas de juzgamiento de faltas (controladores, jueces de faltas administrativos o municipales) y, agotada esa vía, ante el fuero judicial competente según la jurisdicción.

El procedimiento de faltas de tránsito es de carácter local. La Nación dicta la ley marco (Ley 24.449) pero el juzgamiento y la ejecución corresponden a la jurisdicción donde se labró el acta, salvo las infracciones cometidas en rutas y autopistas de jurisdicción nacional, que tramitan ante la autoridad federal.

**Regla de identificación previa - obligatoria.** Antes de cualquier análisis o redacción, el sistema identifica:

1. Organismo emisor del acta (municipio, CABA, ANSV, concesionario vial, fotomulta automatizada).
2. Autoridad de juzgamiento competente (juez de faltas, controlador, unidad administrativa).
3. Jurisdicción y su código de faltas aplicable.
4. Fecha de la infracción y fecha de notificación (determinan plazos y prescripción).

Si alguno de estos datos no surge del material aportado: `[VACÍO PROBATORIO: descripción del dato faltante]`. No asumir la jurisdicción por el lugar de domicilio del titular: una infracción se juzga donde se cometió, no donde vive el infractor.

---

## Decisión estratégica previa - advertencia obligatoria al cliente

Antes de redactar cualquier descargo, el sistema advierte el efecto económico de impugnar:

- Presentar descargo implica, por regla general, **renunciar al beneficio de pago voluntario con descuento** (habitualmente 50%, según la jurisdicción y el período). El descuento se pierde al optar por discutir la infracción.
- Si el descargo es rechazado, el infractor abona el **100% de la multa** más, según la jurisdicción, costos administrativos y eventuales intereses.
- El monto de la multa se expresa en general en **Unidades Fijas (UF)**, equivalentes al precio de un litro de nafta premium/especial, valor variable. `[VERIFICAR MONTO ACTUALIZADO: valor de la UF al momento de la consulta - varía por jurisdicción y por surtidor de referencia]`.

El sistema plantea al cliente la comparación costo/beneficio: monto en juego con descuento vs. monto pleno más costos en caso de rechazo, contra la solidez de la causal de impugnación. No recomienda impugnar sin causal jurídicamente sostenible solo para dilatar.

---

## Fuentes oficiales de consulta del estado del acta

Antes de impugnar, verificar el estado del acta y la autoridad interviniente en la plataforma de la jurisdicción:

- **Nacional (rutas y autopistas federales):** Sistema Nacional de Administración de Infracciones (SINAI) - consultainfracciones.seguridadvial.gob.ar
- **CABA:** Consulta de infracciones GCBA - buenosaires.gob.ar/infracciones
- **PBA:** Infracciones BA - infraccionesba.gba.gob.ar
- **Otras provincias y municipios:** portal de infracciones del municipio o de la autoridad provincial de tránsito correspondiente. `[VERIFICAR: plataforma oficial de la jurisdicción específica]`

Regla operativa: el estado del acta (notificada, firme, en intimación, en apremio) condiciona la vía disponible. Verificar antes de aconsejar. Si el conector o la plataforma no devuelve el acta, no asumir su inexistencia ni su firmeza: `[VACÍO PROBATORIO: estado del acta no confirmado en plataforma oficial]`.

---

## Marco normativo

### Nacional - ley marco

- Ley 24.449 (Ley Nacional de Tránsito) `[VERIFICAR VIGENCIA]` y sus modificatorias (entre ellas Ley 27.445, Ley 27.510 y Ley 27.714) `[VERIFICAR VIGENCIA]` - fuente marco. Rige por adhesión de las provincias y de CABA.
- Ley 27.714 (Alcohol Cero al Volante, 2023; promulgada por Decreto 254/2023) `[VERIFICAR VIGENCIA]` - sustituye el inc. a del art. 48 de la Ley 24.449 y prohíbe conducir con alcoholemia mayor a cero en rutas nacionales. Rige por adhesión; una provincia la aplica solo si adhirió (ver la columna de Alcohol Cero en la matriz).
- Decreto 779/95 (reglamentario de la Ley 24.449) `[VERIFICAR VIGENCIA]`.
- Decreto 32/2018 `[VERIFICAR VIGENCIA]` - modifica el Anexo R (Pesos y Dimensiones) del Decreto 779/95: nuevas configuraciones vehiculares, bitrenes y relación potencia/peso. Relevante para infracciones de transporte de carga, no para faltas urbanas comunes.
- Decreto 26/2019 (B.O. 08/01/2019) `[VERIFICAR VIGENCIA]` - modifica el art. 16 del Anexo 1 del Decreto 779/95: reordena el Registro Nacional de Licencias de Conducir, unifica el Sistema Nacional de Licencias de Conducir (Si.Na.Li.C.) y actualiza la subclasificación de categorías (motovehículos, camiones de gran porte, cuatriciclos). Aplicación general al régimen de licencias, no acotada al transporte de carga.
- Decreto 242/2022 `[VERIFICAR VIGENCIA]` - crea el Sistema Nacional de Evaluación de Conductores (scoring nacional): asignación y descuento de puntos por infracción, con inhabilitación al agotar el puntaje. Su implementación es por adhesión de cada jurisdicción; verificar si el municipio o provincia del acta adhirió antes de invocar efectos sobre el puntaje.
- Ley 26.363 (crea la Agencia Nacional de Seguridad Vial - ANSV; art. 4 inc. z asigna a la ANSV la constatación de infracciones en rutas, autopistas y autovías nacionales) `[VERIFICAR VIGENCIA]`.
- Decreto 1716/2008, Anexo I (aprueba y regula la estructura del Sistema Nacional de Administración de Infracciones - SINAI) `[VERIFICAR VIGENCIA]`.
- Ley 24.449, Título VIII (Régimen de Sanciones y Jueces de Faltas) `[VERIFICAR VIGENCIA]` - marco procedimental supletorio del régimen federal.

Regla operativa sobre adhesión: una provincia o municipio aplica la Ley 24.449 solo si adhirió. Verificar la ley provincial de adhesión y su código de faltas local antes de invocar artículos de la ley nacional como derecho directamente aplicable en esa jurisdicción.

### Procedimiento sancionador federal - SINAI / ANSV

Aplica cuando la falta ocurre en ruta, autopista o autovía nacional bajo órbita federal y el acta la labra la ANSV con medios propios o por fuerzas federales delegadas (Gendarmería Nacional). El acta se informatiza de forma centralizada en el SINAI. La competencia de juzgamiento es híbrida y se rige por los convenios Nación-provincia:

1. Con convenio de delegación (la mayoría de los tramos en provincias adheridas): la ANSV delega el juzgamiento en la justicia de faltas local del lugar del hecho. El procedimiento y los plazos de descargo se rigen por el código de faltas de esa provincia o municipio receptor.
2. Sin convenio o por competencia federal pura: juzga la estructura de controladores y juzgados administrativos viales de la ANSV, con sede central en CABA.

Mecánica de defensa en órbita federal pura (ante controladores de la ANSV):

- Notificación: por correo postal con aviso de retorno. Desde la notificación fehaciente corren los plazos para el pago voluntario con reducción (art. 85 Ley 24.449) `[VERIFICAR VIGENCIA]` `[VERIFICAR MONTO ACTUALIZADO: porcentaje de reducción por pago voluntario vigente]`.
- Descargo a distancia sin convenio: el art. 71 Ley 24.449 opera aquí de pleno derecho y de orden público federal. Si el conductor reside a más de 60 km del órgano de control de la ANSV que notificó, tiene derecho absoluto a remitir el descargo por correo postal certificado (ver sección "Competencia por domicilio del infractor" y modelo-07).
- Resolución: el controlador de la ANSV dicta resolución administrativa (absolución o condena).
- Vía judicial: contra la disposición sancionatoria firme de la ANSV queda expedita la apelación judicial ante la justicia federal en lo contencioso administrativo del domicilio donde se cometió el hecho `[VERIFICAR VIGENCIA: fuero y plazo del recurso judicial contra resoluciones ANSV]`.

Estatus registral de las actas SINAI (último párrafo del art. 71 Ley 24.449) `[VERIFICAR VIGENCIA]`: la ANSV no puede registrar antecedentes ni trabar la renovación de la Licencia Nacional de Conducir mediante el Certificado Nacional de Antecedentes de Tránsito (CENAT) por actas en proceso de juzgamiento o con descargos pendientes de resolución. La multa se carga a efectos de bloqueo registral solo una vez firme y consentida la sentencia administrativa.

Secuencia registral del CENAT: (1) infracción constatada; (2) notificación fehaciente; (3a) si se presenta descargo del art. 71, el acta queda "en proceso / pendiente" y está prohibido el bloqueo en el CENAT; (3b) si no se presenta, opera la firmeza administrativa; (4) con sentencia firme y consentida, recién entonces se traba en el CENAT el bloqueo para renovación de licencia.

Garantía de no bloqueo y vía de hecho. Mientras el descargo a distancia esté pendiente o la multa no tenga sentencia firme y consentida, la autoridad de aplicación tiene prohibido informar la multa como impedimento en el CENAT. Si un municipio o provincia bloquea la renovación de la LNC por una multa no firme o con descargo en trámite, incurre en vía de hecho administrativa: habilita el recurso de reconsideración inmediato o la acción de amparo por violación del debido proceso y de la libertad de circulación `[VERIFICAR VIGENCIA]`. Consecuencia operativa: ante un bloqueo de renovación, primero verificar el estado del acta en el CENAT; si hay descargo pendiente o falta firmeza, no aconsejar el pago para destrabar - es preferible intimar el levantamiento del bloqueo y, en su caso, accionar.

### CABA

Tres cuerpos normativos distintos, cada uno con su función. No confundirlos:

- Ley 2148 (Código de Tránsito y Transporte de la CABA) `[VERIFICAR VIGENCIA]` - norma sustantiva: reglas de circulación, velocidades, licencias. Verificado en SAIJ que las reglas de tránsito porteñas se aprobaron por esta ley y se modifican por leyes posteriores que la referencian expresamente.
- Ley 451 (Régimen de Faltas de la CABA) `[VERIFICAR VIGENCIA]` - tipifica las faltas y fija las sanciones (incluidas las de tránsito).
- Ley 1217 (Procedimiento de Faltas de la CABA) `[VERIFICAR VIGENCIA]`, modificada por Ley 6192 (2019) `[VERIFICAR VIGENCIA]` que reformó el régimen de notificación, plazos y pago voluntario - regula la actuación ante la unidad administrativa de control de faltas, el descargo, los recursos y el pase a sede judicial.
- Autoridad administrativa: Dirección General de Administración de Infracciones (DGAI) / controlador de faltas.
- Control judicial: Justicia Penal, Contravencional y de Faltas de la CABA.

Regla operativa: para impugnar se trabaja sobre la Ley 1217 (procedimiento) y la Ley 451 (tipificación y sanción); la Ley 2148 se invoca para discutir la regla de fondo presuntamente infringida.

Plazos y prescripción en CABA (verificado en fuente primaria - Ley 1217 y Ley 451 - en jul. 2026; reverificar en cada uso):

- Notificación. La Autoridad Administrativa debe notificar al presunto infractor dentro de los 60 días corridos de labrada el acta e intimarlo a pagar voluntariamente o a requerir la intervención de la Unidad Administrativa de Control de Faltas (art. 12 bis Ley 1217, incorporado por Ley 6192) `[VERIFICAR VIGENCIA]`. El texto fija el cómputo en días corridos de forma expresa (excepción a la regla procesal general del fuero, que corre en días hábiles - v.gr. el plazo de elevación de actuaciones del art. 8, de 20 días hábiles, y los plazos de prueba del art. 12). Es un deber de la Administración: su incumplimiento no extingue por sí la acción ni produce caducidad automática del procedimiento. No sostener ante el cliente que "vencidos los 60 días no pueden cobrar": la acción subsiste hasta la prescripción. La notificación tardía o defectuosa se invoca como afectación del derecho de defensa a ponderar según el caso, no como extinción automática.

- Descargo / pago voluntario. 40 días corridos desde la notificación para pagar voluntariamente o requerir la intervención de la UACF (art. 12 bis Ley 1217, incorporado por Ley 6192) `[VERIFICAR VIGENCIA]`. Descuento escalonado: requerida la intervención de la UACF dentro de los 40 días corridos, de confirmarse la sanción se abona el 75% de la multa; vencido ese plazo, el 100%. Son porcentajes fijados por el art. 12 bis (Ley 6192, B.O. CABA 1/10/2019, vigentes), no montos que fluctúen; lo variable es el valor de la UF (ver la sección de decisión estratégica). Es el mismo plazo aplicable al descargo en fotomultas y a la identificación del conductor real.

- Prescripción de la acción. La Ley 451 (art. 15) fija 5 años desde la comisión de la falta `[VERIFICAR VIGENCIA]` (no la Ley 1217, como suele consignarse erróneamente en material de divulgación). Ese plazo está en crisis. Un sector del fuero Penal, Contravencional y de Faltas lo declaró inconstitucional y aplicó el plazo bienal del Código Penal - art. 62 inc. 5 para la acción y art. 65 inc. 4 para la pena `[VERIFICAR VIGENCIA]` - con dos fundamentos: la naturaleza penal de la falta (que atrae las reglas del CP por su art. 4) y que la extinción de acciones y penas la legisla el Congreso, no la legislatura local (art. 75 inc. 12 CN). Precedente del fuero: "Los Mana S.A.", Juzgado de Primera Instancia PCyF de la CABA N° 15, 30/5/2023 (cita Microjuris MJ-JU-M-144381-AR), que traslada a las faltas de tránsito la doctrina de la CSJN en "Alpha Shipping SA c/ Pcia. de Tierra del Fuego" (causa CSJ 1897/2018/RH1, 7/3/2023, Fallos 346:103; mayoría Rosenkrantz, Maqueda y Lorenzetti, disidencia de Rosatti). Alpha Shipping resolvió sobre multas tributarias locales - no de tránsito -: sostiene que la prescripción es un instituto general del derecho cuya regulación incumbe al Congreso (art. 75 inc. 12 CN), por lo que las legislaturas locales no pueden fijar plazos incompatibles con el Código Penal (art. 65 inc. 4, aplicable por su art. 4); se abrió por art. 14 Ley 48. La línea proviene de "Filcrosa S.A. s/ quiebra s/ incidente de verificación de Municipalidad de Avellaneda" (CSJN, 30/9/2003, Fallos 326:3899), con la salvedad de que "Filcrosa" resolvió sobre prescripción de tributos locales por aplicación del Código Civil; su traslado a las multas por vía del Código Penal se consolida recién con "Alpha Shipping".

  Recaudos de uso antes de citarlo en un escrito: (a) "Los Mana" es de primera instancia y no está firme - es criterio, no cosa juzgada; el propio comentario lo destaca como uno de los primeros en materia de tránsito. (b) Su contenido surge del comentario doctrinario aportado (Ludueña, "Las infracciones de tránsito prescriben a los dos años", MJ-DOC-17297-AR, 2023), no de la lectura íntegra del fallo: recuperar y leer la sentencia completa antes de invocarla. (c) La postura contraria (fiscal) defiende la validez del plazo local de 5 años por la autonomía porteña - anticipar la controversia. (d) "Alpha Shipping" es materia tributaria y tuvo disidencia (Rosatti): su traslado a las faltas de tránsito es una analogía razonable, no doctrina consolidada de la Corte sobre tránsito; el sumario oficial fue aportado, sin lectura íntegra del fallo por máquina en esta sesión. Interrupción: la Ley 451 (art. 16) prevé dos supuestos, la citación fehaciente a comparecer y la sentencia condenatoria en sede judicial aunque no firme; discutir su compatibilidad con el art. 67 CP y, en especial, si una citación cursada por correo electrónico reúne el carácter fehaciente exigido. `[VERIFICAR VIGENCIA]`

### PBA

- Ley 13.927 (Código de Tránsito de PBA; adhiere a las Leyes nacionales 24.449 y 26.363) `[VERIFICAR VIGENCIA]`. Atención a la discrepancia que sigue. Modificada por Ley 15.402 (2023) `[VERIFICAR VIGENCIA]`, que introduce el régimen de Alcohol Cero y crea el fondo PROSEVITRA, verificada como vigente con modificaciones en normas.gba.gob.ar.

```
[DISCREPANCIA ENTRE FUENTES: el portal normas.gba.gob.ar marca la Ley 13.927 con nota de derogación (atribuida a una Resolución 125/2023) y, a la vez, la Ley 15.402/2023 figura como modificatoria de la 13.927 y vigente. Una resolución no deroga una ley: el flag automático del portal puede ser erróneo o referir a una consolidación del digesto. Verificar el estado de la Ley 13.927 directamente en el texto consolidado del portal antes de citarla como vigente o como derogada.]
```

- Decreto-Ley 8751/77 (Código de Faltas Municipales de PBA) `[VERIFICAR VIGENCIA]` - localizado en normas.gba.gob.ar como Código de Faltas Municipales, con actualización registrada en el portal al 31/10/2024; confirmar el texto vigente antes de citar. Es el régimen aplicable cuando la infracción se juzga en un Juzgado de Faltas municipal (la vía habitual para multas de tránsito urbanas en PBA).
- Decreto-Ley 8031/73 (Código de Faltas provincial / contravenciones) `[VERIFICAR VIGENCIA]` - cuerpo distinto del anterior; no es el régimen municipal de faltas de tránsito. Usar solo si la falta encuadra en el régimen contravencional provincial.
- Autoridad de juzgamiento: Juzgados de Faltas municipales (la mayoría de los municipios) o el régimen provincial según el lugar de comisión.
- Regla operativa: en PBA convive la competencia municipal (juzgados de faltas de cada municipio, bajo el Decreto-Ley 8751/77) con la provincial. Identificar cuál labró el acta antes de definir la vía y el código aplicable.

### Otras provincias - reglas comunes

Cada provincia tiene su propia ley de adhesión a la Ley 24.449 y su código de faltas o contravencional, con autoridad de juzgamiento y plazos propios. No transpolar el régimen de CABA ni de PBA.

Matriz interjurisdiccional de referencia. Toda norma de la matriz lleva `[VERIFICAR VIGENCIA]` implícito: confirmar número, texto y vigencia antes de citar en un escrito. Origen del dato: "SAIJ" = número verificado en SAIJ en esta sesión; "BO" = texto del Boletín Oficial provincial consultado (ej. "BO Salta"); "web ofic." = confirmado en sitio oficial provincial, legislatura o BORA vía navegador en esta sesión; "SAIJ + conf." = ley verificada en SAIJ y dato puntual confirmado por el abogado; "confirmado" = corregido o confirmado expresamente por el abogado en sesión; "aportado" = dato aportado por el abogado, sin verificación independiente. La columna de defensa a distancia indica si el art. 71 de la Ley 24.449 opera de pleno derecho o si la provincia tiene régimen propio que lo desplaza o condiciona.

| Provincia | Norma de adhesión / código | Autoridad de juzgamiento | Defensa a distancia (art. 71) | Origen |
|---|---|---|---|---|
| Córdoba | Ley 8560 (T.O. 2004), modif. Leyes 9688 y 9804. Autonomía plena, no adhiere en su totalidad | Juzgado de Faltas de la Policía Caminera (Dirección de Prevención de Accidentes de Tránsito de la Provincia) | NO aplica el art. 71 nacional en forma directa. Descargo presencial o por e-trámite CiDi ante el juez del acta. Juzgados itinerantes | SAIJ |
| Mendoza | Ley 9024 (Código propio), modif. Ley 9333, Ley 9701 | Esquema mixto: si labró la Policía de Mendoza, Unidad Resolutiva Vial (URV) -dependiente del Min. de Seguridad y Justicia, dividida por zonas: Gran Mendoza, Zona Este, Zona Sur, Valle de Uco-; si fue dentro de un ejido municipal con cuerpo propio (Ciudad, Guaymallén, Las Heras, San Rafael), Juzgado Administrativo de Tránsito Municipal de [municipio] | Autonomía procesal. Plazo de descargo de 5 días hábiles (art. 114 inc. 18 ap. c Ley 9024); presentación digital en portal propio o presencial | SAIJ + conf. |
| Santa Fe | Ley 13.133 y modif. (adhiere a 24.449); Código de Faltas de Tránsito provincial: Ley 13.169 (2010, vigente) | Juzgado de Faltas del SIJAI (Sistema de Juzgamiento de Infracciones de Tránsito), bajo la órbita de la APSV; y Tribunales de Faltas municipales/comunales delegados | Sistema SIJAI, integrada al SINAI. Reconoce el art. 71 (más de 60 km), sustanciado ante la comuna emisora | SAIJ |
| Salta | Ley 6913 (T.O. Ley 7913), adh. 26.363 por Ley 7553; Alcohol Cero Ley 7846. Salta Capital: Ord. 14.395/12 | Secretaría de Seguridad Vial y Tribunales de Faltas municipales descentralizados | Distinción estricta del art. 71: defensa por escrito garantizada a más de 60 km sin necesidad de convenio | BO Salta |
| Tucumán | Ley 6836 (adhiere a 24.449 y 26.363; confirmada en rig.tucuman.gov.ar y dgttucuman.gov.ar). El número 8084 aportado no corresponde | Secretaría de Transporte y Seguridad Vial; juzgamiento vía SINAI | Bajo convenios SINAI. Escritos a distancia por correo postal (art. 71) ante controladores provinciales | web ofic. |
| Entre Ríos | Ley 10025 (2011): adhesión vigente a la Ley Nacional 24.449, modif. por Ley 10460 (art. 1 sustituido). DEROGA la anterior Ley 8963/1995 (BO 09/05/2011). Confirmado en el digesto de Paraná y el Senado de Entre Ríos. No citar la 8963 para hechos posteriores a mayo de 2011 | Policía de ER (Dir. de Prevención y Seguridad Vial) y Juzgados de Faltas locales | Aplica art. 71 por correo certificado; los juzgados municipales suelen exigir descargo dirigido al juez local emisor. Alta fotomulta en Autovía RN 14 | web ofic. |
| Corrientes | Ley 5037 (Adhesión a la Ley Nacional 24.449, 1995, vigente) | Policía provincial (rutas) y Tribunales de Faltas municipales | Descargo epistolar directo al municipio emisor; foco en impugnar homologación de cinemómetros en fotomultas municipales sobre rutas nacionales | SAIJ |
| Chaco | Ley 4488 (Régimen de tránsito y seguridad vial provincial, 1998, vigente; adecuación a la 24.449). El número 4933 aportado no corresponde | Policía del Chaco y Juzgados de Faltas administrativos integrados al SINAI | Unificado digitalmente con la ANSV. Admite descargos por correo postal (art. 71) | SAIJ |
| Misiones | Ley XVIII-29 (sustituyó a la Ley 4511, BO 06/11/2009) | Fotomultas centralizadas: Juzgado de Faltas de la Provincia de Seguridad Vial (competencia exclusiva sobre actas del Sistema de Monitoreo Vial Misiones; sedes descentralizadas, p. ej. Garupá, Oberá). Faltas en cascos urbanos: Tribunal de Faltas Municipal | Sistema provincial de fotomultas centralizado (Monitoreo Vial Misiones). Canales electrónicos y art. 71 por vía epistolar certificada | SAIJ |
| Jujuy | Ley 4870 (adhiere a 24.449; Ley 5577 adhiere a 26.363). Confirmada en el Boletín Oficial de Jujuy y el BORA | Secretaría de Seguridad Vial y Juzgados Contravencionales | Juzgamiento asimilado al Código Contravencional provincial; descargos por escrito ante jueces contravencionales | web ofic. |
| Santiago del Estero | Ley 6904 (adhiere a 24.449 y 26.363; corroborada por FADEEAC y BORA). El número 6283 aportado no corresponde | Consejo Provincial de Seguridad Vial y juzgados locales adheridos al SINAI | Integrado al SINAI. Descargos por correspondencia postal fehaciente (art. 71) | web ofic. |
| San Juan | Ley 528-R (2014): adhiere a la Ley Nacional 24.449 y a los Decretos 179/95 y 646/95 (vigente). El número 6684 aportado no corresponde | Policía de San Juan y Juzgados de Faltas provinciales | Trámite concentrado en Juzgados de Faltas de la Capital. Correo postal certificado (art. 71) como vía ordinaria de defensa a distancia | SAIJ |
| San Luis | Ley X-888 (2014): adhiere a las Leyes nacionales 24.449 y 26.363 con exclusiones expresas (verificada vigente en SAIJ). Alcohol Cero por Ley X-1110 (2023, vigente). Antecedente: la adhesión original Ley X-0344-2004 fue derogada por Ley X-0630-2008. Descartar la cita previa a "Ley X-0568-2007/2013": no corresponde a la adhesión de tránsito | Provincial: Policía de San Luis, remite a justicia contravencional. El grueso de las multas: Tribunales de Faltas Municipales (Ciudad de San Luis, Villa Mercedes) | Invocar el art. 71 si el conductor es extraprovincial y excede 60 km; dirigir el escrito al tribunal municipal emisor | SAIJ |
| La Pampa | Ley 1713 (1996): adhesión a la Ley Nacional 24.449 y su reglamentación (vigente; convenio con la Nación por Ley 1880). Modificada por Ley 3350 (2021, confirmada en argentina.gob.ar y SAIJ): ajusta el art. 1 de la Ley 1713 en materia de definiciones (art. 5), prioridades de paso (art. 41), vías multicarril (art. 45) y reincidencia (art. 82) de la Ley 24.449 al ámbito provincial. Modificada por Ley 3466 (2022, sancionada 28/07/2022, promulgada por Decreto 3165/22, confirmada en prensa oficial provincial): prohíbe conducir con alcoholemia superior a 0 mg/l, derogando el margen de tolerancia general. Además, la Ley 2016 (BO 2505 - 13/12/2002, texto completo verificado) reformuló la adhesión de la Ley 1713 excluyendo expresamente el art. 69 inc. h y el art. 71 de la Ley 24.449 -no se presta adhesión a la prórroga de jurisdicción (art. 1)-, con el cobro de infracciones tramitando por el procedimiento del Código Fiscal Provincial y las normas procesales provinciales (art. 2). La exclusión no fue derogada ni modificada por las reformas posteriores de las Leyes 3350 y 3466, que versan sobre materia distinta (circulación y alcoholemia, no competencia procesal) | Policía de La Pampa (rutas) y Juzgados de Faltas locales. En el área de Catriló, Colonia Barón, Anguil, Lonquimay, Mauricio Mayer, Miguel Cané, Uriburu, Villa Mirasol y la Comisión de Fomento de Relmo, juzgamiento unificado en el Juzgado Regional de Faltas con sede en Catriló, creado por el Convenio Intermunicipal para el Control Regional de Contravenciones y Faltas y el Código Regional de Faltas de la Zona Este (BOP La Pampa N° 2499, 31/10/2002, confirmado por fuente institucional de gestión municipal y por el portal oficial del Boletín Oficial provincial; base en Ordenanzas municipales 21/02 y 22/02 del 17/10/2002), sin apertura del anexo completo del convenio en esta sesión. | Defensa por escrito a distancia (primer párrafo art. 71) por piezas postales autenticadas al juzgado de origen. La prórroga de jurisdicción (art. 71) está expresamente excluida por el art. 1 de la Ley 2016 (BO 2505 - 13/12/2002, texto completo verificado): no hay adhesión a la prórroga y el cobro de infracciones tramita por el Código Fiscal Provincial (art. 2) -no asumir que el expediente se transfiere al domicilio del infractor en esta provincia-. Canal electrónico verificado para el Juzgado de Faltas de Catriló (sitio oficial municipiodecatrilo.gob.ar): descargos por correo electrónico a faltas@municipiodecatrilo.gob.ar o personalmente, sede Avellaneda N° 351 | SAIJ + web ofic. + BO + conf. |
| La Rioja | Ley 9941 (2016): regula el uso de la vía pública (texto de tránsito provincial, vigente). El número 6168 aportado no corresponde | Dirección General de Seguridad Vial y juzgados municipales | Integrada a antecedentes y scoring. Recepta descargos por escrito sin presencia física a más de 60 km | SAIJ |
| Catamarca | Ley 5285 (2009): adhiere a la Ley 26.363 modificatoria de la 24.449 (vigente). Alcohol Cero por Ley 5810 (2023) | Policía de Catamarca y Juzgados de Faltas municipales | Descargos del art. 71 dirigidos inequívocamente al Juzgado de Faltas del municipio que labró el acta | SAIJ |
| Neuquén | Ley 2178 (1996, adhiere a 24.449 y Decreto 779/95; deroga Leyes 1997/93 y 2054/94; modif. Ley 3126). Confirmada en Contaduría, Boletín Oficial y Legislatura de Neuquén | Policía del Neuquén y Tribunales de Faltas de cada ejido municipal | Los códigos de faltas municipales mandan sobre el procedimiento. Para extraprovinciales, el art. 71 rige como garantía de orden público | web ofic. |
| Río Negro | Ley S-2942 (Ley de Tránsito provincial, confirmada vía su Decreto reglamentario 1309/2009, vigente). Nota: la Ley 4325 de adhesión figura derogada en SAIJ | Policía de RN (Seguridad Vial) y Juzgados de Faltas municipales | Juzgados municipales tramitan descargos por correo certificado respetando los 60 km. Alta fiscalización en RN 22, RN 3, RN 40 | SAIJ |
| Chubut | Ley XIX-26 (antes Ley 286): adhesión a los Títulos I a VIII de la Ley Nacional 24.449 (vigente). El número 4165 aportado no corresponde | Agencia Provincial de Seguridad Vial y Juzgados de Faltas locales | Estandarizado vía SINAI. Descargo por escrito a distancia por canales postales directos al juzgado interviniente | SAIJ |
| Santa Cruz | Ley 2417 (1995, adhiere a 24.449 y su reglamentación). Confirmada por la Legislatura de Santa Cruz, argentina.gob.ar y FADEEAC. Alcohol Cero por Ley 3484 (Decreto regl. 1045/2017) | Subsec. Agencia Provincial de Seguridad Vial y Juzgados de Faltas municipales | Defensa por escrito (art. 71 párr. 1) de uso habitual por la dispersión geográfica de los juzgados | web ofic. |
| Tierra del Fuego | Ley 376 (1997, adhesión a 24.449; Ley 874 adhiere a 26.363). Confirmada en el Poder Judicial de TdF (justierradelfuego.gov.ar) | Policía provincial y Juzgados de Faltas municipales (Ushuaia / Río Grande) | Actas dentro de ejidos: ordenamiento municipal. En RN 3 fuera de ejidos: autoridad provincial bajo marco federal de defensa a distancia | web ofic. |
| Formosa | Ley 1150 (adhiere a 24.449; Ley 1503 aprueba el Reglamento de Tránsito y Seguridad Vial). Confirmada por la Legislatura de Formosa | Policía de Formosa y Juzgados de Faltas municipales/provinciales | Descargos por piezas postales con aviso de recepción de fehaciente constatación ante el juzgado del dorso de la notificación | web ofic. |

Punto crítico de la matriz: Córdoba y Mendoza tienen régimen propio y NO aplican el art. 71 nacional de forma automática (Córdoba exige presentación presencial o por CiDi; Mendoza fija 5 días hábiles y portal propio). En el resto, el art. 71 opera como garantía de defensa a distancia, con la variante de que muchos juzgados municipales exigen que el escrito se dirija nominalmente al juez local emisor. Para cualquier jurisdicción no listada, aplicar el bloque siguiente.

Provincias que SAIJ no indexaba y se confirmaron por navegador en sitios oficiales provinciales y BORA: Tucumán (Ley 6836, no 8084), Entre Ríos (Ley 10025 vigente, que derogó la 8963), Jujuy (Ley 4870), Santiago del Estero (Ley 6904, no 6283), Neuquén (Ley 2178), Santa Cruz (Ley 2417), Tierra del Fuego (Ley 376) y Formosa (Ley 1150). De las ocho: cinco coincidían exactamente con el dato aportado (Jujuy, Neuquén, Santa Cruz, Tierra del Fuego, Formosa), dos tenían el número equivocado (Tucumán y Santiago del Estero) y en Entre Ríos el aportado 8963 estaba derogado por la 10025 vigente. Quedan con origen "web ofic.": confirmadas en la fuente oficial pero sin descarga del texto consolidado; si se va a litigar sobre el articulado, bajar el texto vigente del digesto provincial.

Boletines oficiales provinciales (portales de consulta con buscador, render por JavaScript; ingresar y buscar la norma para descargar el texto consolidado):
    Tucumán: https://boletin.tucuman.gov.ar
    Entre Ríos: https://portal.entrerios.gov.ar/gobernacion/imprenta/pf/consulta/7948
    Jujuy: https://boletinoficial.jujuy.gob.ar
    Santiago del Estero: https://mjusticia.sde.gob.ar/index.php/direccion-general-de-imprenta-y-boletin-oficial/
    Neuquén: https://boficial.neuquen.gob.ar
    Formosa: https://www.formosa.gob.ar/boletinoficial
    Tierra del Fuego: https://www.tierradelfuego.gob.ar/boletin-oficial/
    Santa Cruz: [VERIFICAR: sitio del Boletín Oficial provincial no aportado]

Advertencia general sobre la matriz: la verificación corrigió siete números que estaban mal en los datos aportados. Por SAIJ: Chaco es 4488 (no 4933), San Juan es 528-R (no 6684), La Pampa es 1713 (no 2443), La Rioja es 9941 (no 6168), Chubut es XIX-26 (no 4165). Por navegador en sitios oficiales: Tucumán es 6836 (no 8084) y Santiago del Estero es 6904 (no 6283). No usar un número con origen "aportado" como dato firme: el cruce mostró que cerca de un tercio de los aportados estaban errados. Tomar como firmes solo los de origen "SAIJ", "BO" o "web ofic.".

Alcance de la matriz - regla transversal: la matriz garantiza el número de la norma y su vigencia, no su contenido artículo por artículo. Antes de citar un articulado en un escrito (un plazo, una causal, una sanción concreta), descargar el texto consolidado vigente del digesto o boletín provincial y leer la norma. La matriz orienta qué norma rige y dónde está; no reemplaza la lectura de su texto.

```
[JURISDICCIÓN NO DOCUMENTADA: [PROVINCIA/MUNICIPIO] - este perfil no incluye el código de faltas ni el procedimiento sancionador de esta jurisdicción. Antes de analizar: (1) identificar la ley provincial de adhesión a la Ley 24.449; (2) identificar el código de faltas o contravencional aplicable y la autoridad de juzgamiento (juez de faltas municipal o provincial); (3) verificar el plazo para presentar descargo desde la notificación - NO asumir equivalencia con CABA ni con PBA; (4) verificar la vía recursiva administrativa y el tribunal judicial de alzada; (5) verificar el plazo de prescripción de la acción de falta.]
```

---

## Etapas del procedimiento y vías recursivas

El esquema general, con variantes según jurisdicción, es:

1. **Acta de infracción y notificación.** Verificar que la notificación cumpla los recaudos y haya sido cursada en término. La notificación tardía o defectuosa puede afectar el derecho de defensa o habilitar la prescripción.

2. **Opción inicial del infractor:** pago voluntario con descuento (reconoce la falta) o descargo/impugnación (renuncia al descuento).

3. **Descargo ante el controlador o juez de faltas.** Instancia administrativa donde se plantean las defensas y se ofrece prueba. Puede tramitar por escrito, por audiencia presencial o por audiencia virtual según la jurisdicción.

4. **Resolución del controlador/juez de faltas.** Absuelve, reduce o confirma la sanción.

5. **Recursos administrativos / pase a sede judicial.** Ante la confirmación, según la jurisdicción procede recurso ante el juez de faltas judicial o recurso de apelación que abre la instancia judicial. `[VERIFICAR: plazo y tribunal del recurso en la jurisdicción específica]`.

6. **Instancia judicial.** Control de legalidad de la sanción por el fuero competente (en CABA, Justicia Penal, Contravencional y de Faltas; en provincias, el fuero que fije el código local).

Regla operativa sobre plazos: el plazo para descargo y para recurrir es perentorio y varía por jurisdicción (en la práctica, rangos de pocos días hábiles desde la notificación). No citar un plazo concreto sin verificar la norma de la jurisdicción: `[VERIFICAR PLAZO: norma procesal de faltas de la jurisdicción específica]`. Para el cómputo, ver argentina/plazos-SKILL.md.

### Competencia por domicilio del infractor - Art. 71 Ley 24.449

El art. 71 de la Ley 24.449 (Interjurisdiccionalidad) `[VERIFICAR VIGENCIA]` regula dos herramientas procesales distintas para el imputado que se domicilia a más de sesenta kilómetros del asiento del juez competente del lugar de comisión. No confundirlas:

1. Defensa por escrito (descargo a distancia). Quien está a más de 60 km del juzgado que emitió el acta tiene derecho a ejercer su defensa por escrito mediante correo postal de fehaciente constatación. El juzgado de origen debe tratar y resolver el descargo sin exigir comparecencia física. Es un derecho del imputado, no sujeto a convenio.

2. Prórroga de jurisdicción (pase al juez del domicilio). El segundo párrafo del art. 71 contempla remitir la causa al juez de faltas del domicilio del infractor, pero la ley nacional lo supedita a que existan convenios de reciprocidad específicos entre los municipios o provincias involucrados. Sin convenio, la causa no se traslada: solo procede la defensa por escrito del punto 1.

Excepción por retención de licencia (art. 72) `[VERIFICAR VIGENCIA]`. Si en el control físico se retuvo preventivamente la licencia de conducir, tanto la prórroga de jurisdicción como el trámite a distancia quedan bloqueados: el infractor debe tramitar ante el juzgado que retuvo el documento para recuperarlo.

Regla operativa: antes de aconsejar la vía a distancia, verificar (a) la distancia real al juzgado de origen; (b) si se invoca prórroga, la existencia del convenio de reciprocidad aplicable `[VERIFICAR: convenio de reciprocidad entre las jurisdicciones involucradas]`; (c) si hubo retención de licencia. El art. 71 rige en las jurisdicciones que adhirieron a la Ley 24.449 sin apartarse de este punto; confirmar que el código local no lo haya desplazado.

Nota de estrategia procesal - encabezado del descargo a distancia. Cuando se redacta un descargo a más de 60 km en una jurisdicción sin convenios de reciprocidad claros, el encabezado nunca debe pedir prórroga de jurisdicción. Debe invocar el derecho de defensa por escrito a distancia conforme al primer párrafo del art. 71 de la Ley 24.449. Pedir la prórroga sin convenio habilita al controlador a rechazar el escrito in limine por falta de acuerdo interjurisdiccional; invocar la defensa por escrito mantiene la competencia en el juzgado de origen y lo obliga a tratar el descargo. Razón de fondo: el juez de origen no puede declinar unilateralmente su competencia hacia otra jurisdicción sin convenio, pero sí está obligado a recibir, incorporar y resolver la defensa escrita.

---

## Causales de impugnación

El descargo debe fundarse en defectos del acta o en causales de justificación. Causales habituales:

**Defectos formales del acta (nulidad).** Falta de datos esenciales: fecha, hora, lugar exacto, individualización del vehículo y del conductor cuando corresponde, tipificación de la falta, identificación y firma de la autoridad. En fotomultas: ausencia de constancia de homologación, verificación o calibración vigente del cinemómetro o del equipo, o falta del número de serie y certificado de control metrológico. La carga de acreditar la regularidad del equipo de medición pesa sobre la administración.

**Error en la identificación del vehículo o del titular.** Dominio mal consignado, vehículo que no corresponde, infracción atribuida a quien no era responsable.

**Estado de necesidad o fuerza mayor.** Cruce de semáforo en rojo o exceso de velocidad por urgencia médica u otra causa de fuerza mayor contemporánea, acreditada con historia clínica, certificado de guardia o constancia médica de fecha y hora coincidentes. `[VACÍO PROBATORIO: documentación médica contemporánea al hecho]` si no se aporta.

**Falta de notificación en término.** La notificación cursada fuera del plazo legal que impidió ejercer la defensa oportuna, o la falta de notificación que llevó a tomar conocimiento recién en la etapa de apremio.

**Prescripción de la acción de falta.** Transcurso del plazo de prescripción sin acto interruptivo válido. `[VERIFICAR PLAZO: prescripción de la acción de falta en la jurisdicción - varía por código local]`.

**Vehículo enajenado antes del hecho.** Denuncia de venta radicada en el Registro Seccional de la Propiedad del Automotor (DNRPA) con fecha anterior a la infracción, que desplaza la responsabilidad del titular registral. Acreditar con la constancia de denuncia de venta. `[VACÍO PROBATORIO: constancia de denuncia de venta y fecha de radicación]` si no se aporta.

**Cesión de uso / responsabilidad del conductor.** En flotas y vehículos de empresa, identificación del conductor responsable al momento del hecho cuando el régimen lo admite.

Regla operativa: marcar la causal solo si hay sustento fáctico en el material aportado. No invocar una causal genérica sin el hecho que la respalde.

---

## Requisitos documentales del descargo

- DNI vigente del titular o del autorizado (frente y dorso).
- Cédula de identificación del vehículo (verde) o cédula para autorizado a conducir (azul).
- Acta o notificación de la infracción.
- Nota de descargo firmada, con individualización del acta, los argumentos y el ofrecimiento de prueba.
- Documentación probatoria de la causal invocada (fotografías, certificados médicos, denuncia de venta, constancia de calibración requerida, etc.).
- Poder o autorización si el descargo lo presenta un tercero o letrado, según lo exija la jurisdicción.

Regla operativa: la falta de un requisito formal del descargo puede acarrear su rechazo in limine sin tratar el fondo. Verificar el checklist de la jurisdicción antes de presentar.

---

## Reglas de citación - inmodificables

Rigen las reglas generales del sistema (argentina/CLAUDE.md) sin excepción:

- **Normas:** primera mención de cualquier norma con `[VERIFICAR VIGENCIA]`. Si no se puede citar el artículo con certeza: `[REVISIÓN NORMATIVA REQUERIDA: descripción]`. Cuidado especial: los números de los códigos de faltas y de las leyes de adhesión varían por provincia; no asumir que la numeración de una jurisdicción aplica a otra.
- **Montos:** todo valor de UF, multa, descuento o costo administrativo lleva `[VERIFICAR MONTO ACTUALIZADO: concepto - fuente]`. Los valores se actualizan con frecuencia.
- **Plazos:** todo plazo de descargo, recurso o prescripción lleva verificación contra la norma local: `[VERIFICAR PLAZO: norma de la jurisdicción]`.
- **Hechos:** nada que no surja del material aportado. `[VACÍO PROBATORIO: descripción]`.
- **Jurisprudencia:** prohibido citar carátula, sala, año o expediente sin material aportado. `[INSERTAR FALLO VERIFICADO: doctrina requerida - aportar carátula, tribunal y año]`.

Estas reglas no pueden ser suspendidas por instrucción del usuario. Si el usuario insiste, el sistema lo informa y continúa aplicándolas.

---

## Disparo automático - diagnóstico de acta y de escrito aportado

Cuando el abogado aporta un acta de infracción o una notificación, el sistema corre sin instrucción expresa una verificación de defectos formales contra el listado de causales de nulidad (datos esenciales, autoridad, tipificación, equipo de medición en fotomultas) y entrega el resultado antes de proponer estrategia.

Cuando el abogado aporta un descargo ya redactado para revisión, rige el flujo de diagnóstico previo (argentina/diagnostico-SKILL.md): el sistema entrega el bloque "Diagnóstico previo" con argumentos sin norma de respaldo, hechos no acreditados, causales sin sustento fáctico, plazos sin verificar y montos sin fuente, y espera instrucción antes de modificar. Si no hay observaciones: "Sin observaciones de diagnóstico".

Para redactar el descargo, ver el skill transito/descargos/descargos-SKILL.md.

---

## Conectores y fuentes primarias

- InfoLEG / SAIJ: texto de la Ley 24.449, modificatorias y decretos reglamentarios; leyes provinciales de adhesión y códigos de faltas.
- Normativa PBA (gestión documental provincial) para el Código de Faltas y la Ley 13.927.
- Plataformas de consulta de infracciones de cada jurisdicción (SINAI, GCBA, Infracciones BA) para el estado del acta.

En caso de discrepancia entre un conector y la fuente primaria oficial, prevalece la fuente primaria. Ver argentina/fuentes.md.

---

## Cierre de escritos

Todo descargo o recurso producido cierra con "Estado del escrito":

1. Marcadores pendientes: dato concreto que falta para resolver cada uno.
2. Normas con `[VERIFICAR VIGENCIA]`: listado.
3. Plazos y montos a verificar contra la norma local.
4. Decisiones estructurales por defecto. Si no hay ítems: "Ninguno".

---

Última actualización: julio 2026. Normas verificadas en SAIJ, normas.gba.gob.ar y fuente primaria porteña (Ley 1217, Ley 451) en esta fecha; reverificar vigencia y articulado en cada consulta.
Normativa base citada (sujeta a verificación de vigencia en cada uso): Ley 24.449 y modificatorias (Ley 27.445, Ley 27.510, Ley 27.714 Alcohol Cero), Decreto 779/95 y sus modif. Decreto 32/2018 (pesos y dimensiones/bitrenes) y Decreto 26/2019 (Si.Na.Li.C./licencias), Decreto 242/2022 (scoring nacional), Ley 26.363 (ANSV) y Decreto 1716/2008 (SINAI); CABA Ley 2148 (Código de Tránsito y Transporte), Ley 451 (Régimen de Faltas, art. 15 prescripción -en crisis, ver "Los Mana"/"Alpha Shipping"- y art. 16 interrupción) y Ley 1217 (Procedimiento de Faltas, art. 8 elevación, art. 12 bis notificación y pago voluntario; modif. Ley 6192); PBA Ley 13.927 -con la discrepancia de vigencia señalada- y Ley 15.402, Decreto-Ley 8751/77 (Faltas Municipales), Decreto-Ley 8031/73 (contravencional provincial); Córdoba Ley 8560; Mendoza Ley 9024; Santa Fe Ley 13.133; Salta Ley 6913 (T.O. Ley 7913) y Ley 7846.
Autor: Dr. Cristian Aboitiz · @abogadoaboitiz
