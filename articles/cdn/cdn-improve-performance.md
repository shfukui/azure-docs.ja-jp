---
title: "Azure CDN でのファイル圧縮によるパフォーマンスの向上 | Microsoft Docs"
description: "Azure CDN でファイルを圧縮して、ファイル転送速度とページ読み込みパフォーマンスを向上させる方法を説明します。"
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: af1cddff-78d8-476b-a9d0-8c2164e4de5d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 86f1f8f0aaa9a699d2f816781cef65cda868ee55
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/11/2017
---
# <a name="improve-performance-by-compressing-files-in-azure-cdn"></a>Azure CDN でのファイル圧縮によるパフォーマンスの向上
圧縮は、サーバーからファイルを送信する前にファイル サイズを減らすことができるので、ファイルの転送速度を改善し、ページ読み込みのパフォーマンスを向上するには簡単で効率的な方法です。 帯域幅のコストが軽減され、ユーザーへの応答も改善されます。

圧縮を有効にするには、2 つの方法があります。

* 配信元サーバーで圧縮を有効にします。 この方法では、CDN は圧縮ファイルをパス スルーし、要求したクライアントに対して圧縮ファイルを配信します。
* CDN エッジ サーバーで直接、圧縮を有効にします。 この方法では、配信元サーバーで圧縮されていない場合でも、CDN でファイルが圧縮され、エンド ユーザーに渡されます。

> [!IMPORTANT]
> CDN 構成の変更がネットワーク全体に反映されるまでには時間がかかる可能性があります。  <b>Azure CDN from Akamai</b> プロファイルの場合、通常、反映は 1 分以内で完了します。  <b>Azure CDN from Verizon</b> プロファイルの場合、通常、反映は 90 分以内で完了します。  今回初めて CDN エンドポイントの圧縮を設定した場合は、トラブルシューティングの前に、圧縮設定が確実に POP に反映されるように 1 ～ 2 時間の待機時間を検討してください。
> 
> 

## <a name="enabling-compression"></a>圧縮の有効化
> [!NOTE]
> Standard および Premium CDN レベルでは同じ圧縮機能が提供されますが、ユーザー インターフェイスは異なります。  Standard と Premium CDN レベルの違いの詳細については、 [Azure CDN の概要](cdn-overview.md)に関する記述を参照してください。
> 
> 

### <a name="standard-tier"></a>Standard レベル
> [!NOTE]
> このセクションは、**Azure CDN Standard from Verizon** プロファイルと **Azure CDN Standard from Akamai** プロファイルに適用されます。
> 
> 

1. CDN プロファイル ページで、管理する CDN エンドポイントをクリックします。
   
    ![CDN プロファイル エンドポイント](./media/cdn-file-compression/cdn-endpoints.png)
   
    CDN エンドポイントのページが開きます。
2. **[構成]** をクリックします。
   
    ![[CDN プロファイル] の [管理] ボタン](./media/cdn-file-compression/cdn-config-btn.png)
   
    CDN 構成ページが開きます。
3. **[圧縮]**をオンにします。
   
    ![CDN の圧縮オプション](./media/cdn-file-compression/cdn-compress-standard.png)
4. 既定の種類を使用するか、ファイルの種類を削除または追加して一覧を変更します。
   
   > [!TIP]
   > 圧縮形式に圧縮を適用することは可能ですが、推奨されません。 たとえば、ZIP、MP3、MP4、JPG などの形式です。
   > 
 
5. 変更したら、 **[保存]** をクリックします。

### <a name="premium-tier"></a>Premium レベル
> [!NOTE]
> このセクションは、 **Azure CDN Premium from Verizon** プロファイルに適用されます。
> 
> 

1. CDN プロファイル ページで、 **[管理]** をクリックします。
   
    ![[CDN プロファイル] の [管理] ボタン](./media/cdn-file-compression/cdn-manage-btn.png)
   
    CDN 管理ポータルが開きます。
2. **[HTTP ラージ]** タブ、**[キャッシュの設定]** フライアウトの順にマウスのカーソルを合わせます。  **[圧縮]**をクリックします。

    ![ファイル圧縮の選択](./media/cdn-file-compression/cdn-compress-select.png)
   
    圧縮のオプションが表示されます。
   
    ![ファイルの圧縮オプション](./media/cdn-file-compression/cdn-compress-files.png)
