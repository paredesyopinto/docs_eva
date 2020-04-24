# Archivo de configuración

El archivo `appsettings.json` almacena los datos de configuración del sistema. El formato del archivo de configuración se parece a esto:

```json
{
  "data-configuration": {
    "typeQualifiedName": "FullTypeName",
    "defaultConnectionString": "DefaultValue",
    "logFolderPath": "{runtime:home}\\Logs"
  },
  "connection-strings": {
    "sqliteDataProvider": "PathToSqliteFile",
    "sqlServerDataProvider": "DBConnectionStringsForSqlServer"
  },
  "misc-configuration": {
    "email-admin": "email@email.com",
    "failOver-behavior": "DoNotCheck",
    "mixPanel-token": "97zff8z35e91fff8bb963zbb38eu98b5"
  },
  "service-configuration": {
    "name": "Evertec Slack Virtual Assistant",
    "description": "Host del asistente virtual para Slack de Evertec",
    "displayName": "EVA for Slack",
    "account": "LocalSystem"
  },
  "api-configuration": {
    "serviceUrl": "{env:EVA:SERVICE_URL}",
    "authorizedApiKeys": [
      "{env:EVA:APIKEY}"
    ]
  }
}
```

## Sección data-configuration

Almacena información relevante relacionada con la configuración de datos del sistema.

| Clave                     | Descripción   | Valores admitidos  | Variables de entorno | Valor predeterminado |
| ------------------------- |-------------  | -----| :-----: | ---- |
| `typeQualifiedName`       | Nombre completo de la clase que se utiliza como predeterminada para el repositorio de datos. | [1] o [2]| No | [1] |
| `defaultConnectionString` | Clave de la sección `connection-strings` que se utiliza para conectar con la base de datos | Uno de los valores en `connection-strings` | No | `sqliteDataProvider` |
| `logFolderPath`           | Ruta de acceso de la carpeta donde se dejan los archivos logs de sistema | Ruta de acceso de una carpeta donde se puedan escribir archivos | Si | `{runtime:home}\\Logs` |

[1] **Para usar SqlServer** =>
`Everco.Utils.EVA.Implementation.Data.SqlServerDataProvider, Everco.Utils.EVA.Implementation`

[2] **Para usar Sqlite** =>
`Everco.Utils.EVA.Implementation.Data.SqliteDataProvider, Everco.Utils.EVA.Implementation`

## Sección connection-strings

Almacena información de cadenas de conexión del sistema.

