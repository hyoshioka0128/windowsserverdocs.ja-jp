---
title: bitsadmin Transfer
description: Windows コマンド」のトピック**bitsadmin 転送**-1 つまたは複数のファイルを転送します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fe302141-b33a-4a05-835e-dc4fc4db7d5a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2ef29a242a834fae42d1de3994a82aedcf87ec2d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852463"
---
# <a name="bitsadmin-transfer"></a>bitsadmin Transfer

1 つまたは複数のファイルを転送します。 複数の指定を 1 つ以上のファイルを転送する\<RemoteFileName\>-\<LocalFileName\>ペア。 ペアは、スペースで区切られたです。

## <a name="syntax"></a>構文

```
bitsadmin /Transfer <Name> [<Type>] [/Priority <Job_Priority>] [/ACLFlags <Flags>] [/DYNAMIC] <RemoteFileName> <LocalFileName>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|名前|ジョブの名前を指定します。 ほとんどのコマンドとは異なり**名前**名前および GUID ではない可能性がありますのみを指定します。|
|種類|省略可能: ジョブの種類を指定します。 使用**ダウンロード/** (既定) ダウンロード ジョブ用または **/アップロード**アップロード ジョブ。|
|Priority|省略可能: 値は次のいずれかに、job_priority を設定します。</br>前景色</br>-高</br>-標準</br>-低|
|ACLFlags|省略可能-ダウンロードされるファイルの所有者と ACL の情報を維持することを示します。 たとえば、ファイル所有者とグループを維持するためにフラグを設定`OG`します。 次のフラグの 1 つ以上を指定します。</br>-/O:ファイルの所有者情報をコピーします。</br>-G:ファイル グループ情報をコピーします。</br>-D:DACL 情報をファイルにコピーします。</br>-%S:ファイルの SACL の情報をコピーします。|
|\/動的|使用してジョブを構成します。 [ **BITS_JOB_PROPERTY_DYNAMIC_CONTENT**](/windows/desktop/api/bits5_0/ne-bits5_0-bits_job_property_id)、サーバー側の要件を緩和します。|
|RemoteFileName|サーバーに転送するときに、ファイルの名前。|
|LocalFileName|ローカルに存在するファイルの名前。|

## <a name="remarks"></a>注釈

既定では、BITSAdmin サービスが実行されるダウンロード ジョブを作成します**標準**優先度、転送が完了するまで、または重大なエラーが発生するまで、進行状況に関する情報をコマンド ウィンドウを更新しています。 サービスは、すべてのファイル転送が正常に重大なエラーが発生した場合は、ジョブをキャンセルする場合に、ジョブを完了します。 ファイルをジョブに追加することがない場合、またはの無効な値を指定した場合、サービスがジョブを作成しません*型*または*Job_Priority*します。 複数の指定を 1 つ以上のファイルを転送する*RemoteFileName*-*LocalFileName*ペア。 ペアは、スペースで区切られたです。

> [!NOTE]
> BITSAdmin コマンドは、一時的なエラーが発生した場合に実行を続けます。 コマンドを終了するには、CTRL + C キーを押します。

## <a name="BKMK_examples"></a>例

という名前のジョブでの転送を次の例が開始*myDownloadJob*します。
```
C:\>bitsadmin /Transfer myDownloadJob http://prodserver/audio.wma c:\downloads\audio.wma
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)