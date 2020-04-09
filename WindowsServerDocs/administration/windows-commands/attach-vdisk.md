---
title: vdisk のアタッチ
description: '**Vdisk**の Windows コマンドに関するトピックでは、仮想ハードディスク (VHD) をアタッチし (マウントまたはサーフェスと呼ばれることもあります)、ホストコンピューターにローカルのハードディスクドライブとして表示されるようにします。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 882ab875-0c14-4eb3-98ef-fd0e8fa40d9c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a3a903ed231e34ac902ce10b5342f27e772ac89f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851265"
---
# <a name="attach-vdisk"></a>vdisk のアタッチ

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

仮想ハードディスク (VHD) を接続します。これにより、ホストコンピューターにローカルハードディスクドライブとして表示されます。 VHD をアタッチするときに、ディスクパーティションとファイルシステムボリュームが既に存在する場合、VHD 内のボリュームにはドライブ文字が割り当てられます。

> [!NOTE]
> このコマンドは、Windows 7 と Windows Server 2008 R2 に該当するだけです。

## <a name="syntax"></a>構文

```
attach vdisk [readonly] { [sd=<SDDL>] | [usefilesd] } [noerr]
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| readonly | VHD を読み取り専用としてアタッチします。 書き込み操作では、エラーが返されます。 |
| `sd=<SDDL string>` | VHD のユーザーフィルターを設定します。 フィルター文字列は SDDL (Security Descriptor Definition Language) 形式である必要があります。 既定では、ユーザーフィルターは物理ディスクでのようにアクセスを許可します。 SDDL 文字列は複雑になることがありますが、最も単純な形式では、アクセスを保護するセキュリティ記述子は随意アクセス制御リスト (DACL) と呼ばれます。 形式は次のとおりです: `D:<dacl_flags><string_ace1><string_ace2>`... `<string_acen>`<p>一般的な DACL フラグは次のとおりです。<p>- **ます**。アクセスを許可する<p>- **D**。アクセスの拒否<p>一般的な権限は次のとおりです。<p>- **GA**。 すべてのアクセス<p>- **GR**。 読み取りアクセス権<p>- **GW**。 書き込みアクセス<p>一般的なユーザーアカウントは次のとおりです。<p>- **BA**。 組み込みの管理者<p>**AU**を - します。 認証済みユーザー<p>- **CO**。 作成者所有者<p>- **WD**。 全員<p>例:<p>**D: P: (A;;GR;;;AU**を使用すると、すべての認証済みユーザーに読み取りアクセス権が付与されます。<p>**D: P: (A;;GA、;、WD**は、すべてのユーザーにフルアクセスを付与します。 |
| usefilesd | .Vhd ファイルのセキュリティ記述子を VHD で使用することを指定します。 **Usefilesd**パラメーターが指定されていない場合、 **Sd**パラメーターで指定されていない限り、VHD には明示的なセキュリティ記述子がありません。 |
| noerr | スクリプト作成にのみ使用されます。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。 |

## <a name="remarks"></a>コメント

- この操作を成功させるには、VHD を選択してデタッチする必要があります。 使用して、 **vdisk を選択して** コマンド、VHD を選択し、それにフォーカスをします。

## <a name="examples"></a><a name=BKMK_Examples></a>例

選択した VHD を読み取り専用としてアタッチするには、次のように入力します。

```
attach vdisk readonly
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [compact vdisk](compact-vdisk.md)

- [詳細 vdisk](detail-vdisk.md)

- [vdisk のデタッチ](detach-vdisk.md)

- [vdisk を展開する](expand-vdisk.md)

- [マージ vdisk](merge-vdisk.md)

- [vdisk の選択](select-vdisk.md)

- [表](list_1.md)
