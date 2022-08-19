# privacidad-windows-11

Configuración de privacidad para Windows 11 (valido para versiones con el editor de políticas de grupo de Windows)

> **Importante**: Esta guía ha sido fruto de recopilaciones de información en varios sitios de internet y testeado en mi equipo. De igual forma no me hago responsable de cualquier daño ocasionado. Se puede volver al estado anterior devolviendo el valor modificado a su valor inicial. No es obligatorio aplicar todas estas opciones pudiendo elegir las que mas se ajusta a sus necesidades.

## CONFIGURACIONES GENÉRICAS

**Instalar el sistema sin conectarlo a internet** y hacer estas primeras configuraciones:

* Cambiar el nombre del equipo y reiniciar

* abrir cualquier carpeta e ir a "menu - opciones" y cambiar lo siguiente:

Pestaña General:
```
Abrir el Explorador de archivos en: Este equipo
Privacidad - Desmarcar las 2 opciones (mostrar los archivos... y Mostrar las carpetas...)
```

Pestaña Ver:
```
Mostrar archivos, carpetas y unidades ocultos - Elegir (Cuidado con borrar carpetas del sistema)
Ocultar las extensiones de archivo para tipos de archivo conocidos - Quitar selección
```

### Configuración de Windows

> **Importante**: Modificar la Seguridad de Windows con las opciones a continuación deja un poco mas vulnerable tu equipo frente a amenazas de virus y demás. Si no estas seguro mejor no tocar esa parte!

Hay que ir a Inicio - configuración y elegir:


* Seguridad de Windows - Protección contra antivirus y contra amenazas (se abrirá una ventana)

*Al aplicar esta configuración suele salir de vez en cuando el icono de exclamación en la barra de tarea pero descartando el mensaje se quita*

```
Protección contra antivirus y contra amenazas - Administrar la configuración Protección basada en la nube y envío de muestras automático: Desactivado
```

*Al aplicar esta configuración suele salir de vez en cuando el icono de exclamación en la barra de tarea pero descartando el mensaje se quita*

```
Control de aplicaciones y navegador - Protección basada en reputación - Configuración de Protección basada en reputación: Desactivado todo
```

* Inicio - configuración - Privacidad y seguridad:

```
General: Desactivado todo
Voz: Desactivado
Personalización de entrada manuscrita y escritura: Desactivado
Comentarios y diagnósticos: Desactivado todo y en Frecuencias de comentarios elegir nunca
Historial de actividad: ninguna opción seleccionada
Permisos de búsqueda: Desactivado todo
Ubicación: Servicio de ubicación Desactivado
Notificaciones: Desactivado (por si te molestan que con el Windows 7 no había y no me importaba `:smile:` )
Información de cuenta: Desactivado
Diagnósticos de la aplicación: Desactivado
```

* Inicio - configuración - Windows Update

```
Opciones avanzadas - Optimización de distribución: Desactivado (Si tienes internet lento quizás vale la pena dejarlo)
```

* Inicio - configuración - Sistema - Portapapeles

```
Historial del portapapeles: Desactivado
```

* Inicio - configuración - Aplicaciones - Aplicaciones y características

```
Compartir entre dispositivos: Desactivado
```

* Inicio - configuración - Personalización

```
Inicio - Mostrar aplicaciones agregadas recientemente, Mostrar las aplicaciones más usadas y Mostrar los elementos abiertos recientemente...: Desactivado
Barra de tarea - Buscar, Widgets y Chat: Desactivado
```

* Poner el reloj en UTC (Util si tienes Dual Boot con otro sistema Operativo GNU/Linux). Hay que iniciar una terminal con derecho de administrador. Con el botón derecho del ratón encima del Inicio elegir "Terminal Windows (Administrador) y pegar el siguiente código.

```
reg add "HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\TimeZoneInformation" /v RealTimeIsUniversal /d 1 /t REG_DWORD /f
```

Este código añade en el registro de Windows la clave DWORD RealTimeIsUniversal con el valor 1 en la ruta HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\TimeZoneInformation". Si queremos volver atrás simplemente tenemos que borrar la clave del registro y reiniciar

## EDITOR DE POLÍTICA DE GRUPO

**El primer paso** seria abrir la aplicación de editor de políticas de grupo de Windows y para ello, vamos inicio (o presionando la tecla de Windows en el teclado) y escribimos:

```
gpedit.msc
```
A continuación podemos elegir que aplicar.

### Desactivar la telemetría de Windows:

Se suele enviar información de uso del sistema. Podemos desactivarla eligiendo  en la siguiente ruta "Habilitar" y en Opciones elegir "Datos de diagnóstico desactivados (no recomendado):

