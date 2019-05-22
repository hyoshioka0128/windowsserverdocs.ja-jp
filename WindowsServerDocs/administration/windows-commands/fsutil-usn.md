---
ms.assetid: faad34aa-4ba1-4129-bc1f-08088399e2fa
title: fsutil usn
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 4bef63f4938b5ce786bbbfdbf3bdd2081280ce95
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829983"
---
# <a name="fsutil-usn"></a>fsutil usn
>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8、Windows Server 2008 R2、Windows 7

更新シーケンス番号 (USN) 変更ジャーナルを管理します。

## <a name="syntax"></a>構文

```
fsutil usn [createjournal] m=<MaxSize> a=<AllocationDelta> <VolumePath>
fsutil usn [deletejournal] {/D | /N} <volumepath>
fsutil usn [enablerangetracking] <volumepath> [options]
fsutil usn [enumdata] <FileRef> <LowUSN> <HighUSN> <VolumePath>
fsutil usn [queryjournal] <VolumePath>
fsutil usn [readdata] <FileName>
fsutil usn [readjournal] [c= <chunk-size> s=<file-size-threshold>] <volumepath>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------------|---------------|
|createjournal|USN 変更ジャーナルを作成します。|
|m =\<MaxSize >|NTFS が、変更ジャーナルの割り当てをバイト単位で最大のサイズを指定します。|
|=\<AllocationDelta >|末尾に追加され、変更ジャーナルの先頭から削除されるメモリの割り当てのバイト単位のサイズを指定します。|
|\<VolumePath >|ドライブ文字 (コロンに続く) を指定します。|
|deletejournal|削除またはアクティブな USN 変更ジャーナルを無効にします。 **注:** ボリュームの完全な (と時間のかかる) のスキャンを実行するこれらのサービスが必要になるために、ファイル レプリケーション サービス (FRS) とインデックス サービスに影響変更ジャーナルを削除します。 これはさらに悪い、FRS SYSVOL レプリケーションと DFS リンクの代替中に、ボリュームがスキャンされている間のレプリケーションに影響します。|
|/d|アクティブな USN 変更ジャーナルを無効にし、変更ジャーナルを無効にされている入力/出力 (I/O) の制御が返されます。|
|/n|アクティブな USN 変更ジャーナルを無効にし、変更ジャーナルが無効になった後にのみ、I/O のコントロールを返します。|
|enablerangetracking|USN 書き込み範囲が、ボリュームの追跡を有効にします。|
|c=\<chunk-size>|ボリュームに追跡するために、チャンク サイズを指定します。|
|s=\<file-size-threshold>|追跡の範囲のファイル サイズのしきい値を指定します。|
|enumdata|列挙し、2 つの指定した境界の間の変更ジャーナルのエントリを一覧表示されます。|
|\<FileRef >|列挙体が開始されるボリューム上のファイル内の位置を表す序数を指定します。|
|\<LowUSN >|返されるレコードをフィルター処理するために使用する範囲の USN 値の下限の境界を指定します。 最終変更ジャーナルの USN レコードのみが間、または等しく、 *LowUSN*と*HighUSN*メンバーの値が返されます。|
|\<HighUSN >|返されるファイルをフィルター処理するために使用する範囲の USN 値の上限の境界を指定します。|
|queryjournal|現在の変更ジャーナル、そのレコードでは、その容量に関する情報を収集するために、ボリュームの USN データを照会します。|
|readdata|ファイルの USN データを読み取ります。|
|\<FileName>|たとえば、ファイル名と拡張子を含む、ファイルへの完全パスを指定します。C:\documents\filename.txt|
|readjournal|USN ジャーナルで USN のレコードを読み取ります。|
|minver =\<番号 >|返す USN_RECORD の最小値メジャー バージョン。 既定値 = 2 です。|
|maxver =\<番号 >|返す USN_RECORD の最大のメジャー バージョン。 既定値 = 4 です。|
|startusn =\<USN 番号 >|USN から USN ジャーナルの読み取りを開始します。 既定 = 0。|


## <a name="remarks"></a>注釈

-   USN 変更ジャーナルについて

    USN 変更ジャーナルでは、ボリューム上のファイルに加えられたすべての変更の永続的なログを提供します。 ファイル、ディレクトリ、およびその他の NTFS オブジェクトが追加、削除、および変更と、NTFS は、コンピューター上のボリュームごとに 1 つずつ、USN 変更ジャーナルにレコードを入力します。 レコードはそれぞれ、変更の種類と変更されたオブジェクトを示します。 ストリームの末尾には、新しいレコードが追加されます。

    プログラムは、一連のファイルに加えられたすべての変更を決定する、USN 変更ジャーナルを参照してください。 USN 変更ジャーナルは、タイムスタンプの確認やファイルの通知の登録よりもはるかに効率的です。 USN 変更ジャーナルでは、有効になっているされ、インデックス サービス、ファイル レプリケーション サービス (FRS)、リモート インストール サービス (RIS) とリモート記憶域で使用することができます。

-   使用して**createjournal**

    変更ジャーナルはボリュームに既に存在する場合、 **createjournal**パラメーターの更新、変更ジャーナルの*MaxSize*と*AllocationDelta*パラメーター。 これにより、無効にすることがなく作業中のジャーナルを保持するレコードの数を拡張することができます。

-   使用して**m**

    変更ジャーナルは、この対象の値よりも大きくできますが、変更ジャーナルがこの値より小さくする次の NTFS のチェックポイントで切り捨てられます。 NTFS が、変更ジャーナルに調べの値を超えた場合、トリム*MaxSize*の値プラス*AllocationDelta*します。 NTFS のチェックポイントでは、オペレーティング システムは、どのような処理は、障害から復旧するために必要かを判断する NTFS を有効にする NTFS ログ ファイルにレコードを書き込みます。

-   使用して ****

    変更ジャーナルの複数の値の合計の拡張可能*MaxSize*と*AllocationDelta*を削除する対象の前にします。

-   使用して**deletejournal**

    削除またはアクティブな変更ジャーナルを無効にするとは非常に時間がかかり、システムのマスター ファイル テーブル (MFT) 内のすべてのレコードへのアクセスし、0 (ゼロ) に最後の USN 属性を設定する必要があります。 このプロセスは数分かかるし、再起動が必要なシステムが再起動した後に続行できます。 このプロセス中に変更ジャーナルがアクティブと見なされないも無効にされています。 システムが履歴を無効にするときにアクセスできないし、journal のすべての操作がエラーを返します。 悪影響を与える、ジャーナルを使用している他のアプリケーションに影響するので、active、journal では、無効にする場合に、細心の注意を使用してください。

## <a name="BKMK_examples"></a>例
作成には、USN は、ジャーナル ドライブ C の型を変更します。

```
fsutil usn createjournal m=1000 a=100 c:
```

アクティブなを削除するのには、USN は、ジャーナル ドライブ C の型を変更します。

```
fsutil usn deletejournal /d c:
```

範囲指定チャンク サイズのファイル サイズのしきい値と追跡を有効にするには、次のように入力します。

```
fsutil usn enablerangetracking c=16384 s=67108864 C:
```

列挙をドライブ C 上の 2 つの指定した境界の間の変更ジャーナルのエントリの一覧は、次のように入力します。

```
fsutil usn enumdata 1 0 1 c:
```

ドライブ C 上のボリュームに USN のデータを照会するには、次のように入力します。

```
fsutil usn queryjournal c:
```

USN のデータを C ドライブの \Temp フォルダにあるファイルを読み取り、次のように入力します。

```
fsutil usn readdata c:\temp\sample.txt
```

特定の開始の USN と USN ジャーナルを読み取り、次のように入力します。

```
fsutil usn readjournal startusn=0xF00
```

#### <a name="additional-references"></a>その他の参照情報
[コマンドライン構文キー](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)


