---
title: 'Azure PowerShell-Skriptbeispiel: Konfigurieren einer VNET-zu-VNET-VPN-Verbindung | Microsoft-Dokumentation'
description: Konfigurieren einer Site-to-Site-VPN-Verbindung (S2S)
services: vpn-gateway
documentationcenter: vpn-gateway
author: cherylmc
manager: jpconnock
editor: ''
tags: ''
ms.assetid: ''
ms.service: vpn-gateway
ms.devlang: powershell
ms.topic: sample
ms.tgt_pltfrm: ''
ms.workload: infrastructure
ms.date: 05/02/2018
ms.author: anzaman
ms.openlocfilehash: 0d93161cbc30ea1e310e35cb22f6bb7f6ebbf6e5
ms.sourcegitcommit: eb75f177fc59d90b1b667afcfe64ac51936e2638
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/16/2018
ms.locfileid: "34210850"
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-powershell"></a>Konfigurieren einer VNet-zu-VNet-VPN-Gatewayverbindung mithilfe von PowerShell

Dieses Skript stellt zwischen zwei virtuellen Netzwerken eine VNET-zu-VNET-Verbindung her.

```azurepowershell-interactive
# Declare variables for VNET 1
  $RG1 = "TestRG1"
  $VNetName1  = "VNet1"
  $FESubName1 = "FrontEnd"
  $BESubName1 = "Backend"
  $GWSubName1 = "GatewaySubnet"
  $VNetPrefix11 = "10.1.0.0/16"
  $FESubPrefix1 = "10.1.0.0/24"
  $BESubPrefix1 = "10.1.1.0/24"
  $GWSubPrefix1 = "10.1.255.0/27"
  $RG = "TestRG1"
  $Location1 = "East US"
  $GWName1 = "VNet1GW"
  $GWIPName1 = "VNet1GWIP"
  $GWIPconfName1 = "gwipconfig1"
  $Connection12 = "VNet1toVNet2"
  
# Declare variables for VNET 2  
  $RG2 = "TestRG2"
  $VNetName2  = "VNet2"
  $FESubName2 = "FrontEnd"
  $BESubName2 = "Backend"
  $GWSubName2 = "GatewaySubnet"
  $VNetPrefix21 = "10.2.0.0/16"
  $FESubPrefix2 = "10.2.0.0/24"
  $BESubPrefix2 = "10.2.1.0/24"
  $GWSubPrefix2 = "10.2.255.0/27"
  $Location2 = "East US"
  $GWName2 = "VNet2GW"
  $GWIPName2 = "VNet2GWIP"
  $GWIPconfName2 = "gwipconfig2"
  $Connection21 = "VNet2toVNet1"
# Create a resource group
New-AzureRmResourceGroup -Name TestRG1 -Location EastUS
# Create a virtual network 1
$virtualNetwork1 = New-AzureRmVirtualNetwork `
  -ResourceGroupName $RG1 `
  -Location EastUS `
  -Name VNet1 `
  -AddressPrefix 10.1.0.0/16
# Create a subnet configuration
$subnetConfig1 = Add-AzureRmVirtualNetworkSubnetConfig `
  -Name Frontend `
  -AddressPrefix 10.1.0.0/24 `
  -VirtualNetwork $virtualNetwork1
# Set the subnet configuration for virtual network 1
$virtualNetwork1 | Set-AzureRmVirtualNetwork
# Add a gateway subnet
$vnet1 = Get-AzureRmVirtualNetwork -ResourceGroupName $RG1 -Name VNet1
Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.1.255.0/27 -VirtualNetwork $vnet1
# Set the subnet configuration for the virtual network
$virtualNetwork1 | Set-AzureRmVirtualNetwork
# Request a public IP address
$gwpip1= New-AzureRmPublicIpAddress -Name VNet1GWIP -ResourceGroupName $RG1 -Location 'East US' `
 -AllocationMethod Dynamic
# Create the gateway IP address configuration
$vnet1 = Get-AzureRmVirtualNetwork -Name VNet1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet1
$gwipconfig1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name gwipconfig1 -SubnetId $subnet.Id -PublicIpAddressId $gwpip1.Id
# Create the VPN gateway
New-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName $RG1 `
 -Location 'East US' -IpConfigurations $gwipconfig -GatewayType Vpn `
 -VpnType RouteBased -GatewaySku VpnGw1 
# Create the second resource group
New-AzureRmResourceGroup -Name $RG2 -Location EastUS
# Create a virtual network 2
$virtualNetwork1 = New-AzureRmVirtualNetwork `
  -ResourceGroupName $RG2 `
  -Location EastUS `
  -Name VNet2 `
  -AddressPrefix 10.2.0.0/16
# Create a subnet configuration
$subnetConfig2 = Add-AzureRmVirtualNetworkSubnetConfig `
  -Name Frontend `
  -AddressPrefix 10.2.0.0/24 `
  -VirtualNetwork $virtualNetwork2
