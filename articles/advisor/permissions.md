---
title: Berechtigungen in Azure Advisor
description: Advisor-Berechtigungen und wie sie Ihre Möglichkeit zum Konfigurieren von Abonnements oder zum Zurückstellen oder Verwerfen von Empfehlungen blockieren können.
ms.topic: article
ms.date: 04/03/2019
ms.openlocfilehash: 6b5dfdeb888b0577a40562536bd7a6dfc271cb19
ms.sourcegitcommit: 3d79f737ff34708b48dd2ae45100e2516af9ed78
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "87057583"
---
# <a name="permissions-in-azure-advisor"></a>Berechtigungen in Azure Advisor

Azure Advisor bietet Empfehlungen basierend auf der Nutzung und Konfiguration Ihrer Azure-Ressourcen und -Abonnements. Advisor verwendet die über die [rollenbasierte Zugriffssteuerung](../role-based-access-control/overview.md) (RBAC) bereitgestellten [integrierten Rollen](../role-based-access-control/built-in-roles.md), um Ihren Zugriff auf die Empfehlungen und Advisor-Funktionen zu verwalten. 

## <a name="roles-and-their-access"></a>Rollen und der zugehörige Zugriff

In der folgenden Tabelle sind die Rollen und der zugehörige Zugriff in Advisor definiert:

| **Rolle** | **Anzeigen von Empfehlungen** | **Bearbeiten von Regeln** | **Bearbeiten der Abonnementkonfiguration** | **Bearbeiten der Ressourcengruppenkonfiguration**| **Verwerfen oder Zurückstellen von Empfehlungen**|
|---|:---:|:---:|:---:|:---:|:---:|
|Besitzer des Abonnements|**X**|**X**|**X**|**X**|**X**|
|Mitwirkender des Abonnements|**X**|**X**|**X**|**X**|**X**|
|Abonnementleser|**X**|--|--|--|--|
|Ressourcengruppenbesitzer|**X**|--|--|**X**|**X**|
|Ressourcengruppenmitwirkender|**X**|--|--|**X**|**X**|
|Ressourcengruppenleser|**X**|--|--|--|--|
|Ressourcenbesitzer|**X**|--|--|--|**X**|
|Ressourcenmitwirkender|**X**|--|--|--|**X**|
|Ressourcenleser|**X**|--|--|--|--|

> [!NOTE]
> Der Zugriff zum Anzeigen von Empfehlungen hängt von Ihrem Zugriff auf die von den Empfehlungen betroffene Ressource ab.

## <a name="permissions-and-unavailable-actions"></a>Berechtigungen und nicht verfügbare Aktionen

Fehlende erforderliche Berechtigungen können dazu führen, dass Sie in Advisor keine Aktionen ausführen können. Im Folgenden sind einige häufiger auftretende Probleme aufgeführt.

### <a name="unable-to-configure-subscriptions-or-resource-groups"></a>Abonnements oder Ressourcengruppen können nicht konfiguriert werden

Wenn Sie versuchen, Abonnements oder Ressourcengruppen in Advisor zu konfigurieren, ist die Option zum Einschließen oder Ausschließen möglicherweise deaktiviert. Dieser Status gibt an, dass Sie über keine ausreichende Berechtigungsebene für die jeweilige Ressourcengruppe oder das betreffende Abonnement verfügen. Machen Sie sich damit vertraut, wie Sie [den Zugriff für einen Benutzer gewähren](../role-based-access-control/quickstart-assign-role-user-portal.md), um dieses Problem zu beheben.

### <a name="unable-to-postpone-or-dismiss-a-recommendation"></a>Eine Empfehlung kann nicht zurückgestellt oder verworfen werden

Wenn beim Zurückstellen oder Verwerfen einer Empfehlung eine Fehlermeldung angezeigt wird, verfügen Sie möglicherweise nicht über ausreichende Berechtigungen. Stellen Sie sicher, dass Sie zumindest über Zugriff als „Mitwirkender“ auf die Ressource haben, für die Sie die Empfehlung zurückstellen oder verwerfen möchten. Machen Sie sich damit vertraut, wie Sie [den Zugriff für einen Benutzer gewähren](../role-based-access-control/quickstart-assign-role-user-portal.md), um dieses Problem zu beheben.

## <a name="next-steps"></a>Nächste Schritte

In diesem Artikel haben Sie einen Überblick darüber erhalten, wie in Advisor mithilfe von RBAC Benutzerberechtigungen gesteuert und häufiger auftretende Probleme behoben werden. Weitere Informationen zum Advisor:

- [Was ist Azure Advisor?](./advisor-overview.md)
- [Erste Schritte mit Azure Advisor](./advisor-get-started.md)
