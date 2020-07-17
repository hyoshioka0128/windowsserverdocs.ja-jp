---
title: fsutil usn
description: Update Sequence Number (USN) 変更ジャーナルを管理する fsutil usn コマンドのリファレンス記事です。
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
ms.assetid: faad34aa-4ba1-4129-bc1f-08088399e2fa
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: b3f71588c7221f0ba8e3659d9a1a1dd133971ce9
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85930475"
---
# <a name="fsutil-usn"></a>fsutil usn

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8

Update Sequence Number (USN) 変更ジャーナルを管理します。 USN 変更ジャーナルは、ボリューム上のファイルに加えられたすべての変更の永続的なログを提供します。 ファイル、ディレクトリ、およびその他の NTFS オブジェクトが追加、削除、および変更されると、NTFS によって、コンピューター上のボリュームごとに1つずつ、レコードが USN 変更ジャーナルに入力されます。 レコードはそれぞれ、変更の種類と変更されたオブジェクトを示します。 ストリームの末尾に新しいレコードが追加されます。

## <a name="syntax"></a>構文

```
fsutil usn [createjournal] m=<maxsize> a=<allocationdelta> <volumepath>
fsutil usn [deletejournal] {/d | /n} <volumepath>
fsutil usn [enablerangetracking] <volumepath> [options]
fsutil usn [enumdata] <fileref> <lowUSN> <highUSN> <volumepath>
fsutil usn [queryjournal] <volumepath>
fsutil usn [readdata] <filename>
fsutil usn [readjournal] [c= <chunk-size> s=<file-size-threshold>] <volumepath>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| createjournal | USN 変更ジャーナルを作成します。 |
| m =`<maxsize>` | NTFS によって変更ジャーナルに割り当てられる最大サイズをバイト単位で指定します。 |
| a =`<allocationdelta>` | 最後に追加され、変更ジャーナルの先頭から削除されるメモリ割り当てのサイズ (バイト単位) を指定します。 |
| `<volumepath>` | ドライブ文字を指定します (その後にコロンが続きます)。 |
| deletejournal | アクティブな USN 変更ジャーナルを削除または無効にします。<p>**注意:** 変更ジャーナルを削除すると、ファイルレプリケーションサービス (FRS) とインデックスサービスに影響します。これは、これらのサービスがボリュームの完全な (および時間のかかる) スキャンを実行する必要があるためです。 これは、FRS SYSVOL レプリケーションに悪影響を及ぼし、ボリュームの再スキャン中に、DFS リンク間のレプリケーションを交互に切り替えます。 |
| /d | アクティブな USN 変更ジャーナルを無効にし、変更ジャーナルを無効にしている間に入出力 (i/o) コントロールを返します。 |
| /n | アクティブな USN 変更ジャーナルを無効にし、変更ジャーナルが無効になった後にのみ i/o 制御を返します。 |
| enablerangetracking | ボリュームの USN 書き込み範囲の追跡を有効にします。 |
| c =`<chunk-size>` | ボリューム上で追跡するチャンクサイズを指定します。 |
| s =`<file-size-threshold>` | 範囲追跡のファイルサイズのしきい値を指定します。 |
| enumdata | 指定した2つの境界間の変更ジャーナルエントリを列挙して一覧表示します。 |
| `<fileref>` | 列挙を開始するボリューム上のファイル内の位置を示す序数を指定します。 |
| `<lowUSN>` | 返されるレコードをフィルター処理するために使用される USN 値の範囲の下限を指定します。 最後の変更ジャーナル USN が*lowusn*および*highusn*メンバーの値以下であるレコードのみが返されます。 |
| `<highUSN>` | 返されるファイルをフィルター処理するために使用する USN 値の範囲の上限を指定します。 |
| queryjournal | ボリュームの USN データを照会して、現在の変更ジャーナル、そのレコード、およびその容量に関する情報を収集します。 |
| readdata | ファイルの USN データを読み取ります。 |
| `<filename>` | ファイル名と拡張子を含むファイルへの完全パスを指定します (例: *C:\documents\filename.txt*)。 |
| readjournal | USN ジャーナル内の USN レコードを読み取ります。 |
| minver =`<number>` | 返される USN_RECORD の最小メジャーバージョン。 既定値は2です。 |
| maxver =`<number>` | 返す USN_RECORD の最大メジャーバージョン。 既定値は4です。 |
| startusn =`<USN number>` | USN ジャーナルの読み取りを開始する USN。 既定値は 0 です。 |

#### <a name="remarks"></a>注釈

- プログラムは USN 変更ジャーナルを参照して、一連のファイルに加えられたすべての変更を確認できます。 USN 変更ジャーナルは、タイムスタンプをチェックしたり、ファイル通知を登録したりするよりもはるかに効率的です。 USN 変更ジャーナルは、インデックスサービス、ファイルレプリケーションサービス (FRS)、リモートインストールサービス (RIS)、およびリモートストレージによって有効にされ、使用されます。

- 変更ジャーナルがボリュームに既に存在する場合は、 **createjournal**パラメーターによって変更ジャーナルの**maxsize**および割り当て**デルタ**パラメーターが更新されます。 これにより、アクティブなジャーナルで保持されるレコードの数を拡張して、無効にすることができます。

- 変更ジャーナルはこのターゲット値よりも大きくなる可能性がありますが、変更ジャーナルは次の NTFS チェックポイントで切り捨てられ、この値より小さくなります。 NTFS は、変更ジャーナルを調べて、サイズが**maxsize**の値と割り当て**デルタ**の値を超えたときにトリミングします。 Ntfs チェックポイントでは、オペレーティングシステムは ntfs ログファイルにレコードを書き込みます。これにより、NTFS は、障害からの復旧に必要な処理を特定できます。

- 変更ジャーナルは、切り捨てられる前に、 **maxsize**と割り当て**デルタ**の値の合計より大きくなることがあります。

- アクティブな変更ジャーナルを削除または無効化するには、非常に時間がかかります。これは、システムがマスターファイルテーブル (MFT) 内のすべてのレコードにアクセスし、last USN 属性を 0 (ゼロ) に設定する必要があるためです。 この処理には数分かかることがあり、再起動が必要な場合は、システムの再起動後に続行できます。 このプロセスでは、変更ジャーナルはアクティブと見なされず、無効になります。 システムがジャーナルを無効にしている間はアクセスできず、すべてのジャーナル操作でエラーが返されます。 アクティブなジャーナルを無効にする場合は、ジャーナルを使用している他のアプリケーションに悪影響を及ぼすため、細心の注意を払ってください。

### <a name="examples"></a>例

ドライブ C に USN 変更ジャーナルを作成するには、次のように入力します。

```
fsutil usn createjournal m=1000 a=100 c:
```

ドライブ C のアクティブな USN 変更ジャーナルを削除するには、次のように入力します。

```
fsutil usn deletejournal /d c:
```

指定されたチャンクサイズとファイルサイズのしきい値で範囲の追跡を有効にするには、次のように入力します。

```
fsutil usn enablerangetracking c=16384 s=67108864 C:
```

C ドライブの指定した2つの境界の間にある変更ジャーナルエントリを列挙して一覧表示するには、次のように入力します。

```
fsutil usn enumdata 1 0 1 c:
```

ドライブ C のボリュームの USN データを照会するには、次のように入力します。

```
fsutil usn queryjournal c:
```

ドライブ C の \Temp フォルダーにあるファイルの USN データを読み取るには、次のように入力します。

```
fsutil usn readdata c:\temp\sample.txt
```

特定の開始 USN を持つ USN ジャーナルを読み取るには、次のように入力します。

```
fsutil usn readjournal startusn=0xF00
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [fsutil](fsutil.md)
