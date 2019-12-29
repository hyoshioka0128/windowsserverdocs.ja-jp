---
title: repair-bde
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 534dca1a-05f7-4ea8-ac24-4fe5f14f988a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 817e5fb5cf032376ddfddb3a54f73411ac175def
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384554"
---
# <a name="repair-bde"></a>repair-bde



BitLocker を使用してドライブが暗号化されている場合は、重大な損傷を受けたハードディスク上の暗号化されたデータにアクセスします。 有効な回復パスワードまたは回復キーを使用してデータの暗号化が解除されるなら、repair-bde はドライブの重要な部分を再構築して、回復可能なデータを修復できます。 ドライブの BitLocker メタデータ データが破損した場合は、回復パスワードまたは回復キーに加えて、バックアップ キー パッケージを提供できる必要があります。 Active Directory ドメイン サービス (AD DS) バックアップの既定の設定を使用した場合、このキー パッケージは AD DS にバックアップされます。 このキー パッケージと回復パスワードまたは回復キーを使用すると、ディスクが破損した場合でも、BitLocker で保護されたドライブの部分の暗号化を解除できます。 各キー パッケージは、対応するドライブ識別子があるドライブに対してのみ動作します。 [Active Directory の BitLocker 回復パスワードビューアー](https://technet.microsoft.com/library/dd875531(v=ws.10).aspx)を使用して、AD DS からこのキーパッケージを取得できます。

> [!NOTE]
> BitLocker 回復パスワードビューアーは、Windows Server 2012 のサーバー管理を使用してインストール可能な、オプションの管理機能の1つとして含まれています。

修復 bde コマンドラインツールには、次の制限があります。
-   修復-bde は、暗号化または暗号化解除のプロセス中に失敗したドライブを修復できません。
-   ドライブに暗号化がある場合は、ドライブが完全に暗号化されていることを前提としています。

このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
repair-bde <InputVolume> <OutputVolumeorImage> [-rk] [–rp] [-pw] [–kp] [–lf] [-f] [{-?|/?}]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<InputVolume >|修復する BitLocker で暗号化されたドライブのドライブ文字を指定します。 ドライブ文字にはコロンを含める必要があります。例えば：**C:** 。|
|\<OutputVolumeorImage >|修復されたドライブの内容を保存するドライブを指定します。 出力ドライブのすべての情報が上書きされます。|
|-rk|ボリュームのロックを解除するために使用する回復キーの場所を指定します。 このコマンドは **、-recoverykey**として指定することもできます。|
|-rp|ボリュームのロックを解除するために使用する必要がある数値回復パスワードを指定します。 このコマンドは **、-recoverypassword**として指定することもできます。|
|-pw|ボリュームのロックを解除するために使用するパスワードを指定します。 このコマンドは **、パスワード**として指定することもできます。|
|-kp|ボリュームのロックを解除するために使用できる回復キーパッケージを識別します。 このコマンドは **、-keypackage**として指定することもできます。|
|-lf|修復 bde エラー、警告、および情報メッセージを格納するファイルへのパスを指定します。 このコマンドは **、-logfile**として指定することもできます。|
|-f|ボリュームをロックできない場合でも、強制的にマウントを解除します。 このコマンドは **、-force**として指定することもできます。|
|-? または /?|コマンド プロンプトでヘルプを表示します。|

## <a name="remarks"></a>コメント

キーパッケージへのパスが指定されていない場合、**修復-bde**はドライブでキーパッケージを検索します。 ただし、ハードドライブが破損している場合は、**修復-bde**でパッケージを見つけることができず、パスを入力するように求められます。

## <a name="BKMK_Examples"></a>例

次の例では、ドライブ C の修復を試み、ドライブ C からドライブ D にコンテンツを書き込みます。ドライブ F に格納されている回復キーファイル (RecoveryKey) を使用して、この試行の結果をドライブ Z のログファイル (output.txt) に書き込みます。
```
repair-bde C: D: -rk F:\RecoveryKey.bek –lf Z:\log.txt
```
次の例では、ドライブ C の修復を試行し、指定された48桁の回復パスワードを使用してドライブ C にコンテンツを書き込みます。 回復パスワードは、各ブロックをハイフンで区切った6桁の8つのブロックで入力する必要があります。
```
repair-bde C: D: -rp 111111-222222-333333-444444-555555-666666-777777-888888
```
次の例では、ドライブ c をマウント解除してからドライブ c の修復を試行し、ドライブ F に格納されている回復キーパッケージと回復キーファイル (RecoveryKey) を使用してドライブ c にコンテンツを書き込みます。
```
repair-bde C: D: -kp F:\RecoveryKeyPackage -rk F:\RecoveryKey.bek -f
```
次の例では、ドライブ c の修復を試行し、ドライブ C からドライブ D にコンテンツを書き込みます。ドライブ C: のロックを解除するためのパスワードを入力する必要があります。
```
repair-bde C: D: -pw
```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンド ライン構文の記号](command-line-syntax-key.md)