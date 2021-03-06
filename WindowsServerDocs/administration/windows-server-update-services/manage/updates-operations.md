---
title: 更新操作
description: Windows Server Update Service (WSUS) のトピックでは、承認プロセスを含む、更新プログラムを管理する方法
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-wsus
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4cb7ff54-3014-4e91-842a-a7b831ea59ff
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4d99e006a03e12d7201390748aec8671236cf297
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59822553"
---
# <a name="updates-operations"></a>更新操作

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

、更新プログラムが WSUS サーバーに同期された後は、サーバーのクライアント コンピューターに関連性を自動的がスキャンされます。 ただし、ネットワーク上のコンピューターに展開する前に、更新プログラムを承認する必要があります。 更新プログラムを承認するときにする、基本的に、WSUS 操作を実行する (選択項目が**インストール**または**拒否**新しい更新プログラム)。 更新プログラムを承認することができます、**すべてのコンピューター**グループやサブグループの。 更新プログラムが承認されない場合は、承認の状態のまま**承認されていない**、WSUS サーバーは、クライアントがこれらの更新が必要かどうかを評価するとします。

WSUS サーバーがレプリカ モードで実行している場合、WSUS サーバーで更新プログラムを承認することができなきます。 レプリカ モードの詳細については、次を参照してください。[を実行している WSUS レプリカ モード](running-wsus-replica-mode.md)します。

## <a name="approving-updates"></a>更新プログラムの承認
WSUS ネットワーク内のすべてのコンピューターまたは別のコンピューター グループの更新プログラムのインストールを承認することができます。 更新プログラムを承認した後、次のいずれか (または複数) を行うことができます。

-   存在する場合は、この承認子グループに適用されます。

-   自動インストールの期日を設定します。 このオプションを選択するときに設定する特定の時間と日付を更新プログラムをインストールするクライアント コンピューターの設定を無効します。 さらに、すぐにインストールする、次回クライアント コンピューターが WSUS サーバーにアクセス) 更新プログラムを承認する場合は、過去の日付を期限を指定できます。

-   その更新プログラムは、削除をサポートしている場合は、インストールされている更新プログラムを削除します。

2 つの重要な考慮事項に注意する必要があります。

-   最初に、ユーザー入力は (たとえば、更新プログラムに関連する設定を指定する) 必要な場合は、更新プログラムの自動インストールの期日を設定できません。 更新プログラムがユーザー入力を求めるかどうかを判断するために見て、**ユーザー入力を要求する場合があります**フィールドに表示される更新プログラムの更新のプロパティで、**更新**ページ。 メッセージを確認しても、**更新プログラムの承認**ボックスをオンにすると、"**、選択した更新がユーザー入力が必要し、インストールの期限をサポートしていない**"。

-   WSUS サーバーのコンポーネントに更新プログラムがある場合は、WSUS の更新プログラムが承認されるまでクライアント システムに他の更新プログラムを承認することはできません。 更新プログラムの承認 ダイアログ ボックスには、この警告メッセージが表示されます。"承認されていない WSUS の更新プログラムがあります。 承認すべきこの更新プログラムを承認する前に WSUS の更新プログラム。" この場合、WSUS の更新プログラム ノードをクリックし、そのビューで更新プログラムのすべてが、一般的な更新プログラムに返す前に承認されたことを確認する必要があります。

#### <a name="to-approve-updates"></a>更新プログラムを承認するには

1.  WSUS 管理コンソールでは、次のようにクリックします。**更新**順にクリックします**すべての更新プログラム**します。

2.  更新プログラムの一覧で、承認しを右クリックし (または 操作 ウィンドウに移動キーを押す)、したい更新プログラムを選択し、更新プログラムの承認 ダイアログ ボックスで、更新プログラムを承認するコンピューター グループを選択し、その横にある矢印をクリックします。

3.  選択**インストールの承認**、 をクリックし、**承認**します。

4.  **承認の進行状況**ウィンドウは、承認の完了に向けた進行状況が表示されます。 プロセスが完了したら、**閉じる**ボタンが表示されます。 **[閉じる]** をクリックします。

