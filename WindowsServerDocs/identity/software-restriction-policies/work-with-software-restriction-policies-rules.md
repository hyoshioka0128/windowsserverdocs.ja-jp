---
title: ソフトウェアの制限のポリシーの規則の使用
description: Windows Server のセキュリティ
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-software-restriction-policies
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4a8047d5-9bb9-4bed-bc8f-583a237731e2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 2dd1810b50f4f02be99eb2e2c0893501f99d1e93
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59844953"
---
# <a name="work-with-software-restriction-policies-rules"></a>ソフトウェアの制限のポリシーの規則の使用

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

このトピックでは、証明書、パス、インターネット ソフトウェア制限ポリシーを使用してゾーンとハッシュの規則の操作手順を説明します。

## <a name="introduction"></a>概要
ソフトウェアの制限のポリシーを識別およびどのようなソフトウェアの実行が許可されるかを指定して、信頼されていないソフトウェアからコンピューティング環境を保護できます。 既定のセキュリティ レベルを定義する**Unrestricted**または**許可しない**のグループ ポリシー オブジェクト (GPO) ソフトウェアが、許可または拒否できないように既定で実行します。 この既定のセキュリティ レベルの例外は、ソフトウェア制限ポリシーの規則を特定のソフトウェアを作成して行うことができます。 たとえば、既定のセキュリティ レベルが **[許可しない]** に設定されている場合には、特定のソフトウェアに対して実行を許可する規則を作成できます。 ルールの種類は次のとおりです。

