# Backlog — Epicas e historias

Sale de `Tabla Modulos Casos de Uso Agromag`. **Un modulo = una epica. Un caso de uso = una historia.**
Los modulos que faltan en la documentacion estan aparte, en [modulos-propuestos.md](./modulos-propuestos.md).

## Como se traduce a Jira

| Aca | En Jira |
|---|---|
| Epica (E1, E2...) | Epic |
| Historia | Story, enlazada a su Epic |
| Reglas (RN-xxx) | Criterios de aceptacion de la Story |

Formato de la historia: **Como** `<actor>` **quiero** `<accion>` **para** `<valor>`.
Las reglas de negocio de la columna "Reglas" son el punto de partida de los criterios de aceptacion — no son la lista completa, pero es lo que ya esta acordado con el cliente.

---

## E0 · Base tecnica

No es un modulo del negocio: es lo que hay que tener listo para que el resto se pueda construir.

| Historia | Descripcion | Estado |
|---|---|---|
| Configurar proyecto Astro | Scaffold, Tailwind, estructura de carpetas | Hecho (AGRO-1) |
| Integracion continua | Build automatico en cada PR | Hecho (AGRO-2) |
| Definir modelo de datos | Entidades: cita, producto, usuario admin, valoracion, promocion, anuncio | Pendiente |
| Elegir backend y persistencia | El SRS decia PHP+MySQL; el proyecto es Astro. Falta decidir con que se guardan los datos | **Bloqueante** |
| Layout base y componentes | Header, footer, tipografia, colores, botones reutilizables | Pendiente |
| Despliegue | Donde vive el sitio y como se publica | Pendiente |

> El ticket de backend bloquea casi todas las epicas del panel administrativo. Es el primero que hay que cerrar.

---

# Panel administrativo

## E1 · Autenticacion
Actor: personal administrativo

| Historia | Como... quiero... para... | Reglas |
|---|---|---|
| Iniciar sesion | Como personal quiero entrar con usuario y contrasena para acceder al panel | RN-011, RN-029, RN-030 |
| Cerrar sesion | Como personal quiero cerrar sesion para que nadie use mi cuenta en una maquina compartida | RN-038 |
| Recuperar contrasena | Como personal quiero recuperar el acceso por correo para no depender del superadmin | RN-030 |
| Cambiar contrasena | Como personal quiero cambiar mi contrasena para mantener mi cuenta segura | RN-030 |

Ojo: RN-029 (bloqueo tras 3 intentos, 15 min) y RN-038 (sesion expira a los 30 min de inactividad) son historias tecnicas que se cuelan aca; conviene que sean criterios de aceptacion, no tickets aparte.

## E2 · Dashboard
Actor: personal administrativo

| Historia | Como... quiero... para... | Reglas |
|---|---|---|
| Ver resumen del dashboard | Como personal quiero ver un resumen al entrar para saber que atender hoy | — |
| Consultar citas del dia | Como personal quiero ver las citas de hoy para preparar la jornada | RN-021 |
| Consultar productos sin existencia | Como personal quiero ver que productos se agotaron para reponerlos | RN-022 |
| Consultar valoraciones pendientes | Como personal quiero ver las valoraciones sin revisar para aprobarlas o rechazarlas | RN-013 |

Depende de E3, E5 y E8: el dashboard solo muestra datos que otros modulos generan. **Hacerlo al final**, no al principio.

## E3 · Citas (admin)
Actor: personal administrativo

| Historia | Como... quiero... para... | Reglas |
|---|---|---|
| Gestionar citas | Como personal quiero ver todas las citas agendadas para organizar la agenda | RN-020 |
| Filtrar citas por fecha | Como personal quiero filtrar por fecha para encontrar una cita rapido | — |
| Actualizar estado de cita | Como personal quiero marcar una cita como completada, ausente o cancelada para llevar el control | RN-021 |
| Consultar detalle de cita | Como personal quiero ver los datos del cliente y su mascota para atender preparado | RN-001 |

