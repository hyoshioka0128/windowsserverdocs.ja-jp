---
title: 拡張機能で PowerShell を使用する
description: 拡張機能での PowerShell の使用 Windows 管理センター SDK (Project ホノルル)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 05/09/2019
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 6e99fc43d4acb7a70dfd3a8ba19dae6492c41b2b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357051"
---
# <a name="using-powershell-in-your-extension"></a>拡張機能で PowerShell を使用する #

>適用先:Windows Admin Center、Windows Admin Center Preview

Windows 管理センターの拡張機能 SDK の詳細について説明します。拡張機能に PowerShell コマンドを追加する方法について説明します。

## <a name="powershell-in-typescript"></a>TypeScript での PowerShell ##

Gulp ビルド```{!ScriptName}.ps1```プロセスには、 ```\src\resources\scripts```フォルダー内に配置されたを取得して、フォルダーの```\src\generated```下の```powershell-scripts```クラスにビルドする生成手順があります。

>[!NOTE] 
> ```powershell-scripts.ts``` またはファイルを手動で```strings.ts```更新しないでください。 行った変更は、次の生成時に上書きされます。

## <a name="running-a-powershell-script"></a>PowerShell スクリプトの実行 ##
ノードで実行するすべてのスクリプトは、に```\src\resources\scripts\{!ScriptName}.ps1```配置できます。 
>[!IMPORTANT] 
> ```{!ScriptName}.ps1```ファイルに加えられた変更は、が実行されるまで```gulp generate```プロジェクトに反映されません。

API は、まずターゲットとするノードで PowerShell セッションを作成し、渡す必要があるパラメーターを使用して PowerShell スクリプトを作成し、作成されたセッションでスクリプトを実行することで機能します。

たとえば、次のスクリプト```\src\resources\scripts\Get-NodeName.ps1```があります。
``` ps1
Param
 (
    [String] $stringFormat
 )
 $nodeName = [string]::Format($stringFormat,$env:COMPUTERNAME)
 Write-Output $nodeName
```

ここでは、ターゲットノードの PowerShell セッションを作成します。
``` ts
const session = this.appContextService.powerShell.createSession('{!TargetNode}'); 
```
次に、入力パラメーターを使用して PowerShell スクリプトを作成します。
```ts
const script = PowerShell.createScript(PowerShellScripts.Get_NodeName, {stringFormat: 'The name of the node is {0}!'});
```
最後に、作成したセッションでそのスクリプトを実行する必要があります。
``` ts
  public ngOnInit(): void {
    this.session = this.appContextService.powerShell.createAutomaticSession('{!TargetNode}');
  }

  public getNodeName(): Observable<any> {
    const script = PowerShell.createScript(PowerShellScripts.Get_NodeName.script, { stringFormat: 'The name of the node is {0}!'});
    return this.appContextService.powerShell.run(this.session, script)
    .pipe(
        map(
        response => {
            if (response && response.results) {
                return response.results;
            }
            return 'no response';
        }
      ) 
    );
  }

  public ngOnDestroy(): void {
    this.session.dispose()
  }

```
ここでは、作成した観測可能な関数をサブスクライブする必要があります。 次のようにして、PowerShell スクリプトを実行する関数を呼び出す必要があります。
```ts
this.getNodeName().subscribe(
     response => {
    console.log(response)
     }
);
```
CreateSession メソッドにノード名を指定すると、新しい PowerShell セッションが作成され、使用された後、PowerShell 呼び出しの完了時にすぐに破棄されます。 

### <a name="key-options"></a>キーオプション ###
PowerShell API を呼び出すときに使用できるオプションがいくつかあります。 セッションが作成されるたびに、キーの有無に関係なく作成できます。 

**キー:** これにより、コンポーネント間でも検索と再利用が可能なキー付きセッションが作成されます (つまり、Component1 はキー "SME-岩" を使用してセッションを作成でき、Component2 は同じセッションを使用できます)。キーが指定されている場合は、上記の例のように dispose () を呼び出すことによって、作成されたセッションを破棄する必要があります。 セッションは、5分を超えて破棄されることなく保持されません。 
```ts
  const session = this.appContextService.powerShell.createSession('{!TargetNode}', '{!Key}');
```

**キーなし**セッションのキーが自動的に作成されます。 このセッションは、3分後に自動的に破棄されます。 キーなしを使用すると、セッションの作成時に既に使用可能な実行空間の使用を拡張でリサイクルできます。 新しい実行空間が使用できない場合は、それが作成されます。 この機能は1回限りの呼び出しに適していますが、繰り返し使用するとパフォーマンスに影響する場合があります。 セッションの作成には約1秒かかります。そのため、継続的なリサイクルセッションによって、パフォーマンスが低下する可能性があります。

