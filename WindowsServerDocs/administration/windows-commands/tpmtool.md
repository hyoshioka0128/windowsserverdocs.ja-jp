---
title: tpmtool
description: Tpmtool - の Windows コマンド」のトピックでは、トラステッド プラットフォーム モジュールに関する情報を取得します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
author: ashleytqy
ms.author: ashleytqy
manager: ronaldai
ms.date: 05/07/2019
ms.openlocfilehash: e125dbf6127b92c91e041c431f1e462e1f884168
ms.sourcegitcommit: 0ff812a80f654fa2c35b1632524e27841eca75c7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68230863"
---
# <a name="tpmtool"></a>tpmtool

このユーティリティを使用して、情報を取得すること、[トラステッド プラットフォーム モジュール (TPM)](https://docs.microsoft.com/windows/security/information-protection/tpm/trusted-platform-module-overview)します。

>[!IMPORTANT]
>一部の情報はリリース前の製品に関することであり、正式版がリリースされるまでに大幅に変更される可能性があります。 Microsoft は、ここで提供される情報に関して、明示または黙示を問わず、いかなる保証も行いません。

このコマンドを使用する方法の例については、[例](#tpmtool_examples)を参照してください。

## <a name="syntax"></a>構文

```
tpmtool /parameter [<arguments>]
```
## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|getdeviceinformation|TPM の基本情報が表示されます。 情報フラグの値の意味はあります[ここ](https://docs.microsoft.com/windows/desktop/SecProv/win32-tpm-isreadyinformation#parameters)します。|
|gatherlogs [出力ディレクトリのパス]|TPM のログを収集し、指定したディレクトリに配置します。 そのディレクトリが存在しない場合は作成されます。 既定では、現在のディレクトリにそれらに配置されます。 生成される可能なファイルは次のとおりです。 </br>-TpmEvents.evtx</br>-TpmInformation.txt</br>-SRTMBoot.dat</br>-SRTMResume.dat</br>-DRTMBoot.dat</br>-DRTMResume.dat</br>|
|drivertracing [開始/停止]|開始/TPM ドライバーのトレースの収集を停止します。 TPMTRACE.etl、トレース ログが生成され、現在のディレクトリに配置します。|
|parsetcglogs [-検証 (-v)]|次のように解析された TCG ログとも呼ばれる、Windows ブート構成ログ (WBCL) が表示されます。 最新のイベントの説明を確認できます、 [TCG の web サイト](https://trustedcomputinggroup.org/resource/pc-client-specific-platform-firmware-profile-specification/)**イベントの説明**します。 場合、`-validate`フラグを設定、TPM をプラットフォーム構成レジスタ (PCR) 値が、ログ内の値に一致することを検証します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="tpmtool_examples"></a>例

TPM の基本的な情報を表示するには、次のように入力します。
```
tpmtool getdeviceinformation
```
TPM のログを収集し、現在のディレクトリに配置、次のように入力します。
```
tpmtool gatherlogs
```
TPM のログを収集し、それらを配置する`C:\Users\Public`種類。
```
tpmtool gatherlogs C:\Users\Public
```
TPM ドライバーのトレースを収集するには、次のように入力します。
```
tpmtool drivertracing start
# Run scenario
tpmtool drivertracing stop
```
TCG ログを解析します。
```
tpmtool parsetcglogs
```
TCG ログを解析すると、PCRs の検証します。
```
tpmtool parsetcglogs -validate
```

## <a name="decoding-error-codes"></a>エラー コードの解読

TPM に固有のエラー コードが記載されている[ここ](https://docs.microsoft.com/windows/desktop/com/com-error-codes-6)します。