## E4 · Usuarios administrativos
Actor: superadmin

| Historia | Como... quiero... para... | Reglas |
|---|---|---|
| Registrar usuario administrativo | Como superadmin quiero crear cuentas para dar acceso al personal nuevo | RN-011, RN-030 |
| Editar usuario administrativo | Como superadmin quiero editar los datos de una cuenta para mantenerlos al dia | RN-011 |
| Desactivar usuario administrativo | Como superadmin quiero desactivar una cuenta para quitar el acceso a quien ya no trabaja aca | RN-011 |

## E5 · Catalogo de productos (admin)
Actor: personal administrativo

| Historia | Como... quiero... para... | Reglas |
|---|---|---|
| Agregar producto | Como personal quiero agregar un producto para que aparezca en el catalogo publico | RN-007, RN-008, RN-009 |
| Editar producto | Como personal quiero editar precio y datos para mantener el catalogo actualizado | RN-008, RN-009 |
| Eliminar producto | Como personal quiero eliminar un producto que ya no se vende | RN-008 |
| Consultar lista de productos | Como personal quiero ver todo el catalogo para saber que hay cargado | RN-007 |
| Marcar producto sin existencia | Como personal quiero marcar un producto agotado para que el cliente no lo pida en vano | RN-022 |

## E6 · Promociones y eventos (admin)
Actor: personal administrativo

| Historia | Como... quiero... para... | Reglas |
|---|---|---|
| Publicar promocion o evento | Como personal quiero publicar una campana para atraer clientes | RN-015 |
| Editar promocion o evento | Como personal quiero corregir una promocion publicada | RN-015 |
| Eliminar promocion o evento | Como personal quiero bajar una promocion que ya no aplica | RN-015 |
| Consultar promociones y eventos | Como personal quiero ver las promociones activas y vencidas | RN-015 |

RN-015: toda promocion lleva fecha de inicio y vencimiento, y al vencer el sistema la oculta **solo**. Eso es logica automatica, no un boton.

## E7 · Anuncios (admin)
Actor: personal administrativo

| Historia | Como... quiero... para... | Reglas |
|---|---|---|
| Publicar anuncio | Como personal quiero publicar un comunicado para informar a los clientes | RN-026 |
| Editar anuncio | Como personal quiero corregir un anuncio publicado | RN-026 |
| Eliminar anuncio | Como personal quiero borrar un anuncio que ya no aplica | RN-026 |
| Consultar anuncios | Como personal quiero ver los anuncios publicados | RN-026 |

E6 y E7 son casi el mismo CRUD. Vale la pena construir uno y reutilizar la mitad del trabajo en el otro.

## E8 · Valoraciones (admin)
Actor: personal administrativo

| Historia | Como... quiero... para... | Reglas |
|---|---|---|
| Consultar valoraciones | Como personal quiero ver las valoraciones recibidas para revisarlas | RN-013 |
| Aprobar valoracion | Como personal quiero aprobar una valoracion para que se vea en el sitio | RN-013 |
| Rechazar valoracion | Como personal quiero rechazar una valoracion para que no se publique | RN-013 |
| Eliminar valoracion | Como personal quiero eliminar una valoracion ofensiva | RN-035 |

---

# Sitio publico

## E9 · Agendamiento de citas
Actor: cliente (sin cuenta)

| Historia | Como... quiero... para... | Reglas |
|---|---|---|
| Consultar disponibilidad de horarios | Como cliente quiero ver que espacios hay libres para elegir uno que me sirva | RN-002, RN-020, RN-031, RN-032 |
| Agendar cita | Como cliente quiero reservar una cita sin crear cuenta para no perder tiempo | RN-001, RN-005, RN-012, RN-031, RN-032 |
| Consultar estado de cita | Como cliente quiero saber si mi cita sigue en pie ingresando mi correo | RN-021 |
| Cancelar cita | Como cliente quiero cancelar con anticipacion para liberar el espacio | RN-006 |
| Reagendar cita existente | Como cliente quiero mover mi cita en vez de cancelarla y volver a empezar | RN-006, RN-020 |

