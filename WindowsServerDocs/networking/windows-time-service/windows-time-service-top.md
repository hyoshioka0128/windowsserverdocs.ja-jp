---
ms.assetid: e34622ff-b2d0-4f81-8d00-dacd5d6c215e
title: Windows タイム サービス (W32Time)
author: dcuomo
ms.author: dacuo
manager: dougkim
ms.date: 05/08/2018
ms.topic: article
ms.openlocfilehash: 2bd28bc9e774ebdd30c81397bfe3a3bb6320a679
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87997390"
---
# <a name="windows-time-service-w32time"></a>Windows タイム サービス (W32Time)

>適用先:Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows 10 以降

Windows タイム サービス (W32Time) では、Active Directory Domain Services (AD DS) で実行されているすべてのコンピューターの日付と時刻の同期が行われます。 時刻の同期は、多くの Windows サービスと基幹業務 (LOB) アプリケーションを適切に操作するために不可欠です。 Windows タイム サービスでは、ネットワーク タイム プロトコル (NTP) を使用して、ネットワーク上のコンピューターを同期します。 NTP によって、正確なクロック値 (タイムスタンプ) がネットワークの検証とリソースのアクセス要求に確実に割り当てられます。

Windows タイム サービス (W32Time) のトピックで、次の内容を確認できます。
- **[Windows Server 2016 の正確な時刻](accurate-time.md)。** Windows Server 2016 での同期の精度が大幅に向上しました。以前の Windows バージョンとの NTP の完全な後方互換性は維持されています。 妥当な運用条件下では、Windows Server 2016 と Windows 10 Anniversary Update ドメインのメンバーには、UTC に関して 1 ミリ秒またはそれ以上の精度を維持できます。
- **[高精度環境の時間のサポート範囲](support-boundary.md)。** この記事では、高精度かつ安定したシステム時刻を必要とする環境での Windows タイム サービス (W32Time) のサポート範囲について説明します。
- **[高精度を確保するためのシステム構成](configuring-systems-for-high-accuracy.md)。** Windows 10 と Windows Server 2016 での時刻の同期が大幅に向上しています。  妥当な運用条件下では、(UTC に関して) 1 ms (ミリ秒) 以上の精度を維持するようにシステムを構成できます。
- **[追跡可能性のための Windows タイム](windows-time-for-traceability.md)。** さまざまな部門の規制により、システムが UTC に対して追跡可能であることが要求されます。  これは、システムのオフセットを UTC に関して証明できることを意味します。  規制遵守シナリオを有効にするために、Windows 10 と Server 2016 には、オペレーティング システム側から見た場合の状況を提供して、システム クロック上で実行された操作を理解するための新しいイベント ログが用意されています。  これらのイベント ログは、Windows タイム サービス用に継続的に生成され、調査したり、後で分析するためにアーカイブしたりできます。
- **[Windows タイム サービスのテクニカル リファレンス](windows-time-service-tech-ref.md)。** W32Time サービスを使用すると、広範な構成を必要とせずに、コンピューターのネットワーク クロック同期を行うことができます。 W32Time サービスは Kerberos V5 認証が正常に動作するために必須の機能であるため、AD DS ベースの認証にも必須です。
    - **[Windows タイム サービスのしくみ](How-the-Windows-Time-Service-Works.md)。** Windows タイム サービスは、ネットワーク タイム プロトコル (NTP) の正確な実装ではありませんが、ネットワーク全体のコンピューターのクロックが可能な限り正確であることを確認する NTP 仕様で定義されているアルゴリズムの複雑なスイートを使用します。
    - **[Windows タイム サービスのツールと設定](Windows-Time-Service-Tools-and-Settings.md)。** ほとんどのドメイン メンバー コンピューターのタイム クライアントの種類は NT5DS です。これは、ドメイン階層から時刻が同期されることを意味します。 この唯一の例外としての典型例は、フォレスト ルート ドメインのプライマリ ドメイン コントローラ (PDC) エミュレーター操作マスタとして機能するドメイン コントローラーです。これは通常、外部のタイム ソースを使用して時間を同期するように構成されています。


## <a name="related-topics"></a>関連トピック
ドメイン階層とスコアリング システムの詳細については、[Windows タイム サービスの概要](/archive/blogs/w32time/what-is-windows-time-service)に関する記事 をご覧ください。

Windows タイム プロバイダー プラグイン モデルについては、[TechNet に記載されています](/windows/win32/sysinfo/time-provider)。

Windows 2016 の正確な時刻の記事で参照されている補遺は、[こちらから](https://windocs.blob.core.windows.net/windocs/WindowsTimeSyncAccuracy_Addendum.pdf)ダウンロードできます。

Windows タイム サービスの概要については、こちらの[概要ビデオ](https://aka.ms/WS2016TimeVideo)をご覧ください。