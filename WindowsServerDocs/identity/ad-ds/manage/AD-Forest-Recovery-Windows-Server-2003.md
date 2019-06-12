---
title: AD フォレストの回復 - Windows Server 2003 の回復
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adds
ms.openlocfilehash: 1a9db8b4cdfbb4cc7d7edc2a17a3e747943fb073
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66442807"
---
# <a name="ad-forest-recovery---windows-server-2003-recovery"></a>AD フォレストの回復 - Windows Server 2003 の回復

>適用先:Windows Server 2003

このトピックでは、Windows Server 2003 を実行するドメイン コント ローラー (Dc) のフォレストの回復手順を説明します。 フォレストの回復に関する一般的なプロセスは、Windows Server 2003 Dc と変わりませんが、さまざまなツールのための具体的な手順の異なる可能性があります。 たとえば、バックアップおよび Windows Server バックアップまたは Wbadmin.exe が使用される Windows Server 2008 を実行しているドメイン コント ローラーまたはそれ以降は、Windows Server 2003 Dc を実行している Dc を復元する Ntdsutil.exe を使用できます。  
  
- [システム状態データをバックアップします。](#backing-up-the-system-state-data)  
- [権限のない復元を実行します。](#performing-a-nonauthoritative-restore)  
- [インストールして、DNS サーバー サービスの構成](#install-and-configure-the-dns-server-service)

## <a name="backing-up-the-system-state-data"></a>システム状態データをバックアップします。
Windows Server 2003 を実行している DC の現在のバックアップ操作用に選択した他のデータと共に、システム状態データをバックアップするには、次の手順を使用します。 Windows Server 2003 には、システム状態データをバックアップするために使用できる Ntbackup ツールが含まれています。  
  
メンバーシップ**管理者**または**Backup Operators**、またはそれと同等がファイルとフォルダーをバックアップするために必要な最低限です。   
  
システム状態データをテープにバックアップすると、バックアップ プログラムがない未使用のメディア使用可能なことを示します、リムーバブル記憶域を使用する必要があります。 そのバックアップで使用できるように、テープを空きメディア プールこの追加されます。  
  
ローカル コンピューター上に、システム状態データをバックアップすることができますのみ。 その操作は、リモート コンピューターをバックアップできません。  
  
### <a name="to-back-up-the-system-state-data-on-a-domain-controller-that-runs-windows-server-2003"></a>Windows Server 2003 を実行するドメイン コント ローラーのシステム状態データをバックアップするのには  
  
1. をクリックして**開始**、 をポイント**すべてのプログラム**、 をポイント**アクセサリ**、 をポイント**システム ツール**、順にクリックします**バックアップ**.  
2. **ようこそ** ページで  **詳細設定モード**します。  
3. **バックアップ** タブで、ドライブ、フォルダー、またはバックアップするファイルのチェック ボックスをオンにします。  
4. 選択、**システム状態**チェック ボックスをオンします。  
5. クリックして**バックアップ開始**します。  
  
## <a name="performing-a-nonauthoritative-restore"></a>権限のない復元を実行します。  

Windows Server 2003 を実行している DC の権限のない状態の復元を実行するのにには、次の手順を使用します。 Windows Server 2003 で Active Directory で権限のない状態の復元を実行すると、SYSVOL の権限のない状態の復元が自動的に実行します。 追加の手順は必要ありません。  
  
> [!NOTE]
> 場合は、Windows Server 2003 オペレーティング システムを再インストールも可能性がありますか、コンピューターをドメインに参加しない可能性があり、コンピューターにオペレーティング システムのセットアップ時に任意の名前を付けることができます。 Active Directory をインストールしないでください。 オペレーティング システムを再インストール後に、手順 4 に直接移動します。  
  
システム状態のデータのみを復元した Windows Server 2003 ドメイン コント ローラーにも復旧する前に、Dc 上で実行されていたすべてのソフトウェア アプリケーションを再インストールする必要があります。 どちらも、システム状態データの一部であるために、レジストリを復元も AD DS ドメインの最初の dc を復元します。 レジストリに保存されたあらゆる情報があれば、これらの Dc で実行されているすべてのアプリケーションがある場合は、この点に留意してください。  
  
ソフトウェアを再インストールに必要な時間を節約するには、仮想 DC の複製と互換性の Dc にインストールする必要があるアプリケーションがあるかどうかを決定します。 このようなアプリケーションは、時間と複製仮想ドメイン コント ローラーにインストールするための労力を節約するために複製する前に、ソース ドメイン コント ローラーにインストールできます。  
  
### <a name="to-perform-a-nonauthoritative-restore"></a>権限のない復元を実行するには
  
1. ドメイン コント ローラーを起動した後は、ディレクトリ サービス復元モード (DSRM) でコンピューターを再起動する f8 キーを押します。  
2. 選択**ディレクトリ サービス復元モード (Windows ドメイン コント ローラーのみ)** します。  
3. 復元モードで起動するオペレーティング システムを選択します。  
4. (しか使用できないドメインのログオン オプションなしでローカル コンピューター アカウントを使用することができます)、管理者としてログオンします。  
5. コマンド プロンプトで「 **ntbackup**、し、ENTER キーを押します。  
6. **へようこそ]** ] ページで [ **[詳細設定モード**を選び、**復元とメディアの管理**タブ。(選択しないでください**復元ウィザード**)。  
7. 復元していることを確認する適切なバックアップ ファイルの選択、**システム ディスク**と**システム状態**チェック ボックスがオンにします。  
8. クリックして**の復元を開始**します。  
9. 復元操作が完了すると、コンピューターを再起動します。  
  
次の手順を使用すると、Windows Server 2003 を実行している DC の SYSVOL の権限のある (プライマリとも呼ばれます) 復元を実行できます。 ドメインに復元する最初の Windows Server 2003 DC でのみこの手順を実行します。  
  
### <a name="to-perform-an-authoritative-restore-of-sysvol"></a>SYSVOL の authoritative restore を実行するには  
  
1. 前の手順では、手順 1 ~ 8 を実行します。  
2. **復元の確認**ダイアログ ボックスで、をクリックして**詳細**。  
3. SYSVOL の authoritative restore を実行するには、チェック ボックスをオン**を復元するには、データ セットがレプリケートされる、ときに、すべてのレプリカをプライマリ データとして、復元されたデータをマーク**します。  

   > [!NOTE]
   > 復元されたデータをプライマリ、バックアップ データと等しい設定としてマーク、 **BurFlags** D4 に次のレジストリ サブキーの下のエントリ。  
   >   
   > **レプリカ セットの HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NtFrs\Parameters\Cumulative\\**  *GUID*  

4. 復元操作が完了すると、コンピューターを再起動します。  
  
## <a name="install-and-configure-the-dns-server-service"></a>インストールして、DNS サーバー サービスの構成

バックアップから復元された DC が Windows Server 2003 を実行中の場合は、DC を任意のネットワークに接続しなくても DNS サーバーをインストールできます。  
  
### <a name="to-install-and-configure-the-dns-server-service"></a>インストールして、DNS サーバー サービスを構成するには  
  
1. Windows コンポーネント ウィザードを開きます。 ウィザードを開きます。  

   - **[スタート]** 、 **[コントロール パネル]** 、 **[プログラムの追加と削除]** の順にクリックします。  
   - クリックして**Windows コンポーネントの追加/削除**します。  

2. **コンポーネント**を選択、**ネットワーク サービス**チェック ボックスをオンにして**詳細**します。  
3. **ネットワーク サービスのサブコンポーネント**を選択、**ドメイン ネーム システム (DNS)**  チェック ボックスをクリックします**ok**、順にクリックします**次**します。  
4. 求められた場合**ファイルのコピー元**、配布ファイルの完全なパスを入力し、クリックして**OK**します。  

   インストール後、DNS サーバーを構成するには、次の手順を完了します。  

5. クリックして**開始**、 をポイント**すべてのプログラム**、 をポイント**管理ツール**、順にクリックします**DNS**します。  
6. 重要な誤動作する前に、DNS サーバーにホストされていた同じ DNS ドメイン名の DNS ゾーンを作成します。 詳細については、Add a Forward Lookup Zone を参照してください ([https://go.microsoft.com/fwlink/?LinkId=74574](https://go.microsoft.com/fwlink/?LinkId=74574))。  
7. 重要な誤動作する前に存在していた DNS データを構成します。 例:  

   - AD DS に格納される DNS ゾーンを構成します。 詳細については、変更、ゾーンの種類を参照してください ([https://go.microsoft.com/fwlink/?LinkId=74579](https://go.microsoft.com/fwlink/?LinkId=74579))。  
   - 安全な動的更新を許可するドメイン コント ローラー ロケーター (DC ロケーター) リソース レコードに対する権限のある DNS ゾーンを構成します。 詳細については、許可 Only Secure Dynamic Updates を参照してください ([https://go.microsoft.com/fwlink/?LinkId=74580](https://go.microsoft.com/fwlink/?LinkId=74580))。  

8. 親 DNS ゾーンにはでこの DNS サーバーでホストされている子ゾーンの委任リソース レコード (ネーム サーバー (NS) とグルー ホスト (A) リソース レコード) が含まれていることを確認します。 詳細については、ゾーンの委任を作成するを参照してください ([https://go.microsoft.com/fwlink/?LinkId=74562](https://go.microsoft.com/fwlink/?LinkId=74562))。  
9. DNS を構成した後は、コマンド プロンプトで次のコマンドを入力し、し、ENTER キーを押します。  

   **net stop netlogon**

10. 次のコマンドを入力して、Enter キーを押します。  

    **net start netlogon**

    > [!NOTE]
    > Net Logon に、この DC の DNS で DC ロケーターのリソース レコードを登録します。 子ドメイン内のサーバーに DNS サーバー サービスをインストールする場合、この DC はすぐにそのレコードを登録できません。 現在の分離、回復プロセスとそのプライマリ DNS サーバーの一部は、フォレスト ルート DNS サーバーがあるためにです。 DC サービス参照の失敗を回避するために、障害前と同じ IP アドレスでは、このコンピューターを構成します。

## <a name="next-steps"></a>次の手順

- [AD フォレストの回復 - 前提条件](AD-Forest-Recovery-Prerequisties.md)  
- [AD フォレストの回復 - カスタム フォレスト回復の計画を立てる](AD-Forest-Recovery-Devising-a-Plan.md)  
- [AD フォレストの回復の問題の特定](AD-Forest-Recovery-Identify-the-Problem.md)
- [AD フォレストの回復に回復する方法を決定](AD-Forest-Recovery-Determine-how-to-Recover.md)
- [AD フォレストの回復 - 最初の回復を実行します。](AD-Forest-Recovery-Perform-initial-recovery.md)  
- [AD フォレストの回復 - 手順](AD-Forest-Recovery-Procedures.md)  
- [AD フォレストの回復 - よく寄せられる質問](AD-Forest-Recovery-FAQ.md)  
- [AD フォレストの回復 - Multidomain フォレスト内の 1 つのドメインを回復します。](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
- [AD フォレストの回復 - Windows Server 2003 ドメイン コント ローラーとフォレストの回復](AD-Forest-Recovery-Windows-Server-2003.md) 
