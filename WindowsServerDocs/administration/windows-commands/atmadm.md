---
title: atmadm
description: Windows コマンド**に関するトピックでは**、Atm コールマネージャーによって非同期転送モード (atm) ネットワークに登録されている接続とアドレスを監視します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 37156c2e-c4d4-4fd8-a03d-245fb60bf996
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cbfb787c472eaad4cbef5f86e7546f7b6f1da305
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851275"
---
# <a name="atmadm"></a>atmadm

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

AtM コールマネージャーによって非同期転送モード (atM) ネットワークに登録されている接続とアドレスを監視します。 **Atmadm**を使用して、atM アダプターでの着信および発信呼び出しの統計情報を表示できます。 パラメーターを指定せずに使用します。 **atmadm**には、アクティブな atM 接続の状態を監視するための統計情報が表示されます。 

## <a name="syntax"></a>構文

```
atmadm [/c][/a][/s]
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ------- | -------- |
| /c | このコンピューターにインストールされている atM ネットワークアダプターへの現在のすべての接続に関する呼び出し情報を表示します。 |
| /a | このコンピューターにインストールされている各アダプターの登録済み atM ネットワークサービスアクセスポイント (NSAP) アドレスを表示します。 |
| /s | アクティブな atM 接続の状態を監視するための統計情報を表示します。 |
| /? | コマンド プロンプトでヘルプを表示します。 |

## <a name="remarks"></a>コメント

- **Atmadm/c**コマンドを実行すると、次のような出力が生成されます。

    ```
    Windows atM call Manager Statistics
    atM Connections on Interface : [009] Olicom atM PCI 155 Adapter
       Connection   VPI/VCI   remote address/
                              Media Parameters (rates in bytes/sec)
       In  PMP SVC    0/193   47000580FFE1000000F21A2E180020481A2E180B
                              Tx:UBR,Peak 0,Avg 0,MaxSdu 1516
                              Rx:UBR,Peak 16953936,Avg 16953936,MaxSdu 1516
       Out P-P SVC    0/192   47000580FFE1000000F21A2E180020481A2E180B
                              Tx:UBR,Peak 16953936,Avg 16953936,MaxSdu 1516
                              Rx:UBR,Peak 16953936,Avg 16953936,MaxSdu 1516
       In  PMP SVC    0/191   47000580FFE1000000F21A2E180020481A2E180B
                              Tx:UBR,Peak 0,Avg 0,MaxSdu 1516
                              Rx:UBR,Peak 16953936,Avg 16953936,MaxSdu 1516
       Out P-P SVC    0/190   47000580FFE1000000F21A2E180020481A2E180B
                              Tx:UBR,Peak 16953936,Avg 16953936,MaxSdu 1516
                              Rx:UBR,Peak 16953936,Avg 16953936,MaxSdu 1516
       In  P-P SVC    0/475   47000580FFE1000000F21A2E180000C110081501
                              Tx:UBR,Peak 16953984,Avg 16953984,MaxSdu 9188
                              Rx:UBR,Peak 16953936,Avg 16953936,MaxSdu 9188
       Out PMP SVC    0/194   47000580FFE1000000F21A2E180000C110081501 (0)
                              Tx:UBR,Peak 16953984,Avg 16953984,MaxSdu 9180
                              Rx:UBR,Peak 0,Avg 0,MaxSdu 0
       Out P-P SVC    0/474   4700918100000000613E5BFE010000C110081500
                              Tx:UBR,Peak 16953984,Avg 16953984,MaxSdu 9188
                              Rx:UBR,Peak 16953984,Avg 16953984,MaxSdu 9188
       In  PMP SVC    0/195   47000580FFE1000000F21A2E180000C110081500
                              Tx:UBR,Peak 0,Avg 0,MaxSdu 0
                              Rx:UBR,Peak 16953936,Avg 16953936,MaxSdu 9180
    ```

    次の表に、 **atmadm/c**サンプル出力の各要素について説明します。

    | データの種類 | 画面表示 | 説明 |
    | -------- | --------- | -------- |
    | 接続情報 | 入出力 | 呼び出しの方向。 **の**は、別のデバイスからの atM ネットワークアダプターに対するものです。  これは、atM ネットワークアダプターから別のデバイスに**送信**されます。 |
    | PMP | ポイント対 multipoint 呼び出し。 |
    | P-P | ポイントツーポイントの呼び出し。 |
    | SVC | スイッチの仮想回線上に接続しています。 |
    | PVC | 接続は永続的な仮想回線上にあります。 |
    | VPI/VCI 情報 | VPI/VCI | 受信または送信呼び出しの仮想パスと仮想チャネル。 |
    | リモートアドレス/メディアパラメーター | 47000580FFE1000000F21A2E180000C110081500 | **(では)** 、または呼び出された **(Out)** と呼ばれる atM デバイスの NSAP アドレス。 |
    | Tx | **Tx**パラメーターには、次の3つの要素が含まれています。<p>-既定または指定されたビットレートの種類 (UBR、CBR、VBR、または ABR)<p>-既定または指定された回線速度<p>-指定されたサービスデータユニット (SDU) のサイズ。 |
    | Rx | **Rx**パラメーターには、次の3つの要素が含まれます。<p>-既定または指定されたビットレートの種類 (UBR、CBR、VBR、または ABR)<p>-既定または指定された回線速度<p>-指定された SDU サイズ。 |

- **Atmadm/a**コマンドを実行すると、次のような出力が生成されます。

    ```
    Windows atM call Manager Statistics
    atM addresses for Interface : [009] Olicom atM PCI 155 Adapter
    47000580FFE1000000F21A2E180000C110081500
    ```

- **Atmadm/s**コマンドを実行すると、次のような出力が生成されます。

    ```
    Windows atM call Manager Statistics
    atM call Manager statistics for Interface : [009] Olicom atM PCI 155 Adapter
    Current active calls                        = 4
    Total successful Incoming calls             = 1332
    Total successful Outgoing calls             = 1297
    Unsuccessful Incoming calls                 = 1
    Unsuccessful Outgoing calls                 = 1
    calls Closed by remote                      = 1302
    calls Closed Locally                        = 1323
    Signaling and ILMI Packets Sent            = 33655
    Signaling and ILMI Packets Received        = 34989
    ```

    次の表に、 **atmadm/s**サンプル出力の各要素について説明します。

    | コールマネージャーの統計情報 | 説明 |
    | ------------- | -------- |
    | 現在のアクティブな呼び出し | このコンピューターにインストールされている atM アダプターで現在アクティブになっている呼び出し。 |
    | 成功した着信呼び出しの合計数 | この atM ネットワーク上の他のデバイスから正常に受信した呼び出し。 |
    | 成功した送信呼び出しの合計数 | このコンピューターから、このネットワーク上の他の atM デバイスへの呼び出しが正常に完了しました。 |
    | 失敗した着信呼び出し | このコンピューターへの接続に失敗した着信呼び出し。 |
    | 失敗した発信呼び出し | ネットワーク上の別のデバイスに接続できなかった発信呼び出し。 |
    | リモートによって閉じられた呼び出し | ネットワーク上のリモートデバイスによって閉じられた呼び出し。 |
    | ローカルで閉じられた呼び出し | このコンピューターによって閉じられた呼び出し。 |
    | 送信されたシグナリングと ILMI パケット | このコンピューターが接続しようとしているスイッチに送信された統合ローカル管理インターフェイス (ILMI) パケットの数。 |
    | 受信したシグナリングと ILMI パケット | AtM スイッチから受信した ILMI パケットの数。 |

## <a name="examples"></a><a name=BKMK_Examples></a>例

このコンピューターにインストールされている atM ネットワークアダプターへの現在のすべての接続の呼び出し情報を表示するには、次のように入力します。

```
atmadm /c
```

このコンピューターにインストールされている各アダプターの登録済み atM ネットワークサービスアクセスポイント (NSAP) アドレスを表示するには、次のように入力します。

```
atmadm /a
```

アクティブな atM 接続の状態を監視するための統計情報を表示するには、次のように入力します。

```
atmadm /s
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
