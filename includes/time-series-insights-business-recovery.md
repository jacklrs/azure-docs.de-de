---
ms.topic: include
ms.service: time-series-insights
author: deepakpalled
ms.author: dpalled
manager: diviso
ms.date: 07/09/2020
ms.openlocfilehash: de5d3f8f32e928c77ffd6028ec764793ab7229ac
ms.sourcegitcommit: 3543d3b4f6c6f496d22ea5f97d8cd2700ac9a481
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/20/2020
ms.locfileid: "86495335"
---
## <a name="business-disaster-recovery"></a>Business Disaster Recovery

Dieser Abschnitt beschreibt Features von Azure Time Series Insights, die den Betrieb von Apps und Diensten auch im Katastrophenfall sicherstellen (bekannt als *Business Disaster Recovery*).

### <a name="high-availability"></a>Hochverfügbarkeit

Als Azure-Dienst bietet Azure Time Series Insights bestimmte *Hochverfügbarkeitsfeatures*, indem Redundanzen auf Azure-Regionsebene verwendet werden. Beispielsweise unterstützt Azure dank des Features für die *regionsübergreifende Verfügbarkeit* von Azure Funktionen für die Notfallwiederherstellung.

Zu den zusätzlichen Hochverfügbarkeitsfeatures von Azure (auch für alle Azure Time Series Insights-Instanzen verfügbar) gehören:

- **Failover**: Azure bietet [Georeplikation und Lastenausgleich](https://docs.microsoft.com/azure/architecture/resiliency/recovery-loss-azure-region).
- **Daten-** und **Speicherwiederherstellung**: Azure bietet [mehrere Optionen zum Beibehalten und Wiederherstellen von Daten](https://docs.microsoft.com/azure/architecture/resiliency/recovery-data-corruption).
- **Azure Site Recovery**: Azure bietet Features für die Sitewiederherstellung über [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/).
- **Azure Backup**: [Azure Backup](https://docs.microsoft.com/azure/backup/backup-architecture) unterstützt sowohl lokale als auch cloudbasierte Sicherungen von Azure-VMs.

Stellen Sie sicher, dass Sie die relevanten Azure-Features aktivieren, um eine globale, regionsübergreifende Hochverfügbarkeit für Ihre Geräte und Benutzer zu gewährleisten.

> [!NOTE]
> Ist Azure für regionsübergreifende Verfügbarkeit konfiguriert, ist in Azure Time Series Insights keine zusätzliche Konfiguration der regionsübergreifenden Verfügbarkeit erforderlich.

### <a name="iot-and-event-hubs"></a>IoT und Event Hubs

Einige Azure IoT-Dienste enthalten auch integrierte Business Disaster Recovery-Features:

- [Hochverfügbarkeit und Notfallwiederherstellung von Azure IoT Hub](https://docs.microsoft.com/azure/iot-hub/iot-hub-ha-dr), einschließlich intraregionaler Redundanz
- [Azure Event Hubs-Richtlinien](https://docs.microsoft.com/azure/event-hubs/event-hubs-geo-dr)
- [Azure-Speicherredundanz](https://docs.microsoft.com/azure/storage/common/storage-redundancy)

Die Integration von Azure Time Series Insights in die anderen Dienste bietet zusätzliche Möglichkeiten für die Notfallwiederherstellung. Beispielsweise können an Ihren Event Hub gesendete Telemetriedaten in einer Sicherungsdatenbank von Azure Blob Storage gespeichert werden.

### <a name="azure-time-series-insights"></a>Azure Time Series Insights

Es gibt mehrere Möglichkeiten, den Betrieb Ihrer Daten, Apps und Dienste von Azure Time Series Insights aufrechtzuerhalten, auch wenn sie gestört sind. 

Möglicherweise ist auch eine vollständige Sicherungskopie Ihrer Azure Time Series-Umgebung für folgende Zwecke erforderlich:

- Als eine *Failoverinstanz* speziell für Azure Time Series Insights, zu der Daten und Datenverkehr umgeleitet werden
- Zum Bewahren von Daten und Überwachungsinformationen

Im Allgemeinen ist die beste Möglichkeit zum Duplizieren einer Azure Time Series Insights-Umgebung die Erstellung einer zweiten Azure Time Series Insights-Umgebung in einer Azure-Sicherungsregion. Ereignisse werden auch von Ihrer primären Ereignisquelle Ereignisse an diese sekundäre Umgebung gesendet. Stellen Sie sicher, dass Sie eine zweite dedizierte Consumergruppe verwenden. Folgen Sie den Business Disaster Recovery-Richtlinien dieser Quelle, wie es weiter oben beschrieben ist.

So erstellen Sie eine Duplikatumgebung:

1. Erstellen Sie eine Umgebung in einer zweiten Region. Weitere Informationen finden Sie unter [Erstellen einer neuen Azure Time Series Insights-Umgebung über das Azure-Portal](https://docs.microsoft.com/azure/time-series-insights/time-series-insights-get-started).
1. Erstellen Sie eine zweite dedizierte Consumergruppe für Ihre Ereignisquelle.
1. Verbinden Sie diese Ereignisquelle mit der neuen Umgebung. Stellen Sie sicher, dass Sie die zweite dedizierte Consumergruppe festlegen.
1. Machen Sie sich mit der [IoT Hub](https://docs.microsoft.com/azure/time-series-insights/time-series-insights-how-to-add-an-event-source-iothub)- und [Event Hubs](https://docs.microsoft.com/azure/time-series-insights/time-series-insights-data-access)-Dokumentation für Azure Time Series Insights vertraut.

Bei Auftreten eines Ereignisses:

1. Wenn Ihre primäre Region während eines Notfalls betroffen ist, leiten Sie den Betrieb in die Azure Time Series Insights-Sicherungsumgebung um.
1. Verwenden Sie Ihre zweite Region zum Sichern und Wiederherstellen aller Azure Time Series Insights-Telemetrie- und -Abfragedaten.

> [!IMPORTANT]
> Bei Auftreten eines Failovers:
> 
> * Es kann auch eine Verzögerung auftreten.
> * Es kann eine momentane Spitze bei der Nachrichtenverarbeitung auftreten, wenn der Betrieb und Vorgänge umgeleitet werden.
> 
> Weitere Informationen finden Sie unter [Minimieren von Latenzen in Azure Time Series Insights](https://docs.microsoft.com/azure/time-series-insights/time-series-insights-environment-mitigate-latency).