# Set the subnet configuration for virtual network 2
$virtualNetwork2 | Set-AzureRmVirtualNetwork
# Add a gateway subnet
$vnet2 = Get-AzureRmVirtualNetwork -ResourceGroupName $RG2 -Name VNet2
Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.2.255.0/27 -VirtualNetwork $vnet2
# Set the subnet configuration for the virtual network
$virtualNetwork2 | Set-AzureRmVirtualNetwork
# Request a public IP address
$gwpip2 = New-AzureRmPublicIpAddress -Name VNet2GWIP -ResourceGroupName $RG2 -Location 'East US' `
 -AllocationMethod Dynamic
# Create the gateway IP address configuration
$vnet2 = Get-AzureRmVirtualNetwork -Name VNet2 -ResourceGroupName $RG2
$subnet2 = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet2
$gwipconfig2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name gwipconfig2 -SubnetId $subnet.Id -PublicIpAddressId $gwpip1.Id
# Create the VPN gateway
New-AzureRmVirtualNetworkGateway -Name VNet2GW -ResourceGroupName $RG2 `
 -Location 'East US' -IpConfigurations $gwipconfig2 -GatewayType Vpn `
 -VpnType RouteBased -GatewaySku VpnGw1
# Create the connections
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 `
-VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 `
-ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 `
-VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 `
-ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
 ```
 
## <a name="clean-up-resources"></a>Bereinigen von Ressourcen

Wenn Sie die erstellten Ressourcen nicht mehr benötigen, löschen Sie die Ressourcengruppe mit dem Befehl [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup). Damit löschen Sie die Ressourcengruppe mit allen enthaltenen Ressourcen.

```azurepowershell-interactive
Remove-AzureRmResourceGroup -Name TestRG1
Remove-AzureRmResourceGroup -Name TestRG2
```
 
 
 ## <a name="script-explanation"></a>Erläuterung des Skripts

Dieses Skript verwendet die folgenden Befehle zum Erstellen der Bereitstellung. Jedes Element in der Tabelle ist mit der befehlsspezifischen Dokumentation verknüpft.

| Get-Help | Notizen |
|---|---|
| [Add-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig) | Fügt eine Subnetzkonfiguration hinzu. Diese Konfiguration wird mit dem Prozess der Erstellung des virtuellen Netzwerks verwendet. |
| [Get-AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork) | Ruft Details zu einem virtuellen Netzwerk ab. |
| [Get-AzureRmVirtualNetworkGateway](/powershell/module/azurerm.network/get-azurermvirtualnetworkgateway) | Ruft Details zu einem Gateway für virtuelle Netzwerke ab. |
| [Get-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | Ruft Details zur Subnetzkonfiguration für virtuelle Netzwerke ab. |
| [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Erstellt eine Ressourcengruppe, in der alle Ressourcen gespeichert sind. |
| [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | Erstellt eine Subnetzkonfiguration. Diese Konfiguration wird mit dem Prozess der Erstellung des virtuellen Netzwerks verwendet. |
| [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | Erstellen Sie ein virtuelles Netzwerk. |
| [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) | Erstellt eine öffentliche IP-Adresse. |
| [New-AzureRmVirtualNetworkGatewayIpConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworkgatewayipconfig) | Erstellt eine neue Gateway-IP-Konfiguration. |
| [New-AzureRmVirtualNetworkGateway](/powershell/module/azurerm.resources/new-azurermvirtualnetworkgateway) | Erstellt ein VPN-Gateway. |
| [New-AzureRmVirtualNetworkGatewayConnection](/powershell/module/azurerm.resources/ new-azurermvirtualnetworkgatewayconnection) | Erstellt eine VNET-zu-VNET-Verbindung. |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | Entfernt eine Ressourcengruppe und alle darin enthaltenen Ressourcen. |
| [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) | Legt die Subnetzkonfiguration für das virtuelle Netzwerk fest. |
| [Set-AzureRmVirtualNetworkGateway](/powershell/module/azurerm.network/set-azurermvirtualnetworkgateway) | Legt die Konfiguration für das VPN-Gateway fest. |

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zum Azure PowerShell-Modul finden Sie in der [Azure PowerShell-Dokumentation](/powershell/azure/overview).