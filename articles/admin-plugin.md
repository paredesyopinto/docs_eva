# Administración de plugins

La administración de plugins en EVA se hace a través del [módulo de PowerShell](../api/powershell-module.md), que tiene comandos para instalar, modificar y eliminar los plugins del sistema.

Cuando un desarrollar libera el instalador de un plugin, incluye un archivo de manifiesto. Este archivo se evalúa y procesa durante la instalación permitiendo al desarrollador definir los elementos de configuración necesarios para el correcto funcionamiento de su plugin. Por ejemplo, si su plugin necesitará de una cadena de conexión a una base de datos, bastaría con agregar en el archivo de manifiesto una entrada para que se solicite este valor durante el proceso de instalación. Luego, el desarrollador puede recuperar el valor en tiempo de ejecución y conectar con la base de datos.

## Ejemplo del archivo de manifiesto
