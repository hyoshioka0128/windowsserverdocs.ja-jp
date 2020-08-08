---
title: AD フォレストの回復-Windows Server 2003 の回復
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 07/07/2017
ms.topic: article
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.openlocfilehash: 6693f2af67e0de32e54eec309b62f5333505f559
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87943650"
---
# <a name="ad-forest-recovery---windows-server-2003-recovery"></a>AD フォレストの回復-Windows Server 2003 の回復

>適用対象: Windows Server 2003

このトピックでは、Windows Server 2003 を実行するドメインコントローラー (Dc) のフォレスト回復手順について説明します。 フォレストの回復の一般的なプロセスは、Windows Server 2003 Dc とは異なりますが、ツールが異なると、特定の手順が異なる場合があります。 たとえば、Ntdsutil.exe を使用して、Windows Server 2003 Dc を実行する Dc をバックアップおよび復元できます。一方、Windows Server バックアップまたは Wbadmin.exe は、Windows Server 2008 以降を実行する Dc に使用されます。

- [システム状態データのバックアップ](#backing-up-the-system-state-data)
- [権限のない復元を実行する](#performing-a-nonauthoritative-restore)
- [DNS サーバーサービスのインストールと構成](#install-and-configure-the-dns-server-service)

## <a name="backing-up-the-system-state-data"></a>システム状態データのバックアップ
Windows Server 2003 を実行している DC のシステム状態データを、現在のバックアップ操作用に選択した他のデータと共にバックアップするには、次の手順に従います。 Windows Server 2003 には、システム状態データのバックアップに使用できる Ntbackup ツールが含まれています。

ファイルとフォルダーをバックアップするには、 **Administrators**または**Backup Operators**のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。

システム状態データをテープにバックアップしていて、使用可能な未使用メディアがないことをバックアッププログラムが示している場合は、リムーバブル記憶域を使用することが必要になる場合があります。 これにより、テープが空きメディアプールに追加され、バックアップで使用できるようになります。

システム状態データは、ローカルコンピューター上でのみバックアップできます。 リモートコンピューターにバックアップすることはできません。

### <a name="to-back-up-the-system-state-data-on-a-domain-controller-that-runs-windows-server-2003"></a>Windows Server 2003 を実行しているドメインコントローラーのシステム状態データをバックアップするには

1. [**スタート**] をクリックし、[**すべてのプログラム**] をポイントします。次に、[**アクセサリ**]、[**システムツール**] の順にポイントし、[**バックアップ**] をクリックします。
2. [**ようこそ**] ページで、[**詳細設定モード**] をクリックします。
3. [**バックアップ**] タブで、バックアップするドライブ、フォルダー、またはファイルのチェックボックスをオンにします。
4. [**システム状態**] チェックボックスをオンにします。
5. [**バックアップの開始**] をクリックします。

## <a name="performing-a-nonauthoritative-restore"></a>権限のない復元を実行する

Windows Server 2003 を実行している DC の権限のない復元を実行するには、次の手順に従います。 Windows Server 2003 の Active Directory で権限のない復元を実行すると、SYSVOL の authoritative restore が自動的に実行されます。 追加の手順は必要ありません。

> [!NOTE]
> Windows Server 2003 オペレーティングシステムも再インストールする場合、コンピューターをドメインに参加させたり、オペレーティングシステムのセットアップ時にコンピューターに名前を付けたりすることはできません。 Active Directory をインストールしないでください。 オペレーティングシステムを再インストールしたら、手順4に直接進みます。

システム状態データのみを復元した Windows Server 2003 ドメインコントローラーでは、回復する前に、Dc で実行されていたソフトウェアアプリケーションも再インストールする必要があります。 ドメイン内の最初の DC で AD DS を復元すると、両方ともシステム状態データの一部であるため、レジストリも復元されます。 これらの Dc でアプリケーションを実行していて、レジストリに何らかの情報が格納されている場合は、この点に注意してください。

ソフトウェアの再インストールに必要な時間を節約するには、Dc にインストールする必要があるアプリケーションが仮想 DC の複製と互換性があるかどうかを判断します。 複製する前にこのようなアプリケーションをソース DC にインストールして、複製された仮想 Dc にインストールするために必要な時間と労力を節約できます。

### <a name="to-perform-a-nonauthoritative-restore"></a>権限のない復元を実行するには

1. DC を起動したら、F8 キーを押して、ディレクトリサービス復元モード (DSRM) でコンピューターを再起動します。
2. [**ディレクトリサービス復元モード (Windows ドメインコントローラーのみ)**] を選択します。
3. 復元モードで起動するオペレーティングシステムを選択します。
4. 管理者としてログオンします (ローカルコンピューターアカウントのみ使用でき、ドメインログオンオプションは使用できません)。
5. コマンドプロンプトで、「 **ntbackup**」と入力し、enter キーを押します。
6. [**ようこそ**] ページで、[**詳細設定モード**] をクリックし、[**メディアの復元と管理**] タブを選択します ([**復元ウィザード**] を選択しないでください)。
7. 復元元として適切なバックアップファイルを選択し、[**システムディスク**] および [**システム状態**] チェックボックスがオンになっていることを確認します。
8. **[復元の開始]** をクリックします。
9. 復元操作が完了したら、コンピューターを再起動します。

Windows Server 2003 を実行している DC で、SYSVOL の権限のある (プライマリとも呼ばれる) 復元を実行するには、次の手順を使用します。 この手順は、ドメインで復元された最初の Windows Server 2003 DC でのみ実行してください。

### <a name="to-perform-an-authoritative-restore-of-sysvol"></a>SYSVOL の authoritative restore を実行するには

1. 前の手順の手順 1. ~ 8. を実行します。
2. [**復元の確認**] ダイアログボックスで、[**詳細設定**] をクリックします。
3. SYSVOL の authoritative restore を実行するには、レプリケートされたデータセットを復元するときにチェックボックスをオンにし、復元された**データをすべてのレプリカのプライマリデータとしてマーク**します。

   > [!NOTE]
   > 復元されたデータをバックアップのプライマリデータとしてマークすることは、次のレジストリサブキーの下で、 **BurFlags**エントリを D4 に設定することと同じです。
   >
   > **\System\currentcontrolset\services\ntfrs\parameters\cumulative レプリカセット \\ の HKEY_LOCAL_MACHINE***GUID*

4. 復元操作が完了したら、コンピューターを再起動します。

## <a name="install-and-configure-the-dns-server-service"></a>DNS サーバーサービスのインストールと構成

バックアップから復元した DC が Windows Server 2003 を実行している場合は、DC をどのネットワークにも接続せずに DNS サーバーをインストールできます。

### <a name="to-install-and-configure-the-dns-server-service"></a>DNS サーバーサービスをインストールして構成するには

1. Windows コンポーネントウィザードを開きます。 ウィザードを開くには:

   - [**スタート**]、[**コントロール パネル**]、[**プログラムの追加と削除**] の順にクリックします。
   - [ **Windows コンポーネントの追加と削除**] をクリックします。

2. [**コンポーネント**] で、[**ネットワークサービス**] チェックボックスをオンにし、[**詳細**] をクリックします。
3. **ネットワークサービスのサブコンポーネント**で、[**ドメインネームシステム (DNS)** ] チェックボックスをオンにし、[ **OK**] をクリックして、[**次へ**] をクリックします。
4. メッセージが表示されたら、[**ファイルのコピー元**] ボックスに配布ファイルの完全なパスを入力し、[ **OK]** をクリックします。

   インストールが完了したら、次の手順を実行して DNS サーバーを構成します。

5. [**スタート**] をクリックし、[**すべてのプログラム**]、[**管理ツール**] の順にポイントして、[ **DNS**] をクリックします。
6. 重大な誤動作を行う前に、DNS サーバーでホストされていたのと同じ DNS ドメイン名の DNS ゾーンを作成します。 詳細については、「前方参照ゾーンを追加する」 () を参照してください [https://go.microsoft.com/fwlink/?LinkId=74574](https://go.microsoft.com/fwlink/?LinkId=74574) 。
7. 重大な障害の前に存在していた DNS データを構成します。 例:

   - AD DS に格納されるように DNS ゾーンを構成します。 詳細については、「ゾーンの種類を変更する」 () を参照してください [https://go.microsoft.com/fwlink/?LinkId=74579](https://go.microsoft.com/fwlink/?LinkId=74579) 。
   - ドメインコントローラーロケーター (DC ロケーター) リソースレコードに対して権限のある DNS ゾーンを構成して、セキュリティで保護された動的更新を実行できるようにします。 詳細については、「セキュリティで保護された動的更新のみを許可する」 () を参照してください [https://go.microsoft.com/fwlink/?LinkId=74580](https://go.microsoft.com/fwlink/?LinkId=74580) 。

8. 親 DNS ゾーンに、この DNS サーバーでホストされている子ゾーンの委任リソースレコード (ネームサーバー (NS) とグルーホスト (A) リソースレコード) が含まれていることを確認します。 詳細については、「ゾーンの委任を作成する」 () を参照してください [https://go.microsoft.com/fwlink/?LinkId=74562](https://go.microsoft.com/fwlink/?LinkId=74562) 。
9. DNS を構成した後、コマンドプロンプトで次のコマンドを入力し、enter キーを押します。

   **net stop netlogon**

10. 次のコマンドを入力し、Enter キーを押します。

    **net start netlogon**

    > [!NOTE]
    > Net Logon は、DC ロケーターリソースレコードをこの DC の DNS に登録します。 子ドメインのサーバーに DNS サーバーサービスをインストールする場合、この DC はそのレコードをすぐに登録できません。 これは、復旧プロセスの一部として現在分離されており、そのプライマリ DNS サーバーがフォレストのルート DNS サーバーであるためです。 DC サービスの参照エラーを回避するために、障害が発生する前と同じ IP アドレスを使用してこのコンピューターを構成してください。

## <a name="next-steps"></a>次の手順

- [AD フォレストの回復 - 前提条件](AD-Forest-Recovery-Prerequisties.md)
- [AD フォレストの回復-カスタムフォレストの復旧計画の作成](AD-Forest-Recovery-Devising-a-Plan.md)
- [AD フォレストの回復-問題の特定](AD-Forest-Recovery-Identify-the-Problem.md)
- [AD フォレストの回復-回復方法を決定する](AD-Forest-Recovery-Determine-how-to-Recover.md)
- [AD フォレストの回復-最初の回復を実行する](AD-Forest-Recovery-Perform-initial-recovery.md)
- [AD フォレストの回復 - 手順](AD-Forest-Recovery-Procedures.md)
- [AD フォレストの回復-よく寄せられる質問](AD-Forest-Recovery-FAQ.md)
- [AD フォレストの回復-マルチドメインフォレスト内の単一ドメインの回復](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)
- [AD フォレストの回復-Windows Server 2003 ドメインコントローラーを使用したフォレストの回復](AD-Forest-Recovery-Windows-Server-2003.md)
