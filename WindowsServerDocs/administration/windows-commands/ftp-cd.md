---
title: ftp cd
description: Ftp cd コマンドのリファレンストピックで、リモートコンピューター上の作業ディレクトリを変更します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a574855a-31b4-45c6-bce2-581c7231c99b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dbeff9c2fca654120347f0f616325b700f5c9be3
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820002"
---
# <a name="ftp-cd"></a>ftp cd

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモートコンピューター上の作業ディレクトリを変更します。

## <a name="syntax"></a>構文

```
cd <remotedirectory>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| <remotedirectory> | 変更するリモートコンピューター上のディレクトリを指定します。 |

### <a name="examples"></a>例

リモートコンピューター上のディレクトリを*Docs*に変更するには、次のように入力します。

```
cd Docs
```

リモートコンピューター上のディレクトリを5月の*ビデオ*に変更するには、次のように入力します。

```
cd  May Videos
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [追加の FTP ガイダンス](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
