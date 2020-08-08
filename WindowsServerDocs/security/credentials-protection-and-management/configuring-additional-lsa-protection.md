---
title: 追加の LSA の保護の構成
description: Windows Server のセキュリティ
ms.topic: article
ms.assetid: 038e7c2b-c032-491f-8727-6f3f01116ef9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 78533908de1a1f43cbfac9054dcfe6ec83edce9d
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87948755"
---
# <a name="configuring-additional-lsa-protection"></a>追加の LSA の保護の構成

>適用先:Windows Server (半期チャネル)、Windows Server 2016

IT プロフェッショナル向けのこのトピックでは、資格情報に損害を与える可能性があるコード インジェクションを防止する、ローカル セキュリティ機関 (LSA) のプロセスに対して、追加の保護を構成する方法について説明します。

LSA には、Local Security Authority Server Service (LSASS) プロセスが含まれており、ローカルおよびリモート サインインでユーザーを検証し、ローカル セキュリティ ポリシーを適用します。 Windows 8.1 オペレーティングシステムは、保護されていないプロセスによるメモリやコードインジェクションの読み取りを防ぐために、LSA の追加の保護を提供します。 これにより、LSA が格納して管理する資格情報のセキュリティが強化されます。 LSA の保護されたプロセス設定は Windows 8.1 で構成できますが、Windows RT 8.1 では構成できません。 この設定をセキュア ブートと組み合わせて使用した場合、HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa レジストリ キーを無効にしても効果がなくなるため、さらに保護が強化されます。

### <a name="protected-process-requirements-for-plug-ins-or-drivers"></a>プラグインまたはドライバーの保護されたプロセスの要件
LSA のプラグインまたはドライバーが保護されたプロセスとして正常に読み込まれるには、次の要件を満たしている必要があります。

