---
title: 'リリース ノート: Windows Server バージョン 1709 に関する重要な問題'
description: クラッシュ、ハング、インストールの失敗、データの損失を回避するための回避策を必要とする重大な問題についてまとめます。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.date: 04/23/2018
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 134aab85-664f-4d44-87ef-9e5fd389071f
author: jaimeo
ms.author: jaimeo
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: 4eebc498289a81c7f27fcf4b84d81ae13bc38e4f
ms.sourcegitcommit: e84e328c13a701e8039b16a4824a6e58a6e59b0b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2018
ms.locfileid: "4133858"
---
# リリース ノート: Windows Server バージョン 1709 に関する重要な問題

>適用対象: Windows Server の半期チャネル

これらのリリース ノートは、Windows Server&reg; オペレーティング システムの最も重大な問題とその回避策 (存在する場合) についてまとめます。 このリリースにおける計画的な変更点、新機能、および修正プログラムについては、「[Windows Server バージョン 1709 の新機能](whats-new-in-windows-server-1709.md)」と特定の機能チームからのお知らせを参照してください。 特に指定がない限り、レポートされる問題はそれぞれ、Windows Server 2016 のすべてのエディションおよびインストール オプションに適用されます。  

このドキュメントは継続的に更新されています。 解決策が必要な重大な問題が発見された場合、および新しい解決策および修正が使用可能になった場合は、ここに追加されます。  
  
## 記憶域スペース ダイレクト
[comment]: # (ID: 不明です。提出者: stevenek です。状態: サインオフ)  
記憶域スペース ダイレクトは Windows Server バージョン 1709 には含まれません。 Windows Server バージョン 1709 を実行しているサーバーで *Enable-ClusterStorageSpacesDirect* またはそのエイリアス *Enable-ClusterS2D* を呼び出した場合、「要求された操作がサポートされていません」というメッセージと共にエラーが返されます。

Windows Server バージョン 1709 を実行しているサーバーを、Windows Server 2016 記憶域スペース ダイレクトの展開に導入することもサポートされていません。

Windows Server のリリース モデルで、新しいオプションが提供されます。これは、[Windows 10](https://docs.microsoft.com/windows/deployment/update/waas-overview) と [Office 365 ProPlus](https://support.office.com/article/Overview-of-the-upcoming-changes-to-Office-365-ProPlus-update-management-78b33779-9356-4cdf-9d2c-08350ef05cca?ui=en-US&rs=en-US&ad=US) で行われている同様のリリースおよびサービス モデルに連動するためのものです。 半期チャネルのリリースでは、迅速なペースで移行する必要があるお客様に新しい機能を提供します。新しいリリースは、年に 2 回、春と秋に提供されます。

Windows Server の半期チャネルがコンテナーおよびなイノベーションを高速な活用するアプリケーション シナリオに重点を置いて、追加の情報をこの[ブログ](https://cloudblogs.microsoft.com/windowsserver/2018/03/29/windows-server-semi-annual-channel-update)をご覧ください。 記憶域スペース ダイレクトなどのインフラストラクチャの役割を探しているユーザーは、Windows Server 2016 (利用できるようになりました) と[Windows Server 2019](https://cloudblogs.microsoft.com/windowsserver/2018/03/20/introducing-windows-server-2019-now-available-in-preview) (今年後半近日公開予定) などの Long-Term Servicing チャネル リリースを使用してください。 ハイパーコンバージド インフラストラクチャ、最適なプラットフォームの構築に取り組んでいます、新機能を開発し、お客様のフィードバックに基づいて、既存の向上を継続します。 

記憶域スペース ダイレクトは、Windows Server 2016 で導入された、Microsoft のハイパーコンバージド プラットフォームの基盤です。 Microsoft ハイパーコンバージド プラットフォームの積極的な導入が進んでおり、Microsoft ではこれからもお客様へのコミットメントに取り組んでまいります。

お客様のフィードバックを待機してしたし、[次世代の技術革新設定](https://blogs.technet.microsoft.com/windowsserver/2017/09/07/sneak-peek-2-windows-server-version-1709-hyper-converged-infrastructure/)に対して、ハイパーコンバージド プラットフォームを提供する作業します。 これらの機能は[Windows Insider](https://insider.windows.com/for-business/)ビルドで現在利用可能としようとして、お客様のフィードバックを共有することをお寄せします。 検証済みのハイパーコンバージド ソリューションをお探しのお客様には、[Windows Server Software Defined](http://microsoft.com/wssd) プログラムをお勧めします。
