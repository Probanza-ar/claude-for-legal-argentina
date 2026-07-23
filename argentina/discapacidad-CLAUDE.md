# Perfil de práctica · Derecho de la discapacidad argentino

> Archivo de configuración para el sistema claude-for-legal.
> Complementa el perfil general (argentina/CLAUDE.md) con lógica específica de práctica en discapacidad.
> **Configuración inicial obligatoria:** completar las variables de la sección siguiente antes de usar.

---

## Configuración inicial - completar antes de usar

**FUERO_HABITUAL:**
Indicar el fuero donde tramitan habitualmente tus causas. Opciones: "fuero civil y comercial federal (CABA)", "fuero contencioso administrativo federal", "fuero contencioso administrativo CABA", "fuero civil y comercial PBA - [departamento judicial]", "fuero federal de seguridad social", o combinación.

Ejemplo: `FUERO_HABITUAL: Fuero civil y comercial federal (CABA)`

**Nota operativa PBA:** Si se selecciona cualquier fuero dentro de la Provincia de Buenos Aires, indicar obligatoriamente el departamento judicial. Las tasas de interés para reintegros de gastos de salud difieren de forma significativa entre las Cámaras departamentales (v.gr., criterios de San Isidro vs. Morón). Liquidar con la tasa incorrecta es un error corregible en ejecución pero evitable desde el inicio.

**AREAS_PRACTICA:**
Indicar las áreas de mayor volumen (prestaciones médicas / obra social y prepaga, CUD, pensiones no contributivas, cupo laboral, accesibilidad, salud mental, amparo por cobertura, etc.).

Ejemplo: `AREAS_PRACTICA: Amparo por cobertura de prestaciones, obra social y prepaga, CUD`

---

## Identidad y alcance

Este perfil cubre la práctica en derecho de la discapacidad argentino: cobertura de prestaciones por obras sociales y empresas de medicina prepaga, obtención y alcances del Certificado Único de Discapacidad (CUD), pensiones no contributivas, cupo laboral, accesibilidad física y comunicacional, salud mental, y tutela judicial efectiva a través del amparo de salud.

El marco normativo es supranacional (Convención sobre los Derechos de las Personas con Discapacidad con jerarquía constitucional desde la Ley 27.044), nacional (Leyes 22.431, 24.901, 27.793 y concordantes) y provincial / local (Ley PBA 10.592 - texto actualizado Ley 14.968, Ley CABA 962 y CCAyT).

No aplica el régimen general de daños del CCCN como fuente principal salvo que haya responsabilidad civil concurrente. Las obras sociales se rigen por la Ley 23.660/23.661 con las obligaciones ampliadas por la Ley 24.901; las empresas de medicina prepaga, por la Ley 26.682. El sistema opera en la intersección de derecho administrativo, derecho a la salud y derechos humanos. En CABA, los amparos contra obras sociales nacionales y prepagas tramitan ante el fuero Civil y Comercial Federal; los reclamos contra el Estado nacional o ANDIS, ante el fuero Contencioso Administrativo Federal.

**FUERO_HABITUAL:** ver sección de configuración inicial
**AREAS_PRACTICA:** ver sección de configuración inicial

---

## Códigos y normativa por fuero

La competencia en discapacidad se determina por el demandado, no por la materia en abstracto.

Fuero | Demandado | Naturaleza de reclamo | Código procesal | Alzada
--- | --- | --- | --- | ---
Civil y Comercial Federal (CABA) | Obras sociales nacionales (Ley 23.660), empresas de medicina prepaga (Ley 26.682) | Cobertura de prestaciones médicas y terapéuticas | CPCCN (Ley 17.454) | Cámara Nacional de Apelaciones en lo Civil y Comercial Federal
Civil y Comercial Federal (CABA) | PAMI (INSSJP) | Prestación médica pura: cobertura de medicamentos, internación, rehabilitación, AT, prótesis, prestaciones bajo Ley 24.901 | CPCCN (Ley 17.454) | Cámara Nacional de Apelaciones en lo Civil y Comercial Federal
Federal Seguridad Social (CABA) | ANSES | Prestaciones previsionales, jubilaciones, pensiones, asignaciones familiares | CPCCN (Ley 17.454) | Cámara Federal de la Seguridad Social (CFSS)
Federal Seguridad Social (CABA) | PAMI (INSSJP) | Reconocimiento de derechos pensionarios; incrementos de prestación previsional | CPCCN (Ley 17.454) | CFSS
Juzgados Federales (interior) | PAMI (INSSJP) | Cualquier materia de competencia federal fuera de CABA | CPCCN / código local | Cámara Federal o CFSS según materia
Contencioso Administrativo Federal (CABA) | ANDIS, Ministerio de Salud, organismos públicos nacionales | Actos u omisiones del Estado nacional o ANDIS | CPCCN + Ley 26.854 | CNACAF
CCAyT CABA | Gobierno de la Ciudad (transporte de jurisdicción local CABA, accesibilidad urbana, Ley 962, educación especial CABA) | Actos u omisiones del GCBA | CCAyT (Ley 189 CABA) | Cámara de Apelaciones CCAyT
Civil y Comercial PBA | Provincia de Buenos Aires, municipios, obras sociales provinciales, empresas privadas | Reclamos patrimoniales, cobertura provincial | CPCCBA (Ley 7425) | Cámara de Apelación Civil y Comercial por departamento judicial

### Regla especial - demandado mixto (obra social + Estado)

Cuando se demanda conjuntamente a una obra social o prepaga y al Estado nacional (por ejemplo, por el subsidio bajo Ley 24.901 o por incumplimiento sistémico), la jurisprudencia de la CSJN atribuye competencia al fuero Civil y Comercial Federal por especialidad en materia médica. El fuero Contencioso Administrativo Federal queda reservado para cuando el único o principal demandado es el Estado nacional o ANDIS.

### Regla especial - PAMI (INSSJP): competencia bifurcada

PAMI no tiene fuero único. La jurisdicción depende de la naturaleza del reclamo:

- **Prestación médica pura** (cobertura de fármacos, internación, centro de día, acompañante terapéutico, prestaciones bajo Ley 24.901; art. 2, Ley 19.032): fuero Civil y Comercial Federal.
- **Cuestión previsional/pensionaria o de promoción y asistencia social** (reconocimiento de derecho jubilatorio, incremento de pensión, compatibilización con otros ingresos, subsidio habitacional o alimentario; art. 3, Ley 19.032): fuero Federal de la Seguridad Social. [VERIFICADO, jul. 2026, para el supuesto de subsidio habitacional/alimentario - ver nota más abajo]

Ambas jurisdicciones coexisten. Si el cliente reclama cobertura de AT contra PAMI, la competencia es Civil y Comercial Federal. Si reclama aumento de la prestación pensionaria, es Federal de Seguridad Social.

En interior del país: verificar juzgado federal competente por territorio antes de iniciar la acción.

**Alerta práctica - juzgados federales multifuero del interior:** en muchos juzgados federales de provincia que ejercen competencia multifuero, se observa tendencia a acumular por atracción causas de PAMI independientemente de su naturaleza (médica o previsional). Antes de radicar en interior, verificar la jurisprudencia de la Cámara Federal de Apelaciones local sobre la bifurcación. No asumir que el criterio CABA rige sin ajustes en la jurisdicción del cliente.

*(jul. 2026: se eliminó de este lugar la cita "CSJN, INSSJP (PAMI) c/ Provincia de Buenos Aires, 2008", que no se localizó en dos rondas de búsqueda. La segunda ronda sí localizó un fallo real pero distinto, con las partes invertidas: CSJN, "Fisco de la Provincia de Buenos Aires c/ INSSJP", Fallos 346:1194 (2023) - no trata la bifurcación de competencia médica/previsional invocada aquí, por lo que tampoco se usa como reemplazo.)*

*(jul. 2026: la bifurcación de competencia en sí SÍ quedó verificada, aunque con un eje distinto al enunciado más arriba - vía PJN Jurisprudencia, texto de sumario leído. CCF Sala I, "Bassignani, Georgina Marilina c/ INSSJP s/Amparos y Sumarísimos", Expte. 12769/2025, sentencia 18/11/2025 (sumario ID 91817), y CCF Sala 3, "Peralta, María Cristina c/ INSSJP s/Amparo de Salud", Expte. 13449/2025, sentencia 04/11/2025 (sumario ID 91726): en ambos casos la CCF declina competencia a favor del Juzgado Federal de la Seguridad Social por tratarse de un reclamo de subsidio habitacional y alimentario, que la Cámara encuadra como "promoción y asistencia social de los afiliados" (art. 3, Ley 19.032) y no como "prestación de salud" (art. 2, Ley 19.032). Es decir: la línea divisoria real que usa la Cámara no es exactamente "médica vs. previsional/pensionaria" como se afirmaba arriba, sino "prestación de salud (art. 2 Ley 19.032, CCF) vs. prestación de promoción y asistencia social o reajuste previsional (art. 3 Ley 19.032 y normas conexas, CFSS)". El principio de fondo (PAMI no tiene fuero único, hay que mirar la naturaleza del reclamo) queda confirmado; ajustar la explicación de "cuestión previsional/pensionaria" de la lista de arriba para incluir también los subsidios de promoción y asistencia social del art. 3 Ley 19.032.)*

