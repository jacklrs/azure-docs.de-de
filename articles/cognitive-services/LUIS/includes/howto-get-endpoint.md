---
title: include file
description: include file
services: cognitive-services
author: diberry
manager: nitinme
ms.custom: seodec18
ms.service: cognitive-services
ms.date: 05/06/2020
ms.subservice: language-understanding
ms.topic: include
ms.author: diberry
ms.openlocfilehash: 01d102de24185eba789e041d8534d6fdce8c260b
ms.sourcegitcommit: 46f8457ccb224eb000799ec81ed5b3ea93a6f06f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/28/2020
ms.locfileid: "87375809"
---
Kopieren Sie im Abschnitt **Verwalten** (Menü rechts oben) auf der Seite **Azure-Ressourcen** (linkes Menü) die URL der **Beispielabfrage**, und fügen Sie sie in einen neuen Browsertab ein.

Die Endpunkt-URL sieht wie folgt aus (mit Ihrer eigene App-ID und Ihrem eigenen Endpunktschlüssel anstelle von „APP-ID“ und „KEY-ID“):

```console
https://YOUR-CUSTOM-SUBDOMAIN.api.cognitive.microsoft.com/luis/prediction/v3.0/apps/APP-ID/slots/production/predict?subscription-key=KEY-ID&verbose=true&show-all-intents=true&log=true&query=YOUR_QUERY_HERE
```