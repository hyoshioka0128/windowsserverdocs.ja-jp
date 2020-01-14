---
title: Windows Server 2008 および 2008 R2 の拡張セキュリティ更新プログラム
description: サポート ライフサイクルが終了した後、Windows Server 2008 および 2008 R2 の拡張セキュリティ更新プログラム (ESU) を使用する方法について説明します。
ms.prod: windows-server
ms.technology: server-general
ms.mktglfcycl: manage
author: iainfoulds
ms.author: iainfou
ms.topic: get-started-article
ms.localizationpriority: high
ms.date: 12/16/2019
ms.openlocfilehash: a5af1ad5a730f1dc90111734a9b8b1aacc91201b
ms.sourcegitcommit: bfe9c5f7141f4f2343a4edf432856f07db1410aa
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2019
ms.locfileid: "75466345"
---
# <a name="how-to-use-windows-server-2008-and-2008-r2-extended-security-updates-esu"></a>Windows Server 2008 および 2008 R2 の拡張セキュリティ更新プログラム (ESU) を使用する方法

>適用先:Windows Server 2008 / 2008 R2

Windows Server 2008 および Windows Server 2008 R2 は、2020 年 1 月 14 日にサポート ライフサイクルが終了します。 Windows Server の長期サービス チャネル (LTSC) には、最低 10 年間のサポートが含まれています。メインストリーム サポートの 5 年間、拡張サポートの 5 年間です。 このサポートには、定期的なセキュリティ更新プログラムが含まれます。

サポートの終了は、セキュリティ更新プログラムの終了も意味します。 このシナリオでは、セキュリティやコンプライアンスに関する問題が発生し、ビジネスアプリケーションが危険にさらされる可能性があります。 最新のセキュリティ、パフォーマンス、およびイノベーションを実現するには、[最新バージョンの Windows Server にアップグレードする](modernize-windows-server-2008.md)ことをお勧めします。

サポート ライフサイクル期限の終わりまでにすべてのサーバーをアップグレードできない場合は、アップグレードの移行中に、次のオプションを使用してアプリケーションとデータを保護できます。

* 既存の Windows Server 2008 と 2008 R2 のワークロードをそのまま Azure Virtual Machines (VM) に移行する。
    * この Azure への移行により、拡張セキュリティ更新プログラム (ESU) が自動的に 3 年分追加されます。 Azure VM のコスト以外に拡張セキュリティ更新プログラムの追加料金は発生しません。追加の構成も必要ありません。
* 新しい Windows Server のバージョンにアップグレードする準備が整うまで、サーバーの拡張セキュリティ更新プログラムのサブスクリプションを購入し、保護された状態を維持する。
    * この更新プログラムは、サポート ライフサイクルの終了日から最大 3 年間提供されます。

3 年間の拡張更新プログラムが過ぎると、コンピューターが追加の更新プログラムを受信することができません。

## <a name="what-are-extended-security-updates-for-windows-server"></a>Windows Server の拡張セキュリティ更新プログラムとは

Windows Server の拡張セキュリティ更新プログラム (ESU) には、2020 年 1 月 14 日から最大 3 年間のセキュリティ更新プログラムと、*クリティカル*または*重要*と判断された情報が含まれます。 拡張セキュリティ更新プログラムに、次のものは含まれません。

* 新機能
* お客様から要求されたセキュリティ以外に関する修正プログラム
* 設計変更要求

