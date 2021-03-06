---
title: 'Azure PowerShell: Konfigurieren von VM-Skalierungsgruppen mit einer vorhandenen Azure Load Balancer-Instanz'
description: Erfahren Sie, wie Sie eine VM-Skalierungsgruppe mit einer vorhandenen Azure Load Balancer-Instanz konfigurieren.
author: asudbring
ms.author: allensu
ms.service: load-balancer
ms.topic: how-to
ms.date: 03/26/2020
ms.openlocfilehash: 858315008434f511e3adc0a91d591d924634fc39
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "84809503"
---
# <a name="configure-a-virtual-machine-scale-set-with-an-existing-azure-load-balancer-using-azure-powershell"></a>Konfigurieren einer VM-Skalierungsgruppe mit einer vorhandenen Azure Load Balancer-Instanz mithilfe von Azure PowerShell

In diesem Artikel erfahren Sie, wie Sie eine VM-Skalierungsgruppe mit einer vorhandenen Azure Load Balancer-Instanz konfigurieren. 

## <a name="prerequisites"></a>Voraussetzungen

- Ein Azure-Abonnement.
- Ein vorhandener Standard-SKU-Lastenausgleich in dem Abonnement, in dem die VM-Skalierungsgruppe bereitgestellt werden soll
- Eine Azure Virtual Network-Instanz für die VM-Skalierungsgruppe

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)] 

[!INCLUDE [updated-for-az](../../includes/updated-for-az.md)]

## <a name="sign-in-to-azure-cli"></a>Anmelden bei der Azure-Befehlszeilenschnittstelle

Melden Sie sich bei Azure an.

```azurepowershell-interactive
Connect-AzAccount
```

## <a name="deploy-a-virtual-machine-scale-set-with-existing-load-balancer"></a>Bereitstellen einer VM-Skalierungsgruppe mit einem vorhandenen Lastenausgleich

Ersetzen Sie die Werte in den spitzen Klammern durch die Namen der Ressourcen in Ihrer Konfiguration.

```azurepowershell-interactive

$rsg = <resource-group>
$loc = <location>
$vms = <vm-scale-set-name>
$vnt = <virtual-network>
$sub = <subnet-name>
$lbn = <load-balancer-name>
$pol = <upgrade-policy-mode>

$lb = Get-AzLoadBalancer -ResourceGroupName $rsg -Name $lbn

New-AzVmss -ResourceGroupName $rsg -Location $loc -VMScaleSetName $vms -VirtualNetworkName $vnt -SubnetName $sub -LoadBalancerName $lb -UpgradePolicyMode $pol

```

Im folgenden Beispiel wird eine VM-Skalierungsgruppe mit den folgenden Ressourcen bereitgestellt:

- Eine VM-Skalierungsgruppe namens **myVMSS**
- Ein Azure-Lastenausgleich namens **myLoadBalancer**
- Ein Back-End-Pool für den Lastenausgleich namens **myBackendPool**
- Ein virtuelles Azure-Netzwerk namens **myVnet**
- Ein Subnetz namens **mySubnet**
- Eine Ressourcengruppe namens **myResourceGroup**

```azureppowershell-interactive

$rsg = "myResourceGroup"
$loc = "East US 2"
$vms = "myVMSS"
$vnt = "myVnet"
$sub = "mySubnet"
$pol = "Automatic"
$lbn = "myLoadBalancer"

$lb = Get-AzLoadBalancer -ResourceGroupName $rsg -Name $lbn

New-AzVmss -ResourceGroupName $rsg -Location $loc -VMScaleSetName $vms -VirtualNetworkName $vnt -SubnetName $sub -LoadBalancerName $lb -UpgradePolicyMode $pol
```
> [!NOTE]
> Nachdem die Skalierungsgruppe erstellt wurde, kann der Back-End-Port für eine Lastenausgleichsregel, die von einem Integritätstest des Load Balancers verwendet wird, nicht mehr geändert werden. Zum Ändern des Ports können Sie den Integritätstest entfernen, indem Sie die Azure-VM-Skalierungsgruppe aktualisieren, den Port aktualisieren und dann den Integritätstest erneut konfigurieren.

## <a name="next-steps"></a>Nächste Schritte

In diesem Artikel haben Sie eine VM-Skalierungsgruppe mit einer vorhandenen Azure Load Balancer-Instanz konfiguriert.  Weitere Informationen über VM-Skalierungsgruppen und Lastenausgleiche finden Sie unter:

- [Was versteht man unter Azure Load Balancer?](load-balancer-overview.md)
- [Was sind Skalierungsgruppen für virtuelle Computer?](../virtual-machine-scale-sets/overview.md)
                                