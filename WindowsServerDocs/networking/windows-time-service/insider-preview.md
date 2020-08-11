---
title: Windows Server 2019 の Windows タイム サービス機能に関する Insider Preview
description: Windows Server 2019 の Windows タイム サービスの新機能
author: dcuomo
ms.author: dacuo
ms.date: 06/06/2020
ms.topic: article
ms.openlocfilehash: 6a07290efff6d36f58a75c409eb9f50284218bd1
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87953888"
---
# <a name="insider-preview"></a>Insider Preview


## <a name="leap-second-support"></a>うるう秒のサポート

> 適用先:Windows Server 2019 および Windows 10 バージョン 1809

うるう秒は、UTC に対する 1 秒間の臨時の調整です。 地球の自転が遅くなるにつれて、[UTC](https://en.wikipedia.org/wiki/Coordinated_Universal_Time) (アトミック タイムスケール) は、[平均太陽時](https://en.wikipedia.org/wiki/Solar_time#Mean_solar_time) または天文時からずれていきます。 UTC のずれが最大 .9 秒に達した時点で、UTC と平均太陽時との間の同期を維持するために[うるう秒](https://en.wikipedia.org/wiki/Leap_second)が挿入されます。

うるう秒は、米国と欧州連合の両方で、正確さと追跡可能性に関する規制要件を満たすために重要になっています。

詳細については、次のドキュメントを参照してください。

- 当社の[発表に関するブログ](https://techcommunity.microsoft.com/t5/networking-blog/top-10-networking-features-in-windows-server-2019-10-accurate/ba-p/339739/)

- [開発者向け](https://aka.ms/Dev-LeapSecond)の検証ガイド

- [IT プロ向け](https://aka.ms/ITPro-LeapSecond)の検証ガイド


## <a name="precision-time-protocol"></a>精度タイム プロトコル

> 適用先:Windows Server 2019 および Windows 10 バージョン 1809

Windows Server 2019 と Windows 10 (バージョン 1809) に含まれている新しいタイム プロバイダーでは、精度タイム プロトコル (PTP) を使用して時刻を同期できます。 ネットワークを経由して時間を分散すると、遅延 (待機時間) が発生します。これが考慮されない場合、または対称でない場合は、タイム サーバーから送信されたタイムスタンプを理解することがますます困難になります。 PTP によって、ネットワーク デバイスは、各ネットワーク デバイスによって導入された待機時間をタイミング測定に追加することで、Windows クライアントに対してより正確なタイム サンプルを提供できます。

詳細については、次のドキュメントを参照してください。

- 当社の[発表に関するブログ](https://techcommunity.microsoft.com/t5/networking-blog/top-10-networking-features-in-windows-server-2019-10-accurate/ba-p/339739/)

- [IT プロ向け](https://aka.ms/PTPValidation)の検証ガイド


## <a name="software-timestamping"></a>ソフトウェアのタイムスタンプ

> 適用先:Windows Server 2019 および Windows 10 バージョン 1809

タイム サーバーからネットワーク経由でタイミング パケットを受信する場合は、タイム サービスで使用される前に、オペレーティング システムのネットワーク スタックによって処理される必要があります。 ネットワーク スタック内の各コンポーネントによって、タイミング測定の精度に影響を与える不定量の待機時間が導入されます。

![ソフトウェアのタイムスタンプ](../media/Windows-Time-Service/software-timestamping.png)

この問題に対処するために、ソフトウェアのタイムスタンプでは、上記の "Windows ネットワーク コンポーネント" の前後に、オペレーティング システムの遅延を考慮してパケットにタイムスタンプを設定できます。

詳細については、次のドキュメントを参照してください。

- 当社の[発表に関するブログ](https://techcommunity.microsoft.com/t5/networking-blog/top-10-networking-features-in-windows-server-2019-10-accurate/ba-p/339739/)

- [開発者および IT プロフェッショナル向けの検証ガイド](https://github.com/microsoft/W32Time/tree/master/Leap%20Seconds)


---
