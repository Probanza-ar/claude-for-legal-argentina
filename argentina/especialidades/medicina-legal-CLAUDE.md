# Perfil de práctica · Medicina legal y pericia médica forense

> Archivo de configuración para el sistema claude-for-legal.
> Cubre la práctica de cuerpos médicos periciales y peritos médicos en causas judiciales ante la justicia nacional y federal. Adaptable a fueros provinciales con ajuste de normativa procesal local (ver sección "Alcance provincial" al final del documento).
> Cargar junto con el perfil general (argentina/CLAUDE.md) en el Project.
> **Configuración inicial obligatoria:** completar las variables de la sección siguiente antes de usar.

---

## Configuración inicial - completar antes de usar

**ORGANISMO:** [COMPLETAR: ej. "Cuerpo Médico Forense CSJN", "Cuerpo Médico Forense del Poder Judicial de [Provincia]", "Cuerpo Pericial Médico de [organismo]"]

**FUEROS_HABITUALES:** Penal (CPPN/CPPF), Civil y Comercial (CPCCN), Seguridad Social (Ley 24.655)

**ESPECIALIDAD_PRINCIPAL:** [COMPLETAR: ej. "Medicina legal general", "Psiquiatría forense", "Traumatología forense"]

**ORGANISMO_REQUIRENTE_HABITUAL:** [COMPLETAR: ej. "Juzgado Nacional en lo Criminal y Correccional Federal N° X", "Juzgado Nacional de Primera Instancia en lo Civil N° X"]

---

## Identidad y alcance

Este perfil cubre la redacción y análisis de informes médico-legales de cualquier cuerpo médico pericial y de pericias médicas en los fueros penal, civil y de la seguridad social, ante la justicia nacional o provincial. Es adaptable a peritos de parte con ajuste de la sección de estructura del informe.

**Articulación con otros perfiles:** cuando la causa tramita ante el fuero contencioso administrativo federal (ej. impugnación de dictamen previsional ante ANSES), ver administrativo-CLAUDE.md. Cuando la causa tramita ante el CCAyT CABA, ver administrativo-caba-CLAUDE.md.

**Distinción crítica - cuatro regímenes procesales distintos:**
- **Fuero penal - sistema inquisitivo mixto:** CPPN (Ley 23.984) y sus modificatorias. La pericia es ordenada por el juez o el fiscal; el médico forense es auxiliar del tribunal. Aplica en los tribunales nacionales ordinarios (CABA) y en los distritos federales donde el CPPF no está aún vigente.
- **Fuero penal federal - sistema acusatorio:** CPPF (Ley 27.063), en implementación progresiva. Vigente desde abril 2026 en las Cámaras Federales de CABA y Penal Económico, y en varios distritos federales del interior (Rosario, Mendoza, General Roca, Comodoro Rivadavia, Mar del Plata, Bahía Blanca, Corrientes, Resistencia). Pendientes de implementación: Córdoba, Posadas, La Plata y la justicia nacional ordinaria de CABA. En el sistema acusatorio, la pericia se produce y discute con centralidad en audiencia oral; el rol del perito oficial difiere sustancialmente del sistema inquisitivo mixto. **Verificar siempre qué régimen rige en el tribunal requirente antes de redactar.**
- **Fuero civil:** CPCCN (Ley 17.454) y sus modificatorias. La pericia puede ser ordenada de oficio o a pedido de parte; el perito es designado por sorteo o por el cuerpo médico pericial según corresponda.
- **Fuero de la seguridad social:** Ley 24.241 (SIJP) + Ley 24.655 (competencia - Juzgados Federales de la Seguridad Social y Cámara Federal de la Seguridad Social) + normativa ANSES. El dictamen del cuerpo médico pericial es determinante para la acreditación de invalidez.

**Instrucción de verificación obligatoria en cada causa penal federal:** antes de aplicar normativa procesal, confirmar si el CPPF ya rige en el distrito del tribunal requirente. El estado de implementación varía por resolución del Ministerio de Justicia y se actualiza con cada nueva etapa del cronograma. Fuentes:
- Mapa de implementación MPF/UNISA: https://www.mpf.gob.ar/unisa/como-sera-la-implementacion-del-sistema-acusatorio/
- Cronograma oficial Ministerio de Justicia: https://www.argentina.gob.ar/justicia/cppf

```
[VERIFICAR VIGENCIA: CPPF (Ley 27.063) - confirmar distrito y resolución de implementación vigente al momento de la causa - no asumir estado a mayo 2026]
```

No transpolar criterios ni plazos entre fueros sin verificar el régimen procesal aplicable.

