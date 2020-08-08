---
title: 管理機能
description: System Insights では、機能ごとに構成できるさまざまな設定が公開されており、これらの設定を調整して、展開の特定のニーズに対応することができます。 このトピックでは、Windows 管理センターまたは PowerShell を使用して、各機能のさまざまな設定を管理する方法について説明します。これらの設定を調整する方法については、PowerShell の基本的な例と Windows 管理センターのスクリーンショットを示します。
ms.topic: article
author: gawatu
ms.author: gawatu
manager: mallikarjun.chadalapaka
ms.date: 6/05/2018
ms.openlocfilehash: e78afb47877bb908df81876afe01d2f60b853c70
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87996704"
---
# <a name="managing-capabilities"></a>管理機能

>適用先:Windows Server 2019

Windows Server 2019 では、System Insights は、機能ごとに構成できるさまざまな設定を公開しています。これらの設定は、展開の特定のニーズに対応するように調整できます。 このトピックでは、Windows 管理センターまたは PowerShell を使用して、各機能のさまざまな設定を管理する方法について説明します。これらの設定を調整する方法については、PowerShell の基本的な例と Windows 管理センターのスクリーンショットを示します。

>[!TIP]
>また、これらの短いビデオを使用して、System Insights の使用を開始し、自信を持って管理することもできます。[システムインサイトの概要10分](https://blogs.technet.microsoft.com/filecab/2018/07/24/getting-started-with-system-insights-in-10-minutes/)

このセクションでは PowerShell の例を紹介しますが、system [Insights powershell のドキュメント](https://aka.ms/systeminsightspowershell)を使用して、system insights 内のすべてのコマンドレット、パラメーター、パラメーターセットを確認できます。

## <a name="viewing-capabilities"></a>表示機能

開始するには、 **InsightsCapability**コマンドレットを使用して、使用可能なすべての機能を一覧表示します。

```PowerShell
Get-InsightsCapability
```
これらの機能は、System Insights 拡張機能にも表示されます。

![使用可能な機能を一覧表示する System Insights の概要ページ](media/overview-page-contoso.png)

## <a name="enabling-and-disabling-a-capability"></a>機能の有効化と無効化
各機能は、有効または無効にすることができます。 機能を無効にすると、その機能を呼び出すことができなくなり、既定以外の機能については、機能を無効にすると、その機能のすべてのデータコレクションが停止します。 既定では、すべての機能が有効になっているため、 **InsightsCapability**コマンドレットを使用して機能の状態を確認できます。

機能を有効または無効にするには、 **InsightsCapability**コマンドレットと**InsightsCapability**コマンドレットを使用します。

```PowerShell
Enable-InsightsCapability -Name "CPU capacity forecasting"
Disable-InsightsCapability -Name "Networking capacity forecasting"
```
これらの設定は、Windows 管理センターで [**有効**] または [**無効**] ボタンをクリックして選択した機能によって切り替えることもできます。

### <a name="invoking-a-capability"></a>機能の呼び出し
機能を呼び出すと、直ちに予測を取得する機能が実行され、管理者は Windows 管理センターの [**起動**] ボタンをクリックするか、 **InsightsCapability**コマンドレットを使用して、いつでも機能を呼び出すことができます。

```PowerShell
Invoke-InsightsCapability -Name "CPU capacity forecasting"
```

>[!TIP]
>機能の呼び出しがコンピューター上の重要な操作と競合しないようにするには、営業時間外に予測をスケジュールすることを検討してください。

## <a name="retrieving-capability-results"></a>機能の結果の取得
機能が呼び出されると、 **InsightsCapability**または**InsightsCapabilityResult**を使用して最新の結果が表示されます。 これらのコマンドレットは、各機能の最新の**状態**と**状態の説明**を出力します。各機能は、各予測の結果を表します。 **状態**と**状態の説明**のフィールドについては、機能についての[ドキュメント](understanding-capabilities.md)を参照してください。

さらに、 **InsightsCapabilityResult**コマンドレットを使用して、最後の30個の予測結果を表示し、予測に関連付けられたデータを取得することもできます。

```PowerShell
# Specify the History parameter to see the last 30 prediction results.
Get-InsightsCapabilityResult -Name "CPU capacity forecasting" -History

# Use the Output field to locate and then show the results of "CPU capacity forecasting."
# Specify the encoding as UTF8, so that Get-Content correctly parses non-English characters.
$Output = Get-Content (Get-InsightsCapabilityResult -Name "CPU capacity forecasting").Output -Encoding UTF8 | ConvertFrom-Json
$Output.ForecastingResults
```
System Insights 拡張機能は、予測履歴を自動的に表示し、JSON 結果の結果を解析して、各予測の直感的で忠実性の高いグラフを提供します。

![予測グラフと予測履歴を示す単一の機能ページ](media/cpu-forecast-2.png)

### <a name="using-the-event-log-to-retrieve-capability-results"></a>イベントログを使用して機能の結果を取得する
System Insights では、機能が予測を終了するたびにイベントがログに記録されます。 これらのイベントは、 **Microsoft-Windows-System insights/Admin**チャネルで表示されます。 system insights は、状態ごとに異なるイベント ID を発行します。

| 予測の状態 | イベント ID |
| --------------- | --------------- |
| [OK] | 151 |
| 警告 | 148 |
| 重大 | 150 |
| エラー | 149 |
| None | 132 |

>[!TIP]
>[Azure Monitor](https://azure.microsoft.com/services/monitor/)または[System Center Operations Manager](/system-center/scom/welcome?view=sc-om-1807)を使用してこれらのイベントを集計し、マシングループ全体で予測結果を表示します。


## <a name="setting-a-capability-schedule"></a>機能スケジュールの設定
要求時の予測に加えて、指定した機能が定義済みのスケジュールに基づいて自動的に呼び出されるように、各機能の定期的な予測を構成できます。 機能スケジュールを表示するには、 **InsightsCapabilitySchedule**コマンドレットを使用します。

>[!TIP]
>PowerShell のパイプライン演算子を使用すると、 **InsightsCapability**コマンドレットによって返されるすべての機能に関する情報を確認できます。

```PowerShell
Get-InsightsCapability | Get-InsightsCapabilitySchedule
```

定期的な予測は既定で有効になっていますが、 **InsightsCapabilitySchedule**および**InsightsCapabilitySchedule**コマンドレットを使用していつでも無効にすることができます。

```PowerShell
Enable-InsightsCapabilitySchedule -Name "Total storage consumption forecasting"
Disable-InsightsCapabilitySchedule -Name "Volume consumption forecasting"
```

各既定の機能は、毎日午前3時に実行されるようにスケジュールされています。 ただし、機能ごとにカスタムスケジュールを作成できます。 System Insights では、 **InsightsCapabilitySchedule**コマンドレットを使用して構成できるさまざまなスケジュールの種類がサポートされています。

```PowerShell
Set-InsightsCapabilitySchedule -Name "CPU capacity forecasting" -Daily -DaysInterval 2 -At 4:00PM
Set-InsightsCapabilitySchedule -Name "Networking capacity forecasting" -Daily -DaysOfWeek Saturday, Sunday -At 2:30AM
Set-InsightsCapabilitySchedule -Name "Total storage consumption forecasting" -Hourly -HoursInterval 2 -DaysOfWeek Monday, Wednesday, Friday
Set-InsightsCapabilitySchedule -Name "Volume consumption forecasting" -Minute -MinutesInterval 30
```
>[!NOTE]
>既定の機能では毎日のデータが分析されるので、これらの機能には毎日のスケジュールを使用することをお勧めします。 既定の機能の詳細について[は、こちら](understanding-capabilities.md)を参照してください。

Windows 管理センターを使用して、[**設定**] をクリックして各機能のスケジュールを表示および設定することもできます。 現在のスケジュールは、[**スケジュール**] タブに表示されます。また、GUI ツールを使用して、新しいスケジュールを作成することもできます。

![現在のスケジュールを表示している設定ページ](media/schedule-page-contoso.png)

## <a name="creating-remediation-actions"></a>修復アクションの作成
System Insights では、機能の結果に基づいてカスタム修復スクリプトを開始することができます。 各機能について、予測状態ごとにカスタム PowerShell スクリプトを構成できます。これにより、管理者は手動での介入を必要とする代わりに、自動的に修正措置を講じることができます。

修復アクションの例としては、ディスククリーンアップの実行、ボリュームの拡張、重複除去の実行、Vm のライブマイグレーション、Azure File Sync の設定などがあります。

各機能のアクションは、 **InsightsCapabilityAction**コマンドレットを使用して確認できます。

```PowerShell
Get-InsightsCapability | Get-InsightsCapabilityAction
```

**InsightsCapabilityAction**および**InsightsCapabilityAction**コマンドレットを使用して、新しいアクションを作成したり、既存のアクションを削除したりできます。 各アクションは、 **Actioncredential**パラメーターで指定された資格情報を使用して実行されます。

>[!NOTE]
>最初の System Insights リリースでは、ユーザーディレクトリ以外で修復スクリプトを指定する必要があります。 この問題は今後のリリースで修正される予定です。

```PowerShell
$Cred = Get-Credential
Set-InsightsCapabilityAction -Name "CPU capacity forecasting" -Type Warning -Action "C:\Users\Public\WarningScript.ps1" -ActionCredential $Cred
Set-InsightsCapabilityAction -Name "CPU capacity forecasting" -Type Critical -Action "C:\Users\Public\CriticalScript.ps1" -ActionCredential $Cred

Remove-InsightsCapabilityAction -Name "CPU capacity forecasting" -Type Warning
```

Windows 管理センターを使用して、[**設定**] ページの [**操作**] タブで修復アクションを設定することもできます。

![ユーザーが修復アクションを指定できる設定ページ](media/actions-page-contoso.png)


## <a name="additional-references"></a>その他の参照情報
System Insights の詳細については、次のリソースを参照してください。

- [システム インサイトの概要](overview.md)
- [機能について](understanding-capabilities.md)
- [機能の追加と開発](adding-and-developing-capabilities.md)
- [System Insights の FAQ](faq.md)