---
ms.assetid: b198d8ca-a5b7-430f-8911-5cbb9f50484c
title: fsutil リソース
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: b55063c3c5ea41b43573e6322b5efb36d2dad90e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59828333"
---
# <a name="fsutil-resource"></a>fsutil リソース
>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8、Windows Server 2008 R2、Windows 7、Windows 2008、Windows Vista

セカンダリ トランザクション リソース マネージャーを作成しますが起動またはトランザクション リソース マネージャーでは、停止またはトランザクション リソース マネージャーに関する情報が表示され、次の動作を変更します。

-   既定のトランザクション リソース マネージャーが、[次へ] のマウントにトランザクション メタデータをクリーンアップするかどうか

-   可用性経由での整合性を優先する指定したトランザクション リソース マネージャー

-   指定したトランザクション リソース マネージャーの一貫性より可用性を優先するには

-   特性のトランザクション リソース マネージャーを実行します。

このコマンドを使用する方法の例については、次を参照してください。[例](#BKMK_examples)します。

## <a name="syntax"></a>構文

```
fsutil resource [create] <RmRootPathname>
fsutil resource [info] <RmRootPathname>
fsutil resource [setautoreset] {true|false} <DefaultRmRootPathname>
fsutil resource [setavailable] <RmRootPathname>
fsutil resource [setconsistent] <RmRootPathname>
fsutil resource [setlog] [growth {<Containers> containers|<Percent> percent} <RmRootPathname>] [maxextents <Containers> <RmRootPathname>] [minextents <Containers> <RmRootPathname>] [mode {full|undo} <RmRootPathname>] [rename <RmRootPathname>] [shrink <percent> <RmRootPathname>] [size <Containers> <RmRootPathname>]
fsutil resource [start] <RmRootPathname> [<RmLogPathname> <TmLogPathname>
fsutil resource [stop] <RmRootPathname>

```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------------|---------------|
|作成|セカンダリ トランザクション リソース マネージャーを作成します。|
|<RmRootPathname>|トランザクション リソース マネージャーのルート ディレクトリにフルパスを指定します。|
|情報|指定したトランザクション リソース マネージャーの情報が表示されます。|
|setautoreset|既定のトランザクション リソース マネージャーが、[次へ] のマウントにトランザクション メタデータをクリーンアップするかどうかを指定します。<br /><br />-設定、 **setautoreset**パラメーターを**true**トランザクション リソース マネージャーが既定では、[次へ] のマウントにトランザクション メタデータをクリーンアップするを指定します。<br />-設定、 **setautoreset**パラメーターを**false**トランザクション リソース マネージャーが、既定では、[次へ] のマウントにトランザクション メタデータをクリーンアップできないことを指定します。|
|<DefaultRmRootPathname>|コロンの後にドライブ名を指定します。|
|setavailable|トランザクション リソース マネージャーが一貫性よりも可用性を優先するを指定します。|
|setconsistent|トランザクション リソース マネージャーが可用性経由での一貫性を好むことを指定します。|
|setlog|トランザクション リソース マネージャーの既に実行されている特性を変更します。|
|成長|トランザクション リソース マネージャーのログを拡張できる量を指定します。<br /><br />拡張パラメーターは、次のように指定できます。<br /><br />形式を使用して、コンテナーの数:*コンテナー***コンテナー**<br />-   パーセンテージ形式を使用します。*%***%**|
|<containers>|トランザクション リソース マネージャーによって使用されるデータ オブジェクトを指定します。|
|maxextent|指定したトランザクション リソース マネージャーのコンテナーの最大数を指定します。|
|minextent|指定したトランザクション リソース マネージャーのコンテナーの最小数を指定します。|
|モード {0} 完全&#124;を元に戻す}|すべてのトランザクションが記録されているかどうかを指定します (**完全**) またはのみロールバック イベントがログに記録されます (**を元に戻す**)。|
|rename|トランザクション リソース マネージャーの GUID を変更します。|
|shrink|トランザクション リソース マネージャーのログを自動的に小さくされる割合を指定します。|
|size|トランザクション リソース マネージャーのサイズを指定した数で指定*コンテナー*します。|
|start|指定したトランザクション リソース マネージャーを起動します。|
|stop|指定したトランザクション リソース マネージャーを停止します。|

### <a name="BKMK_examples"></a>例
トランザクション リソース マネージャーの 5 つのコンテナーを自動的に拡張して、c:\test で指定されているログを設定するには、次のように入力します。

```
fsutil resource setlog growth 5 containers c:test
```

トランザクション リソース マネージャーの 2 つのパーセントを自動的に拡張して、c:\test で指定されているログを設定するには、次のように入力します。

```
fsutil resource setlog growth 2 percent c:test
```

既定のトランザクション リソース マネージャーが、[次へ] のマウント ドライブ C 上のトランザクションのメタデータを削除することを指定するには、次のように入力します。

```
fsutil resource setautoreset true c:\  
```

### <a name="additional-references"></a>その他の参照情報
[コマンドライン構文キー](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)

[トランザクション NTFS](https://go.microsoft.com/fwlink/?LinkID=165402)