5.  期限を選択するには、更新プログラムを右クリックし、適切なコンピューター グループを選択するとの横の矢印をクリックするとをクリックして**期限**します。

    -   標準の期限 (1 週間、2 週間、1 か月) のいずれかを選択またはクリックすることができます**カスタム**日付と時刻を指定します。

    -   クライアント コンピューターの連絡先、サーバーとすぐにインストールされるように更新する場合は、クリックして**カスタム**、し、日付と時刻を現在の日付と時刻に、または過去のいずれかに、設定します。

#### <a name="to-approve-multiple-updates"></a>複数の更新プログラムを承認するには

1.  WSUS 管理コンソールでは、次のようにクリックします。**更新**順にクリックします**すべての更新プログラム**します。

2.  隣接する複数の更新プログラムを選択するキーを押します。 **shift**ながら更新プログラムを選択します。 隣接しない複数の更新プログラムを選択する押し**CTRL**ながら更新プログラムを選択します。

3.  選択範囲を右クリックし、をクリックして**承認**します。 **更新プログラムの承認**ダイアログが開きます、**承認状態**に設定**の既存の承認を保持**と **[ok]** ボタンを無効にします。

4.  個々 のグループの承認規則を変更できますが、そのためには影響しません子承認。 承認を変更するグループを選択し、左側にある矢印をクリックします。 ショートカット メニューでクリックして**インストールの承認**します。

5.  選択したグループの承認に変更**インストール**します。 任意の子グループがある場合、承認のまま**既存の承認を保持**します。 子グループの承認を変更するには、グループをクリックしの左側にある矢印をクリックします。 ショートカット メニューでクリックして**の子に適用**します。

6.  親からそのすべての承認を継承するように特定の子を設定するには、[子] をクリックしの左側にある矢印をクリックします。 ショートカット メニューでクリックして**親と同じ**します。 承認を継承する子の設定、親の承認を変更しない場合は、子は、親の既存の承認を継承します。

7.  承認動作をすべての子を変更する場合は、承認**すべてのコンピューター**を選び、**の子に適用**します。

8.  クリックして**OK**すべての承認を設定した後。 **承認の進行状況**ウィンドウは、承認の完了に向けた進行状況が表示されます。 プロセスが完了したら、**閉じる**ボタンが表示されます。 **[閉じる]** をクリックします。

## <a name="declining-updates"></a>更新プログラムの拒否
このオプションを選択した場合、更新プログラムが利用可能な更新の既定の一覧から削除し、WSUS サーバーはクライアントでは、いずれかの評価またはインストールする更新プログラムが提供されません。 このオプションは、更新または更新し、右クリックするかしようとして、[操作] ウィンドウのグループを選択してアクセスできます。 拒否された更新プログラムは、選択した場合にのみ更新プログラムの一覧に表示されます**拒否済み**更新リストのフィルターを指定するときに承認一覧に**ビュー**します。

#### <a name="to-decline-updates"></a>更新プログラムを拒否するには

1.  WSUS 管理コンソールでは、次のようにクリックします。**更新**、 をクリックし、**すべての更新プログラム**。

2.  更新プログラムの一覧で、拒否する 1 つまたは複数の更新プログラムを選択します。

3.  選択**辞退**、順にクリックします**はい**確認のメッセージ。

## <a name="cleaning-up-declined-updates"></a>拒否した更新プログラムのクリーンアップ
拒否した更新プログラムは引き続き WSUS サーバー リソースを消費します。 サーバー クリーンアップ ウィザードを拒否した更新プログラムを WSUS データベースから削除を実行する必要があります。 参照トピック[サーバー クリーンアップ ウィザード](the-server-cleanup-wizard.md)、さらに詳細です。

## <a name="reinstating-declined-updates"></a>拒否した更新プログラムの再開
更新プログラムが拒否された後は、まだ再開できます。

#### <a name="to-reinstate-declined-updates"></a>拒否した更新プログラムを元に戻す

1.  WSUS 管理コンソールでは、次のようにクリックします。**更新**順にクリックします**すべての更新プログラム**します。

2.  変更**承認**に**拒否済み** をクリック**更新**します。 拒否した更新プログラムの一覧を読み込みます。

