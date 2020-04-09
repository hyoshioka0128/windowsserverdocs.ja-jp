---
title: netcfg
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e2daaab7-12db-4e36-b70c-db8906d084f7 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4895928ffdd5d923d370f82e699d69f42c0f81a5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80838935"
---
# <a name="netcfg"></a>netcfg

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Windows プレインストール環境 (WinPE) で、ワークステーションを展開するために使用する Windows の軽量バージョンをインストールします。
## <a name="syntax"></a>構文
```
netcfg [/v] [/e] [/winpe] [/l ] /c /i
```
#### <a name="parameters"></a>パラメーター
|パラメーター|説明|
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

## <a name="examples"></a><a name=BKMK_Examples></a>例

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
## <a name="additional-references"></a>その他の参照情報
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)
