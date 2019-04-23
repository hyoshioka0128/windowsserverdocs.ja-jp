---
title: 管理機能
description: システム Insights は、さまざまな機能ごとに構成できる設定を公開し、アドレスは、特定のデプロイのニーズがこれらの設定を調整できます。 このトピックでは、Windows Admin Center や PowerShell、PowerShell の基本的な例とこれらの設定を調整する方法を示す Windows Admin Center スクリーン ショットを提供することで各機能のさまざまな設定を管理する方法について説明します。
ms.custom: na
ms.prod: windows-server
ms.technology: system-insights
ms.topic: article
author: gawatu
ms.author: gawatu
manager: mallikarjun.chadalapaka
ms.date: 6/05/2018
ms.openlocfilehash: 9081a0b576ab9871b47df38255047b6cbe889419
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868023"
---
# <a name="managing-capabilities"></a>管理機能

>適用先:Windows Server 2019

Windows Server の 2019 でシステム Insights は、さまざまな機能ごとに構成できる設定を公開およびアドレスは、特定のデプロイのニーズがこれらの設定を調整できます。 このトピックでは、Windows Admin Center や PowerShell、PowerShell の基本的な例とこれらの設定を調整する方法を示す Windows Admin Center スクリーン ショットを提供することで各機能のさまざまな設定を管理する方法について説明します。 

