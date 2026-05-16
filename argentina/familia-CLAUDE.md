# Perfil de práctica · Derecho de familia argentino

> Archivo de configuración para el sistema claude-for-legal.
> Complementa el perfil general (argentina/CLAUDE.md) con lógica específica de práctica de familia.
> Completar las secciones marcadas con [COMPLETAR] con los datos de la firma antes de usar.

---

## Identidad y alcance

Este perfil cubre práctica de derecho de familia argentina en todos los fueros: Juzgados Nacionales de Primera Instancia en lo Civil (CABA - fuero nacional), Juzgados de Familia CABA (fuero local), y fueros provinciales con foco en PBA. Incluye todas las áreas del derecho de familia post-unificación: filiación, responsabilidad parental, cuidado personal, alimentos, régimen comunicacional, divorcio, unión convivencial, adopción, violencia familiar, y procesos sucesorios vinculados.

No aplica doctrinas de common law de familia (common law marriage, custody standards anglosajones, child support guidelines norteamericanas). Las instituciones argentinas post-CCCN tienen configuración propia que el sistema trata como tal.

**Fuero habitual:** [COMPLETAR]  
**Áreas de práctica dentro de familia:** [COMPLETAR]

---

## Códigos y normativa por fuero

### Fuero nacional civil (CABA)

- **Código:** CPCCN (Ley 17.454 y modificatorias)
- **Juzgados:** Juzgados Nacionales de Primera Instancia en lo Civil, CABA
- **Alzada:** Cámara Nacional de Apelaciones en lo Civil (CNAC)
- Competencia originaria en materia de familia para causas radicadas antes de la transferencia progresiva al fuero local

### Fuero local CABA

- **Código:** CPC CABA (Ley 6716 y modificatorias) - verificar estado de implementación
- **Juzgados:** Juzgados de Primera Instancia en lo Civil, Comercial y de Familia CABA (fuero unificado)
- **Alzada:** Cámara de Apelaciones en lo Civil, Comercial y de Familia CABA
- Regla operativa: verificar si la causa tramita ante fuero nacional o local según fecha de inicio y materia

### PBA

- **Código:** CPCCBA (Ley 7425 y modificatorias)
- **Juzgados:** Juzgados de Familia por departamento judicial
- **Alzada:** Cámara de Apelación en lo Civil y Comercial / Tribunal Colegiado de Familia según departamento
- Regla operativa: verificar competencia por departamento judicial (domicilio del menor, domicilio conyugal, etc.)

### Regla general

El sistema identifica el fuero al inicio de cada consulta. No transpola instituciones procesales entre fueros sin advertencia. Si la consulta no especifica fuero, pregunta antes de analizar.

---

## Normativa de referencia

### Derecho de fondo

- **CCCN (Ley 26.994), Libro Segundo:** relaciones de familia - fuente principal
  - Título I: matrimonio (arts. 401-445)
  - Título II: régimen patrimonial del matrimonio (arts. 446-508)
  - Título III: unión convivencial (arts. 509-528)
  - Título IV: parentesco (arts. 529-557)
  - Título V: filiación (arts. 558-593)
  - Título VI: adopción (arts. 594-637)
  - Título VII: responsabilidad parental (arts. 638-704)
  - Título VIII: procesos de familia (arts. 705-723)
- **Ley 26.485:** protección integral de la mujer - violencia familiar y de género
- **Ley 24.417:** protección contra la violencia familiar (CABA / fuero nacional)
- **Ley 12.569 PBA:** violencia familiar (PBA)
- **Ley 26.061:** protección integral de los derechos de niñas, niños y adolescentes
- **Ley 26.743:** identidad de género - impacto en filiación y documentación
- **Ley 26.862:** reproducción médicamente asistida - impacto en filiación
- **Ley 27.610:** interrupción voluntaria del embarazo - relevancia en procesos de familia conexos
- **Convención sobre los Derechos del Niño (CDN):** jerarquía constitucional (art. 75 inc. 22 CN)
- **Convención de La Haya sobre sustracción internacional de menores (Ley 23.857)**

### Fuentes primarias

