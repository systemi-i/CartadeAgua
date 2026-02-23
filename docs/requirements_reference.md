# Carta de Agua — Application Requirements & Form Structure Reference

> Source: Four application templates from different Costa Rican ASADAs:
> 1. ASADA Santa Rosa, Oreamuno, Cartago (AAARSRO-FS-002) — most detailed/formal
> 2. ASADA Puente de Piedra, Grecia, Alajuela — simple requirements sheet
> 3. ASADA San Rafael de Ojo de Agua, Alajuela (Formulario Nº 01) — compact form
> 4. ASADA Poás y Barrio Corazón de Jesús, Aserrí (CDA-ASADAS v2.0 2021) — most comprehensive, federation-standardized
>
> Purpose: Define the canonical data model, validation rules, and regulatory basis for the Nosara carta de agua agentic platform.

---

## 1. REGULATORY BASIS

All forms derive from the **Reglamento de Prestación de Servicios de AyA (RPSAyA)**, specifically:

| Article | Subject |
|---------|---------|
| **Art. 15** | General requirements for all services |
| **Art. 29** | General framework for constancia de disponibilidad |
| **Art. 30** | Admissibility requirements and conditions for the application |
| **Art. 31** | Requirements for registered properties (inmuebles inscritos), fraccionamientos, urbanizaciones |
| **Art. 32** | Requirements for unregistered properties (inmuebles sin inscribir) |
| **Art. 33** | Requirements for State-administered territories with special legal regime |
| **Art. 34** | Requirements for agricultural, livestock, forestry, or mixed-use parcels |
| **Art. 37** | Validity and renewal of constancias |
| **Art. 39–40** | Other types of constancias |
| **Art. 41** | Vigencia (validity period) of constancias |
| **Ley 8220, Art. 6** | Deadline rules — 10 business days to complete missing requirements, or application is denied |

---

## 2. LEGAL DEADLINES (From RPSAyA + Ley 8220)

| Rule | Deadline |
|------|----------|
| Applicant must complete missing requirements | **10 business days** from notification |
| If deadline passes without completion | Application is **automatically denied**; must reapply |
| ASADA resolution for individual cases (single dwelling/commerce) | Up to **15 business days** after complete submission |
| ASADA resolution for urban development/industrial/commercial projects | Up to **20 business days** after complete submission |
| Validity of constancia (single dwelling or individual commerce) | **12 months**, renewable up to **24 months** consecutively |
| Renewal must be requested within | **Last quarter** of the validity period |
| If renewal not requested in time | Constancia **expires (caduca)**; must reapply under current conditions |
| Renewal conditions | Applicant demonstrates concrete progress, project conditions unchanged, technical feasibility still exists |

---

## 3. APPLICATION TYPES (Motivo de Solicitud)

The forms reveal several distinct application tracks, each with different information requirements:

### A. By purpose (visado de planos / land operations)
- **Fraccionamiento / Segregación / Lotificación** — splitting land into lots (must specify lot count)
- **Reunión de Fincas** — merging properties (must specify property count)
- **Rectificación de medidas** — correcting property measurements

### B. By construction purpose
- **Nuevo proyecto constructivo** — new construction project
- **Remodelación** — remodeling
- **Ampliación** — expansion
- **Aumento de unidades habitacionales / incremento del consumo** — increasing units or consumption

### C. First time vs. renewal
- **Por primera vez** — first request
- **Primera renovación** — first renewal
- **Segunda renovación** — second renewal

---

## 4. CANONICAL DATA FIELDS (Union of All Forms)

### Section I — Request Metadata
| Field | Type | Notes |
|-------|------|-------|
| Número de solicitud | Auto-assigned by ASADA | Sequential tracking number |
| Fecha de solicitud | Date | Date of submission |
| Motivo de solicitud | Selection | See application types above |
| Primera vez / Renovación | Selection | First time, 1st renewal, 2nd renewal |
| Existing service on property? | Yes/No | If yes: how many services + abonado numbers |

