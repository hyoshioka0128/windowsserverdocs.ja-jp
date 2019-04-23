---
author: shortpatti
ms.author: pashort
ms.date: 10/02/2018
ms.prod: windows-server-threshold
ms:topic: include
ms.openlocfilehash: 4e8e3234b89630bf16148eef644f0c6607ad38bd
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852343"
---
## <a name="importance-of-time-protocols"></a>時間プロトコルの重要性
時間プロトコルは、時間の情報を交換し、その情報を使用して、クロックの同期を 2 台のコンピューター間で通信します。 Windows タイム サービス時間プロトコルでは、クライアントは、サーバーから時刻の情報を要求し、受信する情報に基づいて、そのクロックを同期します。
  
Windows タイム サービスは、NTP を使用して、ネットワーク経由で時刻を同期します。 NTP は、時計を同期させるために必要な作業分野のアルゴリズムを含むインターネット時刻プロトコルです。 NTP がより正確なタイム プロトコルよりも、単純なネットワーク タイム プロトコル (SNTP) Windows; の一部のバージョンで使用されています。ただし、W32Time は、Windows 2000 などの SNTP ベースのタイム サービスを実行しているコンピューターとの下位互換性を有効にする SNTP をサポートするためには続行されます。

これは、さまざまな理由が正確な時刻をする必要があります。  Windows の一般的には、Kerberos クライアントとサーバー間の精度が 5 分必要があります。  ただし、これには時間精度を含めることによって影響を受けることができます、他の多くの領域があります。


- 政府の規制は次のようです。
    - 米国で FINRA の精度が 50 ミリ秒
    - 1 ミリ秒 ESMA (MiFID II)、EU 内に存在します。
- 暗号化アルゴリズム
- クラスター/Sql/exchange、およびドキュメント Db のような分散システム
- トランザクションのビットコイン ブロック チェーン フレームワーク
- 分散ログと脅威の分析 
- AD レプリケーション
- PCI (Payment Card Industry)、現在 1 の 2 つ目の精度