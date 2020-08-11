---
title: Windows Server 2008 および 2008 R2 の拡張セキュリティ更新プログラム
description: サポート ライフサイクルが終了した後、Windows Server 2008 および 2008 R2 の拡張セキュリティ更新プログラム (ESU) を使用する方法について説明します。
ms.mktglfcycl: manage
author: iainfoulds
ms.author: iainfou
ms.topic: get-started-article
ms.localizationpriority: high
ms.date: 02/21/2020
ms.openlocfilehash: c74c8a278612d2ca47346ad95105f1258761494a
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87990474"
---
# <a name="how-to-use-windows-server-2008-and-2008-r2-extended-security-updates-esu"></a>Windows Server 2008 および 2008 R2 の拡張セキュリティ更新プログラム (ESU) を使用する方法

>適用先:Windows Server 2008 および Windows Server 2008 R2

Windows Server 2008 および Windows Server 2008 R2 は、2020 年 1 月 14 日にサポート ライフサイクルが終了しました。 Windows Server の長期サービス チャネル (LTSC) には、最低 10 年間のサポートが含まれています。メインストリーム サポートの 5 年間、拡張サポートの 5 年間です。 このサポートには、定期的なセキュリティ更新プログラムが含まれます。

サポートの終了は、セキュリティ更新プログラムの終了も意味します。 このシナリオでは、セキュリティやコンプライアンスに関する問題が発生し、ビジネスアプリケーションが危険にさらされる可能性があります。 最新のセキュリティ、パフォーマンス、およびイノベーションを実現するには、[最新バージョンの Windows Server にアップグレードする](modernize-windows-server-2008.md)ことをお勧めします。

サーバーをまだアップグレードしていない場合は、次のオプションを使用すると、移行中にアプリとデータを保護することができます。

* 既存の Windows Server 2008 と 2008 R2 のワークロードをそのまま Azure Virtual Machines (VM) に移行する。
  * この Azure への移行により、拡張セキュリティ更新プログラム (ESU) が自動的に 3 年分追加されます。 Azure VM のコスト以外に拡張セキュリティ更新プログラムの追加料金は発生しません。追加の構成も必要ありません。
* 新しい Windows Server のバージョンにアップグレードする準備が整うまで、サーバーの拡張セキュリティ更新プログラムのサブスクリプションを購入し、保護された状態を維持する。
  * この更新プログラムは、サポート ライフサイクルの終了日から最大 3 年間提供されます。

延長された更新プログラムの 3 年間が終了した後、Windows Server 2008 および 2008 R2 の更新は停止されます。 できるだけ早くご使用のバージョンの Windows Server を新しいバージョンに更新することをお勧めします。

## <a name="what-are-extended-security-updates-for-windows-server"></a>Windows Server の拡張セキュリティ更新プログラムとは

Windows Server の拡張セキュリティ更新プログラム (ESU) には、2020 年 1 月 14 日から最大 3 年間のセキュリティ更新プログラムと、*クリティカル*または*重要*と判断された情報が含まれます。 拡張セキュリティ更新プログラムに、次のものは含まれません。

* 新機能
* お客様から要求されたセキュリティ以外に関する修正プログラム
* 設計変更要求

