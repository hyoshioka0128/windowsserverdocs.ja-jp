---
ms.assetid: e34622ff-b2d0-4f81-8d00-dacd5d6c215e
title: Windows タイム サービス
description: ''
author: shortpatti
ms.author: pashort
manager: brianlic
ms.date: 02/01/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: b997d1f26e8da82e0d595b1ce13763e0a87d6d03
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="windows-time-service-w32time"></a>Windows タイム サービス (W32Time)

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Windows タイム サービス (W32Time) では、Active Directory ドメイン サービス (AD DS) で実行されているすべてのコンピューターの日時を同期します。 時刻の同期は、多くの Windows サービスや基幹業務 (LOB) アプリケーションの通常の操作に重要です。 Windows タイム サービスは、ネットワーク タイム プロトコル (NTP) を使用して、ネットワーク上のコンピューターの時計を同期します。 NTP は、ネットワーク アクセス要求を検証し、リソースを割り当てることが、正確なクロックの値、または、タイムスタンプを確認します。

Windows タイム サービス (W32Time) のトピックでは、次の内容は使用可能です。
- **[Windows 2016 の正確な時刻](accurate-time.md)します。** Windows Server 2016 で時刻の同期の精度は完全な下位古いバージョンの Windows と NTP の互換性を維持しながら、大幅に強化されました。  1 を維持する妥当な動作条件下で ms の正確性に関して、UTC または Windows Server 2016 および Windows 10 Anniversary Update のドメイン メンバーの向上します。
- **[Windows タイム サービスのテクニカル リファレンス](windows-time-service-tech-ref.md)します。** W32Time サービスは、ネットワークの広範な構成なしのコンピューターの時計の同期を提供します。 W32Time サービスは、Kerberos V5 認証の操作が成功して、そのため、AD DS ベースの認証に不可欠です。
    - **[Windows タイム サービスのしくみ](How-the-Windows-Time-Service-Works.md)します。** Windows タイム サービスは、ネットワーク タイム プロトコル (NTP) の正確な実装ではありませんが、ネットワーク全体のコンピューターのクロックが可能な限り正確であることを確認する NTP 仕様で定義されているアルゴリズムの複雑なスイートを使用します。
    - **[Windows タイム サービス ツールと設定](Windows-Time-Service-Tools-and-Settings.md)します。** ほとんどのドメイン メンバー コンピューターでは、タイム クライアント型の NT5DS で、ドメインの階層からの時間を同期することを意味を持ちます。 一般的なだけの例外は、外部のタイム ソースと時刻を同期するように構成は、通常、フォレスト ルート ドメインのプライマリ ドメイン コントローラー (PDC) エミュレーター操作マスターとして機能するドメイン コントローラーです。

## <a name="related-topics"></a>関連するトピック
ドメインの階層とスコア システムに関する詳細については、次を参照してください、["Windows タイム サービスは何ですか?"。](https://blogs.msdn.microsoft.com/w32time/2007/07/07/what-is-windows-time-service/) ブログの投稿します。

Windows タイム プロバイダー プラグイン モデルが[technet「について](https://msdn.microsoft.com/en-us/library/windows/desktop/ms725475%28v=vs.85%29.aspx)します。

Windows 2016 の正確性時刻資料によって参照される補遺をダウンロードできます[次のとおり](http://windocs.blob.core.windows.net/windocs/WindowsTimeSyncAccuracy_Addendum.pdf)

Windows タイム サービスの概要、見てこの[大まかな概要ビデオ](https://aka.ms/WS2016TimeVideo)します。

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

