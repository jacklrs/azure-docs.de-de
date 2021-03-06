---
title: Verwenden der Azure-Befehlszeilenschnittstelle zum Zuweisen einer RBAC-Rolle für den Datenzugriff
titleSuffix: Azure Storage
description: Erfahren Sie, wie Sie mit der Azure-Befehlszeilenschnittstelle Berechtigungen für einen Azure Active Directory-Sicherheitsprinzipal mit rollenbasierter Zugriffssteuerung (Role-Based Access Control, RBAC) zuweisen. Azure Storage unterstützt für die Authentifizierung über Azure AD integrierte und benutzerdefinierte Azure-Rollen.
services: storage
author: tamram
ms.service: storage
ms.topic: how-to
ms.date: 07/16/2020
ms.author: tamram
ms.reviewer: ozgun
ms.subservice: common
ms.openlocfilehash: afa48c07e628eaeb013c24fa38fcda1adea2555a
ms.sourcegitcommit: f353fe5acd9698aa31631f38dd32790d889b4dbb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/29/2020
ms.locfileid: "87368970"
---
# <a name="use-azure-cli-to-assign-an-rbac-role-for-access-to-blob-and-queue-data"></a>Verwenden der Azure-Befehlszeilenschnittstelle zum Zuweisen einer RBAC-Rolle für den Zugriff auf Blob- und Warteschlangendaten

Azure Active Directory (Azure AD) autorisiert Rechte für den Zugriff auf abgesicherte Ressourcen über die [rollenbasierte Zugriffssteuerung (RBAC)](../../role-based-access-control/overview.md). Azure Storage bietet eine Reihe in Azure integrierter Rollen mit allgemeinen Berechtigungssätzen für den Zugriff auf Blob- und Warteschlangendaten.

Wenn einem Azure AD-Sicherheitsprinzipal eine RBAC-Rolle zugewiesen wird, gewährt Azure diesem Sicherheitsprinzipal Zugriff auf diese Ressourcen. Der Zugriff kann auf die Ebene des Abonnements, der Ressourcengruppe, des Speicherkontos oder eines einzelnen Containers oder einer Warteschlange begrenzt werden. Eine Azure AD-Sicherheitsprinzipal kann ein Benutzer, eine Gruppe, ein Anwendungsdienstprinzipal oder eine [verwaltete Identität für Azure-Ressourcen](../../active-directory/managed-identities-azure-resources/overview.md) sein.

In diesem Artikel wird beschrieben, wie Sie mithilfe der Azure-Befehlszeilenschnittstelle integrierte Azure-Rollen auflisten und diese Benutzern zuweisen. Weitere Informationen zur Verwendung der Azure CLI finden Sie unter [Azure-Befehlszeilenschnittstelle (CLI)](/cli/azure).

## <a name="rbac-roles-for-blobs-and-queues"></a>RBAC-Rollen für Blobs und Warteschlangen

[!INCLUDE [storage-auth-rbac-roles-include](../../../includes/storage-auth-rbac-roles-include.md)]

## <a name="determine-resource-scope"></a>Bestimmen des Ressourcenumfangs

[!INCLUDE [storage-auth-resource-scope-include](../../../includes/storage-auth-resource-scope-include.md)]

## <a name="list-available-rbac-roles"></a>Auflisten verfügbarer RBAC-Rollen

