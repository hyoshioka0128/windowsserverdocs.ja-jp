---
title: リリース ノート - Windows Server バージョン 1803 に関する重要な問題
description: Windows Server バージョン 1803 をインストールする前に必要な既知の情報、制限時刻、その他の情報について説明する
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.date: 05/07/2018
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
ms.author: elizapo
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: e9bd860769ec375a6d89ac452e3430b791fff3ad
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2019
ms.locfileid: "63688734"
---
# <a name="release-notes-important-issues-in-windows-server-version-1803"></a>リリース ノート:Windows Server バージョン 1803 に関する重要な問題

>適用先:Windows Server 半期チャネル

これらのリリース ノートは、Windows Server オペレーティング システムの最も重大な問題と既知の問題の回避策についてまとめます。 このリリースの最新機能については、「[Windows Server バージョン 1803 の新機能](whats-new-in-windows-server-1803.md)」を参照してください。 Windows Server バージョン 1803 のコンテナーの実行に関心がある場合は、「[Windows コンテナーについて](https://docs.microsoft.com/virtualization/windowscontainers/about/)」を確認してください。 

特に指定がない限り、レポートされる問題はそれぞれ、Windows Server バージョン 1803 のすべてのエディションおよびインストール オプションに適用されます。  

この記事は継続的に更新していきます。 既知の問題が特定されると、ここでそれを文書化します。 


## <a name="software-defined-datacenter"></a>ソフトウェア定義データセンター

記憶域スペース ダイレクトなどのソフトウェア定義のデータセンター機能、ソフトウェア定義のネットワーク、およびシールドされた仮想マシンは、Windows Server バージョン 1803 に含まれません。 「[Windows Server 半期チャネルの更新プログラム](https://cloudblogs.microsoft.com/windowsserver/2018/03/29/windows-server-semi-annual-channel-update/)」に記されているように、Windows Server の半期チャネルは、迅速な革新から利益が得られるコンテナーとアプリケーション シナリオに重点を置いています。 

インフラストラクチャ ロールが必要な場合は、長期的なサービス チャネル リリースを使用してください。Windows Server 2016 (現在の利用可能) または[Windows Server 2019](https://cloudblogs.microsoft.com/windowsserver/2018/03/20/introducing-windows-server-2019-now-available-in-preview) (今年の後半に登場)。

ハイパーコンバージド インフラストラクチャの最適なプラットフォームの構築に取り組んでおり、新しい機能の開発や、お客様のフィードバックに基づいた既存の機能の改善を継続しています。 [記憶域スペース ダイレクトのクラスターが 10,000 を超え](https://blogs.technet.microsoft.com/filecab/2018/03/27/storage-spaces-direct-momentum)、ご協力いただきありがとうございます。 今年の後半ではさらに多くを共有できることを楽しみにしています。