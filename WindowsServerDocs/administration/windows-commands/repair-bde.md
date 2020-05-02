---
title: repair-bde
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 534dca1a-05f7-4ea8-ac24-4fe5f14f988a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 501ab801e76980f7e94e88213dd3aa42ee04d4d7
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722397"
---
# <a name="repair-bde"></a>repair-bde



BitLocker を使用してドライブが暗号化されている場合は、重大な損傷を受けたハードディスク上の暗号化されたデータにアクセスします。 有効な回復パスワードまたは回復キーを使用してデータの暗号化が解除されるなら、repair-bde はドライブの重要な部分を再構築して、回復可能なデータを修復できます。 ドライブの BitLocker メタデータ データが破損した場合は、回復パスワードまたは回復キーに加えて、バックアップ キー パッケージを提供できる必要があります。 Active Directory ドメイン サービス (AD DS) バックアップの既定の設定を使用した場合、このキー パッケージは AD DS にバックアップされます。 このキー パッケージと回復パスワードまたは回復キーを使用すると、ディスクが破損した場合でも、BitLocker で保護されたドライブの部分の暗号化を解除できます。 各キー パッケージは、対応するドライブ識別子があるドライブに対してのみ動作します。 [Active Directory の BitLocker 回復パスワードビューアー](https://technet.microsoft.com/library/dd875531(v=ws.10).aspx)を使用して、AD DS からこのキーパッケージを取得できます。

> [!NOTE]
> BitLocker 回復パスワードビューアーは、Windows Server 2012 のサーバー管理を使用してインストール可能な、オプションの管理機能の1つとして含まれています。

修復 bde コマンドラインツールには、次の制限があります。
-   修復-bde は、暗号化または暗号化解除のプロセス中に失敗したドライブを修復できません。
-   ドライブに暗号化がある場合は、ドライブが完全に暗号化されていることを前提としています。



## <a name="syntax"></a>構文

```
repair-bde <InputVolume> <OutputVolumeorImage> [-rk] [–rp] [-pw] [–kp] [–lf] [-f] [{-?|/?}]
```

#### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|\<InputVolume>|修復する BitLocker で暗号化されたドライブのドライブ文字を指定します。 ドライブ文字にはコロンを含める必要があります。例: **C:**。|
|\<OutputVolumeorImage>|修復されたドライブの内容を保存するドライブを指定します。 出力ドライブのすべての情報が上書きされます。|
|-rk|ボリュームのロックを解除するために使用する回復キーの場所を指定します。 このコマンドは **、-recoverykey**として指定することもできます。|
|-rp|ボリュームのロックを解除するために使用する必要がある数値回復パスワードを指定します。 このコマンドは **、-recoverypassword**として指定することもできます。|
|-pw|ボリュームのロックを解除するために使用するパスワードを指定します。 このコマンドは **、パスワード**として指定することもできます。|
|-kp|ボリュームのロックを解除するために使用できる回復キーパッケージを識別します。 このコマンドは **、-keypackage**として指定することもできます。|
|-lf|修復 bde エラー、警告、および情報メッセージを格納するファイルへのパスを指定します。 このコマンドは **、-logfile**として指定することもできます。|
|-f|ボリュームをロックできない場合でも、強制的にマウントを解除します。 このコマンドは **、-force**として指定することもできます。|
|-? または /?|コマンド プロンプトでヘルプを表示します。|

## <a name="remarks"></a>Remarks

キーパッケージへのパスが指定されていない場合、**修復-bde**はドライブでキーパッケージを検索します。 ただし、ハードドライブが破損している場合は、**修復-bde**でパッケージを見つけることができず、パスを入力するように求められます。

## <a name="examples"></a>例

ドライブ C の修復を試行し、ドライブ C からドライブ D にコンテンツを書き込むには、ドライブ F に格納された回復キーファイル (RecoveryKey. bek) を使用して、ドライブ Z のログファイル (output.txt) にこの試行の結果を書き込みます。
```
repair-bde C: D: -rk F:\RecoveryKey.bek –lf Z:\log.txt
```
はドライブ C の修復を試行し、指定された48桁の回復パスワードを使用してドライブ C にコンテンツを書き込みます。 回復パスワードは、各ブロックをハイフンで区切った6桁の8つのブロックで入力する必要があります。
```
repair-bde C: D: -rp 111111-222222-333333-444444-555555-666666-777777-888888
```
ドライブ C を強制的にマウント解除し、ドライブ c の内容をドライブ c に書き込むには、ドライブ F に格納されている回復キーパッケージと回復キーファイル (RecoveryKey. bek) を使用します。
```
repair-bde C: D: -kp F:\RecoveryKeyPackage -rk F:\RecoveryKey.bek -f
```
ドライブ c の修復を試行し、ドライブ c からドライブ D にコンテンツを書き込むには、次のようにメッセージが表示されたら、C: ドライブのロックを解除するためのパスワードを入力する必要があります。
```
repair-bde C: D: -pw
```

## <a name="additional-references"></a>その他のリファレンス

-   - [コマンド ライン構文の記号](command-line-syntax-key.md)