---
title: "Azure Policy の概要 | Microsoft Docs"
description: "Azure Policy は Azure のサービスであり、Azure 環境でのポリシー定義の作成、割り当て、管理に使うことができます。"
services: azure-policy
keywords: 
author: Jim-Parker
ms.author: jimpark; nini
ms.date: 10/06/2017
ms.topic: overview
ms.service: azure-policy
manager: jochan
ms.custom: mvc
ms.openlocfilehash: 01b0915cdf37ddc00a4e6a38c99ce7f6f8c4f9c9
ms.sourcegitcommit: 51ea178c8205726e8772f8c6f53637b0d43259c6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/11/2017
---
# <a name="what-is-azure-policy"></a>Azure Policy とは

IT ガバナンスは、ビジネス目標と IT プロジェクトの間の関係を明確にします。 適切な IT ガバナンスには、イニシアチブの計画と、戦略的なレベルの優先順位の設定が含まれます。 解決できそうもないほど多くの IT の問題を抱えている企業は、ポリシーを実装すると問題の管理の向上と防止に役立ちます。 そのような場合は、Azure Policy を利用できます。

Azure Policy は Azure のサービスであり、ポリシー定義の作成、割り当て、管理に使うことができます。 ポリシー定義は、リソースにさまざまなルールとアクションを適用し、会社の標準とサービス レベル契約へのリソースの準拠が維持されるようにします。 そのために、リソースの評価を実行して、設定されているポリシー定義に準拠していないリソースをスキャンします。

## <a name="policy-definition"></a>ポリシー定義

すべてのポリシー定義には、ポリシーが適用される条件と、条件が満たされた場合に実行される付随アクションが含まれます。

Azure Policy には、既定で使うことができる組み込みポリシーがいくつかあります。 For example:

- **SQL Server 12.0 を必要とする**: このポリシー定義の条件/ルールでは、すべての SQL Server がバージョン 12.0 を使うことが保証されます。 アクションでは、これらの条件を満たしていないすべてのサーバーが拒否されます。
- **許可されるストレージ アカウント SKU**: このポリシー定義の一連の条件/ルールでは、デプロイされているストレージ アカウントが SKU サイズのセット内かどうかが判定されます。 アクションでは、定義されている SKU サイズのセットに準拠していないすべてのサーバーが拒否されます。
- **許可されるリソースの種類**: このポリシー定義の一連の条件/ルールでは、組織がデプロイできるリソースの種類が指定されます。 アクションでは、この定義済みリストの一部ではないすべてのリソースが拒否されます。