```ts
  const session = this.appContextService.powerShell.createSession('{!TargetNodeName}');
```
または 
``` ts 
const session = this.appContextService.powerShell.createAutomaticSession('{!TargetNodeName}');
```
ほとんどの場合、 ```ngOnInit()```メソッドでキー付きセッションを作成し、で```ngOnDestroy()```そのセッションを破棄します。 1つのコンポーネントに複数の PowerShell スクリプトがあり、基になるセッションがコンポーネント間で共有されていない場合は、このパターンに従います。
最良の結果を得るには、セッションの作成がサービスではなくコンポーネント内で管理されていることを確認してください。これにより、有効期間とクリーンアップを適切に管理できるようになります。

最良の結果を得るには、セッションの作成がサービスではなくコンポーネント内で管理されていることを確認してください。これにより、有効期間とクリーンアップを適切に管理できるようになります。

### <a name="powershell-stream"></a>PowerShell ストリーム ###
実行時間の長いスクリプトがあり、データが徐々に出力される場合、PowerShell ストリームを使用すると、スクリプトが終了するのを待たずにデータを処理できます。 観測可能な次の () は、データが受信されるとすぐに呼び出されます。
```ts
this.appContextService.powerShellStream.run(session, script);
```

### <a name="long-running-scripts"></a>実行時間の長いスクリプト ###
バックグラウンドで実行するスクリプトが長時間実行されている場合は、作業項目を送信できます。 スクリプトの状態はゲートウェイによって追跡され、状態の更新を通知に送信できます。 
```ts
const workItem: WorkItemSubmitRequest = {
    typeId: 'Long Running Script',
    objectName: 'My long running service',
    powerShellScript: script,
    
    //in progress notifications
    inProgressTitle: 'Executing long running request',
    startedMessage: 'The long running request has been started',
    progressMessage: 'Working on long running script – {{ percent }} %',

    //success notification
    successTitle: 'Successfully executed a long running script!',
    successMessage: '{{objectName}} was successful',
    successLinkText: 'Bing',
    successLink: 'http://www.bing.com',
    successLinkType: NotificationLinkType.Absolute,

    //error notification
    errorTitle: 'Failed to execute long running script',
    errorMessage: 'Error: {{ message }}'

    nodeRequestOptions: {
       logAudit: true,
       logTelemetry: true
    }
};

return this.appContextService.workItem.submit('{!TargetNode}', workItem);
```

>[!NOTE] 
> 進行状況を表示するには、記述したスクリプトに書き込みの進行状況が含まれている必要があります。 以下に例を示します。
> ``` ps1
>  Write-Progress -Activity ‘The script is almost done!' -percentComplete 95
>```

#### <a name="workitem-options"></a>WorkItem オプション ####

| 関数 (function) | 説明 |
| ----- | ----------- |
| submit () | 作業項目を送信します 
| submitAndWait () | 作業項目を送信し、実行が完了するまで待機する
| wait () | 既存の作業項目が完了するまで待機する
| query () | Id による既存の作業項目のクエリ
| find () | TargetNodeName、ModuleName、または typeId を使用して、作業項目を検索します。

### <a name="powershell-batch-apis"></a>PowerShell Batch Api ###
同じスクリプトを複数のノードで実行する必要がある場合は、batch PowerShell セッションを使用できます。 以下に例を示します。
```ts
const batchSession = this.appContextService.powerShell.createBatchSession(
    ['{!TargetNode1}', '{!TargetNode2}', sessionKey);
  this.appContextService.powerShell.runBatchSingleCommand(batchSession, command).subscribe((responses: PowerShellBatchResponseItem[]) => {
    for (const response of responses) { 
      if (response.error || response.errors) {
        //handle error
      } else {
        const results = response.properties && response.properties.results;
        //response.nodeName
        //results[0]
      }
    }
     },
     Error => { /* handle error */ });  

```


#### <a name="powershellbatch-options"></a>PowerShellBatch オプション ####
| オプション | 説明 |
| ----- | ----------- |
| runSingleCommand | 配列内のすべてのノードに対して1つのコマンドを実行します。 
| 実行 | ペアのノードで対応するコマンドを実行する
| cancel | 配列内のすべてのノードでコマンドを取り消します。
