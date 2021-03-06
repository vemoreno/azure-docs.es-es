# [Documentación de Virtual Network](index.md)

# Información general
## [Redes virtuales](virtual-networks-overview.md)
## [Enrutamiento](virtual-networks-udr-overview.md)
## [Emparejamiento de redes virtuales](virtual-network-peering-overview.md)
## [Puntos de conexión del servicio de redes virtuales](virtual-network-service-endpoints-overview.md)
## [Red virtual para los servicios de Azure](virtual-network-for-azure-services.md)
## [Seguridad](security-overview.md)
## [Redes de contenedores](container-networking.md)
## [Continuidad del negocio](virtual-network-disaster-recovery-guidance.md)
## [Direccionamiento IP](virtual-network-ip-addresses-overview-arm.md)
## [Protección contra DDOS](ddos-protection-overview.md)
## [Preguntas más frecuentes](virtual-networks-faq.md)
## Clásico
### [Direccionamiento IP](virtual-network-ip-addresses-overview-classic.md)
### [Listas de control de acceso](virtual-networks-acl.md)

# Introducción
## [Creación de red virtual: Portal](quick-create-portal.md)
## [Creación de red virtual: PowerShell](quick-create-powershell.md)
## [Creación de red virtual: CLI de Azure](quick-create-cli.md)

# Procedimientos
## Planeamiento y diseño
### [Redes virtuales](virtual-network-vnet-plan-design-arm.md)
### [Grupos de seguridad de red](virtual-networks-nsg.md)

## Implementación

### Grupos de seguridad de red
#### [Azure Portal](virtual-networks-create-nsg-arm-pportal.md)
#### [Azure PowerShell](virtual-networks-create-nsg-arm-ps.md)
#### [CLI de Azure](virtual-networks-create-nsg-arm-cli.md)
#### [Plantilla](virtual-networks-create-nsg-arm-template.md)
#### [Grupos de seguridad de la aplicación](create-network-security-group-preview.md)
#### Clásico
##### [Azure PowerShell](virtual-networks-create-nsg-classic-ps.md)
##### [CLI de Azure 1.0](virtual-networks-create-nsg-classic-cli.md)

### Tablas de ruta
#### [Azure Portal](tutorial-create-route-table-portal.md)
#### [Azure PowerShell](tutorial-create-route-table-powershell.md)
#### [CLI de Azure](tutorial-create-route-table-cli.md)
#### [Plantilla](virtual-network-create-udr-arm-template.md)
#### Clásico
##### [Azure PowerShell](virtual-network-create-udr-classic-ps.md)
##### [CLI de Azure](virtual-network-create-udr-classic-cli.md)

### Emparejamiento de redes virtuales de Azure
#### Mismo modelo de implementación, misma suscripción
##### [Azure Portal](tutorial-connect-virtual-networks-portal.md)
##### [Azure PowerShell](tutorial-connect-virtual-networks-powershell.md)
##### [CLI de Azure](tutorial-connect-virtual-networks-cli.md)
#### [Mismo modelo de implementación, diferentes suscripciones](create-peering-different-subscriptions.md)
#### [Diferentes modelos de implementación, misma suscripción](create-peering-different-deployment-models.md)
#### [Diferentes modelos de implementación, diferentes suscripciones](create-peering-different-deployment-models-subscriptions.md)

### Puntos de conexión del servicio Virtual Network
#### [Azure Portal](tutorial-restrict-network-access-to-resources.md)
#### [Azure PowerShell](tutorial-restrict-network-access-to-resources-powershell.md)
#### [CLI de Azure](tutorial-restrict-network-access-to-resources-cli.md)

### Máquinas virtuales
#### [Rendimiento de red de máquinas virtuales](virtual-machine-network-throughput.md)
#### Creación de una máquina virtual con una dirección IP pública estática
##### [Azure Portal](virtual-network-deploy-static-pip-arm-portal.md)
##### [Azure PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
##### [CLI de Azure](virtual-network-deploy-static-pip-arm-cli.md)
##### [Plantilla](virtual-network-deploy-static-pip-arm-template.md)
##### Clásico
###### [Azure PowerShell](virtual-networks-reserved-public-ip.md)

