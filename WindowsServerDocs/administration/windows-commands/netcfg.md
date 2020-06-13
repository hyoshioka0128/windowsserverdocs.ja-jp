---
title: netcfg
description: Netcfg コマンドのリファレンストピックでは、Windows プレインストール環境 (WinPE) をインストールします。これは、ワークステーションの展開に使用される簡易版の Windows です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e2daaab7-12db-4e36-b70c-db8906d084f7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5a308441df55873b205972d703ec52f53345beb5
ms.sourcegitcommit: 99d548141428c964facf666c10b6709d80fbb215
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/12/2020
ms.locfileid: "84721555"
---
# <a name="netcfg"></a>netcfg

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Windows プレインストール環境 (WinPE) で、ワークステーションを展開するために使用する Windows の軽量バージョンをインストールします。

## <a name="syntax"></a>構文

```
netcfg [/v] [/e] [/winpe] [/l ] /c /i
```

### <a name="parameters"></a>パラメーター

| パラメーター | Description |
| --------- | ----------- |
| /v | 詳細 (詳細) モードで実行します。 |
| /e | は、インストールおよびアンインストール中にサービス環境変数を使用します。 |
| /winpe | Windows プレインストール環境 (WinPE) 用の TCP/IP、NetBIOS、および Microsoft クライアントをインストールします。 |
| /l | INF ファイルの場所を提供します。 |
| /c | インストールするコンポーネントのクラスを提供します。**プロトコル**、**サービス**、または**クライアント**。 |
| /i | コンポーネント ID を提供します。 |
| /s | アダプターの**\ ta**や、net コンポーネントの**n**など、表示するコンポーネントの種類を提供します。 |
| /b | バインドパスを表示します。その後にパスの名前を含む文字列を指定します。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

### <a name="examples"></a>例

このプロトコルの*例*をインストールするには、次のように入力します。

```
netcfg /l c:\oemdir\example.inf /c p /i example
```

*MS_Server*サービスをインストールするには、次のように入力します。

```
netcfg /c s /i MS_Server
```

Windows プレインストール環境用に TCP/IP、NetBIOS、および Microsoft クライアントをインストールするには、次のように入力します。

```
netcfg /v /winpe
```

コンポーネント*MS_IPX*がインストールされているかを表示するには、次のように入力します。

```
netcfg /q MS_IPX
```

コンポーネント*MS_IPX*をアンインストールするには、次のように入力します。

```
netcfg /u MS_IPX
```

インストールされたすべての net コンポーネントを表示するには、次のように入力します。

```
netcfg /s n
```

*MS_TCPIP*を含むバインドパスを表示するには、次のように入力します。

```
netcfg /b ms_tcpip
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)