-   **証明書の規則**

    手順については、「[証明書の規則の操作](#BKMK_Cert_Rules)」を参照してください。

-   **ハッシュの規則**

    手順については、「[ハッシュの規則の操作](#BKMK_Hash_Rules)」を参照してください。

-   **インターネット ゾーンの規則**

    手順については、次を参照してください。[のインターネット ゾーンの規則の操作](#BKMK_Internet_Zone_Rules)します。

-   **パスの規則**

    手順については、「[パスの規則の操作](#BKMK_Path_Rules)」を参照してください。

ソフトウェア制限ポリシーを管理するには、その他のタスクについては、次を参照してください。[ソフトウェア制限ポリシーの管理](administer-software-restriction-policies.md)します。

## <a name="BKMK_Cert_Rules"></a>証明書の規則の操作
ソフトウェア制限ポリシー、証明書によってソフトウェアを識別できます。 ソフトウェアを特定する証明書の規則を作成し、セキュリティ レベルに応じてソフトウェアの実行を許可するか、実行を許可しないかを指定できます。 たとえば、証明書の規則を使用すると、ドメイン内にある信頼できる発行元のソフトウェアを、ダイアログを表示することなく自動的に信頼することができます。 証明書の規則を使えばほかにも、オペレーティング システム内の許可されていない領域でファイルを実行できます。 既定では、証明書の規則は有効になっていません。

グループ ポリシーを使用して、ドメインのルールが作成されると、作成またはグループ ポリシー オブジェクトを変更する権限が必要です。 ローカル コンピューターに規則を作成するときは、そのコンピューターの管理者の資格情報が必要です。

#### <a name="to-create-a-certificate-rule"></a>証明書の規則を作成するには

1.  [ソフトウェアの制限のポリシー] を開きます。

2.  コンソール ツリーまたは詳細ウィンドウで、右クリック**追加ルール**、 をクリックし、**新しい証明書の規則**。

3.  **[参照]** をクリックし、証明書または署名されているファイルを選択します。

4.  **セキュリティ レベル**、 をクリックするか**許可しない**または**Unrestricted**します。

5.  **[説明]** にこの規則の説明を入力し、**[OK]** をクリックします。

> [!NOTE]
> -   グループ ポリシー オブジェクト (GPO) についてソフトウェアの制限のポリシーの設定を作成していない場合には、この設定の新規作成が必要になることがあります。
> -   既定では、証明書の規則は有効になっていません。
> -   証明書の規則の影響を受けるファイルの種類は、ソフトウェアの制限のポリシーの詳細ウィンドウの **[指定されたファイルの種類]** に列挙されているもののみです。 指定されたファイルの種類の一覧は 1 つであり、それがあらゆる規則の間で共有されます。
> -   ソフトウェア制限のポリシーを有効にする、ユーザーからログオフし、自分のコンピューターにログオンしてポリシー設定を更新する必要があります。
> -   ポリシーの設定には、複数のソフトウェアの制限のポリシー規則が適用されるときに競合を処理するためのルールの優先順位があります。

### <a name="enabling-certificate-rules"></a>証明書の規則の有効化
証明書の規則を有効にする手順は、環境に応じて異なります。

-   [ローカル コンピューターの](#BKMK_1)

-   [グループ ポリシー オブジェクトがドメインに参加しているサーバーには](#BKMK_2)

-   [グループ ポリシー オブジェクトをしているドメイン コント ローラーまたはリモート サーバー管理ツールがインストールされているワークステーション](#BKMK_3)

-   [のみのドメインのコント ローラーを使用しているドメイン コント ローラーまたはワークステーションにインストールされているリモート サーバー管理ツール パックを](#BKMK_4)

#### <a name="BKMK_1"></a>ローカル コンピューターの証明書の規則を有効にするには

1.  [ローカル セキュリティ設定] を開きます。

2.  コンソール ツリーで、クリックして**セキュリティ オプション**セキュリティの設定/ローカル ポリシーの下にあります。

3.  詳細ウィンドウでダブルクリック**システム設定。Windows 実行可能ファイルに対して証明書の規則を使用して、ソフトウェア制限ポリシーの**します。

4.  次のいずれかの操作を行い、**[OK]** をクリックします。

    -   証明書の規則を有効にするには、**[有効]** をクリックします。

    -   証明書の規則を無効にするには、**[無効]** をクリックします。

#### <a name="BKMK_2"></a>グループ ポリシー オブジェクトとでドメインに参加しているサーバーでは証明書の規則を有効にするには

1.  Microsoft 管理コンソール (MMC) を開きます。

2.  **[ファイル]** メニューで、**[スナップインの追加と削除]** をクリックし、**[追加]** をクリックします。

3.  **[ローカル グループ ポリシー オブジェクト エディター]** をクリックし、**[追加]** をクリックします。

4.  **[グループ ポリシー オブジェクトの選択]** で、**[参照]** をクリックします。

5.  **グループ ポリシー オブジェクトの参照**、適切なドメイン、サイト、または組織単位にグループ ポリシー オブジェクト (GPO) を選択します。- または、新しく作成し、クリック**完了**。

6.  **[閉じる]** をクリックし、 **[OK]** をクリックします。

7.  コンソール ツリーで、クリックして**セキュリティ オプション**の下にある*GroupPolicyObject* [*ComputerName*] ポリシー/コンピューターの構成/Windows の設定/セキュリティポリシーの設定/ローカル/。

8.  詳細ウィンドウでダブルクリック**システム設定。Windows 実行可能ファイルに対して証明書の規則を使用して、ソフトウェア制限ポリシーの**します。

9. ポリシー設定をまだ定義していない場合は、**[これらのポリシーの設定を定義する]** チェック ボックスをオンにします。

10. 次のいずれかの操作を行い、**[OK]** をクリックします。

    -   証明書の規則を有効にするには、**[有効]** をクリックします。

    -   証明書の規則を無効にするには、**[無効]** をクリックします。

#### <a name="BKMK_3"></a>グループ ポリシー オブジェクトでは、ルール証明書を有効にして、ドメイン コント ローラー上またはリモート サーバー管理ツールがインストールされているワークステーションには

1.  [Active Directory ユーザーとコンピューター] を開きます。

2.  コンソール ツリーで、証明書の規則を有効にするグループ ポリシー オブジェクト (GPO) を右クリックします。

3.  **[プロパティ]**、**[グループ ポリシー]** タブの順にクリックします。

4.  **[編集]** をクリックして、編集する GPO を開きます。 このほか、**[新規作成]** をクリックして新しい GPO を作成し、**[編集]** をクリックする方法があります。

5.  コンソール ツリーで、クリックして**セキュリティ オプション**の下にある*GroupPolicyObject*[*ComputerName*] ポリシー/コンピューターの構成/Windows の設定/セキュリティ設定/ローカル ポリシー。

6.  詳細ウィンドウでダブルクリック**システム設定。Windows 実行可能ファイルに対して証明書の規則を使用して、ソフトウェア制限ポリシーの**します。

7.  ポリシー設定をまだ定義していない場合は、**[これらのポリシーの設定を定義する]** チェック ボックスをオンにします。

8.  次のいずれかの操作を行い、**[OK]** をクリックします。

    -   証明書の規則を有効にするには、**[有効]** をクリックします。

    -   証明書の規則を無効にするには、**[無効]** をクリックします。

#### <a name="BKMK_4"></a>ドメイン コント ローラーとのみの証明書の規則はドメイン コント ローラー上またはリモート サーバー管理ツールがインストールされているワークステーションに有効にするには

1.  [ドメイン コントローラー セキュリティの設定] を開きます。

2.  コンソール ツリーで、**GroupPolicyObject** [*ComputerName*] ポリシー/コンピューターの構成/Windows の設定/セキュリティの設定/ローカル ポリシー/ にある *[セキュリティ オプション]* をクリックします。

3.  詳細ウィンドウでダブルクリック**システム設定。Windows 実行可能ファイルに対して証明書の規則を使用して、ソフトウェア制限ポリシーの**します。

4.  ポリシー設定をまだ定義していない場合は、**[これらのポリシーの設定を定義する]** チェック ボックスをオンにします。

5.  次のいずれかの操作を行い、**[OK]** をクリックします。

    -   証明書の規則を有効にするには、**[有効]** をクリックします。

    -   証明書の規則を無効にするには、**[無効]** をクリックします。

> [!NOTE]
> 証明書の規則を有効にするには、この手順を実行する必要があります。

### <a name="set-trusted-publisher-options"></a>信頼された発行元のオプションを設定します。
ソフトウェアの署名は、増え続けるソフトウェア発行者およびアプリケーション開発者によって、そのアプリケーションの発行元が信頼できることを確認するために使用されています。 しかし、多くのユーザーは、自分がインストールするアプリケーションに関連付けられている署名証明書について理解していないか、ほとんど関心がありません。

管理者は証明書パスの検証ポリシーの **[信頼された発行元]** タブにあるポリシー オプションを使って、信頼できる発行元の証明書として許可する証明書を制御できます。

##### <a name="to-configure-the-trusted-publishers-policy-settings-for-a-local-computer"></a>ローカル コンピューターの信頼された発行元ポリシー設定を構成するには

1.  **開始**画面で「**gpedit.msc**し、ENTER キーを押します。

2.  コンソール ツリーで、**[ローカル コンピューター ポリシー\コンピューターの構成\Windows の設定\セキュリティの設定]** の **[公開キーのポリシー]** をクリックします。

3.  **[証明書パス検証の設定]** をダブルクリックし、**[信頼された発行元]** タブをクリックします。

4.  **[これらのポリシーの設定を定義する]** チェック ボックスをオンにし、適用するポリシー設定を選択します。**[OK]** をクリックして新しい設定を適用します。

##### <a name="to-configure-the-trusted-publishers-policy-settings-for-a-domain"></a>ドメインの信頼された発行元ポリシー設定を構成するには

1.  開いている**グループ ポリシー管理**します。

2.  コンソール ツリーで、ダブルクリック**グループ ポリシー オブジェクト**フォレストおよびドメインを含む、**既定のドメイン ポリシー**を編集するグループ ポリシー オブジェクト (GPO)。

3.  **[既定のドメイン ポリシー]** GPO を右クリックし、 **[編集]** をクリックします。

4.  コンソール ツリーで、**[コンピューターの構成\Windows の設定\セキュリティの設定]** の **[公開キーのポリシー]** をクリックします。

5.  **[証明書パス検証の設定]** をダブルクリックし、**[信頼された発行元]** タブをクリックします。

6.  **[これらのポリシーの設定を定義する]** チェック ボックスをオンにし、適用するポリシー設定を選択します。**[OK]** をクリックして新しい設定を適用します。

##### <a name="to-allow-only-administrators-to-manage-certificates-used-for-code-signing-for-a-local-computer"></a>ローカル コンピューターのコード署名に使用される証明書の管理を管理者のみに許可するには

1.  **開始**画面、型、 **gpedit.msc**で、**プログラムとファイルの検索**または Windows 8 でデスクトップ、および ENTER キーを押します。

2.  下のコンソール ツリーで**既定のドメイン ポリシー**または**ローカル コンピューター ポリシー**、ダブルクリックして**コンピューターの構成**、 **Windowsの設定**、および**セキュリティ設定**、 をクリックし、**公開キーのポリシー**します。

3.  **[証明書パス検証の設定]** をダブルクリックし、**[信頼された発行元]** タブをクリックします。

4.  **[これらのポリシーの設定を定義する]** チェック ボックスをオンにします。

5.  **[信頼された発行元の管理]** の **[すべての管理者のみに信頼される発行元の管理を許可する]** をクリックし、**[OK]** をクリックして新しい設定を適用します。

##### <a name="to-allow-only-administrators-to-manage-certificates-used-for-code-signing-for-a-domain"></a>ドメインのコード署名に使用される証明書の管理を管理者のみに許可するには

1.  開いている**グループ ポリシー管理**します。

2.  コンソール ツリーで、ダブルクリック**グループ ポリシー オブジェクト**フォレストおよびドメインを含む、**既定のドメイン ポリシー** GPO を編集します。

3.  **[既定のドメイン ポリシー]** GPO を右クリックし、 **[編集]** をクリックします。

4.  コンソール ツリーで、**[コンピューターの構成\Windows の設定\セキュリティの設定]** の **[公開キーのポリシー]** をクリックします。

5.  **[証明書パス検証の設定]** をダブルクリックし、**[信頼された発行元]** タブをクリックします。

6.  **[これらのポリシーの設定を定義する]** チェック ボックスをオンにし、必要な変更を行い、**[OK]** をクリックして新しい設定を適用します。

## <a name="BKMK_Hash_Rules"></a>ハッシュの規則の操作
ハッシュとは、ソフトウェア プログラムまたはファイルを一意に特定できる固定長のバイトです。 ハッシュは、ハッシュ アルゴリズムによる計算で導き出されます。 あるソフトウェア プログラムについてハッシュの規則を作成すると、ソフトウェアの制限のポリシーによってプログラムのハッシュが計算されます。 ユーザーがソフトウェア プログラムを開こうとした時点で、プログラムのハッシュがソフトウェアの制限のポリシーの既存のハッシュの規則と比較されます。 ソフトウェア プログラムのハッシュは、そのプログラムがコンピューターのどこに置かれていても、常に同じです。 ただし、ソフトウェア プログラムがなんらかの形で変更されていると、ハッシュも変化します。このため、そのハッシュは、ソフトウェアの制限のポリシーのハッシュの規則によるハッシュと一致しなくなります。

たとえば、ハッシュの規則を作成してセキュリティ レベルを **[許可しない]** に設定すると、ユーザーが特定のファイルを実行できなくすることができます。 ファイルは名前の変更のほか、別のフォルダーに移動した場合でも、同じハッシュとなります。 ただし、ファイルそのものに変更を加えた場合には、ハッシュ値が変化するため、ファイルが制限の対象外になります。

#### <a name="to-create-a-hash-rule"></a>ハッシュの規則を作成するには

1.  [ソフトウェアの制限のポリシー] を開きます。

2.  コンソール ツリーまたは詳細ウィンドウで、右クリック**追加ルール**、 をクリックし、**新しいハッシュの規則**。

3.  クリックして**参照**ファイルを検索します。

    > [!NOTE]
    > Windows xp で事前に計算されたハッシュを貼り付けすることは**ファイル ハッシュ**します。 Windows Server 2008 R2、Windows 7 以降のバージョンでこのオプションは使用できません。

4.  **セキュリティ レベル**、 をクリックするか**許可しない**または**Unrestricted**します。

5.  **[説明]** にこの規則の説明を入力し、**[OK]** をクリックします。

> [!NOTE]
> -   グループ ポリシー オブジェクト (GPO) についてソフトウェアの制限のポリシーの設定を作成していない場合には、この設定の新規作成が必要になることがあります。
> -   ウイルスやトロイの木馬の実行を防ぐことを目的としてハッシュの規則を作成することができます。
> -   他のユーザーにウイルスが実行されないように、ハッシュの規則を使用する場合は、ソフトウェアの制限のポリシーを使用して、ウイルスのハッシュを計算し、ハッシュ値を他のユーザーを電子メールで送信します。 ウイルス自体を電子メールで送信されません。
> -   ウイルスが電子メールで送信された場合は、電子メールの添付ファイルの実行を防止するためのパス規則を作成することもできます。
> -   ファイルの名前を変更したり、別のフォルダーに移動したりした場合には、ハッシュは変わりません。 異なるハッシュ結果ファイル自体を変更します。
> -   ハッシュの規則の影響を受けるファイルの種類は、ソフトウェアの制限のポリシーの詳細ウィンドウの **[指定されたファイルの種類]** に列挙されているもののみです。 指定されたファイルの種類の一覧は 1 つであり、それがあらゆる規則の間で共有されます。
> -   ソフトウェア制限のポリシーを有効にする、ユーザーからログオフし、自分のコンピューターにログオンしてポリシー設定を更新する必要があります。
> -   ポリシーの設定には、複数のソフトウェアの制限のポリシー規則が適用されるときに競合を処理するためのルールの優先順位があります。

## <a name="BKMK_Internet_Zone_Rules"></a>インターネット ゾーンの規則の操作
インターネット ゾーンの規則は、Windows インストーラー パッケージにのみ適用されます。 ゾーンの規則では、Internet Explorer で指定したゾーンから来たソフトウェアを特定できます。 ゾーンには、インターネット、ローカル イントラネット、制限付きサイト、信頼済みサイト、およびマイ コンピューターがあります。 インターネット ゾーンの規則は、ユーザーがダウンロードとソフトウェアをインストールできないように設計されています。

#### <a name="to-create-an-internet-zone-rule"></a>インターネット ゾーンの規則を作成するには

1.  [ソフトウェアの制限のポリシー] を開きます。

2.  コンソール ツリーまたは詳細ウィンドウで、右クリック**追加ルール**、 をクリックし、**新しいインターネット ゾーンの規則**。

3.  **[インターネット ゾーン]** で、インターネット ゾーンをクリックします。

4.  **セキュリティ レベル**、いずれかをクリックします**許可しない**または**Unrestricted**、順にクリックします**OK**します。

> [!NOTE]
> -   グループ ポリシー オブジェクト (GPO) についてソフトウェアの制限のポリシーの設定を作成していない場合には、この設定の新規作成が必要になることがあります。
> -   ゾーンの規則は、.msi ファイル (Windows インストーラー パッケージ) にのみ適用されます。
> -   ソフトウェア制限のポリシーを有効にする、ユーザーからログオフし、自分のコンピューターにログオンしてポリシー設定を更新する必要があります。
> -   ポリシーの設定には、複数のソフトウェアの制限のポリシー規則が適用されるときに競合を処理するためのルールの優先順位があります。

## <a name="BKMK_Path_Rules"></a>パスの規則の操作
パスの規則では、ファイル パスによってソフトウェアを特定します。 たとえば、既定のセキュリティ レベルが **[許可しない]** になっているコンピューターでも、各ユーザーに特定のフォルダーに対する無制限のアクセス権を付与することができます。 これには、ファイル パスを使用してパスの規則を作成し、そのセキュリティ レベルを **[制限なし]** に設定します。 この種の規則でよく使用するパスは、%userprofile%、%windir%、%appdata%、%programfiles%、および %temp% です。 このほか、ソフトウェアのレジストリ キーをパスとして使用したレジストリ パスの規則を作成できます。

ここに挙げた規則はパスを使って指定するため、ソフトウェア プログラムを移動すると、パスの規則が適用されなくなります。

#### <a name="to-create-a-path-rule"></a>パスの規則を作成するには

1.  [ソフトウェアの制限のポリシー] を開きます。

2.  コンソール ツリーまたは詳細ウィンドウで、右クリック**追加ルール**、 をクリックし、**新しいパスの規則**。

3.  **[パス]** で、パスを入力するか、**[参照]** をクリックしてファイルまたはフォルダーを指定します。

4.  **セキュリティ レベル**、 をクリックするか**許可しない**または**Unrestricted**します。

5.  **[説明]** にこの規則の説明を入力し、**[OK]** をクリックします。

> [!CAUTION]
> -   特定のフォルダーで、Windows フォルダーなど、セキュリティ設定レベルを**許可しない**オペレーティング システムの動作が低下します。 オペレーティング システムまたはそれに依存するプログラムに不可欠な要素を許可しない設定にしないようにしてください。

> [!NOTE]
> -   グループ ポリシー オブジェクト (GPO) についてソフトウェアの制限のポリシーを作成していない場合には、このポリシーの新規作成が必要になることがあります。
> -   ソフトウェアにパスの規則を作成し、セキュリティ レベルを **[許可しない]** に設定している場合には、そのソフトウェアを別の場所にコピーすると、そのソフトウェアを依然として実行できます。
> -   パスの規則でサポートされているワイルドカード文字は、* と ? です。
> -   パスの規則には、環境変数 (%programfiles%、%systemroot% など) を使用できます。
> -   コンピューターのどこに保存されているかはわからないものの、レジストリ キーはわかっているソフトウェアについて、パスの規則を作成するときには、レジストリ パスの規則を作成します。
> -   ユーザーが電子メールの添付ファイルを実行できないようにするには、電子メールの添付ファイルを実行できないように、電子メール プログラムの添付ファイルのディレクトリ パスの規則を作成できます。
> -   パスの規則の影響を受けるファイルの種類は、ソフトウェアの制限のポリシーの詳細ウィンドウの **[指定されたファイルの種類]** に列挙されているもののみです。 指定されたファイルの種類の一覧は 1 つであり、それがあらゆる規則の間で共有されます。
> -   ソフトウェア制限のポリシーを有効にする、ユーザーからログオフし、自分のコンピューターにログオンしてポリシー設定を更新する必要があります。
> -   ポリシーの設定には、複数のソフトウェアの制限のポリシー規則が適用されるときに競合を処理するためのルールの優先順位があります。

#### <a name="to-create-a-registry-path-rule"></a>レジストリ パスの規則を作成するには

1.  **開始**画面で「regedit」と入力します。

2.  コンソール ツリーで、規則を作成するレジストリ キーを右クリックし、**[キー名のコピー]** をクリックします。 詳細ウィンドウに表示されている値の名前を確認してください。

3.  [ソフトウェアの制限のポリシー] を開きます。

4.  コンソール ツリーまたは詳細ウィンドウで、右クリック**追加ルール**、 をクリックし、**新しいパスの規則**。

5.  **パス**、続いて値名レジストリ キー名を貼り付けます。

6.  レジストリ パスは、パーセント記号 (%)、たとえば、%hkey_local_machine\software\microsoft\platformsdk\directories\installdir% で囲みます。

7.  **セキュリティ レベル**、 をクリックするか**許可しない**または**Unrestricted**します。

8.  **[説明]** にこの規則の説明を入力し、**[OK]** をクリックします。