3.  更新プログラムの一覧で再開する拒否した更新プログラムが 1 つまたは複数を選択します。

4.  特定の更新プログラムを元に戻す、クリックし、更新プログラムを右クリックして**承認**します。 **更新プログラムの承認**ダイアログ ボックスで、をクリックして **[ok]** を既定の「承認されていない」の承認状態を再適用します。 更新プログラムは、として一覧に表示されます**承認されていない**拒否済みの代わりにします。

拒否された更新プログラムが WSUS サーバー クリーンアップ ウィザードを使用して、クリーンアップされた後は、WSUS サーバーから削除され、すべての更新プログラム ビューでは表示されなくします。 拒否済み、Microsoft Update カタログからのクリーンアップの更新プログラムを再インポートすることができます。 詳細については、次を参照してください。 [WSUS とカタログ サイト](wsus-and-the-catalog-site.md)します。

## <a name="change-an-approved-update-to-not-approved"></a>承認された更新プログラムに承認されていない変更します。
更新プログラムが承認されている、この時点でインストールして、将来の時刻のために保存する代わりにしないようにする場合は、承認されていない状態に更新プログラムを変更できます。 つまり、更新プログラムは利用可能な更新の既定の一覧に残りますとクライアントのコンプライアンスが報告されますが、クライアントではインストールされません。

#### <a name="to-change-an-update-from-approved-to-not-approved"></a>承認されていないことを承認されてから更新プログラムを変更するには

1.  WSUS 管理コンソールでは、次のようにクリックします。**更新**、 をクリックし、**すべての更新プログラム**。

2.  更新プログラムの一覧で承認されていないを変更する承認済み更新プログラムが 1 つまたは複数を選択します。

3.  ショートカット メニューで、または**アクション**ペインで、**承認されていない**、順にクリックします**はい**確認のメッセージ。

## <a name="approving-updates-for-removal"></a>削除する更新プログラムを承認します。
削除用の更新プログラムを承認することができます (つまり、既にインストールされている更新をアンインストールする)。 このオプションは、更新プログラムが既にインストールされているし、削除をサポートしている場合にのみ使用します。 アンインストールする更新プログラムの期限を指定したり、更新をすぐに (クライアント コンピューターに WSUS サーバーにお問い合わせください [次へ] の時刻) を削除する場合に、期限を過去の日付を指定できます。

すべての更新プログラムが削除をサポートすることは言うまでも重要になります。 更新プログラムが個々 の更新プログラムを選択し、見ての削除をサポートしているかどうかを参照してください、**詳細**ウィンドウ。 **詳細**が表示されます、**リムーバブル**カテゴリ。 WSUS を介して更新プログラムを削除できない場合によってが削除される場合**を追加または削除プログラム**から**コントロール パネルの **します。

#### <a name="to-approve-updates-for-removal"></a>更新プログラムの削除を承認するには

1.  WSUS 管理コンソールでは、次のようにクリックします。**更新**順にクリックします**すべての更新プログラム**します。

2.  更新プログラムの一覧で、削除を承認して右クリックしする 1 つまたは複数の更新プログラムを選択します (を参照するか、**アクション**ウィンドウ)。

3.  **更新プログラムの承認**ダイアログ ボックスで、更新プログラムを削除するコンピューター グループを選択し、その横にある矢印をクリックします。

4.  選択**削除が承認**、順にクリックします、**削除**ボタンをクリックします。

5.  削除の承認が完了したら後、は、更新プログラムをもう一度右クリックし、適切なコンピューター グループを選択し、その横にある矢印をクリックして、期限を選択できます。 選び**期限**します。 標準の期限 (1 週間、2 週間、1 か月) のいずれかを選択する場合がありますまたはクリックすることができます**カスタム**を特定の日付と時刻を選択します。

6.  クライアント コンピューターの連絡先、サーバーとすぐに削除する更新プログラムを実行する場合に、クリックして**カスタム**過去の日付を設定します。