#### Creación de máquina virtual: Dirección IP privada estática
##### [Azure Portal](virtual-networks-static-private-ip-arm-pportal.md)
##### [Azure PowerShell](virtual-networks-static-private-ip-arm-ps.md)
##### [CLI de Azure](virtual-networks-static-private-ip-arm-cli.md)
##### Clásico
###### [Azure Portal](virtual-networks-static-private-ip-classic-pportal.md)
###### [Azure PowerShell](virtual-networks-static-private-ip-classic-ps.md)
###### [CLI de Azure](virtual-networks-static-private-ip-classic-cli.md)

#### Creación de máquina virtual: Varias interfaces de red
##### [Azure PowerShell](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
##### [CLI de Azure](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
##### [Plantilla](virtual-network-deploy-multinic-arm-template.md)

##### Clásico
###### [Azure PowerShell](virtual-network-deploy-multinic-classic-ps.md)
###### [CLI de Azure](virtual-network-deploy-multinic-classic-cli.md)

#### Creación de máquina virtual: Varias direcciones IP
##### [Azure Portal](virtual-network-multiple-ip-addresses-portal.md)
##### [Azure PowerShell](virtual-network-multiple-ip-addresses-powershell.md)
##### [CLI de Azure](virtual-network-multiple-ip-addresses-cli.md)
##### [Plantilla](virtual-network-multiple-ip-addresses-template.md)

#### Creación de máquina virtual: Redes aceleradas
##### [Azure PowerShell](create-vm-accelerated-networking-powershell.md)
##### [CLI de Azure](create-vm-accelerated-networking-cli.md)

### Escenarios de conectividad
#### [De red virtual (VNet) a red virtual](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
#### [De red virtual (Resource Manager) a red virtual (clásica)](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
#### [De red virtual a red local (VPN)](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
#### [De red virtual a red local (ExpressRoute)](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
#### [Arquitectura de red híbrida de alta disponibilidad](../guidance/guidance-hybrid-network-expressroute-vpn-failover.md?toc=%2fazure%2fvirtual-network%2ftoc.json)

### Escenarios de seguridad
#### [Protección de redes con aplicaciones virtuales](virtual-network-scenario-udr-gw-nva.md)
#### [Red perimetral entre Internet y Azure](../guidance/guidance-iaas-ra-secure-vnet-dmz.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
#### [Servicio en la nube y seguridad de red](../best-practices-network-security.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
##### [Creación de una red perimetral con grupos de seguridad de red](virtual-networks-dmz-nsg.md)
##### [Creación de una red perimetral con grupos de seguridad de red (modelo clásico)](virtual-networks-dmz-nsg-asm.md)
##### [Creación de una red perimetral con firewall y grupos de seguridad de red (modelo clásico)](virtual-networks-dmz-nsg-fw-asm.md)
##### [Red perimetral con firewall, enrutamiento definido por el usuario y grupos de seguridad de red (modelo clásico)](virtual-networks-dmz-nsg-fw-udr-asm.md)

##### [Aplicación de ejemplo](virtual-networks-sample-app.md)

### Clásico
#### [Red virtual](create-virtual-network-classic.md)
##### [Azure Portal](virtual-networks-create-vnet-classic-pportal.md)
##### [Azure PowerShell](virtual-networks-create-vnet-classic-netcfg-ps.md)
##### [CLI de Azure](virtual-networks-create-vnet-classic-cli.md)
#### [Especificación de una configuración DNS en un archivo de configuración de red virtual](virtual-networks-specifying-a-dns-settings-in-a-virtual-network-configuration-file.md)
#### [Especificación de la configuración DNS en un archivo de configuración del servicio](virtual-networks-specifying-dns-settings-in-a-service-configuration-file.md)

## Configuración
### Máquinas virtuales
#### [Adición o eliminación de interfaces de red](virtual-network-network-interface-vm.md)
#### [Resolución de nombres para las máquinas virtuales y servicios en la nube](virtual-networks-name-resolution-for-vms-and-role-instances.md)
#### [Uso de DNS dinámico para registrar nombres de host en su propio servidor DNS](virtual-networks-name-resolution-ddns.md)
#### [Optimización del rendimiento de la red](virtual-network-optimize-network-bandwidth.md)
#### [Visión y modificación de nombres de host](virtual-networks-viewing-and-modifying-hostnames.md)
#### Clásico
##### Direcciones IP estáticas
###### [PowerShell](virtual-networks-reserved-private-ip.md)
###### [CLI](virtual-networks-static-private-ip-classic-cli.md)
##### [Dirección IP pública en el nivel de instancia](virtual-networks-instance-level-public-ip.md)

