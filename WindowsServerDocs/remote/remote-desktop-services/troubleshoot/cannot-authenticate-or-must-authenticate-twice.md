---
title: ユーザーが認証できない、または 2 回認証する必要がある
description: リモート デスクトップ接続の開始時にユーザーが認証できない、または 2 回認証する必要がある問題のトラブルシューティング。
ms.reviewer: rklemen
ms.topic: troubleshooting
author: kaushika-msft
manager: dcscontentpm
ms.author: delhan
ms.date: 07/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: 8fd7cfda8814347f8bab9dc7b3f7632e3b992ecb
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857235"
---
# <a name="user-cant-authenticate-or-must-authenticate-twice"></a>ユーザーが認証できない、または 2 回認証する必要がある

この記事では、ユーザーの認証に影響する可能性のあるいくつかの問題について説明します。

## <a name="access-denied-restricted-type-of-logon"></a>アクセス拒否、制限された種類のログオン

この状況では、Windows 10 のユーザーが Windows 10 または Windows Server 2016 のコンピューターに接続しようとすると、次のメッセージでアクセスを拒否されます。

> リモート デスクトップ接続:  
> 使用できるログオンの種類 (ネットワークまたは対話型) がシステム管理者により制限されています。 サポートが必要な場合は、システム管理者かテクニカル サポートに問い合わせてください。

この問題は、RDP 接続にネットワーク レベル認証 (NLA) が必要であり、ユーザーが **Remote Desktop Users** グループのメンバーではない場合に発生します。 また、**Remote Desktop Users** グループが **[ネットワーク経由でのアクセス]** ユーザー権利に割り当てられていない場合にも、発生する可能性があります。

