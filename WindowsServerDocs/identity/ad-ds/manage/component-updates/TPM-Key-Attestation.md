---
ms.assetid: 16a344a9-f9a6-4ae2-9bea-c79a0075fd04
title: TPM キーの構成証明
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 3cfc047fe1a66617abbda1de5f2c5842dcbdeb12
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862883"
---
# <a name="tpm-key-attestation"></a>TPM キーの構成証明

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

**作成者**:Justin Turner、シニア サポート エスカレーション エンジニア、Windows グループ  
  
> [!NOTE]  
> この内容は Microsoft カスタマー サポート エンジニアによって作成され、TechNet が通常提供しているトピックよりも詳細な Windows Server 2012 R2 の機能やソリューションの技術的説明を求めている、経験豊かな管理者とシステム設計者を対象としています。 ただし、TechNet と同様の編集過程は実施されていないため、言語によっては通常より洗練されていない文章が見られる場合があります。  
  
## <a name="overview"></a>概要  
サポートの中に、Windows 8 以降 TPM で保護されたキーが存在していたはありませんでした Ca が暗号によってトラステッド プラットフォーム モジュール (TPM) によって証明書の要求者の秘密キーが実際に保護されることを証明するためのメカニズム。 この更新により、その構成証明を実行して、発行された証明書では、その構成証明を反映するように CA です。  
  
