# vehicletypenet-on-deepstream
vehicletypenet-on-deepstream は、DeepStream 上で VehicleTypeNet の AIモデル を動作させるマイクロサービスです。  

## 動作環境
- NVIDIA 
    - DeepStream
- VehicleTypeNet
- Docker
- TensorRT Runtime

## VehicleTypeNetについて
VehicleTypeNet は、画像内の車を検出し、６種類の車種に分類したカテゴリラベルを返すAIモデルです。  
VehicleTypeNet は、特徴抽出にResNet18を使用しており、混雑した場所でも正確に物体検出を行うことができます。  
なお、VehicleTypeNet は、DashCamNetのモデルで検知された車に対して、車種を分類するモデルのため、VehicleTypeNet のリソースと合わせて利用されます。  

## 動作手順
### Dockerコンテナの起動
Makefile に記載された以下のコマンドにより、VehicleTypeNet の Dockerコンテナ を起動します。
```
docker-run: ## Docker ストリーミング用コンテナを建てる
	docker-compose -f docker-compose.yaml up -d
```
### ストリーミングの開始
Makefile に記載された以下のコマンドにより、DeepStream 上の VehicleTypeNet でストリーミングを開始します。  
```
stream-start: ## ストリーミングを開始する
        xhost +
        docker exec -it deepstream-vehicletypenet deepstream-app -c /app/src/deepstream_app_source1_dashcamnet_vehiclemakenet_vehicletypenet.txt
```
## 相互依存関係にあるマイクロサービス  
本マイクロサービスを実行するために VehicleTypeNet の AIモデルを最適化する手順は、[vehicletypenet-on-tao-toolkit](https://github.com/latonaio/vehicletypenet-on-tao-toolkit)を参照してください。  


## engineファイルについて
engineファイルである vehicletypenet.engine は、[vehicletypenet-on-tao-toolkit](https://github.com/latonaio/vehicletypenet-on-tao-toolkit)と共通のファイルであり、当該レポジトリで作成した engineファイルを、本リポジトリで使用しています。  
