---
title: "独自に開発したアプリケーションのトークン有効期間の既定値を変更する方法 | Microsoft Docs"
description: "Azure AD で開発しているアプリケーションのトークンの有効期間ポリシーを更新する方法"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: a28eacd820ed28a6470992ce86b060e886c00bcb
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/11/2017
---
# <a name="how-to-change-the-token-lifetime-defaults-for-a-custom-developed-application"></a>独自に開発したアプリケーションのトークン有効期間の既定値を変更する方法

Azure AD Premium では、非機密クライアントに対して発行されたトークンの有効期間をアプリ開発者とテナント管理者が構成できます。 トークンの有効期間ポリシーは、テナント全体またはアクセスされるリソースに対して設定されます。

 * トークンの有効期間ポリシーを設定するには、[Azure AD PowerShell モジュール](https://www.powershellgallery.com/packages/AzureADPreview)をダウンロードする必要があります。

 * **Connect-AzureAD -Confirm** コマンドを実行します。

 * 次のサンプル ポリシーは、MaxAgeSingleFactor 更新トークンを設定します。 次のポリシーを作成します。 ```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```

 * その他のカスタム ポリシーを作成する方法については、[トークンの有効期間の構成](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)に関するドキュメントを参照してください。

## <a name="next-steps"></a>次のステップ
[トークンの有効期間の構成](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)<br>

[Azure AD のトークン リファレンス](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-token-and-claims)

