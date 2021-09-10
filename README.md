# Azure-Resources

<br />

### 参考情報
- <a href="https://docs.microsoft.com/ja-jp/azure/cloud-adoption-framework/ready/azure-best-practices/resource-naming">名前付け規則を定義する</a>

- <a href="https://docs.microsoft.com/ja-jp/azure/cloud-adoption-framework/ready/azure-best-practices/resource-abbreviations">Azure リソースの種類に推奨される省略形</a>

<br />

### リソースの展開
- [仮想ネットワーク](#仮想ネットワーク)
- [Windows Server 仮想マシン](#windows-server-仮想マシン)
- [SQL Server 仮想マシン](#sql-server-仮想マシン)
- [SQL Database](#sql-database)

<br />

## 仮想ネットワーク

<br />

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhiroyay-ms%2FAzure-Resources%2Fmain%2Ftemplates%2Fdeploy-vnet.json)

### パラメーター
- **virtualNetworkName**: 仮想ネットワーク名

- **location**: リージョン

- **addressPrefix**: IPv4 名前空間

- **subnetName1**: サブネット名

- **subnetPrefix1**: サブネット アドレス範囲

- **subnetName2**: サブネット名

- **subnetPrefix2**: サブネット アドレス範囲

<br />

## Windows Server 仮想マシン

<br />

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhiroyay-ms%2FAzure-Resources%2Fmain%2Ftemplates%2Fdeploy-windows-vm.json)

### パラメーター
- **virtualNetworkName**: 仮想マシンを展開する仮想ネットワーク

- **subnetName**: 仮想マシンを展開するサブネット

- **vnetResourceGroup**: 仮想ネットワークが所属するリソース グループ

- **virtualMachineName**: 仮想マシン名

- **osVersion**: OS イメージ（Windows Server 2012 R2, Windows Server 2016, Windows Server 2019 から選択）

- **machineSize**: マシン サイズ（B, Dv3, Fv2 から選択）

- **storageType**: ストレージの種類（Standard_LRS, StandardSSD_LRS, Premium_SSD から選択）

- **adminUserName**: 管理者アカウント

- **adminPassword**: 管理者パスワード

- **publicIPAddress**: Public IP Address の作成

### 提供イメージの取得
```PowerShell
Get-AzVMImageSku -Location WestUS2 -PublisherName "MicrosoftWindowsServer" -Offer "WindowsServer"
```

<br />

## SQL Server 仮想マシン

- SQL Server 認証有効化（アカウント名：SqlUser, パスワード：OS 管理者と同じ）

<br />

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhiroyay-ms%2FAzure-Resources%2Fmain%2Ftemplates%2Fdeploy-sqlserver-vm.json)


### パラメーター
- **virtualNetworkName**: 仮想マシンを展開する仮想ネットワーク

- **subnetName**: 仮想マシンを展開するサブネット

- **vnetResourceGroup**: 仮想ネットワークが所属するリソース グループ

- **virtualMachineName**: 仮想マシン名

- **osVersion**: OS イメージ（OS と SQL Server のバージョンを選択）

- **edition**: SQL Server エディション（Enterprise, Standard, Web, Express から選択）

- **machineSize**: マシン サイズ（B, Dv3, Fv2 から選択）

- **storageType**: ストレージの種類（Standard_LRS, StandardSSD_LRS, Premium_SSD から選択）

- **adminUserName**: 管理者アカウント

- **adminPassword**: 管理者パスワード

- **publicIPAddress**: Public IP Address の作成

<br />

### 提供イメージの取得（SQL Server）
```PowerShell
Get-AzVMImageOffer -Location $location -PublisherName "MicrosoftSQLServer"
```

```PowerShell
Get-AzVMImageSku -Location $location -PublisherName "MicrosoftSQLServer" -Offer $offerName
```

<br />

## SQL Database

- サーバー新規作成
- サービス レベル： 汎用目的
- コンピューティング レベル： プロビジョニング済み/サーバーレス
- ストレージ サイズ： 5GB
- ゾーン冗長性： false
- メンテナンス期間： 金曜日から日曜日 10:00PM から 6:00AM 太平洋標準時
- 接続ポリシー： Default
- Azure リソースからのアクセスを許可

<br />

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhiroyay-ms%2FAzure-Resources%2Fmain%2Ftemplates%2Fdeploy-sqldatabase-generalpurpose.json)

### パラメーター
- **sqlServerName**: SQL Server 名

- **sqlAdministratorLogin**: サーバー管理者

- **sqlAdministratorPassword**: パスワード

- **skuName**: コンピューティング レベル（プロビジョニング済み、サーバーレスを選択）

- **databaseName**: データベース名

- **collation**: 照合順序

- **backupStorage**: バックアップ ストレージの冗長性

<br />

### SKU の取得
```PowerShell
Get-AzSqlServerServiceObjective -Location $location | Where-Object {$_.Edition -eq "GeneralPurpose"}
```
