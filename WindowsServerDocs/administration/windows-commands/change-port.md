---
title: change port
description: Windows コマンドに関するトピックでは、MS-DOS アプリケーションと互換性があるように、COM ポートのマッピングを一覧表示または変更します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3d772c90-e849-4e74-b9ec-b6cae1159336 Lizap
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 39273382038edb7709f2d99baea8090d71df3a57
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848075"
---
# <a name="change-port"></a>change port

> 適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

一覧表示したり、MS-DOS アプリケーションと互換性がある COM ポートのマッピングを変更します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

> [!NOTE]
> Windows Server 2008 R2 では、ターミナル サービスはリモート デスクトップ サービスという名前に変更されました。 最新バージョンの新機能については、Windows Server TechNet ライブラリの「 [Windows server 2012 のリモートデスクトップサービスの新機能](https://technet.microsoft.com/library/hh831527)」を参照してください。

## <a name="syntax"></a>構文

```
change port [<PortX>=<PortY| /d <PortX| /query]
```

### <a name="parameters"></a>パラメーター


|    パラメーター    |              説明               |
|-----------------|----------------------------------------|
| <PortX>=<PortY> | COM <*PortX*>*を < の*> にマップします。 |
|   /d <PortX>    | COM <*PortX*のマッピングを削除し> |
|     /query      | 現在のポートマッピングを表示します。 |
|       /?        | コマンドプロンプトでヘルプを表示します。 |

## <a name="remarks"></a>コメント

- ほとんどの MS-DOS アプリケーションは、COM1 ~ COM4 のシリアルポートのみをサポートしています。 **ポートの変更**コマンドは、シリアルポートを別のポート番号にマップします。これにより、高番号の COM ポートをサポートしていないアプリケーションでシリアルポートにアクセスできるようになります。 再マッピングは現在のセッションに対してのみ機能し、セッションからログオフして再度ログオンした場合は保持されません。

- パラメーターを指定せずに**ポートを変更**して、使用可能な COM ポートとその現在のマッピングを表示します。

## <a name="examples"></a><a name=BKMK_examples></a>例

- MS-DOS ベースのアプリケーションで使用するために COM12 を COM1 にマップするには、次のように入力します。
  ```
  change port com12=com1
  ```
- 現在のポートマッピングを表示するには、次のように入力します。
  ```
  change port /query
  ```

### <a name="additional-references"></a>その他の参照情報
- - [コマンド ライン構文の記号](command-line-syntax-key.md)
- [change](change.md)
- [リモート デスクトップ サービス (ターミナル サービス) のコマンド リファレンス](remote-desktop-services-terminal-services-command-reference.md)
