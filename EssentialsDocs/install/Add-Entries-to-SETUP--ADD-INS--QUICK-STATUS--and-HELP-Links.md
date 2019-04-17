---
title: "セットアップ、アドイン、簡単な状態、およびヘルプ リンクにエントリを追加します。"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c0a8f10d-fd85-4c8d-b9bb-176cb1db1f46
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 6d3303f2c6d84932ad9d5dee8a547cd478447732
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="add-entries-to-setup-add-ins-quick-status-and-help-links"></a>セットアップ、アドイン、簡単な状態、およびヘルプ リンクにエントリを追加します。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

タスクを追加することができます、**セットアップ**、**アドイン**、**簡単な状態**タスク一覧と、ダッシュ ボードのホーム ページのコミュニティ リンク] セクションにリンクを追加することができます。 OEMHomePageContent.home ファイルまたは埋め込みリソース ファイルを %ProgramFiles%\Windows server \bin\addins\home に OEMHomePageContent.dll という名前のという XML ファイルを配置することによって、タスクとリンクは、これらの一覧とセクションに追加されます。 埋め込みリソース ファイルは、タスクとリンクを追加することでテキストをローカライズするために使用します。 .Home ファイルには、タスクとリンクの XML 定義が含まれています。  
  
## <a name="adding-tasks-to-the-setup-add-ins-quick-status-task-lists-and-adding-links-to-help-task"></a>セットアップ、アドイン、簡単な状態タスク一覧にタスクを追加して、ヘルプ タスクにリンクを追加します。  
 タスクを追加することができます、**セットアップ**、**アドイン**、**簡単な状態**タスクの一覧、およびへのリンク、**ヘルプ**タスクとリンクの XML を使用して定義することでタスク必要に応じて、埋め込みリソース ファイルを作成し、サーバー上のファイルをインストールします。 XML ファイルがインストールする場合、サーバーをリソース ファイルなしで、OEMHomePageContent.home が名前する必要があります。 アセンブリが XML ファイルとリソース ファイルの両方をインストールに使用されている場合、OEMHomePageContent.dll という必要があり、Authenticode 署名する必要があります。  
  
### <a name="define-the-tasks-and-links"></a>タスクとリンクを定義します。  
 メモ帳などのテキスト エディタを使用するには、.home ファイルを作成または埋め込みリソース ファイルも作成している場合は、ファイルを定義する Visual Studio 2010 以降を使用することができます。 次の手順では、Visual Studio 2010 以降を使用して、ファイルを作成する方法を示します。  
  
##### <a name="to-define-the-tasks-and-links"></a>タスクとリンクを定義するには  
  
1.  [スタート] メニューにプログラムを右クリックして、Visual Studio 2010 以降を管理者としてを開く**管理者として実行**します。  
  
2.  をクリックして**ファイル**、] をクリックして**新規**、] をクリックし、**プロジェクト**します。  
  
3.  **テンプレート**] ウィンドウで、] をクリックして**クラス ライブラリ**、種類**OEMHomePageContent**で、**名**ボックスで、クリックして**[OK]**します。  
  
4.  Class1.cs ファイルを削除します。  
  
5.  新しいプロジェクトを右クリックし、をクリックして**追加**、] をクリックし、**新しい項目**します。  
  
6.  **テンプレート**] ウィンドウで、] をクリックして**XML ファイル**、種類**OEMHomePageContent.home**で、**名**ボックスで、クリックして**追加**します。  
  
    > [!NOTE]
    >  XML ファイルがインストールする場合、リソース ファイルを使用せず、OEMHomePageContent.home が名前する必要があります。 それが含まれる場合、アセンブリを指定できます任意の名前、拡張子が .home 限りです。  
  
