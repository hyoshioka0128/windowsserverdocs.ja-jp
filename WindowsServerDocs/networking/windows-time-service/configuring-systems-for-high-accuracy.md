---
ms.assetid: ''
title: 高精度のシステムの構成
description: Windows 10 と Windows Server 2016 での時刻の同期が大幅に改善されました。  合理的な運用条件下では、1ミリ秒 (ミリ秒) の精度以上 (UTC に関して) を維持するようにシステムを構成できます。
author: shortpatti
ms.author: dacuo
ms.date: 05/08/2018
ms.topic: article
ms.prod: windows-server
ms.technology: networking
ms.openlocfilehash: b7cd256fdbbdbe7432e5b5d5b16254314132560f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405197"
---
# <a name="configuring-systems-for-high-accuracy"></a>高精度のシステムの構成
>適用対象:Windows Server 2016、Windows 10 バージョン1607以降

Windows 10 と Windows Server 2016 での時刻の同期が大幅に改善されました。  合理的な運用条件下では、1ミリ秒 (ミリ秒) の精度以上 (UTC に関して) を維持するようにシステムを構成できます。

次のガイダンスは、高い精度を実現するようにシステムを構成するのに役立ちます。  この記事では、次の要件について説明します。

- サポートされるオペレーティング システム
- システム構成 

> [!WARNING]
> **以前のオペレーティングシステムの精度の目標**<br>
>Windows Server 2012 R2 以降では、同じ高精度の目標を満たすことができません。 これらのオペレーティングシステムは、高い精度ではサポートされていません。
>
>これらのバージョンでは、Windows タイムサービスは次の要件を満たしています。
>
> - Kerberos version 5 の認証要件を満たすために必要な時間精度が提供されました。
> - 共通の Active Directory フォレストに参加している Windows クライアントおよびサーバーの正確な時間を指定します。
>
>2012 R2 以下の許容範囲が、Windows タイムサービスの設計仕様の範囲を超えています。

## <a name="windows-10-and-windows-server-2016-default-configuration"></a>Windows 10 および Windows Server 2016 の既定の構成

Windows 10 または Windows Server 2016 の1ミリ秒までの精度はサポートされていますが、ほとんどのお客様にとって、非常に正確な時間は必要ありません。

そのため、**既定の構成**は、以前のオペレーティングシステムと同じ要件を満たすことを目的としています。

- Kerberos version 5 の認証要件を満たすために必要な時間の精度を指定します。
- 共通の Active Directory フォレストに参加している Windows クライアントとサーバーの正確な時間を指定します。

## <a name="how-to-configure-systems-for-high-accuracy"></a>システムの精度を高めるためにシステムを構成する方法

>[!IMPORTANT]
>**非常に正確なシステムのサポートに関する注意**<br>
> 時間の精度は、権限のあるタイムソースからエンドデバイスへの正確な時刻のエンドツーエンドの分布を伴います。  このパスに沿って測定値に assymetry を追加すると、精度に悪影響を及ぼすことがあります。これは、デバイスで実現可能な精度に影響します。
>
>このため、高精度のターゲットに対応するためにも満たす必要がある環境要件を概説した[高精度の環境で Windows タイムサービスを構成するためのサポート境界](support-boundary.md)について説明しました。

### <a name="operating-system-requirements"></a>必要なオペレーティング システム

高精度構成には、Windows 10 または Windows Server 2016 が必要です。  タイムトポロジ内のすべての Windows デバイスは、上位の階層の Windows タイムサーバーを含むこの要件を満たしている必要があります。また、仮想化されたシナリオでは、時間の影響を受ける仮想マシンを実行する Hyper-v ホストでなければなりません。 これらのデバイスはすべて、Windows 10 または Windows Server 2016 以降である必要があります。

次に示す図では、高精度を必要とする仮想マシンでは、Windows 10 または Windows Server 2016 が実行されています。  同様に、仮想マシンが存在する Hyper-v ホストと上流の Windows タイムサーバーも Windows Server 2016 を実行する必要があります。

![時間のトポロジ-1607](../media/Windows-Time-Service/Configuring-Systems-for-High-Accuracy/Topology2016.png)


>[!TIP] 
>**Windows のバージョンを確認する**<br>
> コマンドプロンプトでコマンド `winver` を実行すると、OS のバージョンが1607以上であることを確認できます。 OS のビルドは 14393 (またはそれ以降) であることを確認できます。次に例を示します。
>
> ![Winver-2016 1607](../media/Windows-Time-Service/Configuring-Systems-for-High-Accuracy/winver2016.png)

### <a name="system-configuration"></a>システム構成

