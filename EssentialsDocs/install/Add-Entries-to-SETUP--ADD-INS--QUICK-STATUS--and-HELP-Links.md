---
title: セットアップ リンク、アドイン リンク、簡単な状態リンク、ヘルプ リンクへのエントリの追加
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: c0a8f10d-fd85-4c8d-b9bb-176cb1db1f46
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 78eb8a24b32763ae4f7c048889529f87d3b4fecf
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80817665"
---
# <a name="add-entries-to-setup-add-ins-quick-status-and-help-links"></a>セットアップ リンク、アドイン リンク、簡単な状態リンク、ヘルプ リンクへのエントリの追加

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

**セットアップ**、**アドイン**、**簡単な状態** タスク一覧にタスクを追加でき、ダッシュボードのホーム ページの コミュニティ リンク セクションにリンクを追加できます。 タスクやリンクをこれらの一覧とセクションに追加するには、OEMHomePageContent.home ファイルという名前の XML ファイルまたは OEMHomePageContent.dll という名前の埋め込みリソース ファイルを %ProgramFiles%\Windows Server\Bin\Addins\Home に配置します。 埋め込みリソース ファイルを使用して、追加したタスクとリンクのテキストをローカライズできます。 .home ファイルには、タスクとリンクの XML 定義が含まれます。  
  
## <a name="adding-tasks-to-the-setup-add-ins-quick-status-task-lists-and-adding-links-to-help-task"></a>セットアップ、アドイン、簡単な状態タスク一覧にタスクを追加し、ヘルプ タスクにリンクを追加する  
 **[セットアップ]** 、 **[アドイン]** 、 **[簡単な状態]** タスク一覧にタスクを追加し、 **[ヘルプ]** タスクにリンクを追加するには、XML を使用してタスクとリンクを定義し、任意で埋め込みリソース ファイルを作成して、ファイルをサーバーにインストールします。 XML ファイルをリソース ファイルなしでサーバーにインストールする場合、OEMHomePageContent.home という名前にする必要があります。 アセンブリが XML ファイルとリソース ファイルのインストールに使用されている場合、OEMHomePageContent.dll という名前にし、Authenticode 署名する必要があります。  
  
### <a name="define-the-tasks-and-links"></a>タスクとリンクの定義  
 メモ帳などのテキスト エディターを使用して .home ファイルを作成できます。埋め込みリソース ファイルも作成している場合は、Visual Studio 2010 以上を使用してファイルを定義できます。 次の手順では、Visual Studio 2010 以降を使用してファイルを作成する方法を示します。  
  
##### <a name="to-define-the-tasks-and-links"></a>タスクとリンクを定義するには  
  
1. スタート メニューのプログラムを右クリックし、**管理者として実行** を選択して、Visual Studio 2010 以降を管理者として開きます。  
  
2. **[ファイル]** をクリックし、 **[新規作成]** をクリックし、 **[プロジェクト]** をクリックします。  
  
3. **[テンプレート]** ウィンドウで、 **[クラス ライブラリ]** をクリックし、 **[名前]** ボックスに「**OEMHomePageContent**」と入力して、 **[OK]** をクリックします。  
  
4. Class1.cs ファイルを削除します。  
  
5. 新しいプロジェクトを右クリックし、 **[追加]** をクリックし、 **[新しい項目]** をクリックします。  
  
6. **[テンプレート]** ウィンドウで **[XML ファイル]** をクリックし、 **[名前]** ボックスに「**OEMHomePageContent.home**」と入力して、 **[追加]** をクリックします。  
  
   > [!NOTE]
   >  XML ファイルをリソース ファイルなしでインストールする場合、OEMHomePageContent.home という名前にする必要があります。 アセンブリに含める場合は、拡張子が .home である限り、任意の名前を指定できます。  
  