7.  次の XML コードを OEMHomePageContent.home ファイルに追加します。  
  
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
  
     どこ：  
  
    |属性|説明|  
    |---------------|-----------------|  
    |名前 (タスク)|タスク一覧に表示される名前です。 埋め込みリソース ファイルを作成する場合、この属性の値は文字列リソースです。|  
    |(タスク) の説明|タスクの説明です。 埋め込みリソース ファイルを作成する場合、この属性の値は文字列リソースです。|  
    |Id (タスク)|タスクの識別子。 この識別子は、GUID である必要があります。 新しい GUID を作成する、**exe**タスクが、**グローバル**サブタブの作業ウィンドウに対してタスクを定義するときに作成した GUID を使用するタスク、します。GUID の作成の詳細については、次を参照してください。[Guid の作成 (guidgen.exe)](https://go.microsoft.com/fwlink/?LinkId=116098)します。|  
    |イメージ|このフィールドは無視されます。|  
    |名前 (アクション)|タスクの名前が表示されます。|  
    |(操作) の種類|タスクの種類について説明します。 タスクでは、次のいずれかのことができます。-**グローバル**タスク、**exe**、または url タスクです。 A**グローバル**タスクは、サブタブの作業ウィンドウに対してタスクを定義するときに作成した同じグローバル タスクです。サブタブの両方のタスク] ウィンドウとホーム ページの作業の開始タスクまたは共通タスク一覧で使用できるグローバル タスクの作成の詳細については、サポート クラスの œCreating を参照してください。œHow で: サブタブの作成ですか?[Windows Server Solutions SDK](https://go.microsoft.com/fwlink/?LinkID=248648)します。 **Exe**作業の開始タスクからアプリケーションを実行するタスクを使用することができます、または共通タスク一覧します。|  
    |exelocation|タスクに関連付けられているアプリケーションへのパス。 この属性はの使用のみ**exe**タスクです。|  
    |replaceid|このタスクに置き換えられるタスクの識別子。|  
    |アセンブリ|簡単な状態のクエリを実装するクラスを提供するアセンブリの AssemblyName。 アセンブリは、Program files \ Windows Server\bin\\ に配置する必要があります。|  
    |クラス|クラスの名前は、簡単な状態のクエリを実装します。 クラスを実装する必要がある**ITaskStatusQuery**インターフェイス。|  
    |タイトル (リンク)|リンクに表示されるテキストです。 埋め込みリソース ファイルを作成する場合、この属性の値は文字列リソースです。|  
    |(リンク) の説明|リンク先の説明です。 埋め込みリソース ファイルを作成する場合、この属性の値は文字列リソースです。|  
    |ShellExecPath|アプリケーション、または URL へのパス。<br /><br /> **注:**環境変数が ShellExecPath 属性でサポートされています。|  
  
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
  
8.  タスクまたはリンクを表す属性値を変更します。  
  
9. **ソリューション エクスプ ローラー**、右クリックして**OEMHomePageContent.home**、] をクリックし、**プロパティ**します。  **プロパティ**] ウィンドウで、**ビルド アクション**を選択**埋め込みリソース**します。  
  