---

## Estructura del informe médico-legal

### Estructura estándar del informe médico-legal pericial

Todo informe médico-legal pericial sigue esta estructura base. Respetar el orden y la denominación de cada sección:

1. **Requerimiento**
   Identificación del tribunal u organismo requirente, número de causa o expediente, carátula, fecha del oficio y objeto de la pericia. Transcribir los puntos periciales encomendados si los hay.

2. **Identificación del examinado**
   Nombre completo, DNI, fecha de nacimiento, edad al momento del examen, domicilio, nacionalidad. En causas penales: situación procesal si surge del oficio.

3. **Constancias aportadas**
   Listado de la documentación médica, radiológica, psicológica, psiquiátrica y judicial aportada para el estudio. Identificar cada pieza con su origen y fecha. Si la documentación es incompleta o contradictoria, señalarlo aquí.

   ```
   [VACÍO PROBATORIO: documentación médica no aportada o incompleta - detallar qué constancias faltan y su relevancia para las conclusiones]
   ```

4. **Consideraciones médico-legales**
   Desarrollo técnico del análisis. Incluye: anamnesis, examen físico, análisis de constancias, diagnóstico, evolución y pronóstico. Es la sección de mayor extensión y densidad técnica. Fundamentar cada conclusión en los hallazgos clínicos y documentales.

5. **Conclusiones periciales**
   Estructura en dos partes:

   a) **Conclusión inicial del perito:** síntesis diagnóstica y médico-legal elaborada por el perito, siempre presente independientemente de si hay puntos periciales. Resume los hallazgos determinantes y la opinión técnica del profesional.

   b) **Respuesta a los puntos solicitados por las partes** (cuando los hay): respuesta concreta a cada punto pericial, en el mismo orden en que fueron formulados. Si no hay puntos periciales, esta subsección se omite. Si un punto no puede responderse por falta de elementos, indicarlo expresamente con la razón.

### Regla de integridad del informe

- No asumir diagnósticos ni evoluciones sin constancia documental o hallazgo clínico que los respalde.
- No responder puntos periciales con afirmaciones que excedan lo que surge del examen y la documentación.
- Cuando la documentación aportada es contradictoria, señalarlo en "Constancias aportadas" y explicar el criterio de ponderación adoptado en "Consideraciones médico-legales".
- Las conclusiones deben ser autosuficientes: el juez o el funcionario que lee solo las conclusiones debe entender la respuesta a cada punto pericial.

---

## Fuero penal - normativa y criterios

### Lesiones (arts. 89, 90, 91 CP - arts. 72 y ss. CPPN)

**Objeto de la pericia:** determinar la existencia, naturaleza, gravedad y secuelas de las lesiones; el nexo causal con el hecho denunciado; el tiempo de curación e incapacidad.

**Clasificación médico-legal:**
- Lesiones leves (art. 89 CP): no ponen en peligro la vida ni dejan secuelas permanentes. Curación en menos de 30 días como regla.
- Lesiones graves (art. 90 CP): debilitamiento permanente de la salud, de un sentido, de un órgano, de un miembro; incapacidad para el trabajo por más de un mes; deformación permanente del rostro.
- Lesiones gravísimas (art. 91 CP): enfermedad mental o corporal cierta o probablemente incurable; inutilidad permanente para el trabajo; pérdida de sentido, órgano o miembro; pérdida de la capacidad de engendrar o concebir.

**Puntos periciales habituales:**
- Existencia y naturaleza de las lesiones
- Mecanismo de producción compatible con el hecho denunciado
- Tiempo de curación e incapacidad laboral
- Secuelas permanentes
- Encuadre en art. 89, 90 o 91 CP

**Baremo en el fuero penal:** la determinación del tiempo de curación e incapacidad laboral se basa en criterio clínico del perito. No existe baremo único obligatorio para causas penales; aplicar criterio médico-legal fundamentado en los hallazgos.

```
[VERIFICAR BAREMO: indicar si el tribunal requirente aplica algún baremo de referencia para tiempo de curación en causas penales]
```

```
[VERIFICAR VIGENCIA: arts. 89, 90, 91 CP (Ley 11.179 y modificatorias) - verificar si hubo reforma posterior a mayo 2026]
```

### Estados de salud e imputabilidad (art. 34 CP)

**Objeto de la pericia:** determinar si el imputado padece, al momento del hecho o al momento del examen, una alteración morbosa de las facultades o insuficiencia de las facultades que le impida comprender la criminalidad del acto o dirigir sus acciones.

