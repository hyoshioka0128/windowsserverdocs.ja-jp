---
ms.assetid: 16a344a9-f9a6-4ae2-9bea-c79a0075fd04
title: "TPM キーの構成証明"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 9d08efe825e10d526763a1654c7e090427719c51
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="tpm-key-attestation"></a>TPM キーの構成証明

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

**作成者**: Windows グループに Justin チューナー シニア サポート エスカレーション エンジニア  
  
> [!NOTE]  
> このコンテンツが、Microsoft カスタマー サポート エンジニアによって書き込まれるあり、経験豊富な管理者と TechNet の通常のトピックよりも機能と Windows Server 2012 R2 で解決策の詳細な技術的説明を求めているシステム アーキテクトです。 ただし、実施されていません、同様の編集過程のため、TechNet の「新機能が見つかった通常より洗練されて、言語によってように見える場合があります。  
  
## <a name="overview"></a>概要  
サポート中に、Windows 8 から TPM で保護されたキーが存在しているがなかった Ca が暗号によって証明書要求者の秘密キーがトラステッド プラットフォーム モジュール (TPM) によって保護される実際にことを証明するためのメカニズム。 この更新プログラムは、その構成証明を実行して、発行された証明書では、その構成証明を反映するように CA を使用できます。  
  
> [!NOTE]  
> この記事では、読者が証明書テンプレートの概念を理解している前提としています (リファレンスについては、次を参照してください。[証明書テンプレート](https://technet.microsoft.com/library/cc730705.aspx))。 前提としています、リーダーは証明書テンプレートに基づいて証明書を発行するエンタープライズ Ca を構成する方法を理解している (リファレンスについては、次を参照してください。[チェックリスト: 構成の発行と管理の証明書の Ca](https://technet.microsoft.com/library/cc771533.aspx))。  
  
### <a name="terminology"></a>用語集  
  
|用語|定義|  
|--------|--------------|  
|EK|保証キー。 これは、TPM (製造時に挿入) 内に含まれる非対称キーです。 EK は、各 TPM に対して一意で確認できます。 EK を変更または削除することはできません。|  
|EKpub|EK の公開キーを指します。|  
|EKPriv|EK の秘密キーを指します。|  
|EKCert|EK の証明書。 TPM の製造元によって発行された証明書の EKPub します。 すべての Tpm では、EKCert があります。|  
|TPM|トラステッド プラットフォーム モジュールです。 TPM はハードウェア ベースのセキュリティに関連する機能を提供するよう設計されています。 TPM チップは、セキュリティで保護された暗号プロセッサ暗号化操作を実行するように設計されたです。 チップには改ざんされにくい、する複数の物理的なセキュリティ メカニズムが含まれています、悪意のあるソフトウェアは、TPM のセキュリティ機能を改ざんすることができます。|  
  
### <a name="background"></a>バック グラウンド  
Windows 8 以降では、トラステッド プラットフォーム モジュール (TPM) を使用して証明書の秘密キーをセキュリティで保護します。 Microsoft プラットフォーム暗号化プロバイダー キー格納プロバイダー (KSP) は、この機能を使用できます。 実装の 2 つの問題が発生しました。  

-   キーが実際には、(ユーザーが簡単にスプーフィングするソフトウェア KSP ローカル管理者の資格情報を使って TPM KSP として) TPM によって保護されているという保証はありませんでした。

-   Enterprise (イベントで PKI 管理者は、使用環境での証明書を取得できるデバイスの種類を制御したい) に発行された証明書を保護することができる Tpm のリストを制限できませんでした。  

### <a name="tpm-key-attestation"></a>TPM キーの構成証明  
TPM キーの構成証明は、暗号で証明書の要求、RSA キーが CA が信頼している「、」または「、」TPM によって保護されている CA を証明するために、証明書を要求しているエンティティの機能です。 TPM 信頼モデルの詳細については、[展開の概要](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_DeploymentOverview)このトピックで後述します。  
  
### <a name="why-is-tpm-key-attestation-important"></a>TPM キーの構成証明が重要な理由  
TPM 証明キーを使用して、ユーザー証明書は、非エクスポート、ハンマリング対策、および TPM によって提供されるキーの分離によってバックアップ、上位のセキュリティ保証を提供します。  
  
TPM キーの構成証明で新しい管理パラダイムが可能になりました。管理者は、ユーザーが (VPN やワイヤレス アクセス ポイントなど) の企業リソースにアクセスして使用できるデバイスのセットを定義できます**強力な**保証にアクセスするその他のデバイスが使用されません。 この新しいアクセス制御のパラダイム**強力な**に結び付けられているので、*ハードウェアにバインドされた*ソフトウェア ベースの資格情報をよりも強力であるユーザー id。
  
### <a name="how-does-tpm-key-attestation-work"></a>TPM キーの構成証明のしくみ  
一般に、TPM キーの構成証明は、次の柱に基づいています。  
  
1.  各 TPM には一意の非対称キーが付属と呼ばれる、*保証キー* (EK) は、製造元によって書き込みます。 としてこのキーの公開の部分を参照してください*EKPub*と関連付けられている秘密キーに*EKPriv*します。 いくつかの TPM チップがある、EKPub の製造元によって発行される EK 証明書もします。 としてこの証明書を参照してください*EKCert*します。  
  
2.  CA は、TPM EKPub または ekcert のどちらのいずれかの信頼を確立します。  
  
3.  ユーザーは、証明書の要求を RSA キーが、EKPub に関連する暗号化に使用して、ユーザーが、EKpriv を所有している CA に証明されます。  
  
4.  CA は、特別な発行ポリシーをキーが TPM で保護する証明できるようになりましたことを示す OID と証明書を発行します。  
  
## <a name="BKMK_DeploymentOverview"></a>展開の概要  
この展開で Windows Server 2012 R2 のエンタープライズ CA がセットアップされていると見なされます。 また、エンタープライズ CA を使用してそのに登録する (Windows 8.1) が構成されているクライアント証明書テンプレートの。 

TPM キーの構成証明を展開する手順は次の 3 つです。  
  
1.  **TPM 信頼モデルを計画する:**最初の手順でを使用する TPM 信頼モデルを決定します。 この操作のサポートされている 3 つの方法があります。  
  
    -   **信頼がユーザーの資格情報に基づく:**エンタープライズ CA が証明書の要求の一部としてユーザーが指定した EKPub を信頼し、検証は行われません以外、ユーザーのドメイン資格情報。  
  
    -   **EKCert に基づいて信頼:**エンタープライズ CA の一覧を管理者が管理に対して証明書の要求の一部として提供されている EKCert チェーンの検証*許容 EK の証明書チェーン*します。 許容チェーン製造元ごとに定義された、(中間の 1 つのストア) は、ルート CA 証明書のいずれかの発行元 CA で、次の 2 つのカスタム証明書ストア経由で表されます。 この信頼モードでは、ことを意味**すべて**特定の製造元の Tpm は信頼します。 いるこのモードでは、環境で使用されて Tpm 含める必要があります EKCerts に注意してください。
  
    -   **EKPub に基づいて信頼:**エンタープライズ CA は、管理者が管理の一覧に表示されます、証明書の要求の一部として提供 EKPub に EKPubs が許可されていることを検証します。 この一覧は、このディレクトリ内の各ファイルの名前が許可されている EKPub の SHA-2 ハッシュのファイルのディレクトリで表されます。 このオプションは、最高の保証レベルを提供、各デバイスが個別に識別されるため、複数の管理作業が必要です。 この信頼モデルでは、TPM の EKPub EKPubs の許可リストに追加されているデバイスのみが許可される TPM 証明の証明書を登録します。  
  
    どの方法を使用すると、によって CA は、発行された証明書に OID する、さまざまな発行ポリシーが適用されます。 発行ポリシーの Oid の詳細については、発行ポリシーの Oid の表を参照してください、[証明書テンプレートを構成する](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_ConfigCertTemplate)」セクションを参照します。  
  
    TPM 信頼モデルの組み合わせを選択することがあることに注意してください。 この場合、CA を受け入れるすべての構成証明の方法と、発行ポリシーの Oid が成功したすべての構成証明メソッドに反映されます。  
  
2.  **証明書テンプレートを構成する:**で説明されている証明書テンプレートを構成するは、[の展開の詳細](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_DeploymentDetails)」セクションを参照します。 この記事がエンタープライズ CA にこの証明書テンプレートを割り当てる方法をカバーか方法を登録していないユーザーのグループに付与されます。 詳細については、次を参照してください。[チェックリスト: 構成の発行と管理の証明書の Ca](https://technet.microsoft.com/library/cc771533.aspx)します。  
  
3.  **TPM 信頼モデルの CA を構成します。**  
  
    1.  **信頼がユーザーの資格情報に基づく:**特定の構成は必要ありません。  
  
    2.  **EKCert に基づいて信頼:**管理者が TPM の製造元から EKCert チェーンの証明書を取得し、TPM キーの構成証明を実行している CA で、管理者によって作成された、2 つの新しい証明書ストアにインポートする必要があります。 詳細については、次を参照してください。、[CA 構成](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_CAConfig)」セクションを参照します。  
  
    3.  **EKPub に基づいて信頼:**、管理者が許可されている EKPubs の一覧に追加し、TPM 証明の証明書が必要なは各デバイス用 EKPub を取得する必要があります。 詳細については、次を参照してください。、[CA 構成](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_CAConfig)」セクションを参照します。  
  
    > [!NOTE]  
    > -   この機能では、Windows 8.1/Windows Server 2012 R2 が必要です。  
    > -   サード パーティ製のスマート カード Ksp に TPM キーの構成証明はサポートされていません。 Microsoft プラットフォーム暗号化プロバイダーの KSP を使用する必要があります。  
    > -   TPM キーの構成証明は、RSA キーに対してのみ動作します。  
    > -   スタンドアロン CA では、TPM キーの構成証明はサポートされていません。  
    > -   TPM キーの構成証明はサポートしていません[非持続の証明書の処理](https://technet.microsoft.com/library/ff934598)します。  
  
## <a name="BKMK_DeploymentDetails"></a>展開の詳細  
  
### <a name="BKMK_ConfigCertTemplate"></a>証明書テンプレートを構成します。  
TPM キーの構成証明の証明書テンプレートを構成するのには、次の構成手順を実行します。  
  
1.  **互換性**] タブ  
  
    **互換設定**セクション。  
  
    -   確認**Windows Server 2012 R2**用に選択された、**証明機関**します。  
  
    -   確認**Windows 8.1/Windows Server 2012 R2**用に選択された、**証明書の受信者**します。  
  
    ![TPM キーの構成証明](media/TPM-Key-Attestation/GTR_ADDS_CompatibilityTab.gif)  
  
2.  **Cryptography** ] タブ  
  
    確認して**Key Storage Provider**用に選択された、**プロバイダーのカテゴリ**と**RSA**用に選択された、**アルゴリズム名**します。 確認して**要求は、次のプロバイダーのいずれかを使用する必要があります**が選択されていると、**Microsoft プラットフォーム暗号化プロバイダー**下にあるオプションを選択した**プロバイダー**します。  
  
    ![TPM キーの構成証明](media/TPM-Key-Attestation/GTR_ADDS_CryptoTab.gif)  
  
3.  **キーの構成証明**] タブ  
  
    これは、Windows Server 2012 R2 の新しいタブ] です。  
  
    ![TPM キーの構成証明](media/TPM-Key-Attestation/GTR_ADDS_ConfigCertTemplate.gif)  
  
    利用可能な 3 つのオプションから、構成証明モードを選択します。  
  
    ![TPM キーの構成証明](media/TPM-Key-Attestation/GTR_ADDS_KeyModes.gif)  
  
    -   **なし:**意味するキーの構成証明を使用しないでください  
  
    -   **必要に応じて、クライアントが対応の場合:** TPM をサポートしていないデバイス上のユーザーがキーの構成証明をその証明書の登録を続行します。 構成証明を実行できるユーザーは、特別な発行ポリシー OID で識別されます。 一部のデバイスは、古い TPM キー認証、または、TPM がまったくないデバイスをサポートしないため、構成証明を実行できない可能性があります。
  
    -   **必要です。**クライアント*必要があります*TPM キーの構成証明を実行、それ以外の場合、証明書の要求は失敗します。  
  
    TPM 信頼モデルを選択します。 もう一度は 3 つのオプションがあります。  
  
    ![TPM キーの構成証明](media/TPM-Key-Attestation/GTR_ADDS_KeyTypeToEnforce.gif)  
  
    -   **ユーザーの資格情報:**、ドメイン資格情報を指定して有効な TPM を保証するユーザーが認証できるようにします。  
  
    -   **保証証明書:**デバイスの [EKCert を管理者が管理 TPM 中間 CA 証明書によって、管理者が管理ルート CA 証明書を検証する必要があります。 このオプションを選択する場合は、場合と EKRoot を設定する必要があります証明書の発行元の CA 上のストア」の説明に従って、[CA 構成](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_CAConfig)」セクションを参照します。  
  
    -   **保証キー:**デバイスの EKPub が PKI 管理者が管理一覧に表示する必要があります。 このオプションでは、最高の保証レベルを提供するより多くの管理作業が必要です。 場合このオプションを選択する必要がありますを設定する、発行元 CA で、EKPub リスト」の説明に従って、[CA 構成](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_CAConfig)」セクションを参照します。  
  
    最後に、発行された証明書に表示するには、どの発行ポリシーを決定します。 既定では、各実施の種類は、その実施型を渡すように、次の表で説明されている場合、証明書に挿入される関連付けられているオブジェクト識別子 (OID) を持っています。 強制方法の組み合わせを選択することであるに注意してください。 この場合、構成証明の方法のいずれかの CA はそのまま使用され、発行ポリシー OID には、すべての構成証明メソッドが成功したことが反映されます。  
  
    **発行ポリシーの Oid**  
  
    |OID|キーの構成証明の種類|説明|保証レベル|  
    |-------|------------------------|---------------|-------------------|  
    |1.3.6.1.4.1.311.21.30|EK|「EK の検証済み」: EK の一覧を管理者が管理について|高|  
    |1.3.6.1.4.1.311.21.31|保証証明書|「EK の証明書の検証済み」: EK の証明書チェーンを検証するとき|[中]|  
    |1.3.6.1.4.1.311.21.32|ユーザーの資格情報|「使用で信頼された EK」: ユーザー証明 EK の|低|  
  
    場合、発行された証明書に挿入される、Oid**発行ポリシーを含める**は (既定の構成) を選択します。  
  
    ![TPM キーの構成証明](media/TPM-Key-Attestation/GTR_ADDS_IssuancePolicies.gif)  
  
    > [!TIP]  
    > 証明書の OID を持つことの 1 つの潜在的な使用の方法では、VPN へのアクセスを制限またはワイヤレス ネットワークの特定のデバイスにです。 たとえば、アクセス ポリシーが許可されて接続 (または別の VLAN へのアクセス) OID 1.3.6.1.4.1.311.21.30 が証明書に存在する場合。 これにより、TPM が EK が EKPUB リスト内に存在するデバイスへのアクセスを制限することができます。  
  
### <a name="BKMK_CAConfig"></a>CA の構成  
  
1.  **発行元の CA の場合と EKROOT の証明書ストアをセットアップします。**  
  
    選択した場合**保証証明書**設定については、テンプレートには、以下の構成手順を実行します。  
  
    1.  Windows PowerShell を使用して、TPM キーの構成証明を実行する証明機関 (CA) サーバー上の 2 つの新しい証明書ストアを作成します。  
  
    2.  中間を入手し、ルート CA の証明書、エンタープライズ環境で許可する場合の製造元からします。 必要に応じて以前作成した証明書ストア (場合および EKROOT) には、これらの証明書をインポートする必要があります。  
  
    次の Windows PowerShell スクリプトは、両方の手順を実行します。 次の例では、TPM の製造元 Fabrikam が、ルート証明書を提供*FabrikamRoot.cer*と発行元の CA 証明書*Fabrikamca.cer*します。  
  
    ```powershell  
    PS C:>\cd cert:  
    PS Cert:\>cd .\\LocalMachine  
    PS Cert:\LocalMachine> new-item EKROOT  
    PS Cert:\ LocalMachine> new-item EKCA  
    PS Cert:\EKCA\copy FabrikamCa.cer .\EKCA  
    PS Cert:\EKROOT\copy FabrikamRoot.cer .\EKROOT  
    ```  
  
2.  **EK の構成証明の種類を使用して場合 EKPUB リストをセットアップします。**  
  
    選択した場合**保証キー**テンプレート設定で、[次へ] の構成手順を作成および発行元の ca では、0 バイトのファイルを含むフォルダーを構成は、許可されている、EK の SHA-2 ハッシュの各という名前です。 このフォルダーは、「許可リスト」TPM キー証明の証明書の取得が許可されているデバイスのとして機能します。 構成証明された証明書を必要とする各デバイスの EKPUB を手動で追加する必要があります、ために、TPM キーの構成証明された証明書を取得する権限を持つデバイスの保証と、企業を提供します。 このモードの CA を構成するには、2 つの手順が必要です。  
  
    1.  **EndorsementKeyListDirectories レジストリ エントリを作成します。** Certutil コマンド ライン ツールを使用してように、次の表で説明されている信頼された EKpubs が定義されているフォルダーの場所を構成します。  
  
        |操作|コマンドの構文|  
        |-------------|------------------|  
        |フォルダーの場所を追加します。|Certutil.exe-setreg CA\EndorsementKeyListDirectories +"<folder>"|  
        |フォルダーの場所を削除します。|Certutil.exe-setreg CA\EndorsementKeyListDirectories-"<folder>"|  
  
        Certutil コマンドで EndorsementKeyListDirectories は、次の表で説明するようにレジストリ設定です。  
  
        |値の名前|種類|データ|  
        |--------------|--------|--------|  
        |EndorsementKeyListDirectories|REG_MULTI_SZ|< EKPUB へのローカルまたは UNC パスを許可する一覧 ><br /><br />例:<br /><br />*\\\blueCA.contoso.com\ekpub*<br /><br />*\\\bluecluster1.contoso.com\ekpub*<br /><br />D:\ekpub|  
  
        HKLM\SYSTEM\CurrentControlSet\Services\CertSvc\Configuration\\<CA Sanitized Name>  
  
        *EndorsementKeyListDirectories*を CA に対する読み取りアクセス権を持つフォルダーをポイントしている各 UNC またはローカル ファイル システムのパスの一覧が含まれます。 各フォルダーは 0 を含めることがまたは詳細許可一覧のエントリ、SHA-2 である名前のファイルを各エントリがここでは、信頼される側の EKpub のハッシュ ファイル拡張子は付けずにします。 
        作成またはこのレジストリ キーの構成を編集するには、既存の CA レジストリ構成の設定と同じように、CA の再起動が必要です。 ただし、構成設定の編集は直ちに反映され、CA を再起動するのには必要ありません。  
  
        > [!IMPORTANT]  
        > 改ざんから、一覧内のフォルダーをセキュリティで保護し、不正アクセスのみ管理者に承認できるようにアクセス許可の構成の読み取り/書き込みアクセス権。 CA のコンピューター アカウントには、読み取り専用アクセスが必要です。  
  
    2.  **EKPUB リスト:**、次の Windows PowerShell コマンドレットを使用して、各デバイスで Windows PowerShell を使用して、TPM EK の公開キー ハッシュを取得して、このパブリック ca のハッシュのキーし、EKPubList フォルダーに保存を送信します。  
  
        ```powershell  
        PS C:>\$a=Get-TpmEndorsementKeyInfo -hashalgorithm sha256  
        PS C:>$b=new-item $a.PublickKeyHash -ItemType file  
        ```  
  
## <a name="troubleshooting"></a>トラブルシューティング  
  
### <a name="key-attestation-fields-are-unavailable-on-a-certificate-template"></a>キーの構成証明のフィールドが証明書テンプレートで利用できません。  
キーの構成証明のフィールドは、テンプレートの設定が構成証明の要件を満たしていない場合は、ご利用いただけません。 一般的な理由は次のとおりです。  
  
1.  互換性の設定が正しく構成されていません。 次のように構成されていることを確認します。  
  
    1.  **証明機関**: **Windows Server 2012 R2**  
  
    2.  **証明書の受信者**: **Windows 8.1/Windows Server 2012 R2**  
  
2.  暗号化の設定が正しく構成されていません。 次のように構成されていることを確認します。  
  
    1.  **プロバイダーのカテゴリ**:**キー記憶域プロバイダー**  
  
    2.  **アルゴリズム名**: **RSA**  
  
    3.  **プロバイダー**: **Microsoft プラットフォーム暗号化プロバイダー**  
  
3.  要求の処理の設定が正しく構成されていません。 次のように構成されていることを確認します。  
  
    1.  **プライベート キーのエクスポートを許可する**オプションが選択されていない必要があります。  
  
    2.  **サブジェクトの秘密キーをアーカイブ**オプションが選択されていない必要があります。  
  
### <a name="verification-of-tpm-device-for-attestation"></a>構成証明の TPM のデバイスの検証  
Windows PowerShell コマンドレットを使用して**Confirm CAEndorsementKeyInfo**、TPM の特定のデバイスが Ca によって信頼された構成証明のことを確認します。 2 つのオプションがある: EKCert と、EKPub を確認するため、その他を確認するための 1 つです。 コマンドレットか、ローカルで実行、CA 上またはリモートの Ca で Windows PowerShell リモート処理を使用しています。  
  
1.  EKPub での信頼を検証するには、次の 2 つの手順を実行します。  
  
    1.  **クライアント コンピューターから、EKPub を抽出:**、EKPub を使用してクライアント コンピューターから抽出する**Get TpmEndorsementKeyInfo**します。 管理者特権のコマンド プロンプトから次の手順を実行します。  
  
        ```  
        PS C:>\$a=Get-TpmEndorsementKeyInfo -hashalgorithm sha256  
        ```  
  
    2.  **CA コンピューターで、EKCert の信頼の確認:**抽出された文字列 (、EKPub の SHA-2 ハッシュ) (たとえば、電子メール) 経由でサーバーにコピーし、Confirm CAEndorsementKeyInfo コマンドレットに渡すことです。 このパラメーターは 64 文字である必要がありますに注意してください。  
  
        ```  
        Confirm-CAEndorsementKeyInfo [-PublicKeyHash] <string>  
        ```  
  
2.  EKCert での信頼を検証するには、次の 2 つの手順を実行します。  
  
    1.  **クライアント コンピューターから、EKCert を抽出:**、EKCert を使用してクライアント コンピューターから抽出する**Get TpmEndorsementKeyInfo**します。 管理者特権のコマンド プロンプトから次の手順を実行します。  
  
        ```  
        PS C:>\$a= Get- TpmEndorsementKeyInfo  
        PS C:>\$a.manufacturerCertificates|Export-Certificate c:\myEkcert.cer  
        ```  
  
    2.  **CA コンピューターで、KCert 上の信頼の確認:** CA (たとえば、電子メールまたは xcopy) を介してを抽出した EKCert (EkCert.cer) にコピーします。 CA サーバーに証明書ファイル"c:\diagnose"フォルダーをコピーする場合は、例として、検証を完了するのには、次を実行します。  
  
        ```  
        PS C:>new-object System.Security.Cryptography.X509Certificates.X509Certificate2 "c:\diagnose\myEKcert.cer" | Confirm-CAEndorsementKeyInfo  
        ```  
  
## <a name="see-also"></a>参照してください。  
[トラステッド プラットフォーム モジュール技術概要](https://technet.microsoft.com/library/jj131725.aspx)  
[トラステッド プラットフォーム モジュールの外部リソース:](http://www.cs.unh.edu/~it666/reading_list/Hardware/tpm_fundamentals.pdf)  
  