| Clave                     | Descripción   | Valores admitidos  | Variables de entorno | Valor predeterminado |
| ------------------------- |-------------  | -----| :-----: | --------- |
| `sqliteDataProvider`      | Una cadena de conexión que puede establecer comunicación con instancias de Sqlite o la ruta de acceso del archivo. | [SQLite connection strings](https://www.connectionstrings.com/sqlite/) | Si | `Data Source = {runtime:home}\\Data\\eva.sqlite` |
| `sqlServerDataProvider`   | Una cadena de conexión que puede establecer comunicación con instancias de SQL Server | [SQL Server connection strings](https://www.connectionstrings.com/sql-server/) | Si | `#N/A` |

## Sección misc-configuration

Almacena información de varios tipos de configuración.

| Clave                     | Descripción   | Valores admitidos  | Variables de entorno | Valor predeterminado |
| ------------------------- |-------------  | -----| :-----: |
| `emailAdmin`      | Cuenta de correo asociada con el administrador del sistema. Este valor se mostrará en algunos mensajes al usuario final. | [Cadena en formato email](https://en.wikipedia.org/wiki/Email_address) | Si | `{env:EVA:ADMIN:EMAIL}` |
| `failOverBehavior`   | Un valor que establece el comportamiento del servicio cuando no puede contecra con el API de Slack.  | StopAtFirstError o DoNotCheck | No | `DoNotCheck` |
| `mixPanelToken`   | EVA utiliza MixPanel guardar la información que luego permita analizar la interacción los usuarios, al permitir analizar en tiempo real el uso de los comandos para identificar tendencias, comprender el comportamiento de los usuarios y tomar decisiones sobre el producto. Coloque aquí su token de proyecto. [¿Dónde localizar el token de proyecto?](https://help.mixpanel.com/hc/en-us/articles/115004502806) Si no tiene una cuenta de MixPanel puede crear una gratuita.  | Token del proyecto. Generalmente un valor de 32 caracteres. | Si | `System.String.Empty` |

[1] **StopAtFirstError**
Detiene el procesamiento de todos los Bots al encontrar una falla.

[2] **DoNotCheck**
Intenta procesar el siguiente Bot al encontrar una falla.

## Sección service-configuration

Almacena información de configuración del servicio del Sistema Operativo.

| Clave                     | Descripción   | Valores admitidos  | Variables de entorno | Valor predeterminado |
| ------------------------- |-------------  | -----| :-----: |
| `name`      | El nombre que identifica el servicio en el Administrador de servicios del sistema operativo |  | No | `EVA` |
| `description`   | La descripción que identifica el servicio en el Administrador de servicios del sistema operativo  | | No | `Eva Host` |
| `displayName`   |  El nombre descriptivo para el servicio. |   | No | `EVASrv` |
| `account`   | La cuenta de usuario que proporciona el contexto de seguridad para el servicio. | LocalSystem, ServiceSystem, NetworkService  | No | `LocalSystem` |

## Sección api-configuration

Almacena información de configuración del API del servicio.

| Clave                     | Descripción   | Valores admitidos  | Variables de entorno | Valor predeterminado |
| ------------------------- |-------------  | -----| :-----: |
| `serviceUrl`   | URL donde se expone el servicio de adminstración | [System.Uri](https://docs.microsoft.com/en-us/dotnet/api/system.uri) | Si | `http://localhost` |
| `authorizedApiKeys`   | Lista separadas por comas | Lorem ipsum dolor sit amet, consectetur adipiscing elit. | Si | `{env:EVA:APIKEY}` |

## Variables de entorno

Cuando se define un valor que soporta variables de entorno, puede utilizar la forma `{env:NAME}` reemplazndo `NAME` por el nombre de la variable para que el tiempo de ejecución de **`EVA`** busque una variable de ambiente en el sistema operativo utilice este valor para la configuración.

Por ejemplo, si tuviera una variable de ambiente con el nombre ABCDE y desea utilizarla, simplemente coloque en el archivo de configuración el valor `{env:ABCDE}`. El tiempo de ejecución de **`EVA`** buscará esa variable y la establecerá como el valor de configuración. Si el tiempo de ejecución no encuentra la variable, se intentará utilizar un valor predeterminado. Si el valor predeterminado no fuera valido para la configuración, ocurrirá un error en tiempo de ejecución y el servicio no se iniciará. Se dejará registro de esta situación excepcional en los archivos de logs del servicio.

El uso de variables de entorno es muy común con valores que no se quieren persistir en los archivos de configuración como pueden ser claves, usuarios o cualquier otro valor de carácter sensible.

### Ejemplo de uso

Supongamos que desea configurar una cadena de conexión, pero no quiere dejar en el archivo de configuración el usuario y la clave por un requerimiento de seguridad. Podría crear una variable de entorno para almacenar el valor del usuario y otra para el de clave y dejar en la configuración algo de la forma:

```plain
User={env:MYCUSTOMUSER}Pwd={env:MYCUSTOMPASSWORD}
```

Donde `MYCUSTOMUSER` y `MYCUSTOMPASSWORD` son variables de ambiente.

### Comprobar el valor de una variable de ambiente

En una ventana de PowerShell, escriba: `$env:CUSTOMNAME` reemplazando `CUSTOMNAME` por el nombre de la variable de ambiente.

Para conocer el valor de todas las variables de ambiente, en una ventana de PowerShell escriba:

```powershell
Get-ChildItem env:
```

# [Setting An Environment Variable](#tab/tabid-1)

- [ Set Environment Variable – CMD & PowerShell](https://www.shellhacks.com/windows-set-environment-variable-cmd-powershell/)
- [Create and Modify Environment Variables on Windows](https://superuser.com/questions/949560/how-do-i-set-system-environment-variables-in-windows-10)

# [How to Set Environment Variables in Windows](#tab/tabid-2)

> [!Video https://www.youtube.com/embed/bEroNNzqlF4]

***

> [!WARNING]
> Recuerde que los valores establecidos para una variable de entorno solo se procesan al iniciar el proceso del sistema operativo, así que cualquier cambio en una variable de entorno será visible solo hasta que se reinicie el proceso.