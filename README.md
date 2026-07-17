# Sistema Inteligente de Gestión de Alícuotas

> Proyecto académico desarrollado en **Oracle Database** para la gestión administrativa y financiera de una urbanización, integrando SQL avanzado, PL/SQL, ORDS, API REST, JSON, auditoría y un módulo de consultas en lenguaje natural.

---

## Tabla de contenido

- [Descripción general](#descripción-general)
- [Objetivo del proyecto](#objetivo-del-proyecto)
- [Arquitectura general](#arquitectura-general)
- [Tecnologías utilizadas](#tecnologías-utilizadas)
- [Módulos implementados](#módulos-implementados)
- [Modelo lógico del sistema](#modelo-lógico-del-sistema)
- [Tablas principales](#tablas-principales)
- [Flujo funcional](#flujo-funcional)
- [API REST con ORDS](#api-rest-con-ords)
- [Endpoints principales](#endpoints-principales)
- [Ejemplos de consumo en Postman](#ejemplos-de-consumo-en-postman)
- [Consultas avanzadas y reportes](#consultas-avanzadas-y-reportes)
- [PL/SQL, triggers y auditoría](#plsql-triggers-y-auditoría)
- [JSON y consultas en lenguaje natural](#json-y-consultas-en-lenguaje-natural)
- [Estructura sugerida del repositorio](#estructura-sugerida-del-repositorio)
- [Evidencias sugeridas](#evidencias-sugeridas)
- [Autor](#autor)

---

## Descripción general

El **Sistema Inteligente de Gestión de Alícuotas** permite administrar los cobros mensuales de una urbanización o conjunto residencial.

El sistema contempla el registro de propietarios, viviendas, períodos de cobro, alícuotas, pagos, egresos, movimientos de caja, reportes financieros, auditoría y consultas en lenguaje natural.

La lógica principal se encuentra implementada directamente en la base de datos mediante:

- Tablas relacionales normalizadas.
- Consultas SQL avanzadas.
- Índices de optimización.
- Procedimientos y funciones PL/SQL.
- Triggers de auditoría.
- Vistas de reportes.
- Vistas JSON.
- Endpoints REST mediante ORDS.
- Módulo de lenguaje natural preparado para integración con IA.

---

## Objetivo del proyecto

Diseñar e implementar una solución de base de datos para gestionar las alícuotas de una urbanización, permitiendo controlar ingresos, egresos, deudas, pagos, reportes administrativos y consultas inteligentes.

El proyecto busca demostrar el uso de herramientas avanzadas de Oracle Database aplicadas a un caso realista de administración financiera residencial.

---

## Arquitectura general

```txt
Cliente / Navegador / Postman
        |
        v
ORDS - Oracle REST Data Services
        |
        v
API REST
http://localhost:8080/ords/alicuotas/api/
        |
        v
Oracle Database
Esquema: PROY_ALICUOTAS_ASTUDILLO
        |
        v
Tablas, vistas, PL/SQL, triggers, JSON y reportes
```

---

## Tecnologías utilizadas

| Tecnología | Uso en el proyecto |
|---|---|
| Oracle Database | Motor principal de base de datos |
| SQL | Consultas, reportes, joins, agregaciones y filtros |
| PL/SQL | Procedimientos, funciones y lógica de negocio |
| ORDS | Publicación de API REST |
| JSON | Respuestas estructuradas y vistas JSON |
| Postman | Prueba de endpoints REST |
| SQL Developer | Desarrollo y administración de scripts |
| GitHub | Control y presentación del proyecto |

---

## Módulos implementados

- Gestión de urbanización.
- Gestión de propietarios.
- Gestión de viviendas.
- Gestión de períodos mensuales.
- Gestión de alícuotas.
- Registro de pagos.
- Registro de egresos.
- Movimientos de caja.
- Reportes financieros.
- Consulta de deudores.
- Auditoría automática mediante triggers.
- Vistas JSON para intercambio de información.
- API REST con ORDS.
- Módulo de lenguaje natural / IA simulada.

---

## Modelo lógico del sistema

El sistema está basado en una estructura jerárquica y financiera:

```txt
URBANIZACION
     |
     |--- VIVIENDA
              |
              |--- ALICUOTA
                       |
                       |--- PAGO

PROPIETARIO
     |
     |--- VIVIENDA

URBANIZACION
     |
     |--- EGRESO

PAGO y EGRESO
     |
     |--- CAJA_MOVIMIENTO

OPERACIONES IMPORTANTES
     |
     |--- AUDITORIA_SISTEMA
```

---

## Tablas principales

| Tabla | Descripción |
|---|---|
| `URBANIZACION` | Representa el conjunto residencial completo. |
| `PROPIETARIO` | Registra los datos de los dueños o responsables de viviendas. |
| `VIVIENDA` | Representa casas, departamentos o locales dentro de la urbanización. |
| `PERIODO` | Define el mes y año de cobro. |
| `ALICUOTA` | Registra el valor mensual que debe pagar cada vivienda. |
| `PAGO` | Guarda los pagos realizados por los propietarios. |
| `EGRESO` | Registra gastos comunes de la urbanización. |
| `CAJA_MOVIMIENTO` | Controla ingresos y egresos de caja. |
| `CONSULTA_IA` | Guarda preguntas en lenguaje natural y SQL generado. |
| `AUDITORIA_SISTEMA` | Registra eventos importantes del sistema mediante triggers. |

---

## Flujo funcional

El flujo correcto del sistema es:

```txt
1. Crear urbanización.
2. Crear propietario.
3. Crear vivienda asociada al propietario.
4. Crear período mensual.
5. Crear o generar alícuotas.
6. Registrar pago de alícuota.
7. Registrar egresos administrativos.
8. Consultar caja, deudores y reportes.
9. Revisar auditoría y consultas IA.
```

Ejemplo real:

```txt
Urbanización: La Florida
Viviendas: 20 casas
Alícuota mensual por vivienda: $45

Ingreso mensual esperado:
20 casas x $45 = $900

Egreso:
Mantenimiento de puerta principal = $120

Saldo:
$900 - $120 = $780
```

---

## API REST con ORDS

La API fue publicada mediante **Oracle REST Data Services** con el alias:

```txt
alicuotas
```

URL base:

```txt
http://localhost:8080/ords/alicuotas/api/
```

Endpoint informativo:

```http
GET http://localhost:8080/ords/alicuotas/api/info/
```

---

## Endpoints principales

### Información general

| Método | Endpoint | Descripción |
|---|---|---|
| GET | `/info/` | Muestra información general de la API. |

---

### Urbanización

| Método | Endpoint | Descripción |
|---|---|---|
| GET | `/urbanizacion/` | Lista urbanizaciones. |
| GET | `/urbanizacion/{id}/` | Consulta una urbanización por ID. |
| POST | `/urbanizacion/crear/` | Crea una urbanización. |
| PUT | `/urbanizacion/actualizar/` | Actualiza una urbanización. |
| DELETE | `/urbanizacion/eliminar/` | Elimina o inactiva una urbanización según la lógica definida. |

---

### Propietarios

| Método | Endpoint | Descripción |
|---|---|---|
| GET | `/propietarios/` | Lista propietarios. |
| GET | `/propietarios/{id}/` | Consulta propietario por ID. |
| POST | `/propietarios/crear/` | Crea propietario con JSON. |
| PUT | `/propietarios/actualizar/` | Actualiza propietario con JSON. |
| DELETE | `/propietarios/eliminar/` | Inactiva propietario. |

---

### Viviendas

| Método | Endpoint | Descripción |
|---|---|---|
| GET | `/viviendas/` | Lista viviendas. |
| GET | `/viviendas/{id}/` | Consulta vivienda por ID. |
| POST | `/viviendas/crear/` | Crea vivienda. |
| PUT | `/viviendas/actualizar/` | Actualiza vivienda. |
| DELETE | `/viviendas/eliminar/` | Inactiva vivienda. |

---

### Períodos

| Método | Endpoint | Descripción |
|---|---|---|
| GET | `/periodos/` | Lista períodos. |
| GET | `/periodos/{id}/` | Consulta período por ID. |
| POST | `/periodos/crear/` | Crea período mensual. |
| PUT | `/periodos/actualizar/` | Actualiza estado del período. |
| DELETE | `/periodos/eliminar/` | Cierra o desactiva período según la lógica definida. |

---

### Alícuotas

| Método | Endpoint | Descripción |
|---|---|---|
| GET | `/alicuotas/` | Lista alícuotas. |
| GET | `/alicuotas/{id}/` | Consulta alícuota por ID. |
| POST | `/alicuotas/crear/` | Crea alícuota individual. |
| POST | `/alicuotas/generar-mensual/` | Genera alícuotas para todas las viviendas. |
| PUT | `/alicuotas/actualizar/` | Actualiza datos de una alícuota. |
| DELETE | `/alicuotas/anular/` | Anula una alícuota. |

---

### Pagos

| Método | Endpoint | Descripción |
|---|---|---|
| GET | `/pagos/` | Lista pagos. |
| GET | `/pagos/{id}/` | Consulta pago por ID. |
| POST | `/pagos/registrar/` | Registra pago de alícuota. |
| PUT | `/pagos/actualizar/` | Actualiza datos administrativos del pago. |
| DELETE | `/pagos/eliminar/` | Endpoint protegido para evitar descuadre financiero. |

---

### Egresos

| Método | Endpoint | Descripción |
|---|---|---|
| GET | `/egresos/` | Lista egresos. |
| GET | `/egresos/{id}/` | Consulta egreso por ID. |
| POST | `/egresos/registrar/` | Registra gasto de la urbanización. |
| PUT | `/egresos/actualizar/` | Actualiza datos administrativos del egreso. |
| DELETE | `/egresos/eliminar/` | Endpoint protegido para evitar descuadre financiero. |

---

### Reportes

| Método | Endpoint | Descripción |
|---|---|---|
| GET | `/deudores/` | Lista deudores. |
| GET | `/deudores/filtro/A/9/12/` | Deudores con apellido A que deben septiembre y diciembre. |
| GET | `/deuda-propietarios/` | Deuda total por propietario. |
| GET | `/recaudacion-mensual/` | Recaudación agrupada por mes. |
| GET | `/saldo-caja/` | Saldo actual de caja. |
| GET | `/top-deudores/` | Propietarios con mayor deuda. |
| GET | `/reporte-financiero-json/` | Reporte financiero en formato JSON. |
| GET | `/auditoria/` | Consulta eventos auditados. |
| GET | `/consultas-ia/` | Consulta preguntas procesadas por el módulo IA/NLQ. |

---

## Ejemplos de consumo en Postman

Para operaciones `POST`, `PUT` y `DELETE` con JSON:

```txt
Body -> raw -> JSON
Header -> Content-Type: application/json
```

---

### Crear propietario

```http
POST http://localhost:8080/ords/alicuotas/api/propietarios/crear/
```

```json
{
  "cedula": "0109999999",
  "nombres": "Juan",
  "apellidos": "Arias",
  "telefono": "0999999999",
  "correo": "juan.arias@gmail.com"
}
```

---

### Actualizar propietario

```http
PUT http://localhost:8080/ords/alicuotas/api/propietarios/actualizar/
```

```json
{
  "id_propietario": 51,
  "cedula": "0109999999",
  "nombres": "Juan Carlos",
  "apellidos": "Arias",
  "telefono": "0988888888",
  "correo": "juan.actualizado@gmail.com",
  "estado": "ACTIVO"
}
```

---

### Crear vivienda

```http
POST http://localhost:8080/ords/alicuotas/api/viviendas/crear/
```

```json
{
  "id_urbanizacion": 1,
  "id_propietario": 51,
  "numero_vivienda": "A-21",
  "manzana": "A",
  "tipo_vivienda": "CASA",
  "estado": "HABITADA"
}
```

---

### Crear período

```http
POST http://localhost:8080/ords/alicuotas/api/periodos/crear/
```

```json
{
  "mes": 9,
  "anio": 2026,
  "estado": "ABIERTO"
}
```

---

### Generar alícuotas mensuales

```http
POST http://localhost:8080/ords/alicuotas/api/alicuotas/generar-mensual/
```

```json
{
  "mes": 10,
  "anio": 2026,
  "valor": 45
}
```

---

### Registrar pago

```http
POST http://localhost:8080/ords/alicuotas/api/pagos/registrar/
```

```json
{
  "id_alicuota": 10,
  "valor_pagado": 45,
  "metodo_pago": "EFECTIVO",
  "referencia": "REC-001"
}
```

---

### Registrar egreso

```http
POST http://localhost:8080/ords/alicuotas/api/egresos/registrar/
```

```json
{
  "categoria": "Mantenimiento",
  "descripcion": "Mantenimiento de la puerta principal de ingreso",
  "valor": 120,
  "responsable": "Joaquin Astudillo"
}
```

---

### Consultar deudores por filtro

```http
GET http://localhost:8080/ords/alicuotas/api/deudores/filtro/A/9/12/
```

La consulta representa la pregunta:

```txt
Dame un listado de las personas que deben en septiembre y diciembre y que comiencen con el apellido A.
```

---

## Consultas avanzadas y reportes

El sistema incluye reportes para:

- Deudores por período.
- Deuda total por propietario.
- Recaudación mensual.
- Estado de alícuotas.
- Saldo de caja.
- Movimientos financieros.
- Top de deudores.
- Reporte financiero general.
- Deudores filtrados por letra de apellido y meses específicos.

Además, se implementaron índices para mejorar consultas frecuentes sobre:

- Apellidos de propietarios.
- Estado de alícuotas.
- Períodos.
- Viviendas.
- Fechas de pago.
- Movimientos de caja.
- Manzanas.

---

## PL/SQL, triggers y auditoría

El proyecto implementa procedimientos y funciones PL/SQL para centralizar la lógica de negocio.

### Funciones

- `fn_deuda_vivienda`
- `fn_deuda_propietario`

### Procedimientos

- `pr_registrar_pago`
- `pr_generar_alicuotas_mensuales`
- `pr_actualizar_vencidas`
- `pr_registrar_egreso`
- `pr_consulta_lenguaje_natural`

### Triggers

- Auditoría de cambios de estado en alícuotas.
- Auditoría de pagos registrados.
- Auditoría de egresos registrados.
- Validación de pagos.

La tabla `AUDITORIA_SISTEMA` permite conservar evidencia de las operaciones importantes realizadas dentro del sistema.

---

## JSON y consultas en lenguaje natural

El proyecto incluye vistas JSON para representar información de manera estructurada, facilitando el consumo de datos por aplicaciones externas.

También se implementó un módulo de consultas en lenguaje natural mediante PL/SQL. Este módulo permite recibir una pregunta del usuario, identificar palabras clave, generar una consulta SQL relacionada y guardar la evidencia en la tabla `CONSULTA_IA`.

Ejemplo de pregunta:

```txt
Dame un listado de las personas que deben en septiembre y diciembre y que comiencen con el apellido A.
```

Nota técnica:

> En el entorno actual no se encontró un perfil activo de SELECT AI. Por ello, se implementó un módulo NLQ/IA simulado y preparado para integración futura con SELECT AI.

---

## Estructura sugerida del repositorio

```txt
Proyecto_Alicuotas_Astudillo/
│
├── 01_sql/
│   ├── 01_creacion_tablas.sql
│   ├── 02_inserts_dataset.sql
│   ├── 03_consultas_avanzadas.sql
│   ├── 04_indices_optimizacion.sql
│   ├── 05_plsql_funciones_procedimientos.sql
│   ├── 06_triggers_auditoria.sql
│   ├── 07_vistas_json.sql
│   ├── 08_api_rest_ords.sql
│   └── CRUD_COMPLETO_ORDS_ALICUOTAS.sql
│
├── 02_postman/
│   └── Plantillas_Postman_API_Alicuotas.txt
│
├── 03_evidencias/
│   ├── api_info_funcionando.png
│   ├── postman_deudores_filtro.png
│   ├── postman_crud_propietarios.png
│   ├── postman_pagos.png
│   └── postman_egresos.png
│
├── 04_documentacion/
│   └── informe_proyecto.pdf
│
└── README.md
```

---

## Evidencias sugeridas

Para demostrar el funcionamiento del sistema se recomienda incluir capturas de:

- API `/info/` funcionando.
- Endpoints GET en navegador.
- CRUD de propietarios en Postman.
- Creación de vivienda.
- Generación mensual de alícuotas.
- Registro de pago.
- Registro de egreso.
- Saldo de caja actualizado.
- Reporte de deudores.
- Auditoría del sistema.
- Consulta IA/NLQ procesada.
- Objetos ORDS publicados.
- Objetos de base de datos sin errores.

---

## Seguridad y buenas prácticas

No subir al repositorio:

- Contraseñas.
- Wallets de Oracle Cloud.
- Archivos `.env`.
- Tokens.
- Claves API.
- Capturas con credenciales.
- Datos sensibles reales.

El proyecto debe incluir únicamente scripts, documentación, evidencias académicas y plantillas de prueba.

---

## Estado del proyecto

| Componente | Estado |
|---|---|
| Modelo relacional | Implementado |
| Dataset de prueba | Implementado |
| Consultas avanzadas | Implementado |
| Índices | Implementado |
| PL/SQL | Implementado |
| Triggers | Implementado |
| Auditoría | Implementado |
| Vistas JSON | Implementado |
| API REST ORDS | Implementado |
| Pruebas Postman | Implementado |
| Módulo NLQ/IA simulada | Implementado |

---

## Autor

**Joaquín Astudillo**

Proyecto académico de base de datos desarrollado con Oracle Database, ORDS, SQL, PL/SQL y API REST.

---

## Frase de defensa del proyecto

> Este sistema demuestra cómo Oracle Database puede ser utilizado no solo como repositorio de datos, sino también como plataforma central de lógica de negocio, reportes, auditoría, servicios REST y consultas inteligentes aplicadas a la administración financiera de una urbanización.
