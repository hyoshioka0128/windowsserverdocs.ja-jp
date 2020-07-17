---
title: vdisk のアタッチ
description: アタッチ vdisk コマンドの参照記事。このコマンドは、仮想ハードディスク (VHD) をアタッチして、ホストコンピューター上にローカルハードディスクドライブとして表示されるようにします。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 882ab875-0c14-4eb3-98ef-fd0e8fa40d9c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d0d07af390a025a60fabf53635ce156cab7b71d6
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923910"
---
# <a name="attach-vdisk"></a>vdisk のアタッチ

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

仮想ハードディスク (VHD) を接続します。これにより、ホストコンピューターにローカルハードディスクドライブとして表示されます。 VHD をアタッチするときに、ディスクパーティションとファイルシステムボリュームが既に存在する場合、VHD 内のボリュームにはドライブ文字が割り当てられます。

> [!IMPORTANT]
> この操作を成功させるには、VHD を選択してデタッチする必要があります。 使用して、 **vdisk を選択して** コマンド、VHD を選択し、それにフォーカスをします。

## <a name="syntax"></a>構文

```
attach vdisk [readonly] { [sd=<SDDL>] | [usefilesd] } [noerr]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| readonly | VHD を読み取り専用としてアタッチします。 書き込み操作では、エラーが返されます。 |
| `sd=<SDDL string>` | VHD のユーザーフィルターを設定します。 フィルター文字列は SDDL (Security Descriptor Definition Language) 形式である必要があります。 既定では、ユーザーフィルターは物理ディスクでのようにアクセスを許可します。 SDDL 文字列は複雑になることがありますが、最も単純な形式では、アクセスを保護するセキュリティ記述子は随意アクセス制御リスト (DACL) と呼ばれます。 次の形式で使用されます。 `D:<dacl_flags><string_ace1><string_ace2>``<string_acen>`<p>一般的な DACL フラグは次のとおりです。<ul><li>**。** アクセスを許可</li><li>**D**。 アクセス拒否</li></ul>一般的な権限は次のとおりです。<ul><li>**GA**。 すべてのアクセス</li><li>**GR**。 読み取りアクセス</li><li> **GW**。 書き込みアクセス</li></ul>一般的なユーザーアカウントは次のとおりです。<ul><li>**BA**。 組み込みの管理者</li><li>**AU**。 認証されたユーザー</li><li>**CO**。 作成者所有者</li><li>**WD**。 Everyone</li></ul>例:<ul><li>**D: P: (A;;GR;;;AU**。 すべての認証済みユーザーに読み取りアクセス権を付与します。</li><li>**D: P: (A;;GA、;、WD**。 すべてのユーザーにフルアクセスを付与します。</li></ul> |
| usefilesd | .Vhd ファイルのセキュリティ記述子を VHD で使用することを指定します。 **Usefilesd**パラメーターが指定されていない場合、 **Sd**パラメーターで指定されていない限り、VHD には明示的なセキュリティ記述子がありません。 |
| noerr | スクリプト作成にのみ使用されます。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。 |

## <a name="examples"></a>例

選択した VHD を読み取り専用としてアタッチするには、次のように入力します。

```
attach vdisk readonly
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [select vdisk](select-vdisk.md)

- [compact vdisk](compact-vdisk.md)

- [detail vdisk](detail-vdisk.md)

- [detach vdisk](detach-vdisk.md)

- [expand vdisk](expand-vdisk.md)

- [merge vdisk](merge-vdisk.md)

- [list](list_1.md)