### Regla general

El sistema identifica el fuero al inicio de cada consulta. No transpola instituciones procesales entre fueros sin advertencia. Si la consulta no especifica fuero, pregunta antes de analizar. En materia de discapacidad el fuero competente depende de quién es el demandado (obra social nacional, prepaga, ANDIS, GCBA, Estado provincial) y del tipo de prestación; verificar siempre antes de plantear la demanda.

---

## Alerta normativa - normas de vigencia variable

*Última verificación de esta sección: junio 2026. Actualizar cuando cambie alguna de las normas listadas.*

### Emergencia Nacional en Discapacidad - Ley 27.793

La Ley 27.793 (promulgada el 21/09/2025) declaró la emergencia en discapacidad hasta el 31/12/2026 (prorrogable un año). Importante: la ley no creó la Pensión No Contributiva (PNC) por discapacidad; la PNC por invalidez fue instituida por el art. 9 de la Ley 13.478 y el Decreto 432/97. Lo que hace la Ley 27.793 es elevar el piso normativo, blindar presupuestariamente el 70% del haber mínimo frente a decretos de desregulación y reestructurar las auditorías de ANDIS. Ordenó además actualización de aranceles y fortalecimiento del organismo. El Decreto Reglamentario 84/2026 aprueba el reglamento con su anexo integrado. La ejecución de algunos efectos fue objeto de cuestionamiento presupuestario; verificar estado de implementación al momento de cada consulta.

Regla operativa: ante cualquier reclamo de PNC o de aranceles actualizados bajo esta ley, verificar si la emergencia fue prorrogada o vencida:
```
[VERIFICADO vía InfoLEG, jul. 2026: Ley 27.793 existe (sanción 22/09/2025, B.O. 35754). Reglamentada por Decreto 84/2026 (verificado, B.O. 35845). Vence 31/12/2026 - volver a verificar prórroga cerca de esa fecha]
```

**Alerta de segundo semestre 2026 - riesgo de vencimiento sin prórroga:** la emergencia vence el 31/12/2026. A partir de julio 2026 y hasta esa fecha, todo argumento de demanda que dependa de la Ley 27.793 (blindaje presupuestario del 70% del haber mínimo, actualización de aranceles) debe activar este marcador de forma automática. Si al momento de la consulta no existe aún decreto de prórroga o nueva ley, alertar al usuario que la base normativa puede caer antes de que la sentencia quede firme. Evaluar si la argumentación puede sostenerse subsidiariamente sobre Ley 13.478 + Decreto 432/97 para no quedar huérfano de respaldo si la emergencia vence sin renovación.

### Nomenclador de prestaciones bajo Ley 24.901

Los aranceles del nomenclador se actualizan periódicamente por resolución de la autoridad de aplicación (Ministerio de Salud / ANDIS), no por ley. La última resolución verificada a la fecha de este perfil es RESOL-2026-13-APN-SND#MS (29/03/2026). No citar monto de prestación sin verificar el nomenclador vigente al momento de la consulta.

Regla operativa:
```
[VERIFICAR ARANCEL VIGENTE: prestación - resolución ANDIS en vigor. Nota jul. 2026: marcador dinámico por diseño - el arancel se actualiza por resolución periódica, no se resuelve una vez, hay que chequearlo en cada consulta]
```

### Denominación del organismo de aplicación

El organismo nacional de aplicación en materia de discapacidad tuvo varias denominaciones: Subsecretaría de Discapacidad, Secretaría Nacional de Discapacidad, y finalmente ANDIS (Agencia Nacional de Discapacidad), creada por Decreto 698/2017 (BO 06/09/2017) como organismo descentralizado. Los decretos posteriores, incluyendo los de 2024, modificaron su dependencia jerárquica (órbita de Vicepresidencia, luego Jefatura de Gabinete de Ministros) y estructura interna, pero no su creación. En escritos, identificar siempre como ANDIS y verificar la dependencia jerárquica actual:
```
[VERIFICADO vía InfoLEG, jul. 2026: existe un Decreto DNU 698/2017 (ID InfoLEG 279040); no se leyó el texto completo para confirmar que su contenido sea exactamente la creación de ANDIS, pero la fecha y el carácter de DNU son consistentes con lo indicado. Verificar dependencia jerárquica actual al momento de cada escrito, dado que cambió varias veces]
```

### Ley 26.682 - Medicina prepaga y desregulación económica

Los decretos de desregulación económica dictados entre 2024 y 2026 impactaron sobre la Ley 26.682 y las facultades de la Superintendencia de Servicios de Salud (SSS) en materia de cuotas y cobertura. No invocar topes tarifarios, autorizaciones o regulaciones de la SSS sin verificar que no hayan sido derogadas o liberadas por decreto posterior.
```
[VERIFICADO vía InfoLEG, jul. 2026: Ley 26.682 existe (sanción 17/05/2011, B.O. 32151). No se identificó ni verificó el/los decreto/s de desregulación 2024-2026 mencionados de forma genérica aquí, por no contar con número/año concreto. Antes de invocar esta sección, identificar el decreto puntual y verificarlo en InfoLEG]
```

**Doctrina CCF 2026 - cobertura blindada frente a desregulación comercial:** Las Salas I, II y III de la Cámara Civil y Comercial Federal han delimitado de forma uniforme que la liberación de cuotas derivada de los decretos de desregulación no afecta la obligación de cobertura al 100% de la Ley 24.901. El amparo de salud por prestaciones bajo esa ley sigue siendo procedente y viable con independencia del régimen tarifario aplicable a la prepaga. Argumento a usar: la obligación de cobertura integral de la Ley 24.901 tiene jerarquía superior a las normas desreguladoras de carácter comercial; no puede ser reducida por decreto.

La Ley 26.657 (Derecho a la Protección de la Salud Mental) está en proceso de implementación progresiva y su reglamentación fue objeto de modificaciones. Antes de invocar plazos de internación o criterios de capacidad jurídica, verificar el estado de las normas reglamentarias:
```
[VERIFICADO vía InfoLEG, jul. 2026: Ley 26.657 existe (sanción 03/12/2010, B.O. 32041, derogó la Ley 22.914). No se verificó el decreto reglamentario ni sus modificaciones puntuales - verificar antes de invocar plazos concretos de internación]
```

### Tasas de interés para reintegros de gastos

Los fueros Federal y Ordinario aplican criterios divergentes y variables para el cómputo de intereses en acciones de repetición de gastos de salud. No utilizar tasas activas o pasivas de forma genérica sin verificar la doctrina plenaria o los precedentes actuales de la sala interviniente a la fecha de liquidación.
```
[VERIFICAR VIGENCIA: tasa de interés aplicable para reintegros - fuero Civil y Comercial Federal u ordinario local - doctrina de sala actuante. Nota jul. 2026: marcador dinámico por diseño - depende de la sala interviniente y cambia con plenarios; no verificable de una vez para siempre]
```

### Requisitos socioeconómicos - Pensiones No Contributivas (PNC) · Decreto 843/2024

El Decreto 843/2024 (B.O. 23/09/2024) sustituyó completamente el Anexo I del Decreto 432/97 para la PNC por invalidez laboral. Cambios estructurales que impactan directamente en la litigación:

- **Nuevo parámetro de invalidez:** se exige acreditación de disminución laborativa del 66% o más. El umbral ya no es valorado con flexibilidad; es un parámetro cuantitativo estricto que ANDIS aplica de forma rígida en sus dictámenes.
- **Marco de incompatibilidades endurecido:** redefinición de ausencia de vínculo laboral formal y de incompatibilidad con regímenes contributivos y no contributivos.
- **Derogación expresa:** los Decretos 7/2023 y 566/2023 (que habían flexibilizado los requisitos) quedaron derogados. No invocarlos; su texto ya no está en vigor.

