# Archivos de logs

Los archivos de logs pueden proporcionarle una amplia gama de información sobre la instalación de **`EVA`**. Esta información puede incluir información detallada sobre errores, usuarios, excepciones generales y mucho más. Para ver los archivos de registros en **`EVA`**, siga estos pasos:

Vaya a la carpeta de instalación del servicio y ubique la subcarpeta Logs. Allí encontrará varios archivos. **`EVA`** crea un tipo de archivo de log por cada día, anexando al final del nombre del archivo la fecha en la que fue creado. 

## ¿Cómo saber la ruta de la carpeta donde está instalado el servicio?

En una ventana de PowerShell, escriba:

```powershell
Import-Module PSEva
Get-Deployment
```


## Nombrado de los archivos de logs

El nombre de los archivos de logs siempre estará compuesto por tres partes. El prefijo **`Everco.Utils.EVA.Host-`** seguido de una palabra que puede ser **`Debug`**, **`Info`** o **`Error`** y la fecha en la que se creó el archivo en formato **`yyyy-MM-dd`**. Siempre tendrán la extensión .txt.

## Tipos de archivos de Logs

| Tipo de archivo | Descripción | Auto-Reciclaje |
|:------:|-----|:-----------:
|   `Debug`    | Almacena información del flujo de control interno y volcados de estado de diagnóstico para facilitar la localización de problemas.  | 2 días |
|   `Info`     | Almacena información de eventos de interés o que tienen relevancia para los desarrolladores.  | 2 días |
|   `Error`    | Almacena información de errores críticos que pueden indicar una falla dentro de la aplicación.  | 30 días |

> [!NOTE]
> ¿Se pueden eliminar de forma segura los archivos de logs antiguos? **Definitivamente si**, aunque estos archivos se reciclan periódicamente (con una estrategia basada en la fecha, para mantener solo los últimos archivos). Si por algún motivo necesita recuperar el espacio en disco inmediatamente, **puede borrarlos**. Tenga presente que no podrá borrar el archivo del día en curso porque estará siendo utilizado por el servicio.

## Visor de eventos del sistema operativo

La información de errores críticos se replica en el registro de sucesos del equipo local, para que otras aplicaciones o componentes del sistema operativo puedan localizar en un registro centralizado esta información.

[Puede utilizar el visor de eventos del sistema operativo](https://en.wikipedia.org/wiki/Event_Viewer) o la linea de comandos para acceder a esta información. En una ventana de PowerShell, escriba:

```powershell
# Consultar los últimos 10 registros
Get-EventLog -LogName Evertec -Newest 10

# Consultar los detalles del último registro
Get-EventLog -LogName Evertec -Newest 1 | Select-Object -Property *
```
