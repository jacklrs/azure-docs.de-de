---
title: 'Zuordnungsdatenfluss: Entpivotierungstransformation'
description: 'Azure Data Factory-Mappingdatenfluss: Entpivotierungstransformation'
author: kromerm
ms.author: makromer
ms.service: data-factory
ms.topic: conceptual
ms.custom: seo-lt-2019
ms.date: 07/14/2020
ms.openlocfilehash: e7c0a4cd6e44994c4b002fcc2e5fde441cf22283
ms.sourcegitcommit: 8def3249f2c216d7b9d96b154eb096640221b6b9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/03/2020
ms.locfileid: "87541650"
---
# <a name="azure-data-factory-unpivot-transformation"></a>Azure Data Factory: Entpivotierungstransformation

[!INCLUDE[appliesto-adf-asa-md](includes/appliesto-adf-asa-md.md)]

Verwenden Sie das Entpivotieren in einem ADF-Mappingdatenfluss, um ein nicht normalisiertes Dataset in eine stärker normalisierte Version zu ändern, indem Werte aus mehreren Spalten eines einzelnen Datensatzes in mehrere Datensätze mit den gleichen Werten in einer einzelnen Spalte erweitert werden.

![Entpivotierungstransformation](media/data-flow/unpivot1.png "Entpivotierungsoptionen 1")

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE4B1RR]

## <a name="ungroup-by"></a>Gruppierung aufheben nach

![Entpivotierungstransformation](media/data-flow/unpivot5.png "Entpivotierungsoptionen 2")

Legen Sie zuerst die Spalten fest, nach denen Sie für Ihre Pivotaggregation gruppieren möchten. Legen Sie eine oder mehrere Spalten für das Aufheben der Gruppierung mit dem Pluszeichen (+) neben der Spaltenliste fest.

## <a name="unpivot-key"></a>Entpivotierungsschlüssel

![Entpivotierungstransformation](media/data-flow/unpivot6.png "Entpivotierungsoptionen 3")

Der Pivotschlüssel ist die Spalte, die ADF von Zeile in Spalte pivotiert. Standardmäßig wird jeder eindeutige Wert im Dataset für dieses Feld in eine Spalte pivotiert. Sie können jedoch die Werte aus dem Dataset optional eingeben, die in Spaltenwerte pivotiert werden sollen.

## <a name="unpivoted-columns"></a>Entpivotierte Spalten

![Entpivotierungstransformation](media/data-flow//unpivot7.png "Entpivotierungsoptionen 4")

Wählen Sie abschließend die für die pivotierten Werte zu verwendende Aggregation aus, und wählen Sie aus, wie die Spalten in der neuen Ausgabeprojektion der Transformation angezeigt werden sollen.

(Optional) Sie können ein Benennungsmuster mit einem Präfix, einem Mittelteil und einem Suffix festlegen, das/der jedem neuen Spaltennamen aus den Zeilenwerten hinzugefügt wird.

Wenn Sie beispielsweise „Umsatz“ nach „Region“ pivotieren, erhalten Sie einfach neue Spaltenwerte aus den einzelnen Umsatzzahlen. Beispiel: „25“, „50“, „1000“, ... Wenn Sie jedoch den Präfixwert „Umsatz“ festlegen, wird „Umsatz“ den Werten vorangestellt.

![Bild der Spalten „PO“ (Bestellung), „Vendor“ (Lieferant) und „Fruit“ (Obst) vor und nach einer Entpivotierungstransformation, bei der die Spalte „Fruit“ als Entpivotierungsschlüssel verwendet wird.](media/data-flow/unpivot3.png)

Wenn Sie die Spaltenanordnung auf „Normal“ festlegen, werden alle pivotierten Spalten zusammen mit ihren aggregierten Werten gruppiert. Wenn Sie die Spaltenanordnung auf „Lateral“ festlegen, wird zwischen Spalte und Wert gewechselt.

![Entpivotierungstransformation](media/data-flow//unpivot7.png "Entpivotierungsoptionen 5")

Im letzten Resultset der entpivotierten Daten werden die Spaltensummen angezeigt, die jetzt in separaten Zeilenwerten entpivotiert sind.

## <a name="next-steps"></a>Nächste Schritte

Verwenden der [Pivotierungstransformation](data-flow-pivot.md) zum Pivotieren von Zeilen zu Spalten