### Section II — Property Data
| Field | Type | Notes |
|-------|------|-------|
| Naturaleza del inmueble | Selection | Inmueble inscrito / Parcela agrícola / Terreno sin inscribir |
| Título de propiedad | Selection + Number | Folio Real o Matrícula / Título de Propiedad / Contrato-Concesión / Declaración Jurada (Privada o Protocolizada) |
| Plano catastrado | Number | Format: Province-Number-Year (e.g., C-1234567-2020) |
| Plano de agrimensura | Number + Cod ATP | Alternative to plano catastrado for unregistered properties |
| Extensión de la propiedad | Number (m²) | Property area |
| Folio Real | Number | Registry number |
| Derecho de posesión | Text | For possession rights (not registered) |

### Section III — Property Owner / Titular
| Field | Type | Notes |
|-------|------|-------|
| Tipo de titular | Selection | Propietario registral / Representante legal / Albacea / Curador / Tutor / Autorizado legal / Concesionario / Poseedor |
| Nombre (persona física) | Text | Full name (nombre + primer apellido + segundo apellido) |
| Nº de cédula (persona física) | ID Number | Costa Rican cédula |
| Razón social (persona jurídica) | Text | Corporate name |
| Nº de cédula jurídica | ID Number | Corporate ID |
| Representante legal | Text | Name of legal representative (for jurídica) |

### Section IV — Property Location
| Field | Type | Notes |
|-------|------|-------|
| Provincia | Selection | Costa Rica has 7 provinces |
| Cantón | Selection | Dependent on provincia |
| Distrito | Selection | Dependent on cantón |
| Barrio / Sector | Text | Neighborhood or sector name |
| Dirección exacta | Free text | Exact address description |

### Section V — Notification Preferences
| Field | Type | Notes |
|-------|------|-------|
| Correo electrónico (principal) | Email | Primary notification method |
| Teléfono fijo | Phone | |
| Teléfono móvil | Phone | |
| Secondary contact methods | Same fields | Backup notification channel |

### Section VI — Project Description
| Field | Type | Notes |
|-------|------|-------|
| Project classification | Selection | See detailed taxonomy below |
| Project subcategory | Selection | Dependent on classification |
| Cantidad de lotes/fincas/unidades | Number | For developments |
| Área de construcción | Number (m²) | For construction projects |
| Niveles constructivos | Number | Building stories |
| Caudal requerido | Number (L/s) | Required water flow rate (optional for small projects) |
| Descripción del proyecto | Free text | Detailed description in applicant's own words |
| Cantidad de dormitorios | Number | For residential |
| Cantidad de habitaciones | Number | For hotels |
| Cantidad de camas | Number | For hospitals |
| Cantidad de estudiantes | Number | For schools |

### Section VII — Signatures
| Field | Type | Notes |
|-------|------|-------|
| Firma del propietario/representante/autorizado | Signature | Required |
| Firma del funcionario que recibe | Signature | ASADA staff who receives application |
| Fecha de recepción | Date | |

### Section VIII — ASADA Internal Use
| Field | Type | Notes |
|-------|------|-------|
| Cumplimiento de requisitos (checklist) | Checkboxes | Per RPSAyA articles 30–34 |
| Estado de la solicitud | Selection | Aprobado / Denegado |
| Referencia de acta | Text | Board meeting minutes reference |
| Justificación | Free text | Reason for approval/denial |
| Croquis de ubicación | Drawing/Map | Sketch of property location and distribution lines |
| Resultado medición de presión | Number (mca) | Pressure measurement result |
| Fecha de inspección | Date | |
| Hora de inspección | Time | |
| Funcionario de inspección | Text + Signature | Inspector name and signature |

---

## 5. PROJECT CLASSIFICATION TAXONOMY

The most comprehensive form (ASADA Poás, CDA-ASADAS v2.0) provides a detailed project taxonomy. This is the best reference for building the application's project classification logic:

