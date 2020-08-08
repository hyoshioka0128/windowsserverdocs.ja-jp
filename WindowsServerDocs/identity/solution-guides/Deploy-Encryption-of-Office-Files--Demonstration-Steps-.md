---
ms.assetid: 2c76e81a-c2eb-439f-a89f-7d3d70790244
title: Deploy Encryption of Office Files (Demonstration Steps)
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 1eba541baf7b00556efa686fc7b1572255498475
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87952863"
---
# <a name="deploy-encryption-of-office-files-demonstration-steps"></a>Deploy Encryption of Office Files (Demonstration Steps)

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

Contoso の金融部門には、ドキュメントを格納する多数のファイルサーバーがあります。 これらのドキュメントは、一般的なドキュメントである場合も、ビジネスに大きな影響を与えるもの (HBI) である場合もあります。 たとえば、機密情報が含まれているドキュメントは、ビジネスに大きな影響を与えるものと Contoso によって見なされます。 Contoso では、すべてのドキュメントに最小限の保護を施し、HBI ドキュメントが適切なユーザーに制限されるようにしたいと考えています。 これを実現するために、Contoso では、ファイル分類インフラストラクチャ (FCI) と Windows Server 2012 で利用可能な AD RMS を使用して調査しています。 Contoso では、FCI を使用することで、コンテンツに基づいてファイル サーバー上のすべてのドキュメントを分類してから、AD RMS を使用して適切な権利ポリシーを適用する予定です。

このシナリオでは、次の手順を実行します。