Verwenden Sie zum Auflisten verfügbarer integrierter Azure-Rollen mit der Azure-Befehlszeilenschnittstelle den Befehl [az role definition list](/cli/azure/role/definition#az-role-definition-list):

```azurecli-interactive
az role definition list --out table
```

Die integrierten Azure Storage-Datenrollen werden zusammen mit anderen integrierten Rollen für Azure aufgelistet:

```Example
Storage Blob Data Contributor             Allows for read, write and delete access to Azure Storage blob containers and data
Storage Blob Data Owner                   Allows for full access to Azure Storage blob containers and data, including assigning POSIX access control.
Storage Blob Data Reader                  Allows for read access to Azure Storage blob containers and data
Storage Queue Data Contributor            Allows for read, write, and delete access to Azure Storage queues and queue messages
Storage Queue Data Message Processor      Allows for peek, receive, and delete access to Azure Storage queue messages
Storage Queue Data Message Sender         Allows for sending of Azure Storage queue messages
Storage Queue Data Reader                 Allows for read access to Azure Storage queues and queue messages
```

## <a name="assign-an-rbac-role-to-a-security-principal"></a>Zuweisen einer RBAC-Rolle zu einem Sicherheitsprinzipal

Verwenden Sie den Befehl [az role assignment create](/cli/azure/role/assignment#az-role-assignment-create), um einem Sicherheitsprinzipal eine RBAC-Rolle zuzuweisen. Das Format des Befehls kann je nach Bereich der Zuweisung unterschiedlich sein. Die folgenden Beispiele zeigen, wie Sie einem Benutzer eine Rolle in verschiedenen Bereichen zuweisen können. Sie können jedoch den gleichen Befehl verwenden, um eine Rolle einem beliebigen Sicherheitsprinzipal zuzuordnen.

### <a name="container-scope"></a>Containerbereich

Geben Sie zum Zuweisen einer auf einen Container begrenzten Rolle für den Parameter `--scope` eine Zeichenfolge an, die den Containerbereich enthält. Der Bereich für einen Container weist folgendes Format auf:

```
/subscriptions/<subscription>/resourceGroups/<resource-group>/providers/Microsoft.Storage/storageAccounts/<storage-account>/blobServices/default/containers/<container>
```

Im folgenden Beispiel wird die Rolle **Mitwirkender an Storage-Blobdaten** einem Benutzer zugewiesen und auf die Ebene eines Containers begrenzt. Ersetzen Sie die Beispielwerte und die Platzhalterwerte in Klammern durch Ihre eigenen Werte:

```azurecli-interactive
az role assignment create \
    --role "Storage Blob Data Contributor" \
    --assignee <email> \
    --scope "/subscriptions/<subscription>/resourceGroups/<resource-group>/providers/Microsoft.Storage/storageAccounts/<storage-account>/blobServices/default/containers/<container>"
```

### <a name="queue-scope"></a>Warteschlangenbereich

Geben Sie zum Zuweisen einer auf eine Warteschlange begrenzten Rolle für den Parameter `--scope` eine Zeichenfolge an, die den Warteschlangenbereich enthält. Der Bereich für eine Warteschlange weist folgendes Format auf:

```
/subscriptions/<subscription>/resourceGroups/<resource-group>/providers/Microsoft.Storage/storageAccounts/<storage-account>/queueServices/default/queues/<queue>
```

Im folgenden Beispiel wird die Rolle **Mitwirkender an Storage-Warteschlangendaten** einem Benutzer zugewiesen und auf die Ebene der Warteschlange begrenzt. Ersetzen Sie die Beispielwerte und die Platzhalterwerte in Klammern durch Ihre eigenen Werte:

```azurecli-interactive
az role assignment create \
    --role "Storage Queue Data Contributor" \
    --assignee <email> \
    --scope "/subscriptions/<subscription>/resourceGroups/<resource-group>/providers/Microsoft.Storage/storageAccounts/<storage-account>/queueServices/default/queues/<queue>"
```

### <a name="storage-account-scope"></a>Speicherkontobereich

Geben Sie zum Zuweisen einer auf eine Warteschlange begrenzten Rolle für den Parameter `--scope` den Bereich der Speicherkontoressource an. Der Bereich für ein Speicherkonto weist folgendes Format auf:

```
/subscriptions/<subscription>/resourceGroups/<resource-group>/providers/Microsoft.Storage/storageAccounts/<storage-account>
```

Im folgenden Beispiel wird veranschaulicht, wie die Rolle **Storage-Blobdatenleser** einem Benutzer auf Speicherkontoebene zugewiesen wird. Ersetzen Sie die Beispielwerte durch Ihre eigenen Werte: \

```azurecli-interactive
az role assignment create \
    --role "Storage Blob Data Reader" \
    --assignee <email> \
    --scope "/subscriptions/<subscription>/resourceGroups/<resource-group>/providers/Microsoft.Storage/storageAccounts/<storage-account>"
```

### <a name="resource-group-scope"></a>Ressourcengruppenbereich

Geben Sie zum Zuweisen einer auf eine Ressourcengruppe begrenzten Rolle für den Parameter `--resource-group` den Namen oder die ID der Ressourcengruppe an. Im folgenden Beispiel wird die Rolle **Storage-Warteschlangendatenleser** einem Benutzer auf Ressourcengruppenebene zugewiesen. Ersetzen Sie die Beispielwerte und Platzhalterwerte in Klammern durch Ihre eigenen Werte:

```azurecli-interactive
az role assignment create \
    --role "Storage Queue Data Reader" \
    --assignee <email> \
    --resource-group <resource-group>
```

### <a name="subscription-scope"></a>Abonnementbereich

Geben Sie zum Zuweisen einer auf das Abonnement begrenzten Rolle für den Parameter `--scope` den Bereich für das Abonnement an. Der Bereich für ein Abonnement weist folgendes Format auf:

```
/subscriptions/<subscription>
```

Im folgenden Beispiel wird veranschaulicht, wie die Rolle **Storage-Blobdatenleser** einem Benutzer auf Speicherkontoebene zugewiesen wird. Ersetzen Sie die Beispielwerte durch Ihre eigenen Werte: 

```azurecli-interactive
az role assignment create \
    --role "Storage Blob Data Reader" \
    --assignee <email> \
    --scope "/subscriptions/<subscription>"
```

## <a name="next-steps"></a>Nächste Schritte

- [Verwalten des Zugriffs auf Azure-Ressourcen mit RBAC und Azure PowerShell](../../role-based-access-control/role-assignments-powershell.md)
- [Grant access to Azure blob and queue data with RBAC using Azure PowerShell (Gewähren von Zugriff auf Azure-Blob- und -Warteschlangendaten mit RBAC über Azure PowerShell)](storage-auth-aad-rbac-powershell.md)
- [Gewähren von Zugriff auf Azure-Blob- und -Warteschlangendaten mit RBAC über das Azure-Portal](storage-auth-aad-rbac-portal.md)
