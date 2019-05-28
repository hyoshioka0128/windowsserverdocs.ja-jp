---
title: 拡張機能で PowerShell を使用する
description: Windows Admin Center SDK (プロジェクト ホノルル) 拡張機能で PowerShell を使用します。
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 05/09/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 7375732fd464519cd1533043d271065e488fd46a
ms.sourcegitcommit: 7cb939320fa2613b7582163a19727d7b77debe4b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/14/2019
ms.locfileid: "65621358"
---
# <a name="using-powershell-in-your-extension"></a>拡張機能で PowerShell を使用する #

>適用先:Windows Admin Center、Windows Admin Center プレビュー

Windows Admin Center の拡張機能 SDK にさらに深くしましょう: 拡張機能への PowerShell コマンドを追加する方法について説明します。

## <a name="powershell-in-typescript"></a>TypeScript での PowerShell ##

Gulp のビルド プロセスがいずれかを実行する生成手順```{!ScriptName}.ps1```に配置する、```\src\resources\scripts```フォルダーにそれらをビルドし、```powershell-scripts```クラスの下で、```\src\generated```フォルダー。

>[!NOTE] 
> 手動で更新しない、```powershell-scripts.ts```も```strings.ts```ファイル。 [次へ] の生成に対して行った変更が上書きされます。

## <a name="running-a-powershell-script"></a>PowerShell スクリプトを実行します。 ##
ノードで実行する任意のスクリプトを配置できる```\src\resources\scripts\{!ScriptName}.ps1```します。 
>[!IMPORTANT] 
> 変更、```{!ScriptName}.ps1```までプロジェクトのファイルは反映されません```gulp generate```が実行されています。

API の動作を対象とする、渡される必要があるすべてのパラメーターで、PowerShell スクリプトを作成して作成されたセッションでスクリプトを実行し、ノードで PowerShell セッションを作成します。

たとえば、このスクリプトがある```\src\resources\scripts\Get-NodeName.ps1```:
``` ps1
Param
 (
    [String] $stringFormat
 )
 $nodeName = [string]::Format($stringFormat,$env:COMPUTERNAME)
 Write-Output $nodeName
```

ターゲット ノードは、PowerShell セッションを作成します。
``` ts
const session = this.appContextService.powerShell.createSession('{!TargetNode}'); 
```
入力パラメーターは、PowerShell スクリプトを作成します。
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
今すぐは先ほど作成した監視可能な関数をサブスクライブする必要があります。 この PowerShell スクリプトを実行する関数を呼び出す必要がありますに配置します。
```ts
this.getNodeName().subscribe(
     response => {
    console.log(response)
     }
);
```
CreateSession メソッドに、ノードの名前を指定して、新しい PowerShell セッションが作成、使用、および PowerShell 呼び出しの完了時にすぐに破棄します。 

### <a name="key-options"></a>キーのオプション ###
PowerShell API を呼び出すときに、いくつかのオプションがあります。 セッションが作成されるたびに作成できます、キーの有無。 

**キー:** これには、検索して (つまり Component2 がその同じセッションを使用して Component1"SME ROCKS、"キーを使用してセッションを作成できます) のコンポーネントでも、再利用が可能なキー付きのセッションが作成されます。キーが指定されている場合に作成されるセッション破棄する必要がの呼び出し元の dispose() 上記の例で作成しました。 5 分以上の破棄されず、セッションを保持する必要があります。 
```ts
  const session = this.appContextService.powerShell.createSession('{!TargetNode}', '{!Key}');
```

**キーを使用しません。** キーは、セッションに自動的に作成されます。 このセッションでは、3 分後に自動的に破棄します。 キーを使用しないを使用すると、セッションの作成時に使用可能な既にすべての実行空間の使用をリサイクルする、拡張機能ができます。 実行空間がない場合よりも、新たに作成されます。 この機能は、1 回限りの呼び出しが繰り返し使用されるパフォーマンスに影響することができます。 セッションは作成するには約 1 秒、速度低下を招くので継続的にセッションをリサイクルします。

```ts
  const session = this.appContextService.powerShell.createSession('{!TargetNodeName}');
```
または 
``` ts 
const session = this.appContextService.powerShell.createAutomaticSession('{!TargetNodeName}');
```
ほとんどの場合、キー付きのセッションを作成、```ngOnInit()```メソッド、および内のイメージの dispose```ngOnDestroy()```します。 コンポーネントがコンポーネント間で共有されていない、基になるセッション内の複数の PowerShell スクリプトがある場合、このパターンに従います。
最良の結果をサービスではなく、コンポーネントの内部で管理されるセッションの作成 - その有効期間を維持するかどうかを確認し、クリーンアップを適切に管理することができます。

最良の結果をサービスではなく、コンポーネントの内部で管理されるセッションの作成 - その有効期間を維持するかどうかを確認し、クリーンアップを適切に管理することができます。

### <a name="powershell-stream"></a>PowerShell Stream ###
実行時間の長いスクリプトとデータがある場合を出力段階的に、PowerShell ストリームには、スクリプトを完了するまで待機することがなく、データを処理することができます。 監視可能な next() は、データを受信すると、すぐに呼び出されます。
```ts
this.appContextService.powerShellStream.run(session, script);
```

### <a name="long-running-scripts"></a>長時間実行されるスクリプト ###
バック グラウンドで実行するには実行時間の長いスクリプトがあれば、作業項目を送信できます。 スクリプトの状態は、ゲートウェイによって追跡され、ステータスの更新は通知を送信できます。 
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
> 表示される進行状況は、Write-progress を記述したスクリプトに含める必要があります。 例:
> ``` ps1
>  Write-Progress -Activity ‘The script is almost done!’ -percentComplete 95
>```

#### <a name="workitem-options"></a>作業項目のオプション ####

| 関数 (function) | 説明 |
| ----- | ----------- |
| submit() | 作業項目を送信します。 
| submitAndWait() | 作業項目を送信し、その実行の完了を待つ
| wait() | 既存の職場の待機を完了する項目
| query() | 既存の作業項目 id でのクエリ
| find() | 既存の TargetNodeName、ModuleName、または typeId によって作業項目を見つけてします。

### <a name="powershell-batch-apis"></a>PowerShell の Batch Api ###
複数のノードで同じスクリプトを実行する必要があります、batch の PowerShell セッションを使用できます。 例:
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
| runSingleCommand | 配列内のすべてのノードに対して 1 つのコマンドを実行します。 
| 実行 | ペアになっているノードに対応するコマンドを実行します。
| キャンセル | 配列内のすべてのノードでコマンドをキャンセルします。