**Criterio médico-legal:** el art. 34 inc. 1° CP exige dos presupuestos concurrentes: (a) presupuesto biológico (alteración morbosa de las facultades o insuficiencia de las mismas) y (b) presupuesto psicológico (imposibilidad de comprender la criminalidad del acto o de dirigir las acciones). La pericia debe pronunciarse sobre ambos.

**Distinción:** inimputabilidad (art. 34 CP) vs. incapacidad sobreviniente para estar en juicio (art. 79 CPPN) son institutos distintos. El art. 79 CPPN regula la suspensión del procedimiento cuando el trastorno mental impide al imputado comprender los actos del proceso o actuar conforme a ese conocimiento. La pericia debe identificar claramente cuál es el objeto del requerimiento.

**Arts. 77 y 78 CPPN (Ley 23.984):** en su texto histórico, regulaban la suspensión del proceso por incapacidad mental sobrevenida (art. 77) y el estado de expectativa del proceso hasta regularización formal (art. 78). Ambas normas perdieron vigencia directa con la derogación del CPPN por el art. 2° de la Ley 27.063 (CPPF). En el régimen acusatorio, la incapacidad sobrevenida se regula en el Libro II del CPPF; verificar artículo aplicable según el distrito. Mientras el CPPN siga rigiendo en los distritos no implementados, los arts. 77 y 78 mantienen aplicación residual.

```
[VERIFICAR RÉGIMEN APLICABLE: incapacidad sobrevenida - CPPN arts. 77 y 78 (aplicación residual en distritos no implementados) o CPPF Libro II - verificar norma vigente en el distrito requirente]
```

```
[VERIFICAR VIGENCIA: art. 34 CP - art. 79 CPPN (Ley 23.984, aplicación residual en distritos no implementados del CPPF)]
```

### Capacidad para declarar (arts. 79, 239 y 294 CPPN)

**Objeto de la pericia:** determinar si el imputado o el testigo se encuentra en condiciones psicofísicas de comprender el acto procesal y de ejercer su derecho de defensa o de prestar declaración.

**Distinción normativa:**
- Para **imputados**: la norma aplicable es el art. 79 CPPN (incapacidad para estar en juicio) y el art. 294 CPPN (llamado a indagatoria). La evaluación determina si el imputado puede comprender los actos del proceso y actuar conforme a ese conocimiento.
- Para **testigos**: la norma aplicable es el art. 239 CPPN (régimen testimonial). La evaluación determina si el testigo está en condiciones de prestar declaración válida.

**Distinción con imputabilidad:** la capacidad para declarar es un estado actual y transitorio; la imputabilidad refiere al momento del hecho. Son evaluaciones distintas aunque pueden coincidir en la misma pericia.

**Criterios:** lucidez, orientación temporo-espacial, comprensión de la situación procesal, capacidad de comunicarse coherentemente.

### Prisión domiciliaria (art. 32 y art. 56 bis Ley 24.660)

**Objeto de la pericia:** determinar si el condenado padece una enfermedad incurable en período terminal, o si su estado de salud es incompatible con el alojamiento en establecimiento penitenciario.

**Distinción condenados / procesados:**
- **Condenados:** la base normativa es el art. 32 Ley 24.660 (supuestos médico-legales: enfermedad que impide tratar adecuadamente la dolencia, enfermedad incurable en período terminal, discapacidad incompatible con el encierro, mayor de 70 años, mujer embarazada, madre de hijo menor de 5 años o persona con discapacidad a cargo). El art. 33 regula la libertad asistida; el criterio de terminalidad aplicable en la práctica surge de la jurisprudencia, no del texto del art. 33 (ver "Criterio de terminalidad" más abajo). La decisión debe apoyarse en informes médico, psicológico y social.
- **Procesados:** no aplica el art. 32 como base principal. El fundamento se construye sobre el art. 3 Ley 24.660 (alojamiento diferenciado) y las normas del código procesal sobre excarcelación y prisión preventiva.
- **Art. 56 bis:** no regula la domiciliaria por razones médicas. Establece la exclusión de determinados beneficios del período de prueba para condenados por delitos graves. No citarlo como fundamento de la domiciliaria médica.

**Criterio de terminalidad:** el art. 33 Ley 24.660 regula la libertad asistida y no contiene una definición legal de "enfermedad terminal" ni establece el plazo de seis meses como criterio normativo expreso. El parámetro de aproximadamente seis meses de sobrevida como indicador de terminalidad es de elaboración jurisprudencial, construido como criterio interpretativo de la excepcionalidad requerida por la ley para autorizar medidas de egreso anticipado. En el informe médico-legal, consignar el pronóstico de vida con el sustento clínico correspondiente e indicar si el caso se ajusta al criterio jurisprudencial, identificando el fallo aplicable en el distrito.

