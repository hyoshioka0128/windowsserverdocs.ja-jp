---
title: サブコマンドの開始-名前空間
description: サブコマンドの開始名前空間の参照記事。スケジュールされたキャストの名前空間を開始します。
ms.topic: article
ms.assetid: 2dd1c11e-6ab7-4129-9e3a-3f80e0ba59c0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7a80664fb4a4f90f58823b87f278b344561422ef
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87882081"
---
# <a name="subcommand-start-namespace"></a>サブコマンド: 開始-名前空間

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

スケジュールされたキャストの名前空間を開始します。

## <a name="syntax"></a>構文
```
wdsutil /start-Namespace /Namespace:<Namespace name[/Server:<Server name>]
```
### <a name="parameters"></a>パラメーター

|          パラメーター          |                                                                                                                                                                                             説明                                                                                                                                                                                             |
|-----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /Namespace: 名前空間名を <しています| 名前空間の名前を指定します。 これは、フレンドリ名ではない、一意である必要があることに注意してください。<p>-   **配置サーバー**: 名前空間名の構文は、/NAMSPACE: WDS: <Image group> / <Image name> / <Index> です。 例: **WDS:ImageGroup1/install.wim/1**<br />-   **トランスポートサーバー**: この名前は、サーバー上で作成されたときに名前空間に指定された名前と一致する必要があります。 |
|   [/Server:<Server name>]   |                                                                                                           サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。                                                                                                           |

## <a name="examples"></a>例
名前空間を開始するには、次のいずれかを入力します。
```
wdsutil /start-Namespace /Namespace:Custom Auto 1
wdsutil /start-Namespace /Server:MyWDSServer /Namespace:Custom Auto 1
```
## <a name="additional-references"></a>その他の参照情報
- [コマンドライン構文のキー](command-line-syntax-key.md) 
[Get AllNamespaces コマンド](using-the-get-allnamespaces-command.md) 
 の使用[新しい名前空間のコマンド](using-the-new-namespace-command.md) 
 を使用する[名前空間の削除コマンドを使用する](using-the-remove-namespace-command.md)