> [!NOTE]  
> この記事では、リーダーが証明書テンプレートの概念に精通している前提としています (リファレンスについては、次を参照してください。[証明書テンプレート](https://technet.microsoft.com/library/cc730705.aspx))。 リーダーが証明書テンプレートに基づいて証明書を発行するエンタープライズ Ca を構成する方法を理解することも想定 (リファレンスについては、次を参照してください。[チェックリスト。発行する Ca を構成して、証明書の管理](https://technet.microsoft.com/library/cc771533.aspx))。  
  
### <a name="terminology"></a>用語  
  
|用語|定義|  
|--------|--------------|  
|EK|保証キー。 これは、(製造時に挿入された) TPM 内に含まれる非対称キーです。 EK は、tpm ごとに一意な識別できます。 EK を変更したり、削除したりすることはできません。|  
|EKpub|EK の公開キーを表します。|  
|EKPriv|EK の秘密キーを表します。|  
|EKCert|EK 証明書。 TPM の製造元が発行した証明書 EKPub の。 すべての Tpm では、EKCert があります。|  
|TPM|トラステッド プラットフォーム モジュール。 TPM はハードウェア ベースのセキュリティ関連機能を提供する設計されています。 TPM チップは、暗号化操作を実行するように設計されたセキュアな暗号プロセッサです。 このチップには、改ざんに強い複数の物理セキュリティ メカニズムが搭載されており、悪意のあるソフトウェアが TPM のセキュリティ機能を破ることはできません。|  
  
### <a name="background"></a>背景  
Windows 8 以降では、トラステッド プラットフォーム モジュール (TPM) を使用して証明書の秘密キーをセキュリティで保護します。 Microsoft プラットフォーム暗号化プロバイダー キー格納プロバイダー (KSP) では、この機能を有効します。 実装に関する 2 つの問題が発生しました。  

-   キーが実際には、(だれかが簡単にスプーフィングするソフトウェア KSP としてのローカル管理者の資格情報での TPM KSP) TPM によって保護されている保証はありませんでした。

-   (イベントで、PKI 管理者では、環境で証明書の取得に使用できるデバイスの種類を制御しようとして)、証明書を発行する企業を保護できるは Tpm のリストを制限することでした。  

### <a name="tpm-key-attestation"></a>TPM キーの構成証明  
TPM キー認証は、暗号化された証明書要求の RSA キーが CA を信頼するか、"a"または「、」TPM によって保護されていることを CA に証明するために、証明書を要求したエンティティの機能です。 TPM の信頼モデルの詳細については、[展開の概要](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_DeploymentOverview)このトピックで後述します。  
  
### <a name="why-is-tpm-key-attestation-important"></a>TPM キー認証が重要な理由  
TPM 証明キーを持つユーザーの証明書は、非エクスポート可能性、ハンマリング対策および TPM によって提供されるキーの分離によってバックアップより高いセキュリティ保証を提供します。  
  
TPM キー認証で新しい管理パラダイムが可能になりました。管理者は、ユーザーが VPN やワイヤレス アクセス ポイントなど) で企業リソースにアクセスして使用できるデバイスのセットを定義できます**強力な**それらにアクセスするその他のデバイスが使用されませんが保証されます。 この新しいアクセス制御のパラダイムは**強力な**に結び付けられているので、*ハードウェア バインド*ユーザー id は、ソフトウェア ベースの資格情報よりも強力です。
  
### <a name="how-does-tpm-key-attestation-work"></a>TPM キー認証のしくみ  
一般に、TPM キー認証は、次の柱に基づいています。  
  
1.  TPM ごとに固有の非対称キーでは、付属と呼ばれる、*保証キー*製造元によって書き込まれた (EK)。 としてこのキーの公開部分を参照してください*EKPub*と関連付けられている秘密キーに*EKPriv*します。 TPM チップでは、EKPub の製造元によって発行される EK 証明書もあります。 としてこの証明書を参照してください*EKCert*します。  
  
2.  CA は、TPM EKPub または EKCert のいずれかの信頼を確立します。  
  
3.  ユーザーは、証明書を要求する対象の RSA キーが、EKPub に関連する暗号化に使用して、ユーザーが、EKpriv を所有していることを CA に証明します。  
  
4.  CA は、特別な発行ポリシーをキーが TPM で保護するようになりました attested ことを示すために OID と証明書を発行します。  
  
## <a name="BKMK_DeploymentOverview"></a>展開の概要  
この展開で Windows Server 2012 R2 のエンタープライズ CA が設定されていると見なされます。 また、エンタープライズ CA を使用してそのに対して登録する (Windows 8.1) が構成されているクライアントの証明書テンプレート。 

TPM キー認証を展開する手順は次の 3 つです。  
  
1.  **TPM の信頼モデルを計画します。** 最初の手順では、TPM を使用する信頼モデルを決定します。 これを行うための 3 つのサポートされている方法はあります。  
  
    -   **ユーザーの資格情報に基づく信頼:** エンタープライズ CA が証明書の要求の一部として、ユーザー指定の EKPub を信頼し、検証は実行されません、ユーザーのドメイン資格情報以外。  
  
    -   **EKCert に基づいて信頼:** エンタープライズ CA には、管理者が管理の一覧と、証明書要求の一部として提供されている EKCert チェーンが検証されます。 *EK 証明書チェーンの許容される*します。 許容されるチェーンでは、製造元ごとの定義と、(中間の 1 つのストア) は、ルート CA 証明書のいずれかの発行元 CA で、2 つのカスタム証明書ストアを使用して表されます。 この信頼モードでは、ことを意味**すべて**特定の製造元から Tpm に信頼されます。 このモードで Tpm 環境で使用されている必要がありますを含む EKCerts に注意してください。
  
    -   **EKPub に基づいて信頼:** エンタープライズ CA の管理者が管理リストが表示されます、証明書要求の一部として指定された EKPub EKPubs が許可されることを検証します。 この一覧は、このディレクトリ内の各ファイルの名前は許可されている EKPub の sha-2 ハッシュのファイルのディレクトリとして表されます。 このオプションは、最高の保証レベルを提供していますが、各デバイスが個別に識別されるため、複数の管理作業が必要です。 この信頼モデルでは、その TPM の EKPub が EKPubs の許可リストに追加されているデバイスのみが TPM attested 証明書を登録する許可されます。  
  
    CA は、どのメソッドを使用すると、によって発行された証明書に別の発行ポリシー OID が適用されます。 発行ポリシー Oid の詳細については、発行ポリシー Oid の表を参照してください、[証明書テンプレートを構成する](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_ConfigCertTemplate)このトピックの「します。  
  
    TPM に信頼されたモデルの組み合わせを選択することはことに注意してください。 この場合、CA を受け入れるすべての構成証明の方法と、発行ポリシーの Oid が成功するすべての構成証明メソッドに反映されます。  
  
2.  **証明書テンプレートを構成するには。**「証明書テンプレートを構成する、[展開の詳細](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_DeploymentDetails)このトピック「します。 この記事ではないこの証明書テンプレートをエンタープライズ CA を割り当てる方法について説明または登録する方法のユーザーのグループに付与されます。 詳細については、次を参照してください。[チェックリスト。発行する Ca を構成して、証明書の管理](https://technet.microsoft.com/library/cc771533.aspx)します。  
  
3.  **TPM の信頼モデルの CA を構成します。**  
  
    1.  **ユーザーの資格情報に基づく信頼:** 特定の構成は必要ありません。  
  
    2.  **EKCert に基づいて信頼:** 管理者は、TPM の製造元から EKCert チェーンの証明書を取得し、TPM キー認証を実行する CA で、管理者によって作成された、2 つの新しい証明書ストアにインポートする必要があります。 詳細については、次を参照してください。、 [CA 構成](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_CAConfig)このトピックの「します。  
  
    3.  **EKPub に基づいて信頼:** 管理者は TPM attested 証明書が必要し、許可されている EKPubs のリストに追加される各デバイスの EKPub を取得する必要があります。 詳細については、次を参照してください。、 [CA 構成](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_CAConfig)このトピックの「します。  
  
    > [!NOTE]  
    > -   この機能には、Windows 8.1/Windows Server 2012 R2 が必要です。  
    > -   サード パーティ製のスマート カード Ksp の TPM キー認証がサポートされていません。 Microsoft プラットフォーム暗号化プロバイダーの KSP を使用する必要があります。  
    > -   TPM キー認証は、RSA キーに対してのみ機能します。  
    > -   スタンドアロン CA では、TPM キー認証はサポートされていません。  
    > -   TPM キー認証はサポートしていません[非永続的証明書の処理](https://technet.microsoft.com/library/ff934598)します。  
  
## <a name="BKMK_DeploymentDetails"></a>展開の詳細  
  
### <a name="BKMK_ConfigCertTemplate"></a>証明書テンプレートを構成します。  
TPM キー認証の証明書テンプレートを構成するには、次の構成手順を実行します。  
  
1.  **互換性** タブ  
  
    **互換性設定**セクション。  
  
    -   確認**Windows Server 2012 R2**が選択されている、**証明機関**します。  
  
    -   確認**Windows 8.1/Windows Server 2012 R2**が選択されている、**証明書の受信者**します。  
  
    ![TPM キーの構成証明](media/TPM-Key-Attestation/GTR_ADDS_CompatibilityTab.gif)  
  
2.  **暗号化** タブ  
  
    確認**Key Storage Provider**が選択されている、**プロバイダーのカテゴリ**と**RSA**が選択されている、**アルゴリズム名**します。 確認**要求は、次のプロバイダーのいずれかを使用する必要があります**が選択されていると、 **Microsoft プラットフォーム暗号化プロバイダー**オプションを選択する**プロバイダー**します。  
  
    ![TPM キーの構成証明](media/TPM-Key-Attestation/GTR_ADDS_CryptoTab.gif)  
  
3.  **キーの構成証明** タブ  
  
    これは、Windows Server 2012 R2 用に新しいタブです。  
  
    ![TPM キーの構成証明](media/TPM-Key-Attestation/GTR_ADDS_ConfigCertTemplate.gif)  
  
    3 つのオプションから、構成証明モードを選択します。  
  
    ![TPM キーの構成証明](media/TPM-Key-Attestation/GTR_ADDS_KeyModes.gif)  
  
    -   **None:** キーの構成証明を使用しない必要がありますを意味します。  
  
    -   **必要に応じて、クライアントが対応している場合。** その証明書の登録を続行する TPM キー認証をサポートしていないデバイス上には、ユーザーを許可します。 構成証明を実行できるユーザーは、特別な発行ポリシー OID で識別されます。 一部のデバイスはできないため、キーの構成証明または TPM がまったくないデバイスをサポートしない古い TPM 構成証明を実行することがあります。
  
    -   **必須：** クライアント*する必要があります*、TPM キー認証を実行して、それ以外の場合、証明書の要求は失敗します。  
  
    次に、TPM の信頼モデルを選択します。 もう一度は 3 つのオプションがあります。  
  
    ![TPM キーの構成証明](media/TPM-Key-Attestation/GTR_ADDS_KeyTypeToEnforce.gif)  
  
    -   **ユーザーの資格情報:** ドメイン資格情報を指定することで有効な TPM を保証するユーザーが認証を許可します。  
  
    -   **保証証明書:** デバイスの EKCert は、管理者が管理 TPM 中間 CA 証明書によって、管理者に管理されたルート CA 証明書を検証する必要があります。 このオプションを選択する場合は、場合と EKRoot を設定する必要があります」の説明に従って、発行元 CA 上のストアの証明書、 [CA 構成](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_CAConfig)このトピックの「します。  
  
    -   **保証キー:** デバイスの EKPub は、PKI 管理者が管理一覧に表示する必要があります。 このオプションは、最高の保証レベルを提供していますが、管理の労力が必要です。 このオプションを選択する場合、必要がありますを設定する発行元 ca を EKPub リスト」の説明に従って、 [CA 構成](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_CAConfig)このトピックの「します。  
  
    最後に、発行された証明書に表示するには、どの発行ポリシーを決定します。 既定では、それぞれの強制の種類は、次の表に示すように、その強制型をパスした場合、証明書に挿入される関連付けられたオブジェクト識別子 (OID) を持ちます。 強制方法の組み合わせを選択することはことに注意してください。 ここでは、構成証明の方法のいずれか、CA はそのまま使用され、発行ポリシー OID には、すべての構成証明メソッドが成功したことが反映されます。  
  
    **発行ポリシー Oid**  
  
    |OID|キーの構成証明の種類|説明|保証レベル|  
    |-------|------------------------|---------------|-------------------|  
    |1.3.6.1.4.1.311.21.30|EK|"EK ことを確認します。" EK の一覧を管理者が管理について|高|  
    |1.3.6.1.4.1.311.21.31|証明書の保証|「EK 証明書の検証」:EK 証明書チェーンを検証するとき|中|  
    |1.3.6.1.4.1.311.21.32|ユーザーの資格情報|「EK は、使用するときに信頼できる。」ユーザー証明 EK の|低|  
  
    Oid の場合、発行された証明書に挿入されます**発行ポリシーを含める**は (既定の構成) を選択します。  
  
    ![TPM キーの構成証明](media/TPM-Key-Attestation/GTR_ADDS_IssuancePolicies.gif)  
  
    > [!TIP]  
    > 証明書の OID の潜在的な用途の 1 つは、VPN へのアクセスを制限またはワイヤレス ネットワークの特定のデバイスにすることです。 たとえば、アクセス ポリシーが OID 1.3.6.1.4.1.311.21.30 が証明書に存在する場合、接続 (または別の VLAN へのアクセス) を許可できます。 これにより、その TPM EK が EKPUB リストに存在するデバイスへのアクセスを制限することができます。  
  
### <a name="BKMK_CAConfig"></a>CA の構成  
  
1.  **発行元の CA の場合と EKROOT の証明書ストアをセットアップします。**  
  
    選択した場合**保証証明書**テンプレートの設定には、次の構成手順を実行します。  
  
    1.  Windows PowerShell を使用すると、TPM キー認証を実行する証明機関 (CA) サーバー上の 2 つの新しい証明書ストアを作成できます。  
  
    2.  中間を取得し、エンタープライズ環境で許可する製造元からの CA 証明書のルートします。 必要に応じて以前に作成された証明書ストア (場合および EKROOT) には、これらの証明書をインポートする必要があります。  
  
    次の Windows PowerShell スクリプトは、両方の手順を実行します。 次の例では、Fabrikam の TPM の製造元が、ルート証明書を提供*FabrikamRoot.cer*と発行元の CA 証明書*Fabrikamca.cer*します。  
  
    ```powershell  
    PS C:>\cd cert:  
    PS Cert:\>cd .\\LocalMachine  
    PS Cert:\LocalMachine> new-item EKROOT  
    PS Cert:\ LocalMachine> new-item EKCA  
    PS Cert:\EKCA\copy FabrikamCa.cer .\EKCA  
    PS Cert:\EKROOT\copy FabrikamRoot.cer .\EKROOT  
    ```  
  
2.  **EK 構成証明書の種類を使用して場合 EKPUB リストを設定します。**  
  
    選択した場合**保証キー**テンプレートの設定で、[次へ] の構成手順が作成および発行元の ca では、0 バイトのファイルを含むフォルダーを構成するが、許可されている、EK の sha-2 ハッシュの各名前付き。 このフォルダーは、TPM キー attested 証明書の取得を許可するデバイスの"allow リスト"として機能します。 Attested の証明書を必要とする各デバイスの EKPUB を手動で追加する必要があります、ために、デバイスが TPM キー attested 証明書を取得する承認されていることを保証エンタープライズを提供します。 このモード用の CA を構成するには、2 つの手順が必要です。  
  
    1.  **EndorsementKeyListDirectories のレジストリ エントリを作成します。** Certutil コマンド ライン ツールを使用して、次の表に示すように信頼された EKpubs が定義されているフォルダーの場所を構成します。  
  
        |操作|コマンドの構文|  
        |-------------|------------------|  
        |フォルダーの場所を追加します。|certutil.exe -setreg CA\EndorsementKeyListDirectories +"<folder>"|  
        |フォルダーの場所を削除します。|certutil.exe -setreg CA\EndorsementKeyListDirectories -"<folder>"|  
  
        Certutil のコマンドで EndorsementKeyListDirectories では、次の表に示すように、レジストリ設定です。  
  
        |値の名前|種類|データ|  
        |--------------|--------|--------|  
        |EndorsementKeyListDirectories|REG_MULTI_SZ|< EKPUB へのローカルまたは UNC パスでは、リストを許可する ><br /><br />以下に例を示します。<br /><br />*\\\blueCA.contoso.com\ekpub*<br /><br />*\\\bluecluster1.contoso.com\ekpub*<br /><br />D:\ekpub|  
  
        HKLM\SYSTEM\CurrentControlSet\Services\CertSvc\Configuration\\<CA Sanitized Name>  
  
        *EndorsementKeyListDirectories*各 CA は、読み取りアクセス権を持つフォルダーを指す UNC またはローカル ファイル システム パスの一覧が含まれます。 各フォルダーは、0 を含めることができます。 または詳細は許可リストのエントリ、sha-2 である名前のファイルの各エントリが、信頼の EKpub のハッシュ ファイル拡張子なし。 
        作成またはこのレジストリ キーの構成を編集するには、既存の CA レジストリ構成の設定と同じように、CA の再起動が必要です。 ただし、構成設定の編集はすぐに反映され、CA を再起動する必要はありません。  
  
        > [!IMPORTANT]  
        > 改ざんからリスト内のフォルダーをセキュリティで保護し、ため、管理者にのみ承認されたアクセス許可を構成することによって、未承認のアクセスが読み取りおよび書き込みアクセス。 CA のコンピューター アカウントには、読み取り専用アクセスが必要です。  
  
    2.  **EKPUB リストを設定します。** 各デバイスで Windows PowerShell を使用して、TPM EK の公開キー ハッシュを取得して、この公開キー ハッシュを CA に送信し、EKPubList フォルダーに保存するには、次の Windows PowerShell コマンドレットを使用します。  
  
        ```powershell  
        PS C:>\$a=Get-TpmEndorsementKeyInfo -hashalgorithm sha256  
        PS C:>$b=new-item $a.PublicKeyHash -ItemType file  
        ```  
  
## <a name="troubleshooting"></a>トラブルシューティング  
  
### <a name="key-attestation-fields-are-unavailable-on-a-certificate-template"></a>キーの構成証明のフィールドは、証明書テンプレートを使用することはありません。  
キーの構成証明のフィールドは、テンプレートの設定が構成証明書の要件を満たしていない場合に使用できません。 一般的な理由は次のとおりです。  
  
1.  互換性設定が正しく構成されていません。 次のように構成されていることを確認します。  
  
    1.  **[証明機関]**:**Windows Server 2012 R2**  
  
    2.  **証明書の受信者**:**Windows 8.1/Windows Server 2012 R2**  
  
2.  暗号化の設定が正しく構成されていません。 次のように構成されていることを確認します。  
  
    1.  **プロバイダーのカテゴリ**:**キー記憶域プロバイダー**  
  
    2.  **アルゴリズム名**:**RSA**  
  
    3.  **プロバイダー**:**Microsoft プラットフォーム暗号化プロバイダー**  
  
3.  要求処理の設定が正しく構成されていません。 次のように構成されていることを確認します。  
  
    1.  **をエクスポートする秘密キーを許可する**オプションが選択されていない必要があります。  
  
    2.  **サブジェクトの秘密キーをアーカイブ**オプションが選択されていない必要があります。  
  
### <a name="verification-of-tpm-device-for-attestation"></a>TPM デバイス構成証明書の検証  
Windows PowerShell コマンドレットを使用して、**確認 CAEndorsementKeyInfo**、特定の TPM デバイスが Ca によって信頼されている構成証明書であることを確認します。 2 つのオプションがあります。 EKCert とその他、EKPub を検証するための確認のいずれか。 コマンドレットか、ローカルで実行またはリモート Ca の ca で Windows PowerShell リモート処理を使用しています。  
  
1.  EKPub での信頼を検証するためには、次の 2 つの手順を実行します。  
  
    1.  **クライアント コンピューターから、EKPub を抽出します。** 使用してクライアント コンピューターから抽出できる、EKPub **Get TpmEndorsementKeyInfo**します。 管理者特権でコマンド プロンプトで、次の手順を実行します。  
  
        ```  
        PS C:>\$a=Get-TpmEndorsementKeyInfo -hashalgorithm sha256  
        ```  
  
    2.  **CA コンピューターで、EKCert の信頼を確認します。**(たとえば、電子メール) 経由でサーバーに、抽出された文字列 (、EKPub の sha-2 のハッシュ) をコピーし、確認 CAEndorsementKeyInfo コマンドレットに渡します。 このパラメーターは 64 文字である必要がありますに注意してください。  
  
        ```  
        Confirm-CAEndorsementKeyInfo [-PublicKeyHash] <string>  
        ```  
  
2.  EKCert での信頼を検証するためには、次の 2 つの手順を実行します。  
  
    1.  **クライアント コンピューターから、EKCert を抽出します。** 使用してクライアント コンピューターから抽出できる、EKCert **Get TpmEndorsementKeyInfo**します。 管理者特権でコマンド プロンプトで、次の手順を実行します。  
  
        ```  
        PS C:>\$a=Get-TpmEndorsementKeyInfo
        PS C:>\$a.manufacturerCertificates|Export-Certificate -filepath c:\myEkcert.cer
        ```  
  
    2.  **CA コンピューターで、EKCert の信頼を確認します。** CA (たとえば、電子メールまたは xcopy) を介して展開された EKCert (EkCert.cer) にコピーします。 たとえば、CA サーバーでは、証明書ファイルの"c:\diagnose"フォルダーをコピーする場合は、検証を完了するには、次を実行します。  
  
        ```  
        PS C:>new-object System.Security.Cryptography.X509Certificates.X509Certificate2 "c:\diagnose\myEKcert.cer" | Confirm-CAEndorsementKeyInfo  
        ```  
  
## <a name="see-also"></a>関連項目  
[トラステッド プラットフォーム モジュール テクノロジの概要](https://technet.microsoft.com/library/jj131725.aspx)  
[外部のリソース:トラステッド プラットフォーム モジュール](http://www.cs.unh.edu/~it666/reading_list/Hardware/tpm_fundamentals.pdf)  