この問題を解決するには、次のいずれかを実行します。

  - [ユーザーのグループ メンバーシップまたはユーザー権利の割り当てを変更する](#modify-the-users-group-membership-or-user-rights-assignment)
  - NLA をオフにします (非推奨)。
  - Windows 10 以外のリモート デスクトップ クライアントを使います。 たとえば、Windows 7 クライアントではこの問題は発生しません。

### <a name="modify-the-users-group-membership-or-user-rights-assignment"></a>ユーザーのグループ メンバーシップまたはユーザー権利の割り当てを変更する

この問題の影響を受けるユーザーが 1 人だけの場合、この問題の最も簡単な解決策は、ユーザーを **Remote Desktop Users** グループに追加することです。

ユーザーが既にこのグループのメンバーである場合は (または、複数のグループ メンバーに同じ問題がある場合は)、リモートの Windows 10 または Windows Server 2016 コンピューターでユーザー権利の構成を確認します。

1. グループ ポリシー オブジェクト エディター (GPE) を開き、リモート コンピューターのローカル ポリシーに接続します。
2. **[コンピューターの構成] > [Windows の設定] > [セキュリティ設定] > [ローカル ポリシー] > [ユーザー権利の割り当て]** に移動し、 **[ネットワーク経由でのアクセス]** を右クリックして、 **[プロパティ]** を選択します。
3. **Remote Desktop Users** (または親グループ) のユーザーとグループの一覧を確認します。
4. リストに **Remote Desktop Users** または **Everyone** のような親グループが含まれていない場合は、一覧に追加する必要があります。 展開に複数のコンピューターがある場合は、グループ ポリシー オブジェクトを使用してください。  
    たとえば、 **[ネットワーク経由でのアクセス]** の既定のメンバーシップには、**Everyone** が含まれています。 展開でグループ ポリシー オブジェクトを使って **Everyone** を削除している場合は、グループ ポリシー オブジェクトを更新して **Remote Desktop Users** を追加することにより、アクセスを復元することが必要な場合があります。

## <a name="access-denied-a-remote-call-to-the-sam-database-has-been-denied"></a>アクセス拒否、SAM データベースへのリモート呼び出しが拒否される

この動作が発生する可能性が最も高いのは、ドメイン コントローラーで Windows Server 2016 以降が実行されていて、ユーザーがカスタマイズされた接続アプリを使って接続しようとした場合です。 具体的には、Active Directory のユーザーのプロファイル情報にアクセスするアプリケーションは、アクセスを拒否されます。

この動作は、Windows に対する変更による結果です。 Windows Server 2012 R2 以前のバージョンでは、ユーザーがリモート デスクトップにサインインすると、リモート接続マネージャー (RCM) はドメイン コントローラー (DC) にアクセスし、Active Directory Domain Services (AD DS) 内のユーザー オブジェクト上にあるリモート デスクトップに固有の構成をクエリします。 この情報は、[Active Directory ユーザーとコンピューター] MMC スナップインで、ユーザーのオブジェクト プロパティの [リモート デスクトップ サービスのプロファイル] タブに表示されます。

Windows Server 2016 以降では、RCM は AD DS 内のユーザーのオブジェクトをクエリしなくなっています。 リモート デスクトップ サービスの属性を使っているため、RCM で AD DS をクエリする必要がある場合は、クエリを手動で有効にする必要があります。

> [!IMPORTANT]  
> 慎重にこのセクションの手順に従います。 レジストリを正しく変更しないと、重大な問題が発生する可能性があります。 変更する前に、問題が発生した場合に[復元するためにレジストリをバックアップ](https://support.microsoft.com/help/322756)します。

RD セッション ホスト サーバーで以前の RCM の動作を有効にするには、次のレジストリ エントリを構成した後、**リモート デスクトップ サービス**のサービスを再起動します。  
  - **HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Policies\\Microsoft\\Windows NT\\Terminal Services**
  - **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server\\WinStations\\\<Winstation name\>\\**  
      - 名前: **fQueryUserConfigFromDC**
      - 次のように入力します。**Reg\_DWORD**
      - 値:**1** (10 進)

RD セッション ホスト サーバー以外のサーバーで以前の RCM の動作を有効にするには、これらのレジストリ エントリと、次の追加レジストリ エントリを構成します (その後、サービスを再起動します)。
  - **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server**

この動作について詳しくは、KB 3200967 「[Windows Server のリモート接続マネージャーへの変更](https://support.microsoft.com/help/3200967/changes-to-remote-connection-manager-in-windows-server)」をご覧ください。

## <a name="user-cant-sign-in-using-a-smart-card"></a>ユーザーがスマート カードを使用してサインインできない

このセクションでは、ユーザーがスマート カードを使用してリモート デスクトップにサインインできない 3 つの一般的なシナリオについて説明します。

### <a name="cant-sign-in-with-a-smart-card-in-a-branch-office-with-a-read-only-domain-controller-rodc"></a>読み取り専用ドメイン コントローラー (RODC) を使用するブランチ オフィスにスマート カードでサインインできない

この問題は、RODC を使うブランチ サイトに RDSH サーバーが含まれる展開で発生します。 RDSH サーバーは、ルート ドメインでホストされます。 ブランチ サイトのユーザーは子ドメインに属し、認証にスマート カードを使います。 RODC はユーザーのパスワードをキャッシュするように構成されています (RODC は **Allowed RODC Password Replication グループ**に属しています)。 ユーザーは、RDSH サーバー上のセッションにサインインしようとすると、次のようなメッセージを受け取ります。"実行しようとしたログオンは無効です。 ユーザー名または認証情報に誤りがあります。"

この問題は、ルート DC と RDOC によるユーザー資格情報の暗号化の管理方法が原因で発生します。 ルート DC では暗号化キーを使って資格情報が暗号化され、RODC では復号化キーがクライアントに提供されます。 ユーザーが "無効" エラーを受け取った場合、2 つのキーが合致していないことを意味します。

この問題に対処するには、次のいずれかを試してみてください。

- RODC でパスワードのキャッシュを無効にすることによって DC のトポロジを変更するか、書き込み可能 DC をブランチ サイトに展開します。
- RDSH サーバーをそのユーザーと同じ子ドメインに移動します。
- ユーザーがスマート カードなしでサインインできるようにします。

これらのいずれの解決策でも、パフォーマンスまたはセキュリティ レベルの低下が避けられないことに留意してください。

### <a name="user-cant-sign-in-to-a-windows-server-2008-sp2-computer-using-a-smart-card"></a>ユーザーがスマート カードを使用して Windows Server 2008 SP2 のコンピューターにサインインできない

この問題は、ユーザーが KB4093227 (2018.4B) で更新された Windows Server 2008 SP2 コンピューターにサインインするときに発生します。 ユーザーは、スマート カードを使ってサインインしようとすると、次のようなメッセージでアクセスを拒否されます。"No valid certificates found. Check that the card is inserted correctly and fits tightly.” (有効な証明書が見つかりませんでした。カードが正しく挿入され、密着していることを確認してください。) 同時に、Windows Server コンピューターでは次のアプリケーション イベントが記録されます。"挿入されたスマート カードからデジタル証明書を取得しているときにエラーが発生しました。 署名が無効です。"

この問題を解決するには、KB 4093227 「[Windows Server 2008 における Windows リモート デスクトップ プロトコル (RDP) のサービス拒否の脆弱性を解決するためのセキュリティ更新プログラムについて:2018 年 4 月 10 日](https://support.microsoft.com/help/4093227/security-update-for-vulnerabilities-in-windows-server-2008)」の 2018.06 B の再リリースで Windows Server コンピューターを更新してください。

### <a name="cant-stay-signed-in-with-a-smart-card-and-remote-desktop-services-service-hangs"></a>スマート カードでのサインインを維持できず、リモート デスクトップ サービスのサービスがハングする

この問題は、ユーザーが KB 4056446 で更新された Windows または Windows Server コンピューターにサインインするときに発生します。 最初、ユーザーはスマート カードを使ってシステムにサインインできる場合がありますが、その後 "SCARD\_E\_NO\_SERVICE" のエラー メッセージを受け取ります。 リモート コンピューターが応答しなくなる可能性があります。

この問題を回避するには、リモート コンピューターを再起動します。

この問題を解決するには、適切な修正プログラムでリモート コンピューターを更新します。

  - Windows Server 2008 SP2: KB 4090928、[Windows leaks handles in the lsm.exe process and smart card applications may display "SCARD\_E\_NO\_SERVICE" errors](https://support.microsoft.com/help/4090928/scard-e-no-service-errors-when-windows-leaks-handles-in-the-lsm-exe) (Windows の lsm.exe プロセスでハンドルがリークし、スマート カード アプリケーションで "SCARD_E_NO_SERVICE" エラーが表示される場合がある)
  - Windows Server 2012 R2KB 4103724、[2018 年 5 月 17 日 — KB4103724 (マンスリー ロールアップのプレビュー)](https://support.microsoft.com/help/4103724/windows-81-update-kb4103724)
  - Windows Server 2016 および Windows 10 バージョン 1607: KB 4103720、[2018 年 5 月 17 日 — KB4103720 (OS ビルド 14393.2273)](https://support.microsoft.com/help/4103720/windows-10-update-kb4103720)

## <a name="if-the-remote-pc-is-locked-the-user-needs-to-enter-a-password-twice"></a>リモート PC がロックされている場合、ユーザーがパスワードを 2 回入力する必要がある

この問題は、RDP 接続に NLA を必要としない展開内の Windows 10 バージョン 1709 が実行されているリモート デスクトップにユーザーが接続しようとしたときに発生する可能性があります。 これらの条件下では、リモート デスクトップがロックされている場合、ユーザーは接続するときに資格情報を 2 回入力する必要があります。

この問題を解決するには、Windows 10 バージョン 1709 コンピューターを KB 4343893、[2018 年 8 月 30 日 — KB4343893 (OS ビルド 16299.637)](https://support.microsoft.com/help/4343893/windows-10-update-kb4343893) で更新します。

## <a name="user-cant-sign-in-and-receives-authentication-error-and-credssp-encryption-oracle-remediation-messages"></a>ユーザーがサインインできず、"認証エラー" および "CredSSP 暗号化オラクルの修復" のメッセージを受け取る

ユーザーは、Windows Vista SP2 以降または Windows Server 2008 SP2 以降の任意のバージョンを使ってサインインしようとすると、アクセスを拒否され、以下のようなメッセージを受け取ります。

```
An authentication error has occurred. The function requested is not supported.
...
This could be due to CredSSP encryption oracle remediation
...
```

"CredSSP 暗号化オラクルの修復" とは、2018 年の 3 月、4 月、5 月にリリースされた一連のセキュリティ更新プログラムのことです。 CredSSP は、他のアプリケーションに対する認証要求を処理する認証プロバイダーです。 2018 年 3 月 13 日の "3B" およびそれ以降の更新プログラムでは、攻撃者がユーザーの資格情報を中継してターゲット システムでコードを実行する悪用に対処しました。

最初の更新プログラムでは、新しいグループ ポリシー オブジェクトである暗号化オラクルの修復のサポートが追加されました。設定できる値は次のとおりです。

  - Vulnerable (脆弱性あり):CredSSP を使用するクライアント アプリケーションは安全でないバージョンにフォールバックできますが、この動作はリモート デスクトップを攻撃の危険にさらします。 CredSSP を使用するサービスは、更新されていないクライアントを受け付けます。
  - Mitigated (軽減済み):CredSSP を使用するクライアント アプリケーションは安全でないバージョンにフォールバックできませんが、CredSSP を使用するサービスは更新されていないクライアントを受け付けます。
  - Force Updated Clients (更新されたクライアントを強制する):CredSSP を使用するクライアント アプリケーションは安全でないバージョンにフォールバックできず、CredSSP を使用するサービスは修正プログラムが適用されていないクライアントを受け付けません。 
    > [!NOTE]
    > この設定は、すべてのリモート ホストが最新バージョンをサポートするようになるまで、展開しないでください。

2018 年 5 月 8 日の更新プログラムでは、暗号化オラクルの修復の既定の設定が Vulnerable (脆弱性あり) から Mitigated (軽減済み) に変更されました。 この変更により、更新プログラムが適用されたリモート デスクトップ クライアントは、適用されていないサーバー (または、更新後に再起動されていないサーバー) に接続できません。 CredSSP 更新プログラムの詳細については、[KB 4093492](https://support.microsoft.com/help/4093492/credssp-updates-for-cve-2018-0886-march-13-2018) に関するページをご覧ください。

この問題を解決するには、すべてのシステムを更新して再起動します。 更新プログラムの完全な一覧および脆弱性の詳細については、「[CVE-2018-0886 | CredSSP のリモートでコードが実行される脆弱性](https://portal.msrc.microsoft.com/security-guidance/advisory/CVE-2018-0886)」をご覧ください。

更新が完了するまでこの問題を回避するには、KB 4093492 で許可される接続の種類を確認してください。 可能な代替手段がない場合、次のいずれかの方法を検討できます。

- 影響を受けているクライアント コンピューターで、暗号化オラクルの修復のポリシーを **[Vulnerable]\(脆弱性あり\)** に戻します。
- **[コンピューターの構成] > [管理用テンプレート] > [Windows コンポーネント] > [リモート デスクトップ サービス] > [リモート デスクトップ セッション ホスト] > [セキュリティ]** グループ ポリシー フォルダーで、次のポリシーを変更します。  
  - **[リモート (RDP) 接続に特定のセキュリティ レイヤーの使用を必要とする]** : **[有効]** に設定し、 **[RDP]** を選択します。
  - **[リモート接続にネットワーク レベル認証を使用したユーザー認証を必要とする]** : **[無効]** に設定します。
    > [!IMPORTANT]  
    > これらのグループ ポリシーを変更すると、展開のセキュリティが低下します。 これらは一時的にのみ使用することをお勧めします。

グループ ポリシーの使用について詳しくは、「[ブロックしている GPO を変更する](rdp-error-general-troubleshooting.md#modifying-a-blocking-gpo)」をご覧ください。

## <a name="after-you-update-client-computers-some-users-need-to-sign-in-twice"></a>クライアント コンピューターを更新した後、一部のユーザーが 2 回サインインする必要がある

ユーザーが Windows 7 または Windows 10 バージョン1709 が実行されているコンピューターを使用してリモート デスクトップにサインインすると、2 つ目のサインイン プロンプトがすぐに表示されます。 この問題は、クライアント コンピューターに次の更新プログラムがある場合に発生します。

  - Windows 7: KB 4103718、[2018 年 5 月 8 日 — KB4103718 (マンスリー ロールアップ)](https://support.microsoft.com/help/4103718/windows-7-update-kb4103718)
  - Windows 10 1709: KB 4103727、[2018 年 5 月 8 日 — KB4103727 (OS ビルド 16299.431)](https://support.microsoft.com/help/4103727/windows-10-update-kb4103727)

この問題を解決するには、ユーザーが接続するコンピューター (および RDSH または RDVI サーバー) が、2018 年 6 月まで完全に更新されていることを確認します。 これには次の更新プログラムが含まれます。

  - Windows Server 2016: KB 4284880、[2018 年 6 月 12 日 — KB4284880 (OS ビルド 14393.2312)](https://support.microsoft.com/help/4284880/windows-10-update-kb4284880)
  - Windows Server 2012 R2KB 4284815、[2018 年 6 月 12 日 — KB4284815 (マンスリー ロールアップ)](https://support.microsoft.com/help/4284815/windows-81-update-kb4284815)
  - Windows Server 2012: KB 4284855、[2018 年 6 月 12 日 — KB4284855 (マンスリー ロールアップ)](https://support.microsoft.com/help/4284855/windows-server-2012-update-kb4284855)
  - Windows Server 2008 R2:KB 4284826、[2018 年 6 月 12 日 — KB4284826 (マンスリー ロールアップ)](https://support.microsoft.com/help/4284826/windows-7-update-kb4284826)
  - Windows Server 2008 SP2: KB4056564, [Description of the security update for the CredSSP remote code execution vulnerability in Windows Server 2008, Windows Embedded POSReady 2009, and Windows Embedded Standard 2009:March 13, 2018](https://support.microsoft.com/help/4056564/security-update-for-vulnerabilities-in-windows-server-2008) (Windows Server 2008、Windows Embedded POSReady 2009、Windows Embedded Standard 2009 での CredSSP リモート コード実行の脆弱性に対するセキュリティ更新プログラムの説明: 2018 年 3 月 13 日)

## <a name="users-are-denied-access-on-a-deployment-that-uses-remote-credential-guard-with-multiple-rd-connection-brokers"></a>複数の RD 接続ブローカーを含む Remote Credential Guard を使用する展開でユーザーがアクセスを拒否される

この問題は、Windows Defender Remote Credential Guard が使われている場合に、複数のリモート デスクトップ接続ブローカーを使用する高可用性の展開で発生します。 ユーザーは、リモート デスクトップにサインインできません。

この問題は、Remote Credential Guard では認証に Kerberos が使われていて、NTLM が制限されるために発生します。 ただし、負荷分散されている高可用性構成の RD 接続ブローカーでは、Kerberos の操作をサポートできません。

負荷分散された RD 接続ブローカーが含まれる高可用性構成を使う必要がある場合は、Remote Credential Guard を無効にすることで、この問題を回避できます。 Windows Defender Remote Credential Guard の管理方法について詳しくは、「[Windows Defender Remote Credential Guard を使用してリモート デスクトップの資格情報を保護する](https://docs.microsoft.com/windows/security/identity-protection/remote-credential-guard#enable-windows-defender-remote-credential-guard)」をご覧ください。