|タスク|説明|
|--------|---------------|
|[リソース プロパティを有効にする](Deploy-Encryption-of-Office-Files--Demonstration-Steps-.md#BKMK_1.1)|[**影響**] および [**個人を特定できる情報**] リソース プロパティを有効にします。|
|[分類規則を作成する](Deploy-Encryption-of-Office-Files--Demonstration-Steps-.md#BKMK_2)|次の分類規則を作成します。[ **HBI 分類規則** ] および [ **PII 分類規則**]。|
|[ファイル管理タスクを使用して、AD RMS でドキュメントを自動的に保護する](Deploy-Encryption-of-Office-Files--Demonstration-Steps-.md#BKMK_3)|自動的に AD RMS を使用して個人を特定できる情報 (PII) が含まれたドキュメントを保護するファイル管理タスクを作成します。 PII が含まれたドキュメントにアクセスできるのは、FinanceAdmin グループのメンバーのみにします。|
|[結果を表示する](Deploy-Encryption-of-Office-Files--Demonstration-Steps-.md#BKMK_4)|ドキュメントの分類を調べ、ドキュメントのコンテンツの変更に伴いどのように変更されるのかを監視します。 また、ドキュメントが AD RMS によってどのように保護されているのかを確認します。|
|[AD RMS による保護を確認する](Deploy-Encryption-of-Office-Files--Demonstration-Steps-.md#BKMK_5)|ドキュメントが AD RMS によって保護されていることを確認します。|
|||

## <a name="step-1-enable-resource-properties"></a><a name="BKMK_1.1"></a>手順 1:リソース プロパティを有効にする

#### <a name="to-enable-resource-properties"></a>リソース プロパティを有効にするには

1. Hyper-V マネージャーでサーバー ID_AD_DC1 に接続します。 Contoso\Administrator をパスワードと共に使用して、サーバーにサインインし <strong>pass@word1</strong> ます。

2. Active Directory 管理センターを開き、[**ツリー ビュー**] をクリックします。

3. [**ダイナミック アクセス制御**] を展開し、[**リソース プロパティ**] を選択します。

4. [**表示名**] 列の [**Impact**] プロパティまで下にスクロールします。 [**Impact**] を右クリックし、[**有効にする**] をクリックします。

5. [**表示名**] 列の [**Personally Identifiable Information**] プロパティまで下にスクロールします。 [**Personally Identifiable Information**] を右クリックし、[**有効にする**] をクリックします。

6. [**グローバル リソース リスト**] でリソース プロパティをパブリッシュするには、左側のウィンドウで [**リソース プロパティ リスト**] をクリックしてから、[**グローバル リソース プロパティ リスト**] をダブルクリックします。

7. [**追加**] をクリックしてから、下にスクロールし、[**Impact**] をクリックしてリストに追加します。 [**Personally Identifiable Information**] についても同様にします。 [**OK**] を 2 回クリックして完了します。

![ソリューションガイド](media/Deploy-Encryption-of-Office-Files--Demonstration-Steps-/PowerShellLogoSmall.gif)***<em>Windows PowerShell の同等のコマンド</em>***

次の Windows PowerShell コマンドレットは、前の手順と同じ機能を実行します。 各コマンドレットを単一行に入力します。ただし、ここでは、書式上の制約があるために、複数行に改行されて表示される場合があります。

```
Set-ADResourceProperty -Enabled:$true -Identity:"CN=Impact_MS,CN=Resource Properties,CN=Claims Configuration,CN=Services,CN=Configuration,DC=contoso,DC=com"
Set-ADResourceProperty -Enabled:$true -Identity:"CN=PII_MS,CN=Resource Properties,CN=Claims Configuration,CN=Services,CN=Configuration,DC=contoso,DC=com"
```

## <a name="step-2-create-classification-rules"></a><a name="BKMK_2"></a>手順 2:分類規則を作成する
この手順では、「**High Impact**」分類規則を作成する方法について説明します。 このルールでは、ドキュメントの内容を検索し、文字列 "Contoso Confidential" が見つかった場合は、このドキュメントをビジネスに大きな影響を与えるものとして分類します。 この分類は、以前に割り当てられた LBI (ビジネスへの影響が小さいもの) の分類をオーバーライドします。

「**High PII**」規則も作成します。 この規則では、ドキュメントのコンテンツを検索し、社会保障番号が見つかった場合に、ドキュメントを高 PII と分類します。

#### <a name="to-create-the-high-impact-classification-rule"></a>「High Impact」分類規則を作成するには

1. Hyper-V マネージャーでサーバー ID_AD_FILE1 に接続します。 Contoso\Administrator をパスワードと共に使用して、サーバーにサインインし <strong>pass@word1</strong> ます。

2. Active Directory からグローバル リソース プロパティーを更新する必要があります。 Windows PowerShell を開きます。「 `Update-FSRMClassificationPropertyDefinition`」と入力し、Enter キーを押します。 Windows PowerShell を閉じます。

3. ファイル サーバー リソース マネージャーを開きます。 ファイル サーバー リソース マネージャーを開くには、[**スタート**] をクリックし、「**ファイル サーバー リソース マネージャー**」と入力してから、[**ファイル サーバー リソース マネージャー**] をクリックします。

4. ファイル サーバー リソース マネージャーの左側のウィンドウで、[**分類管理**] を展開してから、[**分類規則**] を選択します。

5. [**操作**] ウィンドウで [**分類スケジュールの構成**] をクリックします。 [**自動分類**] タブで [**固定スケジュールを有効にする**] を選択し、[**曜日**] を選択してから、[**新しいファイルの連続分類を許可する**] チェック ボックスを選択します。 **[OK]** をクリックします。

6. [**操作**] ウィンドウで [**分類規則の作成**] をクリックします。 **[分類規則の作成]** ダイアログ ボックスが開きます。

7. [**規則名**] ボックスに「**High Business Impact**」と入力します。

8. [**説明**] ボックスに「」と入力すると、 **"Contoso Confidential" という文字列の有無に基づいて、ドキュメントがビジネスに大きな影響を与えるかどうかが決まり**ます。

9. [**スコープ**] タブで [**フォルダー管理プロパティの設定**] をクリックし、[**フォルダーの使用法**] を選択し、[**追加**] をクリックし、[**参照**] をクリックし、パスとして D:\Finance Documents を参照し、[**OK**] をクリックし、[**グループ ファイル**] というプロパティ値を選択し、[**閉じる**] をクリックします。 管理プロパティを設定したら、[**規則のスコープ**] タブで [**グループ ファイル**] を選択します。

10. [**分類**] タブをクリックします。 [**プロパティをファイルに割り当てる方法を選択**してください] で、ドロップダウンリストから [**コンテンツ分類子**] を選択します。

11. [**ファイルに割り当てるプロパティを選択してください**] でドロップダウン リストから [**Impact**] を選択します。

12. [**値の指定**] でドロップダウン リストから [**High**] を選択します。

13. [**パラメーター**] の [**構成**] をクリックします。  [**分類パラメーター**] ダイアログ ボックスの [**式の種類**] リストから [**文字列**] を選択します。 [ **式** ] ボックスに次の文字列を入力します。「 **Contoso Confidential**」。次に、[ **OK**] をクリックします。

14. [**評価の種類**] タブをクリックします。 [**既存のプロパティ値を再評価**する] をクリックし、[既存の値を**上書き**する] をクリックして、[ **OK** ] をクリックして完了します。

![ソリューションガイド](media/Deploy-Encryption-of-Office-Files--Demonstration-Steps-/PowerShellLogoSmall.gif)***<em>Windows PowerShell の同等のコマンド</em>***

次の Windows PowerShell コマンドレットは、前の手順と同じ機能を実行します。 各コマンドレットを単一行に入力します。ただし、ここでは、書式上の制約があるために、複数行に改行されて表示される場合があります。

```
Update-FSRMClassificationPropertyDefinition
$date = Get-Date
$AutomaticClassificationScheduledTask = New-FsrmScheduledTask -Time $date -Weekly @(3, 2, 4, 5,1,6,0) -RunDuration 0;
Set-FsrmClassification -Continuous -schedule $AutomaticClassificationScheduledTask
New-FSRMClassificationRule -Name "High Business Impact" -Property "Impact_MS" -Description "Determines if the document has a high business impact based on the presence of the string 'Contoso Confidential'" -PropertyValue "3000" -Namespace @("D:\Finance Documents") -ClassificationMechanism "Content Classifier" -Parameters @("StringEx=Min=1;Expr=Contoso Confidential") -ReevaluateProperty Overwrite
```

#### <a name="to-create-the-high-pii-classification-rule"></a>「High PII」分類規則を作成するには

1. Hyper-V マネージャーでサーバー ID_AD_FILE1 に接続します。 Contoso\Administrator をパスワードと共に使用して、サーバーにサインインし <strong>pass@word1</strong> ます。

2. デスクトップから [**Regular Expressions**] という名前のフォルダーを開き、**RegEx-SSN** という名前のテキスト ドキュメントを開きます。 次の正規表現文字列を強調表示してコピーします: **^ (?!000) ([0-7] \d {2} | 7 ([0-7] \d | 7 [012])) ([-]?)(?!00)、(?!)0000) \d {4} $**。 この文字列は、この手順の後半で使用するため、クリップボードに保持しておいてください。

3. ファイル サーバー リソース マネージャーを開きます。 ファイル サーバー リソース マネージャーを開くには、[**スタート**] をクリックし、「**ファイル サーバー リソース マネージャー**」と入力してから、[**ファイル サーバー リソース マネージャー**] をクリックします。

4. ファイル サーバー リソース マネージャーの左側のウィンドウで、[**分類管理**] を展開してから、[**分類規則**] を選択します。

5. [**操作**] ウィンドウで [**分類スケジュールの構成**] をクリックします。 [**自動分類**] タブで [**固定スケジュールを有効にする**] を選択し、[**曜日**] を選択してから、[**新しいファイルの連続分類を許可する**] チェック ボックスを選択します。 [OK] をクリックします。

6. [**規則名**] ボックスに「**High PII**」と入力します。 [**説明**] ボックスに「**社会保障番号の有無に基づいて、ドキュメントが高 PII かどうかを判別します**」と入力します。

7. [**スコープ**] タブで [**グループ ファイル**] チェック ボックスを選択します。

8. [**分類**] タブをクリックします。 [**プロパティをファイルに割り当てる方法を選択**してください] で、ドロップダウンリストから [**コンテンツ分類子**] を選択します。

9. [**ファイルに割り当てるプロパティを選択してください**] でドロップダウン リストから [**Personally Identifiable Information**] を選択します。

10. [**値の指定**] でドロップダウン リストから [**High**] を選択します。

11. [**パラメーター**] の [**構成**] をクリックします。
    [**分類パラメーター**] ウィンドウの [**式の種類**] ボックスの一覧で、[**正規表現**] を選択します。 [**式**] ボックスに、クリップボードのテキストを貼り付けます。 **^ (?!000) ([0-7] \d {2} | 7 ([0-7] \d | 7 [012])) ([-]?)(?!00)、(?!)0000) \d {4} $**」と入力し、[ **OK]** をクリックします。

    > [!NOTE]
    > この式により、無効な社会保障番号が許可されます。 これにより、デモで架空の社会保障番号を使用できます。

12. [**評価の種類**] タブをクリックします。 [**既存のプロパティ値を再評価**する] を選択し、既存の値を**上書き**して、[ **OK** ] をクリックして完了します。

![ソリューションガイド](media/Deploy-Encryption-of-Office-Files--Demonstration-Steps-/PowerShellLogoSmall.gif)***<em>Windows PowerShell の同等のコマンド</em>***

次の Windows PowerShell コマンドレットは、前の手順と同じ機能を実行します。 各コマンドレットを単一行に入力します。ただし、ここでは、書式上の制約があるために、複数行に改行されて表示される場合があります。

```
New-FSRMClassificationRule -Name "High PII" -Description "Determines if the document has a high PII based on the presence of a Social Security Number." -Property "PII_MS" -PropertyValue "5000" -Namespace @("D:\Finance Documents") -ClassificationMechanism "Content Classifier" -Parameters @("RegularExpressionEx=Min=1;Expr=^(?!000)([0-7]\d{2}|7([0-7]\d|7[012]))([ -]?)(?!00)\d\d\3(?!0000)\d{4}$") -ReevaluateProperty Overwrite
```

これで、次の 2 つの分類規則が作成されました。

-   High Business Impact

-   High PII

## <a name="step-3-use-file-management-tasks-to-automatically-protect-documents-with-ad-rms"></a><a name="BKMK_3"></a>手順 3:ファイル管理タスクを使用して、AD RMS でドキュメントを自動的に保護する
コンテンツに基づいてドキュメントを自動的に分類するルールを作成したので、次の手順では、AD RMS を使用して、分類に基づいて特定のドキュメントを自動的に保護するファイル管理タスクを作成します。 この手順では、高 PII のすべてのドキュメントを自動的に保護するファイル管理タスクを作成します。 PII が含まれたドキュメントにアクセスできるのは、FinanceAdmin グループのメンバーのみにします。

#### <a name="to-protect-documents-with-ad-rms"></a>AD RMS を使用してドキュメントを保護するには

1. Hyper-V マネージャーでサーバー ID_AD_FILE1 に接続します。 Contoso\Administrator をパスワードと共に使用して、サーバーにサインインし <strong>pass@word1</strong> ます。

2. ファイル サーバー リソース マネージャーを開きます。 ファイル サーバー リソース マネージャーを開くには、[**スタート**] をクリックし、「**ファイル サーバー リソース マネージャー**」と入力してから、[**ファイル サーバー リソース マネージャー**] をクリックします。

3. 左側のウィンドウで [**ファイル管理タスク**] を選択します。 [**操作**] ウィンドウで [**ファイル管理タスクの作成**] を選択します。

4. [**タスク名:**] フィールドに「**High PII**」と入力します。 [**説明**] フィールドに「**高 PII ドキュメントの自動 RMS 保護**」と入力します。

5. [**スコープ**] タブで [**グループ ファイル**] チェック ボックスを選択します。

6. [**操作**] タブをクリックします。[**種類**] で [ **RMS 暗号化**] を選択します。 [**参照**] をクリックしてテンプレートを選択してから、[**Contoso Finance Admin のみ**] テンプレートを選択します。

7. **[条件]** タブをクリックし、**[追加]** をクリックします。 [**プロパティ**] で [**Personally Identifiable Information**] を選択します。 [**演算子**] で [**等しい**] を選択します。 [**値**] で [**High**] を選択します。 **[OK]** をクリックします。

8. [**スケジュール**] タブをクリックします。[**スケジュール**] セクションで、[**毎週**] をクリックし、[**日曜日**] を選択します。 1 週間に 1 回タスクを実行することで、サービス障害などの中断イベントのために処理されなかった可能性があるドキュメントを捕捉できます。

9. [**連続動作**] セクションで [**タスクを連続実行する: 新規ファイル**] を選択してから、[**OK**] をクリックします。 これで、「High PII」という名前のファイル管理タスクが作成されました。

![ソリューションガイド](media/Deploy-Encryption-of-Office-Files--Demonstration-Steps-/PowerShellLogoSmall.gif)***<em>Windows PowerShell の同等のコマンド</em>***

次の Windows PowerShell コマンドレットは、前の手順と同じ機能を実行します。 各コマンドレットを単一行に入力します。ただし、ここでは、書式上の制約があるために、複数行に改行されて表示される場合があります。

```
$fmjRmsEncryption = New-FSRMFmjAction -Type 'Rms' -RmsTemplate 'Contoso Finance Admin Only'
$fmjCondition1 = New-FSRMFmjCondition -Property 'PII_MS' -Condition 'Equal' -Value '5000'
$date = get-date
$schedule = New-FsrmScheduledTask -Time $date -Weekly @('Sunday')
$fmj1=New-FSRMFileManagementJob -Name "High PII" -Description "Automatic RMS protection for high PII documents" -Namespace @('D:\Finance Documents') -Action $fmjRmsEncryption -Schedule $schedule -Continuous -Condition @($fmjCondition1)
```

## <a name="step-4-view-the-results"></a><a name="BKMK_4"></a>手順 4:結果を表示する
次に、新しい自動分類と AD RMS 保護規則の動作について説明します。 この手順では、ドキュメントの分類を調べ、ドキュメントのコンテンツの変更に伴いどのように変更されるのかを監視します。

#### <a name="to-view-the-results"></a>結果を表示するには

1. Hyper-V マネージャーでサーバー ID_AD_FILE1 に接続します。 Contoso\Administrator をパスワードと共に使用して、サーバーにサインインし <strong>pass@word1</strong> ます。

2. エクスプローラーで D:\Finance Documents にナビゲートします。

3. Finance Memo ドキュメントを右クリックし、[**プロパティ**] をクリックします。[**分類**] タブをクリックし、現在、Impact プロパティに値がないことを確認します。 **[キャンセル]** をクリックします。

4. [**Request for Approval to Hire document**] を右クリックしてから、[**プロパティ**] を選択します。

5. [**分類**] タブをクリックし、現在、[**Personally Identifiable Information**] プロパティに値がないことを確認します。 **[キャンセル]** をクリックします。

6. CLIENT1 に切り替えます。 サインインしているユーザーをサインオフし、パスワードを使用して Contoso\MReid としてサインインし <strong>pass@word1</strong> ます。

7. デスクトップから [**Finance Documents**] 共有フォルダーを開きます。

8. [**Finance Memo**] ドキュメントを開きます。 ドキュメントの下の方に「**Confidential**」という語があります。 これを次のように変更します。 **Contoso Confidential** ドキュメントを保存して閉じます。

9. [**Request for Approval to Hire**] ドキュメントを開きます。 [ **Social Security#:** ] セクションに次の文字列を入力します。777-77-7777。 ドキュメントを保存して閉じます。

    > [!NOTE]
    > 分類が行われるまで 30 秒間待機する必要が生じることがあります。

10. ID_AD_FILE1 に切り替えて戻ります。 エクスプローラーで D:\Finance Documents にナビゲートします。

11. Finance Memo ドキュメントを右クリックし、[**プロパティ**] をクリックします。 [**分類**] タブをクリックします。 **Impact**プロパティが**High**に設定されていることに注意してください。 **[キャンセル]** をクリックします。

12. Request for Approval to Hire ドキュメントを右クリックし、[**プロパティ**] をクリックします。

13. . [**分類**] タブをクリックします。 "**個人を特定できる情報**" プロパティが [**高**] に設定されていることを確認してください。 **[キャンセル]** をクリックします。

## <a name="step-5-verify-protection-with-ad-rms"></a><a name="BKMK_5"></a>手順 5:AD RMS による保護を確認する

#### <a name="to-verify-that-the-document-is-protected"></a>ドキュメントが保護されていることを確認するには

1.  ID_AD_CLIENT1 に切り替えて戻ります。

2.  [**Request for approval to Hire**] ドキュメントを開きます。

3.  [ **OK** ] をクリックして、ドキュメントが AD RMS サーバーに接続できるようにします。

4.  これで、社会保障番号が含まれているため、ドキュメントが AD RMS によって保護されていることが確認できます。


