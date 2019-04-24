---
title: atmadm
description: Windows コマンド」のトピック**atmadm** -モニター接続と、atM で登録されているアドレスは、非同期転送モード (atM) ネットワークでマネージャーを呼び出します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 37156c2e-c4d4-4fd8-a03d-245fb60bf996
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3a8a8883bad9aa2abdc90d5db5702ef42f46c8a8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59831773"
---
# <a name="atmadm"></a>atmadm

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

モニターの接続と、atM で登録されているアドレスは、非同期転送モード (atM) ネットワークでマネージャーを呼び出します。 使用することができます**atmadm** atM アダプターで受信および送信呼び出しの統計情報を表示します。 パラメーターを指定せずに使用される**atmadm** active atM 接続の状態を監視するための統計が表示されます。 

## <a name="syntax"></a>構文

```
atmadm [/c][/a][/s]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------|--------|
|/c|このコンピューターにインストールされている、atM のネットワーク アダプターに現在の接続をすべての呼び出し情報を表示します。|
|/a|登録済みの atM のネットワーク サービス アクセス ポイントのこのコンピューターにインストールされている各アダプターの (NSAP) のアドレスを表示します。|
|/s|AtM のアクティブな接続の状態を監視するための統計情報が表示されます。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

- **Atmadm/c**コマンドには、次のような出力が生成されます。

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
    
    次の表には、各要素の説明が含まれています、 **atmadm/c**サンプル出力します。
    
    |データの種類|画面の表示|説明|
    |--------|---------|--------|
    |接続情報|入力/出力|呼び出しの方向。  **** AtM のネットワーク アダプターには、別のデバイスから。  **Out**が atM のネットワーク アダプターから別のデバイス。|
    ||PMP|ポイント ツー マルチポイント呼び出し。|
    ||P-P|ポイント ツー ポイントの呼び出し。|
    ||SVC|スイッチの仮想回線上の接続です。|
    ||PVC|永続的な仮想回線上の接続です。|
    |VPI 情報情報|VPI 情報|仮想パスと仮想チャネルの受信または送信を呼び出します。|
    |リモート アドレス/メディア パラメーター|47000580FFE1000000F21A2E180000C110081500|NSAP アドレス、呼び出し元の **(In)** と呼ばれるまたは **(Out)** atM デバイス。|
    ||**テキサス州**|**Tx**パラメーターには、次の 3 つの要素が含まれています。<br /><br />-既定値または指定されたビット レートの種類 (UBR、CBR、VBR、または ABR)<br />-既定値または指定した行の速度<br />-指定されたサービスのデータ ユニット (SDU) のサイズ|
    ||**Rx**|**Rx**パラメーターには、次の 3 つの要素が含まれています。<br /><br />-既定値または指定されたビット レートの種類 (UBR、CBR、VBR、または ABR)<br />-既定値または指定した行の速度<br />-指定された SDU サイズ|
    
- **Atmadm/a**コマンドには、次のような出力が生成されます。

    ```
    Windows atM call Manager Statistics
    atM addresses for Interface : [009] Olicom atM PCI 155 Adapter
    47000580FFE1000000F21A2E180000C110081500
    ```
    
- **Atmadm/s**コマンドには、次のような出力が生成されます。

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
    
    次の表には、各要素の説明が含まれています、 **atmadm/s**サンプル出力します。
    
    |コール マネージャー統計情報|説明|
    |-------------|--------|
    |現在アクティブな呼び出し|このコンピューターにインストールされている、atM アダプターで、現在アクティブなを呼び出します。|
    |成功した着信呼び出しを合計します。|この atM ネットワーク上の他のデバイスから正常に受信した呼び出し。|
    |成功した発信呼び出しを合計します。|呼び出しがこのコンピューターからこのネットワーク上の他の atM デバイスに正常に完了しました。|
    |着信呼び出しが失敗しました。|このコンピューターへの接続に失敗した着信します。|
    |発信呼び出しが失敗しました。|ネットワーク上の別のデバイスへの接続に失敗した呼び出しを送信します。|
    |リモートで呼び出し終了|ネットワーク上のリモート デバイスで終了した呼び出し。|
    |閉じられたローカル呼び出し|このコンピューターで終了した呼び出し。|
    |シグナリングと ILMI パケットの送信|スイッチに送信されるローカルの統合の管理インターフェイス (ILMI) パケットの数がこのコンピューターが接続しようとします。|
    |シグナリングと ILMI パケットの受信|AtM スイッチから受信した ILMI パケットの数。|
    
## <a name="BKMK_Examples"></a>例

このコンピューターにインストールされている、atM のネットワーク アダプターに現在のすべての接続の呼び出し情報を表示するには、次のように入力します。

```
atmadm /c
```

このコンピューターにインストールされている各アダプターの登録済みの atM ネットワーク サービス アクセス ポイント (NSAP) アドレスを表示するには、次のように入力します。

```
atmadm /a
```

AtM のアクティブな接続の状態を監視するための統計情報を表示するには、次のように入力します。

```
atmadm /s
```

## <a name="additional-references"></a>その他の参照情報

- [コマンドライン構文キー](command-line-syntax-key.md)