**Estrategia de litigio obligatoria ante denegatoria post-Decreto 843/2024:** dado el endurecimiento del marco reglamentario, la estrategia no puede limitarse a rebatir el dictamen técnico de ANDIS con pericia médica en contrario. Debe plantearse, según el caso concreto, la **inconstitucionalidad e inconvencionalidad** del decreto en su aplicación al cliente:
- El parámetro del 66% aplicado automáticamente puede vulnerar el art. 12 CDPCD (igualdad ante la ley e independencia de la persona con discapacidad) y el art. 28 CDPCD (nivel de vida adecuado y protección social), ambos con jerarquía constitucional (Ley 27.044).
- El argumento central: la aplicación mecánica de techos rígidos de ingresos familiares o de porcentajes de invalidez sin evaluación individualizada de la situación de vulnerabilidad del solicitante viola el mandato convencional de protección específica.
- La doctrina de la CFSS y del Fuero Contencioso Administrativo Federal ya venía flexibilizando la noción de "invalidez" (fallo V., M. A. c/ Ministerio de Desarrollo Social, CFALP 2021); el planteo de inconvencionalidad del 843/2024 tiene base jurisprudencial preexistente.

**Regla condicional obligatoria - denegatoria de PNC posterior a septiembre de 2024:** si el caso involucra una denegatoria de PNC dictada con posterioridad al B.O. 23/09/2024, el escrito DEBE incluir un acápite autónomo fundando la inconvencionalidad del art. 1 del Decreto 843/2024 con base en los arts. 12 y 28 de la CDPCD (jerarquía constitucional, Ley 27.044). Este acápite no es optativo ni depende del perfil específico del cliente: la regla del 66% es un parámetro rígido que, por su estructura, impide la evaluación individualizada de vulnerabilidad que exige la Convención. El planteo de inconvencionalidad preserva además la instancia recursiva para el caso de derrota en primera instancia.

```
[VERIFICADO vía InfoLEG, jul. 2026: Decreto 843/2024 existe (sanción 20/09/2024, B.O. 23/09/2024 N° 35510), modifica el Decreto 432/1997. No se verificó jurisprudencia sobre su constitucionalidad - el fallo "V., M.A. c/ Ministerio de Desarrollo Social" (CFALP Sala II, 2021) citado como base de esta regla en discapacidad-DOCTRINA.md NO pudo verificarse (Cámara Federal de La Plata fuera del alcance de los conectores disponibles)]
```

### Ley 10.592 PBA - texto actualizado

La Ley 10.592 de la Provincia de Buenos Aires fue actualizada por la Ley 14.968. En escritos referidos a PBA, citar el texto actualizado y verificar si hubo nuevas modificaciones:
```
[VERIFICADO vía NormativaPBA, jul. 2026: Ley 10.592 vigente con modificaciones; Ley 14.968 vigente, la modifica. Portal registra además otras normas relacionadas posteriores (Leyes 15.505, 15.296, 15.018, 14.824, 13.762, entre otras) - revisar el texto consolidado en normas.gba.gob.ar antes de citar un artículo puntual]
```

---

## Normativa de referencia

### Fundamento supranacional y constitucional

- **Convención sobre los Derechos de las Personas con Discapacidad (CDPCD):**
  - Ley 26.378: aprobación y ratificación de la Convención.
  - Ley 27.044 (promulgada 18/11/2014): otorga jerarquía constitucional conforme art. 75 inc. 22 CN. Fuente interpretativa obligatoria para toda la normativa interna.
  - Arts. clave: 9 (accesibilidad), 12 (capacidad jurídica), 24 (educación inclusiva), 25 (salud sin discriminación), 27 (trabajo y empleo).
- **Convención Interamericana para la Eliminación de Todas las Formas de Discriminación contra las Personas con Discapacidad (CIADDIS):** Ley 25.280. Jerarquía: superior a las leyes (art. 75 inc. 22 CN) pero NO tiene jerarquía constitucional. Usar como instrumento complementario; fundar los argumentos de derechos fundamentales en la CDPCD, que sí tiene jerarquía constitucional desde la Ley 27.044.

### Aclaración sobre jerarquía de instrumentos internacionales

- **CDPCD (Ley 26.378 / Ley 27.044):** jerarquía constitucional (art. 75 inc. 22 CN). Fuente interpretativa obligatoria de toda norma interna en materia de discapacidad. Cúspide del bloque de constitucionalidad en esta materia.
- **CIADDIS (Ley 25.280):** jerarquía superior a las leyes pero infra-constitucional. No está en el listado del art. 75 inc. 22 CN. Citar como instrumento complementario o refuerzo, nunca como sustituto de la CDPCD.

En petitorios y fundamentos: cuando el argumento dependa de la jerarquía máxima del instrumento, siempre invocar la CDPCD (Ley 27.044) como norma de referencia primaria.

### Leyes nacionales fundamentales

- **Ley 22.431 (Sistema de Protección Integral):** base del sistema. Modificada por Ley 25.689 (cupo laboral). Reglamentada por Decreto 312/10. [VERIFICADO vía InfoLEG, jul. 2026: existe - confirmado por referencias cruzadas de las leyes modificatorias (24.314, 25.504, 25.635, 25.689) y por el Decreto 312/10 que la reglamenta]
- **Ley 24.901 (Prestaciones básicas):** cobertura de obras sociales y prepagas. Prestaciones médico-asistenciales, terapéuticas, educativas y sociales. Obligación de la obra social de cubrir el 100% sin límite de monto. [VERIFICADO vía InfoLEG, jul. 2026: existe, sanción 05/12/1997, B.O. 28789]
  - Art. 17: maestra / acompañante terapéutico
  - Art. 22: prestaciones de rehabilitación
  - Art. 24: centros de día
  - Art. 33: sistema de prestaciones básicas para personas sin obra social (ANDIS / Estado)
- **Ley 27.793 (Emergencia Nacional en Discapacidad):** vigente hasta 31/12/2026 (prorrogable). PNC por discapacidad (70% haber mínimo). Actualización de aranceles. [VERIFICADO vía InfoLEG, jul. 2026: existe, sanción 22/09/2025, B.O. 35754]
- **Ley 27.711 (CUD sin vencimiento):** el Certificado Único de Discapacidad no tiene fecha de vencimiento. Gratuito. Válido en todo el territorio nacional. [VERIFICADO vía InfoLEG, jul. 2026: existe, sanción 02/05/2023, B.O. 35161]
- **Ley 22.431 + Ley 25.504:** régimen original del CUD (reemplazado en lo pertinente por Ley 27.711 respecto del vencimiento). [VERIFICADO vía InfoLEG, jul. 2026: Ley 25.504 existe, sanción 13/12/2001, B.O. 29795, modifica Ley 22.431 sobre expedición del CUD]
- **Ley 25.635 (Transporte gratuito):** libre tránsito en transporte colectivo terrestre con CUD. Eximición de peajes. [VERIFICADO vía InfoLEG, jul. 2026: existe, sanción 27/08/2002, B.O. 29970, modifica Ley 22.431]
- **Ley 24.314 (Accesibilidad y transporte):** accesibilidad para personas con movilidad reducida. [VERIFICADO vía InfoLEG, jul. 2026: existe, sanción 12/04/1994, B.O. 27868, modifica Ley 22.431]
- **Ley 26.522 (art. 66):** accesibilidad en servicios de comunicación audiovisual. Subtitulado, lengua de señas, audiodescripción. [VERIFICADO vía InfoLEG, jul. 2026: existe, sanción 10/10/2009, B.O. 31756]
- **Ley 26.653:** accesibilidad de información en páginas web del Estado, empresas estatales y concesionarias de servicios públicos. [VERIFICADO vía InfoLEG, jul. 2026: existe, sanción 30/11/2010, B.O. 32038]
- **Ley 26.858 (Perro guía o de asistencia):** derecho de acceso a espacios públicos y privados. [VERIFICADO vía InfoLEG, jul. 2026: existe, sanción 14/06/2013, B.O. 32661]
- **Ley 26.657 (Salud mental):** protección del derecho a la salud mental. Internación involuntaria como último recurso. Interacción con CDPCD art. 12 (capacidad jurídica). [VERIFICADO vía InfoLEG, jul. 2026: la ley existe (sanción 03/12/2010, B.O. 32041); no se verificó el decreto reglamentario ni sus plazos específicos de internación]
- **Ley 23.660 / 23.661 (Obras sociales y ANSSAL):** marco del sistema de obras sociales nacionales. Base para la obligación de cobertura bajo Ley 24.901. [VERIFICADO vía InfoLEG, jul. 2026: ambas existen, sanción 29/12/1988, B.O. 26555]
- **Ley 26.682 (Medicina prepaga):** obligación de las empresas de medicina prepaga de cubrir las prestaciones de la Ley 24.901 y el PMO. [VERIFICADO vía InfoLEG, jul. 2026: existe, sanción 17/05/2011, B.O. 32151]

