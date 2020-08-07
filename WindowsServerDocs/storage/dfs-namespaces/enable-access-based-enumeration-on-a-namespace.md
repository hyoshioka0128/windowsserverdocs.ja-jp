---
title: 名前空間でアクセス ベースの列挙を有効にする
description: この記事では、名前空間でアクセス ベースの列挙を有効にする方法について説明します。
ms.date: 6/5/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 507af0f3cdd76ab7af59092f8f099225c113edaa
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87936126"
---
# <a name="enable-access-based-enumeration-on-a-namespace"></a>名前空間でアクセス ベースの列挙を有効にする

> 適用対象: Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

アクセス ベースの列挙では、ユーザーがアクセス許可を持たないファイルとフォルダーが非表示になります。 既定では、DFS 名前空間ではこの機能が有効になっていません。 DFS 管理を使って、DFS フォルダーのアクセス ベースの列挙を有効にすることができます。 フォルダー ターゲット内のファイルとフォルダーのアクセス ベースの列挙を制御するには、共有と記憶域の管理を使って各共有フォルダーでアクセス ベースの列挙を有効にする必要があります。

名前空間でアクセス ベースの列挙を有効にするには、すべての名前空間サーバーで Windows Server 2008 以降が実行されている必要があります。 さらに、ドメイン ベースの名前空間では Windows Server 2008 モードを使う必要があります。 Windows Server 2008 モードの要件について詳しくは、「[名前空間の種類を選択する](choose-a-namespace-type.md)」をご覧ください。

一部の環境では、アクセス ベースの列挙を有効にすると、サーバーの CPU 使用率が高くなり、ユーザーの応答時間が遅くなります。

> [!NOTE]
> 既存のドメイン ベースの名前空間があるときにドメインの機能レベルを Windows Server 2008 にアップグレードする場合、DFS 管理を使うとこれらの名前空間でアクセス ベースの列挙を有効にできます。 ただし、名前空間を Windows Server 2008 モードに移行する場合を除き、グループまたはユーザーからフォルダーを非表示にするアクセス許可を編集することはできません。 詳しくは、「[ドメイン ベースの名前空間を Windows Server 2008 モードに移行する](migrate-a-domain-based-namespace-to-windows-server-2008-mode.md)」をご覧ください。


DFS 名前空間でアクセス ベースの列挙を使うには、以下の手順を実行する必要があります。

-   名前空間でアクセス ベースの列挙を有効にする
-   個々の DFS フォルダーを表示できるユーザーとグループを制御する


> [!WARNING]
> アクセス ベースの列挙を有効にしても、ユーザーが DFS パスを既に知っている場合、フォルダー ターゲットへの紹介の取得を禁止できません。 フォルダー ターゲット (共有フォルダー) 自体の共有アクセス許可または NTFS ファイル システム アクセス許可のみ、ユーザーによるフォルダー ターゲットへのアクセスを禁止できます。 DFS フォルダーのアクセス許可は、アクセスを制御するためではなく、DFS フォルダーを表示または非表示にするためにのみ使用します。読み取りアクセスが、DFS フォルダー レベルにのみ関係するアクセス許可になります。 詳しくは、「[継承されたアクセス許可とアクセス ベースの列挙を使う](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd834874(v=ws.11))」をご覧ください。

<br />
アクセス ベースの列挙は、Windows インターフェイスを使うかコマンド ラインを使って、名前空間で有効にできます。

## <a name="to-enable-access-based-enumeration-by-using-the-windows-interface"></a>Windows インターフェイスを使ってアクセス ベースの列挙を有効にするには

1.  コンソール ツリーの **[名前空間]** ノードで、該当する名前空間を右クリックし、**[プロパティ]** をクリックします。

2.  **[詳細設定]** タブをクリックして **[この名前空間のアクセス ベースの列挙を有効にする]** チェック ボックスをオンにします。

## <a name="to-enable-access-based-enumeration-by-using-a-command-line"></a>コマンド ラインを使ってアクセス ベースの列挙を有効にするには