### Clásico
#### Listas de control de acceso
##### [Azure Portal](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
##### [Azure PowerShell](virtual-networks-acl-powershell.md)

## administración
### [Redes virtuales](manage-virtual-network.md)
#### [Subredes](virtual-network-manage-subnet.md)
#### [Emparejamientos](virtual-network-manage-peering.md)
#### Clásico
##### [Archivo de configuración de red](virtual-networks-using-network-configuration-file.md)
##### [Migración de un grupo de afinidad a una región](virtual-networks-migrate-to-regional-vnet.md)
### Grupos de seguridad de red
#### [Azure Portal](virtual-network-manage-nsg-arm-portal.md)
#### [Azure PowerShell](virtual-network-manage-nsg-arm-ps.md)
#### [CLI de Azure](virtual-network-manage-nsg-arm-cli.md)

#### [Registros](virtual-network-nsg-manage-log.md)
### [Tablas de ruta](manage-route-table.md)
### Interfaces de red (NIC)
#### [Creación, cambio o eliminación de interfaces de red](virtual-network-network-interface.md)
#### [Adición, cambio o eliminación de direcciones IP](virtual-network-network-interface-addresses.md)
### Máquinas virtuales
#### [Movimiento de VM a una subred diferente](virtual-networks-move-vm-role-to-subnet.md)
### [Direcciones IP públicas](virtual-network-public-ip-address.md)
### Protección contra DDOS
#### [Azure Portal](ddos-protection-manage-portal.md)
#### [Azure PowerShell](ddos-protection-manage-ps.md)

## Solución de problemas
### Grupos de seguridad de red
#### [Azure Portal](virtual-network-nsg-troubleshoot-portal.md)
#### [Azure PowerShell](virtual-network-nsg-troubleshoot-powershell.md)
### Rutas
#### [Azure Portal](virtual-network-routes-troubleshoot-portal.md)
#### [Azure PowerShell](virtual-network-routes-troubleshoot-powershell.md)
### [Pruebas de rendimiento](virtual-network-bandwidth-testing.md)
### [No se pueden eliminar redes virtuales](virtual-network-troubleshoot-cannot-delete-vnet.md)
### [Problemas de conectividad entre máquinas virtuales](virtual-network-troubleshoot-connectivity-problem-between-vms.md)
### [Configuración de PTR para comprobación de banners de SMTP](create-ptr-for-smtp-service.md)

## Scripts de ejemplo
### [CLI de Azure](cli-samples.md)
### [Azure PowerShell](powershell-samples.md)

# Referencia
## [Ejemplos de código](https://azure.microsoft.com/resources/samples/?service=virtual-network)
## [Azure PowerShell (Resource Manager)](/powershell/module/azurerm.network)
## [Azure PowerShell (clásico)](/powershell/module/azure/)
## [CLI de Azure](/cli/azure/network)
## [Java](/java/api/)
## [REST (Resource Manager)](https://msdn.microsoft.com/library/mt163658.aspx)
## [REST (clásico)](https://msdn.microsoft.com/library/jj157182.aspx)


# Temas relacionados
## [Virtual Machines](/azure/virtual-machines/)
## [Application Gateway](/azure/application-gateway/)
## [DNS de Azure](/azure/dns/)
## [Traffic Manager](/azure/traffic-manager/)
## [Equilibrador de carga](/azure/load-balancer/)
## [VPN Gateway](/azure/vpn-gateway/)
## [ExpressRoute](/azure/expressroute/)

# Recursos
## [Azure Roadmap](https://azure.microsoft.com/roadmap/?category=networking)
## [Blog de redes](http://azure.microsoft.com/blog/topics/networking)
## [Foro de redes](https://social.msdn.microsoft.com/Forums/azure/home?forum=WAVirtualMachinesVirtualNetwork)
## [Precios](https://azure.microsoft.com/pricing/details/virtual-network)
## [Calculadora de precios](https://azure.microsoft.com/pricing/calculator/)
## [Desbordamiento de la pila](http://stackoverflow.com/questions/tagged/azure-virtual-network)
## [Proveedor de recursos de red](resource-groups-networking.md)
