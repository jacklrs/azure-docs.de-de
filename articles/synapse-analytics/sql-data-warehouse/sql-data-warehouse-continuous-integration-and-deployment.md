---
title: Continuous Integration und Continuous Deployment
description: Professionelle DevOps-Datenbankumgebung für Data Warehousing mit integrierter Unterstützung für Continuous Integration und Continuous Deployment mithilfe von Azure Pipelines
services: synapse-analytics
author: kevinvngo
manager: craigg
ms.service: synapse-analytics
ms.topic: how-to
ms.subservice: sql-dw
ms.date: 02/04/2020
ms.author: kevin
ms.reviewer: igorstan
ms.custom: azure-synapse
ms.openlocfilehash: 725e8165f8a7bdb654f61d7257867a2d0bf17110
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85213566"
---
# <a name="continuous-integration-and-deployment-for-data-warehousing"></a>Continuous Integration und Continuous Deployment für Data Warehousing

In diesem einfachen Tutorial wird erläutert, wie Sie Ihr SSDT-Datenbankprojekt (SQL Server Data Tools) in Azure DevOps integrieren und Azure Pipelines zum Einrichten von Continuous Integration und Continuous Deployment nutzen. Dieses Tutorial ist der zweite Schritt beim Erstellen Ihrer Continuous Integration- und Continuous Deployment-Pipeline für Data Warehousing.

## <a name="before-you-begin"></a>Voraussetzungen

- Lesen Sie das Tutorial zur [Integration der Quellcodeverwaltung](sql-data-warehouse-source-control-integration.md).

- Einrichten von Azure DevOps und Herstellen einer Verbindung

## <a name="continuous-integration-with-visual-studio-build"></a>Continuous Integration mit Visual Studio Build

1. Navigieren Sie zu Azure Pipelines, und erstellen Sie eine neue Buildpipeline.

      ![Neue Pipeline](./media/sql-data-warehouse-continuous-integration-and-deployment/1-new-build-pipeline.png "Neue Pipeline")

2. Wählen Sie Ihr Quellcoderepository (Azure Repos Git) und anschließend die .NET-Desktop-App-Vorlage aus.

      ![Pipelinesetup](./media/sql-data-warehouse-continuous-integration-and-deployment/2-pipeline-setup.png "Pipelinesetup")

3. Bearbeiten Sie Ihre YAML-Datei, damit der richtige Pool Ihres Agents verwendet wird. Ihre YAML-Datei sollte in etwa wie folgt aussehen:

      ![YAML](./media/sql-data-warehouse-continuous-integration-and-deployment/3-yaml-file.png "YAML")

Nun verfügen Sie über eine einfache Umgebung, in der jeder Check-In bei Ihrem Quellcoderepository-Masterbranch automatisch einen erfolgreichen Visual Studio-Build Ihres Datenbankprojekts auslösen sollte. Überprüfen Sie, ob die Automatisierung insgesamt funktioniert, indem Sie eine Änderung an Ihrem lokalen Datenbankprojekt vornehmen und diese Änderung beim Masterbranch einchecken.

## <a name="continuous-deployment-with-the-azure-sql-data-warehouse-or-database-deployment-task"></a>Continuous Deployment mit der Bereitstellungsaufgabe für Azure SQL Data Warehouse (oder SQL-Datenbank)

1. Fügen Sie mithilfe der [Azure SQL-Datenbank-Bereitstellungsaufgabe](/azure/devops/pipelines/targets/azure-sqldb) eine neue Aufgabe hinzu, und füllen Sie die erforderlichen Felder aus, um eine Verbindung mit dem Ziel-Data Warehouse herzustellen. Wenn diese Aufgabe ausgeführt wird, wird die DACPAC-Datei, die vom vorherigen Buildprozess generiert wurde, auf dem Ziel-Data Warehouse bereitgestellt. Sie können auch die [Azure SQL Data Warehouse-Bereitstellungsaufgabe](https://marketplace.visualstudio.com/items?itemName=ms-sql-dw.SQLDWDeployment) verwenden.

      ![Bereitstellungsaufgabe](./media/sql-data-warehouse-continuous-integration-and-deployment/4-deployment-task.png "Bereitstellungsaufgabe")

2. Stellen Sie bei Verwendung eines selbstgehosteten Agents sicher, dass Sie die Umgebungsvariable so festlegen, dass sie die richtige Version von „SqlPackage.exe“ für SQL Data Warehouse verwendet. Der Pfad sollte in etwa wie folgt aussehen:

      ![Umgebungsvariable](./media/sql-data-warehouse-continuous-integration-and-deployment/5-environment-variable-preview.png "Umgebungsvariable")

   C:\Programme (x86)\Microsoft Visual Studio\2019\Preview\Common7\IDE\Extensions\Microsoft\SQLDB\DAC\150  

   Führen Sie Ihre Pipeline aus, und überprüfen Sie sie. Sie können Änderungen lokal vornehmen und Änderungen an der Quellcodeverwaltung einchecken, die eine automatische Erstellung und Bereitstellung generiert.

## <a name="next-steps"></a>Nächste Schritte

- Kennenlernen der [MPP-Architektur des Synapse SQL-Pools](massively-parallel-processing-mpp-architecture.md)
- Führen Sie eine schnelle [Erstellung eines SQL-Pools](create-data-warehouse-portal.md) durch.
- [Laden von Stichprobendaten](load-data-from-azure-blob-storage-using-polybase.md)
- Ansehen von [Videos](sql-data-warehouse-videos.md)
