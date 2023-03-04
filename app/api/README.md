# Azure Functions バックエンドサーバー

- scaffolding
```
cd app
func init LocalFunctionProj --typescript
cd LocalFunctionProj
func new --name HttpExample --template "HTTP trigger" --authlevel "anonymous"
```

- リソース作成
```
# リソースグループを作成する
az group create --name tanakacli-rg --location japaneast

# ストレージアカウントを作成する
az storage account create \
    --name tanakaclisa \
    --location japaneast \
    --resource-group tanakacli-rg \
    --sku Standard_LRS

# App Serviceプランを作成する
az appservice plan create \
    --name tanakaappcli \
    --resource-group tanakacli-rg \
    --sku B1 \
    --is-linux \
    --location japaneast

# Functionを作成する
az functionapp create \
    --name tanakaappcli \
    --resource-group tanakacli-rg \
    --consumption-plan-location japaneast \
    --runtime node \
    --runtime-version 18 \
    --functions-version 4 \
    --storage-account tanakaclisa \
    --os-type Linux
```

- デプロイ
```
yarn build
func azure functionapp publish tanakaapp
```

- クリーンアップ
```
az group delete --name AzureFunctionsQuickstart-rg
```