---
title: リリース ノート - Windows Server バージョン 1709 に関する重要な問題
description: クラッシュ、ハング、インストールの失敗、データの損失を回避するための回避策を必要とする重大な問題についてまとめます。クラッシュ、ハング、インストールの失敗、データの損失を回避するための回避策を必要とする重大な問題についてまとめます。
ms.prod: windows-server
ms.date: 04/23/2018
ms.technology: server-general
ms.topic: article
ms.assetid: 134aab85-664f-4d44-87ef-9e5fd389071f
author: jaimeo
ms.author: jaimeo
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: fea4b259986d1ca6e2f992168f7b0c2e1a177916
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "80826105"
---
# <a name="release-notes-important-issues-in-windows-server-version-1709"></a>リリース ノート:Windows Server バージョン 1709 に関する重要な問題

>適用先:Windows Server 半期チャネル

これらのリリース ノートは、Windows Server&reg; オペレーティング システムの最も重大な問題とその回避策 (存在する場合) についてまとめます。 このリリースにおける計画的な変更点、新機能、および修正プログラムについては、「[Windows Server バージョン 1709 の新機能](whats-new-in-windows-server-1709.md)」と特定の機能チームからのお知らせを参照してください。 特に指定がない限り、レポートされる問題はそれぞれ、Windows Server 2016 のすべてのエディションおよびインストール オプションに適用されます。  

このドキュメントは継続的に更新されています。 解決策が必要な重大な問題が発見された場合、および新しい解決策および修正が使用可能になった場合は、ここに追加されます。  
  
## <a name="storage-spaces-direct"></a>記憶域スペース ダイレクト
[comment]: # (ID: 不明、送信者: stevenek、状態: サインオフ)  
記憶域スペース ダイレクトは Windows Server バージョン 1709 には含まれません。 Windows Server バージョン 1709 を実行しているサーバー上で *Enable-ClusterStorageSpacesDirect* またはそのエイリアス *Enable-ClusterS2D* を呼び出した場合、"要求された操作がサポートされていません" というメッセージと共にエラーが返されます。

Windows Server バージョン 1709 を実行しているサーバーを、Windows Server 2016 記憶域スペース ダイレクトの展開に導入することもサポートされていません。

Windows Server のリリース モデルでは、[Windows 10](https://docs.microsoft.com/windows/deployment/update/waas-overview) と [Office 365 ProPlus](https://support.office.com/article/Overview-of-the-upcoming-changes-to-Office-365-ProPlus-update-management-78b33779-9356-4cdf-9d2c-08350ef05cca?ui=en-US&rs=en-US&ad=US) で行われている同様のリリースおよびサービス モデルに連動するために、新しいオプションが提供されます。 半期チャネルのリリースでは、迅速なペースでの移行を考えているお客様に新しい機能を提供します。新しいリリースは、年に 2 回、春と秋に提供されます。

半期チャネルの Windows Server は、よりすばやいイノベーションからメリットを引き出す、コンテナーとアプリケーションのシナリオに重点を置いています。追加情報については、この[ブログ](https://cloudblogs.microsoft.com/windowsserver/2018/03/29/windows-server-semi-annual-channel-update)を参照してください。 記憶域スペース ダイレクトなどのインフラストラクチャ ロールを探しているお客様は、Windows Server 2016 (現在利用可能) や [Windows Server 2019](https://cloudblogs.microsoft.com/windowsserver/2018/03/20/introducing-windows-server-2019-now-available-in-preview) (今年後半にリリース) のように長期的なサービス チャネルのリリースを使用する必要があります。 ハイパーコンバージド インフラストラクチャの最適なプラットフォームの構築に取り組んでおり、新しい機能の開発や、お客様のフィードバックに基づいた既存の機能の改善を継続しています。 

記憶域スペース ダイレクトは、Windows Server 2016 で導入された、Microsoft のハイパーコンバージド プラットフォームの基盤です。 お陰様で Microsoft ハイパーコンバージド プラットフォームは積極的に導入されており、Microsoft ではこれからもお客様へのコミットメントに取り組んでまいります。

Microsoft では、フィードバックに耳を傾けながら、ハイパーコンバージド プラットフォームに関する[次世代のイノベーション](https://blogs.technet.microsoft.com/windowsserver/2017/09/07/sneak-peek-2-windows-server-version-1709-hyper-converged-infrastructure/)の提供に取り組んでいます。 これらの機能は、現在、[Windows Insider](https://insider.windows.com/for-business/) のビルドで利用できます。ぜひ新しい機能をお試しいただき、フィードバックをお寄せください。 検証済みのハイパーコンバージド ソリューションをお探しのお客様には、[Windows Server Software Defined](https://microsoft.com/wssd) プログラムをお勧めします。