## <a name="approving-updates-automatically"></a>更新プログラムを自動的に承認します。
特定の更新プログラムの自動承認の WSUS サーバーを構成することができます。 利用可能になった既存の更新プログラムに対する改訂の自動承認を指定することもできます。 既定では、このオプションはオンです。 リビジョンがこれに加えられた変更を持つ更新プログラムのバージョン (期限切れ場合がありますが、またはその適用性ルールが変更された可能性など)。 更新プログラムの改訂版を自動的に承認しない場合は、WSUS は、旧バージョンを使用し、更新プログラムの改訂版を手動で承認する必要があります。

同期中に、WSUS サーバーを自動的に適用するルールを作成することができます。 インストール、更新プログラムの分類、製品、およびコンピューター グループを自動的に承認する更新プログラムを指定します。 これは、改訂された更新プログラムではなく、新しい更新プログラムにのみ適用されます。 日数の値と、承認済み更新プログラムが期限インストールする前にオファリングの特定の時間を設定する、更新プログラム承認期限を指定することもできます。 これらの設定が表示されます、**オプション** ウィンドウで、**自動承認**します。

#### <a name="to-automatically-approve-updates"></a>更新プログラムを自動的に承認するには

1.  WSUS 管理コンソールで、次のようにクリックします。**オプション**、 をクリックし、**自動承認**します。

2.  **[更新規則]** で、 **[新しい規則]** をクリックします。

3.  **規則の追加**ダイアログ **手順 1: プロパティを選択します**を使用するかどうかを選択**更新プログラムが特定の分類の場合に**または**更新特定の製品で**(または両方) の条件として。 必要に応じて、選択するかどうか**期限を設定**承認します。

4.  **手順 2: プロパティを編集**分類、製品、および該当する場合、自動承認規則の対象となるコンピューター グループを選択する下線付きのプロパティ をクリックします。 更新プログラムの承認を必要に応じて、選択期限の日付と時刻。

5.  **手順 3。指定名ボックス**規則の一意の名前を入力します。

6.  **[OK]** をクリックします。

自動承認規則は、更新プログラムがまだ同意されていないサーバーでエンドユーザー ライセンス契約 (EULA) を必要とするのには適用されません。 自動承認規則を適用することも承認に関連するすべての更新プログラムは発生しませんを検索する場合は、これらの更新プログラムを手動で承認する必要があります。

## <a name="automatically-approving-revisions-to-updates-and-declining-expired-updates"></a>期限切れ更新プログラムを自動的に更新プログラムに対する改訂の承認と拒否
[オプション] ウィンドウの自動承認」セクションには、自動的に承認済み更新プログラムに対する改訂の承認を既定のオプションが含まれています。 有効期限が切れた更新プログラムを自動的に拒否するように WSUS サーバーを設定することもできます。 を自動的に更新プログラムの改訂版を承認しないように選択する場合、WSUS サーバーが以前のバージョンを使用し、更新プログラムの改訂版を手動で承認する必要があります。

> [!NOTE]
> リビジョンが変更された更新プログラムのバージョン (たとえば、期限が切れている可能性がありますまたは適用性ルールを更新) します。

#### <a name="to-automatically-approve-revisions-to-updates-and-decline-expired-updates"></a>期限切れの更新プログラムを自動的に更新プログラムに対する改訂の承認および拒否するには

1.  WSUS 管理コンソールで、次のようにクリックします。**オプション**、 をクリックし、**自動承認**します。

2.  **詳細設定**  タブで、必ず両方**新しい承認済み更新プログラムの改訂版を自動的に承認**と**新しいリビジョンが切れになるときに自動的に更新プログラムの拒否**が選択されています。

3.  [OK] をクリックします。

    > [!NOTE]
    > これらのオプションの既定値を維持するには、WSUS ネットワーク上で優れたパフォーマンスを維持するが使用できます。 期限切れの更新プログラムを自動的に拒否するしたくない場合は定期的にそれらを手動で拒否することを確認する必要があります。

## <a name="automatically-declining-superseded-updates"></a>置き換えられる更新プログラムを自動的に拒否
自動的に承認した既存の更新を優先する新しい更新プログラムを承認するときに置き換えられる更新プログラムになります「該当しない」コンピューターまたはデバイスにしたら、新しい更新プログラムがインストールされています。 すべてのコンピューターの更新プログラムが該当なし、WSUS コンソールで確認できます。 更新は安全に拒否できます。 さらに、更新プログラムが自動的を拒否する WSUS サーバー クリーンアップ ウィザードを実行するときに。