1.  **分散ファイル システム**の役割サービスまたは**分散ファイル システム ツール**機能がインストールされたサーバーでコマンド プロンプト ウィンドウを開きます。

2.  次のコマンドを入力します。ここで *<名前空間の \_ ルート>* が名前空間のルートになります。

    ```
    dfsutil property abe enable \\ <namespace_root>
    ```

> [!TIP]
> Windows PowerShell を使って名前空間でアクセス ベースの列挙を管理するには、[Set-DfsnRoot](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd834874(v=ws.11))、[Grant-DfsnAccess](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd834874(v=ws.11))、[Revoke-DfsnAccess](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd834874(v=ws.11)) の各コマンドレットを使います。 DFSN Windows PowerShell モジュールは、Windows Server 2012 で導入されました。

Windows インターフェイスを使うかコマンド ラインを使って個々 の DFS フォルダーを表示できるユーザーとグループを制御できます。

## <a name="to-control-folder-visibility-by-using-the-windows-interface"></a>Windows インターフェイスを使ってフォルダーの表示を制御するには

1.  コンソール ツリーの **[名前空間]** ノードの下で、表示を制御するターゲットを含むフォルダーを見つけ、右クリックして **[プロパティ]** をクリックします。

2.  **[詳細設定]** タブをクリックします。

3.  **[DFS フォルダーに明示的なアクセス許可の表示を設定する]**、**[アクセス許可の表示を構成する]** の順にクリックします。

4.  **[追加]** または **[削除]** をクリックして、グループやユーザーを追加または削除します。

5.  ユーザーが DFS フォルダーを表示できるようにするには、グループまたはユーザーを選択し、**[許可]** チェック ボックスをオンにします。

    グループまたはユーザーからフォルダーを非表示にするには、グループまたはユーザーを選択し、**[拒否]** チェック ボックスをオンにします。

## <a name="to-control-folder-visibility-by-using-a-command-line"></a>コマンド ラインを使ってフォルダーの表示を制御するには

1. **分散ファイルシステム**の役割サービスまたは**分散ファイルシステムツール**機能がインストールされているサーバーで、コマンドプロンプトウィンドウを開きます。

2. 次のコマンドを入力します。ここで、 * &lt; &gt; DFSPath*は DFS フォルダー (リンク) のパス、 *<ドメイン \\ アカウント>* はグループまたはユーザーアカウントの名前、 *(...)* は追加の Access Control エントリ (ace) に置き換えられます。

   ```
   dfsutil property sd grant <DFSPath> DOMAIN\Account:R (...) Protect Replace
   ```

   たとえば、ドメイン管理者と CONTOSO \\ トレーナーグループが office\public\training フォルダーに対する読み取り (R) アクセスを許可するアクセス許可を持つ既存のアクセス許可を置き換えるには、 \\ 次のコマンドを入力します。

   ```
   dfsutil property sd grant \\contoso.office\public\training "CONTOSO\Domain Admins":R CONTOSO\Trainers:R Protect Replace
   ```

3. コマンド プロンプトから追加のタスクを実行するには、次のコマンドを使用します。


| command | 説明 |
|---|---|
|[Dfsutil property sd deny](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd759150(v=ws.11))|グループまたはユーザーによるフォルダーの表示を拒否します。|
|[Dfsutil property sd reset](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd759150(v=ws.11)) |フォルダーからすべてのアクセス許可を削除します。|
|[Dfsutil property sd revoke](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd759150(v=ws.11))| フォルダーからグループまたはユーザー ACE を削除します。 |

## <a name="additional-references"></a>その他の参照情報

-   [DFS 名前空間を作成する](create-a-dfs-namespace.md)
-   [DFS 名前空間の管理アクセス許可を委任する](delegate-management-permissions-for-dfs-namespaces.md)
-   [DFS のインストール](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731089(v=ws.11))
-   [アクセスベースの列挙で継承されたアクセス許可を使用する](using-inherited-permissions-with-access-based-enumeration.md)
