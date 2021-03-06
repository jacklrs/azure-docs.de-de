---
title: 'Häufig gestellte Fragen zu Azure Security Center: Fragen zu vorhandenen Log Analytics-Agents'
description: Diese häufig gestellte Fragen beantworten Fragen von Kunden, die den Log Analytics-Agent bereits verwenden und Azure Security Center in Erwägung ziehen, ein Produkt, das Sie beim Verhindern und Erkennen von sowie Reagieren auf Bedrohungen unterstützt.
services: security-center
documentationcenter: na
author: memildin
manager: rkarlin
ms.assetid: be2ab6d5-72a8-411f-878e-98dac21bc5cb
ms.service: security-center
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/25/2020
ms.author: memildin
ms.openlocfilehash: 2fe306cf7d17f0789c5e134c3fcad3f8f07a0b80
ms.sourcegitcommit: 50ef5c2798da04cf746181fbfa3253fca366feaa
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/30/2020
ms.locfileid: "82612825"
---
# <a name="faq-for-customers-already-using-azure-monitor-logs"></a>Häufig gestellte Fragen von Kunden, die bereits Azure Monitor-Protokolle verwenden<a name="existingloganalyticscust"></a>

## <a name="does-security-center-override-any-existing-connections-between-vms-and-workspaces"></a>Überschreibt Security Center bereits vorhandene Verbindungen zwischen virtuellen Computern und Arbeitsbereichen?

Wenn der Log Analytics-Agent bereits als Azure-Erweiterung auf einem virtuellen Computer installiert ist, wird die vorhandene Arbeitsbereichverbindung nicht überschrieben. Stattdessen verwendet Security Center den vorhandenen Arbeitsbereich. Der virtuelle Computer wird geschützt, vorausgesetzt, dass die Lösung „Security“ oder „SecurityCenterFree“ in dem Arbeitsbereich installiert ist, an den er berichtet. 

Eine Security Center-Lösung wird in dem Arbeitsbereich installiert, der im Datensammlungsbildschirm ausgewählt ist, falls noch keine vorhanden ist, und die Lösung wird nur auf die relevanten virtuellen Computer angewendet. Wenn Sie eine Lösung hinzufügen, wird sie automatisch standardmäßig für alle mit Ihrem Log Analytics-Arbeitsbereich verbundenen Windows- und Linux-Agents bereitgestellt. Mit der [Zielgruppenadressierung für Lösungen](../operations-management-suite/operations-management-suite-solution-targeting.md) können Sie einen Geltungsbereich auf Ihre Lösungen anwenden.

> [!TIP]
> Wenn der Log Analytics-Agent direkt auf der VM (also nicht als Azure-Erweiterung) installiert ist, wird der Log Analytics-Agent nicht installiert, und die Sicherheitsüberwachung ist eingeschränkt.

## <a name="does-security-center-install-solutions-on-my-existing-log-analytics-workspaces-what-are-the-billing-implications"></a>Installiert das Security Center Lösungen in meinen vorhandenen Log Analytics-Arbeitsbereichen? Was bedeutet das für die Abrechnung?
Wenn Security Center erkennt, dass ein virtueller Computer bereits mit einem Arbeitsbereich verbunden ist, den Sie erstellt haben, aktiviert Security Center Lösungen in diesem Arbeitsbereich gemäß Ihres Tarifs. Da die Lösungen mittels [Zielgruppenadressierung für Lösungen](../operations-management-suite/operations-management-suite-solution-targeting.md) nur auf die relevanten virtuellen Azure-Computer angewendet werden, bleibt die Abrechnung unverändert.

- **Free-Tarif:** Security Center installiert die Lösung „SecurityCenterFree“ im Arbeitsbereich. Für den Free-Tarif entstehen keine Kosten.
- **Standard-Tarif**: Security Center installiert die Lösung „Security“ im Arbeitsbereich.

   ![Lösungen im Standardarbeitsbereich](./media/security-center-platform-migration-faq/solutions.png)

## <a name="i-already-have-workspaces-in-my-environment-can-i-use-them-to-collect-security-data"></a>In meiner Umgebung sind bereits Arbeitsbereiche vorhanden. Kann ich diese zum Sammeln von Sicherheitsdaten verwenden?
Wenn der Log Analytics-Agent bereits als Azure-Erweiterung auf einem virtuellen Computer installiert ist, verwendet Security Center den vorhandenen verbundenen Arbeitsbereich. Eine Security Center-Lösung wird im Arbeitsbereich installiert, falls noch keine vorhanden ist, und die Lösung wird mittels [Zielgruppenadressierung für Lösungen](../operations-management-suite/operations-management-suite-solution-targeting.md) nur auf die relevanten virtuellen Computer angewendet.

Wenn Security Center den Log Analytics-Agent auf virtuellen Computern installiert, werden dabei die von Security Center erstellten Standardarbeitsbereiche verwendet, wenn Security Center auf keinen vorhandenen Arbeitsbereich verwiesen wird.

## <a name="i-already-have-security-solution-on-my-workspaces-what-are-the-billing-implications"></a>Die Lösung „Security“ ist bereits in meinen Arbeitsbereichen enthalten. Was bedeutet das für die Abrechnung?
Die Lösung „Sicherheit und Überwachung“ wird verwendet, um Funktionen der Security Center-Standardebene für Azure-VMs zu aktivieren. Wenn die Lösung „Sicherheit und Überwachung“ bereits in einem Arbeitsbereich installiert ist, verwendet Security Center die vorhandene Lösung. Die Abrechnung wird dadurch nicht beeinflusst.
