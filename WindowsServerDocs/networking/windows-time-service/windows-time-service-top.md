---
ms.assetid: e34622ff-b2d0-4f81-8d00-dacd5d6c215e
title: Windows タイム サービス
description: ''
author: shortpatti
ms.author: pashort
manager: dougkim
ms.date: 05/08/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: networking
ms.openlocfilehash: a86c2bdde9c65878b228f153009734da8f03960d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856833"
---
# <a name="windows-time-service-w32time"></a>Windows タイム サービス (W32Time)

>適用対象:Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows 10 以降

Windows タイム サービス (W32Time) では、日付と Active Directory Domain Services (AD DS) で実行されているすべてのコンピューターの時刻を同期します。 時刻の同期は、多くの Windows サービスや基幹業務 (LOB) アプリケーションの適切な操作にとって重要です。 Windows タイム サービスは、ネットワーク上のコンピューター クロックの同期をネットワーク タイム プロトコル (NTP) を使用します。 NTP によりネットワーク アクセス要求を検証し、リソースを割り当てることができる、正確な時刻の値とタイムスタンプのようになります。

Windows タイム サービス (W32Time) のトピックでは、次のコンテンツは利用できます。
- **[Windows Server 2016 の正確な時刻](accurate-time.md)します。** 時刻同期の精度の Windows Server 2016 では、完全な下位 NTP の古いバージョンの Windows 互換性を維持しながら、大幅に向上しています。 1 を維持する運用状態で妥当な UTC または Windows Server 2016 および Windows 10 Anniversary Update のドメイン メンバーに対してより良いに関してミリ秒の精度。
- **[高精度の環境サポート境界](support-boundary.md)します。** この記事では、正確かつ安定したシステム時刻を必要とする環境で Windows タイム サービス (W32Time) のサポート範囲を説明します。
- **[高精度のシステムを構成する](configuring-systems-for-high-accuracy.md)します。** Windows 10 および Windows Server 2016 での時刻の同期が大幅に改善されました。  1 ミリ秒 (ミリ秒) を維持するために妥当な条件下でシステムを構成することができます (UTC) に関して以上の精度。
- **[Windows の時間の追跡可能性を](windows-time-for-traceability.md)します。** 多くの分野の規制を UTC にトレース可能システムが必要です。  これは、システムのオフセットは、UTC に対して証明できることを意味します。  Windows 10 およびサーバー 2016年は、規制遵守のシナリオを有効にするには、システム クロックに実行されるアクションの理解を形成するオペレーティング システムの観点から画像を提供する新しいイベント ログを提供します。  これらのイベント ログは Windows タイム サービスの継続的に生成されると、検査または後で分析のためのアーカイブすることができます。
- **[Windows タイム サービスのテクニカル リファレンス](windows-time-service-tech-ref.md)します。** W32Time サービスは、ネットワークの広範な構成を必要としないコンピューターのクロックの同期を提供します。 W32Time サービスは、重要なは、Kerberos V5 認証の成功した操作と、そのためは AD DS ベースの認証です。
    - **[Windows タイム サービスのしくみ](How-the-Windows-Time-Service-Works.md)します。** Windows タイム サービスは、ネットワーク タイム プロトコル (NTP) の正確な実装ではありませんが、ネットワーク全体のコンピューターのクロックが可能な限り正確であることを確認する NTP 仕様で定義されているアルゴリズムの複雑なスイートを使用します。
    - **[Windows タイム サービスのツールと設定](Windows-Time-Service-Tools-and-Settings.md)します。** ほとんどのドメイン メンバー コンピューターがある NT5DS、ドメインの階層からの時間を同期することを意味するのにクライアントの種類。 のみの一般的な例外は、通常は、外部タイム ソースと時刻を同期する構成は、フォレスト ルート ドメインのプライマリ ドメイン コント ローラー (PDC) エミュレーター操作マスターとして機能するドメイン コント ローラーです。


## <a name="related-topics"></a>関連トピック
ドメインの階層とシステムのスコア付けの詳細については、次を参照してください、 ["Windows タイム サービスは何でしょうか。"。](https://blogs.msdn.microsoft.com/w32time/2007/07/07/what-is-windows-time-service/) をご覧ください。

Windows タイム プロバイダー プラグイン モデルは[TechNet に記載されている](https://msdn.microsoft.com/library/windows/desktop/ms725475%28v=vs.85%29.aspx)します。

Windows 2016 の正確性の時間の記事で参照されている補遺がダウンロードできる[ここ](https://windocs.blob.core.windows.net/windocs/WindowsTimeSyncAccuracy_Addendum.pdf)

Windows タイム サービスの簡単な概要については、これを参照してください[概要ビデオ](https://aka.ms/WS2016TimeVideo)します。

<!-- In this guide
In this guide:
Windows Accurate Time
High Accuracy
Support Boundary
Configuration for High Accuracy
Traceability for Compliance
Best Practices
Technical Reference
How the Windows Time Service Works
Windows Time Service Tools and Settings
-->

