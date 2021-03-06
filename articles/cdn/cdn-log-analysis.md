---
title: "Azure CDN の使用パターンを分析する | Microsoft Docs"
description: "顧客は、Azure CDN のログ分析を有効にすることができます。"
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 95e18b3c-b987-46c2-baa8-a27a029e3076
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: v-semcev
ms.openlocfilehash: 04e5499011e72dfcc20dff370d5d837227ed29b6
ms.sourcegitcommit: cf4c0ad6a628dfcbf5b841896ab3c78b97d4eafd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/21/2017
---
# <a name="analyze-azure-cdn-usage-patterns"></a>Azure CDN の使用パターンを分析する

アプリケーションの CDN を有効にした後、CDN の使用状況の監視、配信の正常性の確認、潜在的な問題のトラブルシューティングを行うことができます。 Azure CDN では、これらの機能が次の 2 とおりの方法で利用できます。 

## <a name="verizon-core-reports"></a>Verizon コア レポート

Verizon Standard または Verizon Premium プロファイルを所有する Azure CDN ユーザーは、Verizon 補助ポータルで Verizon コア レポートを表示できます。 Verizon コア レポートには、Azure Portal の **[管理]** オプションからアクセスできます。このレポートには、さまざまなグラフとビューが用意されています。 詳細については、「[Verizon からのコア レポート](cdn-analyze-usage-patterns.md)」を参照してください。

## <a name="verizon-custom-reports"></a>Verizon カスタム レポート

Verizon Standard または Verizon Premium プロファイルを所有する Azure CDN ユーザーは、Verizon 補助ポータルで Verizon カスタム レポートを表示できます。 Verizon カスタム レポートには、Azure Portal の **[管理]** オプションからアクセスできます。 Verizon カスタム レポート ページには、Azure CDN プロファイルに属する各エッジ CName のヒット数や転送されたデータが表示されます。 データは、HTTP 応答コードまたは一定期間にわたるキャッシュの状態でグループ化できます。 詳細については、「[Custom Reports from Verizon (Verizon のカスタム レポート)](cdn-verizon-custom-reports.md)」をご覧ください。

## <a name="core-analytics-via-azure-diagnostic-logs"></a>Azure 診断ログによるコア分析

コア分析は、Verizon (Standard/Premium) および Akamai (Standard) の CDN プロファイルに属しているすべての CDN エンドポイントで使用できます。 Azure 診断ログを使用すると、Azure Storage、イベント ハブ、Operations Management Suite (OMS) Log Analytics のいずれかにコア分析をエクスポートすることができます。 OMS Log Analytics には、ユーザーによる構成とカスタマイズに対応したグラフを含んだソリューションが用意されています。 詳細については、「[Azure diagnostic logs (Azure 診断ログ)](cdn-azure-diagnostic-logs.md)」を参照してください。

