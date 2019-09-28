---
title: Scwcmd ロールバック
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4fd9f89b-0420-420a-ad20-4a328636b1e7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3f089ea3e6e5d5b95080356dd239272b95a76b37
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371213"
---
# <a name="scwcmd-rollback"></a>Scwcmd: rollback

> 適用先:Windows Server 2012 R2、Windows Server 2012

使用可能な最新のロールバックのポリシーを適用し、そのロールバックのポリシーを削除します。

## <a name="syntax"></a>構文

```
scwcmd rollback /m:<ComputerName> [/u:<UserName>] [/pw:<Password>]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/m: \<ComputerName >|NetBIOS 名、DNS 名、またはロールバック操作が実行するコンピューターの IP アドレスを指定します。|
|/u: \<UserName >|リモートのロールバックを実行するときに使用する代替のユーザー アカウントを指定します。 既定値は、ユーザーには、ログオンしています。|
|/pw: \<Password >|リモートのロールバックを実行するときに使用する、代替のユーザー資格情報を指定します。 既定値は、ユーザーには、ログオンしています。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>コメント

Scwcmd.exe は Windows Server 2008 R2、Windows Server 2008 または Windows Server 2003 を実行するコンピューターにできるだけです。

## <a name="BKMK_Examples"></a>例

「172.16.0.0」の IP アドレスにあるコンピューターで、セキュリティ ポリシーをロールバックするには、次ように入力します。
```
scwcmd rollback /m:172.16.0.0
```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンド ライン構文の記号](command-line-syntax-key.md)