1.  署名の検証

    保護モードでは、LSA に読み込まれるすべてのプラグインが、Microsoft 署名を使ってデジタル署名されている必要があります。 そのため、未署名のプラグインや Microsoft 署名を使って署名されていないプラグインは、LSA に読み込まれません。 このようなプラグインの例として、スマート カードのドライバー、暗号化のプラグイン、およびパスワード フィルターがあります。

    スマート カードのドライバーなど、ドライバーである LSA プラグインは、WHQL 認定を使って署名されている必要があります。 詳細については、「 [WHQL リリース署名](https://msdn.microsoft.com/library/windows/hardware/ff553976%28v=vs.85%29.aspx)」を参照してください。

    WHQL 認定プロセスがない LSA プラグインは、 [LSA のファイル署名サービス](https://go.microsoft.com/fwlink/?LinkId=392590)を使用して署名する必要があります。

2.  Microsoft セキュリティ開発ライフサイクル (SDL) のプロセス ガイダンスへの準拠

    プラグインはすべて、該当する SDL のプロセス ガイダンスに準拠している必要があります。 詳細については、「 [Microsoft セキュリティ開発ライフサイクル (SDL) の付録](https://msdn.microsoft.com/library/windows/desktop/cc307891.aspx)」を参照してください。

    プラグインが Microsoft 署名を使って適切に署名されている場合でも、SDL のプロセスに準拠していない場合、プラグインを読み込むことができない可能性があります。

#### <a name="recommended-practices"></a>推奨プラクティス
次の一覧を使用して、機能を広く展開する前に、LSA の保護が有効になっていることを幅広くテストします。

-   組織内で使用されているすべての LSA プラグインおよびドライバーを確認します。
    これには、スマート カードのドライバーや暗号化のプラグインなどの Microsoft 以外のドライバーやプラグイン、およびパスワード フィルターやパスワードの変更通知を適用するために内部で開発されたソフトウェアが含まれます。

-   プラグインの読み込みが失敗しないように、すべての LSA プラグインが Microsoft 証明書でデジタル署名されていることを確認します。

-   正しく署名されたすべてのプラグインが、LSA に正常に読み込むことができ、意図したとおりに動作することを確認します。

-   監査ログを使用して、保護されたプロセスとして実行できない LSA プラグインおよびドライバーを識別します。

#### <a name="limitations-introduced-with-enabled-lsa-protection"></a>LSA の保護を有効にした場合に導入される制限事項

LSA の保護が有効になっている場合は、カスタム LSA プラグインをデバッグすることはできません。
保護されたプロセスであるときに、LSASS にデバッガーをアタッチすることはできません。
一般に、実行中の保護されたプロセスをデバッグする方法はサポートされていません。

## <a name="how-to-identify-lsa-plug-ins-and-drivers-that-fail-to-run-as-a-protected-process"></a>保護されたプロセスとして実行できない LSA プラグインおよびドライバーを識別する方法
ここで説明するイベントは、アプリケーションとサービス ログ\Microsoft\Windows\CodeIntegrity の下にある Operational ログに記録されます。 これらは、署名が原因で読み込まれていない LSA プラグインおよびドライバーを識別するのに役立ちます。 これらのイベントを管理するには、**wevtutil** コマンド ライン ツールを使用できます。 このツールの詳細については、[Wevtutil に関するページ](../../administration/windows-commands/Wevtutil.md)を参照してください。

### <a name="before-opting-in-how-to-identify-plug-ins-and-drivers-loaded-by-the-lsassexe"></a>オプトインの前に:lsass.exe によって読み込まれるプラグインとドライバーを識別する方法
監査モードを使用して、LSA の保護モードで読み込むことができない LSA プラグインおよびドライバーを識別できます。 監査モードでは、システムによってイベント ログが生成され、LSA の保護が有効である場合に、LSA の下で読み込みに失敗するすべてのプラグインとドライバーを識別できます。 メッセージは、プラグインやドライバーをブロックすることなく、ログに記録されます。

##### <a name="to-enable-the-audit-mode-for-lsassexe-on-a-single-computer-by-editing-the-registry"></a>レジストリを編集して単一のコンピューターで Lsass.exe の監査モード有効にするには

1.  レジストリ エディター (RegEdit.exe) を開き、次の場所にあるレジストリ キーに移動します。HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\LSASS.exe

2.  レジストリ キーの値を **AuditLevel=dword:00000008** に設定します。

3.  コンピューターを再起動します。

イベント 3065 およびイベント 3066 の結果を解析します。

その後、次のようなイベントがイベントビューアーに表示されることがあります: Microsoft-Windows-Codeintegrity/Operational:

-   **イベント 3065**: このイベントは、プロセス (通常は lsass.exe) が共有セクションのセキュリティ要件を満たしていない特定のドライバーの読み込みを試行したことを、コードの整合性チェックによって特定したことを記録します。 ただし、設定されたシステム ポリシーのために、イメージの読み込みは許可されました。

-   **イベント 3066**: このイベントは、プロセス (通常は lsass.exe) が Microsoft 署名のレベル要件を満たしていない特定のドライバーの読み込みを試行したことを、コードの整合性チェックによって特定したことを記録します。 ただし、設定されたシステム ポリシーのために、イメージの読み込みは許可されました。

> [!IMPORTANT]
> これらの操作イベントは、カーネル デバッガーがシステムにアタッチされ、有効になっている場合は生成されません。
>
> プラグインまたはドライバーに共有セクションが含まれている場合、イベント 3066 はイベント 3065 と共に記録されます。 プラグインが Microsoft 署名のレベル要件を満たしていない場合を除き、共有セクションを削除すると、どちらのイベントも発生しなくなります。

ドメイン内の複数のコンピューターについて監査モードを有効にするには、グループ ポリシーのレジストリに関するクライアント側拡張機能を使用して、Lsass.exe の監査レベルのレジストリ値を展開できます。 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\LSASS.exe レジストリ キーを変更する必要があります。

##### <a name="to-create-the-auditlevel-value-setting-in-a-gpo"></a>GPO で AuditLevel 値を作成するには

1.  グループ ポリシー管理コンソール (GPMC) を開きます。

2.  ドメイン レベルでリンクされるか、または使用するコンピューター アカウントが含まれている組織単位にリンクされる新しいグループ ポリシー オブジェクト (GPO) を作成します。 あるいは、展開済み GPO を選択できます。

3.  GPO を右クリックし、**[編集]** をクリックしてグループ ポリシー管理エディターを開きます。

4.  **[コンピューターの構成]**、**[基本設定]**、**[Windows の設定]** の順に展開します。

5.  **[レジストリ]** を右クリックし、**[新規]** をポイントして、**[レジストリ項目]** をクリックします。 **[新しいレジストリのプロパティ]** ダイアログ ボックスが表示されます。

6.  [ **Hive** ] の一覧で [HKEY_LOCAL_MACHINE] をクリックし**ます。**

7.  **[キー パス]** の一覧で、**SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\LSASS.exe** に移動します。

8.  **[値の名前]** ボックスに「**AuditLevel**」と入力します。

9. **[値の種類]** ボックスで、**[REG_DWORD]** クリックして選択します。

10. **[値のデータ]** ボックスに「**00000008**」と入力します。

11. **[OK]** をクリックします。

> [!NOTE]
> GPO を有効にするには、GPO の変更をドメイン内のすべてのドメイン コントローラーに対してレプリケートする必要があります。

複数のコンピューターで追加の LSA の保護をオプトインするには、グループ ポリシーのレジストリに関するクライアント側拡張機能を使用して、HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa を変更します。 この方法に関する手順については、このトピックの「[資格情報に対する追加の LSA の保護を構成する方法](#BKMK_HowToConfigure)」を参照してください。

### <a name="after-opting-in-how-to-identify-plug-ins-and-drivers-loaded-by-the-lsassexe"></a>オプトインの後で:lsass.exe によって読み込まれるプラグインとドライバーを識別する方法
イベント ログを使用して、LSA の保護モードで読み込むことができなかった LSA プラグインおよびドライバーを識別できます。 LSA の保護されたプロセスが有効である場合、LSA の下で読み込みに失敗したすべてのプラグインとドライバーを識別できます。

イベント 3033 およびイベント 3063 の結果を解析します。

その後、次のようなイベントがイベントビューアーに表示されることがあります: Microsoft-Windows-Codeintegrity/Operational:

-   **イベント 3033**: このイベントは、プロセス (通常は lsass.exe) が Microsoft 署名のレベル要件を満たしていないドライバーの読み込みを試行したことを、コードの整合性チェックによって特定したことを記録します。

-   **イベント 3063**: このイベントは、プロセス (通常は lsass.exe) が共有セクションのセキュリティ要件を満たしていないドライバーの読み込みを試行したことを、コードの整合性チェックによって特定したことを記録します。

共有セクションは、通常、インスタンス データが同じセキュリティ コンテキストを使用するその他のプロセスを操作するためのプログラミング手法の結果です。 これによりセキュリティの脆弱性が高くなる場合があります。

## <a name="how-to-configure-additional-lsa-protection-of-credentials"></a><a name="BKMK_HowToConfigure"></a>資格情報に対する追加の LSA の保護を構成する方法
Windows 8.1 を実行しているデバイスでは (セキュアブートまたは UEFI の有無にかかわらず)、このセクションで説明されている手順を実行して構成を行うことができます。 Windows RT 8.1 を実行しているデバイスの場合、lsass.exe 保護は常に有効になり、無効にすることはできません。

### <a name="on-x86-based-or-x64-based-devices-using-secure-boot-and-uefi-or-not"></a>x86 ベースまたは x64 ベースのデバイスでセキュア ブートや UEFI を使用するかどうか
セキュアブートまたは UEFI を使用する x86 ベースまたは x64 ベースのデバイスでは、レジストリキーを使用して LSA の保護を有効にしたときに uefi ファームウェアで UEFI 変数が設定されます。 設定がファームウェアに格納されている場合、UEFI 変数はレジストリ キーで削除または変更できません。 UEFI 変数はリセットする必要があります。

UEFI またはセキュア ブートをサポートしていない x86 ベースまたは x64 ベースのデバイスは無効になり、ファームウェアに LSA の保護の構成を格納することはできず、レジストリ キーの存在にのみ依存します。 このシナリオでは、デバイスへのリモート アクセスを使って LSA の保護を無効にできます。

次の手順を使用して、LSA の保護を有効または無効にすることができます。

##### <a name="to-enable-lsa-protection-on-a-single-computer"></a>1 台のコンピューターで LSA の保護を有効にするには

1.  レジストリ エディター (RegEdit.exe) を開き、次の場所にあるレジストリ キーに移動します。HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa

2.  レジストリ キーに次の値を設定します。"RunAsPPL"=dword:00000001

3.  コンピューターを再起動します。

##### <a name="to-enable-lsa-protection-using-group-policy"></a>グループ ポリシーを使用して LSA の保護を有効にするには

1.  グループ ポリシー管理コンソール (GPMC) を開きます。

2.  ドメイン レベルでリンクされるか、または使用するコンピューター アカウントが含まれている組織単位にリンクされる新しい GPO を作成します。 あるいは、展開済み GPO を選択できます。

3.  GPO を右クリックし、**[編集]** をクリックしてグループ ポリシー管理エディターを開きます。

4.  **[コンピューターの構成]**、**[基本設定]**、**[Windows の設定]** の順に展開します。

5.  **[レジストリ]** を右クリックし、**[新規]** をポイントして、**[レジストリ項目]** をクリックします。 **[新しいレジストリのプロパティ]** ダイアログ ボックスが表示されます。

6.  **[ハイブ]** の一覧で、**HKEY_LOCAL_MACHINE** をクリックします。

7.  **キー パス** 一覧の **SYSTEM\CurrentControlSet\Control\Lsa**を参照してください。

8.  **[値の名前]** ボックスに「**RunAsPPL**」と入力します。

9. **[値の種類]** ボックスで、**[REG_DWORD]** をクリックします。

10. **[値のデータ]** ボックスに「**00000001**」と入力します。

11. **[OK]** をクリックします。

##### <a name="to-disable-lsa-protection"></a>LSA の保護を無効にするには

1.  レジストリ エディター (RegEdit.exe) を開き、次の場所にあるレジストリ キーに移動します。HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa

2.  レジストリ キーから次の値を削除します。"RunAsPPL"=dword:00000001

3.  デバイスがセキュア ブートを使用している場合、UEFI 変数を削除するには、ローカル セキュリティ機関 (LSA) で保護されたプロセスのオプトアウト ツールを使います。

    オプトアウト ツールの詳細については、 [正式な Microsoft ダウンロード センターからローカル セキュリティ機関の (LSA) で保護されたプロセスのオプトアウトをダウンロードしてください](https://www.microsoft.com/download/details.aspx?id=40897)。

    セキュア ブートの管理の詳細については、「 [UEFI ファームウェア](https://technet.microsoft.com/library/hh824898.aspx)」を参照してください。

    > [!WARNING]
    > セキュア ブートが無効になると、セキュア ブートおよび UEFI に関連するすべての構成がリセットされます。 LSA の保護を無効にする他の方法がすべて失敗した場合にのみ、セキュア ブートを無効にしてください。

### <a name="verifying-lsa-protection"></a>LSA の保護の確認
Windows が起動したときに LSA が保護モードで起動されたかどうかを検出するには、**[Windows ログ]** の下にある **[System]** ログで次の WinInit イベントを検索します。

-   12:LSASS.exe がレベル4

## <a name="additional-resources"></a>その他のリソース
[資格情報の保護と管理](credentials-protection-and-management.md)

[LSA のファイル署名サービス](https://go.microsoft.com/fwlink/?LinkId=392590)