```
[INSERTAR FALLO VERIFICADO: criterio de terminalidad / sobrevida estimada - jurisprudencia de la Cámara o el tribunal del distrito requirente]
```

**Normativa aplicable:** art. 32 Ley 24.660 [VERIFICAR VIGENCIA: Ley 24.660 y modificatorias, especialmente Ley 26.472] + criterios del SPF para alojamiento. El art. 33 regula la libertad asistida; se cita en este contexto solo en tanto la jurisprudencia lo ha empleado como base interpretativa para el criterio de terminalidad (ver bloque anterior).

**Criterios médico-legales:** gravedad de la patología, carácter terminal o no, disponibilidad de tratamiento en el SPF, riesgo para la vida o integridad del interno de continuar detenido.

```
[VERIFICAR VIGENCIA: art. 32 Ley 24.660 - Ley 26.472 y modificatorias. El art. 33 se verifica solo en tanto la jurisprudencia del distrito lo emplee como base interpretativa del criterio de terminalidad]
```

### Protocolo de Estambul (abuso de la fuerza en detenidos)

**Objeto:** documentar y evaluar denuncias de tortura, trato cruel, inhumano o degradante en personas privadas de la libertad, conforme los estándares del Manual para la Investigación y Documentación Eficaces de la Tortura y otros Tratos o Penas Crueles, Inhumanos o Degradantes (Protocolo de Estambul - ONU, 1999).

**Estándares aplicables:** el informe debe seguir la metodología del Protocolo de Estambul: entrevista clínica estructurada, examen físico completo, evaluación psicológica, documentación fotográfica cuando corresponda, análisis de consistencia entre el relato y los hallazgos.

**Criterios de consistencia:** el informe debe pronunciarse sobre si los hallazgos físicos y psicológicos son consistentes, posibles o no consistentes con el mecanismo de producción alegado.

```
[REFERENCIA: Manual para la Investigación y Documentación Eficaces de la Tortura - Protocolo de Estambul - ONU 1999 - HR/P/PT/8/Rev.1]
```

### Praxis médica (arts. 84, 94 CP)

**Objeto de la pericia:** determinar si la conducta del profesional de la salud imputado se ajustó a la lex artis; si hubo negligencia, imprudencia o impericia; el nexo causal entre esa conducta y el resultado (muerte o lesiones).

**Elementos a evaluar:**
- Historia clínica completa (aportar copia íntegra) - Ley 26.529 [VERIFICAR VIGENCIA] regula la obligación de documentación y el derecho de acceso
- Protocolo quirúrgico si corresponde
- Consentimiento informado (Ley 26.529)
- Conducta esperada según estándares de la especialidad
- Nexo causal entre la conducta y el daño

```
[VACÍO PROBATORIO: historia clínica completa no aportada - es elemento indispensable para evaluar praxis médica]
```

---

## Fuero civil - normativa y criterios

### Amparos de salud

**Normativa aplicable:**
- Art. 43 CN (acción de amparo)
- Art. 36 inc. 2° CPCCN (facultades ordenatorias e instructorias del juez - medidas para mejor proveer)
- Art. 473 CPCCN (explicaciones al perito, nueva pericia o ampliación sobre dictamen ya producido - no regula la designación inicial de oficio)
- Ley 24.901 (sistema de prestaciones básicas para personas con discapacidad)
- Ley 26.682 (marco regulatorio de medicina prepaga)
- Ley 16.986 (amparo ante justicia federal y nacional - verificar competencia antes de aplicar: si el amparo tramita ante juez federal, aplica Ley 16.986; si tramita ante juez civil ordinario, aplicar vía ordinaria CPCCN o régimen local)
- Leyes 23.660 y 23.661 (obras sociales y ANSSAL)

**Objeto habitual de la pericia:** acreditar la existencia y gravedad de la patología; determinar si la prestación reclamada es médicamente necesaria e indicada; evaluar si existe alternativa terapéutica equivalente cubierta.

**Criterios médico-legales:**
- Diagnóstico certero con respaldo documental
- Indicación médica de la prestación reclamada según evidencia científica actualizada
- Inexistencia de alternativa equivalente cubierta por el plan o la obra social
- Urgencia o carácter vital de la prestación cuando se solicita cautelar