置き換えられた更新プログラムを検索するには、すべての更新プログラム ビュー、およびその列の並べ替えで「優先」のフラグ列を選択できます。 4 つのグループがあります。

-   更新されていることはありません (空白のアイコン) を置き換えます。

-   置き換えられたことはありませんが、更新プログラムは、別の更新プログラム (下部にある青い四角形のアイコン) を置き換えます。

-   置き換えられたし、別の更新プログラム (中央の青い四角形のアイコン) が置き換えられる更新。

-   別の更新プログラム (上部にある青い四角形のアイコン) が置き換えられる更新プログラム。

自動的に拒否置き換えられる更新プログラムの新しい更新プログラムを承認されると、Windows Server Update Services の機能はありません。 最初に、承認されていない"、"承認に設定し、サーバー クリーンアップ ウィザードを使用して、関連するすべての条件が満たされたときに自動的に更新プログラムを拒否することをお勧めします。 詳しくは、次のトピックをご覧ください。[サーバー クリーンアップ ウィザード](the-server-cleanup-wizard.md)します。

## <a name="approving-superseding-or-superseded-updates"></a>または優先される更新プログラムの承認
通常、他の更新プログラムを優先する更新プログラムは、次の 1 つ以上を行います。

-   機能強化、改良、または以前にリリースされた 1 つ以上の更新プログラムで提供される修正への機能追加。

-   更新プログラムのインストールが承認された場合、クライアント コンピューターにインストールされる更新プログラム ファイル パッケージの効率を改善します。 たとえば、置き換えられる更新プログラムに、修正、新しい更新プログラムでサポートするオペレーティング システムに関連しないファイルが含まれることがあるため、これらのファイルは置き換える方の更新プログラムのファイル パッケージには含まれません。

-   新しいバージョンのオペレーティング システムを更新します。 また、優先する更新プログラムが以前のバージョンのオペレーティング システムをサポートしていないことに注意してください。 重要です。

逆に、別の更新によって置き換えられる更新プログラムは、次を行います。

-   優先する更新プログラムのような問題を修正します。 ただし、優先する更新プログラムが置き換えられる更新プログラムを提供する修正プログラムを強化する可能性があります。

-   以前のバージョンのオペレーティング システムを更新します。 場合によっては、これらのバージョンのオペレーティング システムは、優先する更新プログラムによって更新されません。

個々 の更新プログラムの詳細 ウィンドウに、情報アイコンをクリックし、上部にメッセージよりも優先されますがいずれかまたは別の更新によって置き換えられることを示します。 さらに、更新プログラムは、置き換えるか、調べることで、更新プログラムによって置き換えられるを判断できます、**この更新プログラムを置き換える更新プログラム**と**この更新プログラムによって置き換えられる更新**エントリ、 **詳細**のセクション、**プロパティ**します。 更新プログラムの一覧の下で、更新プログラムの詳細ペインが表示されます。

WSUS では自動的に拒否し、置き換えられた更新プログラムは拒否されます、優先する更新プログラムを想定しないことをお勧めします。 置き換えられる更新プログラムを拒否する前に、クライアント コンピューターのいずれかが必要ですがなくなったらになっていることを確認します。 次に、置き換えられる更新プログラムをインストールする必要がありますのシナリオの例を示します。

-   以前のバージョンのオペレーティング システムを実行、クライアント コンピューターの一部を優先する更新プログラムがのみ新しいバージョン、オペレーティング システムをサポートする場合。

-   優先する更新プログラムが、更新プログラムよりも適用性をより制限されている場合の後継となります、これとしても、一部のクライアント コンピューターで不適切です。

-   以前にリリースされた更新プログラムは、不要になった新しい変更のために優先する更新プログラム。 場合、 各リリースでの変更を優先する更新プログラム不要になった以前のバージョンで以前置き換えられる更新プログラムが可能性があります。 このシナリオでは、場合でも、優先する更新プログラムにはない更新プログラムによって置き換えられたが、置き換えられる更新プログラムに関するメッセージを引き続き表示されます。