**La epica mas importante y la mas riesgosa.** Es el objetivo de negocio del proyecto y es donde se concentran mas reglas. Merece arrancar temprano y probarse bien.
Pendiente de definir: como se identifica al cliente sin cuenta (asumimos correo) y como se manejan las visitas a domicilio y de campo — ver [modulos-propuestos.md](./modulos-propuestos.md).

## E10 · Catalogo (publico)
Actor: cliente

| Historia | Como... quiero... para... | Reglas |
|---|---|---|
| Consultar catalogo de productos | Como cliente quiero ver los productos disponibles para saber que hay | RN-007, RN-009 |
| Buscar producto | Como cliente quiero buscar por nombre para no recorrer todo el catalogo | RN-007 |
| Ver detalle de producto | Como cliente quiero ver descripcion y precio antes de ir al consultorio | RN-007, RN-009 |
| Consultar disponibilidad de producto | Como cliente quiero saber si hay existencias para no ir en vano | RN-022 |

## E11 · Promociones y eventos (publico)
Actor: cliente

| Historia | Como... quiero... para... | Reglas |
|---|---|---|
| Consultar promociones y eventos | Como cliente quiero ver las promociones vigentes para aprovecharlas | RN-015 |
| Ver detalle de promocion o evento | Como cliente quiero ver las condiciones y fechas de una promocion | RN-015 |

## E12 · Anuncios (publico)
Actor: cliente

| Historia | Como... quiero... para... | Reglas |
|---|---|---|
| Consultar anuncios del consultorio | Como cliente quiero ver los comunicados para enterarme de cambios de horario o noticias | RN-026 |

## E13 · Valoraciones (publico)
Actor: cliente

| Historia | Como... quiero... para... | Reglas |
|---|---|---|
| Enviar valoracion del servicio | Como cliente quiero contar mi experiencia para ayudar a otros y dar retroalimentacion | RN-013, RN-033, RN-034 |

## E14 · Contacto
Actor: cliente

| Historia | Como... quiero... para... | Reglas |
|---|---|---|
| Enviar mensaje de contacto | Como cliente quiero escribirle al consultorio para hacer una consulta | RN-014, RN-018 |

## E15 · Notificaciones
Actor: sistema

| Historia | Como... quiero... para... | Reglas |
|---|---|---|
| Enviar confirmacion de cita | Como cliente quiero recibir un correo al agendar para tener constancia | RN-003 |
| Enviar recordatorio de cita | Como cliente quiero que me recuerden mi cita para no olvidarla | RN-004 |
| Enviar aviso de cancelacion | Como cliente quiero que me avisen si mi cita se cancela para reorganizarme | RN-006 |

El recordatorio de 24 horas (RN-004) necesita algo que corra solo todos los dias. No es una pantalla: es una tarea programada, y suele subestimarse.

---

## Orden sugerido de trabajo

| Momento | Que | Por que |
|---|---|---|
| 1 | E0 (base tecnica) | Sin backend definido no arranca nada del panel |
| 2 | E1 (autenticacion) | Todo el panel depende de que exista un login |
| 3 | E9 (agendamiento) + E15 (notificaciones) | Es el objetivo del proyecto y lo mas riesgoso: cuanto antes se pruebe, mejor |
| 4 | E3 (citas admin) | El personal necesita administrar lo que E9 empieza a generar |
| 5 | E5 + E10 (catalogo) | Segundo objetivo de negocio: que el cliente consulte precios sin llamar |
| 6 | E6, E7, E11, E12 (contenido) | CRUDs parecidos entre si, se hacen rapido en bloque |
| 7 | E8 + E13 (valoraciones), E14 (contacto) | Valor real pero no bloquean nada |
| 8 | E2 (dashboard) | Solo muestra lo que ya generaron los demas modulos |

## Numeros

15 epicas · 49 historias · 4 personas.
Si una historia toma mas de 2 dias, probablemente son dos historias.
