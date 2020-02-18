---
ms.assetid: ''
title: 高精度を確保するためのシステム構成
description: Windows 10 と Windows Server 2016 での時刻の同期が大幅に改善されました。  適切な運用条件下では、(UTC に関しては) 1 ms (ミリ秒) 以上の精度を維持するようにシステムを構成できます。
author: shortpatti
ms.author: dacuo
ms.date: 05/08/2018
ms.topic: article
ms.prod: windows-server
ms.technology: networking
ms.openlocfilehash: b7cd256fdbbdbe7432e5b5d5b16254314132560f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405197"
---
# <a name="configuring-systems-for-high-accuracy"></a>高精度を確保するためのシステム構成
>適用先:Windows Server 2016、および Windows 10 バージョン 1607 以降

Windows 10 と Windows Server 2016 での時刻の同期が大幅に改善されました。  適切な運用条件下では、(UTC に関しては) 1 ms (ミリ秒) 以上の精度を維持するようにシステムを構成できます。

高い精度を確保するようにシステムを構成するうえで、次のガイダンスが役立ちます。  この記事では、次の要件について説明します。

- サポートされるオペレーティング システム
- システム構成 

> [!WARNING]
> **以前のオペレーティング システムの精度の目標**<br>
>Windows Server 2012 R2 以前では、同じ高精度の目標を達成することができません。 これらのオペレーティング システムは、高精度には対応していません。
>
>これらのバージョンでは、Windows タイム サービスは次の要件を満たしています。
>
> - Kerberos バージョン 5 の認証要件を満たすために必要な時刻の精度を提供した。
> - 共通の Active Directory フォレストに参加している Windows のクライアントとサーバーに、ある程度の正確な時刻を提供した。
>
>2012 R2 以前の許容誤差はより大きく、Windows タイム サービスの設計仕様の範囲を超えています。

## <a name="windows-10-and-windows-server-2016-default-configuration"></a>Windows 10 と Windows Server 2016 の既定の構成

Windows 10 や Windows Server 2016 では最大で 1ms の精度を確保していますが、ほとんどのお客様には、そこまで高い精度の時刻は求められていません。

そのため、**既定の構成** は、以前のオペレーティング システムと同じ次の要件を満たすことを目的としています。

- Kerberos バージョン 5 の認証要件を満たすために必要な時刻の精度を提供する。
- 共通の Active Directory フォレストに参加している Windows のクライアントとサーバーに、ある程度の正確な時刻を提供する。

## <a name="how-to-configure-systems-for-high-accuracy"></a>高精度を確保するためのシステム構成方法

>[!IMPORTANT]
>**高精度のシステムのサポートの可否に関する注意**<br>
> 時刻の精度を確保することにより、権限のあるタイム ソースからエンド デバイスへ、エンドツーエンドでの正確な時刻の配信が可能になります。  この経路の中で測定値にひずみを起こさせる要素があると、精度に悪影響を及ぼすことがあり、デバイスで実現できる精度に影響します。
>
>このため、Microsoft では[高精度の環境に向けた Windows タイム サービスの構成を目的とするサポート範囲](support-boundary.md)について文書化し、高精度の目標を達成するために満たす必要がある環境要件について説明しています。

### <a name="operating-system-requirements"></a>オペレーティング システムの要件

高精度の構成には、Windows 10 または Windows Server 2016 が必要です。  タイム トポロジ内のすべての Windows デバイスはこの要件を満たす必要があります。これには、より高い階層の Windows タイム サーバーのほか、仮想化されたシナリオでは時刻に依存する仮想マシンを実行する Hyper-V ホストが含まれます。 これらのデバイスはすべて、Windows 10 または Windows Server 2016 以降である必要があります。

次に示す図では、高精度を必要とする仮想マシンで、Windows 10 または Windows Server 2016 が実行されています。  同様に、仮想マシンが存在する Hyper-V ホストと上流の Windows タイムサーバーも Windows Server 2016 を実行する必要があります。

![タイム トポロジ - 1607](../media/Windows-Time-Service/Configuring-Systems-for-High-Accuracy/Topology2016.png)


>[!TIP] 
>**Windows バージョンの特定**<br>
> コマンド プロンプトでコマンド `winver` を実行すると、以下に示すように OS のバージョンが 1607 (またはそれ以降) で、OS のビルドが 14393 (またはそれ以降) であることを確認できます。
>
> ![Winver - 2016 1607](../media/Windows-Time-Service/Configuring-Systems-for-High-Accuracy/winver2016.png)

### <a name="system-configuration"></a>システム構成