```
Directiva Equipo local - Configuración del equipo - Plantilla administrativa - Componentes de Windows - Recopilación de datos y versiones preliminares - Permitir datos de diagnostico
```


### Desactivar resultado webs en el menu de inicio:

Cuando le damos a inicio y escribimos el nombre de una aplicación suele salir también resultados de búsqueda entre otras cosas que ralentiza un poco el sistema. para desactivarlo tenemos que buscar y habilitar:

```
Directiva Equipo local - Configuración del equipo - Plantilla administrativa - Componentes de Windows - Buscar - No permitir búsqueda en la Web
Directiva Equipo local - Configuración del equipo - Plantilla administrativa - Componentes de Windows - Buscar - No buscar en Internet o mostrar resultados de Internet en Search
```

### Desactivar las actualizaciones de controladores desde Windows update:

**Windows actualiza automáticamente los drivers** pero en ocasiones instala una version anterior (por ejemplo los drivers de tarjeta gráfica AMD en algunos portátiles) lo que es muy molesto. Personalmente descargo los drivers directamente del fabricante. Para desactivarlo debemos ir y "Habilitar":

```
Directiva Equipo local - Configuración del equipo - Plantilla administrativa - Componentes de Windows - Windows Update - Administrar las actualizaciones ofrecidas desde Windows Update - No incluyas controladores con las actualizaciones de Windows
```

### Desactivar las actualizaciones Windows automáticamente:

**Windows descarga e instala automáticamente las actualizaciones** y si dejas el pc encendido por la noche hay ocasiones en que te lo reinicia sin preguntar. Una opción es desactivar las actualizaciones automáticas de forma que te avise cuando haya actualizaciones y tu elijes cuando instalarlas y reiniciar. Tener en cuenta que cuando hay actualizaciones para la base de datos de Windows Defender también lo avisa asi que el mensaje de que hay actualizaciones es muy frecuente pero he encontrado como dejar activado automáticamente solo la base de datos del antivirus. Para desactivarlas debemos Habilitar y en Opciones seleccionar la opción 2  :

```
Directiva Equipo local - Configuración del equipo - Plantilla administrativa - Componentes de Windows - Windows Update - Administrar la experiencia del usuario final - Configurar Actualizaciones  automáticas
```

### Deshabilitar los widget:

**Los widget consume recursos del equipo** y si no los vas a utilizar los puedes desactivar  deshabilitando la siguiente directiva:

```
Directiva Equipo local - Configuración del equipo - Plantilla administrativa - Componentes de Windows - Widget - Permitir widgets
```

### SERVICIOS

**Aunque hemos desactivado la telemetría desde el editor de política de grupo** también podemos desactivar un servicio que se encarga de recopilar información. No se hasta que punto es necesario hacerlo teniendo los pasos anteriores. Lo 1º que tenemos que hacer es ir a inicio y escribir:

```
services.msc
```

Entonces tenemos que "Parar" y "Deshabilitar" el siguiente Servicio:

```
Experiencias del usuario y telemetría asociadas
```

### TAREAS

**Desactivar tareas relacionadas con la privacidad** que también hace que recuperemos recursos de la maquina. La ventaja de desactivarlas frente a eliminarlas es que siempre se puede volver para atrás y es posible que con una actualización futura vuelva a aparecer. Para ello tenemos que "deshabilitar" las 2 siguientes tareas programadas (con el botón derecha encima):

```
Programador de tareas (local) - Biblioteca del Programador de tareas - Microsoft - Windows - Application Experience - Microsoft Compatibility Appraiser
Programador de tareas (local) - Biblioteca del Programador de tareas - Microsoft - Windows - Application Experience - ProgramDataUpdater
```

### PASOS FINALES

**A esta altura** solo quedaría reiniciar e instalar los drivers del equipo. Entonces cuando este todo instalado se puede conectar el dispositivo a internet, configurar la Zona Horaria, sincronizar la hora, buscar actualizaciones de Windows, reiniciar, buscar actualizaciones en la Store de Microsoft, volver a reiniciar y desinstalar las aplicaciones preinstaladas que uno no desea (ejemplo la aplicación de noticias, Microsoft Team, etc... )

Si tiene una cuenta con Xbox Game Pass tienes una opciones a la hora de añadir la cuenta en la aplicación y en el ultimo paso poner que solo se use para las aplicaciones de Microsoft. Después en Configuración - Cuentas - Correo electrónico y cuentas se selecciona la cuenta añadida y en "Opciones de inicio de sesión" elegir "Las aplicaciones deben pedirme permiso par usar esta cuenta"
