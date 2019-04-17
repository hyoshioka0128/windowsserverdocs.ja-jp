---
title: "追加の LSA の保護を構成します。"
description: "Windows Server のセキュリティ"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-credential-protection
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 038e7c2b-c032-491f-8727-6f3f01116ef9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: fcfb0dab10d28413cf4ad06dd583274f217c91fa
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="configuring-additional-lsa-protection"></a>追加の LSA の保護を構成します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

IT プロフェッショナル向けのこのトピックでは、ローカル セキュリティ機関 (LSA) プロセスが資格情報を損なうおそれのあるコード インジェクションを防止する追加の保護を構成する方法について説明します。

ローカル セキュリティ機関サーバー サービス (LSASS) プロセスが含まれており、LSA は、ユーザー ローカルおよびリモート サインインを検証し、ローカル セキュリティ ポリシーを適用します。 Windows 8.1 オペレーティング システムでは、追加のメモリの読み取りを回避し、保護されていないプロセスによるコード インジェクションを LSA の保護を提供します。 これは、LSA が格納し、管理するための資格情報の追加のセキュリティを提供します。 LSA の保護されたプロセス設定は、Windows 8.1 で構成できますが、Windows RT 8.1 で構成することはできません。 この設定は、セキュア ブートと組み合わせて使用、\system\currentcontrolset\control\lsa レジストリ キーを無効にすると影響があるないために、追加の保護は達成されます。

### <a name="protected-process-requirements-for-plug-ins-or-drivers"></a>プラグインまたはドライバーの保護されたプロセスの要件
保護されたプロセスとして正常に読み込ま LSA プラグインまたはドライバーを次の条件を満たす必要がありますそれ。

1.  署名の確認

    保護モードでは、LSA に読み込まれ、すべてのプラグインがデジタル署名されている Microsoft 署名を持つ必要があります。 そのため、署名されていない、または Microsoft 署名を使って署名されていないプラグインは、LSA に読み込まは失敗します。 これらのプラグインには、スマート カードのドライバー、暗号化のプラグイン、およびパスワード フィルターがあります。

    スマート カードのドライバーなど、ドライバーである LSA プラグインは、WHQL 認定を使用して署名する必要があります。 詳細については、次を参照してください。 [WHQL リリース署名 (Windows ドライバー)](https://msdn.microsoft.com/library/windows/hardware/ff553976%28v=vs.85%29.aspx)します。

    使用して、WHQL 認定プロセスがない LSA プラグインを署名する必要があります、[ファイル署名サービスに関する LSA](https://go.microsoft.com/fwlink/?LinkId=392590)します。

2.  Microsoft Security Development Lifecycle (SDL) のプロセス ガイダンスに準拠しています。

    すべてのプラグインは、該当する SDL のプロセス ガイダンスに従ってください。 詳細については、次を参照してください。、 [Microsoft Security Development Lifecycle (SDL) の付録](https://msdn.microsoft.com/library/windows/desktop/cc307891.aspx)します。

    場合でも、プラグインが Microsoft 署名を使って正しく署名されている、非対応、SDL のプロセスを障害、プラグインを読み込むことがあります。

#### <a name="recommended-practices"></a>推奨される方法
機能を広く展開する前に、その LSA の保護を十分にテストする次のリストを使用を有効にします。

-   すべての LSA プラグインと、組織内で使用されているドライバーを識別します。 
    これには、Microsoft 以外のドライバーまたはスマート カードのドライバーなどのプラグインと暗号化のプラグインが含まれますおよびパスワード フィルターやパスワードの変更通知を実施するために使用するソフトウェアを社内で開発されたいずれかです。

-   すべての LSA プラグインはデジタル署名されている Microsoft 証明書で、プラグインの読み込みに失敗しないようにすることを確認します。

-   LSA に正常に読み込むことができますすべて正しく署名された、プラグインのことと、期待どおりに動作することを確認します。

-   監査ログを使用して、LSA プラグインおよびドライバーの保護されたプロセスとして実行に失敗を識別します。

## <a name="how-to-identify-lsa-plug-ins-and-drivers-that-fail-to-run-as-a-protected-process"></a>LSA プラグインおよびドライバーの保護されたプロセスとして実行に失敗を識別する方法
このセクションで説明するイベントが Operational 内にあるアプリケーションとサービス \microsoft\windows\codeintegrity の下のログにします。 LSA プラグインおよびドライバー署名が原因で読み込まれていないを識別するのに役立ちます。 これらのイベントを管理することができますを使用する、 **wevtutil**コマンド ライン ツールです。 このツールの詳細については、次を参照してください。 [Wevtutil](../../administration/windows-commands/Wevtutil.md)します。

### <a name="before-opting-in-how-to-identify-plug-ins-and-drivers-loaded-by-the-lsassexe"></a>オプトインの前に: プラグインと lsass.exe によって読み込まれたドライバーを識別する方法
監査モードを使用して、LSA プラグインおよびドライバーの LSA の保護モードで読み込みに失敗を識別することができます。 監査モードのときに、システムはすべてのプラグインと LSA の保護が有効にした場合、LSA の下で読み込みに失敗するドライバーを識別する、イベント ログを生成します。 プラグインまたはドライバーをブロックすることがなく、メッセージが記録されます。

##### <a name="to-enable-the-audit-mode-for-lsassexe-on-a-single-computer-by-editing-the-registry"></a>有効にする監査モード Lsass.exe の単一のコンピュータにレジストリを編集します。

1.  レジストリ エディター (RegEdit.exe) を開き、場所にあるレジストリ キーに移動します。 hkey_local_machine \software\microsoft\windows nt \currentversion\image ファイル実行 Options\LSASS.exe します。

2.  レジストリ キーの値を設定**AuditLevel = dword:00000008**します。

3.  コンピューターを再起動します。

イベント 3065 およびイベント 3066 の結果を分析します。

-   **イベント 3065**: このイベントは、コードの整合性チェックが、プロセス (通常は lsass.exe) が共有セクションのセキュリティ要件を満たしていない特定のドライバーをロードしようとしたことによって特定したことを記録します。 ただし、設定されているシステムのポリシーのため、イメージが読み込みに許可されました。

-   **イベント 3066**: このイベントは、コードの整合性チェックが、プロセス (通常は lsass.exe) が Microsoft 署名のレベル要件を満たしていない特定のドライバーをロードしようとしたことによって特定したことを記録します。 ただし、設定されているシステムのポリシーのため、イメージが読み込みに許可されました。

> [!IMPORTANT]
> カーネル デバッガーが接続されているし、システム上で有効になっているときに、これらの操作イベントは生成されません。
> 
> 場合、プラグインまたはドライバーに共有セクションが含まれています、イベント 3066 はイベント 3065 と共に記録します。 共有セクションを削除する、両方のイベントのプラグインが満たしていない Microsoft 署名のレベル要件しない限りの発生を防ぐ必要があります。

ドメイン内の複数のコンピューターの監査モードを有効にするのにには、Lsass.exe の監査レベルのレジストリ値を展開するのにグループ ポリシーのレジストリのクライアント側拡張機能を使用できます。 Hkey_local_machine \software\microsoft\windows nt \currentversion\image ファイル実行 Options\LSASS.exe レジストリ キーを変更する必要があります。

##### <a name="to-create-the-auditlevel-value-setting-in-a-gpo"></a>GPO で auditlevel 値を作成するには

1.  グループ ポリシー管理コンソール (GPMC) を開きます。

2.  新しいグループ ポリシー オブジェクト (GPO)、ドメイン レベルでリンクされているか、コンピューター アカウントを含む組織単位にリンクされているを作成します。 または、既に展開されている GPO を選択することができます。

3.  GPO を右クリックし、をクリックして**編集**をグループ ポリシー管理エディターを開きます。

4.  展開**コンピューターの構成**、展開**の基本設定**、し、展開**Windows 設定**します。

5.  右クリック**レジストリ**、] をポイント**新規**、] をクリックし、**レジストリ項目**します。 **新しいレジストリのプロパティ**] ダイアログ ボックスが表示されます。