### Decretos reglamentarios clave

- **Decreto 84/2026:** reglamentación de la Ley 27.793 (Emergencia Nacional en Discapacidad). [VERIFICADO vía InfoLEG, jul. 2026: existe, sanción 04/02/2026, B.O. 35845, aprueba la reglamentación de la Ley 27.793]
- **Decreto 312/10:** reglamentario de la Ley 22.431. Certificación de discapacidad por el Ministerio de Salud / ANDIS. [VERIFICADO vía InfoLEG, jul. 2026: existe, sanción 08/03/2010, B.O. 31858]
- **Decreto 432/97 (texto actualizado por Decreto 843/2024):** condiciones de incompatibilidad y requisitos para PNC por invalidez. El Decreto 843/2024 (B.O. 23/09/2024) sustituyó el Anexo I y derogó los Decretos 7/2023 y 566/2023. Para cualquier reclamo de PNC, operar exclusivamente con el texto vigente del 843/2024; no invocar los decretos derogados. [VERIFICADO vía InfoLEG, jul. 2026: Decreto 432/1997 existe (sanción 15/05/1997, B.O. 28650); Decreto 843/2024 existe (sanción 20/09/2024, B.O. 35510) y figura como modificatorio de aquel, junto con los Decretos 7/2023 y 566/2023 (ambos confirmados existentes). No se verificó jurisprudencia sobre la constitucionalidad del 843/2024]
*(jul. 2026: se eliminó de este lugar la cita "Decreto 1421/02" como reglamentario del cupo laboral en el sector público - se buscó en InfoLEG por número y año en dos oportunidades y no se localizó ningún decreto con esos datos; se descarta como no verificable. El cupo laboral del 4% en el sector público se sostiene igual sobre su base normativa verificada: Ley 22.431 art. 8 y Ley 25.689.)*
- **Decreto 214/06:** homologa el Convenio Colectivo para la Administración Pública Nacional. [VERIFICADO vía InfoLEG, jul. 2026: existe, sanción 01/03/2006, B.O. 30856]

### Normativa provincial y local

- **Ley PBA 10.592 (texto actualizado Ley 14.968):** régimen jurídico básico e integral para personas con discapacidad en la Provincia de Buenos Aires. [VERIFICADO vía NormativaPBA, jul. 2026: Ley 10.592 vigente con modificaciones (promulgada 13/11/1987); Ley 14.968 vigente, la modifica (promulgada 23/10/2017)]
- **Ley CABA 962:** accesibilidad física para todos. Modifica el Código de Edificación de CABA (rampas, aceras, pendientes). [VERIFICADO, jul. 2026 - fuente aportada por el usuario: ciudadyderechos.org.ar, texto completo relevado. Ley CABA N° 962, sancionada 05/12/2002, publicada BOCBA N° 1607 el 13/01/2003. Título real: "Código de la Edificación. Modificación" (art. 1: modifica el Código de la Edificación de CABA conforme Anexo I y gráficos); regula específicamente accesibilidad física]

### Cupo laboral

- **4% mínimo** de personal con discapacidad en: Poder Ejecutivo, Legislativo, Judicial (nacional y provincial), empresas del Estado y servicios públicos.
- Base normativa: Ley 25.689 (modifica Ley 22.431).
- En PBA: verificar régimen específico provincial.

### Fuentes primarias de consulta

- **ANDIS (andis.gob.ar):** organismo de aplicación. Nomenclador, CUD, PNC, normativa actualizada.
- **Infoleg (infoleg.gob.ar):** texto oficial de leyes y decretos nacionales.
- **BOPBA (gob.gba.gov.ar):** normativa provincial PBA.
- **BOCBA (boletinoficial.buenosaires.gob.ar):** normativa CABA.
- **CSJN (csjn.gov.ar):** jurisprudencia federal en materia de discapacidad y amparo de salud.
- **CFSS (cij.gov.ar):** jurisprudencia de la Cámara Federal de la Seguridad Social.
- **SCBA (scba.gov.ar):** jurisprudencia PBA.

---

## Institutos frecuentes y lógica de diagnóstico

### Amparo por cobertura de prestaciones

El amparo de salud es la vía ordinaria para exigir cobertura inmediata de prestaciones. Verificar antes de plantear:

1. ¿El beneficiario tiene CUD vigente o está en trámite?
2. ¿La obra social o prepaga fue intimada fehacientemente y rechazó o guardó silencio?
3. ¿La prestación reclamada está en el nomenclador bajo Ley 24.901 o fue prescripta por profesional habilitado? Si no está en el nomenclador, la obligación de cobertura puede igualmente fundarse en los arts. 25 y 26 CDPCD con jerarquía constitucional (Ley 27.044), siempre que se acredite la inexistencia de alternativa eficaz dentro del nomenclador.
4. ¿La prescripción médica está debidamente fundada? Para prestaciones de tracto sucesivo como acompañante terapéutico (art. 17 Ley 24.901) o maestra de apoyo, acompañar resumen de historia clínica que justifique la especificidad, frecuencia e intensidad de la prestación. La orden médica escueta sin respaldo clínico debilita la verosimilitud.
5. ¿Está configurada la negativa o el silencio? Parametrizar: 48 a 72 horas hábiles sin respuesta en prestaciones urgentes; 10 días corridos en prestaciones de tracto sucesivo. Pasado ese plazo sin respuesta, el silencio es omisión idónea para el amparo.
6. ¿Hay urgencia que justifique medida cautelar autónoma o dentro del amparo?
7. ¿Es obra social nacional o prepaga (fuero Civil y Comercial Federal), obra social provincial (fuero provincial) o demandado estatal único como ANDIS (fuero Contencioso Administrativo Federal)?

**Instrucción operativa obligatoria para el asistente - AT:** ante cualquier reclamo de AT, el modelo debe requerir de forma activa que el usuario aporte la historia clínica detallada del beneficiario antes de redactar el amparo o la medida cautelar. Una prescripción médica aislada o escueta es inmediatamente atacada por el cuerpo médico forense de la obra social o prepaga demandada. Sin historia clínica que respalde el plan terapéutico, el dictamen de la contraria puede invertir la verosimilitud. No avanzar en la redacción de la cautelar sin que el usuario confirme que cuenta con historia clínica o resumen de historia clínica que justifique diagnóstico, objetivos terapéuticos, frecuencia e intensidad del AT.

Alertas específicas:
- La cobertura del 100% bajo Ley 24.901 no admite copagos ni topes de monto. Si la obra social impone coseguro, es resistible.
- La demora de la obra social en responder la prescripción médica puede configurar conducta omisiva suficiente para el amparo sin necesidad de rechazo expreso.
- Verificar siempre si hay prestador de la red; si no lo hay, la obra social debe autorizar el prestador elegido por el beneficiario.
- Acompañante Terapéutico vs. Cuidador Domiciliario: las obras sociales suelen rechazar la cobertura de AT argumentando que la figura corresponde a un cuidador domiciliario (prestación con menor amplitud o no contemplada del mismo modo en el PMO). La distinción es clínica: el AT cumple un rol terapéutico de rehabilitación con objetivos específicos de salud mental o desarrollo, establecidos en un plan de tratamiento; el cuidador es asistencial. Para resistir el rechazo, el dictamen médico debe explicitar el rol terapéutico y los objetivos rehabilitatorios del AT. Sin ese respaldo, la obra social puede sostener la sustitución.

### Medida cautelar de urgencia

En amparos de salud / discapacidad la medida cautelar es casi siempre autónoma respecto del fondo. Fundamentos habituales:

- Verosimilitud: dictamen médico + Ley 24.901 + CUD (o constancia de trámite)
- Peligro en la demora: irreversibilidad del daño a la salud o al desarrollo del paciente
- Contracautela: en caso de persona en situación de vulnerabilidad, pedir eximición o juratoria

Regla operativa: en amparos de salud en fuero Civil y Comercial Federal, verificar si aplica la Ley 26.854 cuando hay codemandado estatal:
```
[VERIFICADO vía InfoLEG, jul. 2026: Ley 26.854 existe, sanción 30/04/2013, B.O. 32629 (medidas cautelares en causas donde es parte el Estado Nacional). No se verificó jurisprudencia específica sobre su aplicación en amparos de salud con codemandado estatal - analizar caso por caso]
```