3. **[Compression Enabled]** ラジオ ボタンをクリックして圧縮を有効にします。  **[ファイルの種類]** テキストボックスで、コンマ区切りのリスト (スペースなし) として圧縮する MIME の種類を入力します。
   
   > [!TIP]
   > 圧縮形式に圧縮を適用することは可能ですが、推奨されません。 たとえば、ZIP、MP3、MP4、JPG などの形式です。
   > 
4. 変更したら、 **[更新]** をクリックします。

## <a name="compression-rules"></a>圧縮のルール
次の表に、すべてのシナリオでの Azure CDN 圧縮動作を示します。

> [!IMPORTANT]
> **Azure CDN from Verizon** プロファイル (Standard と Premium) の場合、条件を満たすファイルのみが圧縮されます。  圧縮を実行可能にするためのファイルの条件は、次のとおりです。
> 
> * 128 バイトより大きい
> * 1 MB 未満
> 
> これらのプロファイルは、**gzip** (GNU zip)、**deflate**、**bzip2**、または **br** (Brotli) エンコードをサポートしています。 Brotli エンコーディングでは、圧縮はエッジのみで行われます。 クライアント/ブラウザーが Brotli エンコーディングのために要求を送信する必要があります。圧縮されるアセットは最初に配信元で圧縮されている必要があります。 

> [!IMPORTANT]
> **Azure CDN from Akamai** プロファイルの場合、すべてのファイルが圧縮対象です。 ただし、ファイルの MIME タイプは、[圧縮用に構成されている](#enabling-compression)必要があります。
> 
>これらのプロファイルは、**gzip** エンコードのみをサポートしています。 プロファイル エンドポイントが **gzip** でエンコーディングされたファイルを要求すると、クライアントの要求に関係なく、常に配信元から要求されます。 

### <a name="compression-disabled-or-file-is-ineligible-for-compression"></a>圧縮が無効であるか、ファイルの圧縮が実行不可能
| クライアントから要求された形式 (Accept-Encoding ヘッダー経由) | キャッシュされたファイルの形式 | クライアントへの CDN の応答 | メモ |
| --- | --- | --- | --- |
| 圧縮 |圧縮 |圧縮 | |
| 圧縮 |非圧縮 |非圧縮 | |
| 圧縮 |キャッシュなし |圧縮または非圧縮 |配信元の応答に依存 |
| 非圧縮 |圧縮 |非圧縮 | |
| 非圧縮 |非圧縮 |非圧縮 | |
| 非圧縮 |キャッシュなし |非圧縮 | |

### <a name="compression-enabled-and-file-is-eligible-for-compression"></a>圧縮が有効でファイルの圧縮が実行可能
| クライアントから要求された形式 (Accept-Encoding ヘッダー経由) | キャッシュされたファイルの形式 | クライアントへの CDN の応答 | メモ |
| --- | --- | --- | --- |
| 圧縮 |圧縮 |圧縮 |サポートされている形式間での CDN のトランスコード |
| 圧縮 |非圧縮 |圧縮 |CDN が圧縮を実行 |
| 圧縮 |キャッシュなし |圧縮 |配信元から非圧縮が返された場合、CDN が圧縮を実行します。  **Azure CDN from Verizon** は、最初の要求で圧縮されていないファイルを渡し、後続の要求のためにファイルを圧縮してキャッシュします。  `Cache-Control: no-cache` ヘッダーがあるファイルは圧縮されません。 |
| 非圧縮 |圧縮 |非圧縮 |CDN が展開を実行 |
| 非圧縮 |非圧縮 |非圧縮 | |
| 非圧縮 |キャッシュなし |非圧縮 | |

## <a name="media-services-cdn-compression"></a>Media Services CDN の圧縮
Media Services CDN が有効なストリーミング エンドポイントの場合、既定で次のコンテンツ タイプについて圧縮が有効です。 
- application/vnd.ms-sstr+xml 
- application/dash+xml
- application/vnd.apple.mpegurl
- application/f4m+xml 

これらのコンテンツ タイプの圧縮は、Azure Portal を使用して有効または無効に切り替えることはできません。  

## <a name="see-also"></a>関連項目
* [CDN ファイルの圧縮のトラブルシューティング](cdn-troubleshoot-compression.md)    