```
├── VIVIENDA UNIFAMILIAR
│   ├── Vivienda en lote individual
│   └── Vivienda en lote de urbanización/condominio
│
├── VIVIENDA MULTIFAMILIAR
│   ├── Apartamentos
│   └── Multifamiliares
│
├── PROYECTO HABITACIONAL
│   ├── Condominio (→ cantidad de lotes/fincas, área, niveles, caudal)
│   ├── Urbanización (→ cantidad de lotes, área, niveles, caudal)
│   ├── Conjunto Residencial (→ cantidad unidades, área, niveles, caudal)
│   └── [Anteproyecto / Proyecto / Modificación]
│
├── LOCAL COMERCIAL Y ALMACENAMIENTO
│   ├── Centro Comercial
│   ├── Local Comercial
│   ├── Supermercado
│   ├── Bodegas
│   ├── Galerón
│   ├── Oficinas
│   └── Parqueos
│
├── FINES TURÍSTICOS Y RECREATIVOS
│   ├── Centro Turístico
│   └── Piscinas
│
├── EXPENDIOS Y MANIPULACIÓN DE ALIMENTOS
│   ├── Bar
│   ├── Restaurante
│   └── Soda
│
├── HOTELES Y SIMILARES
│   ├── Hotel (→ cantidad de habitaciones)
│   ├── Motel
│   └── Cabinas
│
├── EDIFICIOS PARA EDUCACIÓN
│   ├── Escuela
│   ├── Colegio
│   ├── Universidad
│   └── Centro Parauniversitario
│   └── (→ cantidad de estudiantes)
│
├── EDIFICIOS DE ASISTENCIA HOSPITALARIA
│   ├── EBAIS
│   ├── Clínica
│   └── Hospital
│   └── (→ cantidad de camas)
│
├── ESTABLECIMIENTOS INDUSTRIALES
│   ├── Centro de Recuperación Residuos Valorizables
│   ├── Estación de transferencia de Residuos Sólidos
│   ├── Granja Avícola
│   ├── Granja Porcícola
│   ├── Invernadero
│   ├── Zona Franca
│   └── Estación de Servicio / Gas LP / Mixta
│
├── FINES AGRÍCOLAS / PECUARIOS / FORESTALES
│   ├── Terreno agrícola/ganadero
│   ├── Lechería
│   └── (requires municipal authorization if buildings planned)
│
└── OTRO (free text description)
```

---

## 6. REQUIREMENTS BY PROPERTY TYPE (Checklist Logic)

The agent's intake validation must apply different requirement sets depending on property registration status:

### A. Inmueble Inscrito (Registered Property) — Art. 30 RPSAyA
- [ ] Completed and signed application form
- [ ] ID document of owner or legal representative
- [ ] If persona jurídica: personería jurídica certificate (max 30 days old)
- [ ] Certified copy of plano catastrado
  - If no plano catastrado exists: plano de agrimensura per Art. 2 inciso q) Reglamento Ley de Catastro Nacional, with CFIA seal
- [ ] Certificación literal de la propiedad (max 30 days old)
- [ ] No outstanding debt with the ASADA (verified internally)

### B. Inmueble Registrado en Derechos / Fraccionamientos / Urbanizaciones — Art. 31 RPSAyA
- [ ] All items from Art. 30, plus:
- [ ] If copropietarios: certificación registral with list of all derechos + certificación literal of the applicant(s)
- [ ] If segregation: planos de agrimensura of the segregation or related rejection minutes
- [ ] For new fraccionamientos: certified copy of plano padre (previously approved by municipality) + planos de agrimensura of properties to be split

### C. Inmueble Sin Inscribir (Unregistered Property) — Art. 32 RPSAyA
- [ ] Plano catastrado or plano de agrimensura
- [ ] Declaración jurada signed by possessor + 2 witnesses, describing:
  - Nature of the property
  - Possessory acts
  - Existence of buildings
  - Improvements made
  - Statement that property is not registered
