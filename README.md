# Azure-Resources

<br />

### 参考情報
- <a href="https://docs.microsoft.com/ja-jp/azure/cloud-adoption-framework/ready/azure-best-practices/resource-naming">名前付け規則を定義する</a>

- <a href="https://docs.microsoft.com/ja-jp/azure/cloud-adoption-framework/ready/azure-best-practices/resource-abbreviations">Azure リソースの種類に推奨される省略形</a>

<br />

### リソースの展開
- [仮想ネットワーク](#仮想ネットワーク)
- [仮想ネットワーク with Azure Bastion](#仮想ネットワーク-with-azure-bastion)
- [Windows Server 仮想マシン](#windows-server-仮想マシン)
- [Windows Server 仮想マシン (IE セキュリティ強化の構成無効化)](#windows-server-仮想マシン-ie-セキュリティ強化の構成無効化)
- [SQL Server 仮想マシン](#sql-server-仮想マシン)
- [SQL Database](#sql-database)
- [ストレージ アカウント](#ストレージ-アカウント)
- [Azure Key Vault](#azure-key-vault)

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

## 仮想ネットワーク with Azure Bastion

<br />

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhiroyay-ms%2FAzure-Resources%2Fmain%2Ftemplates%2Fdeploy-vnet-two-subnet-with-bastion.json)

### パラメーター
- **virtualNetworkName**: 仮想ネットワーク名

- **location**: リージョン

- **addressPrefix**: IPv4 名前空間

- **subnetName1**: サブネット名

- **subnetPrefix1**: サブネット アドレス範囲

- **subnetName2**: サブネット名

- **subnetPrefix2**: サブネット アドレス範囲

- **bastionSubnetPrefix**: Azure Bastion を展開するサブネット アドレス範囲

- **bastionHostName**: Azure Bastion の名前

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

## Windows Server 仮想マシン (IE セキュリティ強化の構成無効化)

<br />

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhiroyay-ms%2FAzure-Resources%2Fmain%2Ftemplates%2Fdeploy-windows-vm-with-extension.json)

### パラメーター
- **virtualNetworkName**: 仮想マシンを展開する仮想ネットワーク

- **subnetName**: 仮想マシンを展開するサブネット

- **vnetResourceGroup**: 仮想ネットワークが所属するリソース グループ

- **virtualMachineName**: 仮想マシン名

- **osVersion**: OS イメージ（Windows Server 2012 R2, Windows Server 2016, Windows Server 2019, Windows Server 2022 から選択）

- **machineSize**: マシン サイズ（B, Dv3, Fv2 から選択）

- **storageType**: ストレージの種類（Standard_LRS, StandardSSD_LRS, Premium_SSD から選択）

- **adminUserName**: 管理者アカウント

- **adminPassword**: 管理者パスワード

- **publicIPAddress**: Public IP Address の作成

<br />

## SQL Server 仮想マシン

- SQL Server 認証有効化（アカウント名：SqlUser, パスワード：OS 管理者と同じ）

<br />

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhiroyay-ms%2FAzure-Resources%2Fmain%2Ftemplates%2Fdeploy-sqlserver-vm.json)


### パラメーター
- **virtualNetworkName**: 仮想マシンを展開する仮想ネットワーク

- **subnetName**: 仮想マシンを展開するサブネット

- **vnetResourceGroup**: 仮想ネットワークが所属するリソース グループ

- **location**: 仮想ネットワークを展開した地域

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

<br />

## ストレージ アカウント

- パフォーマンス： Standard
- 接続方法： パブリック エンドポイント（すべてのネットワーク）
- ルーティングの優先順位： Microsoft ネットワーク ルーティング

<br />

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhiroyay-ms%2FAzure-Resources%2Fmain%2Ftemplates%2Fdeploy-storage-account.json)

### パラメーター
- **storageAccountName**: ストレージ アカウント名（英数小文字のみ）

- **sku**: ストレージの冗長性

- **accessTier**: アクセス層

- **isContainerRestoreEnabled**: コンテナーのポイントタイムリストアの有効化

- **isBlobSoftDeleteEnabled**: BLOB の論理的な削除の有効化

- **isContainerSoftDeleteEnabled**: コンテナーの論理的な削除の有効化

- **isVersioningEnabled**: BLOB のバージョン管理の有効化

- **changeFeed**: BLOB の変更フィードの有効化

<br />

## Data Factory

- バージョン： V2
- リポジトリの種類： GitHub（後から構成も可）

<br />

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhiroyay-ms%2FAzure-Resources%2Fmain%2Ftemplates%2Fdeploy-data-factory.json)

### パラメーター
- **name**: 名前

- **vnetEnables**: マネージド仮想ネットワークの有効化

- **publicNetworkAccess**: 接続方法（パブリック エンドポイント or プライベート エンドポイント

- **gitConfigureLater**: 後で Git を構成する

- **gitAccountName**: GitHub アカウント

- **gitRepositoryName**: リポジトリ名

- **gitCollaborationBranch**: ブランチ名

- **gitRootFolder**: ルート フォルダー

<br />

## Azure Key Vault

- アクセスの有効化
  - Azure Virtual Machines (展開用)： false
  - Azure Resource Manager (テンプレートの展開用)： false
  - Azure Disk Encryption (ボリューム暗号化用)： false
- アクセス許可モデル： コンテナーのアクセス ポリシー
- 接続方法
  - パブリック エンドポイント（すべてのネットワーク）

<br />

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhiroyay-ms%2FAzure-Resources%2Fmain%2Ftemplates%2Fdeploy-key-vault.json)

### パラメーター
- **keyVaultName**: Key Vault 名

- **skuName**: 価格レベル（Standard or Premium）

- **enableSoftDelete**: 論理的な削除

- **softDeleteRetentionInDays**: 削除されたコンテナーを保持する日数

- **objectId**: 

<br />

### オブジェクト ID の取得
```
az ad user show --id "Email Address that is used to sign in to Azure" --query "objectId"
```