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

## Prerequisitos

PSEVA no tiene dependencias y está diseñado para funcionar en una computadora con una nueva instalación de Windows.