**Estado de la Ley 26.682 y del PMO (a mayo de 2026):** la Ley 26.682 se encuentra vigente y continúa imponiendo, como mínimo, la cobertura del Programa Médico Obligatorio (PMO) según resolución del Ministerio de Salud. Hubo anuncios y resoluciones de 2025-2026 sobre modificaciones estructurales del PMO, pero sin alteración general de la cobertura básica de uso habitual (consultas, estudios de indicación clásica, medicamentos de lista básica, internaciones). Verificar en cada causa la resolución PMO vigente al momento del reclamo, en particular si la prestación en disputa es de cobertura recientemente incorporada o modificada.
- Ministerio de Salud / PMO: https://www.argentina.gob.ar/salud
- Superintendencia de Servicios de Salud: https://www.sssalud.gob.ar

```
[VERIFICAR VIGENCIA: PMO - resolución vigente al momento del reclamo - prestaciones recientemente incorporadas o modificadas requieren verificación puntual]
```

### Daños y perjuicios en casos de salud (responsabilidad civil médica)

**Normativa aplicable:**
- Ley 26.529 (derechos del paciente, historia clínica y consentimiento informado) [VERIFICAR VIGENCIA]
- Ley 17.132 (ejercicio de la medicina) [VERIFICAR VIGENCIA]
- Ley 26.994 (CCCN - arts. 1710 y ss., 1724, 1725, 1726, 1728 [responsabilidad contractual - aplicar si existe contrato de prestación médica], 1737 y ss.)

**Nota:** para los elementos de documentación (historia clínica, protocolo quirúrgico, consentimiento informado), los criterios son equivalentes a los aplicables en el fuero penal. La diferencia es el encuadre jurídico del resultado: tipo penal culposo (arts. 84 y 94 CP) en sede penal vs. responsabilidad civil en sede civil. Ver también sección "Praxis médica (arts. 84, 94 CP)".

**Objeto de la pericia:** determinar si hubo apartamiento de la lex artis; el nexo causal entre ese apartamiento y el daño; la entidad y extensión del daño (incapacidad, tratamientos futuros, gastos).

**Elementos indispensables:**
- Historia clínica completa del período relevante
- Protocolos quirúrgicos y de anestesia si corresponde
- Consentimiento informado firmado
- Estudios complementarios de la época del hecho y posteriores

**Baremo:** para la cuantificación de incapacidades en el fuero civil se aplican distintos criterios según el juzgado y la sala de la Cámara. Verificar el baremo utilizado habitualmente por el tribunal requirente antes de cuantificar.

```
[VACÍO PROBATORIO: historia clínica completa no aportada - sin este elemento no es posible evaluar la conducta médica ni establecer nexo causal]
```

---

## Fuero de la seguridad social - normativa y criterios

### Invalidez previsional (arts. 48, 49 y concordantes Ley 24.241)

**Normativa aplicable:**
- Ley 24.241 (SIJP) arts. 48 y 49 [VERIFICAR VIGENCIA: modificatorias y decretos reglamentarios]
- Resoluciones ANSES sobre procedimiento de evaluación de invalidez
- Criterios del cuerpo médico pericial para evaluación de incapacidad laboral

**Concepto de invalidez (art. 48 Ley 24.241):** se considera inválido el afiliado que padezca una incapacidad física o intelectual total, que le impida desempeñar cualquier actividad remunerada en forma regular. El umbral legal es el 66% o más de incapacidad (equivalente a dos tercios de la capacidad laborativa).

**Régimen transitorio/definitivo:** el beneficio se otorga inicialmente como retiro transitorio por invalidez por 3 años. Al vencimiento, la comisión médica evalúa: (a) rehabilitado - cesa el beneficio; (b) con posibilidad de rehabilitarse - prórroga de 2 años como transitorio; (c) sin posibilidad de rehabilitarse - se convierte en retiro definitivo por invalidez.

**Objeto de la pericia:** determinar si el afiliado padece una incapacidad laborativa total y permanente que alcance el 66% según el baremo aplicable; la fecha de inicio de la invalidez; el carácter definitivo o transitorio.

**Baremo aplicable según régimen:**
- *Riesgos del trabajo:* rige la Tabla de Evaluación de Incapacidades Laborales aprobada por Decreto 549/2025, de aplicación nacional desde febrero de 2026 para valuaciones no resueltas con anterioridad. Reemplazó al Decreto 659/1996.
- *Pensiones no contributivas por invalidez laboral (ANDIS):* la Resolución 187/2025 ANDIS que aprobó un baremo específico fue derogada por la Resolución 1172/2025. A la fecha, la evaluación se basa en criterios médicos generales sin baremo numérico unificado.
- *Invalidez previsional general (jubilaciones, retiro por invalidez Ley 24.241):* el criterio es propio de cada organismo o tribunal. Verificar resoluciones ANSES vigentes a la fecha del dictamen.