### Certificado Único de Discapacidad (CUD)

- Emitido por ANDIS. Gratuito. Sin fecha de vencimiento (Ley 27.711). Aclaración operativa: "sin vencimiento" no implica que no pueda requerirse actualización de la situación médica o del perfil del beneficiario; la implementación es progresiva según las resoluciones operativas de ANDIS. Verificar si el CUD del beneficiario requiere actualización de datos antes de invocarlo en juicio.
- Habilita: transporte gratuito, cobertura bajo Ley 24.901, pensión no contributiva, cupo laboral, franquicias fiscales.
- La ausencia de CUD no es obstáculo insuperable para el amparo si hay diagnóstico médico acreditado y el trámite está en curso; la jurisprudencia admite la cobertura provisional.

**Regla operativa - demoras administrativas de ANDIS en CUD (Ley 27.711):** cuando el beneficiario tiene CUD sin vencimiento pero ANDIS le exige una "actualización física o digital" del certificado y la demanda no ha completado ese trámite por demoras del propio organismo, incluir obligatoriamente en el amparo un párrafo que advierta que la demora administrativa de ANDIS en procesar la actualización no suspende ni extingue la obligación de cobertura de tracto sucesivo de la demandada. Fundamento: la obligación de cobertura bajo Ley 24.901 es de naturaleza continua; su vigencia no puede quedar sujeta a la eficiencia del organismo público emisor del CUD. El certificado sin fecha de vencimiento (Ley 27.711) acredita la condición de persona con discapacidad con independencia del estado de los trámites internos de ANDIS.

### Pensión No Contributiva (PNC) por discapacidad

- Origen: art. 9 Ley 13.478 y Decreto 432/97. La Ley 27.793 elevó y blindó el piso del 70% del haber mínimo jubilatorio frente a decretos de desregulación.
- Organismo otorgante: ANDIS.
- Monto vigente: 70% del haber mínimo jubilatorio. [VERIFICADO vía InfoLEG, jul. 2026: el 70% surge del texto de la Ley 27.793 (existente, verificada más arriba). El monto en pesos del haber mínimo es dinámico - verificar el valor actualizado en ANSES al momento de la consulta]
- Requisitos de incompatibilidad: verificar si el beneficiario tiene otro ingreso, jubilación o asignación que genere incompatibilidad.
- Vía de impugnación ante denegatoria: recurso administrativo ante ANDIS; agotada la vía, acción contencioso administrativa federal.
- **Atención - denegatoria posterior al 23/09/2024:** si la resolución fue dictada luego de la entrada en vigor del Decreto 843/2024, aplicar la regla condicional obligatoria de inconvencionalidad. Ver sección "Alerta normativa - Decreto 843/2024" y sección "Impugnación de denegatoria de PNC".

### Cupo laboral

- Obligación del 4% en el sector público y servicios públicos (Ley 25.689 / Ley 22.431).
- Para acreditar el incumplimiento: solicitar informe de planta de personal y porcentaje cubierto.
- Alerta de diagnóstico prudente: las acciones judiciales individuales para exigir el nombramiento de una persona concreta tienen progreso acotado. El amparo colectivo o la acción de cumplimiento presentan mejores perspectivas que el reclamo individual, salvo que el beneficiario se encuentre en los primeros lugares de un orden de mérito de concurso ya aprobado y firme. Evaluar la estrategia antes de litigar.
- En PBA: verificar régimen provincial específico. [NO VERIFICADO, jul. 2026 - no se identificó ni buscó una norma puntual de cupo laboral PBA en esta auditoría; identificar la norma provincial específica antes de invocarla]

### Salud mental - internación involuntaria

- La internación involuntaria es de último recurso (Ley 26.657, art. 20). Requiere dictamen del equipo interdisciplinario y control judicial inmediato.
- Plazo máximo de internación involuntaria sin revisión judicial: verificar en la reglamentación vigente.
- Interacción con CDPCD art. 12: la capacidad jurídica de la persona con discapacidad psicosocial o intelectual se presume; las restricciones son de interpretación estricta (CCCN arts. 31-50 post reforma Ley 26.657).

### Reintegro de gastos por prestaciones (acción de repetición)

Cuando el afiliado ya costeó la prestación ante la negativa de la obra social o prepaga, el reclamo pierde su naturaleza de urgencia tutelar y se convierte en una acción de conocimiento de contenido patrimonial. Verificar antes de plantear:

1. **Acreditación del desembolso:** condición sine qua non son las facturas emitidas conforme requisitos de ARCA (ex AFIP) con sus recibos o constancias bancarias de transferencia. La factura proforma o el presupuesto no habilitan la repetición.
2. **Intimación y contemporaneidad:** verificar que exista intimación fehaciente previa al gasto o solicitud de cobertura formal rechazada o silenciada por la demandada. La prescripción médica debe ser contemporánea al período reclamado.
3. **Monto reclamado:** si el gasto supera holgadamente el nomenclador, la demandada intentará limitar su responsabilidad al valor oficial. Si el excedente está clínicamente justificado (inexistencia de prestadores en cartilla o urgencia médica insalvable), fundar la repetición integral en los arts. 25 y 26 CDPCD.
4. **Prescripción aplicable:** 5 años (art. 2560 CCCN). La imprescriptibilidad del derecho a la cobertura no alcanza a la acción de repetición de gastos ya realizados; computar desde cada pago individual.

**Regla operativa crítica - improcedencia de cautelar para sumas consolidadas:** las medidas cautelares tienen efectos exclusivamente ex nunc (hacia el futuro); aseguran la continuidad de una prestación en curso o futura. Los gastos ya devengados antes de la interposición del amparo son un reclamo patrimonial consolidado que no puede canalizarse como medida cautelar. Pedir cautelar para cubrir períodos anteriores es procesalmente improcedente y expone al litigante a rechazo en ese punto, debilitando la presentación.

**Estructura correcta cuando el tratamiento continúa y hay sumas devengadas:**
- **Amparo de salud por cobertura futura** (para la prestación en curso): con medida cautelar de cobertura inmediata a partir de la interposición.
- **Acción ordinaria de reintegro de gastos** acumulada (para los períodos ya pagados): petitorio separado con liquidación de montos según nomenclador ANDIS vigente a cada período de devengamiento, con tasa de interés de la sala actuante desde cada fecha de pago.

Si la prestación ya cesó y el único reclamo es de sumas pasadas, la vía es la acción ordinaria de repetición exclusivamente; no hay urgencia que justifique el amparo.

### Impugnación de denegatoria de PNC (contencioso administrativo federal)

La denegación de una PNC por invalidez lesiona derechos de carácter alimentario. Verificar antes de plantear:

1. **Vía ordinaria vs. amparo:** si la denegatoria se funda en una cuestión formal de ingresos o incompatibilidad reglamentaria del Decreto 432/97, la vía adecuada es la impugnación contencioso-administrativa ordinaria, previa habilitación de instancia. El amparo procede solo si la arbitrariedad es manifiesta o si la demora genera peligro de daño irreparable para la subsistencia inmediata.
2. **Agotamiento de la vía:** recurso de reconsideración + jerárquico ante ANDIS conforme Ley 19.549. Verificar plazos de caducidad desde la notificación de la resolución denegatoria (art. 25 Ley 19.549). La omisión puede derivar en excepción de falta de habilitación de instancia.
3. **Dictamen de ANDIS como núcleo de la denegatoria:** para combatirlo judicialmente es obligatorio ofrecer pericial médica en sede judicial. Los informes médicos particulares actúan solo como elementos de verosimilitud inicial.
4. **Vulnerabilidad socioeconómica:** acreditar que el beneficiario reúne los requisitos del Decreto 432/97 (ausencia de bienes, ingresos o familiares obligados con capacidad de sostén). Sin ese capítulo, la demanda carece de sustento fáctico.
5. **Regla condicional obligatoria - denegatoria posterior al 23/09/2024:** si la resolución denegatoria de ANDIS fue dictada con posterioridad al B.O. 23/09/2024, el escrito DEBE incluir un acápite autónomo planteando la inconvencionalidad del art. 1 del Decreto 843/2024 con base en los arts. 12 y 28 de la CDPCD (jerarquía constitucional, Ley 27.044). Ver desarrollo completo en sección "Alerta normativa - Decreto 843/2024". Este planteo no es optativo: su omisión cierra la vía recursiva y deja sin base la pretensión si el juez aplica el parámetro del 66% de forma literal.

### Incumplimiento de cupo laboral (4%)

Diagnóstico estratégico obligatorio PREVIO a cualquier acción. La estrategia cambia radicalmente según si el empleador es privado o público.

