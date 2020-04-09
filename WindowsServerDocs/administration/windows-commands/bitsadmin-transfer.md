---
title: bitsadmin Transfer
description: Bitsadmin Transfer の Windows コマンドトピック。1つ以上のファイルを転送します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fe302141-b33a-4a05-835e-dc4fc4db7d5a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4e960b4d94416d57e6c42ec27057dafef5e44516
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849005"
---
# <a name="bitsadmin-transfer"></a>bitsadmin Transfer

1つ以上のファイルを転送します。 複数のファイルを転送するには、複数の \<RemoteFileName\>-\<LocalFileName\> のペアを指定します。 ペアはスペースで区切られます。

## <a name="syntax"></a>構文

```
bitsadmin /Transfer <Name> [<Type>] [/Priority <Job_Priority>] [/ACLFlags <Flags>] [/DYNAMIC] <RemoteFileName> <LocalFileName>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Name|ジョブの名前を指定します。 ほとんどのコマンドとは異なり、 **name**には GUID ではなく名前のみを指定できます。|
|種類|省略可能: ジョブの種類を指定します。 ダウンロードジョブの場合は **/ダウンロード**(既定値)、アップロードジョブの場合は **/upload**を使用します。|
|優先順位|省略可能: job_priority を次のいずれかの値に設定します。</br>-前景</br>-高</br>-通常</br>-低|
|ACLFlags|省略可能: ファイルをダウンロードするときに所有者と ACL の情報を保持することを示します。 たとえば、ファイルで所有者とグループを管理するには、フラグを `OG`に設定します。 次のフラグの1つまたは複数を指定します。</br>-O: 所有者の情報をファイルにコピーします。</br>-G: グループ情報をファイルと共にコピーします。</br>-D: DACL 情報をファイルと共にコピーします。</br>-S: ファイルを使用して SACL 情報をコピーします。|
|/動的|[**BITS_JOB_PROPERTY_DYNAMIC_CONTENT**](/windows/desktop/api/bits5_0/ne-bits5_0-bits_job_property_id)を使用してジョブを構成します。これにより、サーバー側の要件が緩和されされます。|
|RemoteFileName|サーバーに転送されるときのファイルの名前です。|
|LocalFileName|ローカルに存在するファイルの名前。|

## <a name="remarks"></a>コメント

既定では、BITSAdmin サービスは、**通常**の優先順位で実行されるダウンロードジョブを作成し、転送が完了するか重大なエラーが発生するまで、進行状況の情報を使用してコマンドウィンドウを更新します。 サービスは、すべてのファイルを正常に転送し、重大なエラーが発生した場合にジョブをキャンセルすると、ジョブを完了します。 ジョブにファイルを追加できない場合、または*種類*または*Job_Priority*に無効な値を指定した場合、サービスはジョブを作成しません。 複数のファイルを転送するには、複数の*remotefilename*-*localfilename*のペアを指定します。 ペアはスペースで区切られます。

> [!NOTE]
> 一時的なエラーが発生した場合、BITSAdmin コマンドは引き続き実行されます。 コマンドを終了するには、CTRL + C キーを押します。

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、 *Mydownloadjob*という名前の転送ジョブを開始します。
```
C:\>bitsadmin /Transfer myDownloadJob http://prodserver/audio.wma c:\downloads\audio.wma
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)