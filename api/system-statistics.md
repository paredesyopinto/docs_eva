# Estadísticas de uso

EVA almacena métricas e informaciones útiles sobre cada comando/plugin; como el número de veces que se ha utilizado, y algunas clasificaciones que pueden ser útiles. Revise periódicamente las estadísticas de uso para comprender cómo está funcionando el sistema y cuales comandos podrían requerir de ajustes. 

Distinga las tendencias de uso con promedios mensuales o revise que alertas se están generando para detectar cambios repentinos en el uso y considerar la implementación de nuevos comandos, o descargue cualquier informe para realizar su propio análisis.

Los cambios en el uso de la aplicación pueden indicar cosas buenas y malas: el éxito de un comando o los usuarios que llegan a una condición de la aplicación donde comienzan a producirse fallos. Al evaluar rutinariamente las estadísticas y alertas de la aplicación, puede detectar rápidamente los cambios y luego corregir los problemas antes de que afecten negativamente la experiencia de sus usuarios.

El uso de informes es la forma en que las empresas aprenden sobre los hábitos de los usuarios durante ciertos períodos de tiempo en función de los datos generados. Los informes pueden ayudar a la compañía a predecir patrones, corregir errores y alterar el producto de manera efectiva. Estos reportes son una forma importante de controlar el uso de los sistemas de la compañía.

## Reportes disponibles

### Reporte de uso de comandos

Muestra cuales han sido los comandos más utilizados para un periodo de tiempo. Con la información de este reporte puede planificar que tan exitosa ha sido la implementación y uso de cada comando en el sistema.  

```powershell
Get-CommandUsageReport -TimeLapse 'ThisMonth'
# Comandos más usuados este mes.

Get-CommandUsageReport -StartDate (Get-Date -Year 2020 -Month 1 -Day 1)
# Comandos más usuados desde el 1 de enero del 2020 hasta hoy

Get-CommandUsageReport -StartDate (Get-Date -Year 2020 -Month 1 -Day 1) -EndDate (Get-Date -Year 2020 -Month 1 -Day 31)
# Comandos más usuados entre el 1 de enero del 2020 y el 31 de enero del 2020

Get-CommandUsageReport -TimeLapse ThisMonth -Top 5
# Top 5 comandos más usuados en este mes

Get-CommandUsageReport -TimeLapse -100 -Top 50
# 50 comandos más usados en los últimos 100 días.
```

### Reporte de usuarios más activos

¿Qué tanto utilizan los usuarios el sistema? Este reporte le ayuda a determinarlo. 

```powershell
Get-UserActivityReport -TimeLapse 'ThisMonth'
# Usuarios más activos este mes.

Get-UserActivityReport -StartDate (Get-Date -Year 2020 -Month 1 -Day 1)
# Usuarios más activos desde el 1 de enero del 2020 hasta hoy

Get-UserActivityReport -StartDate (Get-Date -Year 2020 -Month 1 -Day 1) -EndDate (Get-Date -Year 2020 -Month 1 -Day 31)
# Usuarios más activos entre el 1 de enero del 2020 y el 31 de enero del 2020

Get-UserActivityReport -TimeLapse ThisMonth -Top 5
# Top 5 usuarios más activos en este mes

Get-UserActivityReport -TimeLapse -100 -Top 50
# 50 usuarios más activos en los últimos 100 días.
```

### Reporte de Feedback

El plugin de Feedback proporciona un mecanismo para que los usuarios se comuniquen sus ideas y necesidades. Este reporte le ayuda a identificar las ideas más populares.

```powershell
Get-FeedbackReport -TimeLapse 'ThisMonth'
# Ideas más populares este mes.

Get-FeedbackReport -StartDate (Get-Date -Year 2020 -Month 1 -Day 1)
# Ideas más populares desde el 1 de enero del 2020 hasta hoy

Get-FeedbackReport -StartDate (Get-Date -Year 2020 -Month 1 -Day 1) -EndDate (Get-Date -Year 2020 -Month 1 -Day 31)
# Ideas más populares  entre el 1 de enero del 2020 y el 31 de enero del 2020

Get-FeedbackReport -TimeLapse ThisMonth -Top 5
# Top 5 ideas más populares de este mes

Get-FeedbackReport -TimeLapse -100 -Top 50
# 50 ideas más populares de los últimos 100 días.
```