**Regla operativa:** antes de asesorar al cliente sobre cupo laboral, definir:
1. ¿Sector privado o público?
2. Si es público, ¿nacional o local?
3. ¿Qué organismo o empresa es el demandado?

La respuesta determina fuero, plazo, procedimiento y estrategia. No equiparar cupo privado con cupo público.

#### A. Cupo laboral en sector PRIVADO

- **Régimen:** Ley 25.689 (modifica Ley 22.431) + Ley de Contrato de Trabajo.
- **Plazo:** 2 años desde el acto discriminatorio (art. 256 LCT).
- **Fuero:** laboral (provincial si la empresa actúa en provincia; federal si la relación tiene componente federal).
- **Procedimiento:** demanda ordinaria ante juez laboral.

Perspectiva de éxito: baja si no hay (i) concurso previo donde el cliente fue descalificado por la discapacidad, (ii) testigos internos, o (iii) prueba de trato discriminatorio específico. Estrategia recomendada: amparo laboral si la discriminación es manifiesta, más demanda por daño moral por discriminación; no limitar la pretensión a la reincorporación.

#### B. Cupo laboral en sector PÚBLICO NACIONAL (Administración Pública Nacional, empresas estatales)

- **Régimen:** Ley 25.164 [VERIFICADO vía InfoLEG, jul. 2026: existe, sanción 08/10/1999, B.O. 29247] + Ley 19.549 [VERIFICADO vía InfoLEG, jul. 2026: existe].
- **Plazo:** 60 días hábiles desde la notificación de la resolución denegatoria, o desde el vencimiento del silencio administrativo (30 días hábiles sin respuesta = rechazo tácito), conforme art. 25 Ley 19.549.
- **Fuero:** Contencioso Administrativo Federal. NO fuero laboral.
- **Vía administrativa previa (OBLIGATORIA):**
  - Recurso de reconsideración: ante el mismo órgano que dictó la resolución; plazo 10 días hábiles desde la notificación.
  - Recurso jerárquico (si correspondiere): ante la autoridad superior; plazo 10 días hábiles desde la denegación de la reconsideración.
  - Silencio: si el órgano no responde en 30 días hábiles, se considera tácitamente rechazada la solicitud; corre el plazo del art. 25 Ley 19.549.
- **Riesgo procesal:** omitir el agotamiento de la vía administrativa habilita la excepción de falta de habilitación de instancia, que cierra la puerta al contencioso. Verificar siempre antes de iniciar la demanda.

Estrategia recomendada: (1) amparo colectivo promovido por ONG legitimada, pidiendo que el organismo cumpla el 4% y respete el orden de mérito en designaciones futuras (tasa de éxito alta); (2) acción contencioso-administrativa individual solo si el cliente tiene orden de mérito firme y fue preterido; (3) acción de cumplimiento para obligar al organismo a implementar políticas de cupo sin designación nominal (tasa de éxito media-alta). Evitar: reclamo individual pidiendo designación en cargo específico sin concurso previo; la CSJN lo rechaza de forma uniforme.

#### C. Cupo laboral en sector PÚBLICO LOCAL (CABA, PBA, municipios)

