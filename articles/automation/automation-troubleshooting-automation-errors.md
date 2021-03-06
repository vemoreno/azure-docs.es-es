---
title: Solución de problemas comunes de Azure Automation| Microsoft Docs
description: En este artículo se proporciona información para solucionar los errores comunes de Azure Automation.
services: automation
ms.service: automation
author: georgewallace
ms.author: gwallace
ms.date: 03/16/2018
ms.topic: article
manager: carmonm
tags: top-support-issue
keywords: error de automatización, solución de problemas, problema
ms.openlocfilehash: 9764068dd7a1a499c61695f39bff726a8ea3aac9
ms.sourcegitcommit: 48ab1b6526ce290316b9da4d18de00c77526a541
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/23/2018
---
# <a name="troubleshooting-common-issues-in-azure-automation"></a>Solución de problemas comunes en Azure Automation 
Este artículo proporciona ayuda para solucionar los errores comunes que puede experimentar en Azure Automation y sugiere posibles soluciones para resolverlos.

## <a name="authentication-errors-when-working-with-azure-automation-runbooks"></a>Errores de autenticación al trabajar con runbooks de Azure Automation
### <a name="scenario-sign-in-to-azure-account-failed"></a>Escenario: Fallo del inicio de sesión en la cuenta de Azure
**Error**: Recibe el error "Unknown_user_type: Tipo de usuario desconocido" mientras trabaja con los cmdlets Add-AzureAccount o Login-AzureRmAccount.

**Motivo del error:** este error se produce si el nombre de activo de credencial no es válido o si el nombre de usuario y la contraseña que usó para configurar el activo de credencial de Automation no son válidos.

**Sugerencias para solucionar el problema:** para determinar cuál es el problema, siga estos pasos:  

1. Asegúrese de que el nombre de activo de la credencial de Automation que use para conectarse a Azure no contenga caracteres especiales, incluido el carácter **@** .  
2. Compruebe que puede utilizar el nombre de usuario y la contraseña que se almacenan en la credencial de Azure Automation en su editor local ISE de PowerShell. Puede hacerlo ejecutando los siguientes cmdlets en el ISE de PowerShell:  

        $Cred = Get-Credential  
        #Using Azure Service Management   
        Add-AzureAccount –Credential $Cred  
        #Using Azure Resource Manager  
        Login-AzureRmAccount –Credential $Cred