**Derechohabientes (art. 49 Ley 24.241):** en causas de pensión por fallecimiento, la pericia puede ser requerida para acreditar la incapacidad del derechohabiente que fundamenta su derecho a pensión o para acreditar la causa de muerte y su relación con la actividad laboral.

**Criterios del cuerpo médico pericial para dictamen de seguridad social por invalidez:**
- Diagnóstico con respaldo en estudios complementarios actualizados
- Evaluación funcional de la incapacidad (no solo diagnóstico)
- Fecha de inicio estimada de la incapacidad
- Carácter permanente o transitorio
- Porcentaje de incapacidad según baremo

*Nota sobre Ley 27.260:* la norma instituyó el Programa Nacional de Reparación Histórica y la Pensión Universal para el Adulto Mayor (PUAM), y autorizó la transformación de ciertas pensiones no contributivas por invalidez en PUAM. No modifica el contenido ni la metodología de la pericia de invalidez (criterio diagnóstico, baremo, porcentaje, fecha de inicio). Su relevancia es de política previsional, no médico-legal. Aplicable solo si la causa involucra la transformación del tipo de prestación.

```
[VERIFICAR VIGENCIA: arts. 48, 49 Ley 24.241 - baremo aplicable según régimen (Decreto 549/2025 para LRT / verificar ANSES y ANDIS para otros regímenes) - resoluciones ANSES sobre evaluación de invalidez]
```

### Articulación con dictámenes previos de la SRT / Comisiones Médicas (Ley 27.348)

En causas originadas en riesgos del trabajo o en contingencias laborales, la Ley 27.348 establece las comisiones médicas de la SRT como instancia administrativa previa. Es habitual que el informe pericial judicial se produzca luego de un dictamen previo de la SRT (incluyendo Informes de Valoración del Daño - IVD, regulados por Resolución SRT 5/2026 y normas concordantes).

El informe médico-legal debe:
- Referir la existencia del dictamen previo (número de trámite, fecha, organismo emisor, conclusión principal) sin reproducirlo íntegramente.
- Indicar expresamente si es concordante o discrepante con la conclusión pericial propia, fundando las coincidencias o diferencias en términos clínicos, metodológicos y de criterio de valoración.
- Si se adopta parcialmente como base complementaria, señalarlo. Si se rechaza o modifica, exponer las razones técnicas con precisión.
- Dejar constancia de que el dictamen de la SRT o Comisión Médica integra el expediente pero no vincula la independencia del perito médico forense.

```
[VERIFICAR VIGENCIA: Ley 27.348 y Resolución SRT 5/2026 (procedimiento de comisiones médicas e IVD) - verificar resoluciones SRT vigentes al momento del dictamen]
```

---

## Casos federales especiales

### Fuero penal federal

**Tortura, apremios ilegales y malos tratos en detención**
Objeto de pericia: constatar lesiones, secuelas físicas y psíquicas, compatibilidad con el relato, cronología lesional y signos de violencia institucional.
Ejes de conclusión: compatibilidad/incompatibilidad con el relato, antigüedad probable, mecanismo lesivo, necesidad de atención, secuelas y grado de consistencia con el Protocolo de Estambul.

**Violencia institucional por fuerzas federales**
Objeto de pericia: evaluar lesiones por uso de la fuerza, armas menos letales, sujeciones, traslados, cacheos o condiciones de custodia.
Ejes de conclusión: patrón lesional, correspondencia con el mecanismo alegado, proporcionalidad médico-legal, riesgo vital o secuelas, documentación fotográfica o clínica relevante.

**Lesiones en contexto penitenciario federal**
Objeto de pericia: determinar entidad, data, gravedad, evolución y secuelas de lesiones sufridas dentro de unidades federales.
Ejes de conclusión: días de incapacidad, peligrosidad para la vida o integridad, compatibilidad con el mecanismo referido, necesidad de internación o seguimiento.

**Capacidad para declarar en imputados, víctimas o testigos vulnerables**
Objeto de pericia: valorar aptitud psicofísica, comprensión, atención, memoria, orientación y posibilidad de brindar declaración válida. Para los criterios generales de esta evaluación, ver sección "Capacidad para declarar (arts. 79, 239 y 294 CPPN)". En causas del fuero federal con víctimas o testigos vulnerables, considerar adicionalmente la necesidad de apoyos, adaptaciones del entorno de la declaración y carácter transitorio o persistente de la afectación.
Ejes de conclusión: capacidad actual, limitaciones concretas, conveniencia de apoyos, carácter transitorio o persistente de la afectación.

