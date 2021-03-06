---
title: Actualización 1 de App Service en Azure Stack | Microsoft Docs
description: Conozca el contenido de la actualización 1 para App Service en Azure Stack, los problemas conocidos y la ubicación dónde debe descargarse.
services: azure-stack
documentationcenter: ''
author: apwestgarth
manager: stefsch
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2018
ms.author: anwestg
ms.reviewer: brenduns
ms.openlocfilehash: 0c33c8fdefbb27ba8414e58bed1b42ee7aaba88a
ms.sourcegitcommit: 8aab1aab0135fad24987a311b42a1c25a839e9f3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/16/2018
---
# <a name="app-service-on-azure-stack-update-one-release-notes"></a>Notas de la versión de la actualización 1 de App Service en Azure Stack

*Se aplica a: sistemas integrados de Azure Stack y Kit de desarrollo de Azure Stack*

Estas notas de la versión describen las mejoras y correcciones de la actualización 1 de Azure App Service en Azure Stack y todos los problemas conocidos. Los problemas conocidos se dividen en aquellos que están relacionados directamente con el proceso de actualización y aquellos que están relacionados con la compilación (posteriores a la instalación).

> [!IMPORTANT]
> Aplique la actualización 1802 al sistema integrado de Azure Stack o implemente el kit de desarrollo de Azure Stack más reciente antes de implementar Azure App Service.
>
>

## <a name="build-reference"></a>Referencia de compilación

El número de compilación de la actualización 1 de App Service en Azure Stack es **69.0.13698.9**

### <a name="prerequisites"></a>requisitos previos

> [!IMPORTANT]
> Azure App Service en Azure Stack requiere ahora un [certificado comodín con tres firmantes](azure-stack-app-service-before-you-get-started.md#get-certificates) debido a las mejoras en la forma en que se trata SSO para Kudu en este momento en Azure App Service.  El nuevo tema es ** *. sso.appservice.<region>. <domainname>.<extension>**
>
>

Remítase a la [documentación de introducción](azure-stack-app-service-before-you-get-started.md) antes de comenzar la implementación.

### <a name="new-features-and-fixes"></a>Nuevas características y correcciones

La actualización 1 de Azure App Service en Azure Stack incluye las siguientes correcciones y mejoras:

- **Alta disponibilidad de Azure App Service**: la actualización 1802 de Azure Stack permitía que las cargas de trabajo se implementaran en dominios con errores.  Por lo tanto, la infraestructura de App Service es tolerante a errores ya que se implementará en dominios con error.  De forma predeterminada, todas las nuevas implementaciones de Azure App Service tendrán esta funcionalidad; sin embargo, para las implementaciones secundarias completadas antes de que se aplicara la actualización 1802 de Azure Stack, consulte la [documentación del dominio de error de App Service](azure-stack-app-service-fault-domain-update.md).

- **Implementación en la red virtual existente**: los clientes ahora pueden implementar App Service en Azure Stack dentro de una red virtual existente.  La implementación de una red virtual existente permite a los clientes conectarse al servidor de archivos y a SQL Server, lo que es necesario para Azure App Service, a través de puertos privados.  Durante la implementación, los clientes pueden seleccionar llevarla a cabo en una red virtual existente, sin embargo [deben crear subredes para que App Service las use](azure-stack-app-service-before-you-get-started.md#virtual-network) antes de la implementación.

- Actualizaciones de las **herramientas de Kudu, los portales de Functions, Admin e inquilino de App Service**.  Es coherente con la versión del SDK de Azure Stack Portal.

- **Actualizaciones de las herramientas y plataformas de aplicaciones siguientes**:
    - Se agregó compatibilidad con **.Net Core 2.0**
    - Versiones de **Node.JS** agregadas:
        - 6.11.2
        - 6.11.5
        - 7.10.1
        - 8.0.0
        - 8.1.4
        - 8.4.0
        - 8.5.0
        - 8.7.0
        - 8.8.1
        - 8.9.0
    - Versiones de **NPM** agregadas:
        - 3.10.10
        - 4.2.0
        - 5.0.0
        - 5.0.3
        - 5.3.0
        - 5.4.2
        - 5.5.1
    - Actualizaciones de **PHP** agregadas:
        - 5.6.32
        - 7.0.26 (x86 y x64)
        - 7.1.12 (x86 y x64)
    - **Git para Windows** actualizado a v 2.14.1
    - **Mercurial** actualizado a v4.5.0

  - Se agregó compatibilidad con la característica **solo para HTTPS**  dentro de la característica de dominio personalizado en el portal de inquilinos de App Service. 

  - Se agregó la validación de la conexión de almacenamiento en el selector de almacenamiento personalizado para Azure Functions 

#### <a name="fixes"></a>Correcciones

- Al crear un paquete de implementación sin conexión, los clientes ya no recibirán un mensaje de error de acceso denegado al abrir la carpeta desde el instalador de App Service

- Se resuelven los problemas que se producen cuando se trabaja en la característica de dominios personalizados en el portal de inquilinos de App Service.

- Se evita que los clientes usen durante la instalación nombres de administrador reservados

- Se habilita la implementación de App Service con un servidor de archivos **unido a un dominio**

- Se mejora la recuperación del certificado raíz de Azure Stack en un script y se comprueba ahora el certificado raíz en el instalador de App Service.

- Se devuelve un estado incorrecto fijo a Azure Resource Manager cuando se elimina una suscripción que contenía recursos en el espacio de nombres Microsoft.Web.

### <a name="known-issues-with-the-deployment-process"></a>Problemas conocidos relacionados con el proceso de implementación

- No hay ningún problema conocido para la implementación de la actualización 1 de Azure App Service en Azure Stack.

### <a name="known-issues-with-the-update-process"></a>Problemas conocidos relacionados con el proceso de actualización

- No hay ningún problema conocido para la actualización 1 de Azure App Service en Azure Stack.

### <a name="known-issues-post-installation"></a>Problemas conocidos (posteriores a la instalación)

- No hay ningún problema conocido para la instalación de la actualización 1 de Azure App Service en Azure Stack.

### <a name="known-issues-for-cloud-admins-operating-azure-app-service-on-azure-stack"></a>Problemas conocidos para los administradores en la nube que trabajan con Azure App Service en Azure Stack

Consulte la documentación de las [notas de la versión de Azure Stack 1802](azure-stack-update-1802.md)

## <a name="see-also"></a>Otras referencias

- Para obtener información general de Azure App Service, consulte la [Información general de Azure App Service en Azure Stack](azure-stack-app-service-overview.md).
- Para obtener más información acerca de cómo prepararse para implementar App Service en Azure Stack, consulte [Antes de empezar a trabajar con App Service en Azure Stack](azure-stack-app-service-before-you-get-started.md).