3. Si la autenticación falla localmente, esto significa que no ha configurado correctamente las credenciales de Azure Active Directory. Vea la entrada de blog [Authenticating to Azure using Azure Active Directory (Autenticación en Azure mediante Azure Active Directory)](https://azure.microsoft.com/blog/azure-automation-authenticating-to-azure-using-azure-active-directory/) para conseguir configurar correctamente la cuenta de Active Directory.  

### <a name="scenario-unable-to-find-the-azure-subscription"></a>Escenario: No se encuentra la suscripción de Azure
**Error:** recibe el error "The subscription named ``<subscription name>`` cannot be found" (La suscripción denominada XX no se puede encontrar) cuando trabaja con los cmdlets de Select-AzureSubscription o seleccione AzureRmSubscription.

**Motivo del error:** este error se produce si el nombre de la suscripción no es válido o si el usuario de Azure Active Directory que está intentando obtener los detalles de suscripción no está configurado como un administrador de la suscripción.

**Sugerencias para solucionar el problema:** para determinar si se ha autenticado correctamente en Azure y tener acceso a la suscripción que intenta seleccionar, siga estos pasos:  

1. Asegúrese de que ejecuta **Add-AzureAccount** antes de ejecutar el cmdlet **Select-AzureSubscription**.  
2. Si continúa recibiendo este mensaje de error, modifique el código agregando el cmdlet **Get-AzureSubscription** a continuación del cmdlet **Add-AzureAccount** y luego ejecute el código. Ahora compruebe si la salida de Get-AzureSubscription contiene los detalles de su suscripción.  

   * Si no ve los detalles de la suscripción en la salida, esto significa que la suscripción no se ha inicializado todavía.  
   * Si ve los detalles de suscripción en la salida, confirme que está usando el nombre o el identificador correctos de la suscripción con el cmdlet **Select-AzureSubscription** .   

### <a name="scenario-authentication-to-azure-failed-because-multi-factor-authentication-is-enabled"></a>Escenario: Error de autenticación en Azure porque está habilitada la autenticación multifactor
**Error:** recibe el error "Add-AzureAccount: AADSTS50079: Es necesaria una inscripción de autenticación fuerte (proofup)" al autenticarse en Azure con el nombre de usuario y la contraseña de Azure.

**Motivo del error:** si dispone de autenticación multifactor en su cuenta de Azure, no puede usar un usuario de Azure Active Directory para autenticarse en Azure. En su lugar, tiene que utilizar un certificado o una entidad de servicio para autenticarse en Azure.

**Sugerencias para solucionar el problema**: para usar un certificado con los cmdlets del modelo de implementación clásica de Azure, consulte el artículo sobre [cómo crear y agregar un certificado para administrar los servicios de Azure](http://blogs.technet.com/b/orchestrator/archive/2014/04/11/managing-azure-services-with-the-microsoft-azure-automation-preview-service.aspx). Para usar una entidad de servicio con los cmdlets de Azure Resource Manager, consulte [Creación de aplicación de Active Directory y entidad de servicio mediante el portal](../azure-resource-manager/resource-group-create-service-principal-portal.md) y [Autenticación de una entidad de servicio con Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).

## <a name="common-errors-when-working-with-runbooks"></a>Errores comunes al trabajar con runbooks
### <a name="scenario-the-runbook-job-start-was-attempted-three-times-but-it-failed-to-start-each-time"></a>Escenario: se intentó iniciar el trabajo de runbook tres veces, pero las tres se produjo un error
**Error:** el runbook genera el error "El trabajo se ha intentado realizar tres veces, pero se produjo un error".

**Motivo del error:** este error puede deberse a las siguientes razones:  

1. Límite de memoria. Se han documentado límites en la cantidad de memoria asignada a un espacio aislado con los [límites del servicio Automation](../azure-subscription-service-limits.md#automation-limits), de modo que un trabajo puede producir un error, si está utilizando más de 400 MB de memoria. 

2. Módulo incompatible. Puede ocurrir si las dependencias del módulo no son correctas. En este caso, el runbook normalmente devuelve un mensaje similar a "Comando no encontrado" o "No se puede enlazar el parámetro". 

**Sugerencias para solucionar el problema:** cualquiera de las siguientes alternativas soluciona este problema:

* Algunos métodos sugeridos para trabajar dentro del límite de memoria son dividir la carga de trabajo entre varios runbooks, no procesar tantos datos en la memoria, no escribir el resultado innecesario de los runbooks o considerar cuántos puntos de control se escriben en los runbooks de flujo de trabajo de PowerShell.  

* Actualice los módulos de Azure siguiendo los pasos de [Actualización de módulos de Azure PowerShell en Azure Automation](automation-update-azure-modules.md).  


### <a name="scenario-runbook-fails-because-of-deserialized-object"></a>Escenario: error en runbook debido a un objeto deserializado
**Error**: El runbook falla y recibe el error "No se puede enlazar el parámetro ``<ParameterName>``. No se puede convertir el valor ``<ParameterType>`` de tipo deserializado ``<ParameterType>`` a tipo ``<ParameterType>``".

**Motivo del error:** Si su Runbook es un flujo de trabajo de PowerShell almacena objetos complejos en un formato deserializado, para conservar el estado del Runbook si se suspende el flujo de trabajo.

**Sugerencias para solucionar el problema:** cualquiera de las siguientes tres alternativas soluciona este problema:

1. Si canaliza objetos complejos de un cmdlet a otro, encapsule estos cmdlets en un InlineScript.
2. En lugar de pasar el objeto complejo entero, pase solamente el nombre o valor del mismo que necesite.
3. Use un runbook de PowerShell en lugar de un runbook de flujo de trabajo de PowerShell.

### <a name="scenario-runbook-job-failed-because-the-allocated-quota-exceeded"></a>Escenario: Error de trabajo de Runbook porque superó la cuota asignada
**Error:** Su trabajo de runbook falla y recibe el error "Se ha alcanzado la cuota para el tiempo de ejecución de trabajo mensual para esta suscripción".

**Motivo del error:** Este error se produce cuando la ejecución del trabajo supera la cuota gratuita de 500 minutos para su cuenta. Esta cuota se aplica a todos los tipos de tareas de ejecución de trabajo como realizar pruebas de un trabajo, iniciar un trabajo desde el portal, ejecutar un trabajo usando Webhook y programar un trabajo para ejecutar mediante el Portal de Azure o en su centro de datos. Para obtener más información sobre precios para, consulte [Precios de Automation](https://azure.microsoft.com/pricing/details/automation/).

**Sugerencias para solucionar el problema:** Si desea usar más de 500 minutos de procesamiento por mes tiene que cambiar la suscripción del nivel Gratis al nivel Básico. Puede actualizar al nivel Básico realizando los pasos siguientes:  

1. Inicie sesión en la suscripción de Azure  
2. Seleccione la cuenta de Automation que desee actualizar  
3. Haga clic en **Configuración** > **Precios**.
4. Haga clic en **Habilitar** en la parte inferior de la página para actualizar su cuenta al nivel **Básico**.

### <a name="scenario-cmdlet-not-recognized-when-executing-a-runbook"></a>Escenario: No se reconoce el Cmdlet cuando se ejecuta un runbook
**Error**: se produce un error en su trabajo de runbook con el mensaje "``<cmdlet name>``: El término ``<cmdlet name>`` no se reconoce como nombre de un cmdlet, una función, un archivo de script o un programa ejecutable".

**Motivo del error:** este error se produce cuando el motor de PowerShell no puede encontrar el cmdlet que está usando en su Runbook. Esto podría deberse a que el módulo que contiene el cmdlet no está presente en la cuenta, a que haya un conflicto de nombres con un nombre de runbook o a que el cmdlet también existe en otro módulo y Automation no puede resolver el nombre.

**Sugerencias para solucionar el problema:** cualquiera de las siguientes alternativas soluciona este problema:  

* Compruebe que ha escrito correctamente el nombre del cmdlet.  
* Asegúrese de que el cmdlet existe en su cuenta de Automation y de que no hay ningún conflicto. Para comprobar si está presente el cmdlet, abra un runbook en modo de edición y busque el cmdlet que quiere encontrar en la biblioteca o ejecute **Get-Command``<CommandName>``**. Una vez que haya comprobado que el cmdlet está disponible para la cuenta y que no hay conflictos de nombres con otros cmdlets o runbooks, agréguelo al lienzo y asegúrese de que está utilizando un parámetro válido establecido en su runbook.  
* Si tiene un conflicto de nombres y el cmdlet está disponible en dos módulos diferentes, puede resolver este problema mediante el nombre completo del cmdlet. Por ejemplo, puede usar **NombreDeMódulo\NombredeCmdlet**.  
* Si está ejecutando el runbook local en un grupo de trabajo híbrido, asegúrese de que el cmdlet o módulo está instalado en el equipo que hospeda el trabajo híbrido.

### <a name="scenario-a-long-running-runbook-consistently-fails-with-the-exception-the-job-cannot-continue-running-because-it-was-repeatedly-evicted-from-the-same-checkpoint"></a>Escenario: un runbook de larga duración presenta errores constantemente con la excepción: "El trabajo no se puede seguir ejecutando porque se expulsó repetidamente desde el mismo punto de control".
**Motivo del error:** el diseño de este comportamiento se debe a la supervisión de "reparto justo" de los procesos de Azure Automation, que suspende automáticamente un runbook si se ejecuta durante más de tres horas. Sin embargo, el mensaje de error devuelto no proporciona opciones para qué hacer a continuación. Un runbook se puede suspender por varios motivos. Las suspensiones se producen principalmente debido a errores. Por ejemplo, una excepción no detectada en un runbook, un error de red o un bloqueo en el servicio Runbook Worker que ejecuta el runbook hará que el runbook se suspenda y se inicie desde su último punto de control cuando se reanude.

**Sugerencias para solucionar el problema:** la solución documentada para evitar este problema consiste en usar puntos de control en un flujo de trabajo. Para más información, consulte el artículo con [información sobre los flujos de trabajo de PowerShell](automation-powershell-workflow.md#checkpoints). Encontrará una explicación más completa del "reparto equitativo" y los puntos de control en este artículo de blog [Using Checkpoints in Runbooks](https://azure.microsoft.com/blog/azure-automation-reliable-fault-tolerant-runbook-execution-using-checkpoints/)(Uso de puntos de control en los runbooks).

## <a name="common-errors-when-importing-modules"></a>Errores comunes al importar módulos
### <a name="scenario-module-fails-to-import-or-cmdlets-cant-be-executed-after-importing"></a>Escenario: No se puede importar el módulo o no se puede ejecutar cmdlets después de la importación
**Error:** un módulo no se puede importar o se importa correctamente, pero no se extrae ningún cmdlet.

**Motivo del error:** algunas razones comunes por las que un módulo no se importa correctamente a Azure Automation son:

* La estructura no coincide con la estructura que Automation necesita.
* El módulo depende de otro módulo que no se ha implementado en su cuenta de Automation.
* Al módulo le faltan sus dependencias en la carpeta.
* El cmdlet **New-AzureRmAutomationModule** se está usando para cargar el módulo y no se ha proporcionado la ruta de acceso de almacenamiento completa o no se ha cargado el módulo usando una URL de acceso público.

**Sugerencias para solucionar el problema:** cualquiera de las siguientes alternativas soluciona este problema:

* Asegúrese de que el módulo sigue el formato siguiente: NombreMódulo.Zip **->** NombreMódulo o número de versión **->** (NombreMódulo.psm1, NombreMódulo.psd1)
* Abra el archivo. psd1 y compruebe si el módulo tiene dependencias. Si es así, cargue estos módulos en la cuenta de Automation.
* Asegúrese de que todos los archivos .dll a los que se hace referencia están presentes en la carpeta del módulo.

## <a name="common-errors-when-working-with-desired-state-configuration-dsc"></a>Errores comunes al trabajar con la Configuración de estado deseado (DSC)
### <a name="scenario-node-is-in-failed-status-with-a-not-found-error"></a>Escenario: el nodo se encuentra en estado de error con el error "No encontrado"
**Error**: El nodo tiene un informe de estado de **error** que contiene el mensaje "Error al intentar obtener la acción del servidor https://``<url>``//accounts/``<account-id>``/Nodes(AgentId=``<agent-id>``)/GetDscAction porque no se encontró una configuración ``<guid>`` válida".

**Motivo del error:** este error suele ocurrir cuando se asigna al nodo un nombre de configuración (por ejemplo, ABC), en lugar de un nombre de configuración de nodo (por ejemplo, ABC.WebServer).

**Sugerencias de solución de problemas:**

* Asegúrese de estar asignando al nodo un "nombre de configuración de nodo" y no el "nombre de configuración".
* Puede asignar una configuración de nodo a un nodo mediante el Portal de Azure o con un cmdlet de PowerShell.

  * Para asignar una configuración de nodo a un nodo mediante Azure Portal, abra la página **Nodos DSC**, seleccione un nodo y haga clic en el botón **Asignar configuración de nodo**.  
  * Para asignar una configuración de nodo a un nodo mediante un cmdlet de PowerShell, use el cmdlet **AzureRmAutomationDscNode Set** .

### <a name="scenario-no-node-configurations-mof-files-were-produced-when-a-configuration-is-compiled"></a>Escenario: no se produjeron configuraciones de nodo (archivos MOF) al compilarse una configuración
**Error:** el trabajo de compilación de DSC se suspendió con el error "La compilación finalizó correctamente, pero no se generaron archivos .mof de configuración de nodo".

**Motivo del error**: cuando la expresión que aparece junto a la palabra clave **Node** en la configuración de DSC se evalúa como `$null`, no se produce ninguna configuración de nodo.

**Sugerencias para solucionar el problema:** cualquiera de las siguientes alternativas soluciona este problema:

* Asegúrese de que la expresión junto a la palabra clave **Node** en la definición de configuración no se está evaluando como $null.
* Si se pasan datos de configuración al compilar la configuración, asegúrese de que se pasan los valores esperados que la configuración necesita de [ConfigurationData](automation-dsc-compile.md#configurationdata).

### <a name="scenario-the-dsc-node-report-becomes-stuck-in-progress-state"></a>Escenario: el informe de nodo de DSC se queda bloqueado en el estado "en curso"
**Error:** el agente DSC genera el mensaje "No se encontró ninguna instancia con los valores de propiedad especificados".

**Motivo del error:** ha actualizado la versión de WMF y ha dañado WMI.

**Sugerencias para solucionar el problema:** para solucionar el problema, siga las instrucciones que se indican en la entrada del blog [DSC known issues and limitations](https://msdn.microsoft.com/powershell/wmf/5.0/limitation_dsc) (Limitaciones y problemas conocidos de DSC) para corregir el problema.

### <a name="scenario-unable-to-use-a-credential-in-a-dsc-configuration"></a>Escenario: no se puede usar una credencial en una configuración de DSC
**Error**: el trabajo de compilación de DSC se suspendió con el error "Error System.InvalidOperationException al procesar la propiedad 'Credential' de tipo ``<some resource name>``: se permite convertir y almacenar una contraseña cifrada como texto no cifrado solo si PSDscAllowPlainTextPassword se establece en true".

**Motivo del error**: ha usado una credencial en la configuración pero no ha proporcionado el valor adecuado de **ConfigurationData** para establecer **PSDscAllowPlainTextPassword** como true para cada configuración de nodo.

**Sugerencias de solución de problemas:**

* Asegúrese de que pasa el valor adecuado de **ConfigurationData** para establecer **PSAllowPlainTextPassword** como true para cada configuración de nodo mencionada en la configuración. Para más información, consulte los [recursos en DSC de Azure Automation](automation-dsc-compile.md#assets).

## <a name="common-errors-when-onboarding-solutions"></a>Errores comunes al incorporar soluciones

Al incorporar soluciones puede encontrar errores. A continuación se enumera una lista de los errores más comunes que puede encontrar.

### <a name="computergroupqueryformaterror"></a>ComputerGroupQueryFormatError

**Motivo del error:**

Este código de error significa que la consulta de búsqueda guardada del grupo de equipos que se utilizó tomando a la solución como objetivo no tenía un formato correcto. Puede que haya cambiado la consulta, o puede que lo haya hecho el sistema.

**Sugerencias de solución de problemas:**

Puede eliminar la consulta para esta solución y reincorporar la solución, con lo que se vuelve a crear la consulta. La consulta puede encontrarse en el área de trabajo, en **Búsquedas guardadas**. El nombre de la consulta es **MicrosoftDefaultComputerGroup**, y la categoría de la consulta es el nombre de la solución asociada a esta consulta. Si se habilitan varias soluciones, **MicrosoftDefaultComputerGroup** se muestra varias veces en **Búsquedas guardadas**.

### <a name="policyviolation"></a>PolicyViolation

**Motivo del error:**

Este código de error significa que no se pudo realizar la implementación debido a la infracción de una o varias directivas.

**Sugerencias de solución de problemas:**

Para implementar correctamente la solución, debe considerar modificar la directiva indicada. Dado que hay muchos tipos diferentes de directivas que se pueden definir, los cambios específicos necesarios dependen de la directiva que se ha infringido. Por ejemplo, si se define una directiva en un grupo de recursos que deniega el permiso para cambiar el contenido de ciertos tipos de recursos dentro de ese grupo de recursos podría realizar cualquiera de las siguientes acciones:

*   Eliminar por completo la directiva.
* Intentar realizar una incorporación a otro grupo de recursos.
* Revisar la directiva, por ejemplo:
   * Cambiar el destino de la directiva a un recurso concreto (por ejemplo, en cuanto a una cuenta de Automation específica).
   * Revisar el conjunto de recursos para los que se configuró en la directiva denegar el acceso.

Compruebe las notificaciones en la esquina superior derecha de Azure Portal o desplácese hasta el grupo de recursos que contiene la cuenta de Automation y seleccione **Implementaciones** en **Configuración** para ver la implementación con errores. Para más información acerca de Azure Policy, visite: [Introducción a Azure Policy](../azure-policy/azure-policy-introduction.md?toc=%2fazure%2fautomation%2ftoc.json).

## <a name="next-steps"></a>Pasos siguientes

Si ha seguido los pasos de solución de problemas anteriores y no puede encontrar la respuesta, puede revisar las opciones de soporte técnico adicionales siguientes.

* Obtener ayuda de expertos de Azure. Envíe su problema a los [foros de MSDN de Azure o Stack Overflow](https://azure.microsoft.com/support/forums/).
* Registrar un incidente de soporte técnico de Azure. Vaya al [Sitio del soporte técnico de Azure](https://azure.microsoft.com/support/options/) y haga clic en **Obtener soporte técnico** en **Soporte técnico y facturación**.
* Si está buscando una solución de Runbook o un módulo de integración de Azure Automation, publique una solicitud de script en el [Centro de scripts](https://azure.microsoft.com/documentation/scripts/) .
* Si tiene comentarios o solicitudes de características para Azure Automation, publíquelos en [User Voice](https://feedback.azure.com/forums/34192--general-feedback).
