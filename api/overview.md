# Conceptos básicos

**`EVA`** se ejecuta como un servicio del sistema operativo para evitar la necesidad de tener administrar la instancia. El instalador se encargará de configurar el servicio para que se inicie con el sistema operativo, de tal manera que no requiera de intervención humana. Este servicio esta diseñando para conectar con múltiples instancias de Slack de tal suerte que pueda atender las solicitudes de diferentes bots de ser necesario. Así las cosas, es posible tener un bot que agrupe las solicitudes comunes de un área X y otro que agrupe las solicitudes de un área Y, donde cada bot puede tener sus propios usuarios y permisos además de su propia personalidad (nombre + logo + descripción).

Cuando se inicia del servicio del sistema operativo, **`EVA`** conecta con su repositorio de base de datos e intenta conectar con el API de Slack. Si por algún motivo no logrará conectar, dejará un log con información relevante.

Llegados a este punto podrían ocurrir dos problemas. No hay conexión con internet o la clave de conexión de Slack en invalida. Recuerde que el servicio del sistema operativo se está ejecutando en un contexto de seguridad del propio sistema operativo, por lo que tal vez sea necesario establecer un proxy o alguna excepción para lograr la conexión. En la sección de configuración del sistema veremos cómo establecer un usuario para la ejecución del servicio del sistema operativo.

## Crea un bot de Slack personalizado

Slack es una herramienta muy popular para empresas y equipos que tiene un gran potencial de automatización, al ofrecer docenas de integraciones y mantener todo en un solo lugar.

A continuación, necesitamos crear una aplicación en Slack que pueda recibir, procesar y responder a mensajes particulares en un canal de Slack. Utilizaremos a  **`EVA`** como un contenedor para la API de mensajería en tiempo real de Slack.

Para agregar nuestra configuración, utilizaremos la integración de Slack conocida como "Usuario Bot".

Para hacerlo, necesitamos obtener un token de conexión iniciando sesión en [slack.com](https://slack.com) y luego yendo a `https://<EspacioDeTrabajoDeSlack>.slack.com/apps/A0F7YS25R-bots`. A continuación, haga clic en "Agregar configuración" o “Añadir a Slack” e ingrese la información solicitada.

Al finalizar la creación, obtendrá un token en el siguiente formato:

`xoxb-000000-000000-x0x0xxXxX0XXxx0x`

Copie el valor del token y guárdelo de forma segura. Lo utilizaremos más adelante.

## Espacios de trabajo en Slack

Un espacio de trabajo de Slack es un centro compartido formado por canales donde los miembros del equipo pueden comunicarse y trabajar juntos. Para unirse a un espacio de trabajo, deberá crear una cuenta de Slack con su dirección de correo electrónico. Para que un usuario pueda hacer uso del bot, deberá invitarlo a formar parte del espacio de trabajo. Puede hacerlo enviando un correo de invitación desde la apropia aplicación de Slack o utilizando alguna de sus aplicaciones nativas.

Los usuarios pueden unirse a tantos espacios de trabajo como deseen, ya que no hay límite para la cantidad de cuentas de Slack que se pueden crear con la misma dirección de correo electrónico.

Cuando se crea un espacio de trabajo, el usuario con el que se crea se convertirá en el propietario principal del espacio de trabajo, aunque es posible transferir la propiedad de un espacio de trabajo, pero tenga presente que solo el propietario principal podrá hacerlo. En [este enlace se describe el proceso de transferencia](https://slack.com/intl/en-co/help/articles/204401633)

Las páginas de ayuda de Slack describen [todas las formas de invitar a nuevos miembros al espacio de trabajo](https://slack.com/intl/en-co/help/articles/201330256). También es posible crear un enlace de invitación compartido y luego, enviarlo con quien quiera que se una a dicho espacio de trabajo.

## Invitar a un usuario a participar

- Envie la invitación para que los usuarios se unan al espacio de trabajo.
- Cuando los usuarios acepten la invitación e inicien sesión verán en su barra de navegación una entrada en la sección de **Apps** con el nombre del bot.
- Asegurese de [establecer permisos de ejecución](../api/system-admin.md#establecer-permisos-de-ejecución) para que los usuarios puedan hacer uso de los comandos en el bot.
