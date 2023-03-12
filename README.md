# Base Node Kurulum Rehberi
![image](https://user-images.githubusercontent.com/101635385/224575552-0347013d-400d-44a0-8ea7-955bb2fde062.png)


<h1 align="center"> Base Node </h1>
<h1 align="center"> Merhaba Base Node kurulum rehberi <br> << Hercules >>
</h1>

## 🟢 Ön bilgi

Base Node için herhangi bir teşvik yoktur isteyen kurabilir. Base bir Coinbase Markasıdır bu yüzden yapılacak her işlem önemli olduğunu düşünüyorum. <br>


### Linkler
 * [Hercules Node Telegram](https://t.me/HerculesNode)
 * [Hercules Twitter](https://twitter.com/Hercules4413)
 * [Base Dc](https://discord.gg/buildonbase)
 
 ## 🟢 Sistem özellikleri

Gereksinimler:
- 16 GB RAM
- 100 GB Yer


## 🟢 Sistem Güncelleme
```shell
sudo apt update
```

```shell
sudo apt upgrade
```


## 🟢 Docker Setup

```shell
apt install docker-compose
```

```shell

sudo apt-get update && sudo apt install jq && sudo apt install apt-transport-https ca-certificates curl software-properties-common -y && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - && sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable" && sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin && sudo apt-get install docker-compose-plugin

```
<br><br>

#### 🟢 1. Base Dosyalarını Klonlayalım.

```
git clone https://github.com/base-org/node.git
```

#### 🟢 2.Screen Oluşturalım
```
screen -S base
```

#### 🟢 3.Base Klasörüne Giriş yapalım
```
cd node
```

#### 🟢 4. Compose dosyasını düzenleyelim

docker-compose.yaml dosyasına giriş yapacağız ve buraya sadece ETH-Goerli RPC ekleyeceğiz bunu Blockpi , infura , Alchemy gibi yerlerden alabilirsiniz. 
<br><br>
Değiştireceğimiz yer : OP_NODE_L1_ETH_RPC=`https://ethereum-goerli-rpc.allthatnode.com`
<br>
Burada almış olduğunuz RPC ile değiştirin ve ctrl + x ile kaydedin.


```
nano docker-compose.yaml
```

![image](https://user-images.githubusercontent.com/101635385/224575903-f8e376ab-e7ff-42c9-bd11-3518a35e2092.png)



#### 🟢 5.Sistemi başlatalım 

<br>

bu işlem biraz sürecek bekleyin. Resimdeki gibi bir çıktı alacaksınız. <br>

```
docker compose up
```

![image](https://user-images.githubusercontent.com/101635385/224575974-59704a03-6f97-4831-9461-03fee8d00793.png)


işlemler bittikten sonra bu şekilde bir log göreceksiniz Senkronize oluyor . Şimdilik bu kadar

![image](https://user-images.githubusercontent.com/101635385/224576077-60d2aae7-5dbc-42a5-8881-42e7a29afb62.png)


<br>
#### 🟢 Yararlı komutlar


docker compose up yaptıktan sonra ana dizinde screen içinde değil aşağıdaki komutu girin ve resimdeki gibi çıktı almanız gerekiyor.

```
curl -d '{"id":0,"jsonrpc":"2.0","method":"eth_getBlockByNumber","params":["latest",false]}' \
  -H "Content-Type: application/json" http://localhost:8545
```
![image](https://user-images.githubusercontent.com/101635385/224576325-64d53939-3ea7-4527-84b9-e9f8f0aec477.png)

<br>


Senkronizasyon ilerlemesine bakma komutu ana dizinde yapın base screen içinde yapmayın ctrl + a + d ile çıkaiblirsiniz.

```
echo Latest synced block behind by: $((($(date +%s)-$( \
  curl -d '{"id":0,"jsonrpc":"2.0","method":"optimism_syncStatus"}' \
  -H "Content-Type: application/json" http://localhost:7545 | \
  jq -r .result.unsafe_l2.timestamp))/60)) minutes
```


Forklamayı ve beğenmeyi unutmayınız :)
