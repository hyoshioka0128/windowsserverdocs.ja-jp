---
title: chkntfs
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 93eca810-8699-4716-8e9d-aecd54f704be
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 876c0e0c254216ac217aea7d165d5f4e3a7da9b4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861993"
---
# <a name="chkntfs"></a>chkntfs



表示またはチェックは、コンピューターの起動時に自動のディスクを変更します。 オプションを指定せずに使用する場合**chkntfs**指定されたボリュームのファイル システムが表示されます。 を実行するファイルの自動チェックがスケジュールされている場合**chkntfs**が表示されますが、指定されたボリュームがダーティまたはされる予定だかどうかチェック、次回コンピューターを起動します。

> [!NOTE]
> 実行する**chkntfs**、Administrators グループのメンバーがあります。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
chkntfs <Volume> [...]
chkntfs [/d]
chkntfs [/t[:<Time>]]
chkntfs [/x <Volume> [...]]
chkntfs [/c <Volume> [...]]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<ボリューム > [...]|コンピューターが起動を確認する 1 つまたは複数のボリュームを指定します。 有効なボリュームには、ドライブ文字 (コロンに続く) が含まれます。 マウント ポイント、またはボリュームの名前。|
|/d|すべて復元**chkntfs**既定のファイルの自動チェックのカウント ダウン時間以外に設定します。 コンピューターが開始されると、既定では、すべてのボリュームがチェックされて、 **chkdsk**がダーティに実行されます。|
|/t [:\<Time>]|Autochk.exe 開始のカウント ダウン時間を秒単位で指定された時間数に変更します。 時刻を入力しない場合 **/t**現在のカウント ダウン時間が表示されます。|
|/x\<ボリューム > [...]|コンピューターの起動時にボリュームが必要であるとマークされている場合でものチェックから除外する 1 つまたは複数のボリュームを指定します**chkdsk**します。|
|/c\<ボリューム > [...]|コンピューターが起動し、実行する場合にチェックする 1 つまたは複数のボリュームをスケジュール**chkdsk**ダーティにあるものにします。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="BKMK_examples"></a>例

ドライブ C のファイル システムの種類を表示するには、次のように入力します。
```
chkntfs c:
```
次の出力では、NTFS ファイル システムを示します。
```
The type of the file system is NTFS.
```

> [!NOTE]
> ファイルの自動チェックが実行をスケジュールに追加の出力が表示されます、チェックを示す、ドライブがダーティか手動で設定されているかどうかスケジュールを次回コンピューターを起動します。

Autochk.exe 開始カウント ダウン時間を表示するには、次のように入力します。
```
chkntfs /t
```
たとえば、カウント ダウン時間が 10 秒に設定されている場合、次の出力が表示されます。
```
The AUTOCHK initiation countdown time is set to 10 second(s).
```
Autochk.exe 開始のカウント ダウン時間を 30 秒に変更するに次のように入力します。
```
chkntfs /t:30
```

> [!NOTE]
> Autochk.exe 開始のカウント ダウン時間を 0 に設定することができますが、できなく時間がかかる可能性があるファイルの自動チェックをキャンセルします。

**/X**コマンド ライン オプションは、累積することはできません。 複数回入力する場合、最新のエントリには、前のエントリが上書きされます。 チェック対象から、複数のボリュームを除外するには、1 つのコマンドで各を一覧表示する必要があります。 たとえば、D および E の両方のボリュームを除外する次のように入力します。
```
chkntfs /x d: e:
```
**/C**コマンド ライン オプションが累積されます。 入力した場合 **/c**各エントリが 2 回以上残ります。 特定のボリュームだけがチェックされていることを確認するには、既定値は、前のすべてのコマンドをクリアして、チェック対象からすべてのボリュームを除外をリセットし、目的のボリュームで自動ファイル確認をスケジュールします。

たとえば、自動ファイル D ボリュームが C または E のボリュームではない確認をスケジュールするには、順序で、次のコマンドを入力します。
```
chkntfs /d
chkntfs /x c: d: e:
chkntfs /c d:
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)