- [ ] Subscribed before competent ASADA official
- [ ] ID document of titular or legal representative

### D. State-Administered Territories — Art. 33 RPSAyA
- [ ] Completed and signed application form
- [ ] ID document of owner or legal representative
- [ ] Express authorization from the corresponding State entity

### E. Agricultural / Livestock / Forestry Parcels — Art. 34 RPSAyA
- [ ] Completed and signed application form
- [ ] ID document of owner or legal representative
- [ ] If buildings for residential use planned: municipal authorization per Reglamento de Fraccionamiento y Urbanismo

### F. Special Zones
- [ ] For zones with aquifer vulnerability/risk designation: ASADA verifies existence of hydrogeological study endorsed by SENARA (in the APC platform during plan approval phase)

---

## 7. ASADA-SIDE EVALUATION CRITERIA

Beyond document completeness, the ASADA must verify (from ASADA Puente de Piedra requirements sheet):

1. **Viabilidad técnica del sistema** — Technical feasibility: sufficient water (hídrica) and hydraulic (hidráulica) capacity
2. **No detrimento del servicio** — The new connection must not harm service quality for existing users
3. **Infraestructura existente** — There must be existing pipeline (tubería) in front of the property
4. **Convenio de Delegación vigente** — The ASADA must have a current delegation agreement with AyA

Additional evaluation elements (from Santa Rosa form):
- **Pressure measurement** at the property location (resultado medición de presión in mca)
- **Croquis/sketch** showing property location relative to distribution lines
- **Field inspection** by ASADA staff with date, time, and inspector signature

---

## 8. VALIDITY & RENEWAL RULES

| Aspect | Rule |
|--------|------|
| Constancia validity (individual dwelling/commerce) | 12 months from issuance |
| Maximum consecutive renewal | Up to 24 months total |
| Renewal request window | Must be filed within the **last quarter** of the validity period |
| Renewal conditions | Applicant proves concrete progress on construction, project conditions unchanged, technical feasibility confirmed by operator |
| Expired constancia | Caducidad — must file a **new application** evaluated under **current** system conditions |
| Projects/urbanizaciones/condominios | Must first have project approved by AyA; then ASADA issues the constancia |

---

## 9. CROSS-ASADA PATTERNS & DESIGN NOTES

### What's consistent across all ASADAs (regulatory floor)
- Same core documents required (cédula, plano catastrado, certificación literal)
- Same RPSAyA article references for different property types
- Same legal deadlines (10 days to complete, 15/20 days to resolve)
- Same validity/renewal framework
- Application must be signed by propietario registral, poseedor, or representante legal
- Morosidad check (no outstanding debt) is standard

### What varies by ASADA (local discretion)
- **Form complexity** — ranges from a simple 1-page form to a 5-page structured template
- **Project classification detail** — some ASADAs ask for a simple description; others use the full taxonomy
- **Whether caudal requerido (L/s) is asked** — not all forms include this
- **Whether a purpose letter is required** — Puente de Piedra requires a separate letter from the owner or professional describing the purpose; others embed this in the form
- **Field inspection protocol** — Santa Rosa has a formal pressure measurement and croquis section; others don't
- **Which entity requested the carta** — Puente de Piedra asks applicants to specify who requires it (Municipality, INVU, Colegio de Ingenieros, etc.)

### Implications for Nosara platform
- The agent should implement the **superset of requirements** (based on RPSAyA articles) as the validation baseline.
- Nosara-specific rules (no factibilidad técnica status, local capacity constraints, Board preferences) are layered on top.
- The project classification taxonomy from the Poás/CDA-ASADAS v2.0 form is the most complete and should be the starting reference for the conversational intake flow.
- The agent should ask which **requesting entity** needs the carta (Municipalidad de Nicoya, INVU, CFIA, etc.) — this helps contextualize the application.
- **Renewal tracking** is a built-in automation opportunity: the system can proactively notify applicants when their constancia is approaching the renewal window or expiration.
