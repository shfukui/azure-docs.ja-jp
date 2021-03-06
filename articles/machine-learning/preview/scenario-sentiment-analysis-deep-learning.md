---
title: "Azure Machine Learning でのディープ ラーニングを使った感情分析 | Microsoft Docs"
description: "Azure ML Workbench でディープ ラーニングを使って感情分析を行う方法を説明します。"
services: machine-learning
documentationcenter: 
author: miprasad
manager: kristin.tolle
editor: miprasad
ms.assetid: 
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/16/2017
ms.author: miprasad
ms.openlocfilehash: 39ae2aa7217b45e8fab77f528b27b77a1b1256bf
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/11/2017
---
# <a name="sentiment-analysis-using-deep-learning-with-azure-machine-learning"></a>Azure Machine Learning でのディープ ラーニングを使った感情分析

感情分析は、自然言語処理の分野ではよく知られているタスクです。 与えられた一連のテキストについて、その感情を判断します。 このソリューションの目的は、CNTK を Keras (ディープ ラーニング モデルを構築するための高水準のビルディング ブロックを提供するモデル レベルのライブラリ) のバックエンドとして使用して、映画のレビューの感情分析を実装することです。

このソリューションは https://github.com/Azure/MachineLearningSamples-SentimentAnalysis にあります。

## <a name="link-to-the-gallery-github-repository"></a>ギャラリーの GitHub リポジトリへのリンク

以下は、パブリック GitHub リポジトリのリンクです。

[https://github.com/Azure/MachineLearningSamples-SentimentAnalysis](https://github.com/Azure/MachineLearningSamples-SentimentAnalysis)

## <a name="use-case-overview"></a>ユース ケースの概要

データの急増とモバイル デバイスの普及に伴い、人々はあらゆる物事に対して、いつでも自分の感情や態度を表現できるようになりました。 こうした人々の意見、つまり "センチメント (感情)" は、主にソーシャル チャンネルでのレビューやチャット、共有、いいね!、ツイートなどに表れます。センチメントは、企業が商品やサービスの改善を図ったり、情報に基づく決定を下したり、ブランドのプロモーションを促進したりする際の重要な指針となります。

企業が感情分析を活用するには、構造化されていない膨大なソーシャル データを掘り起こして、実践的な分析情報を得られるようにする必要があります。 このサンプルでは、AMLWorkbench を使って、映画のレビューの感情分析を行うディープ ラーニング モデルを構築します。

## <a name="prerequisites"></a>前提条件

* [Azure アカウント](https://azure.microsoft.com/free/) (無料試用版もご利用いただけます)。

* [Azure Machine Learning Workbench](./overview-what-is-azure-ml.md)。[クイックスタート インストール ガイド](./quickstart-installation.md)に従ってプログラムをインストールし、ワークスペースを作成します。

* 運用化のために、Docker エンジンをローカルにインストールして実行することをお勧めします。 運用化しない場合はクラスター オプションを使用することもできますが、 Azure Container Service (ACS) の実行には高額なコストがかかることがあります。

* このソリューションでは、Docker エンジンをローカルにインストールした Windows 10 で Azure Machine Learning Workbench を実行しているものとします。 macOS の場合も、手順の多くは同じです。

## <a name="data-description"></a>データの説明

このサンプルで使用するデータセットは手作業で作成された小規模なデータセットで、[data フォルダー](https://github.com/Azure/MachineLearningSamples-SentimentAnalysis/tree/master/data)にあります。

最初の列には映画のレビューが、2 列目にはそれぞれのセンチメント (0 は否定的なセンチメント、1 は肯定的なセンチメント) が含まれています。 このデータセットはデモンストレーション用です。より堅牢なセンチメント スコアを利用するには、通常はより大規模なデータセットが必要です。 たとえば、Keras の [IMDB Movie reviews sentiment classification](https://keras.io/datasets/#datasets ) (IMDB の 映画レビューのセンチメント分類) では、IMDB が持つ映画レビュー 25,000 件の データセットが、センチメント別 (肯定または否定) にラベル付けされています。 このラボの目的は、AMLWorkbench でディープ ラーニングを使って感情分析を行う方法を示すことです。

## <a name="scenario-structure"></a>シナリオの構成

フォルダー構造は次のようになっています。

1. AMLWorkbench を使用した感情分析に関連するすべてのコードはルート フォルダーに含まれています
2. data: このソリューションで使用するデータセットが含まれています
3. docs: すべてのハンズオン ラボが含まれています

このソリューションのハンズオン ラボの実行順序は次のとおりです。

| 順序| ファイル名 | 関連ファイル |
|--|-----------|------|
| 1 | [`SentimentAnalysisDataPreparation.md`](https://github.com/Azure/MachineLearningSamples-SentimentAnalysis/blob/master/docs/SentimentAnalysisDataPreparation.md) | 'data/sampleReviews.txt' |
| 2 | [`SentimentAnalysisModelingKerasWithCNTKBackend.md`](https://github.com/Azure/MachineLearningSamples-SentimentAnalysis/blob/master/docs/SentimentAnalysisModelingKerasWithCNTKBackend.md) | 'SentimentExtraction.py' |
| 3 | [`SentimentAnalysisModelingDocker.md`](https://github.com/Azure/MachineLearningSamples-SentimentAnalysis/blob/master/docs/SentimentAnalysisModelingDocker.md) | 'SentimentExtractionDocker.py' |
| 4 | [`SentimentAnalysisOperationalization.md`](https://github.com/Azure/MachineLearningSamples-SentimentAnalysis/blob/master/docs/SentimentAnalysisOperationalization.md) | 'Operaionalization' |

## <a name="conclusion"></a>まとめ

このソリューションでは、Azure Machine Learning Workbench でディープ ラーニングを使って感情分析を行う方法を紹介します。 このソリューションには、CNTK/Tensorflow を Keras のバックエンドとして使用する柔軟性があります。 さらに、HDF5 モデルを使って運用化します。