高精度のターゲットに到達するには、システム構成が必要です。  この構成を実行するには、レジストリやグループポリシーを使用して、さまざまな方法があります。  これらの各設定の詳細については、「Windows タイムサービステクニカルリファレンス– [Windows タイムサービスツール](Windows-Time-Service-Tools-and-Settings.md#windows-time-service-tools)」を参照してください。

#### <a name="windows-time-service-startup-type"></a>Windows タイムサービスのスタートアップの種類

Windows タイムサービス (W32Time) は連続的に実行する必要があります。  これを行うには、Windows タイムサービスのスタートアップの種類を "自動" に構成します。

![自動構成](../media/Windows-Time-Service/Configuring-Systems-for-High-Accuracy/AutomaticService.PNG)

#### <a name="cumulative-one-way-network-latency"></a>累積一方向のネットワーク待機時間

ネットワーク待機時間の増加に応じて、測定の不確実性と "ノイズ" が発生します。  そのため、ネットワーク待機時間が妥当な境界内にあることが不可欠です。  特定の要件は、ターゲットの精度に依存しており、「[高精度環境用に Windows タイムサービスを構成するためのサポート境界](support-boundary.md)」で説明されています。

一方向の累積ネットワーク待機時間の累積を計算するには、時間トポロジ内の NTP クライアントサーバーノードのペア間に個々の一方向の遅延を追加します。これは、ターゲットから始まり、高精度の階層1タイムソースで終了します。

以下に例を示します。非常に正確なソース、2つの中間 NTP サーバー A と B、およびその順序でのターゲットコンピューターを使用したタイム同期階層を考えてみます。 ターゲットとソースの間の累積ネットワーク待機時間を取得するには、次の間隔の個々の NTP ラウンドトリップ時間 (RTTs) を測定します。

- ターゲットとタイムサーバー B
- タイムサーバー B とタイムサーバー A
- タイムサーバー A とソース

この測定値は、受信トレイの w32tm ツールを使用して取得できます。  これを行うには :

1. ターゲットとタイムサーバー B から計算を実行します。
    
    `w32tm /stripchart /computer:TimeServerB /rdtsc /samples:450 > c:\temp\Target_TsB.csv`

2. タイムサーバー b の計算をタイムサーバー a に対して実行します。
    
    `w32tm /stripchart /computer:TimeServerA /rdtsc /samples:450 > c:\temp\Target_TsA.csv`

3. タイムサーバー a からソースに対して計算を実行します。
 
4. 次に、前の手順で測定した average RoundTripDelay を追加し、2で除算して、ターゲットとソース間の累積ネットワーク遅延を取得します。

#### <a name="registry-settings"></a>レジストリの設定

# <a name="minpollintervaltabminpollinterval"></a>[MinPollInterval](#tab/MinPollInterval)
システムポーリングで許容される log2 秒単位の最小間隔を構成します。

|  |  | 
|---------|---------|
|キーの場所     | HKLM:\ SYSTEM\CurrentControlSet\Services\W32Time\Config        |
|設定    | 6        |
|結果 | 最小ポーリング間隔が64秒になりました。 |

次のコマンドは、更新された設定を取得するために Windows タイムを通知します。

`w32tm /config /update`


# <a name="maxpollintervaltabmaxpollinterval"></a>[MaxPollInterval](#tab/MaxPollInterval)
システムポーリングで許容される log2 秒単位の最大間隔を構成します。

|  |  |  
|---------|---------|
|キーの場所     | HKLM:\ SYSTEM\CurrentControlSet\Services\W32Time\Config        |
|設定    | 6        |
|結果 | 最大ポーリング間隔が64秒になりました。  |

次のコマンドは、更新された設定を取得するために Windows タイムを通知します。

`w32tm /config /update`

# <a name="updateintervaltabupdateinterval"></a>[UpdateInterval](#tab/UpdateInterval)
フェーズ修正調整の間のクロックティック数。

|  |  |  
|---------|---------|
|キーの場所     | HKLM:\ SYSTEM\CurrentControlSet\Services\W32Time\Config       |
|設定    | 100        |
|結果 | フェーズ修正調整の間のクロックティック数は、100ティックになりました。 |

次のコマンドは、更新された設定を取得するために Windows タイムを通知します。

`w32tm /config /update`

# <a name="specialpollintervaltabspecialpollinterval"></a>[SpecialPollInterval](#tab/SpecialPollInterval)
特別間隔0x1 フラグが有効になっている場合のポーリング間隔を秒単位で構成します。

|  |  |  
|---------|---------|
|キーの場所     | HKLM:\ SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\NtpClient        |
|設定    | 64        |
|結果 | ポーリング間隔が64秒になりました。 |

次のコマンドを実行すると、Windows タイムを再起動して更新された設定を取得します。

`net stop w32time && net start w32time`

# <a name="frequencycorrectratetabfrequencycorrectrate"></a>[FrequencyCorrectRate](#tab/FrequencyCorrectRate)

|  |  |  
|---------|---------|
|キーの場所     | HKLM:\ SYSTEM\CurrentControlSet\Services\W32Time\Config      |
|設定    | 2        |


---