10. OEMHomePageContent.home ファイルを保存します。  
  
 ドキュメントとサンプルを参照してください、簡単な状態のクエリを実装する方法、[Windows Server Solutions SDK](https://go.microsoft.com/fwlink/?LinkID=248648)します。  
  
#### <a name="change-the-status-of-a-setupadd-ins-task"></a>セットアップ/アドイン タスクの状態を変更します。  
 [セットアップ] と [アドインに記載されているタスクの状態の切り替え可能完了 (Add-ins 用に構成) (構成されていない Add-ins の) が完了するとします。  
  
 新しいタスクに関連付けられているアプリケーションを定義するときは、(が、Windows Server Solutions SDK に記載されていない)、Microsoft.WindowsServerSolutions.Administration.ObjectModel.TaskStatusHelper 名前空間の SetTaskStatus メソッドを使用することができます、タスクの状態を変更します。 たとえば、でしたを変更する、チェック マーク灰色から緑色に列挙値 TaskStatus.Complete で SetTaskStatus メソッドを呼び出すことによって (SetTaskStatus (id, TaskStatus.Complete)、場所**id**タスクの識別子は、)。 使用できる列挙値は TaskStatus.Complete、TaskStatus.Incomplete、taskstatus.hidden です。  
  
##### <a name="replace-tasks"></a>タスクを置換します。  
 タスクの GUID をタスク定義の replaceid 属性に追加することで、作業の開始タスクまたは共通タスク一覧で事前に定義できるタスクを置き換えることができます。 次の表は、タスクと、ダッシュ ボードで置換できる対応する id:  
  
|タスク名|識別子|  
|---------------|----------------|  
|他の Microsoft 製品の更新プログラムを入手します。|8412D35A-13EE-4112-AE0B-F7DBC83EA83D|  
|サーバー バックアップの設定します。|F68B3F3F-19DE-499D-9ACB-4BB41B8FF420|  
|Anywhere Access をセットアップします。|8991302D-676A-4A7C-B244-D1E08AE0EFEA|  
|電子メール アラート通知をセットアップします。|DE6F2B36-F19C-4FAF-998B-9772300E3530|  
|ユーザー アカウントを追加します。|6D5B5D5F-2EC7-4B1F-9580-4DB084B278B1|  
|サーバー フォルダーを追加します。|03F1F438-D94E-439B-A9F7-0C817C37D625|  
|Anywhere Access - 簡単な状態|6093B462-1F04-4212-8804-9BC823070FAD|  
|サーバー バックアップ - 簡単な状態|156947D8-21DC-45FE-A9A8-2F80AE304191|  
|サーバー フォルダー - 簡単な状態|C657E8AB-AC1F-4AA1-8E80-5AF6BB27C314|  
|アクティブなユーザー アカウント - 簡単な状態|68BCB125-CE8F-467F-B65B-56AD45A614B5|  
|電子メール アラート通知 - 簡単な状態|75AB06E7-A679-4D62-A5EC-65362FE4F9DB|  
|コンピューター - 簡単な状態|7966A974-D52D-4F5D-B37F-05C1B73CEEF3|  
  
##### <a name="optional-create-the-resource-file"></a>(省略可能)リソース ファイルを作成します。  
 作業の開始タスク、共通タスク、およびコミュニティへのリンクに追加するタスクのテキストをローカライズする場合、.home ファイルを含むアセンブリを作成する必要があります、および。テキスト文字列を定義する.home.resx ファイル。  
  
###### <a name="to-create-the-resource-file"></a>リソース ファイルを作成するには  
  
1.  タスク用に作成したプロジェクトを右クリックし、をクリックして**追加**、] をクリックし、**新しい項目**します。  
  
2.  **テンプレート**] ウィンドウで、] をクリックして**リソース ファイル**、種類**OEMHomePageContent.home.resx**で、**名**ボックスで、クリックして**追加**します。  
  
    > [!NOTE]
    >  リソース ファイルでもかまいませんが任意の名前が付いているように限り、。home.resx 拡張します。  
  
3.  各タスクまたはリンクを追加するには、OEMHomePageContent.home ファイルで定義されているタスクとリンクの要素に一致する OEMHomePageContent.home.resx ファイルに文字列と値を追加する必要があります。 次のコード例は、リソース ファイルの構造化された Tasks.xml ファイルの例を示します。  
  
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
  
4.  使用して MyTask、MyTaskDescription、MyActionName、および IconForAction のリソース名を .resx ファイルに適切な値に追加します。  
  
5.  OEMHomePageContent.home.resx ファイルを保存して、ソリューションをビルドします。  
  
#####  <a name="BKMK_SignAssembly"></a>Authenticode 署名によるアセンブリを署名します。  
 オペレーティング システムで使用されるようにアセンブリの Authenticode 署名する必要があります。 アセンブリの署名の詳細については、次を参照してください。[Authenticode によるコードのチェックの署名と](https://msdn.microsoft.com/library/ms537364\(VS.85\).aspx#SignCode)します。  
  
##### <a name="install-the-task-files"></a>作業ファイルをインストールします。  
 .Home を作成した後と。home.resx ファイル、する必要がありますサーバーにインストールします。  
  
###### <a name="to-install-the-task-files"></a>タスクのファイルをインストールするには  
  
1.  エラーなしでソリューションがビルドすることを確認します。  
  
2.  埋め込みリソース ファイルを作成しなかった場合、OEMHomePageContent.home ファイルのコピー **%ProgramFiles%\Windows server \bin\addins\home**サーバーにします。 埋め込みリソース ファイルを作成した場合、OEMHomePageContent.dll ファイルのコピー **%ProgramFiles%\Windows server \bin\addins\home**サーバーにします。  
  
## <a name="see-also"></a>参照してください。  
 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)