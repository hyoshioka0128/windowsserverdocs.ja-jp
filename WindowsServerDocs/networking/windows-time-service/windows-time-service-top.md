---
ms.assetid: e34622ff-b2d0-4f81-8d00-dacd5d6c215e
title: Windows タイム サービス
description: ''
author: shortpatti
ms.author: pashort
manager: dougkim
ms.date: 05/08/2018
ms.topic: article
ms.prod: windows-server
ms.technology: networking
ms.openlocfilehash: e3dbaa188426ac81073e706db3adc6ab0a655c01
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405190"
---
# <a name="windows-time-service-w32time"></a>Windows タイムサービス (W32Time)

>適用対象:Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows 10 以降

Windows タイムサービス (W32Time) は、Active Directory Domain Services (AD DS) で実行されているすべてのコンピューターの日付と時刻を同期します。 多くの Windows サービスと基幹業務 (LOB) アプリケーションを適切に動作させるには、時刻の同期が不可欠です。 Windows タイムサービスは、ネットワークタイムプロトコル (NTP) を使用して、ネットワーク上のコンピューターの時計を同期します。 NTP を使用すると、正確なクロック値 (タイムスタンプ) をネットワーク検証およびリソースアクセス要求に割り当てることができます。

Windows タイムサービス (W32Time) のトピックでは、次の内容を利用できます。
- **[Windows Server 2016 の正確な時刻](accurate-time.md)。** Windows Server 2016 での同期精度が大幅に向上し、以前のバージョンの Windows との NTP の完全な互換性が維持されています。 合理的な運用条件下では、Windows Server 2016 および Windows 10 記念日更新ドメインのメンバーに対して、UTC またはそれ以上の精度で1ミリ秒の精度を維持できます。
- **[高精度の環境のサポート境界](support-boundary.md)。** この記事では、非常に正確で安定したシステム時刻を必要とする環境での Windows タイムサービス (W32Time) のサポート境界について説明します。
- **[システムの精度を高めるための構成](configuring-systems-for-high-accuracy.md)。** Windows 10 と Windows Server 2016 での時刻の同期が大幅に改善されました。  合理的な運用条件下では、1ミリ秒 (ミリ秒) の精度以上 (UTC に関して) を維持するようにシステムを構成できます。
- **[追跡可能性のための Windows タイム](windows-time-for-traceability.md)。** 多くの部門では、システムが UTC に対して追跡可能である必要があります。  これは、システムのオフセットを UTC に対して証明できることを意味します。  規制遵守シナリオを有効にするために、Windows 10 およびサーバー2016では、オペレーティングシステムの観点から画像を提供してシステムクロックで実行されるアクションを理解するための新しいイベントログを提供しています。  これらのイベントログは、Windows タイムサービスに対して継続的に生成され、後で分析するために調査またはアーカイブできます。
- **[Windows タイムサービスのテクニカルリファレンス](windows-time-service-tech-ref.md)。** W32Time サービスを使用すると、広範な構成を必要とせずに、コンピューターのネットワーククロック同期を行うことができます。 W32Time サービスは、Kerberos V5 認証を正常に動作させるために不可欠であり、したがって AD DS ベースの認証に必要です。
    - **[Windows タイムサービスの動作について説明](How-the-Windows-Time-Service-Works.md)します。** Windows タイム サービスは、ネットワーク タイム プロトコル (NTP) の正確な実装ではありませんが、ネットワーク全体のコンピューターのクロックが可能な限り正確であることを確認する NTP 仕様で定義されているアルゴリズムの複雑なスイートを使用します。
    - **[Windows タイムサービスのツールと設定](Windows-Time-Service-Tools-and-Settings.md)** ほとんどのドメインメンバーコンピューターには、time クライアントタイプの NT5DS があります。これは、ドメイン階層から時刻を同期することを意味します。 この唯一の一般的な例外は、フォレストルートドメインのプライマリドメインコントローラー (PDC) エミュレーター操作マスタとして機能するドメインコントローラーです。これは通常、時間を外部タイムソースと同期するように構成されています。


## <a name="related-topics"></a>関連トピック
ドメイン階層とスコアリングシステムの詳細については、「 [Windows タイムサービスとは](https://blogs.msdn.microsoft.com/w32time/2007/07/07/what-is-windows-time-service/)」を参照してください。 をご覧ください。

Windows タイムプロバイダプラグインモデルは[TechNet に記載](https://msdn.microsoft.com/library/windows/desktop/ms725475%28v=vs.85%29.aspx)されています。

Windows 2016 の正確な時刻に関する記事で言及されている補遺は[ここ](https://windocs.blob.core.windows.net/windocs/WindowsTimeSyncAccuracy_Addendum.pdf)からダウンロードできます

Windows タイムサービスの簡単な概要については、この[概要ビデオ](https://aka.ms/WS2016TimeVideo)をご覧ください。