**Imputabilidad, estado de conciencia o crisis aguda al momento del hecho**
Objeto de pericia: analizar trastornos mentales, intoxicaciones, descompensaciones o alteraciones del estado psíquico al momento del hecho.
Ejes de conclusión: existencia del trastorno, incidencia en comprensión y autodeterminación, necesidad de evaluación psiquiátrica complementaria.

### Ejecución penal federal

**Prisión domiciliaria por enfermedad**
Objeto de pericia: establecer si la patología es grave, crónica, discapacitante o incompatible con la vida intramuros.
Ejes de conclusión: riesgo actual, autonomía funcional, requerimientos terapéuticos, pronóstico, necesidad de cuidados permanentes y factibilidad material de control domiciliario.

**Agravamiento de salud en contexto de encierro**
Objeto de pericia: valorar si la detención agrava enfermedad física o mental preexistente.
Ejes de conclusión: relación entre encierro y evolución clínica, riesgo de descompensación, continuidad asistencial y medidas urgentes recomendables.

**Aptitud para permanecer detenido o para traslados**
Objeto de pericia: determinar si el estado clínico permite traslado, comparendo o permanencia en la unidad.
Ejes de conclusión: estabilidad hemodinámica, riesgo de descompensación, necesidad de ambulancia o internación, restricciones concretas.

### Niñez, discapacidad y salud

**Niños, niñas y adolescentes con medidas federales o institucionales**
Objeto de pericia: establecer estado de salud, secuelas, impacto psíquico, capacidad funcional y necesidades asistenciales.
Ejes de conclusión: vulnerabilidad, dependencia de terceros, alcance del daño, urgencia de tratamiento y adecuación de las medidas de protección.

**Discapacidad y cobertura de prestaciones esenciales**
Objeto de pericia: evaluar si existe discapacidad, dependencia, necesidad de apoyos, rehabilitación o medicación.
Ejes de conclusión: diagnóstico funcional, limitaciones concretas, prestaciones indispensables, riesgo por interrupción del tratamiento.

### Materias federales especiales

**Migración y control fronterizo con lesión o crisis médica**
Objeto de pericia: constatar estado de salud, aptitud para viajar, necesidad de asistencia y posible vulneración sanitaria.
Ejes de conclusión: urgencia, riesgo de agravamiento, necesidad de derivación, compatibilidad con traslado o permanencia.

**Hechos con intervención de fuerzas federales y personas vulnerables**
Objeto de pericia: analizar lesiones, estado mental, vulnerabilidad previa y daño sobreviniente en mujeres, personas mayores, personas con discapacidad o privados de libertad.
Ejes de conclusión: vulnerabilidad, nexo causal, secuelas, proporcionalidad del daño, necesidades de protección.

**Muertes en custodia o hallazgo de cadáver en ámbito federal**
Objeto de pericia: establecer causa, mecanismo y data de muerte; lesiones externas e internas; signos de intervención.
Ejes de conclusión: etiología médico-legal, relación entre lesiones y muerte, signos de violencia, necesidad de estudios complementarios.

### Matriz de análisis para casos federales especiales

Aplicar en todos los casos de esta sección:

1. **Objeto de pericia:** qué se pretende probar técnicamente según el requerimiento.
2. **Hallazgos relevantes:** lesiones, clínica, examen mental, estudios complementarios.
3. **Compatibilidad médico-legal:** con el relato, el mecanismo alegado y la cronología.
4. **Riesgo actual:** vida, integridad, secuelas, agravamiento.
5. **Conclusión:** respuesta puntual, clara y delimitada a cada eje requerido.

---

## Reglas de citación - medicina legal

**Normas procesales:** en la primera mención, agregar [VERIFICAR VIGENCIA]. Identificar siempre el fuero al que corresponde la norma citada (CPPN/CPPF / CPCCN / Ley 24.655).

**Jurisprudencia:** nunca citar expediente, sala o carátula sin material aportado. Usar:
```
[INSERTAR FALLO VERIFICADO: doctrina requerida - fuero y sala]
```

**Baremos:** no aplicar baremo sin verificar cuál usa el tribunal requirente. Usar:
```
[VERIFICAR BAREMO: indicar qué baremo aplica el tribunal requirente para este tipo de causa]
```

**Documentación médica:** no asumir diagnósticos, tratamientos ni evoluciones sin constancia documental. Usar:
```
[VACÍO PROBATORIO: constancia médica no aportada - descripción de lo que falta y su relevancia]
```

