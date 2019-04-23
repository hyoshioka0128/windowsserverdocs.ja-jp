---
ms.assetid: ''
title: Windows Server 2019 の Windows タイム サービスの機能の insider preview
description: Windows Server 2019 Windows タイム サービスの新機能
author: shortpatti
ms.author: pashort
ms.date: 09/05/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: networking
ms.openlocfilehash: ef0ff317f5957add5ecbe9f88ef83753b805ec41
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829023"
---
# <a name="insider-preview"></a>Insider Preview 


## <a name="leap-second-support"></a>うるう秒のサポート


>適用対象:Windows Server 2019 および Windows 10、バージョンは 1809

うるう秒は、UTC への不定期の 1 秒あたりの調整です。 地球の回転速度の低下と[UTC](https://en.wikipedia.org/wiki/Coordinated_Universal_Time) (アトミック タイム スケールする) ブロックから分化[ほど時間が太陽](https://en.wikipedia.org/wiki/Solar_time#Mean_solar_time)または、天文学の時間。  UTC 多くて.9 秒間で相違するいると、[うるう秒](https://en.wikipedia.org/wiki/Leap_second)UTC との同期を平均太陽時間の保持に挿入されます。

うるう秒は、精度と米国と欧州連合の両方で、追跡可能性規制要件を満たすために重要になります。

詳しくは、次のトピックをご覧ください。

-  この[の発表に関するブログ](https://blogs.technet.microsoft.com/networking/2018/07/18/top10-ws2019-hatime/)

-  検証のためのガイド、[開発者](https://aka.ms/Dev-LeapSecond)

-  検証のためのガイド、 [IT Pro](https://aka.ms/ITPro-LeapSecond)


## <a name="precision-time-protocol"></a>有効桁数タイム プロトコル

>適用対象:Windows Server 2019 および Windows 10、バージョンは 1809

Windows Server 2019 および Windows 10 (バージョンは 1809) に含まれる新しいタイム プロバイダーを使用すると、有効桁数タイム プロトコル (PTP) を使用して時刻を同期できます。 わけでは、遅延 (遅延) に到達した時刻をネットワーク経由で配布するように、または対称されていない場合は難しく、時間のサーバーから送信されたタイムスタンプを理解します。 PTP は、タイミング測定値を windows クライアントをより正確なタイム サンプルを提供するために、各ネットワーク デバイスで導入された待機時間を追加するネットワーク デバイスを使用できます。

詳しくは、次のトピックをご覧ください。

-  この[の発表に関するブログ](https://blogs.technet.microsoft.com/networking/2018/07/18/top10-ws2019-hatime/)

-  検証のためのガイド、 [IT Pro](https://aka.ms/PTPValidation)


## <a name="software-timestamping"></a>ソフトウェアのタイムスタンプ

>適用対象:Windows Server 2019 および Windows 10、バージョンは 1809

タイム サーバーからネットワーク経由でタイミングのパケットを受信するときに、ことで、タイム サービスで使用される前に、オペレーティング システムのネットワーク スタックによってに処理されなければなりません。 ネットワーク スタック内の各コンポーネントには、タイミング測定値の精度に影響を与える待機時間の量が導入されています。

![ソフトウェアのタイムスタンプ](../media/Windows-Time-Service/software-timestamping.png)

この問題に対処するには、ソフトウェア タイムスタンプにより、タイムスタンプ パケットに、"Windows Networking Components"オペレーティング システムに遅延を考慮する前に示したの前後にできます。

詳しくは、次のトピックをご覧ください。

-  この[の発表に関するブログ](https://blogs.technet.microsoft.com/networking/2018/07/18/top10-ws2019-hatime/)

-  検証のためのガイド、 [IT Pro](https://github.com/Microsoft/SDN/blob/master/FeatureGuide/Validation%20Guide%20-%20RS5%20-%20Software%20Timestamping.docx)



---