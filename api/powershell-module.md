# Módulo de PowerShell

El módulo de PowerShell de EVA facilita la administración de la información, de una instancia del host de forma local o remota. Puede configurar y administrar:

- Usuarios y grupos de seguridad
- Plugins
- Comandos
- Permisos
- Instancias de Bots

## Principales comandos

Para obtener la lista completa de comandos del módulo puede utilizar las siguientes instrucciones:

```powershell
Import-Module PSEva
Get-Command -Module PSEva
```

Para agrupar los resultados por tipo de comando puede utilizar:

```powershell
Import-Module PSEva
Get-Command -Module PSEva  | Group-Object -Property Verb
```

Al igual que para otros módulos de Powershell puede utilizar el comando [Get-Help](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/get-help) para obtener información sobre los comandos. Por ejemplo:

```powershell
Get-Help Nombre-Funcion
# Obtener el texto de ayuda de una función
```

```powershell
Get-Help Nombre-Funcion -Parameter Nombre-Parametro
# Obtener el texto de ayuda de un parámetro en una función
```

## Prerequisitos

PSEVA no tiene dependencias y está diseñado para funcionar en una computadora con una nueva instalación de Windows.