- **Régimen:** leyes locales de empleo público y procedimientos administrativos locales.
- **Plazo:** verificar la ley local (generalmente 60 días para recurso administrativo).
- **Fuero:** CCAyT (CABA), fuero contencioso administrativo provincial (PBA y resto.
- **Procedimiento:** agotamiento de vía administrativa previa análogo al sector público nacional.
- En CABA: verificar si aplica procedimiento simplificado (Ley 189) o procedimiento ordinario contencioso-administrativo. [VERIFICADO, jul. 2026 - fuente aportada por el usuario: índice de Códigos CABA de InfoLEG (infoleg.gob.ar/?page_id=74), que remite a SAIJ e identifica la Ley 189 CABA como el Código Contencioso Administrativo y Tributario de la Ciudad, sanción 13/05/1999. Cupo laboral PBA sigue sin verificar - ver advertencia de la sección anterior]

Fuente: Ley 25.164, Ley 19.549, jurisprudencia CSJN reiterada, doctrina CFSS y Contencioso Administrativo Federal.

### Daños y perjuicios por falta de accesibilidad

Omisiones de barreras físicas, arquitectónicas o comunicacionales encuadran en responsabilidad civil por omisión (Leyes 22.431, 24.314, Ley CABA 962). Verificar antes de plantear:

1. **Configuración del daño concreto:** no basta invocar en abstracto la falta de una rampa o un ascensor adaptado. Acreditar el daño concreto: lesión física por accidente, o daño moral derivado de discriminación, exclusión y pérdida de chance de acceso a un servicio, empleo o educación.
2. **Factor de atribución objetivo:** la responsabilidad se funda en el riesgo creado por la habilitación de un espacio público o privado de acceso público que incumple la normativa imperativa de accesibilidad. No requiere demostrar culpa subjetiva.
3. **Prueba anticipada:** evaluar solicitar mandamiento de constatación u oficio judicial urgente para registrar fotográficamente o mediante perito las barreras físicas antes de que sean modificadas por la demandada.
4. **Beneficio de Litigar sin Gastos:** obligatorio evaluar su promoción en paralelo. El proceso exige peritos de arquitectura/ingeniería, médico y psicológico; las costas en resultado adverso pueden ser significativas. La exención de tasa del amparo no cubre automáticamente este proceso.

### Salud mental - control judicial de internación involuntaria y sistema de apoyos

La internación involuntaria es medida excepcional de privación de la libertad que exige control de legalidad inmediato (Ley 26.657, art. 20). Verificar:

1. **Rol del abogado en internación:** controlar que la medida cuente con dictamen del equipo interdisciplinario que acredite riesgo cierto e inminente para sí o para terceros. Si el riesgo cesó o el dictamen es monodisciplinario (solo psiquiatra), solicitar alta inmediata o externación asistida.
2. **Sistema de Apoyos (art. 12 CDPCD):** en los procesos de restricción de la capacidad jurídica, la labor del especialista no es consentir la declaración de incapacidad sino proponer un diseño a medida de apoyos y salvaguardias. El escrito debe delimitar con precisión para qué actos el cliente necesita asistencia, preservando la presunción de capacidad (arts. 31-50 CCCN). No proponer curatela genérica sin análisis personalizado.
3. **Plazos de revisión:** proponer revisión judicial periódica de la medida (máximo 3 años según CCCN) y mecanismos para evitar conflictos de interés o influencias indebidas sobre la persona designada como apoyo.

### Prescripción y caducidad

No existe un plazo único para acciones en materia de discapacidad. La regla varía según el tipo de reclamo:

Tipo de reclamo | Plazo | Observación
--- | --- | ---
Prestaciones médicas bajo Ley 24.901 (cobertura futura o en curso) | No prescriptible (derecho continuo) | La obligación de cobertura subsiste mientras subsiste la discapacidad
Reintegros dinerarios por prestaciones ya pagadas | 5 años (art. 2560 CCCN) | La imprescriptibilidad alcanza al derecho a la cobertura, no a la acción de repetición de gastos pasados; no reclamar reintegros sin verificar el cómputo desde cada pago
Pensión No Contributiva (Ley 13.478 / Decreto 432/97) | No prescriptible | Derecho de carácter alimentario
Transporte gratuito con CUD | No prescriptible | Derecho continuo vinculado al CUD
Cupo laboral 4% - Sector privado (LCT) | 2 años (art. 256 LCT) | Fuero laboral (provincial o federal); demanda ordinaria. Plazo corre desde el acto de discriminación o el despido discriminatorio.
Cupo laboral 4% - Sector público nacional (Ley 25.164) | 60 días hábiles (art. 25 Ley 19.549) para recurso administrativo; luego caducidad para acción contencioso-administrativa | Fuero Contencioso Administrativo Federal. Requiere agotamiento previo de vía administrativa (recurso de reconsideración + jerárquico). Ver "Incumplimiento de cupo laboral (4%)".
Cupo laboral 4% - Sector público local (CABA, PBA, etc.) | Verificar ley local; generalmente 60 días para recurso administrativo | CCAyT (CABA), fuero contencioso administrativo provincial (PBA). Agotamiento de vía administrativa previa análogo al sector público nacional.
Accesibilidad - daños y perjuicios (Ley 962 / Ley 22.431) | 3 años | Art. 2561 CCCN (responsabilidad civil concurrente)
Amparo federal (Ley 16.986) | 15 días hábiles (art. 2 inc. e Ley 16.986), pero inaplicable cuando el daño es de tracto sucesivo | La CSJN tiene dicho reiteradamente que en materia de salud el plazo de caducidad no rige mientras la lesión sea continua u omisiva; la falta de cobertura renueva el daño a diario
Amparo local CABA (Ley 2145) | 45 días hábiles desde el acto lesivo | Misma excepción por omisión continua según TSJ CABA; alertar siempre y no confiar en la excepción sin verificar jurisprudencia actualizada
Reclamo administrativo (PNC, CUD denegado) | Verificar plazos de silencio y recurso según LPA aplicable | LPA nacional o provincial según el caso

*(jul. 2026: se leyó el texto completo de la Ley 2145 aportado por el usuario - Ley de Amparo CABA, BOCBA 2603, 12/01/2007. El articulado relevado no fija expresamente un plazo de "45 días hábiles desde el acto lesivo" para interponer la acción; el único plazo de caducidad que contiene la ley (art. 25) es de 30 días -60 en amparo colectivo- por inactividad procesal, que es un concepto distinto (caducidad de instancia, no plazo para demandar). [REVISIÓN NORMATIVA REQUERIDA: confirmar de dónde surge el plazo de 45 días hábiles - puede provenir de doctrina/jurisprudencia del TSJ CABA no relevada aquí, o ser un error; no invocarlo en un escrito sin verificar la fuente puntual primero.])*

**Regla de freno - prohibición de extrapolación automática al fuero porteño:** la inaplicabilidad del plazo de caducidad en amparos de salud federal (doctrina CSJN, omisión continua) NO se traslada automáticamente al fuero contencioso-administrativo de CABA. El TSJ CABA aplica la exención por omisión continua bajo la Ley 2145, pero su jurisprudencia es propia y debe verificarse en cada caso. Antes de invocar en sede porteña la exención del plazo de caducidad con fundamento exclusivo en doctrina federal, el modelo debe alertar que la extrapolación no es automática y requerir verificación de jurisprudencia actualizada del TSJ CABA y de las Salas de la Cámara CCAyT. La omisión de este análisis puede derivar en rechazo liminar por caducidad sin posibilidad de subsanación.

Regla operativa: alertar siempre sobre el plazo aplicable y la fecha de inicio del cómputo antes de analizar el fondo. En amparos locales CABA, el plazo de caducidad es una de las primeras verificaciones a realizar.

---

## Procesos especiales

### Amparo de salud - fuero Civil y Comercial Federal (CABA)

- Vía principal para exigir cobertura inmediata contra obras sociales nacionales y empresas de medicina prepaga.
- El escrito debe: acreditar la condición del beneficiario (CUD o constancia de trámite), la prescripción médica, la intimación a la obra social o prepaga y su silencio o rechazo, y la urgencia.
- Petitorio: medida cautelar de cobertura inmediata + sentencia definitiva de condena a cubrir la prestación + imposición de costas a la demandada.
- Regla operativa: incluir siempre en el petitorio la imposición de costas a la obra social, prepaga o Estado demandado, fundada en la naturaleza alimentaria del reclamo y en la tutela del derecho a la salud como derecho humano. La persona con discapacidad no debe ver mermado su patrimonio para defender su salud.
- **Regla operativa - reserva de inconstitucionalidad arancelaria:** al redactar la demanda, incluir siempre la reserva de inconstitucionalidad de toda normativa arancelaria local o tope de la Ley 27.423 [VERIFICADO vía InfoLEG, jul. 2026: existe, sanción 22/12/2017, B.O. 22/12/2017, honorarios de abogados/procuradores] que, en su aplicación al caso concreto, perfore el mínimo legal de honorarios o afecte la indemnidad del profesional que litiga en casos de vulnerabilidad. Fundamento: el derecho del abogado a una retribución digna no puede ser sacrificado por regulaciones tarifarias que no contemplen la complejidad técnica ni el impacto social del litigio en discapacidad. La reserva debe plantearse en la demanda y reiterarse en la regulación de honorarios; su omisión en primera instancia dificulta el planteo en alzada.
- Regla operativa procesal: incluir siempre la prueba documental completa como anexo; el fuero resuelve con celeridad cuando la urgencia está acreditada. Verificar aplicación de Ley 26.854 en materia cautelar si hay demandado estatal codemandado.

### Amparo - fuero contencioso administrativo (CABA o federal)

- Para actos u omisiones del GCBA o del Estado nacional (ANDIS, otros organismos).
- En CABA: Ley 2145 (amparo local). Verificar si la materia es de competencia del CCAyT o del fuero civil.
- Plazo de caducidad en CABA: 45 días hábiles desde el acto lesivo (Ley 2145). Alertar siempre.

```
[VERIFICADO, jul. 2026 - fuente aportada por el usuario: Boletín Oficial CABA, boletinoficialpdf.buenosaires.gob.ar/util/imagen.php?idn=92847&idf=1, texto completo de la Ley A N° 2.145 (Ley de Amparo de la Ciudad Autónoma de Buenos Aires), publicada en BOCBA 2603 del 12/01/2007. El art. 25 fija la caducidad de instancia por inactividad en 30 días (60 en amparo colectivo) - no es un plazo de caducidad para interponer la acción; verificar si la referencia a "45 días hábiles desde el acto lesivo" corresponde a esta ley o a otra norma/doctrina antes de invocarla en un escrito, porque no surge del texto del articulado relevado]
```

### Proceso ordinario - obra social o prepaga

- Cuando la prestación no es urgente o el reclamo es dinerario (reintegros, daños).
- Verificar fuero competente: Civil y Comercial Federal para obras sociales nacionales y prepagas; federal de seguridad social para reclamos previsionales ante ANSES; contencioso administrativo federal si el único demandado es el Estado nacional o ANDIS.

### Proceso ordinario o contencioso contra el Estado nacional / ANDIS - vía administrativa previa

- Antes de iniciar un proceso ordinario contra el Estado nacional o ANDIS, verificar el agotamiento de la vía administrativa (Ley 19.549 [VERIFICADO vía InfoLEG, jul. 2026: existe]): recurso de reconsideración ante el mismo órgano y, si correspondiere, recurso jerárquico ante la autoridad superior. La omisión de este requisito puede derivar en excepción de falta de agotamiento de la vía.
- Excepción para el amparo: la jurisprudencia exime del agotamiento previo cuando el tránsito por la vía administrativa tornaría ilusorio el derecho a la salud o generaría un daño irreversible. En esos casos, la urgencia y el peligro en la demora justifican acudir directamente al amparo sin agotar sede administrativa.
- Regla operativa: ante cualquier reclamo contra el Estado o ANDIS, definir primero si la vía es el amparo (urgencia + omisión continua) o el proceso ordinario (reclamo patrimonial sin urgencia). La elección determina si el agotamiento previo es exigible.

---

## Instrucciones operativas específicas - discapacidad

- Identificar siempre: (a) si el beneficiario tiene CUD vigente o en trámite; (b) quién es el obligado a cubrir (obra social nacional, provincial, prepaga, Estado); (c) si la prestación está en el nomenclador o fue prescripta.
- No asumir cobertura sin verificar que la prestación está contemplada bajo Ley 24.901 o en el PMO. Si hay duda, marcar con [REVISIÓN NORMATIVA REQUERIDA].
- Verificar fuero antes de cualquier análisis procesal: la competencia varía según el tipo de demandado.
- En amparos de salud: plantear siempre la medida cautelar. La demora en la cobertura de prestaciones para personas con discapacidad configura peligro en la demora in re ipsa en la mayoría de los fueros.
- No cuantificar aranceles sin verificar el nomenclador vigente. Si el abogado pide una estimación orientativa, brindarla con marcador [AVANCE BAJO RESERVA] y señalar qué resolución ANDIS corresponde verificar.
- Prescripción: no asumir plazo único; identificar el tipo de reclamo y aplicar la tabla de prescripción y caducidad de este perfil. En amparos locales CABA, verificar el plazo de caducidad de 45 días hábiles como primera verificación.
- Tasa de justicia y BLSG: en amparos de salud / discapacidad, verificar si el fuero aplica exención de tasa de justicia para personas con discapacidad o en situación de vulnerabilidad antes de presentar el escrito inicial. Si el proceso no es un amparo sino un ordinario (ej. daños y perjuicios por falta de accesibilidad), la exención de tasa no cubre automáticamente los gastos de peritos ni las costas en caso de resultado adverso; evaluar y proponer la promoción del Beneficio de Litigar sin Gastos (BLSG) en paralelo con la demanda principal.
```
[VERIFICADO vía PJN Jurisprudencia, jul. 2026 - texto de sumario leído. La exención real y consolidada que existe en la Cámara Civil y Comercial Federal corre por el art. 39 de la Ley 23.661 (agentes del seguro de salud), y beneficia a la OBRA SOCIAL cuando actúa como demandada en el amparo, no automáticamente al actor/paciente con discapacidad: CCF, "Tagliaferro, Graciela Noemí c/ OSDEPYM s/Sumarísimo de Salud", Expte. 7253/2021, sumario ID 70268 (16/04/2024); CCF Sala 3, "Tosar, María c/ Obra Social de la Unión del Personal Civil de la Nación s/Amparo de Salud", Expte. 22817/2019, sumario ID 62097 (21/09/2023). Ambos remiten al leading case CSJN "A.P.S. c/ Medicus SA s/Recurso de Hecho", 04/05/2000, Fallos 323:973, que fijó que la redacción genérica del art. 39 Ley 23.661 comprende la tasa judicial. Para que el ACTOR con discapacidad (no la obra social demandada) quede exento de la tasa, la vía verificada sigue siendo el Beneficio de Litigar sin Gastos, no una exención automática por discapacidad.]
```
- Costas: en todo amparo de salud o medida cautelar que resulte en la concesión de la prestación, incluir siempre en el petitorio la imposición de costas a la demandada (obra social, prepaga o Estado). Ver también regla de costas en sección "Amparo de salud - fuero Civil y Comercial Federal".
- **AT escolar y maestra integradora (regla antievasión de cobertura):** ante cualquier reclamo de AT en ámbito escolar o de maestra de apoyo a la integración, invocar siempre el art. 24 CDPCD (Educación Inclusiva, jerarquía constitucional Ley 27.044) en concordancia con el art. 17 Ley 24.901. Esta doble base normativa neutraliza la defensa estándar de las obras sociales y prepagas que califican la prestación como "educativa" para derivar la responsabilidad al Ministerio de Educación: si el equipo tratante justifica que el AT en el aula es indispensable para la rehabilitación neurocognitiva y la integración psicosocial, la cobertura es médica, no educativa, y es obligatoria bajo Ley 24.901 art. 17. *(jul. 2026: se retiró de este párrafo la cita "M., R.A. c/ OSDE, CCF Sala I 2021" que la respaldaba - no se localizó en PJN Jurisprudencia en dos rondas de búsqueda y se elimina por no poder descartarse que sea inventada. El principio normativo, art. 24 CDPCD + art. 17 Ley 24.901, ambos verificados, se sostiene igual sin esa cita.)*
- Todo escrito en discapacidad cierra con "Estado del escrito" estándar más este bloque analítico obligatorio:
  1. Fuero y competencia determinada.
  2. Condición del beneficiario frente al CUD (Vigente / En trámite / Ausente).
  3. Obligado / Demandado identificado (Obra Social / Prepaga / Estado / Particular).
  4. Tipo de acción seleccionada (Amparo / Ordinario de Reintegro / Contencioso Administrativo / Daños / Determinación de Capacidad).
  5. Prestación en nomenclador (Sí / A verificar / Fuera de nomenclador con fundamento CDPCD / Reclamo de contenido patrimonial u ordinario).
  6. Medida cautelar o tutela de urgencia planteada (Sí / No / Medida preliminar de constatación).
  7. Legajo de Beneficio de Litigar sin Gastos (Iniciado / No requiere por Amparo / A evaluar).
  8. Próximo plazo procesal o estado de la vía administrativa previa.

---

*Última actualización: junio 2026 - revisión de auditoría técnica (v5)*
*Correcciones aplicadas v1: (1) competencia PAMI bifurcada; (2) jerarquía CIADDIS vs. CDPCD; (3) cupo laboral privado/público desdoblado.*
*Correcciones aplicadas v2: (4) Decreto 843/2024; (5) improcedencia cautelar sumas consolidadas; (6) doctrina CCF 2026 cobertura blindada; (7) nota PBA departamento judicial; (8) regla antievasión AT escolar.*
*Correcciones aplicadas v3: (9) regla CUD/ANDIS demoras; (10) regla condicional 843/2024; (11) freno extrapolación caducidad CABA; (12) reserva inconstitucionalidad arancelaria.*
*Correcciones aplicadas v4 (auditoría interna): (A) regla condicional 843/2024 cruzada a sección "Impugnación PNC"; (B) tabla prescripción reordenada - Regla de freno fuera de la tabla; (C) reenvío a regla 843/2024 en sección PNC institutos frecuentes; (D) AFIP corregido a ARCA (ex AFIP); (E) umbral erróneo "50 empleados" eliminado de cupo privado; (F) "transporte" acotado a jurisdicción local CABA en tabla de fueros.*
*Correcciones aplicadas v5 (auditoría externa junio 2026): (N) alerta práctica sobre juzgados federales multifuero del interior - tendencia de acumulación por atracción en causas PAMI; (O) nota operativa de segundo semestre 2026 sobre riesgo de vencimiento de Ley 27.793 sin prórroga y estrategia de respaldo subsidiario; (P) instrucción operativa explícita para el asistente: requerir historia clínica detallada antes de redactar cualquier amparo/cautelar de AT.*
*Correcciones aplicadas v6 (auditoría de verificación, julio 2026): se verificó cada norma marcada con [VERIFICAR VIGENCIA] contra InfoLEG (nacional) o NormativaPBA (provincial). Resultado: prácticamente toda la normativa nacional y provincial citada existe y fue confirmada (Ley 22.431, 24.901, 27.793, 27.711, 25.504, 25.635, 24.314, 26.522, 26.653, 26.858, 26.657, 23.660/661, 26.682, 27.423, 25.164, 19.549, 26.854, Decretos 84/2026, 312/10, 432/97, 843/2024, 214/06, Ley PBA 10.592/14.968). 
*Correcciones aplicadas v7 (segunda auditoría, julio 2026 - (1) Ley CABA 189 -> VERIFICADA vía índice de InfoLEG (page_id=74) con remisión a SAIJ: es el Código Contencioso Administrativo y Tributario de la Ciudad, sanción 13/05/1999. (2) Ley CABA 2145 -> VERIFICADA vía Boletín Oficial CABA (PDF completo, BOCBA 2603, 12/01/2007): es la Ley de Amparo de la Ciudad. Al leer el articulado se detectó una inconsistencia: el archivo afirmaba un plazo de caducidad de "45 días hábiles desde el acto lesivo" para amparos locales, pero el texto de la Ley 2145 no contiene ese plazo - su único plazo de caducidad (art. 25) es de 30/60 días por inactividad procesal (instituto distinto). Se dejó marcador [REVISIÓN NORMATIVA REQUERIDA] en la tabla de prescripción y caducidad señalando que el origen del plazo de 45 días debe confirmarse (posible doctrina/jurisprudencia TSJ CABA no relevada) antes de volver a invocarlo en un escrito.*
*Correcciones aplicadas v9 (julio 2026, cierre de marcador [VERIFICAR JURISPRUDENCIA] pendiente): se buscó y se encontró jurisprudencia sobre exención de tasa de justicia en salud, y se precisó la doctrina de competencia bifurcada PAMI. (1) Tasa de justicia: CCF, "Tagliaferro c/ OSDEPYM", Expte. 7253/2021 (16/04/2024) y CCF Sala 3, "Tosar c/ Obra Social Unión Personal Civil de la Nación", Expte. 22817/2019 (21/09/2023), ambos remitiendo al leading case CSJN "A.P.S. c/ Medicus SA", 04/05/2000, Fallos 323:973: la exención del art. 39 Ley 23.661 beneficia a la obra social demandada, no automáticamente al actor con discapacidad. (2) Competencia PAMI: confirmado con CCF Sala I "Bassignani c/ INSSJP" (18/11/2025) y CCF Sala 3 "Peralta c/ INSSJP" (04/11/2025) que la línea divisoria real de la Cámara es "prestación de salud" (art. 2 Ley 19.032) vs. "promoción y asistencia social/previsional" (art. 3 Ley 19.032), más amplia que el "médica vs. jubilatoria" que traía el archivo.*
*Normativa base: CDPCD (Ley 26.378 / Ley 27.044), Ley 22.431, Ley 24.901, Ley 27.793, Ley 27.711, Ley 26.657, Ley 26.682, Ley 25.164, Ley 19.549*
*Nota: verificar aranceles ANDIS y estado de la emergencia (Ley 27.793) al momento de cada consulta*
*Autor: Dr. Cristian Aboitiz · [@abogadoaboitiz](https://x.com/abogadoaboitiz)*
