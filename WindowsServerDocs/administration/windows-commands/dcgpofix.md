---
title: dcgpofix
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 81d5fa65-2aea-49d3-b353-357441846c00
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2592210ae688f47dcf2d32c7bef560d52223141c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378763"
---
# <a name="dcgpofix"></a>dcgpofix



ドメインの既定のグループポリシーオブジェクト (Gpo) を再作成します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
DCGPOFix [/ignoreschema] [/target: {Domain | DC | Both}] [/?]
```

### <a name="parameters"></a>パラメーター

|    パラメーター    |                                                                                                 説明                                                                                                 |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  /ignoreschema  | スキーマ mc® Active Directory のバージョンを無視します。</br>次のコマンドを実行します。 それ以外の場合、コマンドは、コマンドが配布された Windows バージョンと同じスキーマバージョンでのみ機能します。 |
| /target {ドメイン |                                                                                                     DC                                                                                                      |
|       /?        |                                                                                    コマンド プロンプトでヘルプを表示します。                                                                                     |

## <a name="remarks"></a>コメント

-   **Dcgpofix**コマンドは、windows Server 2008 R2 および windows server 2008 で使用できます。ただし、server Core インストールは除きます。
-   グループポリシー管理コンソール (GPMC) は Windows Server 2008 R2 および Windows Server 2008 と共に配布されますが、サーバーマネージャーを通じてグループポリシー管理を機能としてインストールする必要があります。

## <a name="BKMK_Examples"></a>例

既定のドメインポリシー GPO を元の状態に復元します。 この GPO に対して行った変更はすべて失われます。 ベストプラクティスとして、既定のドメインポリシー GPO は、既定のアカウントポリシー設定、パスワードポリシー、アカウントロックアウトポリシー、および Kerberos ポリシーを管理するためにのみ構成することをお勧めします。 この例では、Active Directory スキーマのバージョンを無視します。そのため、コマンドが配布された Windows バージョンと同じスキーマに、 **dcgpofix**コマンドが制限されることはありません。
```
dcgpofix /ignoreschema /target:Domain
```
既定のドメインコントローラーポリシー GPO を元の状態に復元します。 この GPO に対して行った変更はすべて失われます。 ベストプラクティスとして、既定のドメインコントローラーポリシー GPO は、ユーザー権利と監査ポリシーを設定するためにのみ構成することをお勧めします。 この例では、Active Directory スキーマのバージョンを無視します。そのため、コマンドが配布された Windows バージョンと同じスキーマに、 **dcgpofix**コマンドが制限されることはありません。
```
dcgpofix /ignoreschema /target:DC
```

#### <a name="additional-references"></a>その他の参照情報

-   [グループポリシー TechCenter](https://go.microsoft.com/fwlink/?LinkID=145531)
-   [コマンド ライン構文の記号](command-line-syntax-key.md)