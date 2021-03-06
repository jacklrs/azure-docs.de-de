---
title: 'Azure-Portal: Dynamische Datenmaskierung'
description: Einstieg in die dynamische Datenmaskierung für Azure SQL-Datenbank im Azure-Portal
services: sql-database
ms.service: sql-database
ms.subservice: security
ms.custom: sqldbrb=1
ms.devlang: ''
ms.topic: conceptual
author: DavidTrigano
ms.author: datrigan
ms.reviewer: vanto
ms.date: 04/28/2020
ms.openlocfilehash: 12a187b29737ba9388d9b33ac8bcfedf1339c059
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85253782"
---
# <a name="get-started-with-sql-database-dynamic-data-masking-with-the-azure-portal"></a>Erste Schritte mit der dynamischen Datenmaskierung für SQL-Datenbank im Azure-Portal
[!INCLUDE[appliesto-sqldb](../includes/appliesto-sqldb.md)]

In diesem Artikel wird erläutert, wie die [dynamische Datenmaskierung](dynamic-data-masking-overview.md) im Azure-Portal implementiert wird. Die dynamische Datenmaskierung können Sie auch mithilfe von [Azure SQL-Datenbank-Cmdlets](https://docs.microsoft.com/powershell/module/az.sql/) oder der [REST-API](https://docs.microsoft.com/rest/api/sql/) implementieren.

> [!NOTE]
> Dieses Feature kann nicht über das Portal für Azure Synapse oder SQL Managed Instance festgelegt werden (verwenden Sie stattdessen PowerShell oder die REST-API). Weitere Informationen finden Sie unter [Dynamic Data Masking](/sql/relational-databases/security/dynamic-data-masking).

## <a name="set-up-dynamic-data-masking-for-your-database-using-the-azure-portal"></a>Einrichten der dynamischen Datenmaskierung für Ihre Datenbank im Azure-Portal

1. Starten Sie das Azure-Portal unter [https://portal.azure.com](https://portal.azure.com).
2. Navigieren Sie zur Seite mit den Einstellungen der Datenbank mit den sensiblen Daten, die Sie maskieren möchten.
3. Klicken Sie im Abschnitt **Sicherheit** Ihrer Datenbank auf das Blatt **Dynamische Datenmaskierung**.

   ![Navigationsbereich](./media/dynamic-data-masking-configure-portal/4_ddm_settings_tile.png)

4. Auf der Konfigurationsseite **Dynamische Datenmaskierung** werden ggf. einige Datenbankspalten angezeigt, die von der Empfehlungs-Engine für die Maskierung gekennzeichnet wurden. Klicken Sie zum Akzeptieren der Empfehlungen einfach für eine oder mehrere Spalten auf **Maske hinzufügen**. Basierend auf dem Standardtyp der jeweiligen Spalte wird eine Maskierung erstellt. Sie können die Maskierungsfunktion ändern, indem Sie auf die Maskierungsregel klicken und das Maskierungsfeldformat in ein anderes Format Ihrer Wahl ändern. Klicken Sie auf **Speichern**, um Ihre Einstellungen zu speichern.

    ![Navigationsbereich](./media/dynamic-data-masking-configure-portal/5_ddm_recommendations.png)

5. Klicken Sie zum Hinzufügen einer Maskierung für eine beliebige Spalte der Datenbank oben auf der Konfigurationsseite **Dynamische Datenmaskierung** auf **Maske hinzufügen**, um die Konfigurationsseite **Maskierungsregel hinzufügen** zu öffnen.

    ![Navigationsbereich](./media/dynamic-data-masking-configure-portal/6_ddm_add_mask.png)

6. Wählen Sie **Schema**, **Tabelle** und **Spalte** aus, um das Feld für die Maskierung zu bestimmen.
7. Wählen Sie in der Liste der Kategorien für das Maskieren vertraulicher Daten eine **Maskierungsvariante** aus.

    ![Navigationsbereich](./media/dynamic-data-masking-configure-portal/7_ddm_mask_field_format.png)

8. Klicken Sie auf der Seite für Datenmaskierungsregeln auf **Hinzufügen**, um die Maskierungsregeln in der Richtlinie für die dynamische Datenmaskierung zu aktualisieren.
9. Geben Sie die SQL-Benutzer oder AAD-Identitäten (Azure AD) ein, die von der Maskierung ausgeschlossen werden sollen und Zugriff auf die unmaskierten vertraulichen Daten haben. Hierbei sollte es sich um eine durch Semikolons getrennte Liste mit Benutzern handeln. Benutzer mit Administratorrechten haben immer Zugriff auf die Originaldaten ohne Maskierung.

    ![Navigationsbereich](./media/dynamic-data-masking-configure-portal/8_ddm_excluded_users.png)

    > [!TIP]
    > Damit die Anwendungsschicht vertrauliche Daten für die privilegierten Anwendungsbenutzer anzeigen kann, fügen Sie den SQL-Benutzer oder die Azure AD-Identität hinzu, die von der Anwendung zum Abfragen der Datenbank verwendet wird. Es wird ausdrücklich empfohlen, dass diese Liste nur eine minimale Anzahl von privilegierten Benutzern enthält, um die Anzeige sensibler Daten zu minimieren.

10. Klicken Sie auf der Konfigurationsseite für die Datenmaskierung auf **Speichern**, um die neue oder aktualisierte Maskierungsrichtlinie zu speichern.

## <a name="next-steps"></a>Nächste Schritte

- Eine Übersicht über die dynamische Datenmaskierung finden Sie unter [Dynamische Datenmaskierung](dynamic-data-masking-overview.md).
- Die dynamische Datenmaskierung können Sie auch mithilfe von [Azure SQL-Datenbank-Cmdlets](https://docs.microsoft.com/powershell/module/az.sql/) oder der [REST-API](https://docs.microsoft.com/rest/api/sql/) implementieren.
