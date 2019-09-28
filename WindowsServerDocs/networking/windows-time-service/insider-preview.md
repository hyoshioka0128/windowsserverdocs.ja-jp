---
ms.assetid: ''
title: Windows Server 2019 の Windows タイムサービス機能の Insider preview
description: Windows Server 2019 の新しい Windows タイムサービス機能
author: shortpatti
ms.author: pashort
ms.date: 09/05/2018
ms.topic: article
ms.prod: windows-server
ms.technology: networking
ms.openlocfilehash: 38682afa37a4c6882ee2e63a4abf4cd9fdbd2b27
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405213"
---
# <a name="insider-preview"></a>Insider Preview 


## <a name="leap-second-support"></a>Leap の2番目のサポート


>適用対象:Windows Server 2019 および Windows 10 バージョン1809

うるう秒は、UTC に対して1秒あたりの調整がときどき発生します。 地球の回転速度が低下すると、 [UTC](https://en.wikipedia.org/wiki/Coordinated_Universal_Time) (アトミックなタイムスケール) は[平均太陽時間](https://en.wikipedia.org/wiki/Solar_time#Mean_solar_time)または天文学時間とは異なります。  UTC の分岐が最大で .9 秒に達した時点で、平均太陽時間との間に UTC の同期を維持するために、[閏月](https://en.wikipedia.org/wiki/Leap_second)が挿入されます。

米国と欧州連合の両方で、正確さと追跡可能性に関する規制要件を満たすために、うるう秒が重要になりました。

詳細については、以下をご覧ください。

-  [お知らせのブログ](https://blogs.technet.microsoft.com/networking/2018/07/18/top10-ws2019-hatime/)

-  [開発者](https://aka.ms/Dev-LeapSecond)向けの検証ガイド

-  [IT プロフェッショナル](https://aka.ms/ITPro-LeapSecond)向けの検証ガイド


## <a name="precision-time-protocol"></a>有効桁数のプロトコル

>適用対象:Windows Server 2019 および Windows 10 バージョン1809

Windows Server 2019 および Windows 10 (バージョン 1809) に含まれている新しいタイムプロバイダーを使用すると、有効桁数タイムプロトコル (PTP) を使用して時刻を同期できます。 ネットワークを経由して時間を分散すると、遅延 (待機時間) が発生します。これについて考慮されていない場合、または対称でない場合は、タイムサーバーから送信されたタイムスタンプを理解することがますます困難になります。 ネットワークデバイスは、各ネットワークデバイスによって導入された待機時間をタイミング測定に追加することで、windows クライアントに対してより正確なタイムサンプルを提供します。

詳細については、以下をご覧ください。

-  [お知らせのブログ](https://blogs.technet.microsoft.com/networking/2018/07/18/top10-ws2019-hatime/)

-  [IT プロフェッショナル](https://aka.ms/PTPValidation)向けの検証ガイド


## <a name="software-timestamping"></a>ソフトウェアタイムスタンプ

>適用対象:Windows Server 2019 および Windows 10 バージョン1809

タイムサーバーからネットワーク経由でタイミングのパケットを受信する場合は、タイムサービスで使用される前に、オペレーティングシステムのネットワークスタックによって処理される必要があります。 ネットワークスタック内の各コンポーネントには、タイミング測定の精度に影響を与える変動した待機時間が導入されています。

![ソフトウェアタイムスタンプ](../media/Windows-Time-Service/software-timestamping.png)

この問題に対処するために、ソフトウェアタイムスタンプを使用すると、上に示した "Windows ネットワークコンポーネント" の前後に、オペレーティングシステムの遅延を考慮してパケットのタイムスタンプを行うことができます。

詳細については、以下をご覧ください。

-  [お知らせのブログ](https://blogs.technet.microsoft.com/networking/2018/07/18/top10-ws2019-hatime/)

-  [IT プロフェッショナル](https://github.com/Microsoft/SDN/blob/master/FeatureGuide/Validation%20Guide%20-%20RS5%20-%20Software%20Timestamping.docx)向けの検証ガイド



---