6.  **ハイブ**一覧で、クリックして**HKEY_LOCAL_MACHINE します。**

7.  **キー パス**一覧を参照**\microsoft\windows \software\microsoft\windows nt \currentversion\image ファイル実行 Options\LSASS.exe**します。

8.  **値の名前**ボックスに、入力**AuditLevel**します。

9. **値の型**ボックスで、クリックして選択、 **REG_DWORD**します。

10. **値のデータ**ボックスに、入力**00000008**します。

11. をクリックして**OK**します。

> [!NOTE]
> GPO を有効にするため、GPO の変更は、ドメイン内のすべてのドメイン コント ローラーにレプリケートされる必要があります。

オプトインする複数のコンピューターで追加の LSA の保護に、hkey_local_machine \system\currentcontrolset\control\lsa を変更、グループ ポリシーのレジストリのクライアント側拡張機能を使用できます。 これを行う方法に関する手順については、次を参照してください。[資格情報の追加の LSA の保護を構成する方法](#BKMK_HowToConfigure)このトピックの「します。

### <a name="after-opting-in-how-to-identify-plug-ins-and-drivers-loaded-by-the-lsassexe"></a>オプトインの後で: プラグインと lsass.exe によって読み込まれたドライバーを識別する方法
イベント ログを使用して、LSA プラグインおよび LSA の保護モードで読み込みに失敗したドライバーを識別することができます。 LSA の保護されたプロセスが有効にすると、システムはすべてのプラグインと LSA の下で読み込みに失敗したドライバーを識別するためのイベント ログを生成します。

イベント 3033 およびイベント 3063 の結果を分析します。

-   **イベント 3033**: このイベントは、コードの整合性チェックがプロセス (通常は lsass.exe) が Microsoft 署名のレベル要件を満たしていないドライバーの読み込みを試行したことによって特定したことを記録します。

-   **イベント 3063**: このイベントは、コードの整合性チェックがプロセス (通常は lsass.exe) が共有セクションのセキュリティ要件を満たしていないドライバーの読み込みを試行したことによって特定したことを記録します。

共有のセクションでは、通常、同じセキュリティ コンテキストを使用している他のプロセスとの対話にインスタンス データを許可するプログラミング手法の結果です。 これにより、セキュリティの脆弱性が作成することができます。

## <a name="BKMK_HowToConfigure"></a>資格情報の追加の LSA の保護を構成する方法
(セキュア ブートまたは UEFI の有無にかかわらず) は、Windows 8.1 を実行しているデバイスでは、構成がこのセクションで説明する手順を実行することで可能です。 Windows RT 8.1 を実行しているデバイス、lsass.exe の保護が常に有効にし、オフになっていることはできません。

### <a name="on-x86-based-or-x64-based-devices-using-secure-boot-and-uefi-or-not"></a>X86 ベースまたは x64 ベースのデバイスを使用してセキュア ブートおよび UEFI かどうか
セキュア ブートおよび UEFI を使用する x86 ベースまたは x64 ベースのデバイスでは、レジストリ キーを使用して LSA の保護が有効にすると、UEFI 変数は UEFI ファームウェアで設定されます。 ファームウェアで、設定が保存されると、UEFI 変数を削除またはレジストリ キーに変更できません。 UEFI 変数はリセットする必要があります。

UEFI またはセキュア ブートをサポートしない x86 ベースまたは x64 ベースのデバイスが無効になっている、ことはできません、ファームウェアの LSA の保護の構成を保存し、のみ、レジストリ キーの存在に依存します。 このシナリオで、デバイスへのリモート アクセスを使用して LSA の保護を無効にすることができます。

次の手順を使用して、有効にするか、LSA の保護を無効にできます。

##### <a name="to-enable-lsa-protection-on-a-single-computer"></a>1 台のコンピューターで LSA の保護を有効にするには

1.  レジストリ エディター (RegEdit.exe) を開き、場所にあるレジストリ キーに移動します。 \system\currentcontrolset\control\lsa します。

2.  レジストリ キーの値を設定します。"RunAsPPL"= dword:00000001 します。

3.  コンピューターを再起動します。

##### <a name="to-enable-lsa-protection-using-group-policy"></a>グループ ポリシーを使用して LSA の保護を有効にするには

1.  グループ ポリシー管理コンソール (GPMC) を開きます。

2.  ドメイン レベルでリンクされているか、コンピューター アカウントを含む組織単位にリンクされている、新しい GPO を作成します。 または、既に展開されている GPO を選択することができます。

3.  GPO を右クリックし、をクリックして**編集**をグループ ポリシー管理エディターを開きます。

4.  展開**コンピューターの構成**、展開**の基本設定**、し、展開**Windows 設定**します。

5.  右クリック**レジストリ**、] をポイント**新規**、] をクリックし、**レジストリ項目**します。 **新しいレジストリのプロパティ**] ダイアログ ボックスが表示されます。

