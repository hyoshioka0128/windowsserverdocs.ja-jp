---
title: dcgpofix
description: Windows コマンドに関するトピック (dcgpofix) では、ドメインの既定のグループポリシーオブジェクト (Gpo) が再作成されます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 81d5fa65-2aea-49d3-b353-357441846c00
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1532d4c8c0266c92b4efce57a6744552a54e51b0
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80846705"
---
# <a name="dcgpofix"></a>dcgpofix

ドメインの既定のグループポリシーオブジェクト (Gpo) を再作成します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
DCGPOFix [/ignoreschema] [/target: {Domain | DC | Both}] [/?]
```

#### <a name="parameters"></a>パラメーター

|    パラメーター    |                                                                                                 説明                                                                                                 |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  /ignoreschema  | スキーマ mc® Active Directory のバージョンを無視します。</br>次のコマンドを実行します。 それ以外の場合、コマンドは、コマンドが配布された Windows バージョンと同じスキーマバージョンでのみ機能します。 |
| /target {ドメイン |                                                                                                     DC                                                                                                      |
|       /?        |                                                                                    コマンド プロンプトでヘルプを表示します。                                                                                     |

## <a name="remarks"></a>コメント

-   **Dcgpofix**コマンドは、windows Server 2008 R2 および windows server 2008 で使用できます。ただし、server Core インストールは除きます。
-   グループポリシー管理コンソール (GPMC) は Windows Server 2008 R2 および Windows Server 2008 と共に配布されますが、サーバーマネージャーを通じてグループポリシー管理を機能としてインストールする必要があります。

## <a name="examples"></a><a name=BKMK_Examples></a>例

既定のドメインポリシー GPO を元の状態に復元します。 この GPO に対して行った変更はすべて失われます。 ベストプラクティスとして、既定のドメインポリシー GPO は、既定のアカウントポリシー設定、パスワードポリシー、アカウントロックアウトポリシー、および Kerberos ポリシーを管理するためにのみ構成することをお勧めします。 この例では、Active Directory スキーマのバージョンを無視します。そのため、コマンドが配布された Windows バージョンと同じスキーマに、 **dcgpofix**コマンドが制限されることはありません。
```
dcgpofix /ignoreschema /target:Domain
```
既定のドメインコントローラーポリシー GPO を元の状態に復元します。 この GPO に対して行った変更はすべて失われます。 ベストプラクティスとして、既定のドメインコントローラーポリシー GPO は、ユーザー権利と監査ポリシーを設定するためにのみ構成することをお勧めします。 この例では、Active Directory スキーマのバージョンを無視します。そのため、コマンドが配布された Windows バージョンと同じスキーマに、 **dcgpofix**コマンドが制限されることはありません。
```
dcgpofix /ignoreschema /target:DC
```

## <a name="additional-references"></a>その他の参照情報

-   [グループポリシー TechCenter](https://go.microsoft.com/fwlink/?LinkID=145531)
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)