詳細については、「[拡張セキュリティ更新プログラムのよくある質問 (FAQ)](https://www.microsoft.com/cloud-platform/extended-security-updates)」を参照してください。

## <a name="register-for-extended-security-updates"></a>拡張セキュリティ更新プログラムに登録する

拡張セキュリティ更新プログラムを使用するには、マルチ ライセンス認証キー (MAK) を作成して、Windows Server 2008 および 2008 R2 のコンピューターに適用します。 このキーを使用すると、Windows Update サーバーが、引き続きセキュリティ更新プログラムを受信できることを認識します。 オンプレミスのコンピューターのみを使用する場合でも、拡張セキュリティ更新プログラムに登録して、Azure portal でこれらのキーを管理することができます。

> [!NOTE]
> Azure で Windows Server 2008 / 2008 R2 の VM を実行する場合、次の手順を行う必要はありません。 Azure VM は、拡張セキュリティ更新プログラムに対して自動的に有効になります。 拡張セキュリティ更新プログラムのリソースとキーを作成する必要はありません。Azure VM で拡張セキュリティ更新プログラムを使用するための追加料金も発生しません。

拡張セキュリティ更新プログラムに Azure 以外の VM を登録してキーを作成するには、Azure portal で次の手順を行います。

1. [Azure portal](https://portal.azure.com/) にサインインします。
1. Azure portal の上部にある検索ボックスで、**拡張セキュリティ更新プログラム**を検索して選択します。

    ![Azure portal で拡張セキュリティ更新プログラムを検索する](media/extended-security-updates/esu-portal-search.png)

    以前に拡張セキュリティ更新プログラムを使用したことがない場合は、まず **[+]** を選択して拡張セキュリティ更新プログラムのリソースを作成します。 それ以外の場合は、一覧からリソースを選択します。

1. **[Register for Extended Service Updates]\(拡張サービス更新プログラムに登録する\)** で、 **[Get started]\(開始\)** を選択します。

    ![Azure portal で拡張セキュリティ更新プログラムの使用を開始する](media/extended-security-updates/get-started-with-esu.png)

1. 最初のキーを作成するには、 **[キーの取得]** を選択します。

    ![Azure portal でキーの作成を選択する](media/extended-security-updates/get-key.png)

    > [!NOTE]
    > 拡張セキュリティ更新プログラムのリソースとキーを作成するには、アカウントに関連付けられている Azure サブスクリプションが必要です。 アカウントに Azure サブスクリプションが関連付けられていない場合は、別のユーザー アカウントでサインインするか、portal に表示されている手順に従って Azure サブスクリプションを作成します。

1. **[Azure の詳細]** で、Azure サブスクリプション、リソース グループ、およびキーの場所を選択します。

    **[登録の詳細]** で、次の情報を入力します。

    | 設定             | 値 |
    |---------------------|-------|
    | キー名            | キーの表示名 (*Agreement01* など)。 |
    | 契約番号    | ボリューム ライセンス契約管理システムまたはエンタープライズ契約プログラムの MSLicense によって生成された契約番号。 |
    | コンピューター数 | このキーを使用して拡張セキュリティ更新プログラムをインストールするコンピューターの数を選択します。 |
    | オペレーティング システム    | このキーを使用するオペレーティングシステム (Windows Server 2008、Windows Server 2008 R2 など) を選択します。 |

    準備ができたら、 **[Review + register]\(確認 + 登録\)** を選択します。

1. 検証が正常に完了すると、新しいレジストリ リソースの選択内容の概要が表示されます。 必要に応じて、検証エラーを修正するか、構成の選択を更新します。 Azure の[使用条件](https://azure.microsoft.com/support/legal/)と[プライバシー ポリシー](https://privacy.microsoft.com/privacystatement)を確認できます。

    チェックボックスをオンにして、対象となるコンピューターを所有しており、そのキーが組織内でのみ使用されることを確認します。

    ![キーが組織でのみ使用されることを確認する](media/extended-security-updates/confirm-key-usage.png)

    準備ができたら、 **[作成]** を選択して MAK を生成します。

コンピューターで拡張セキュリティ更新プログラムの登録を使用できるようになりました。 作成されたキーは、セキュリティ更新プログラムの対象として使用する Windows Server 2008 および 2008 R2 コンピューターに適用する必要があります。

## <a name="download-and-apply-extended-security-updates"></a>拡張セキュリティ更新プログラムをダウンロードして適用する

Windows Server 用の拡張セキュリティ更新プログラムの配布、ダウンロード、および適用は、既存の展開プロセスと同じです。 拡張セキュリティ更新プログラムによって提供される更新プログラムは、*セキュリティ*のみを対象としており、すべての更新プログラムが火曜日にリリースされます。

更新プログラムは、既にあるツールとプロセスを使用してインストールできます。 唯一の違いは、更新プログラムをダウンロードしてインストールするには、前のセクションで生成したキーを使用してシステムを登録する必要があることです。

Azure VM では、拡張セキュリティ更新プログラムのためにコンピューターを有効にするプロセスが自動的に完了します。 更新プログラムは、追加の構成なしでダウンロードしてインストールする必要があります。
