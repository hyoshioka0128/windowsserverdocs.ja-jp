---
title: netcfg
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e2daaab7-12db-4e36-b70c-db8906d084f7 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a5945da45ee01fd5bf5f89a7835c4bae0b5534c4
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723804"
---
# <a name="netcfg"></a>netcfg

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Windows プレインストール環境 (WinPE) で、ワークステーションを展開するために使用する Windows の軽量バージョンをインストールします。
## <a name="syntax"></a>構文
```
netcfg [/v] [/e] [/winpe] [/l ] /c /i
```
#### <a name="parameters"></a>パラメーター
|パラメーター|[説明]|
|-------|--------|
|/v|**詳細**(詳細) モードで実行する|
|/e|インストールおよびアンインストール中にサービス**環境**変数を使用する|
|/winpe|Windows プレインストール環境 (WinPE) 用の TCP/IP、NetBIOS、および Microsoft クライアントをインストールします。|
|/l|INF の**場所**を提供します。|
|/c|インストールするコンポーネントの**クラス**を提供します。プロトコル、サービス、またはクライアント|
|/i|コンポーネント**ID**を提供します。|
|/s|**表示**するコンポーネントの種類を提供します。<p>\ta アダプター、n = = net コンポーネント|
|/b|**バインドパス**を表示します。その後にパスの名前を含む文字列を指定します。|
|/?|コマンドプロンプトで**ヘルプ**を表示します。|

## <a name="examples"></a>例

プロトコルをインストールする *例* c:\oemdir\example.inf を使用します。
```
netcfg /l c:\oemdir\example.inf /c p /i example
```
インストールする、 *MS_Server* サービス。
```
netcfg /c s /i MS_Server
```
Windows プレインストール環境の TCP/IP、NetBIOS、および Microsoft のクライアントをインストールするには
```
netcfg /v /winpe
```
コンポーネントを表示する *MS_IPX* がインストールされています。
```
netcfg /q MS_IPX
```
コンポーネントをアンインストールする *MS_IPX*:
```
netcfg /u MS_IPX
```
すべてを表示するには、net のコンポーネントをインストールします。
```
netcfg /s n
```
*MS_TCPIP*を含むバインドパスを表示するには:
```
netcfg /b ms_tcpip
```
## <a name="additional-references"></a>その他のリファレンス
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)
