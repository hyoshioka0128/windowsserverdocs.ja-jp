---
title: San
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d57c2df1-eb82-4b81-b8cd-e30564c6a929
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a999254507de2d90494c1acfb906d4bcf26168aa
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59872503"
---
# <a name="san"></a>San

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

表示またはオペレーティング システムの記憶域エリア ネットワーク (san) のポリシーを設定します。
> [!NOTE]
> このコマンドは、Windows 7 と Windows Server 2008 R2 に該当するだけです。

## <a name="syntax"></a>構文
```
san [policy={onlineAll | offlineAll | offlineShared}] [noerr]
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|policy={ onlineAll &#124; offlineAll &#124; offlineShared }]|起動した現在のオペレーティング システムの san のポリシーを設定します。 San のポリシーは、新しく検出されたディスクがオンラインまたはオフラインのままかどうか、および読み取り/書き込み可能になりますが、読み取り専用のままかどうかを判断します。 ディスクがオフラインのときは、ディスク レイアウトを読み取るがからプラグ アンド プレイ デバイスのボリュームは発生しません。 これは、ディスク上のファイル システムがマウントしないことを意味します。 ディスクがオンラインのとき、ディスクの 1 つまたは複数のボリュームのデバイスがインストールされます。 各パラメーターの説明を次に示します。<br /><br />-   **[onlineall]** します。 新しく検出されたすべてのディスクはオンラインで行われた読み取り/書き込みにするかを指定します。 **大事な：**   指定する**onlineAll**ディスクを共有するサーバーでデータが破損する可能性があります。 そのため、サーバーがクラスターの一部でない限り、ディスクがサーバー間で共有されている場合は、このポリシーを設定しないでください。<br />-   **offlineAll**します。 新しく検出されたすべてのディスク起動ディスクがオフラインになる点を指定既定では andread 取り専用です。<br />-   **オフライン共有**します。 共有バス (SCSI、iSCSI など) に常駐していないディスクがオンラインに戻るを検出し、読み取り/書き込みが行われたすべての新しくを指定します。 オフラインのまま、ディスクは、既定では読み取り専用になります。<br /><br />詳細については、次を参照してください。 [VDS_san_POLICY 列挙](https://go.microsoft.com/fwlink/?LinkId=203815)(https://go.microsoft.com/fwlink/?LinkId=203815)します。|
|noerr|スクリプトのみに使用されます。 エラーが発生すると、DiskPart は、エラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|
## <a name="remarks"></a>注釈
-   コマンドを指定するにはパラメーターなしで、現在の san ポリシーが表示されます。
## <a name="BKMK_Examples"></a>例
現在のポリシーを表示するには、次のように入力します。
```
san
```
起動ディスクを除くすべての新しく検出されたディスクをオフラインであり、既定では読み取り専用にするには、次のように入力します。
```
san policy=offlineAll
```
## <a name="additional-references"></a>その他の参照
-   [コマンドライン構文キー](command-line-syntax-key.md)
