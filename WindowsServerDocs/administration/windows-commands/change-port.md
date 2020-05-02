---
title: change port
description: ポートの変更コマンドのリファレンストピック。 MS-DOS アプリケーションと互換性があるように、COM ポートマッピングを一覧表示または変更します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3d772c90-e849-4e74-b9ec-b6cae1159336 Lizap
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8dcf1097ea037aff9269edafea6e640054a697e3
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82716078"
---
# <a name="change-port"></a>change port

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

一覧表示したり、MS-DOS アプリケーションと互換性がある COM ポートのマッピングを変更します。

> [!NOTE]
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 最新バージョンの新機能については、「 [Windows Server でのリモートデスクトップサービスの新](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn283323(v=ws.11))機能」を参照してください。

## <a name="syntax"></a>構文

```
change port [<portX>=<portY| /d <portX | /query]
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
|-----------------|----------------------------------------|
| <portX>=<portY> | COM `<*portX*>`をにマップする`<*portY*>` |
| d<portX> | COM のマッピングを削除します。`<*portX*>` |
| /query | 現在のポートマッピングが表示されます。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

#### <a name="remarks"></a>Remarks

- ほとんどの MS-DOS アプリケーションは、COM1 ~ COM4 のシリアルポートのみをサポートしています。 **ポートの変更**コマンドは、シリアルポートを別のポート番号にマップします。これにより、高番号の COM ポートをサポートしていないアプリがシリアルポートにアクセスできるようになります。 再マッピングは現在のセッションに対してのみ機能し、セッションからログオフして再度ログオンした場合は保持されません。

- パラメーターを指定せずに**ポートを変更**して、使用可能な COM ポートとその現在のマッピングを表示します。

## <a name="examples"></a>例

- MS-DOS ベースのアプリケーションで使用するために COM12 を COM1 にマップするには、次のように入力します。
  
  ```
  change port com12=com1
  ```

- 現在のポートマッピングを表示するには、次のように入力します。
  
  ```
  change port /query
  ```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [コマンドの変更](change.md)

- [リモート デスクトップ サービス (ターミナル サービス) のコマンド リファレンス](remote-desktop-services-terminal-services-command-reference.md)