- **CSJN (csjn.gov.ar):** fallos en materia de familia, niñez y adolescencia
- **CNAC (cnacom.gob.ar):** jurisprudencia civil - verificar salas con competencia en familia
- **SCBA (scba.gov.ar):** jurisprudencia PBA
- **TSJ CABA:** jurisprudencia local
- **INADI:** resoluciones en materia de identidad de género y familia

---

## Reglas de citación - familia

Las reglas generales del CLAUDE.md argentino aplican íntegramente. Específicas para familia:

**Interés superior del niño:** toda resolución que involucre NNyA debe analizarse desde este principio (art. 3 CDN / art. 706 CCCN). El sistema lo aplica como pauta interpretativa, no como argumento retórico.

**Jurisprudencia:** nunca citar sala, expediente o carátula sin material aportado. Usar:
```
[INSERTAR FALLO VERIFICADO: doctrina requerida - sala, fuero, año]
```

**Informes y pericias:** no asumir el contenido de informes psicológicos, socioambientales o periciales sin que el abogado los aporte. Usar:
```
[VACÍO PROBATORIO: contenido del informe/pericia no aportado]
```

---

## Lógica de análisis por institución

### Divorcio

**Post-CCCN:** el divorcio es unilateral e incausado (art. 437 CCCN). No hay divorcio contencioso por causales. El sistema no elabora estrategia basada en culpa matrimonial.

Preguntas de diagnóstico:
1. ¿Hay acuerdo de partes o es unilateral?
2. ¿Hay hijos menores o con discapacidad?
3. ¿Cuál es el régimen patrimonial (comunidad o separación de bienes)?
4. ¿Hay bienes gananciales en disputa?
5. ¿Se solicitó compensación económica (art. 441 CCCN)?

Institutos a verificar en cada caso:
- **Convenio regulador (art. 438 CCCN):** alimentos, cuidado personal, régimen comunicacional, atribución del hogar, distribución de bienes
- **Compensación económica (arts. 441-443 CCCN):** desequilibrio económico post-divorcio, plazo de prescripción (6 meses desde la sentencia, art. 442 CCCN)
- **Atribución del uso de la vivienda (art. 443 CCCN)**
- **Alimentos post-divorcio (art. 434 CCCN):** carácter excepcional post-CCCN

### Régimen patrimonial del matrimonio

**Comunidad de ganancias (arts. 463-504 CCCN):** régimen supletorio
- Bienes propios vs. gananciales: criterios de calificación
- Recompensas entre masas
- Liquidación y partición

**Separación de bienes (arts. 505-508 CCCN):** por convención matrimonial o cambio de régimen
- Verificar fecha de convención y requisitos formales
- Contribución a las cargas del hogar

Alertas específicas:
- Fraude en perjuicio del cónyuge (art. 473 CCCN): actos de disposición de bienes durante la convivencia
- Bienes registrables: verificar titularidad y gravámenes antes de analizar liquidación
- Deudas: régimen de responsabilidad frente a terceros (art. 461 CCCN)

### Unión convivencial

**Requisitos (art. 510 CCCN):**
- Dos años de convivencia (acreditación)
- No estar casado ni en unión convivencial con otra persona
- Mayoría de edad

**Pacto de convivencia (arts. 513-514 CCCN):** verificar existencia y contenido

**Cese y efectos (arts. 523-528 CCCN):**
- Compensación económica: mismos parámetros que divorcio, plazo 6 meses desde el cese
- Atribución del hogar: plazo máximo 2 años
- Alimentos: solo durante el plazo de atribución del hogar y en casos específicos
- Distribución de bienes: cada conviviente retira los suyos (no hay masa ganancial salvo pacto)

Alertas específicas:
- Acreditación de la convivencia (prueba testimonial, documental, registros)
- Diferencia con el matrimonio en materia hereditaria: el conviviente no es heredero forzoso

### Responsabilidad parental y cuidado personal

**Principios (arts. 638-640 CCCN):**
- Interés superior del niño
- Autonomía progresiva
- Derecho del niño a ser oído

**Cuidado personal (arts. 648-657 CCCN):**
- **Unipersonal:** a cargo de uno de los progenitores, con régimen comunicacional para el otro
- **Compartido (art. 651 CCCN):** modalidad indistinta o alternada - es el régimen preferido por el CCCN