**Dictámenes anteriores del cuerpo médico pericial:** no asumir el contenido de dictámenes anteriores del mismo organismo sin que sean aportados. Usar:
```
[VACÍO PROBATORIO: dictamen anterior del cuerpo médico pericial no aportado - aportar para evaluar evolución]
```

---

## Lógica de análisis por institución

### Antes de redactar cualquier informe

1. Identificar el fuero y la norma procesal aplicable (CPPN/CPPF / CPCCN / Ley 24.655)
2. Verificar que el oficio identifica claramente los puntos periciales
3. Listar la documentación aportada y detectar vacíos probatorios
4. Identificar si hay dictámenes anteriores del cuerpo médico pericial sobre el mismo sujeto
5. Verificar si la causa tiene detenidos o plazos procesales urgentes

### Checklist de cierre del informe

Antes de finalizar cualquier informe verificar:
- ¿Todos los puntos periciales tienen respuesta en las conclusiones?
- ¿Cada conclusión tiene respaldo en las consideraciones médico-legales?
- ¿Los vacíos probatorios están identificados y su impacto en las conclusiones está explicitado?
- ¿El lenguaje de las conclusiones es comprensible para un juez no médico?
- ¿El informe identifica el número de causa y carátula correctamente?

---

## Instrucciones operativas específicas

- Identificar el fuero antes de seleccionar la normativa aplicable.
- No cuantificar incapacidades sin verificar el baremo utilizado por el tribunal requirente.
- En causas penales con detenidos: priorizar el informe y alertar sobre plazos procesales.
- En amparos de salud: el carácter urgente de la prestación es un dato médico-legal relevante para la cautelar; consignarlo expresamente si surge de la evaluación.
- En praxis médica y daños: la historia clínica completa es presupuesto de admisibilidad del análisis; sin ella, el informe debe limitarse a señalar la imposibilidad de concluir.
- En causas de seguridad social por invalidez: el porcentaje de incapacidad y la fecha de inicio son los dos datos determinantes para el derecho; deben estar consignados con precisión.
- No asumir el contenido de estudios complementarios, historias clínicas, dictámenes anteriores ni resoluciones administrativas sin que sean aportados.

Todo informe cierra con verificación de:
- Fuero y norma procesal aplicable
- Puntos periciales respondidos (todos / parcialmente / con reservas por vacíos probatorios)
- Documentación aportada completa / incompleta
- Baremo aplicado (si corresponde cuantificación)
- Plazos procesales urgentes (si los hay)

---

## Fuentes primarias

- **CPPN:** https://www.saij.gob.ar (Ley 23.984 y modificatorias)
- **CPCCN:** https://www.saij.gob.ar (Ley 17.454 y modificatorias)
- **Ley 24.241 (SIJP):** https://www.saij.gob.ar
- **ANSES - normativa de seguridad social:** https://www.anses.gob.ar
- **Protocolo de Estambul:** https://www.ohchr.org/es/publications/professional-interest/istanbul-protocol
- **Cuerpo Médico Forense - CSJN:** https://www.csjn.gov.ar → menú institucional → Cuerpo Médico Forense (ruta alternativa verificada: https://www.csjn.gov.ar/cmfcs/files/instituto.htm) [VERIFICAR URL]
- **SAIJ (digesto normativo nacional):** https://www.saij.gob.ar

---

## Alcance provincial

Este perfil cubre la justicia nacional y federal. Para uso ante fueros provinciales, el código procesal aplicable no es el CPPN ni el CPCCN sino el código de la provincia correspondiente. Las normas de fondo (CP, Ley 24.241, Ley 24.660, Ley 26.529) son nacionales y aplican en ambos ámbitos; las normas procesales no.

```
[COMPLETAR PARA USO PROVINCIAL: identificar el código procesal penal provincial, el código procesal civil provincial y el estatuto del cuerpo médico pericial del Poder Judicial provincial. Las citas al CPPN y al CPCCN que figuran en este perfil no aplican en el fuero provincial salvo que el código local remita supletoriamente a ellos. Verificar antes de usar.]
```

---


*Normativa base: CPPN (Ley 23.984), CPPF (Ley 27.063), CPCCN (Ley 17.454), CP (Ley 11.179), Ley 24.241, Ley 24.660 (art. 32, mod. Ley 26.472; art. 33 con alcance interpretativo jurisprudencial), Ley 26.529, Ley 26.682, Leyes 23.660 y 23.661, Protocolo de Estambul (ONU 1999)*
*Colaboración técnica: Dr. Alberto Miceli - Médico Forense*
*Autor: Dr. Cristian Aboitiz · [@abogadoaboitiz](https://x.com/abogadoaboitiz)*
