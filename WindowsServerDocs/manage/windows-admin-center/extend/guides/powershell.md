---
title: 拡張機能で PowerShell を使用する
description: Windows Admin Center SDK (Project Honolulu) 拡張機能で PowerShell を使用します。
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: b1be4fe7639d913243cc28371dff9e98e0f5827e
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296724"
---
# 拡張機能で PowerShell を使用する #

>適用対象: Windows Admin Center、Windows Admin Center Preview

Windows Admin Center の拡張 SDK をより詳細なみましょう - PowerShell コマンドを拡張機能を追加する方法について説明します。

## TypeScript で PowerShell ##

Gulp ビルド プロセスがいずれかがかかる生成手順```{!ScriptName}.ps1```に配置されますが、```\src\resources\scripts```フォルダーにそれらの作成と、```powershell-scripts```下クラス、```\src\generated```フォルダー。

>[!NOTE] 
> 手動で更新しない、```powershell-scripts.ts```も、```strings.ts```ファイル。 次の生成に対して行った変更は上書きされます。

## Powerhell スクリプトの実行 ##
ノード上で実行するすべてのスクリプトに配置できる```\src\resources\scripts\{!ScriptName}.ps1```します。 
>[!IMPORTANT] 
> すべての変更に、```{!ScriptName}.ps1```しない限り、ファイルをプロジェクトに反映されませんが、生成 

API の動作をターゲットと、パラメーターで渡される必要があると、PowerShell スクリプトを作成および作成されたセッションでスクリプトを実行し、ノード上で PowerShell セッションを作成します。

たとえば、このスクリプトがある```\src\resources\scripts\Get-NodeName.ps1```:
``` ps1
Param
 (
    [String] $stringFormat
 )
 $nodeName = [string]::Format($stringFormat,$env:COMPUTERNAME)
 Write-Output $nodeName
```

このターゲット ノードの PowerShell セッションを作成します。
``` ts
const session = this.appContextService.powerShell.createSession('{!TargetNode}'); 
```
入力パラメーターを使って、PowerShell スクリプトを作成します。
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
ようになりましたが先ほど作成した監視可能な関数をサブスクライブする必要があります。 この PowerShell スクリプトを実行する関数を呼び出す必要があるを配置します。
```ts
this.getNodeName().subscribe(
     response => {
    console.log(response)
     }
);
```
CreateSession メソッドにノード名を用意すると、新しい PowerShell セッションが作成された、使用され、PowerShell の呼び出しの完了時に直ちに破棄します。 

### キーのオプション ###
PowerShell の API を呼び出すといくつかのオプションを利用できます。 セッションが作成されるたびに作成できますまたはキーがない場合。 

**キー:** これには、検索およびコンポーネント (つまり、Component1 キー「SME 岩、」を使用してセッションを作成できます、Component2 は、その同じセッションを使用できます) にわたる場合でも、再利用が可能なキーを持つセッションが作成されます。キーが指定した場合に作成されるセッションする必要がありますによって破棄呼び出し dispose() 上記の例で行ったようします。 セッションは、5 分以上の破棄されずにない保持する必要があります。 
```ts
  const session = this.appContextService.powerShell.createSession('{!TargetNode}', '{!Key}');
```

**キーを使用しない:** キーは、セッションに自動的に作成されます。 このセッションで 3 分後に自動的に破棄します。 キーを使用しないを使用すると、既にある利用可能なセッションの作成時にすべての実行空間の使用をリサイクルする拡張機能ができます。 Runspace 利用できない場合はより新しいファイルが作成されます。 この機能は、1 回限りの呼び出しに適していますが、パフォーマンスに影響が繰り返し使用します。 セッションを作成するには約 1 秒を受け取り、セッションをリサイクルため継続的に発生する可能性が低下します。

```ts
  const session = this.appContextService.powerShell.createSession('{!TargetNodeName}');
```
または 
``` ts 
const session = this.appContextService.powerShell.createAutomaticSession('{!TargetNodeName}');
```
ほとんどの状況でのキーを持つセッションを作成、```ngOnInit()```メソッド、およびでの dispose```ngOnDestroy()```します。 コンポーネントがコンポーネントの間で共有されませんが、基になるセッション内の複数の PowerShell スクリプトがある場合に、このパターンに従ってください。
最適な結果を得るには、セッションの作成がサービスではなく、コンポーネント内で管理されている - その有効期間を区別するかどうかを確認し、クリーンアップを適切に管理することができます。

最適な結果を得るには、セッションの作成がサービスではなく、コンポーネント内で管理されている - その有効期間を区別するかどうかを確認し、クリーンアップを適切に管理することができます。

### PowerShell のストリーム ###
実行時間の長いスクリプトとデータがある場合出力されるにつれて、PowerShell のストリームには、スクリプトを完了するまで待機することがなく、データを処理することができます。 監視可能な next() は、データを受信するとすぐに呼び出されます。
```ts
this.appContextService.powerShellStream.run(session, script);
```

### 長時間実行されているスクリプト ###
バック グラウンドで実行するには実行時間の長いスクリプトを使っている場合は、作業項目を送信できます。 スクリプトの状態は、ゲートウェイによって追跡され、ステータスの更新プログラムは、通知を送信できます。 
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
> 表示する進行状況は、書き込み進行状況を記述したスクリプトに含める必要があります。 例:
> ``` ps1
>  Write-Progress -Activity ‘The script is almost done!’ -percentComplete 95
>```

#### 作業項目のオプション ####

| function | 説明 |
| ----- | ----------- |
| submit() | 作業項目を送信します。 
| submitAndWait() | 作業項目を送信し、その実行の完了を待つ
| wait() | 既存の作業を待機項目を完了するには
| query() | Id によって既存の作業項目の照会
| find() | 既存の TargetNodeName、モジュール名、または typeId によって作業項目を見つけてします。

### PowerShell のバッチ Api 番号
複数のノードで同じスクリプトを実行する必要がある場合は、バッチの PowerShell セッションを使用できます。 例:
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


#### PowerShellBatch オプション ####
| オプション | 説明 |
| ----- | ----------- |
| runSingleCommand | 配列内のすべてのノードに対して 1 つのコマンドを実行します。 
| 実行 | ペアリングされたノードに対応するコマンドを実行します。
| キャンセル | 配列内のすべてのノード上でのコマンドをキャンセルします。