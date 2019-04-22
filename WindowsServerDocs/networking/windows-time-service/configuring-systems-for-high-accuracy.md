---
ms.assetid: ''
title: 高精度のシステムの構成
description: Windows 10 および Windows Server 2016 での時刻の同期が大幅に改善されました。  1 ミリ秒 (ミリ秒) を維持するために妥当な条件下でシステムを構成することができます (UTC) に関して以上の精度。
author: shortpatti
ms.author: dacuo
ms.date: 05/08/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: networking
ms.openlocfilehash: d872252180d49bd41a91e9a8eaf516b834ed242a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814673"
---
# <a name="configuring-systems-for-high-accuracy"></a>高精度のシステムの構成
>適用対象:Windows Server 2016、および Windows 10 バージョン 1607 以降

Windows 10 および Windows Server 2016 での時刻の同期が大幅に改善されました。  1 ミリ秒 (ミリ秒) を維持するために妥当な条件下でシステムを構成することができます (UTC) に関して以上の精度。

次のガイダンスを高い精度を実現するために、システムを構成できます。  この記事では、次の要件について説明します。

- サポートされるオペレーティング システム
- システム構成 

> [!WARNING]
> **以前のオペレーティング システムの正確性の目標**<br>
>Windows Server 2012 R2 と以下同じ高精度の目標を満たしていないことができます。 高精度では、これらのオペレーティング システムはサポートされていません。
>
>これらのバージョンでは、Windows タイム サービスには、次の要件が満たされています。
>
> - Kerberos version 5 認証要件を満たすために必要な時刻の精度を提供します。
> - Windows クライアントおよび一般的な Active Directory フォレストに参加しているサーバーの疎に正確な時刻を提供します。
>
>2012 R2 での上下に大きい値の許容範囲は、Windows タイム サービスの設計仕様外です。

## <a name="windows-10-and-windows-server-2016-default-configuration"></a>Windows 10 および Windows Server 2016 既定の構成

Windows 10 または Windows Server 2016 で最大 1 ミリ秒の精度がサポートされます、中に顧客の大半は正確な時間は必要ありません。

そのため、**既定の構成**が以前のオペレーティング システムと同じ要件を満たすものでは。

- Kerberos version 5 認証要件を満たすために必要な時刻の精度を提供します。
- Windows クライアントおよび一般的な Active Directory フォレストに参加しているサーバーには、疎正確な時刻を提供します。

## <a name="how-to-configure-systems-for-high-accuracy"></a>高精度のシステムを構成する方法

>[!IMPORTANT]
>**正確なシステムのサポートに関するメモ**<br>
> 時刻の精度の正確な時刻のエンド ツー エンドの配布を信頼できるタイム ソースからエンド デバイスにする必要があります。  デバイスで達成可能な精度 assymetry このパスに沿って測定では精度の影響を与える悪影響を追加するものに影響します。
>
>このため、私たちが記載されている、[高精度の環境の Windows タイム サービスを構成するサポート境界](support-boundary.md)も高精度の目標に到達するを満たす必要がある環境の要件のアウトラインを表示します。

### <a name="operating-system-requirements"></a>必要なオペレーティング システム

高精度の構成では、Windows 10 または Windows Server 2016 が必要です。  時間トポロジ内のすべての Windows デバイスでは、上位の階層 Windows タイム サーバーを含むこの要件を満たす必要があり、仮想化シナリオでは、時間を区別する仮想マシンを実行する HYPER-V ホストします。 以上である必要がありますすべてこれらのデバイスの Windows 10 または Windows Server 2016。

以下の図で高精度を必要とする仮想マシンは Windows 10 または Windows Server 2016 を実行しています。  同様に、仮想マシンが存在する HYPER-V ホストと上流の Windows タイム サーバーする必要がありますも Windows Server 2016 を実行します。

![時間トポロジ - 1607](../media/Windows-Time-Service/Configuring-Systems-for-High-Accuracy/Topology2016.png)


>[!TIP] 
>**Windows のバージョンを確認します。**<br>
> コマンドを実行する`winver`OS を確認するコマンド プロンプト バージョン 1607 (またはそれ以降)、OS ビルド 14393 (またはそれ以降) の下に示すように。
>
> ![Winver - 2016 1607](../media/Windows-Time-Service/Configuring-Systems-for-High-Accuracy/winver2016.png)

### <a name="system-configuration"></a>システム構成

