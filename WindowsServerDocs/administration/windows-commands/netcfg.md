---
title: netcfg
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e2daaab7-12db-4e36-b70c-db8906d084f7 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bfbe8cd757f78bfa3e808a9126af7d1698579885
ms.sourcegitcommit: 0a0a45bec6583162ba5e4b17979f0b5a0c179ab2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79320006"
---
# <a name="netcfg"></a>netcfg

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Windows プレインストール環境 (WinPE) で、ワークステーションを展開するために使用する Windows の軽量バージョンをインストールします。
## <a name="syntax"></a>構文
```
netcfg [/v] [/e] [/winpe] [/l ] /c /i
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/v|**詳細**(詳細) モードで実行する|
|/e|インストールおよびアンインストール中にサービス**環境**変数を使用する|
|/winpe|Windows プレインストール環境 (WinPE) 用の TCP/IP、NetBIOS、および Microsoft クライアントをインストールします。|
|/l|INF の**場所**を提供します。|
|/c|インストールするコンポーネントの**クラス**を提供します。プロトコル、サービス、またはクライアント|
|/i|コンポーネント**ID**を提供します。|
|/s|**表示**するコンポーネントの種類を提供します。<br /><br />\ta アダプター、n = = net コンポーネント|
|/b|**バインドパス**を表示します。その後にパスの名前を含む文字列を指定します。|
|/?|コマンドプロンプトで**ヘルプ**を表示します。|

## <a name="BKMK_Examples"></a>例

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
-   [コマンド ライン構文の記号](command-line-syntax-key.md)
