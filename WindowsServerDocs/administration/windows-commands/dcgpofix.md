---
title: dcgpofix
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 179d540371870075906bbcbf8ff912e1b883915d
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433935"
---
# <a name="dcgpofix"></a>dcgpofix



ドメインの既定のグループ ポリシー オブジェクト (Gpo) を再作成します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
DCGPOFix [/ignoreschema] [/target: {Domain | DC | Both}] [/?]
```

### <a name="parameters"></a>パラメーター

|    パラメーター    |                                                                                                 説明                                                                                                 |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  再度作成します  | Active Directory® スキーマの mc のバージョンは無視されます。</br>このコマンドを実行するとします。 それ以外の場合、コマンドは、コマンドが出荷された Windows バージョンと同じスキーマ バージョンでのみ機能します。 |
| /target {ドメイン |                                                                                                     DC                                                                                                      |
|       /?        |                                                                                    コマンド プロンプトでヘルプを表示します。                                                                                     |

## <a name="remarks"></a>注釈

-   **Dcgpofix**コマンドには、Windows Server 2008 R2 および Windows Server 2008 では、Server Core インストールする場合は除きます。
-   グループ ポリシー管理コンソール (GPMC) は、Windows Server 2008 R2 および Windows Server 2008 と共に配布は、サーバー マネージャーから機能としてグループ ポリシーの管理をインストールする必要があります。

## <a name="BKMK_Examples"></a>例

既定のドメイン ポリシー GPO は、元の状態に復元します。 この GPO に対して行った変更は失われます。 ベスト プラクティスとしては、既定アカウント ポリシーの設定、パスワード ポリシー、アカウント ロックアウトのポリシー、および Kerberos のポリシーの管理にのみ、既定のドメイン ポリシー GPO を構成する必要があります。 この例では、Active Directory スキーマのバージョンを無視できるように、 **dcgpofix**コマンドは、コマンドが出荷された Windows バージョンと同じスキーマに限定されません。
```
dcgpofix /ignoreschema /target:Domain
```
既定のドメイン コント ローラー ポリシー GPO は、元の状態に復元します。 この GPO に対して行った変更は失われます。 ベスト プラクティスとして、既定のドメイン コント ローラー ポリシー GPO には、ユーザーの権限を設定して、監査ポリシーのみを構成する必要があります。 この例では、Active Directory スキーマのバージョンを無視できるように、 **dcgpofix**コマンドは、コマンドが出荷された Windows バージョンと同じスキーマに限定されません。
```
dcgpofix /ignoreschema /target:DC
```

#### <a name="additional-references"></a>その他の参照情報

-   [グループ ポリシーの TechCenter](https://go.microsoft.com/fwlink/?LinkID=145531)
-   [コマンド ライン構文の記号](command-line-syntax-key.md)