---
ms.assetid: 16a344a9-f9a6-4ae2-9bea-c79a0075fd04
title: TPM キーの構成証明
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: d7104daaa10cf7093370cb309e0366e1ab2b9b51
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71389858"
---
# <a name="tpm-key-attestation"></a>TPM キーの構成証明

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

**作成者**:Justin 書籍、シニアサポートエスカレーションエンジニア (Windows グループ)  
  
> [!NOTE]  
> この内容は Microsoft カスタマー サポート エンジニアによって作成され、TechNet が通常提供しているトピックよりも詳細な Windows Server 2012 R2 の機能やソリューションの技術的説明を求めている、経験豊かな管理者とシステム設計者を対象としています。 ただし、TechNet と同様の編集過程は実施されていないため、言語によっては通常より洗練されていない文章が見られる場合があります。  
  
## <a name="overview"></a>概要  
TPM で保護されたキーのサポートは Windows 8 以降に存在していましたが、証明書の要求者の秘密キーがトラステッドプラットフォームモジュール (TPM) によって実際に保護されていることを Ca が暗号証明するメカニズムはありませんでした。 この更新により、CA はその構成証明を実行し、発行された証明書にその構成証明を反映させることができます。  
  
> [!NOTE]  
> この記事では、読者が証明書テンプレートの概念を理解していることを前提としています (詳細については、「[証明書テンプレート](https://technet.microsoft.com/library/cc730705.aspx)」を参照)。 また、証明書テンプレートに基づいて証明書を発行するようにエンタープライズ Ca を構成する方法については、読者が理解していることを前提としています (リファレンスについては、@no__t チェックリストを参照してください。証明書を発行および管理するように Ca を構成する @ no__t-0)。  
  
### <a name="terminology"></a>用語  
  
|項目|定義|  
|--------|--------------|  
|EK|保証キー。 これは、(製造時に挿入された) TPM 内に含まれる非対称キーです。 EK は、TPM ごとに一意であり、特定できます。 EK を変更または削除することはできません。|  
|EKpub|EK の公開キーを参照します。|  
|EKPriv|EK の秘密キーを参照します。|  
|EKCert|EK 証明書。 TPM 製造元によって発行された EKPub の証明書。 すべての Tpm が EKCert を持っているわけではありません。|  
|TPM|トラステッド プラットフォーム モジュール。 TPM は、ハードウェアベースのセキュリティ関連機能を提供するように設計されています。 TPM チップは、暗号化操作を実行するように設計されたセキュアな暗号プロセッサです。 このチップには、改ざんに強い複数の物理セキュリティ メカニズムが搭載されており、悪意のあるソフトウェアが TPM のセキュリティ機能を破ることはできません。|  
  
### <a name="background"></a>背景情報  
Windows 8 以降では、トラステッドプラットフォームモジュール (TPM) を使用して、証明書の秘密キーをセキュリティで保護することができます。 Microsoft Platform Crypto Provider キーストレージプロバイダー (KSP) を使用すると、この機能が有効になります。 実装には次の2つの問題がありました。  

-   キーが TPM によって実際に保護される保証はありませんでした (他のユーザーが、ローカル管理者の資格情報を持つ TPM KSP としてソフトウェア KSP を簡単に偽装できます)。

-   エンタープライズ発行の証明書を保護することが許可されている Tpm の一覧を制限することはできませんでした (PKI 管理者が環境内の証明書を取得するために使用できるデバイスの種類を制御する必要がある場合)。  

### <a name="tpm-key-attestation"></a>TPM キーの構成証明  
TPM キーの構成証明とは、証明書の要求に含まれる RSA キーが、CA が信頼する "a" または "a" のいずれかによって保護されていることを証明する証明書を要求するエンティティのことです。 TPM 信頼モデルの詳細については、このトピックで後述する「[展開の概要](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_DeploymentOverview)」を参照してください。  
  
### <a name="why-is-tpm-key-attestation-important"></a>TPM キーの構成証明が重要なのはなぜですか。  
TPM 証明キーを使用するユーザー証明書は、エクスポート、ハンマリング、TPM によって提供されるキーの分離によってバックアップされた、高いセキュリティ保証を提供します。  
  
TPM キーの構成証明により、新しい管理パラダイムが可能になりました。管理者は、ユーザーが会社のリソース (たとえば、VPN やワイヤレスアクセスポイント) にアクセスするために使用できるデバイスのセットを定義し、他のデバイスがアクセスに使用できないことを**強い**保証を持ちます。 この新しいアクセス制御パラダイムは、ソフトウェアベースの資格情報よりも強力な*ハードウェアバインド*ユーザー id に関連付けられているため、**強力**です。
  
### <a name="how-does-tpm-key-attestation-work"></a>TPM キーの構成証明はどのように機能しますか。  
一般に、TPM キーの構成証明は、次の柱に基づいています。  
  
1.  各 TPM には、製造元によって書き込まれた、*保証キー* (EK) と呼ばれる一意の非対称キーが付属しています。 このキーの公開部分を*EKPub*として、関連付けられている秘密キーを*EKPriv*と呼びます。 一部の TPM チップには、EKPub の製造元によって発行された EK 証明書もあります。 この証明書を*EKCert*と呼びます。  
  
2.  CA は、EKPub または EKCert のいずれかを使用して TPM で信頼を確立します。  
  
3.  証明書を要求している RSA キーが EKPub に対して暗号化されており、ユーザーが EKpriv を所有していることが、ユーザーによって CA に証明されます。  
  
4.  CA は、キーが TPM によって保護されるように証明されたことを示すために、特別な発行ポリシー OID を持つ証明書を発行します。  
  
## <a name="BKMK_DeploymentOverview"></a>展開の概要  
この展開では、Windows Server 2012 R2 enterprise CA がセットアップされていることを前提としています。 また、クライアント (Windows 8.1) は、証明書テンプレートを使用して、そのエンタープライズ CA に対して登録するように構成されています。 

TPM キーの構成証明を展開するには、次の3つの手順を実行します。  
  
1.  **TPM 信頼モデルを計画する:** 最初の手順は、使用する TPM 信頼モデルを決定することです。 これを行うには、次の3つの方法がサポートされています。  
  
    -   **ユーザー資格情報に基づく信頼:** エンタープライズ CA は、ユーザーが指定した EKPub を証明書要求の一部として信頼し、ユーザーのドメイン資格情報以外の検証は実行されません。  
  
    -   **EKCert に基づく信頼:** エンタープライズ CA は、証明書の要求の一部として提供されている EKCert チェーンを、管理者が管理する使用*可能な EK 証明書チェーン*の一覧に照らして検証します。 許容されるチェーンは製造元ごとに定義され、発行元 CA の2つのカスタム証明書ストア (中間のストアとルート CA 証明書のストア) を使用して表現されます。 この信頼モードは、特定の製造元からの**すべて**の tpm が信頼されていることを意味します。 このモードでは、環境内で使用される Tpm に EKCerts が含まれている必要があることに注意してください。
  
    -   **EKPub に基づく信頼:** エンタープライズ CA は、証明書の要求の一部として提供された EKPub が、管理者によって管理された許可された EKPubs の一覧に表示されることを検証します。 この一覧は、このディレクトリ内の各ファイルの名前が、許可されている EKPub の SHA-1 ハッシュであるファイルのディレクトリとして表されます。 このオプションは、最も高い保証レベルを提供しますが、各デバイスが個別に識別されるため、より多くの管理作業が必要です。 この信頼モデルでは、許可された EKPubs の一覧に TPM の EKPub が追加されているデバイスのみが、TPM-証明証明書の登録を許可されます。  
  
    使用する方法に応じて、CA は発行された証明書に別の発行ポリシー OID を適用します。 発行ポリシー Oid の詳細については、このトピックの「[証明書テンプレートの構成](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_ConfigCertTemplate)」セクションの「発行ポリシー oid」を参照してください。  
  
    TPM 信頼モデルの組み合わせを選択できることに注意してください。 この場合、CA は任意の構成証明方法を受け入れ、発行ポリシー Oid は成功したすべての構成証明方法を反映します。  
  
2.  **証明書テンプレートを構成します。** 証明書テンプレートの構成については、このトピックの「[展開の詳細](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_DeploymentDetails)」セクションを参照してください。 この記事では、この証明書テンプレートがエンタープライズ CA にどのように割り当てられるか、またはユーザーのグループに登録アクセスが付与される方法については説明しません。 詳細については、「@no__t」チェックリストを参照してください。証明書を発行および管理するように Ca を構成する @ no__t-0。  
  
3.  **TPM 信頼モデル用に CA を構成する**  
  
    1.  **ユーザー資格情報に基づく信頼:** 特定の構成は必要ありません。  
  
    2.  **EKCert に基づく信頼:** 管理者は、tpm キーの構成証明を実行する CA で、TPM の製造元から EKCert チェーン証明書を取得し、管理者によって作成された2つの新しい証明書ストアにインポートする必要があります。 詳細については、このトピックの「 [CA 構成](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_CAConfig)」セクションを参照してください。  
  
    3.  **EKPub に基づく信頼:** 管理者は、TPM 証明証明書を必要とする各デバイスの EKPub を取得し、許可されている EKPubs の一覧に追加する必要があります。 詳細については、このトピックの「 [CA 構成](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_CAConfig)」セクションを参照してください。  
  
    > [!NOTE]  
    > -   この機能には Windows 8.1/Windows Server 2012 R2 が必要です。  
    > -   サードパーティのスマートカード KSPs の TPM キーの構成証明はサポートされていません。 Microsoft プラットフォーム暗号化プロバイダー KSP を使用する必要があります。  
    > -   TPM キーの構成証明は、RSA キーに対してのみ機能します。  
    > -   スタンドアロン CA では、TPM キーの構成証明はサポートされていません。  
    > -   TPM キーの構成証明は[、非永続的な証明書の処理](https://technet.microsoft.com/library/ff934598)をサポートしていません。  
  
## <a name="BKMK_DeploymentDetails"></a>デプロイの詳細  
  
### <a name="BKMK_ConfigCertTemplate"></a>証明書テンプレートを構成する  
TPM キーの構成証明用の証明書テンプレートを構成するには、次の構成手順を実行します。  
  
1.  **[互換性]** タブ  
  
    **[互換性の設定]** セクションで、次の手順を実行します。  
  
    -   **証明機関**に対して**Windows Server 2012 R2**が選択されていることを確認します。  
  
    -   **証明書の受信者**に**Windows 8.1/Windows Server 2012 R2**が選択されていることを確認します。  
  
    ![TPM キーの構成証明](media/TPM-Key-Attestation/GTR_ADDS_CompatibilityTab.gif)  
  
2.  **[暗号化]** タブ  
  
    [**プロバイダー] カテゴリ**に **[キー記憶域プロバイダー]** が選択されていることと、**アルゴリズム名**に**RSA**が選択されていることを確認します。 **[プロバイダー]** で [**次のプロバイダーのいずれかを使用する必要があり** **ます] が**選択されていることを確認します。  
  
    ![TPM キーの構成証明](media/TPM-Key-Attestation/GTR_ADDS_CryptoTab.gif)  
  
3.  **[キーの構成証明]** タブ  
  
    これは、Windows Server 2012 R2 の新しいタブです。  
  
    ![TPM キーの構成証明](media/TPM-Key-Attestation/GTR_ADDS_ConfigCertTemplate.gif)  
  
    使用可能な3つのオプションから構成証明モードを選択します。  
  
    ![TPM キーの構成証明](media/TPM-Key-Attestation/GTR_ADDS_KeyModes.gif)  
  
    -   **存在**キーの構成証明を使用できないことを意味します。  
  
    -   **クライアントに対応できる場合は必須。** TPM キーの構成証明をサポートしていないデバイスのユーザーが、その証明書への登録を続行できるようにします。 構成証明を実行できるユーザーは、特別な発行ポリシー OID と区別されます。 一部のデバイスは、キーの構成証明をサポートしていない古い TPM が原因で構成証明を実行できないか、デバイスに TPM がまったくないため、構成証明を実行できない可能性があります。
  
    -   **必須：** クライアントは、TPM キーの構成証明を実行*する必要があり*ます。そうしないと、証明書の要求は失敗します。  
  
    次に、TPM 信頼モデルを選択します。 次の3つのオプションがあります。  
  
    ![TPM キーの構成証明](media/TPM-Key-Attestation/GTR_ADDS_KeyTypeToEnforce.gif)  
  
    -   **ユーザーの資格情報:** 認証ユーザーがドメインの資格情報を指定して有効な TPM を保証できるようにします。  
  
    -   **保証証明書:** デバイスの EKCert は、管理者が管理する TPM 中間 CA 証明書を使用して、管理者によって管理されるルート CA 証明書に対して検証を行う必要があります。 このオプションを選択する場合は、このトピックの「 [ca の構成](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_CAConfig)」セクションの説明に従って、発行元の CA に EKCA と EKRoot の証明書ストアを設定する必要があります。  
  
    -   **保証キー:** デバイスの EKPub が [PKI 管理者の管理] 一覧に表示されている必要があります。 このオプションは、最も高い保証レベルを提供しますが、より多くの管理作業が必要です。 このオプションを選択する場合は、このトピックの「 [ca の構成](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_CAConfig)」セクションの説明に従って、発行元の Ca で EKPub リストを設定する必要があります。  
  
    最後に、発行された証明書に表示する発行ポリシーを決定します。 既定では、各強制型には関連付けられたオブジェクト識別子 (OID) があり、次の表に示すように、その強制型に合格した場合に証明書に挿入されます。 強制方法の組み合わせを選択できることに注意してください。 この場合、CA は任意の構成証明方法を受け入れ、発行ポリシー OID は成功したすべての構成証明方法を反映します。  
  
    **発行ポリシー Oid**  
  
    |OID|キーの構成証明の種類|説明|保証レベル|  
    |-------|------------------------|---------------|-------------------|  
    |1.3.6.1.4.1.311.21.30|EK|"EK 検証済み": 管理者によって管理される EK のリストの場合|高|  
    |1.3.6.1.4.1.311.21.31|保証証明書|"EK 証明書の検証済み":EK 証明書チェーンが検証されたとき|Medium|  
    |1.3.6.1.4.1.311.21.32|ユーザーの資格情報|"使用中に信頼された EK":ユーザー-証明 EK の場合|Low|  
  
    [発行**ポリシーを含める**] が選択されている場合 (既定の構成)、oid は発行された証明書に挿入されます。  
  
    ![TPM キーの構成証明](media/TPM-Key-Attestation/GTR_ADDS_IssuancePolicies.gif)  
  
    > [!TIP]  
    > 証明書に OID が存在する可能性の1つは、VPN またはワイヤレスネットワークへのアクセスを特定のデバイスに制限することです。 たとえば、アクセスポリシーによって、OID 1.3.6.1.4.1.311.21.30 が証明書に存在する場合、接続 (または別の VLAN へのアクセス) が許可される場合があります。 これにより、TPM EK が EKPUB リストに存在するデバイスへのアクセスを制限することができます。  
  
### <a name="BKMK_CAConfig"></a>CA の構成  
  
1.  **発行元 CA での EKCA と EKROOT の証明書ストアのセットアップ**  
  
    テンプレート設定に **[保証証明書]** を選択した場合は、次の構成手順を実行します。  
  
    1.  Windows PowerShell を使用して、TPM キーの構成証明を実行する証明機関 (CA) サーバーに2つの新しい証明書ストアを作成します。  
  
    2.  エンタープライズ環境で許可する製造元から、中間 CA 証明書とルート CA 証明書を取得します。 これらの証明書は、必要に応じて、以前に作成した証明書ストア (EKCA および EKROOT) にインポートする必要があります。  
  
    次の Windows PowerShell スクリプトでは、これらの手順の両方を実行します。 次の例では、TPM 製造元 Fabrikam は、ルート証明書*FabrikamRoot*と発行元 CA 証明書*contoso-fabrikamca*を提供しています。  
  
    ```powershell  
    PS C:>\cd cert:  
    PS Cert:\>cd .\\LocalMachine  
    PS Cert:\LocalMachine> new-item EKROOT  
    PS Cert:\ LocalMachine> new-item EKCA  
    PS Cert:\EKCA\copy FabrikamCa.cer .\EKCA  
    PS Cert:\EKROOT\copy FabrikamRoot.cer .\EKROOT  
    ```  
  
2.  **EK 構成証明の種類を使用している場合の EKPUB リストの設定**  
  
    テンプレート設定で **[保証キー]** を選択した場合、次の構成手順では、発行元 CA にフォルダーを作成して構成します。これには、許可された EK の sha-1 ハッシュ用に名前が付けられた0バイトのファイルが含まれます。 このフォルダーは、TPM キー証明証明書の取得が許可されているデバイスの "許可リスト" として機能します。 証明証明書を必要とするすべてのデバイスの EKPUB を手動で追加する必要があるため、TPM キー証明証明書の取得が許可されているデバイスが企業に保証されます。 このモードの CA を構成するには、次の2つの手順が必要です。  
  
    1.  **EndorsementKeyListDirectories レジストリエントリを作成します。** Certutil コマンドラインツールを使用して、次の表に示すように、trusted EKpubs が定義されているフォルダーの場所を構成します。  
  
        |操作|コマンド構文|  
        |-------------|------------------|  
        |フォルダーの場所の追加|certutil-setreg CA\EndorsementKeyListDirectories + "<folder>"|  
        |フォルダーの場所の削除|certutil-setreg CA\EndorsementKeyListDirectories-"<folder>"|  
  
        Certutil コマンドの EndorsementKeyListDirectories は、次の表に示すレジストリ設定です。  
  
        |値の名前|種類|data|  
        |--------------|--------|--------|  
        |EndorsementKeyListDirectories|REG_MULTI_SZ|EKPUB 許可リストへのローカルパスまたは UNC パスを < ><br /><br />例:<br /><br />*\\ \ blueCA com\ekpub*<br /><br />*\\ \ bluecluster1 com\ekpub*<br /><br />D:\ekpub|  
  
        HKLM\SYSTEM\CurrentControlSet\Services\CertSvc\Configuration @ no__t-0 @ no__t-1  
  
        *EndorsementKeyListDirectories*には UNC またはローカルファイルシステムのパスの一覧が含まれます。各パスは、CA が読み取りアクセス権を持つフォルダーを指します。 各フォルダーには、0個以上の許可リストエントリを含めることができます。各エントリは、信頼された EKpub の SHA-1 ハッシュである名前を持つファイルで、ファイル拡張子はありません。 
        このレジストリキー構成を作成または編集するには、既存の CA レジストリ構成設定と同じように、CA を再起動する必要があります。 ただし、構成設定の編集はすぐに有効になり、CA を再起動する必要はありません。  
  
        > [!IMPORTANT]  
        > 権限のある管理者のみが読み取りおよび書き込みアクセス権を持つようにアクセス許可を構成することにより、一覧内のフォルダーを改ざんや未承認のアクセスから保護します。 CA のコンピューターアカウントには、読み取りアクセスのみが必要です。  
  
    2.  **EKPUB の一覧を入力します。** 次の Windows PowerShell コマンドレットを使用して、各デバイスで Windows PowerShell を使用して TPM EK の公開キーハッシュを取得し、この公開キーハッシュを CA に送信して、EKPubList フォルダーに保存します。  
  
        ```powershell  
        PS C:>\$a=Get-TpmEndorsementKeyInfo -hashalgorithm sha256  
        PS C:>$b=new-item $a.PublicKeyHash -ItemType file  
        ```  
  
## <a name="troubleshooting"></a>トラブルシューティング  
  
### <a name="key-attestation-fields-are-unavailable-on-a-certificate-template"></a>キーの構成証明フィールドは、証明書テンプレートで使用できません  
テンプレート設定が構成証明の要件を満たしていない場合、[キーの構成証明] フィールドは使用できません。 一般的な理由は次のとおりです。  
  
1.  互換性設定が正しく構成されていません。 次のように構成されていることを確認します。  
  
    1.  **[証明機関]** :**Windows Server 2012 R2**  
  
    2.  **証明書の受信者**:**Windows 8.1/Windows Server 2012 R2**  
  
2.  暗号化の設定が正しく構成されていません。 次のように構成されていることを確認します。  
  
    1.  **プロバイダーのカテゴリ**:**キー記憶域プロバイダー**  
  
    2.  **アルゴリズム名**:**おける**  
  
    3.  **プロバイダー**:**Microsoft プラットフォーム暗号化プロバイダー**  
  
3.  要求処理の設定が正しく構成されていません。 次のように構成されていることを確認します。  
  
    1.  [**秘密キーのエクスポートを許可**する] オプションは選択しないでください。  
  
    2.  [**サブジェクトの暗号化秘密キーをアーカイブ**する] オプションは選択しないでください。  
  
### <a name="verification-of-tpm-device-for-attestation"></a>構成証明用の TPM デバイスの検証  
Windows PowerShell コマンドレット**CAEndorsementKeyInfo**を使用して、特定の TPM デバイスが ca によって構成証明に対して信頼されていることを確認します。 2つのオプションがあります。1つは EKCert の検証用、もう1つは EKPub を確認するためのオプションです。 コマンドレットは、CA でローカルに実行するか、Windows PowerShell リモート処理を使用してリモート Ca で実行します。  
  
1.  EKPub で信頼を確認するには、次の2つの手順を実行します。  
  
    1.  **クライアントコンピューターから EKPub を抽出します。** EKPub は、 **TpmEndorsementKeyInfo**を使用してクライアントコンピューターから抽出できます。 管理者特権でのコマンドプロンプトで、次のコマンドを実行します。  
  
        ```  
        PS C:>\$a=Get-TpmEndorsementKeyInfo -hashalgorithm sha256  
        ```  
  
    2.  **CA コンピューター上の EKCert の信頼を確認します。** 抽出された文字列 (EKPub の SHA-1 ハッシュ) をサーバーにコピーし (たとえば、電子メール経由で)、CAEndorsementKeyInfo コマンドレットに渡します。 このパラメーターは64文字にする必要があることに注意してください。  
  
        ```  
        Confirm-CAEndorsementKeyInfo [-PublicKeyHash] <string>  
        ```  
  
2.  EKCert で信頼を確認するには、次の2つの手順を実行します。  
  
    1.  **クライアントコンピューターから EKCert を抽出します。** EKCert は、 **TpmEndorsementKeyInfo**を使用してクライアントコンピューターから抽出できます。 管理者特権でのコマンドプロンプトで、次のコマンドを実行します。  
  
        ```  
        PS C:>\$a=Get-TpmEndorsementKeyInfo
        PS C:>\$a.manufacturerCertificates|Export-Certificate -filepath c:\myEkcert.cer
        ```  
  
    2.  **CA コンピューター上の EKCert の信頼を確認します。** 抽出された EKCert (EkCert) を CA にコピーします (たとえば、電子メールや xcopy を使用します)。 たとえば、証明書ファイルを CA サーバーの "c:\ 診断" フォルダーにコピーする場合は、次のように実行して検証を完了します。  
  
        ```  
        PS C:>new-object System.Security.Cryptography.X509Certificates.X509Certificate2 "c:\diagnose\myEKcert.cer" | Confirm-CAEndorsementKeyInfo  
        ```  
  
## <a name="see-also"></a>関連項目  
[トラステッドプラットフォームモジュールテクノロジの概要](https://technet.microsoft.com/library/jj131725.aspx)  
@no__t 0External リソース:トラステッドプラットフォームモジュール @ no__t-0  
