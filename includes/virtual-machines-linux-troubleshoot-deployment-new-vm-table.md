---
author: cynthn
ms.service: virtual-machines-linux
ms.topic: include
ms.date: 10/26/2018
ms.author: cynthn
ms.openlocfilehash: d93de4ed758afb5e951bb5e19f4f7adb290e461c
ms.sourcegitcommit: 2ec4b3d0bad7dc0071400c2a2264399e4fe34897
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/27/2020
ms.locfileid: "67178094"
---
In der folgenden Tabelle sind die möglichen Upload- und Erfassungskombinationen von generalisierten und spezialisierten Linux-Betriebssystem-Images aufgeführt. Die Kombinationen, die ohne Fehler verarbeitet werden, sind durch ein „J“ gekennzeichnet, und die Kombinationen, bei denen Fehler ausgelöst werden, durch ein „N“. Die Ursachen und Lösungen für die verschiedenen auftretenden Fehler werden unterhalb der Tabelle beschrieben.

| OS | Upload (spez.) | Upload (gen.) | Erfassung (spez.) | Erfassung (gen.) |
| --- | --- | --- | --- | --- |
| Linux (gen.) |N<sup>1</sup> |J |N<sup>3</sup> |J |
| Linux (spez.) |J |N<sup>2</sup> |J |N<sup>4</sup> |

