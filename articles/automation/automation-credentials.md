---
title: "Azure Automation での資格情報資産 | Microsoft Docs"
description: "Azure Automation の資格情報資産には、Runbook または DSC 構成によってアクセスされるリソースの認証に使用できるセキュリティ資格情報が含まれます。 この記事では、資格情報資産を作成し、Runbook または DSC 構成でそれを使用する方法について説明します。"
services: automation
documentationcenter: 
author: eslesar
manager: carmonm
editor: tysonn
ms.assetid: 3209bf73-c208-425e-82b6-df49860546dd
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/14/2017
ms.author: bwren
ms.openlocfilehash: 70f6272d936b097a9458dfa18279a70727da9d6b
ms.sourcegitcommit: 9c3150e91cc3075141dc2955a01f47040d76048a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/26/2017
---
# <a name="credential-assets-in-azure-automation"></a>Azure Automation での資格情報資産
Automation の資格情報資産は、ユーザー名やパスワードなどのセキュリティ資格情報を含む [PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential) オブジェクトを保持しています。 Runbook および DSC 構成では、認証に PSCredential オブジェクトを受け付けるコマンドレットを使用したり、PSCredential オブジェクトのユーザー名とパスワードを抽出して認証を必要とするアプリケーションやサービスに提供したりできます。 資格情報のプロパティは、Azure Automation に安全に格納されており、Runbook または DSC 構成で [Get-AutomationPSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential.aspx) アクティビティを使用してアクセスできます。

> [!NOTE]
> Azure Automation でセキュリティ保護される資産としては、資格情報、証明書、接続、暗号化された変数などがあります。 これらの資産は、各 Automation アカウント用に生成された一意のキーを使用して暗号化され、Azure Automation に保存されます。 このキーはマスター証明書によって暗号化され、Azure Automation に保存されます。 セキュリティで保護された資産を格納する前に、オートメーション アカウントのキーがマスター証明書を使用して復号化され、資産の暗号化に使用されます。  

## <a name="azure-classic-powershell-cmdlets"></a>Azure クラシック PowerShell コマンドレット
Windows PowerShell で Automation 資格情報資産を作成および管理するには、次の表のコマンドレットを使用します。  これらのコマンドレットは、Automation Runbook と DSC 構成に使用できる [Azure PowerShell モジュール](/powershell/azure/overview) に付属しています。