>[!TIP]
>開始して、自信を持ってシステム Insights の管理に役立つ以下のショート ビデオを使用することもできます。[10 分後にシステム Insights の概要](https://blogs.technet.microsoft.com/filecab/2018/07/24/getting-started-with-system-insights-in-10-minutes/)

このセクションでは、PowerShell の例では、使用すること、[システム Insights の PowerShell ドキュメント](https://aka.ms/systeminsightspowershell)システム Insights 内のコマンドレット、パラメーター、およびパラメーターのセットのすべてを表示します。 

## <a name="viewing-capabilities"></a>表示の機能

最初に、すべての利用可能な機能を使用して一覧できます、 **Get InsightsCapability**コマンドレット。 

```PowerShell
Get-InsightsCapability
``` 
これらの機能でもシステム Insights 拡張機能表示されます。

![利用可能な機能を一覧表示するシステム Insights の [概要] ページ](media/overview-page-contoso.png)

## <a name="enabling-and-disabling-a-capability"></a>有効にして、機能を無効化
各機能を有効または無効にすることができます。 機能が呼び出される防止機能を無効にして、既定以外の機能の機能を無効にするとその機能のすべてのデータ収集を停止します。 既定では、すべての機能が有効になって、しを使用して、機能の状態を確認することができます、 **Get InsightsCapability**コマンドレット。 

有効または機能を無効にする、使用、**有効にする InsightsCapability**と**無効 InsightsCapability**コマンドレット。

```PowerShell
Enable-InsightsCapability -Name "CPU capacity forecasting"
Disable-InsightsCapability -Name "Networking capacity forecasting"
``` 
これらの設定を切り替えることもできますが、Windows Admin Center をクリックしてで機能の 1 つを選択します、**を有効にする**または**を無効にする**ボタン。

### <a name="invoking-a-capability"></a>機能の 1 つを呼び出す
機能をすぐに呼び出し、予測を取得する機能を実行し、管理者呼び出すことができます、機能をいつでもクリックして、 **Invoke** Windows Admin Center を使用してボタン、 **呼び出す InsightsCapability**コマンドレット。

```PowerShell
Invoke-InsightsCapability -Name "CPU capacity forecasting"
```

>[!TIP]
>コンピューターに重要な操作と競合しない機能の 1 つを呼び出すことを確認するには、予測のオフ業務時間中にスケジュール設定を検討してください。

## <a name="retrieving-capability-results"></a>機能の結果を取得します。
最新の結果では、表示を使用している機能の 1 つが呼び出された後**Get InsightsCapability**または**Get InsightsCapabilityResult**します。 これらのコマンドレットの最新出力**状態**と**状態の説明**の各機能は、各予測の結果について説明します。 **状態**と**状態の説明**フィールドの詳細に説明、[について機能ドキュメント](understanding-capabilities.md)します。 

また、使用することができます、 **Get InsightsCapabilityResult**最後の 30 の予測結果を表示して、予測に関連付けられているデータを取得するコマンドレット。 

```PowerShell
# Specify the History parameter to see the last 30 prediction results.
Get-InsightsCapabilityResult -Name "CPU capacity forecasting" -History

# Use the Output field to locate and then show the results of "CPU capacity forecasting."
# Specify the encoding as UTF8, so that Get-Content correctly parses non-English characters.
$Output = Get-Content (Get-InsightsCapabilityResult -Name "CPU capacity forecasting").Output -Encoding UTF8 | ConvertFrom-Json
$Output.ForecastingResults
```
システム Insights 拡張機能では、予測の履歴を表示し、JSON の結果、各予測のグラフを直感的で信頼性の高いを与えるの結果を解析します。

![予測グラフと予測の履歴を示す 1 つの機能 ページ](media/cpu-forecast-2.png)

### <a name="using-the-event-log-to-retrieve-capability-results"></a>イベント ログを使用して、機能の結果を取得するには
Insights のシステムでは、機能の 1 つは、予測を終了するたびにイベントを記録します。 これらのイベントは、 **Microsoft-Windows-システム-Insights/管理者**チャネル、およびシステム Insights は、各状態の別のイベント ID を発行します。   

| 予測の状態 | イベント ID |
| --------------- | --------------- |
| OK | 151 |
| 警告 | 148 |
| 重大 | 150 |
| エラー | 149 |
| なし | 132 |

>[!TIP]
>使用[Azure Monitor](https://azure.microsoft.com/services/monitor/)または[System Center Operations Manager](https://docs.microsoft.com/system-center/scom/welcome?view=sc-om-1807)をこれらのイベントを集計し、マシンのグループ間で予測結果を参照してください。


## <a name="setting-a-capability-schedule"></a>機能のスケジュールの設定
オンデマンドでの予測だけでなく、指定された機能は、定義済みのスケジュールに従って自動的に呼び出されるように、各機能の定期的な予測を構成できます。 使用して、 **Get InsightsCapabilitySchedule**機能のスケジュールを表示するコマンドレット。 

>[!TIP]
>PowerShell でパイプライン演算子を使用して、によって返されるすべての機能の情報を参照してください、 **Get InsightsCapability**コマンドレット。

```PowerShell
Get-InsightsCapability | Get-InsightsCapabilitySchedule
```

使用して、時間で無効にすることができますが、定期的な予測は既定で有効に、**有効にする InsightsCapabilitySchedule**と**無効 InsightsCapabilitySchedule**コマンドレット。

```PowerShell
Enable-InsightsCapabilitySchedule -Name "Total storage consumption forecasting"
Disable-InsightsCapabilitySchedule -Name "Volume consumption forecasting"
```

既定の各機能は、午前 3 時に毎日を実行する予定です。 ただし、機能ごとに、カスタム スケジュールを作成することができます、およびシステム Insights には、さまざまなスケジュールの種類を使用して構成できますがサポートしています、**セット InsightsCapabilitySchedule**コマンドレット。 

```PowerShell
Set-InsightsCapabilitySchedule -Name "CPU capacity forecasting" -Daily -DaysInterval 2 -At 4:00PM
Set-InsightsCapabilitySchedule -Name "Networking capacity forecasting" -Daily -DaysOfWeek Saturday, Sunday -At 2:30AM
Set-InsightsCapabilitySchedule -Name "Total storage consumption forecasting" -Hourly -HoursInterval 2 -DaysOfWeek Monday, Wednesday, Friday
Set-InsightsCapabilitySchedule -Name "Volume consumption forecasting" -Minute -MinutesInterval 30 
```
>[!NOTE]
>既定の機能は、1 日のデータを分析、ため、日単位のスケジュールを使用して、これらの機能にはお勧めします。 詳細については、既定の機能は[ここ](understanding-capabilities.md)します。

表示し、クリックして、機能ごとのスケジュールを設定する、Windows Admin Center を使用することもできます。**設定**します。 現在のスケジュールが表示されます、**スケジュール** タブは、新しいスケジュールを作成する GUI ツールを使用できます。

![設定ページが表示された現在のスケジュール](media/schedule-page-contoso.png)

## <a name="creating-remediation-actions"></a>修復アクションを作成します。
Insights のシステムでは、機能の 1 つの結果に基づくカスタム修復スクリプトを開始することができます。 機能ごとには管理者が手動の介入を必要とするのではなく、自動的に措置を実行できるため各予測状態のカスタムの PowerShell スクリプトを構成できます。 

サンプルの修復アクションには、実行中のディスク クリーンアップには、重複除去を Vm を移行して、Azure ファイル同期を設定するにはライブ実行されているボリュームの拡張が含まれます。

各機能を使用するためのアクションを確認できます、 **Get InsightsCapabilityAction**コマンドレット。

```PowerShell
Get-InsightsCapability | Get-InsightsCapabilityAction
```

新しいアクションを作成またはを使用して既存のアクションを削除することができます、**セット InsightsCapabilityAction**と**削除 InsightsCapabilityAction**コマンドレット。 アクションの実行で指定された資格情報を使用して、 **ActionCredential**パラメーター。

>[!NOTE]
>初期システム Insights リリースでは、ユーザーのディレクトリの外部で修復スクリプトを指定する必要があります。 これは、今後のリリースで修正されます。

```PowerShell
$Cred = Get-Credential
Set-InsightsCapabilityAction -Name "CPU capacity forecasting" -Type Warning -Action "C:\Users\Public\WarningScript.ps1" -ActionCredential $Cred
Set-InsightsCapabilityAction -Name "CPU capacity forecasting" -Type Critical -Action "C:\Users\Public\CriticalScript.ps1" -ActionCredential $Cred

Remove-InsightsCapabilityAction -Name "CPU capacity forecasting" -Type Warning
```

使用して修復アクションを設定する、Windows Admin Center を使用することもできます。、**アクション**タブ内で、**設定**ページ。

![ユーザーが修復アクションを指定するための設定ページ](media/actions-page-contoso.png)


## <a name="see-also"></a>関連項目
システム Insights に関する詳細については、するには、次のリソースを使用します。

- [システム Insights の概要](overview.md)
- [機能の理解](understanding-capabilities.md)
- [追加して、機能の開発](adding-and-developing-capabilities.md)
- [システム Insights に関する FAQ](faq.md)