7. 次の XML コードを OEMHomePageContent.home ファイルに追加します。  
  
   ```  
  
   <Tasks version=?2.0? xmlns=?https://schemas.microsoft.com/WindowsServerSolutions/2010/01/Dashboard>  
      <SetupMyServerTasks>  
         <Task name="MyTask"  
            description="MyTaskDescription"  
            id="GUID">  
                 <Action   
                 name=?MyAction1Name?   
                 image=?IconForAction1?  
                 type=?TaskType?  
                 exelocation=?ActionExeLocation? />  
                 <Action   
                 name=?MyAction2Name?   
                 image=?IconForAction2?  
                 type=?TaskType?  
                 exelocation=?ActionExeLocation? />  
                  ¦  
          </Task>  
                  ¦  
       </SetupMyServerTasks>  
   <MailServiceTasks>  
        <!-- Same schema as in œSetupMyServerTasks? but the tasks are shown in œConnect to Email Service? category. -->  
   </MailServiceTasks>  
   <LineOfBusinessTasks>  
        <!-- Same schema as in œSetupMyServerTasks? but the tasks are shown in œAdd-ins? category. -->  
  
   <GetQuickStatusTasks>  
         <Task name="MyQuickStatusTask1"  
            description="MyQuickStatusTask1Desc   "  
            id="GUID"  
            assembly="AssemblyName of quick status query implementation"  
            class="ClassName of quick status query implementation"           
            replaceid="GUID"/>  
              <!--  Same schema as Actions in œSetupMyServerTasks? -->   
            </Task>  
   </GetQuickStatusTasks>  
      <Links>  
         <Link  
            ID=?GUID?  
            Title="Displayed text of the link"  
            Description="A very short description"  
            ShellExecPath="Path to the application or URL"/>  
      </Links>  
   </Tasks>  
   ```  
  
    各項目の意味は次のとおりです。  
  
   |属性|説明|  
   |---------------|-----------------|  
   |Name (Task)|一覧のタスクに表示される名前です。 埋め込みリソース ファイルを作成する場合、この属性の値は文字列リソースです。|  
   |description (Task)|タスクの説明です。 埋め込みリソース ファイルを作成する場合、この属性の値は文字列リソースです。|  
   |id (Task)|タスクの識別子です。 この識別子は、GUID でなければなりません。 **Exe**タスクに対して新しい guid を作成しますが、**グローバル**タスクの場合は、サブタブの作業ウィンドウに対してタスクを定義したときに作成した guid を使用します。GUID の作成の詳細については、「 [guid の作成 (guidgen.exe)](https://go.microsoft.com/fwlink/?LinkId=116098)」を参照してください。|  
   |image|このフィールドは無視されます。|  
   |Name (Action)|タスクの名前を表示します。|  
   |Type (Action)|タスクの種類を説明します。 タスクは、**グローバル** タスク、**exe**、または URL タスクのいずれかです。 **グローバル**タスクは、サブタブの作業ウィンドウのタスクを定義するときに作成したのと同じグローバルタスクです。サブタブの [タスク] ウィンドウと、ホームページの [はじめにタスク] または [一般的なタスク] の一覧の両方で使用できるグローバルタスクの作成の詳細については、「サポートクラスの作成」を参照してください。ここでは、サブタブを作成する方法について説明します。[Windows Server SOLUTIONS SDK](https://go.microsoft.com/fwlink/?LinkID=248648)の。 **exe** タスクは、作業の開始タスク一覧または共通タスク一覧からアプリケーションを実行するために使用できます。|  
   |exelocation|タスクに関連付けられているアプリケーションへのパスです。 この属性は、**exe** タスクに対してのみ使用されます。|  
   |replaceid|このタスクに置き換えられるタスクの識別子です。|  
   |assembly|簡単な状態のクエリを実装するためのクラスを提供するアセンブリの AssemblyName。 アセンブリは、Program files \ windows server\bin\\に配置されている必要があります。|  
   |class|クラスの名前で簡単な状態のクエリを実装します。 このクラスは、**ITaskStatusQuery** インターフェイスを実装する必要があります。|  
   |Title (link)|リンクに表示されるテキストです。 埋め込みリソース ファイルを作成する場合、この属性の値は文字列リソースです。|  
   |Description (link)|リンク先の説明です。 埋め込みリソース ファイルを作成する場合、この属性の値は文字列リソースです。|  
   |ShellExecPath|アプリケーションへのパスまたは URL です。<br /><br /> **注:** 環境変数は、ShellExecPath 属性でサポートされています。|  
  
    次のコード例は、アプリケーションへのリンクの定義方法を示しています。  
  
   ```  
   <Links>  
      <Link Title="Calc" Description="Launches Calc" ShellExecPath="%windir%\system32\calc.exe" />  
   </Links>  
   ```  
  
    次のコード例は、Web ページへのリンクの定義方法を示しています。  
  
   ```  
   <Links>  
      <Link Title="Browser" Description="Open browser" ShellExecPath="http://www.adventureworks.com/" />  
   </Links>  
   ```  
  
8. タスクまたはリンクを表すように属性値を変更します。  
  
9. **ソリューション エクスプローラー**で、 **[OEMHomePageContent.home]** を右クリックし、 **[プロパティ]** をクリックします。  **[プロパティ]** ウィンドウで、 **[ビルド アクション]** の下にある **[埋め込まれたリソース]** を選択します。  
  
10. OEMHomePageContent.home ファイルを保存します。  
  
    簡単な状態のクエリを実装する方法については、 [Windows Server Solutions SDK](https://go.microsoft.com/fwlink/?LinkID=248648)のドキュメントとサンプルを参照してください。  
  
#### <a name="change-the-status-of-a-setupadd-ins-task"></a>セットアップ/アドイン タスクのステータスの変更  
 [セットアップ] と [アドイン] の一覧に表示されるタスクのステータスを、完了 (アドイン用に構成されています) と完了していません (アドイン用に構成されていません) で切り替えることができます。  
  
 新しいタスクに関連付けられるアプリケーションを定義するときは、Microsoft.WindowsServerSolutions.Administration.ObjectModel.TaskStatusHelper 名前空間の SetTaskStatus メソッドを使用して、タスクのステータスを変更することができます (このメソッドは Windows Server Solutions SDK に付属していますが、ドキュメント化されていません)。 たとえば、列挙値 TaskStatus.Complete で SetTaskStatus メソッドを呼び出し、チェック マークを灰色から緑色に変更できます (SetTaskStatus(id, TaskStatus.Complete)、**id** はタスクの識別子)。 使用可能な列挙値は TaskStatus.Complete、TaskStatus.Incomplete、TaskStatus.Hidden です。  
  
##### <a name="replace-tasks"></a>タスクの置換  
 タスクの GUID をタスク定義の replaceid 属性に追加することで、作業の開始タスクまたは共通タスク一覧で事前に定義されたタスクを置換できます。 次の表は、タスクと、ダッシュボードで置換できる対応する識別子の一覧です。  
  
|[タスク名]|[Identifier]|  
|---------------|----------------|  
|他のマイクロソフト製品の更新プログラムの入手|8412D35A-13EE-4112-AE0B-F7DBC83EA83D|  
|サーバー バックアップのセットアップ|F68B3F3F-19DE-499D-9ACB-4BB41B8FF420|  
|Anywhere Access をセットアップする|8991302D-676A-4A7C-B244-D1E08AE0EFEA|  
|電子メール アラート通知のセットアップ|DE6F2B36-F19C-4FAF-998B-9772300E3530|  
|ユーザー アカウントの追加|6D5B5D5F-2EC7-4B1F-9580-4DB084B278B1|  
|サーバー フォルダーの追加|03F1F438-D94E-439B-A9F7-0C817C37D625|  
|Anywhere Access - 簡単な状態|6093B462-1F04-4212-8804-9BC823070FAD|  
|サーバー バックアップ - 簡単な状態|156947D8-21DC-45FE-A9A8-2F80AE304191|  
|サーバー フォルダー - 簡単な状態|C657E8AB-AC1F-4AA1-8E80-5AF6BB27C314|  
|アクティブなユーザー アカウント - 簡単な状態|68BCB125-CE8F-467F-B65B-56AD45A614B5|  
|電子メール アラート通知 - 簡単な状態|75AB06E7-A679-4D62-A5EC-65362FE4F9DB|  
|コンピューター - 簡単な状態|7966A974-D52D-4F5D-B37F-05C1B73CEEF3|  
  
##### <a name="optional-create-the-resource-file"></a>(省略可能) リソース ファイルの作成  
 作業の開始タスク、共通タスク、コミュニティ リンクに追加するタスクのテキストをローカライズする場合、.home ファイルと、テキスト文字列を定義する .home.resx ファイルが含まれるアセンブリを作成する必要があります。  
  
###### <a name="to-create-the-resource-file"></a>リソース ファイルを作成するには  
  
1.  タスク用に作成したプロジェクトを右クリックし、 **[追加]** をクリックし、 **[新しい項目]** をクリックします。  
  
2.  **[テンプレート]** ウィンドウで、 **[リソース ファイル]** をクリックし、 **[名前]** ボックスに「**OEMHomePageContent.home.resx**」と入力して、 **[追加]** をクリックします。  
  
    > [!NOTE]
    >  リソース ファイルには、拡張子が .home.resx である限り、任意の名前を指定できます。  
  
3.  追加するタスクまたはリンクごとに、OEMHomePageContent.home.resx ファイルに、OEMHomePageContent.home ファイルで定義されている Task 要素と Link 要素に一致する文字列と値を追加する必要があります。 次のコード例は、リソース ファイル用に構造化された Tasks.xml ファイルの例を示しています。  
  
    ```  
  
    <Tasks version=?2.0? xmlns=?https://schemas.microsoft.com/WindowsServerSolutions/2010/01/Dashboard>  
       <SetupMyServerTasks>  
          <Task name="MyTask"  
             description="MyDescription"  
             id="GUID">  
             <Action  
             name="MyActionname"  
             image="IconForAction"  
             type="TaskType"  
             exelocation="ActionExeLocation" />  
          </Task>  
       </SetupMyServerTasks>  
    </Tasks>  
  
    ```  
  
    > [!NOTE]
    >  ローカライズに使用される属性の識別子にスペースを含めることはできません。  
  
4.  適切な値を使用して MyTask、MyTaskDescription、MyActionName、および IconForAction のリソース名を .resx ファイルに追加します。  
  
5.  OEMHomePageContent.home.resx ファイルを保存し、ソリューションをビルドします。  
  
#####  <a name="sign-the-assembly-with-an-authenticode-signature"></a><a name="BKMK_SignAssembly"></a>Authenticode 署名を使用してアセンブリに署名する  
 オペレーティング システムで使用するために、アセンブリを Authenticode で署名する必要があります。 アセンブリの署名の詳細については、「 [Authenticode によるコードの署名と確認 (英語の場合があります)](https://msdn.microsoft.com/library/ms537364\(VS.85\).aspx#SignCode)」を参照してください。  
  
##### <a name="install-the-task-files"></a>タスクのファイルのインストール  
 .home および .home.resx ファイルを作成した後、ファイルをサーバーにインストールする必要があります。  
  
###### <a name="to-install-the-task-files"></a>タスクのファイルをインストールするには  
  
1.  エラーなしでソリューションがビルドされることを確認します。  
  
2.  埋め込みリソース ファイルを作成しなかった場合、OEMHomePageContent.home ファイルをサーバー上の **%ProgramFiles%\Windows Server\Bin\Addins\Home** にコピーします。 埋め込みリソース ファイルを作成した場合、OEMHomePageContent.dll ファイルをサーバー上の **%ProgramFiles%\Windows Server\Bin\Addins\Home** にコピーします。  
  
## <a name="see-also"></a>参照  
 [イメージ  の作成とカスタマイズ](Creating-and-Customizing-the-Image.md)  
 [追加のカスタマイズ](Additional-Customizations.md)   
 [展開  のイメージの準備](Preparing-the-Image-for-Deployment.md)  
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)