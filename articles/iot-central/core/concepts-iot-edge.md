---
title: Azure IoT Edge und Azure IoT Central | Microsoft-Dokumentation
description: Hier erfahren Sie, wie Sie Azure IoT Edge mit einer IoT Central-Anwendung verwenden.
author: dominicbetts
ms.author: dobett
ms.date: 12/12/2019
ms.topic: conceptual
ms.service: iot-central
services: iot-central
ms.openlocfilehash: f8660cb18f5e7ac5f3695eb15475570b107bf25c
ms.sourcegitcommit: 46f8457ccb224eb000799ec81ed5b3ea93a6f06f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/28/2020
ms.locfileid: "87337074"
---
# <a name="connect-azure-iot-edge-devices-to-an-azure-iot-central-application"></a>Verbinden eines Azure IoT Edge-Geräts mit einer Azure IoT Central-Anwendung

*Dieser Artikel gilt für Lösungs- und Geräteentwickler.*

IoT Edge besteht aus drei Komponenten:

* **IoT Edge-Module** sind Container, die Azure-Dienste, Partnerdienste oder Ihren Code ausführen. Module werden auf IoT Edge-Geräten bereitgestellt und lokal auf diesen Geräten ausgeführt.
* Die **IoT Edge-Runtime** wird auf jedem IoT Edge-Gerät ausgeführt und dient zum Verwalten der Module, die auf einem Gerät jeweils bereitgestellt wurden.
* Mit einer **cloudbasierten Schnittstelle** können Sie für IoT Edge-Geräte die Remoteüberwachung und -verwaltung durchführen. IoT Central bildet die Cloudschnittstelle.

Ein **Azure IoT Edge**-Gerät kann ein Gatewaygerät mit nachgeschalteten Geräten sein, die eine Verbindung mit dem IoT Edge-Gerät herstellen. In diesem Artikel werden weitere Informationen zu den Verbindungsmustern von nachgeschalteten Geräten angegeben.

Mit **Gerätevorlagen** werden die Funktionen Ihrer Geräte und IoT Edge-Module definiert. Zu den Funktionen zählen die vom Modul gesendeten Telemetriedaten, die Moduleigenschaften und die Befehle, auf die ein Modul reagiert.

## <a name="downstream-device-relationships-with-a-gateway-and-modules"></a>Beziehungen nachgeschalteter Geräte mit einem Gateway und Modulen

Nachgeschaltete Geräte können über das Modul `$edgeHub` eine Verbindung mit einem IoT Edge-Gatewaygerät herstellen. In diesem Szenario wird das IoT Edge-Gerät zu einem transparenten Gateway.

![Diagramm des transparenten Gateways](./media/concepts-iot-edge/gateway-transparent.png)

Nachgeschaltete Geräte können auch über ein benutzerdefiniertes Modul eine Verbindung mit einem IoT Edge-Gatewaygerät herstellen. Im folgenden Szenario stellen nachgeschaltete Geräte eine Verbindung über ein benutzerdefiniertes ModBus-Modul her.

![Diagramm der Verbindung über das benutzerdefinierte Modul](./media/concepts-iot-edge/gateway-module.png)

Das folgende Diagramm zeigt die Verbindung mit einem IoT Edge-Gatewaygerät über beide Modultypen (benutzerdefiniert und `$edgeHub`).  

![Diagramm der Verbindung über beide Verbindungsmodule](./media/concepts-iot-edge/gateway-module-transparent.png)

Schließlich können nachgeschaltete Geräte über mehrere benutzerdefinierte Module eine Verbindung mit einem IoT Edge-Gatewaygerät herstellen. Das folgende Diagramm zeigt nachgeschaltete Geräte, die über ein benutzerdefiniertes ModBus-Modul, ein benutzerdefiniertes BLE-Modul und das `$edgeHub`-Modul verbunden sind. 

![Diagramm der Verbindung über mehrere benutzerdefinierte Module](./media/concepts-iot-edge/gateway-module2-transparent.png)

## <a name="deployment-manifests-and-device-templates"></a>Bereitstellungsmanifeste und Gerätevorlagen

In IoT Edge können Sie Geschäftslogik in Form von Modulen bereitstellen und verwalten. IoT Edge-Module sind die kleinste der von IoT Edge verwalteten Recheneinheiten und können Azure-Dienste (z. B. Azure Stream Analytics) oder Ihren eigenen lösungsspezifischen Code enthalten. Informationen zum Entwickeln, Bereitstellen und Verwalten von Modulen finden Sie unter [IoT Edge-Module](../../iot-edge/iot-edge-modules.md).

Im Grunde ist ein Bereitstellungsmanifest eine Liste von Modulzwillingen, die mit den gewünschten Eigenschaften konfiguriert sind. Ein Bereitstellungsmanifest teilt einem IoT Edge-Gerät (oder einer Gruppe von Geräten) mit, welche Module installiert und wie diese konfiguriert werden müssen. Bereitstellungsmanifeste enthalten die gewünschten Eigenschaften für jeden Modulzwilling. IoT Edge-Geräte geben die gemeldeten Eigenschaften für jedes Modul zurück.

Verwenden Sie Visual Studio Code, um ein Bereitstellungsmanifest zu erstellen. Weitere Informationen finden Sie unter [Azure IoT Edge für Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-edge).

In Azure IoT Central können Sie ein Bereitstellungsmanifest importieren, um eine Gerätevorlage zu erstellen. Das folgende Flussdiagramm zeigt den Lebenszyklus eines Bereitstellungsmanifests in IoT Central.

![Flussdiagramm des Lebenszyklus eines Bereitstellungsmanifests](./media/concepts-iot-edge/dmflow.png)

IoT Central modelliert ein IoT Edge-Gerät wie folgt:

* Jede IoT Edge-Gerätevorlage verfügt über ein Gerätefunktionsmodell.
* Für jedes benutzerdefinierte Modul im Bereitstellungsmanifest wird ein Modulfunktionsmodell generiert.
* Zwischen den einzelnen Modulfunktionsmodellen und einem Gerätefunktionsmodell wird eine Beziehung eingerichtet.
* Im Modulfunktionsmodell werden Modulschnittstellen implementiert.
* Jede Modulschnittstelle enthält Telemetrie, Eigenschaften und Befehle.

![Diagramm der IoT Edge-Modellierung](./media/concepts-iot-edge/edgemodelling.png)

## <a name="iot-edge-gateway-devices"></a>IoT Edge-Gatewaygeräte

Wenn Sie angegeben haben, dass es sich bei dem IoT Edge-Gerät um ein Gatewaygerät handelt, können Sie für Geräte, die eine Verbindung mit dem Gatewaygerät herstellen sollen, Downstreambeziehungen mit Gerätefunktionsmodellen hinzufügen.

## <a name="next-steps"></a>Nächste Schritte

Wenn Sie ein Geräteentwickler sind, sollten Sie sich als Nächstes über [Gatewaygerätetypen in IoT Central](./tutorial-define-gateway-device-type.md) informieren.