| コマンドレット | 説明 |
|:--- |:--- |
| [Get-AzureAutomationCredential](/powershell/module/azure/get-azureautomationcredential?view=azuresmps-3.7.0) |資格情報資産に関する情報を取得します。 **Get-AutomationPSCredential** アクティビティから取得できるのは、資格情報自体のみです。 |
| [New-AzureAutomationCredential](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |新しい Automation 資格情報を作成します。 |
| [Remove-AzureAutomationCredential](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |Automation 資格情報を削除します。 |
| [Set-AzureAutomationCredential](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |既存の Automation 資格情報のプロパティを設定します。 |

## <a name="azurerm-powershell-cmdlets"></a>AzureRM PowerShell コマンドレット
AzureRM の場合、Windows PowerShell で Automation 資格情報資産を作成および管理するには、次の表のコマンドレットを使用します。  これらのコマンドレットは、Automation Runbook と DSC 構成に使用できる [AzureRM.Automation モジュール](/powershell/azure/overview) に付属しています。

| コマンドレット | Description |
|:--- |:--- |
| [Get-AzureRmAutomationCredential](/powershell/module/azurerm.automation/get-azurermautomationcredential?view=azurermps-4.4.0) |資格情報資産に関する情報を取得します。  |
| [New-AzureRmAutomationCredential](/powershell/module/azurerm.automation/new-azurermautomationcredential?view=azurermps-4.4.0) |新しい Automation 資格情報を作成します。 |
| [Remove-AzureRmAutomationCredential](/powershell/module/azurerm.automation/remove-azurermautomationcredential?view=azurermps-4.4.0) |Automation 資格情報を削除します。 |
| [Set-AzureRmAutomationCredential](/powershell/module/azurerm.automation/set-azurermautomationcredential?view=azurermps-4.4.0) |既存の Automation 資格情報のプロパティを設定します。 |

## <a name="runbook-activities"></a>Runbook アクティビティ
次の表のアクティビティは、Runbook および DSC 構成で資格情報にアクセスするために使用されます。

| アクティビティ | 説明 |
|:--- |:--- |
| Get-AutomationPSCredential |Runbook または DSC 構成で使用する資格情報を取得します。 [System.Management.Automation.PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential) オブジェクトを返します。 |

> [!NOTE]
> Get-AutomationPSCredential の –Name パラメーターを使用すると、設計時に Runbook または DSC 構成と資格情報資産の間の依存関係の検出が複雑になる可能性があるため、使用しないようにする必要があります。

## <a name="python2-functions"></a>Python2 関数
次の表の関数を使用して、Python2 Runbook の資格情報にアクセスします。

| 関数 | Description |
|:---|:---|
| automationassets.get_automation_credential | 資格情報資産に関する情報を取得します。 |

> [!NOTE]
> 資産関数にアクセスするには、お使いの Python Runbook の上部にある "automationassets" モジュールをインポートする必要があります。

## <a name="creating-a-new-credential-asset"></a>新しい資格情報資産の作成

### <a name="to-create-a-new-credential-asset-with-the-azure-portal"></a>Azure ポータルで新しい資格情報資産を作成するには
1. Automation アカウントから、**[資産]** 部分をクリックして **[資産]** ブレードを開きます。
2. **[資格情報]** 部分をクリックして、**[資格情報]** ブレードを開きます。
3. ブレード上部の **[資格情報の追加]** をクリックします。
4. フォームに入力し、 **[作成]** をクリックして新しい資格情報を保存します。

### <a name="to-create-a-new-credential-asset-with-windows-powershell"></a>Windows PowerShell で新しい資格情報資産を作成するには
次のサンプル コマンドでは、新しい Automation 資格情報を作成する方法について説明します。 最初に名前とパスワードで PSCredential オブジェクトを作成し、それを使用して資格情報資産を作成します。 または、 **Get-Credential** コマンドレットを使用し、プロンプトに従って名前とパスワードを入力することもできます。

    $user = "MyDomain\MyUser"
    $pw = ConvertTo-SecureString "PassWord!" -AsPlainText -Force
    $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $user, $pw
    New-AzureAutomationCredential -AutomationAccountName "MyAutomationAccount" -Name "MyCredential" -Value $cred

### <a name="to-create-a-new-credential-asset-with-the-azure-classic-portal"></a>Azure クラシック ポータルで新しい資格情報資産を作成するには
1. Automation アカウントから、ウィンドウの上部にある **[資産]** をクリックします。
2. ウィンドウの下部にある **[設定の追加]**をクリックします。
3. **[資格情報の追加]**をクリックします。
4. In the **Credential Type** dropdown, select **PowerShell Credential**.
5. ウィザードを完了し、チェック ボックスをクリックして新しい資格情報を保存します。

## <a name="using-a-powershell-credential"></a>PowerShell 資格情報の使用
Runbook または DSC 構成で資格情報資産を取得するには、**Get-AutomationPSCredential** アクティビティを使用します。 このアクティビティが返す [PSCredential オブジェクト](http://msdn.microsoft.com/library/system.management.automation.pscredential.aspx)を、PSCredential パラメーターを必要とするアクティビティまたはコマンドレットで使用できます。 また、資格情報オブジェクトのプロパティを取得して個別に使用することもできます。 オブジェクトにはユーザー名と安全なパスワードのプロパティがあります。または、**GetNetworkCredential** メソッドを使用して、安全ではないバージョンのパスワードを提供する [NetworkCredential](http://msdn.microsoft.com/library/system.net.networkcredential.aspx) オブジェクトを取得することもできます。

### <a name="textual-runbook-sample"></a>テキストの Runbook のサンプル
次のサンプル コマンドでは、Runbook で PowerShell 資格情報を使用する方法を示します。 この例では、資格情報を取得し、そのユーザー名とパスワードを変数に代入します。

    $myCredential = Get-AutomationPSCredential -Name 'MyCredential'
    $userName = $myCredential.UserName
    $securePassword = $myCredential.Password
    $password = $myCredential.GetNetworkCredential().Password


### <a name="graphical-runbook-sample"></a>グラフィカルな Runbook のサンプル
グラフィカル エディターの [ライブラリ] ウィンドウで資格情報を右クリックして **[キャンバスに追加]** を選択することにより、**Get-AutomationPSCredential** アクティビティをグラフィカルな Runbook に追加します。

![キャンバスに資格情報を追加する](media/automation-credentials/credential-add-canvas.png)

次の図は、グラフィカルな Runbook で資格情報を使用する例を示したものです。  この例では、「 [Authenticate Runbooks with Azure AD User account (Azure AD ユーザー アカウントでの Runbook の認証)](automation-create-aduser-account.md)」で説明されているように、Runbook 用の認証を Azure リソースに提供するために使用されています。  最初のアクティビティは、Azure サブスクリプションへのアクセス権を持つ資格情報を取得します。  その後、 **Add-AzureAccount** アクティビティはこの資格情報を使用して、その後にあるすべてのアクティビティに認証を提供します。  [Get-AutomationPSCredential](automation-graphical-authoring-intro.md#links-and-workflow) は 1 つのオブジェクトを受け取るので、ここでは **パイプライン リンク** を使用します。  

![キャンバスに資格情報を追加する](media/automation-credentials/get-credential.png)

## <a name="using-a-powershell-credential-in-dsc"></a>DSC での PowerShell 資格情報の使用
Azure Automation の DSC 構成では **Get-AutomationPSCredential**を使用して資格情報資産を参照できますが、必要に応じて、パラメーターを使用して資格情報資産を渡すこともできます。 詳細については、「 [Azure Automation DSC での構成のコンパイル](automation-dsc-compile.md#credential-assets)」を参照してください。

## <a name="using-credentials-in-python2"></a>Python2 の資格情報の使用
次のサンプルでは、Python2 Runbook で資格情報にアクセスする例を示します。

    import automationassets
    from automationassets import AutomationAssetNotFound

    # get a credential
    cred = automationassets.get_automation_credential("credtest")
    print cred["username"]
    print cred["password"]

## <a name="next-steps"></a>次のステップ
* グラフィカル作成でのリンクの詳細については、「 [グラフィカル作成でのリンク](automation-graphical-authoring-intro.md#links-and-workflow)
* Automation のさまざまな認証方法を理解するには、「 [Azure Automation のセキュリティ](automation-security-overview.md)
* グラフィカルな Runbook の使用を開始するには、「 [初めてのグラフィカルな Runbook](automation-first-runbook-graphical.md)
* PowerShell Workflow Runbook の使用を開始するには、「 [最初の PowerShell Workflow Runbook](automation-first-runbook-textual.md) 
* Python2 Runbook の使用を開始するには、[初めての Python2 Runbook](automation-first-runbook-textual-python2.md) に関するページをご覧ください 

