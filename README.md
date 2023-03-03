
- scaffolding
```
cd app
func init LocalFunctionProj --typescript
cd LocalFunctionProj
func new --name HttpExample --template "HTTP trigger" --authlevel "anonymous"
```

- リソース作成
```
az group create --name AzureFunctionsQuickstart-rg --location japaneast
az storage account create --name azurefunctionsquick --location japaneast --resource-group AzureFunctionsQuickstart-rg --sku Standard_LRS
az functionapp create --resource-group AzureFunctionsQuickstart-rg --consumption-plan-location japaneast --runtime node --runtime-version 18 --functions-version 4 --name tanakaapp --storage-account azurefunctionsquick
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