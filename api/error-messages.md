# Mensajes de error

Los mensajes de error, por más indeseados que sean, proporcionan información útil que puede ayudar para comprender cuál podría ser el problema por el que no se ha podido completar una solicitud. **`EVA`** asocia un código interno de seguimiento con el nombre **EventID** (agregado automáticamente por **`EVA`** cuando encuentra que no puede completar una operación) y uno público en el nombre **CorrelationalId** \(que se puede utilizar para [rastrear](trace-request.md) la información de entrada y salida generada para una solicitud\).

Desafortunadamente, no podemos cubrir todos los problemas que se puedan encontrar (son, en nuestra experiencia, los errores más comunes que los usuarios encontraran), pero puede utilizar esta lista de mensajes de error para descifrar lo que está sucediendo y asegurase de seguir las recomendaciones de solución de problemas

Si encuentra un error específico no cubierto en esta publicación y tiene un código de error déjenoslo saber [aquí](#).

## Identificadores de eventos más comunes

### Relacionados con la seguridad

#### Evento: 139070

- **Causa**: No encontramos la configuración del comando a ejecutar. _No se reconoce el texto ingresado por el usuario como un comando del sistema._

- **Resolución**: El usuario puede utilizar el [comando de ayuda](introducing-plugins.md#plugin-de-ayuda) para determinar los comandos reconocidos por el sistema. Puede personalizar el texto de este mensaje utilizando el parámetro del comando `HelpCommandText` del [Cmdlet Update-Bot de PowerShell](powershell-module.md)

#### Evento: 139071

- **Causa**:  Comando está deshabilitado. _El comando que intenta utilizar el usuario se ha sido deshabilitado por el administrador del sistema._

- **Resolución**: Habilite el comando utilizando el [Cmdlet Enable-Command de PowerShell](powershell-module.md)

#### Evento: 139072

- **Causa**:  No encontramos el usuario. _El usuario que intenta utilizar el comando no está registrado como uno de los usuarios del sistema._

- **Resolución**: Registre el usuario utilizando el [Cmdlet Register-User de PowerShell](powershell-module.md)

#### Evento: 139073

- **Causa**: Usuario no está habilitado. _El usuario que intenta utilizar el comando ha sido deshabilitado por el administrador del sistema._

- **Resolución**: Habilite el usuario utilizando el [Cmdlet Enable-User de PowerShell](powershell-module.md)

#### Evento: 139074

- **Causa**: Usuario no tiene permisos para ejecutar este comando. _El usuario que intenta utilizar el comando no tiene permisos para hacerlo._

- **Resolución**: Para que un usuario pueda hacer uso de un comando, debe tener un permiso de uso explicito. Agregue el permiso al usuario utilizando el [Cmdlet GrantPermisssion de PowerShell](powershell-module.md)

### Relacionados con la cache del sistema

En general los errores relacionados por la cache del sistema se pueden identificar porque inician con el texto **140** seguido generalmente por tres dígitos. Cuando se utiliza el modulo de PowerShell para administrar los valores del sistema, **`EVA`** se encarga de mantener sincronizados los datos del repositorio y la cache del sistema, pero si por algún motivo necesita reiniciar o sincronizar la cache del sistema puede utilizar el [Cmdlet RestartCache de PowerShell](powershell-module.md)


#### Temas relacionados

[Seguimiento de una solicitud](trace-request.md)