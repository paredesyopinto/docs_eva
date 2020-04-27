# Creación de un plugin

Los plugins o comandos son el eje central de **`EVA`**. Los plugins o comandos son la única forma de interactuar con la aplicación. De hecho, no tiene sentido tener un bot sin comandos registrados.

Un plugin o comando se crea implementando la interfaz [IPlugin](#interface-iplugin) tan simple como eso. Una vez que tenga un plugin, puede comenzar a definir los comportamientos de los comandos, a través del uso de los atributos **`CommandDescriptionAttribute`** y **`CommandExampleAttribute`**. En resumen, un plugin le dice a **`EVA`** cómo comportarse en tiempo de ejecución cuando un usuario solicita una operación.

Un plugin hace más que permitirle definir el comportamiento de la aplicación. Un plugin también le da acceso al [contexto](context-plugin.md) en el que se procesa la solicitud, ayudándole o facilitándole la generación de la respuesta, que finalmente representa el resultado de la operación para los usuarios.

Puede tener tantos plugins o comandos como desee en la aplicación. **`EVA`** no restringe el número en ninguna circunstancia.

## Configurar su entorno de desarrollo

Curabitur aliquet sapien sagittis, laoreet nisi vitae, varius dui. Curabitur lobortis quam elit, ac finibus lorem finibus sed.

## Desarrollo de sus propios comandos

Curabitur aliquet sapien sagittis, laoreet nisi vitae, varius dui. Curabitur lobortis quam elit, ac finibus lorem finibus sed.

## Descargar la plantilla

Curabitur aliquet sapien sagittis, laoreet nisi vitae, varius dui. Curabitur lobortis quam elit, ac finibus lorem finibus sed. Nam quis dui rutrum, tincidunt mi a, sodales sem. Integer fringilla in mi ac ullamcorper. Nulla eu lacinia augue, at finibus metus. Mauris vitae augue sed dui malesuada dapibus sit amet vel lectus. Nullam euismod id mauris quis malesuada. Nulla lobortis sit amet nibh at viverra. Nulla vitae est a sapien tristique mattis sed in ante. Integer scelerisque quam ac tortor congue porta.

## Interface IPlugin

Esta interfaz define dos operaciones que debe implementar un comando. Estas son:

| Operación   |  Descripción |
|:---:|----|
| **`GetDeferredDescription`**  | Obtiene una descripción de ayuda que permite dar a conocer qué hará el comando antes de ejecutarse. Vea [ejecución de comandos diferidos](../api/introducing-plugins.md#comandos-diferidos) para más información.  |
| **`Execute`**  | Ejecuta la funcionalidad del comando. |

## Uso de atributos

### CommandDescriptionAttribute

Especifica la información que describe e identifica al comando en el sistema. Define tres propiedades que es necesario establecer en el constructor de la clase.

- **DisplayDescription**: Se trata de un texto que describe la funcionalidad del plugin en el sistema.
- **DisplayName**: Se trata de un texto que establece el nombre que identificará al plugin en el sistema.
- **RequestPattern**: Se trata de un texto, patrón o expresión que inicia la invocación del comando.

> [!TIP]
> Al igual que con otras prácticas de nomenclatura, el objetivo al nombrar sus plugins es crear suficiente claridad para evitar entran en conflictos con otros plugins desarrollados por otros programadores en otras áreas o países. Recomendamos  utilizar la siguiente regla al nombrar sus plugins: `<País>.<Área><Tecnología>.<Característica>.<Comando>`, siempre que no supere 150 caracteres.

#### Ejemplo

Si su plugin o comando necesita responder a la expresión holamundo, entonces el código de atributo tendría la siguiente forma. Tenga presente que la expresión no distingue mayúsculas de minúsculas.

```c#
[CommandDescriptionAttribute("Col.Rd.Eva.Samples.HelloWorld", "Muestra un mensaje de bienvenida", "holamundo")]
public class HelloWorldPlugin : IPlugin
{
}
```

Sin embargo, la expresión anterior es un mal ejemplo. ¿Qué ocurriría si el usuario ingresa el comando, separando las palabras hola y mundo? ¿Qué ocurriría si la escribe en inglés? ¿Qué ocurriría si la abrevia a solo hw? Una mejor definición del comando seria ampliando el alcance de la expresión de reconocimiento **`RequestPattern`**, así.

```c#
[CommandDescriptionAttribute("Col.Rd.Eva.Samples.HelloWorld", "Muestra un mensaje de bienvenida", "holamundo|hola\s+mundo|hw|helloworld|hello\s+world")]
public class HelloWorldPlugin : IPlugin
{
}
```

> [!IMPORTANT]
> Conviene encontrar un punto de equilibrio entre el mantenimiento, la comprensión de la expresión y los posibles valores ingresados por los usuarios. Si la expresión de reconocimiento **`RequestPattern`** de su plugin entra en conflicto con otro plugin, el sistema generará el error **`140503`** informando al usuario que hay más de un plugin preparado para generar una respuesta.

### CommandExampleAttribute

Especifica la información que se utiliza como ejemplo del comando en el sistema. Un usuario puede consultar la lista de plugins o comandos disponibles. Este atributo define la información que se muestra al usuario. Define tres propiedades que es necesario establecer en el constructor de la clase.

- **Input** : Se trata del texto al que responde la invocación del comando.  Piense en este valor como _"cuando el usuario digite esto…"_
- **Description** : Se trata del texto que describe lo que hace el comando.  Piense en este valor como la continuación a _"cuando el usuario digite esto haré esto"_.
- **Index** : Cuando EVA muestra la lista de comandos al usuario los ordena por este campo.

## Archivo de manifiesto

Curabitur aliquet sapien sagittis, laoreet nisi vitae, varius dui. Curabitur lobortis quam elit, ac finibus lorem finibus sed. Nam quis dui rutrum, tincidunt mi a, sodales sem. Integer fringilla in mi ac ullamcorper. Nulla eu lacinia augue, at finibus metus. Mauris vitae augue sed dui malesuada dapibus sit amet vel lectus. Nullam euismod id mauris quis malesuada. Nulla lobortis sit amet nibh at viverra. Nulla vitae est a sapien tristique mattis sed in ante. Integer scelerisque quam ac tortor congue porta.

## Preparación del instalador

Curabitur aliquet sapien sagittis, laoreet nisi vitae, varius dui. Curabitur lobortis quam elit, ac finibus lorem finibus sed. Nam quis dui rutrum, tincidunt mi a, sodales sem. Integer fringilla in mi ac ullamcorper. Nulla eu lacinia augue, at finibus metus. Mauris vitae augue sed dui malesuada dapibus sit amet vel lectus. Nullam euismod id mauris quis malesuada. Nulla lobortis sit amet nibh at viverra. Nulla vitae est a sapien tristique mattis sed in ante. Integer scelerisque quam ac tortor congue porta.