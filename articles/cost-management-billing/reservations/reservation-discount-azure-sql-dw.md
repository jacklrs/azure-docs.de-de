---
title: Anwendung von Reservierungsrabatten auf Azure Synapse Analytics | Microsoft-Dokumentation
description: Hier erfahren Sie, wie Reservierungsrabatte auf Azure Synapse Analytics angewendet werden und Sie Geld sparen können.
author: yashesvi
ms.reviewer: yashar
ms.service: cost-management-billing
ms.topic: conceptual
ms.date: 04/30/2020
ms.author: banders
ms.openlocfilehash: 33a0a0a62814579dee10ae046338ff9f78d667cb
ms.sourcegitcommit: 1895459d1c8a592f03326fcb037007b86e2fd22f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82627074"
---
# <a name="how-reservation-discounts-apply-to-azure-synapse-analytics"></a>Anwendung von Reservierungsrabatten auf Azure Synapse Analytics

Nach dem Kauf reservierter Kapazität für Azure Synapse Analytics wird der Reservierungsrabatt automatisch auf die in der entsprechenden Region bereitgestellten Instanzen angewendet. Der Reservierungsrabatt gilt für die über die cDWU-Verbrauchseinheit von Azure Synapse Analytics ausgegebene Nutzung. Die Speicher- und Netzwerknutzung wird entsprechend der nutzungsbasierten Bezahlung abgerechnet.

## <a name="reservation-discount-application"></a>Anwendung des Reservierungsrabatts

Der Rabatt für die reservierte Azure Synapse Analytics-Kapazität wird auf ausgeführte Warehouses auf Stundenbasis angewendet. Wenn Sie in einer Stunde kein Warehouse bereitgestellt haben, verfällt die reservierte Kapazität für diese Stunde. Sie wird nicht übertragen.

Nach dem Kauf wird die erworbene Reservierung auf die durch ausgeführte Warehouses zu einem bestimmten Zeitpunkt ausgegebene Azure Synapse Analytics-Nutzung abgestimmt. Wenn Sie einige Warehouses beenden, werden Reservierungsrabatte automatisch auf andere entsprechende Warehouses angewandt.

Für Warehouses, die eine volle Stunde nicht ausgeführt werden, wird die Reservierung automatisch auf andere entsprechende Instanzen in dieser Stunde angewandt.

## <a name="discount-examples"></a>Beispiele für die Anwendung des Rabatts

Die folgenden Beispiele zeigen, wie der Rabatt für die reservierte Azure Synapse Analytics-Kapazität abhängig von den jeweiligen Bereitstellungen angewendet wird.

- **Beispiel 1:** Sie erwerben als reservierte Kapazität 5 Einheiten mit jeweils 100 cDWU. Sie führen eine Azure Synapse Analytics-Instanz vom Typ „DW1500c“ eine Stunde lang aus. In diesem Fall wird die Nutzung für 15 Einheiten mit 100-cDWU-Nutzung ausgegeben. Der Reservierungsrabatt gilt für die 5 Einheiten, die Sie verwendet haben. Die restlichen 10 Einheiten mit 100-cDWU-Nutzung, die Sie verwendet haben, werden zu Preisen der nutzungsbasierten Bezahlung abgerechnet. Anders ausgedrückt: Eine partielle Abdeckung ist für mehrere Reservierungen möglich.

- **Beispiel 2:** Sie erwerben als reservierte Kapazität 5 Einheiten mit jeweils 100 cDWU. Sie führen zwei Azure Synapse Analytics-Instanzen vom Typ „DW100c“ eine Stunde lang aus. In diesem Fall werden zwei Nutzungsereignisse für 1 Einheit mit 100-cDWU-Nutzung ausgegeben. Der Rabatt der reservierten Kapazität wird auf beide Nutzungsereignisse angewandt. Die verbleibenden 3 Einheiten der reservierten Kapazität mit jeweils 100 cDWU verfallen und werden nicht auf die zukünftige Verwendung übertragen. Anders ausgedrückt: Eine einzelne Reservierung kann mehreren Azure Synapse Analytics-Instanzen zugeordnet werden.

- **Beispiel 3:** Sie erwerben für die reservierte Kapazität 1 Einheit mit 100 cDWU. Sie führen zwei Azure Synapse Analytics-Instanzen vom Typ „DW100c“ aus. Jede Instanz wird jeweils 30 Minuten ausgeführt. In diesem Fall wird der Rabatt der reservierten Kapazität auf beide Nutzungsereignisse angewandt. Keine Nutzung wird zu Preisen der nutzungsbasierten Bezahlung abgerechnet.

## <a name="need-help-contact-us"></a>Sie brauchen Hilfe? Kontakt

- Wenn Sie weitere Fragen haben oder Hilfe benötigen, [erstellen Sie eine Supportanfrage](https://go.microsoft.com/fwlink/?linkid=2083458).

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zu Azure-Reservierungen finden Sie in den folgenden Artikeln:

- [Was sind Azure-Reservierungen?](save-compute-costs-reservations.md)
- [Anzeigen von Reservierungstransaktionen](view-reservations.md)
- [Abrufen von Reservierungstransaktionen und Nutzung über die API](reservation-apis.md)
- [Verwalten von Reservierungen](manage-reserved-vm-instance.md)
