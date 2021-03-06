---
title: Integrieren von Key Vault in die DigiCert-Zertifizierungsstelle
description: Informationen, wie Sie Key Vault in die DigiCert-Zertifizierungsstelle integrieren.
services: key-vault
author: msmbaldwin
manager: rkarlin
tags: azure-resource-manager
ms.service: key-vault
ms.subservice: certificates
ms.topic: tutorial
ms.date: 06/02/2020
ms.author: sebansal
ms.openlocfilehash: 7627625a917a8f652da62d4197368f023ad8c110
ms.sourcegitcommit: 845a55e6c391c79d2c1585ac1625ea7dc953ea89
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/05/2020
ms.locfileid: "85964497"
---
# <a name="integrating-key-vault-with-digicert-certificate-authority"></a>Integrieren von Key Vault in die DigiCert-Zertifizierungsstelle

Azure Key Vault ermöglicht das einfache Bereitstellen und Verwalten von digitalen Zertifikaten für Ihr Netzwerk und das Aktivieren der sicheren Kommunikation für Anwendungen. Ein digitales Zertifikat ist eine elektronische Anmeldeinformation, um einen Identitätsnachweis in einer elektronischen Transaktion zu erbringen. 

Azure Key Vault-Benutzer können DigiCert-Zertifikate direkt aus ihrem Key Vault generieren. Key Vault würde die Verwaltung des End-to-End-Zertifikatlebenszyklus für solche Zertifikate sicherstellen, die von DigiCert über die vertrauenswürdige Partnerschaft von Key Vault mit der DigiCert-Zertifizierungsstelle ausgestellt wurden.

Weitere allgemeine Informationen zu Zertifikaten finden Sie unter [Azure Key Vault-Zertifikate](/azure/key-vault/certificates/about-certificates).

Wenn Sie kein Azure-Abonnement besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) erstellen, bevor Sie beginnen.

## <a name="prerequisites"></a>Voraussetzungen

Für diesen Leitfaden benötigen Sie die folgenden Ressourcen.
* Einen Schlüsseltresor. Sie können einen vorhandenen Schlüsseltresor verwenden oder einen neuen Schlüsseltresor erstellen, indem Sie die Schritte in einem der folgenden Schnellstarts ausführen:
   - [Erstellen eines Schlüsseltresors mit der Azure CLI](../secrets/quick-create-cli.md)
   - [Erstellen eines Schlüsseltresors mit Azure PowerShell](../secrets/quick-create-powershell.md)
   - [Erstellen eines Schlüsseltresors im Azure-Portal](../secrets/quick-create-portal.md)
