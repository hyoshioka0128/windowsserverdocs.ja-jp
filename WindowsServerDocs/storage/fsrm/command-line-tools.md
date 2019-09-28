---
title: ファイル サーバー リソース マネージャー コマンドライン ツール
description: この記事では Windows Server 2016 のコマンド ライン ツールについて説明します。
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 78c054c5b0c3de19d1f3acd825335eab2f140541
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71394299"
---
# <a name="file-server-resource-manager-command-line-tools"></a>ファイル サーバー リソース マネージャー コマンドライン ツール

> 適用対象:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2

ファイル サーバー リソース マネージャーによって、[FileServerResourceManager](https://technet.microsoft.com/itpro/powershell/windows/fileserverresourcemanager/fileserverresourcemanager) PowerShell コマンドレットと共に、次のコマンドライン ツールがインストールされます。

-   **Dirquota.exe**。 クォータ、自動適用クォータ、クォータ テンプレートを作成および管理するために使用します。
-   **Filescrn.exe**。 ファイル スクリーン、ファイル スクリーン テンプレート、ファイル スクリーンの例外、ファイル グループを作成および管理するために使用します。
-   **Storrept.exe**。 レポート パラメーターを設定したり、オン デマンドで記憶域レポートを生成したりするために使用します。 また、**schtasks.exe** を使用してスケジュールできるレポート タスクの作成にも使用します。

これらのツールを使用して、ローカル コンピューターやリモート コンピューター上の記憶域リソースを管理できます。 これらのコマンド ライン ツールの詳細については、次の情報を参照してください。

-   **Dirquota.exe**: <https://go.microsoft.com/fwlink/?LinkId=92741>
-   **Filescrn**: <https://go.microsoft.com/fwlink/?LinkId=92742>
-   **Storrept**: <https://go.microsoft.com/fwlink/?LinkId=92743>


> [!Note]
> 任意のコマンドについてコマンド構文と利用可能なパラメーターを表示するには、コマンドに <strong>/?</strong> パラメーターを指定して実行します。


## <a name="remote-management-using-the-command-line-tools"></a>コマンド ライン ツールを使用したリモート管理

各ツールには、ファイル サーバー リソース マネージャー MMC スナップインから利用できるものと同様の操作を実行するためのオプションがいくつか用意されています。 ローカル コンピューターではなくリモート コンピューターに対してコマンドの操作を実行するには、 **/remote**:*ComputerName* パラメーターを使用します。

たとえば、**Dirquota.exe** には、クォータ テンプレート設定を XML ファイルに書き込むための **template export** パラメーターと、XML ファイルからテンプレート設定を読み取るための **template import** パラメーターがあります。 **/remote**:*ComputerName* パラメーターを **Dirquota.exe template import** コマンドに追加すると、ローカル コンピューター上の XML ファイルからリモート コンピューターにテンプレートがインポートされます。

> [!Note]
> コマンド ライン ツールに **/remote**:<em>ComputerName</em> パラメーターを指定して、リモート コンピューターに対するテンプレートのエクスポート (またはインポート) を実行すると、テンプレートは、ローカル コンピューター上の XML ファイルに書き込まれます (インポートの場合は、XML ファイルからテンプレートがコピーされます)。

<br />

## <a name="additional-considerations"></a>その他の考慮事項 

コマンド ライン ツールを使用してリモート リソースを管理するには

-   ローカル コンピューターとリモート コンピューターの **Administrators** グループのメンバーであるドメイン アカウントを使用して、ログオンする必要があります。
-   コマンド ライン ツールは、管理者特権の [コマンド プロンプト] ウィンドウから事項する必要があります。 管理者特権でのコマンドプロンプトウィンドウを開くには、**スタート** ボタンをクリックし、**すべてのプログラム** をポイントします。次に、**アクセサリ** をクリックし、**コマンドプロンプト** を右クリックして、**管理者として実行**
-   リモート コンピューターで Windows Server が実行され、ファイル サーバー リソース マネージャーがインストールされている必要があります。
-   リモート コンピューターで、 **[リモート ファイル サーバー リソース マネージャー管理]** 例外を有効にする必要があります。 この例外は、[コントロール パネル] の [Windows ファイアウォール] で有効にします。


## <a name="see-also"></a>関連項目

-   [リモートの記憶域リソースを管理する](managing-remote-storage-resources.md)