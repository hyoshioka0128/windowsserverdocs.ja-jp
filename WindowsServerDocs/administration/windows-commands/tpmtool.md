---
title: tpmtool
description: トラステッドプラットフォームモジュールに関する情報を取得する tpmtool のリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: ashleytqy
ms.author: ashleytqy
manager: ronaldai
ms.date: 05/07/2019
ms.openlocfilehash: 6f529939304cb3992992d9587c2180f80f8a0f01
ms.sourcegitcommit: 9889f20270e8eb7508d06cbf844cba9159e39697
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/18/2020
ms.locfileid: "83551119"
---
# <a name="tpmtool"></a>tpmtool

このユーティリティは、[トラステッドプラットフォームモジュール (TPM)](https://docs.microsoft.com/windows/security/information-protection/tpm/trusted-platform-module-overview)に関する情報を取得するために使用できます。

>[!IMPORTANT]
>一部の情報はリリース前の製品に関することであり、正式版がリリースされるまでに大幅に変更される可能性があります。 Microsoft は、ここで提供される情報に関して、明示または黙示を問わず、いかなる保証も行いません。

このコマンドを使用する方法の例については、[例](#tpmtool_examples)を参照してください。

## <a name="syntax"></a>構文

```
tpmtool /parameter [<arguments>]
```
### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|getdeviceinformation|TPM の基本情報が表示されます。 情報フラグの値の意味については、[こちら](https://docs.microsoft.com/windows/desktop/SecProv/win32-tpm-isreadyinformation#parameters)を参照してください。|
|gatherlogs [出力ディレクトリのパス]|TPM ログを収集し、指定したディレクトリに格納します。 このディレクトリが存在しない場合は、作成されます。 既定では、これらは現在のディレクトリに配置されます。 生成される可能性があるファイルは次のとおりです。 </br>-TpmEvents</br>-TpmInformation .txt</br>-SRTMBoot dat</br>-SRTMResume. dat</br>-DRTMBoot dat</br>-DRTMResume dat</br>|
|drivertracing [開始/停止]|TPM ドライバーのトレースの収集を開始または停止します。 トレースログ TPMTRACE が生成され、現在のディレクトリに配置されます。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="examples"></a><a name=tpmtool_examples></a>例

TPM の基本情報を表示するには、次のように入力します。
```
tpmtool getdeviceinformation
```
TPM ログを収集して現在のディレクトリに配置するには、次のように入力します。
```
tpmtool gatherlogs
```
TPM ログを収集してに配置するには、次のように `C:\Users\Public` 入力します。
```
tpmtool gatherlogs C:\Users\Public
```
TPM ドライバーのトレースを収集するには、次のように入力します。
```
tpmtool drivertracing start
# Run scenario
tpmtool drivertracing stop
```

## <a name="decoding-error-codes"></a>エラーコードのデコード

TPM 固有のエラーコードについては、[こちら](https://docs.microsoft.com/windows/desktop/com/com-error-codes-6)を参照してください。