6.  **ハイブ**一覧で、クリックして**HKEY_LOCAL_MACHINE**します。

7.  **キー パス**一覧を参照**system \currentcontrolset\control\lsa**します。

8.  **値の名前**ボックスに、入力**RunAsPPL**します。

9. **値の型**ボックスで、をクリックして、 **REG_DWORD**します。

10. **値のデータ**ボックスに、入力**00000001**します。

11. をクリックして**OK**します。

##### <a name="to-disable-lsa-protection"></a>LSA の保護を無効にするには

1.  レジストリ エディター (RegEdit.exe) を開き、場所にあるレジストリ キーに移動します。 \system\currentcontrolset\control\lsa します。

2.  レジストリ キーから次の値を削除します。"RunAsPPL"= dword:00000001 します。

3.  ローカル セキュリティ機関 (LSA) 保護されたプロセスのオプトアウト ツールを使用すると、デバイスがセキュア ブートを使用する場合は、UEFI 変数を削除できます。

    オプトアウト ツールの詳細については、次を参照してください。[ダウンロード ローカル セキュリティ機関 (LSA) 保護されたプロセスのオプトアウト公式 Microsoft ダウンロード センターから](https://www.microsoft.com/download/details.aspx?id=40897)します。

    セキュア ブートの管理の詳細については、次を参照してください。 [UEFI ファームウェア](https://technet.microsoft.com/library/hh824898.aspx)します。

    > [!WARNING]
    > セキュア ブートをオフにすると、すべてのセキュア ブートおよび UEFI に関連する構成がリセットされます。 LSA の保護を無効にするその他のすべての手段が失敗した場合にのみ、セキュア ブートを無効にする必要があります。

### <a name="verifying-lsa-protection"></a>LSA の保護を確認します。
Windows が起動したときに、LSA を保護モードで起動されたかどうかの検出、次の WinInit イベントを検索、**システム**下にあるログ**Windows ログ**:

-   12: LSASS.exe がレベルで保護されたプロセスとして起動されました: 4

## <a name="additional-resources"></a>その他のリソース
[資格情報の保護と管理](credentials-protection-and-management.md)

[LSA のファイル署名サービス](https://go.microsoft.com/fwlink/?LinkId=392590)


