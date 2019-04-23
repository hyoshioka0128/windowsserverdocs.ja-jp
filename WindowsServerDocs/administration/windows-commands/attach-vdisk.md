---
title: vdisk をアタッチします。
description: Windows コマンド」のトピック**attach vdisk** -ローカルのハード ディスク ドライブとしてホスト コンピューター上に表示されるように (とも呼ばれるマウントまたはサーフェス) の接続が仮想ハード_ディスク (VHD) します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 882ab875-0c14-4eb3-98ef-fd0e8fa40d9c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e715b36f8d9d8b416311567c2455920243dfc7a2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59885613"
---
# <a name="attach-vdisk"></a>vdisk をアタッチします。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

(とも呼ばれるマウントまたはアタッチ サーフェス) 仮想ハード_ディスク (VHD) としてローカル ハード ディスク ドライブをホスト コンピューター上に表示されるようにします。 VHD は、アタッチするには、ディスク パーティションとファイル システムのボリュームを既に持っている場合、vhd のボリュームにドライブ文字が割り当てられます。
> [!NOTE]
> このコマンドは、Windows 7 と Windows Server 2008 R2 に該当するだけです。

## <a name="syntax"></a>構文
```
attach vdisk [readonly] { [sd=<SDDL>] | [usefilesd] } [noerr]
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|読み取り専用|読み取り専用として VHD をアタッチします。 すべての書き込み操作を返します。 エラー。|
|sd=<SDDL string>|VHD 上で、ユーザー フィルターを設定します。 フィルター文字列は、セキュリティ記述子定義言語 (SDDL) 形式である必要があります。 既定では、ユーザー フィルターは、物理ディスク上のようなへのアクセスを許可します。<br /><br />SDDL 文字列が複雑になることができますが、最も単純な形式では、アクセスを保護するセキュリティ記述子は随意アクセス制御リスト (DACL) と呼ばれます。 形式には。D: < dacl_flags >< string_ace1 >< string_ace2 >.< string_acen ><br /><br />DACL の一般的なフラグは次のとおりです。<br /><br />-   **A**アクセスを許可します。<br />-   **D**アクセスを拒否します。<br /><br />一般的な権限は次のとおりです。<br /><br />-   **GA**のすべてのアクセス<br />-   **GR**読み取りアクセス<br />-   **GW**書き込みアクセス<br /><br />共通のユーザー アカウントは次のとおりです。<br /><br />-   **BA**管理者に組み込まれています<br />-   **オーストラリア**認証されたユーザー<br />-   **CO** Creator owner<br />-   **WD** -すべてのユーザー<br /><br />例:<br /><br />**D:P:(A;;GR;;オーストラリア**により、すべての認証済みユーザーに読み取りアクセス<br /><br />**D:P:(A;;GA;;WD**全員の完全なアクセス|
|usefilesd|VHD 上で、.vhd ファイルのセキュリティ記述子を使用することを指定します。 場合、 **Usefilesd**パラメーターが指定されていないを指定しない場合、VHD は、明示的なセキュリティ記述子をありません、 **Sd**パラメーター。|
|noerr|スクリプトのみに使用されます。 エラーが発生すると、DiskPart は、エラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|
## <a name="remarks"></a>注釈
-   VHD の選択し、この操作を正常にデタッチする必要があります。 使用して、 **vdisk を選択して** コマンド、VHD を選択し、それにフォーカスをします。
## <a name="BKMK_Examples"></a>例
読み取り専用として選択した VHD をアタッチするには、次のように入力します。
```
attach vdisk readonly
```
## <a name="additional-references"></a>その他の参照
-   [コマンドライン構文キー](command-line-syntax-key.md)
-   [vdisk を最適化します。](compact-vdisk.md)

-   [詳細 vdisk](detail-vdisk.md)
-   [Vdisk をデタッチします。](detach-vdisk.md)
-   [vdisk を展開します。](expand-vdisk.md)
-   [Vdisk をマージします。](merge-vdisk.md)
-   [vdisk を選択します。](select-vdisk.md)
-   [list_1](list_1.md)