詳細については、「[拡張セキュリティ更新プログラムのよくある質問 (FAQ)](https://www.microsoft.com/cloud-platform/extended-security-updates)」を参照してください。

## <a name="how-to-use-extended-security-updates"></a>拡張セキュリティ更新プログラムの使用方法

Windows Server 2008 または 2008 R2 の VM を Azure で実行すると、拡張セキュリティ更新プログラムがそれらの VM に対して自動的に有効になります。 Azure VM で拡張セキュリティ更新プログラムを使用するために何かを構成する必要はなく、追加料金も発生しません。 Azure VM が更新プログラムを受け取るように構成されている場合、拡張セキュリティ更新プログラムはそれらの VM に自動的に配信されます。

オンプレミスの VM や物理サーバーなど、その他の環境では、拡張セキュリティ更新プログラムを手動で要求して構成する必要があります。 拡張セキュリティ更新プログラムは、Enterprise Agreement (EA)、Enterprise Agreement Subscription (EAS)、Enrollment for Education Solutions (EES)、Server and Cloud Enrollment (SCE) などのボリューム ライセンス プログラムを通じて入手できます。

拡張セキュリティ更新プログラムを購入すると、次のいずれかの方法を使用してキーを取得できます。

* Azure portal から拡張セキュリティ更新プログラムのキーを取得する場合は、[Azure portal で拡張セキュリティ更新プログラムに登録する](#register-for-extended-security-updates-on-azure-portal)ことができます。
* [Microsoft ボリューム ライセンス サービス センターにサインイン](#sign-in-to-the-microsoft-volume-licensing-service-center)して、Azure portal を使用せずにキーを取得することもできます。

### <a name="register-for-extended-security-updates-on-azure-portal"></a>Azure portal で拡張セキュリティ更新プログラムに登録する

Azure 以外の VM で拡張セキュリティ更新プログラムを使用するには、マルチ ライセンス認証キー (MAK) を作成して、Windows Server 2008 および 2008 R2 のコンピューターに適用します。 MAK キーを使用すると、Windows Update サーバーが、引き続きセキュリティ更新プログラムを受信できることを認識します。 オンプレミスのコンピューターのみを使用する場合でも、拡張セキュリティ更新プログラムに登録して、Azure portal でこれらのキーを管理することができます。

> [!NOTE]
> Windows Server 2008 と 2008 R2 を Azure VM で実行している場合は、拡張セキュリティ更新プログラムに登録する必要はありません。 オンプレミスの VM や物理サーバーなど、その他の環境では、[拡張セキュリティ更新プログラムを購入](https://www.microsoft.com/licensing/how-to-buy/how-to-buy)してから、それらを登録して使用する必要があります。

拡張セキュリティ更新プログラムに VM を登録してキーを作成するには、Azure portal を開き、次の手順に従います。

1. [Azure portal](https://portal.azure.com/) にサインインします。
2. Azure portal の上部にある検索ボックスで、**拡張セキュリティ更新プログラム**を検索して選択します。

    ![Azure portal で拡張セキュリティ更新プログラムを検索する](media/extended-security-updates/esu-portal-search.png)

    以前に拡張セキュリティ更新プログラムを使用したことがない場合は、まず **[+ 作成]** を選択して拡張セキュリティ更新プログラムのリソースを作成します。 それ以外の場合は、一覧からリソースを選択します。

3. **[Register for Extended Service Updates]\(拡張サービス更新プログラムに登録する\)** で、 **[Get started]\(開始\)** を選択します。

    ![Azure portal で拡張セキュリティ更新プログラムの使用を開始する](media/extended-security-updates/get-started-with-esu.png)

4. 最初のキーを作成するには、 **[キーの取得]** を選択します。

    ![Azure portal でキーの作成を選択する](media/extended-security-updates/get-key.png)

    拡張セキュリティ更新プログラムのリソースとキーを作成するには、アカウントに関連付けられている Azure サブスクリプションが必要です。 アカウントに Azure サブスクリプションが関連付けられていない場合は、別のユーザー アカウントでサインインするか、Azure portal で Azure サブスクリプションを作成します。

    セキュリティ更新プログラムが動作するには、Azure サブスクリプションに投稿者ロールが割り当てられている必要もあります。 ロールを確認するには、検索ボックスに「サブスクリプション」と入力します。 サブスクリプション ID と名前の横に、お使いのロールを示すテーブルが表示されます。

    投稿者でない場合は、サブスクリプションの所有者にロールを変更するように依頼できます。 サブスクリプションを所有しているユーザーを確認するには、前の段落で説明されているロールのテーブルにアクセスし、サブスクリプションの名前を選択します。 次に、ページの左側にあるメニューに移動し、**アクセス制御 (IAM)**  > **ロールの割り当て** を選択して、テーブルの "所有者" セクションを探します。

5. "登録してマルチ ライセンス認証キーを取得する" と示されたページが表示される場合は、拡張セキュリティ更新プログラムを使用する前に、プライベート プレビューへのアクセスを要求する必要があります。 このページが表示されない場合は、手順 6 に進んでください。

   アクセスを要求するには、 **[join the private preview]\(プライベート プレビューに参加\)** を選択します。 メール メッセージ ウィンドウが開きます。 このメールは、製品チームへのアクセス要求です。

    要求に次の情報を含めます。

    * 顧客名
    * Azure サブスクリプション ID
    * 契約番号 (ESU の場合)
    * ESU サーバーの数

    完了したら、メールを送信します。

    チームは、要求メールに記載されている情報をレビューします。 問題がなければ、承認済みリストに追加されます。

    チームにより要求が承認されない場合は、次のエラーが表示されます。

    [名前空間 'Microsoft.WindowsESU' でリソースの種類が見つかりませんでした。]()

6. **[Azure の詳細]** で、Azure サブスクリプション、リソース グループ、およびキーの場所を選択します。

    **[登録の詳細]** で、次の情報を入力します。

    | 設定             | 値 |
    |---------------------|-------|
    | キー名            | キーの表示名 (*Agreement01* など)。 |
    | 契約番号    | ボリューム ライセンス契約管理システムまたはエンタープライズ契約プログラムの MSLicense によって生成された契約番号。 |
    | コンピューター数 | このキーを使用して拡張セキュリティ更新プログラムをインストールするコンピューターの数を選択します。 |
    | オペレーティング システム    | このキーを使用するオペレーティングシステム (Windows Server 2008、Windows Server 2008 R2 など) を選択します。 |

    準備ができたら、 **[Review + register]\(確認 + 登録\)** を選択します。

    >[!NOTE]
    >プライベート プレビューに参加している Azure サブスクリプションがグローバル フィルターで選択されていることを確認してください。 グローバル サブスクリプション フィルターを確認するには、Azure portal リボンの**フィルター**ボタンを選択します。
    >
    > ![フィルター ボタンが選択された状態の Azure portal リボンの画像](media/azure-ribbon-filter.png)

7. 検証が正常に完了すると、新しいレジストリ リソースの選択内容の概要が表示されます。 必要に応じて、検証エラーを修正するか、構成の選択を更新します。 Azure の[使用条件](https://azure.microsoft.com/support/legal/)と[プライバシー ポリシー](https://privacy.microsoft.com/privacystatement)を確認できます。

    チェックボックスをオンにして、対象となるコンピューターを所有しており、そのキーが組織内でのみ使用されることを確認します。

    ![キーが組織でのみ使用されることを確認する](media/extended-security-updates/confirm-key-usage.png)

    準備ができたら、 **[作成]** を選択して MAK を生成します。

コンピューターで拡張セキュリティ更新プログラムの登録を使用できるようになりました。 作成されたキーは、セキュリティ更新プログラムの対象として使用する Windows Server 2008 および 2008 R2 コンピューターに適用する必要があります。

### <a name="sign-in-to-the-microsoft-volume-licensing-service-center"></a>Microsoft ボリューム ライセンス サービス センターにサインインする

Azure portal へのアクセス権がない場合は、ボリューム ライセンス サービス センターを使用して、ライセンス認証キーを表示およびダウンロードできます。

ボリューム ライセンス サービス センターからキーを取得するには、次のようにします。

1. [ボリューム ライセンス サービス センターのページ](https://www.microsoft.com/vlsc)にアクセスして、Azure の資格情報でサインインします。

2. **[ライセンス]**  >  **[契約一覧]要** >  **[ライセンス ID]**  >  **[プロダクト キー]** を選択します。

対象となる Windows デバイスの拡張セキュリティ更新プログラムを取得する方法の詳細については、[Tech Community の投稿](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/obtaining-extended-security-updates-for-eligible-windows-devices/ba-p/1167091#)を参照してください。

## <a name="download-and-apply-extended-security-updates"></a>拡張セキュリティ更新プログラムをダウンロードして適用する

Windows Server 用の拡張セキュリティ更新プログラムの配布、ダウンロード、および適用は、既存の展開プロセスと同じです。 拡張セキュリティ更新プログラムによって提供される更新プログラムは、*セキュリティ*のみを対象としており、すべての更新プログラムが火曜日にリリースされます。

更新プログラムは、既にあるツールとプロセスを使用してインストールできます。 唯一の違いは、更新プログラムをダウンロードしてインストールするには、前のセクションで生成したキーを使用してシステムを登録する必要があることです。

Azure VM では、拡張セキュリティ更新プログラムのためにコンピューターを有効にするプロセスが自動的に完了します。 更新プログラムは、追加の構成なしでダウンロードしてインストールする必要があります。