*   Sie müssen das DigiCert CertCentral-Konto aktivieren. [Registrieren Sie sich](https://www.digicert.com/account/signup/) für Ihr CertCentral-Konto.
*   Berechtigungen auf Administratorebene in Ihren Konten.


### <a name="before-you-begin"></a>Voraussetzungen

Stellen Sie sicher, dass Sie die folgenden Informationen aus Ihrem DigiCert CertCentral-Konto zur Hand haben:
-   CertCentral-Konto-ID
-   Organisations-ID
-   API-Schlüssel

## <a name="adding-certificate-authority-in-key-vault"></a>Hinzufügen einer Zertifizierungsstelle in Key Vault 
Nachdem Sie die Informationen aus dem DigiCert CertCentral-Konto gesammelt haben, können Sie nun DigiCert der Liste der Zertifizierungsstellen im Schlüsseltresor hinzufügen.

### <a name="azure-portal"></a>Azure-Portal

1.  Um die DigiCert-Zertifizierungsstelle hinzuzufügen, navigieren Sie zu dem Schlüsseltresor, dem Sie DigiCert hinzufügen möchten. 
2.  Wählen Sie auf den Key Vault-Eigenschaftenseiten die Option **Zertifikate** aus.
3.  Wählen Sie die Registerkarte **Zertifizierungsstellen** aus. ![Zertifikateigenschaften](../media/certificates/how-to-integrate-certificate-authority/select-certificate-authorities.png)
4.  Wählen Sie die Option **Hinzufügen** aus.
 ![Zertifikateigenschaften](../media/certificates/how-to-integrate-certificate-authority/add-certificate-authority.png)
5.  Wählen Sie im Bildschirm **Zertifizierungsstelle erstellen** die folgenden Werte aus:
    -   **Name**: Fügen Sie einen identifizierbaren Ausstellernamen hinzu. Beispiel: DigicertCA
    -   **Anbieter**: Wählen Sie DigiCert aus dem Menü aus.
    -   **Account ID (Konto-ID)** : Geben Sie Ihre DigiCert CertCentral-Konto-ID ein.
    -   **Kontokennwort**: Geben Sie den API-Schlüssel ein, den Sie in Ihrem DigiCert CertCentral-Konto erstellt haben.
    -   **Organisations-ID**: Geben Sie die aus dem DigiCert CertCentral-Konto gesammelte OrgID ein. 
    -   Klicken Sie auf **Erstellen**.
   
6.  Sie werden feststellen, dass DigicertCA jetzt in der Liste der Zertifizierungsstellen hinzugefügt ist.


### <a name="azure-powershell"></a>Azure PowerShell

Mit Azure PowerShell können Azure-Ressourcen mithilfe von Befehlen oder Skripts erstellt und verwaltet werden. Azure hostet Azure Cloud Shell, eine interaktive Shell-Umgebung, die Sie über Ihr Azure-Portal im Browser selbst nutzen können.

Wenn Sie PowerShell lokal installieren und verwenden möchten, müssen Sie für dieses Tutorial mindestens die Version 1.0.0 des Azure PowerShell-Moduls verwenden. Geben Sie `$PSVersionTable.PSVersion` ein, um die Version zu ermitteln. Wenn Sie ein Upgrade ausführen müssen, finden Sie unter [Installieren des Azure PowerShell-Moduls](/powershell/azure/install-az-ps) Informationen dazu. Wenn Sie PowerShell lokal ausführen, müssen Sie auch `Login-AzAccount` ausführen, um eine Verbindung mit Azure herzustellen.

```azurepowershell-interactive
Login-AzAccount
```

1.  Erstellen Sie eine **Ressourcengruppe**.

Erstellen Sie mit [New-AzResourceGroup](/powershell/module/az.resources/new-azresourcegroup) eine Azure-Ressourcengruppe. Eine Ressourcengruppe ist ein logischer Container, in dem Azure-Ressourcen bereitgestellt und verwaltet werden. 

```azurepowershell-interactive
New-AzResourceGroup -Name ContosoResourceGroup -Location EastUS
```

2. Erstellen Sie einen **Schlüsseltresor**.

Sie müssen einen eindeutigen Namen für Ihren Schlüsseltresor verwenden. Hier ist „Contoso-Vaultname“ der Name für den Schlüsseltresor in diesem Handbuch.

- **Tresorname**: Contoso-Vaultname.
- **Ressourcengruppenname:** ContosoResourceGroup
- **Standort**: EastUS.

```azurepowershell-interactive
New-AzKeyVault -Name 'Contoso-Vaultname' -ResourceGroupName 'ContosoResourceGroup' -Location 'EastUS'
```

3. Definieren Sie Variablen für aus dem DigiCert CertCentral-Konto gesammelte Informationen.

- Definieren Sie die Variable **Account ID** (Konto-ID).
- Definieren Sie die Variable **Org-ID** (Organisations-ID).
- Definieren Sie die Variable **API Key** (API-Schlüssel).
- Definieren Sie die Variable **Issuer Name** (Ausstellername).

```azurepowershell-interactive
$accountId = "myDigiCertCertCentralAccountID"
$org = New-AzureKeyVaultCertificateOrganizationDetails -Id OrganizationIDfromDigiCertAccount
$secureApiKey = ConvertTo-SecureString DigiCertCertCentralAPIKey -AsPlainText –Force
$issuerName = "DigiCertCA"
```

4. Legen Sie den **Issuer** (Aussteller) fest. Hierdurch wird DigiCert als Zertifizierungsstelle im Schlüsseltresor hinzugefügt.
```azurepowershell-interactive
Set-AzureKeyVaultCertificateIssuer -VaultName $vaultName -IssuerName $issuerName -IssuerProvider DigiCert -AccountId $accountId -ApiKey $secureApiKey -OrganizationDetails $org
```

5. **Festlegen der Richtlinie für das Zertifikat und Ausstellen eines Zertifikats** von DigiCert direkt im Schlüsseltresor.

```azurepowershell-interactive
$Policy = New-AzKeyVaultCertificatePolicy -SecretContentType "application/x-pkcs12" -SubjectName "CN=contoso.com" -IssuerName DigiCertCA -ValidityInMonths 12 -RenewAtNumberOfDaysBeforeExpiry 60
Add-AzKeyVaultCertificate -VaultName "Contoso-Vaultname" -Name "ExampleCertificate" -CertificatePolicy $Policy
```

Das Zertifikat wurde nun erfolgreich von Digicert CA innerhalb des angegebenen Schlüsseltresors durch diese Integration ausgestellt.

## <a name="troubleshoot"></a>Problembehandlung

Wenn das ausgestellte Zertifikat im Azure-Portal den Status „Deaktiviert“ hat, fahren Sie mit der Anzeige des **Zertifikatvorgangs** fort, um die DigiCert-Fehlermeldung für dieses Zertifikat zu überprüfen.

 ![Zertifikateigenschaften](../media/certificates/how-to-integrate-certificate-authority/certificate-operation-select.png)

Weitere Informationen finden Sie unter den [Zertifikatvorgängen in der Referenz zur REST-API für Azure Key Vault](/rest/api/keyvault). Informationen zum Einrichten von Berechtigungen finden Sie unter [Tresore – Erstellen oder Aktualisieren](/rest/api/keyvault/vaults/createorupdate) und [Vaults – Aktualisieren der Zugriffsrichtlinie](/rest/api/keyvault/vaults/updateaccesspolicy).

## <a name="next-steps"></a>Nächste Schritte

- [Authentifizierung, Anforderungen und Antworten](../general/authentication-requests-and-responses.md)
- [Entwicklerhandbuch für Key Vault](../general/developers-guide.md)
