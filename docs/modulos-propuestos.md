# Modulos propuestos

Modulos que **no estan** en `Tabla Modulos Casos de Uso Agromag` pero salieron al revisar el resto de la documentacion y al hablar con el veterinario.
Van aparte a proposito: primero se decide cuales entran, y recien ahi se agregan al documento oficial y al [backlog](./backlog.md).

Estado: `propuesto` = sin decidir · `aprobado` = va al documento oficial · `descartado` = no se hace en esta version.

---

## MP-01 · Horarios de atencion (panel administrativo)

**Estado:** propuesto — *el mas urgente de los tres primeros*

Existe como **RF-003** en el SRS y como **RN-019** ("el horario solo puede ser modificado por el administrador desde el panel"), pero no tiene modulo ni casos de uso.

**Por que importa:** RN-002 dice que solo se agendan citas dentro del horario publicado. Si el horario no se puede administrar, el agendamiento (E9) queda con los horarios quemados en el codigo. **Esto bloquea la epica mas importante del proyecto.**

Casos de uso propuestos:
- Configurar horario de atencion semanal
- Bloquear un dia o franja puntual (feriado, vacaciones, emergencia)
- Consultar horario configurado

---

## MP-02 · Tipos de cita: consultorio, domicilio y campo

**Estado:** propuesto

El veterinario atiende **mascotas y ganaderia**, e incluye visitas medicas a domicilio y servicios en finca (trazabilidad bovina, tuberculosis y brucelosis, asesorias productivas, servicio de rumen). La documentacion actual describe solo consultas en el consultorio.

**Por que importa:** una consulta en el local es un espacio corto en la agenda. Una visita a domicilio o a una finca necesita **direccion**, tiempo de traslado y ocupa mucho mas tiempo. Las reglas RN-002, RN-020, RN-031 y RN-032 estan escritas pensando solo en el consultorio.

Cambios propuestos:
- Campo "tipo de cita" en el agendamiento: consultorio / domicilio / campo
- Direccion obligatoria cuando no es en el consultorio
- Duracion y disponibilidad distintas segun el tipo
- Filtro por tipo de cita en el panel administrativo

No proponemos un modulo nuevo: es una extension de **E9 (agendamiento)** y **E3 (citas admin)**. Pero cambia bastantes historias, asi que conviene decidirlo antes de escribirlas.

---

## MP-03 · Catalogo de servicios

**Estado:** propuesto

Vision y alcance habla de un "catalogo de productos **y servicios**", y **RC-02** pide descripcion, duracion estimada, precio referencial y responsable de cada servicio. La tabla de modulos solo tiene catalogo de **productos**.

Servicios que ofrece el consultorio (confirmados por el veterinario):

cirugias mayores y menores · examenes de laboratorio (hemograma, quimica sanguinea) · limpiezas dentales · radiografias · trazabilidad bovina · asesorias tecnicas productivas · examenes de tuberculosis y brucelosis bovina · visitas medicas a domicilio · servicio de rumen · corte de pelo

**Dos caminos:**

| Opcion | Que implica | Cuando conviene |
|---|---|---|
| **A — Fijos en el codigo** | Los 10 servicios viven en el sitio, se cambian con un PR | Si la lista casi no cambia. Es lo que ya esta hecho en la landing |
| **B — Modulo administrable** | CRUD de servicios en el panel, como el de productos | Si el veterinario quiere cambiar precios y descripciones el solo |

Recomendacion: **opcion A para la version 1.** Son 10 servicios que cambian una o dos veces al ano; un CRUD completo para eso es mas trabajo del que ahorra. Si el veterinario pide editarlos, se pasa a B despues.

---

## MP-04 · Proveedores

**Estado:** propuesto

Existe como **RF-008** y en cuatro reglas de negocio (**RN-017, RN-027, RN-036, RN-037**), pero no tiene modulo ni casos de uso.

Casos de uso propuestos:
- Registrar proveedor (nombre, producto o categoria que suministra, contacto)
- Editar proveedor
- Eliminar proveedor — bloqueado si tiene productos activos asociados (RN-037)
- Consultar lista de proveedores

**Ojo:** RN-037 obliga a asociar cada producto con su proveedor. Eso agrega un campo al modulo de productos (E5) y una validacion al eliminar. No es gratis.

Pregunta para el cliente: **¿el veterinario realmente va a mantener esto al dia?** Un modulo que nadie usa es peor que no tenerlo. Si la respuesta no es un si claro, conviene descartarlo de esta version.

---

## MP-05 · Perfil del equipo medico

**Estado:** propuesto — prioridad baja

**RC-04** pide una seccion con fotografia, especialidad, formacion y experiencia del equipo veterinario, para generar confianza.

En Agromag el equipo medico es **una sola persona: el dueno**. No necesita un modulo administrable — es una seccion estatica en el sitio, del mismo tipo que la landing.

Recomendacion: **historia suelta dentro de E0**, no un modulo.

---

## MP-06 · Blog y contenido educativo

**Estado:** propuesto — candidato a descartar

**RC-05** pide una seccion de articulos sobre cuidado animal, orientada a SEO.

Implica un CRUD completo de articulos, editor de texto, imagenes y, sobre todo, **alguien que escriba contenido de forma sostenida**. Sin eso ultimo, es un modulo que se construye y queda con dos articulos de 2026.

Recomendacion: **descartar para esta version.** Dejarlo escrito como version futura en el documento de alcance.

---

## Resumen para decidir

| # | Modulo | Recomendacion |
|---|---|---|
| MP-01 | Horarios de atencion | **Agregar.** Bloquea el agendamiento |
| MP-02 | Tipos de cita (domicilio y campo) | **Agregar.** El negocio real lo necesita |
| MP-03 | Catalogo de servicios | Fijos en codigo por ahora |
| MP-04 | Proveedores | Preguntarle al cliente si lo va a usar |
| MP-05 | Perfil del equipo medico | Seccion estatica, no modulo |
| MP-06 | Blog | Descartar en esta version |