ターゲットとする高精度を実現するには、システムの構成が必要です。  この構成を実行する方法としては、レジストリで直接実行する、グループ ポリシーを通じて実行するなど、さまざまな方法があります。  これらの各設定の詳細については、Windows タイム サービスのテクニカル リファレンスの「[Windows タイム サービス ツール](Windows-Time-Service-Tools-and-Settings.md#windows-time-service-tools)」を参照してください。

#### <a name="windows-time-service-startup-type"></a>Windows タイム サービスのスタートアップの種類

Windows タイム サービス (W32Time) は連続的に実行する必要があります。  これを行うには、Windows タイム サービスのスタートアップの種類を "自動" に構成します。

![自動構成](../media/Windows-Time-Service/Configuring-Systems-for-High-Accuracy/AutomaticService.PNG)

#### <a name="cumulative-one-way-network-latency"></a>一方向の累積ネットワーク待機時間

ネットワーク待機時間が増加すると、測定の不確実性と "ノイズ" が発生する可能性が高まります。  そのため、ネットワーク待機時間が妥当な境界内にあることが不可欠です。  具体的な要件は、ターゲットとする精度によって異なります。詳細については、[高精度の環境に向けた Windows タイム サービスの構成を目的とするサポート範囲](support-boundary.md)に関するページを参照してください。

一方向の累積ネットワーク待機時間を計算するには、ターゲットから始まり、高精度の階層 1 のタイム ソースで終了する、時間トポロジ内の NTP クライアント-サーバー ノードのペア間の個々の一方向の遅延を追加します。

たとえば、次のように入力します。1 つの精度の高いソース、2 つの中間 NTP サーバー A と B、ターゲット マシンの順番に並んでいる時刻同期階層を考えてみます。 ターゲットとソースの間の累積ネットワーク待機時間を取得するには、次の間隔の個々の NTP のラウンドトリップ時間 (RTT) の平均を測定します。

- ターゲットとタイム サーバー B
- タイム サーバー B とタイム サーバー A
- タイム サーバー A とソース

この測定値は、インボックスの w32tm.exe ツールを使用して取得できます。  そのためには、次の手順に従います。

1. ターゲットとタイムサーバー B から計算を実行します。
    
    `w32tm /stripchart /computer:TimeServerB /rdtsc /samples:450 > c:\temp\Target_TsB.csv`

2. タイム サーバー B からタイム サーバー A に対して計算を実行します。
    
    `w32tm /stripchart /computer:TimeServerA /rdtsc /samples:450 > c:\temp\Target_TsA.csv`

3. タイム サーバー A からソースに対して計算を実行します。
 
4. 次に、前の手順で測定した RoundTripDelay の平均を追加し、2 で除算して、ターゲットとソース間の累積ネットワーク遅延を取得します。

#### <a name="registry-settings"></a>レジストリの設定

# <a name="minpollintervaltabminpollinterval"></a>[MinPollInterval](#tab/MinPollInterval)
システムのポーリングとして許容される最小間隔を log2 秒単位で構成します。

|  |  | 
|---------|---------|
|キーの場所     | HKLM:\SYSTEM\CurrentControlSet\Services\W32Time\Config        |
|設定    | 6        |
|成果 | 最小ポーリング間隔が 64 秒になりました。 |

次のコマンドは、更新された設定を取得するよう、Windows タイムに通知します。

`w32tm /config /update`


# <a name="maxpollintervaltabmaxpollinterval"></a>[MaxPollInterval](#tab/MaxPollInterval)
システムのポーリングとして許容される最大間隔を log2 秒単位で構成します。

|  |  |  
|---------|---------|
|キーの場所     | HKLM:\SYSTEM\CurrentControlSet\Services\W32Time\Config        |
|設定    | 6        |
|成果 | 最大ポーリング間隔が 64 秒になりました。  |

次のコマンドは、更新された設定を取得するよう、Windows タイムに通知します。

`w32tm /config /update`

# <a name="updateintervaltabupdateinterval"></a>[UpdateInterval](#tab/UpdateInterval)
フェーズ修正の調整間のクロック ティック数。

|  |  |  
|---------|---------|
|キーの場所     | HKLM:\SYSTEM\CurrentControlSet\Services\W32Time\Config       |
|設定    | 100        |
|成果 | フェーズ修正の調整間のクロック ティック数が 100 になりました。 |

次のコマンドは、更新された設定を取得するよう、Windows タイムに通知します。

`w32tm /config /update`

# <a name="specialpollintervaltabspecialpollinterval"></a>[SpecialPollInterval](#tab/SpecialPollInterval)
SpecialInterval 0x1 フラグが有効になっているときのポーリング間隔を秒単位で構成します。

|  |  |  
|---------|---------|
|キーの場所     | HKLM:\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\NtpClient        |
|設定    | 64        |
|成果 | ポーリング間隔が 64 秒になりました。 |

次のコマンドは、更新された設定を取得するために、Windows タイムを再起動します。

`net stop w32time && net start w32time`

# <a name="frequencycorrectratetabfrequencycorrectrate"></a>[FrequencyCorrectRate](#tab/FrequencyCorrectRate)

|  |  |  
|---------|---------|
|キーの場所     | HKLM:\SYSTEM\CurrentControlSet\Services\W32Time\Config      |
|設定    | 2 で保護されたプロセスとして起動されました        |


---