高精度のターゲットに達すると、システム構成が必要です。  さまざまなレジストリに直接またはグループ ポリシーを含め、この構成を実行する方法があります。  これらの各設定の詳細については Windows タイム サービスのテクニカル リファレンス – であります[Windows タイム サービス ツール](Windows-Time-Service-Tools-and-Settings.md#windows-time-service-tools)します。

#### <a name="windows-time-service-startup-type"></a>Windows タイム サービスのスタートアップの種類

Windows タイム サービス (W32Time) は、継続的に実行する必要があります。  これを行うには、Windows タイム サービスのスタートアップの種類を '自動' 開始を構成します。

![自動構成](../media/Windows-Time-Service/Configuring-Systems-for-High-Accuracy/AutomaticService.PNG)

#### <a name="cumulative-one-way-network-latency"></a>累積的な一方向のネットワーク待機時間

測定値の不確実性と「ノイズ」忍び寄ってくるネットワーク待機時間が増加します。  そのため、ネットワーク待機時間が妥当な境界内に存在する命令型です。  特定の要件が、ターゲットの精度に依存するために記載されて、[高精度の環境の Windows タイム サービスを構成するサポート境界](support-boundary.md)記事。

累積的な一方向のネットワーク待機時間を計算するには、トポロジでは、時間、ターゲットで開始および終了高精度 stratum 1 タイム ソースの NTP クライアント サーバーのノード ペア間の個々 の一方向遅延を追加します。

例:正確なソース、2 つの中間的な NTP サーバー A、B、およびその順序でターゲット コンピューターでの時間同期階層を検討してください。 ターゲットとソース間の累積的なネットワーク待機時間を取得するには、個々 の NTP ラウンド トリップ間 (Rtt) の時間の平均を測定します。

- ターゲットと時間のサーバー B
- タイム サーバー B とタイム サーバー A
- タイム サーバー A とソース

この測定値は、受信トレイ w32tm.exe ツールを使用して取得できます。  これには、次の手順を実行します。
<!-- Use PowerShell to import the CSV then average the RTT Column -->

1. ターゲットと時間のサーバー B からの計算します。
    
    `w32tm /stripchart /computer:TimeServerB /rdtsc /samples:450 > c:\temp\Target_TsB.csv`

2. (で示される) に対してサーバー b の時刻から計算を実行時のサーバーをします。
    
    `w32tm /stripchart /computer:TimeServerA /rdtsc /samples:450 > c:\temp\Target_TsA.csv`

3. タイム サーバーから、計算を実行するソースに対して。
 
4. 次に、前の手順で測定された平均 RoundTripDelay を追加し、ターゲットとソースの間の累積的なネットワーク遅延を取得する 2 で除算します。

#### <a name="registry-settings"></a>レジストリの設定

# <a name="minpollintervaltabminpollinterval"></a>[MinPollInterval](#tab/MinPollInterval)
Log2 (秒) のシステムのポーリングの許可されている最短の間隔を構成します。

|  |  | 
|---------|---------|
|キーの場所     | HKLM:\SYSTEM\CurrentControlSet\Services\W32Time\Config        |
|設定    | 6        |
|結果 | ポーリング間隔の下限は 64 秒ではようになりました。 |

次のコマンドは、更新された設定を取得する Windows 時間を通知します。

`w32tm /config /update`


# <a name="maxpollintervaltabmaxpollinterval"></a>[MaxPollInterval](#tab/MaxPollInterval)
システムのポーリングの許容される log2 秒の最大間隔を構成します。

|  |  |  
|---------|---------|
|キーの場所     | HKLM:\SYSTEM\CurrentControlSet\Services\W32Time\Config        |
|設定    | 6        |
|結果 | 最大のポーリング間隔は、64 秒ではようになりました。  |

次のコマンドは、更新された設定を取得する Windows 時間を通知します。

`w32tm /config /update`

# <a name="updateintervaltabupdateinterval"></a>[UpdateInterval](#tab/UpdateInterval)
補正の調整のフェーズの間のクロック ティック数。

|  |  |  
|---------|---------|
|キーの場所     | HKLM:\SYSTEM\CurrentControlSet\Services\W32Time\Config       |
|設定    | 100        |
|結果 | 補正の調整のフェーズの間のクロック ティック数が 100 の目盛りではようになりました。 |

次のコマンドは、更新された設定を取得する Windows 時間を通知します。

`w32tm /config /update`

# <a name="specialpollintervaltabspecialpollinterval"></a>[SpecialPollInterval](#tab/SpecialPollInterval)
0x1 SpecialInterval フラグが有効な場合 (秒) には、ポーリング間隔を構成します。

|  |  |  
|---------|---------|
|キーの場所     | HKLM:\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\NtpClient        |
|設定    | 64        |
|結果 | ポーリング間隔は、64 秒ではようになりました。 |

次のコマンドは、更新された設定を取得する Windows の時刻を再起動します。

`net stop w32time && net start w32time`

# <a name="frequencycorrectratetabfrequencycorrectrate"></a>[FrequencyCorrectRate](#tab/FrequencyCorrectRate)

|  |  |  
|---------|---------|
|キーの場所     | HKLM:\SYSTEM\CurrentControlSet\Services\W32Time\Config      |
|設定    | 2        |


---