ポリシー定義の構造について詳しくは、「[ポリシー定義の構造](../azure-resource-manager/resource-manager-policy.md#policy-definition-structure)」をご覧ください。

## <a name="policy-assignment"></a>ポリシー割り当て
ポリシー割り当ては、特定のスコープ内で実行するように割り当てられたポリシー定義です。 このスコープは、管理グループからリソース グループの範囲で指定できます。

ポリシーの定義と割り当ての設定について詳しくは、「[リソース ポリシーの概要](../azure-resource-manager/resource-manager-policy.md)」をご覧ください。

## <a name="policy-parameters"></a>ポリシー パラメーター
ポリシー パラメーターは、作成する必要があるポリシー定義の数を減らしてポリシーの管理を簡素化するのに役立ちます。 ポリシー定義を作成するときにパラメーターを定義して、ポリシー定義を汎用化できます。 その後は、ポリシーを割り当てるときに、異なる値を渡すことで異なるシナリオにそのポリシー定義を再利用できます (サブスクリプションに対する 1 組の場所を指定するなど)。

パラメーターは、ポリシー定義を作成するときに定義/作成します。 パラメーターを定義するときは、名前と、必要に応じて値を指定します。 たとえば、場所としてポリシーのパラメーターを定義した後、ポリシーを割り当てるときに *EastUS* や *WestUS* などの異なる値を指定できます。

ポリシー パラメーターについて詳しくは、「[リソース ポリシーの概要 - パラメーター](../azure-resource-manager/resource-manager-policy.md#parameters)」をご覧ください。

## <a name="initiative-definition"></a>イニシアチブ定義
イニシアチブ定義は、単一の包括的な目標を実現することを目的として調整されたポリシー定義のコレクションです。 たとえば、Azure Security Center で利用可能なすべてのセキュリティ推奨事項を監視することを目的とする、"**Azure Security Center での監視を有効にする**" というタイトルのイニシアチブを作成できます。

このイニシアチブでは、次のようなポリシー定義を作成します。

1. **暗号化されていない SQL Database を Security Center で監視する** – 暗号化されていない SQL データベースとサーバーを監視します。
2. **OS の脆弱性を Security Center で監視する** – 構成されているベースラインを満たしていないサーバーを監視します。
3. **不足している Endpoint Protection を Security Center で監視する** – Endpoint Protection エージェントがインストールされていないサーバーを監視します。

## <a name="initiative-assignment"></a>イニシアチブ割り当て
ポリシー割り当てと同様に、イニシアチブ割り当ては特定のスコープに割り当てられたイニシアチブの定義です。 イニシアチブを割り当てると、スコープごとに複数のイニシアチブを割り当てる必要性が低下します。 このスコープは、管理グループからリソース グループの範囲になる可能性があります。

前の例の **Azure Security Center での監視を有効にする**イニシアチブを、異なるスコープに割り当てることができます。 たとえば、ある割り当てを **subscriptionA** に割り当て、別の割り当てを **subscriptionB** に割り当てることができます。

## <a name="initiative-parameters"></a>イニシアチブ パラメーター
ポリシー パラメーターと同様に、イニシアチブ パラメーターは冗長性を減らすことでイニシアチブの管理を簡素化できます。 イニシアチブ パラメーターは、基本的に、イニシアチブ内のポリシー定義によって使われるパラメーターのリストです。

たとえば、2 つのポリシー定義を含むイニシアチブ定義 **initiativeC** のシナリオについて考えます。 各ポリシー定義では 1 つのパラメーターが定義されています。

|[ポリシー]  |パラメーターの名前     |パラメーターの型  |注                                                                                                |
|--------|----------------------|-------|----------------------------------------------------------------------------------------------------------------|
|policyA |allowedLocations      |array  |このパラメーターは、パラメーターの型が配列として定義されているため、文字列のリストが値として必要です。 |
|policyB |allowedSingleLocation |string |このパラメーターは、パラメーターの型が文字列として定義されているため、1 つの単語が値として必要です。          |

このシナリオで **initiativeC** のイニシアチブ パラメーターを定義する場合、3 つのオプションがあります。

1. このイニシアチブのポリシー定義のパラメーターを利用します。この例では、*allowedLocations* と *allowedSingleLocation* が **initiativeC** のイニシアチブ パラメーターになります。
2. このイニシアチブ定義内でポリシー定義のパラメーターに値を指定します。 この例では、**policyA のパラメーター – allowedLocations** および **policyB のパラメーター – allowedSingleLocation** に場所のリストを提供できます。
このイニシアチブを割り当てるときに値を指定することもできます。
3. このイニシアチブを割り当てるときに使うことができる "*値*" オプションのリストを指定します。 つまり、このイニシアチブを割り当てるときは、イニシアチブ内のポリシー定義から継承したパラメーターは、この指定されたリストの値だけを持つことができます。

たとえば、イニシアチブ定義を作成するときに値オプションのリスト (*EastUS*、*WestUS*、*CentralUS*、*WestEurope*) を指定した場合、*Southeast Asia* のような異なる値は、リストに含まれないのでイニシアチブ割り当てで入力できません。

## <a name="recommendations-for-managing-policies"></a>ポリシー管理に関する推奨事項

ポリシーの定義と割り当てを作成および管理するときは、以下の点に注意することをお勧めします。

- 環境でポリシー定義を作成する場合、最初は、拒否効果ではなく監査効果を定義して、環境でのポリシー定義の影響を追跡することをお勧めします。 アプリケーションを自動スケールアップするスクリプトが既にある場合、拒否効果を設定すると、このような自動化タスクが妨げられる場合があります。
- 定義と割り当てを作成するときは、組織階層に留意することが重要です。 高いレベルで定義を作成し (たとえば、管理グループやサブスクリプションのレベル)、次の子レベルに割り当てることをお勧めします。 たとえば、管理グループ レベルでポリシー定義を作成した場合、その定義のポリシー割り当てではサブスクリプション レベルを対象にできます。
- 環境のコンプライアンス状態をよりよく理解するため、Standard 価格レベルを使うことをお勧めします。
- 考えているポリシーが 1 つだけの場合でも、ポリシー定義ではなくイニシアチブ定義を常に使うことをお勧めします。 たとえば、ポリシー定義 *policyDefA* をイニシアチブ定義 *initiativeDefC* の下に作成すると、*policyDefA* と同じような目標を持つ別のポリシー定義を作成する場合、単に *initiativeDefC* の下に追加して適切に追跡できます。

   イニシアチブ定義からイニシアチブ割り当てを作成した場合、そのイニシアチブ定義に追加される新しいポリシー定義はすべて、そのイニシアチブ定義のイニシアチブ割り当てに自動的にまとめられることに注意してください。 ただし、新しいポリシー定義に新しいパラメーターを追加する場合は、イニシアチブの定義または割り当てを編集してこれを反映する必要があります。

## <a name="next-steps"></a>次のステップ:
Azure Policy の概要と主要な概念がわかったので、次に以下の記事を読むことをお勧めします。

- [ポリシー定義を割り当てる](./assign-policy-definition.md)
- [Azure CLI を使用してポリシー定義を割り当てる](./assign-policy-definition-cli.md)
- [PowerShell を使用してポリシー定義を割り当てる](./assign-policy-definition-ps.md)