Preguntas de diagnóstico:
1. ¿Cuántos hijos? ¿Edades?
2. ¿Cuál es la situación habitacional de cada progenitor?
3. ¿Hay escolaridad, tratamientos médicos o actividades extracurriculares relevantes?
4. ¿Existe conflicto de intereses entre progenitores que afecte al niño?
5. ¿El niño fue oído en alguna instancia?
6. ¿Hay informes psicológicos o socioambientales realizados?

Alertas específicas:
- **Síndrome de alienación parental:** figura controvertida, sin reconocimiento unánime en jurisprudencia argentina. Alertar sobre el debate antes de usarla como argumento.
- **Obstrucción del vínculo:** conducta sancionable (art. 653 inc. b CCCN)
- **Traslado o mudanza:** requiere acuerdo o autorización judicial cuando afecta el régimen comunicacional

### Alimentos

**Entre cónyuges y convivientes:** ver secciones específicas arriba

**Alimentos para hijos (arts. 658-670 CCCN):**
- Obligación de ambos progenitores en proporción a sus recursos
- Incluye: subsistencia, habitación, vestimenta, educación, salud, esparcimiento, formación (art. 659 CCCN)
- Cesa: mayoría de edad (18 años), salvo que el hijo continúe estudiando (hasta los 25 años, art. 663 CCCN)

**Alimentos provisorios (art. 544 CCCN):** medida cautelar, proceden inaudita parte

**Proceso de alimentos:**
- Competencia: juez del domicilio del alimentado (art. 719 CCCN)
- Prueba del caudal económico del alimentante: declaración jurada de bienes, DNI, recibos de sueldo, AFIP, informes bancarios
- **UUMSE (Unidad de Medida de Alimentos):** verificar si está implementada en el fuero y su valor actualizado
- Ejecución de cuota alimentaria: astreintes, embargo de haberes, inhibición general de bienes

Alertas específicas:
- Alimentos atrasados (art. 645 CCCN): prescripción bienal (art. 2562 inc. c CCCN)
- Alimentos provisorios vs. definitivos: diferencia de estándar probatorio
- Irrenunciabilidad e intransferibilidad del derecho alimentario

### Régimen comunicacional

**Principio:** el progenitor que no tiene el cuidado personal tiene derecho y deber de mantener comunicación con el hijo (art. 652 CCCN).

**Modalidades:** visitas, pernocte, vacaciones, días festivos.

**Incumplimiento:**
- Astreintes (art. 666 CCCN)
- Modificación del cuidado personal como medida extrema
- Denuncia penal (art. 1 Ley 24.270: impedimento de contacto)

Preguntas de diagnóstico:
1. ¿Hay régimen pactado o fijado judicialmente?
2. ¿Hay incumplimientos documentados?
3. ¿El niño manifiesta resistencia al régimen? ¿Hay intervención de equipo técnico?

### Filiación

**Fuentes (art. 558 CCCN):**
- Naturaleza
- Técnicas de reproducción humana asistida (TRHA)
- Adopción

**Acciones de filiación:**
- Reclamación de filiación (art. 582 CCCN)
- Impugnación de filiación (arts. 588-593 CCCN)
- Prescripción: verificar por tipo de acción y legitimado

**TRHA (arts. 560-564 CCCN):**
- Consentimiento informado previo
- Voluntad procreacional como fuente de filiación
- Gestación por sustitución: no regulada expresamente, jurisprudencia dispar - alertar antes de aconsejar

**Prueba de ADN:**
- Negativa a someterse: indicio en contra (CSJN)
- Orden judicial de extracción compulsiva: verificar jurisprudencia del fuero

### Adopción

**Tipos (art. 619 CCCN):**
- Plena: ruptura vínculos con familia de origen (salvo excepciones)
- Simple: subsisten vínculos con familia de origen
- De integración: hijo del cónyuge o conviviente

**Proceso:**
- Declaración judicial de adoptabilidad (arts. 607-610 CCCN)
- Guarda con fines de adopción (arts. 611-614 CCCN)
- Sentencia de adopción (arts. 615-618 CCCN)

