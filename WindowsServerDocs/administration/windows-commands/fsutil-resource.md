---
ms.assetid: b198d8ca-a5b7-430f-8911-5cbb9f50484c
title: Fsutil リソース
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 678f3f98a96f44c146b73e9b6081884f8547373c
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725443"
---
# <a name="fsutil-resource"></a>Fsutil リソース
> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8、Windows Server 2008 R2、Windows 7、windows 2008、Windows Vista

セカンダリトランザクションリソースマネージャーを作成するか、トランザクションリソースマネージャーを開始または停止します。または、トランザクションリソースマネージャーに関する情報を表示し、次の動作を変更します。

-   次のマウント時に既定のトランザクションリソースマネージャーがトランザクションメタデータをクリーンアップするかどうか

-   可用性よりも一貫性を優先するように指定されたトランザクションリソースマネージャー

-   一貫性を維持して可用性を優先するように指定されたトランザクションリソースマネージャー

-   実行中のトランザクションリソースマネージャーの特性

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

#### <a name="parameters"></a>パラメーター

|        パラメーター        |                                                                                                                                                                                                                                        説明                                                                                                                                                                                                                                         |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         create          |                                                                                                                                                                                                                    セカンダリトランザクションリソースマネージャーを作成します。                                                                                                                                                                                                                     |
|    <RmRootPathname>     |                                                                                                                                                                                                        トランザクションリソースマネージャーのルートディレクトリへの完全パスを指定します。                                                                                                                                                                                                         |
|          info           |                                                                                                                                                                                                            指定されたトランザクションリソースマネージャーの情報を表示します。                                                                                                                                                                                                            |
|      setautoreset       | 既定のトランザクションリソースマネージャーが次のマウントでトランザクションメタデータをクリーンアップするかどうかを指定します。<p>-既定では、 **setautoreset**パラメーターを**true**に設定して、トランザクションリソースマネージャーが次のマウントでトランザクションメタデータをクリーンアップするように指定します。<br />- **Setautoreset**パラメーターを**false**に設定して、既定では、トランザクションリソースマネージャーが次のマウントでトランザクションメタデータを消去しないように指定します。 |
| <DefaultRmRootPathname> |                                                                                                                                                                                                                       ドライブ名の後にコロンを付けて指定します。                                                                                                                                                                                                                        |
|      setavailable       |                                                                                                                                                                                                 トランザクションリソースマネージャーが整合性よりも可用性を優先することを指定します。                                                                                                                                                                                                 |
|      setconsistent      |                                                                                                                                                                                                 トランザクションリソースマネージャーが可用性よりも一貫性を優先することを指定します。                                                                                                                                                                                                 |
|         growth          |                                                                                                                                                                                                  既に実行されているトランザクションリソースマネージャーの特性を変更します。                                                                                                                                                                                                  |
|         成長          |                                                                                                  トランザクションリソースマネージャーのログを拡張できる量を指定します。<p>拡張パラメーターは次のように指定できます。<p>-_コンテナー_**コンテナー**の形式を使用したコンテナーの数<br />-形式を使用した割合: _%_**%**                                                                                                   |
|      <containers>       |                                                                                                                                                                                                      トランザクションリソースマネージャーによって使用されるデータオブジェクトを指定します。                                                                                                                                                                                                       |
|        maxextent        |                                                                                                                                                                                                指定したトランザクションリソースマネージャーのコンテナーの最大数を指定します。                                                                                                                                                                                                |
|        minextent        |                                                                                                                                                                                                指定されたトランザクションリソースマネージャーのコンテナーの最小数を指定します。                                                                                                                                                                                                |
|  mode {full&#124;undo}  |                                                                                                                                                                                        すべてのトランザクションをログに記録するか (**完全**)、ロールバックされたイベントのみをログに記録するか (**元に戻す**) を指定します。                                                                                                                                                                                         |
|         rename          |                                                                                                                                                                                                                  トランザクションリソースマネージャーの GUID を変更します。                                                                                                                                                                                                                  |
|         shrink          |                                                                                                                                                                                              トランザクションリソースマネージャーのログを自動的に減らすことができる割合を指定します。                                                                                                                                                                                              |
|          size           |                                                                                                                                                                                              指定された*コンテナー*数として、トランザクションリソースマネージャーのサイズを指定します。                                                                                                                                                                                               |
|          start          |                                                                                                                                                                                                                    指定されたトランザクションリソースマネージャーを開始します。                                                                                                                                                                                                                    |
|          stop           |                                                                                                                                                                                                                    指定されたトランザクションリソースマネージャーを停止します。                                                                                                                                                                                                                     |

### <a name="examples"></a><a name="BKMK_examples"></a>例
C:\test によって指定されたトランザクションリソースマネージャーのログを設定するには、次のように入力します。

```
fsutil resource setlog growth 5 containers c:test
```

C:\test によって指定されたトランザクションリソースマネージャーのログを設定するには、次のように入力します。

```
fsutil resource setlog growth 2 percent c:test
```

既定のトランザクションリソースマネージャーで、次にドライブ C にマウントするときにトランザクションメタデータをクリーンアップするように指定するには、次のように入力します。

```
fsutil resource setautoreset true c:\  
```

### <a name="additional-references"></a>その他の参照情報
- [コマンド ライン構文の記号](command-line-syntax-key.md)

[Fsutil](Fsutil.md)

[トランザクション NTFS](https://go.microsoft.com/fwlink/?LinkID=165402)