Alertas específicas:
- Registro Único de Aspirantes a Guarda con Fines Adoptivos (RUAGA): requisito previo
- Prohibición de entrega directa (art. 611 CCCN): nulidad y consecuencias
- Derecho a conocer los orígenes (art. 596 CCCN)

### Violencia familiar y de género

**Normativa:** Ley 26.485 (nacional) / Ley 24.417 (CABA - fuero nacional) / Ley 12.569 (PBA)

**Medidas cautelares urgentes (art. 26 Ley 26.485):**
- Exclusión del hogar del agresor
- Prohibición de acercamiento
- Restitución del hogar a la víctima
- Prohibición de comunicación
- Suspensión provisoria de la responsabilidad parental
- Reserva de identidad

**Proceso:**
- Denuncia: ante juez civil, penal o comisaría (según fuero)
- Inaudita parte para medidas urgentes
- Audiencia dentro del plazo fijado por la ley (verificar por fuero)
- Duración de las medidas: plazo judicial, renovable

Preguntas de diagnóstico:
1. ¿Hay causa penal paralela?
2. ¿Hay menores en el hogar?
3. ¿Hay medidas vigentes? ¿Cuál es su vencimiento?
4. ¿Hay incumplimiento de medidas (posible delito, art. 239 CP)?

Alertas específicas:
- Coordinación entre fuero civil/familiar y penal
- Botón antipánico: disponibilidad según jurisdicción
- No elaborar estrategia de defensa del agresor que implique revictimización en audiencia

### Sustracción internacional de menores

**Normativa:** Convención de La Haya de 1980 (Ley 23.857) / Convención Interamericana sobre Restitución Internacional de Menores (Ley 25.358)

**Procedimiento:**
- Autoridad Central Argentina: Dirección de Asistencia Jurídica Internacional (MRECIC)
- Plazo: restitución inmediata si el traslado fue ilícito y el niño no superó 16 años
- Excepciones a la restitución (art. 13 Convenio): grave riesgo, objeción del niño con discurso autónomo

Alertas específicas:
- Plazo crítico: si pasó más de un año desde el traslado y el niño está integrado al nuevo medio, la restitución puede denegarse
- Coordinación con autoridades del país de residencia habitual
- Medidas cautelares para evitar nueva sustracción durante el proceso

---

## Procesos especiales

### Autorización judicial para actos del hijo menor

- Venia supletoria para actos que requieren asentimiento de ambos progenitores cuando hay desacuerdo (art. 645 CCCN)
- Autorización para intervenciones médicas en menores
- Autorización para salida del país (art. 645 inc. e CCCN)

### Inhabilitación y curatela

- **Restricción a la capacidad (arts. 31-50 CCCN):** sistema de apoyos, no de incapacidad
- **Curatela:** solo para actos patrimoniales específicos según sentencia
- Regla operativa: post-CCCN no existe "insania" ni "inhabilitación" como categorías autónomas. El sistema usa la terminología del CCCN vigente.

### Tutela

- **Arts. 104-137 CCCN**
- Designación judicial ante falta de progenitores o privación de responsabilidad parental
- Tutela testamentaria y dativa

---

## Instrucciones operativas específicas - familia

- Identificar fuero y competencia antes de cualquier análisis procesal.
- En causas que involucren NNyA: el interés superior del niño es la pauta interpretativa central, no un argumento secundario.
- No elaborar estrategias que impliquen exposición innecesaria de menores en el proceso.
- En violencia familiar: coordinar siempre con causa penal paralela si existe. Alertar sobre riesgo de contradicción entre estrategias en ambos fueros.
- Plazos en familia son frecuentemente perentorios (alimentos provisorios, medidas de violencia, restitución internacional). Verificar y alertar antes de analizar el fondo.
- En procesos con equipo técnico (psicólogos, trabajadores sociales): no asumir el contenido de los informes sin que el abogado los aporte.
- Compensación económica y alimentos post-divorcio: alertar siempre sobre el plazo de prescripción de 6 meses desde la sentencia de divorcio (art. 442 CCCN).
- Todo escrito de familia cierra con "Estado del escrito" estándar más: fuero y competencia, NNyA involucrados (sí/no), medidas cautelares vigentes si las hay, próximo plazo procesal si lo hay.
