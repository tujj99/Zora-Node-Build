原作者https://docs.google.com/document/d/1FaENDk4AVP-jWCu5ab6xw3A_ZDJyW9VktTx8j-iAVf8/edit#heading=h.vqqlmaeomxyo
Zora node strategy by ardizor

服务器搭建好以后运行：

• 更新软件列表和软件包：

```
sudo apt-get update && sudo apt-get upgrade -y
```

• 安装运行节点所需的基本库：

```
sudo apt install curl build-essential git screen jq pkg-config libssl-dev libclang-dev ca-certificates gnupg lsb-release -y
```

• 接下来安装 Docker Compose

```
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

• 安装 Docker 及其依赖项：

```
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose
```

• 克隆 Conduit Github 存储库，即部署 Zora 节点的基础设施

```
git clone https://github.com/conduitxyz/node.git
```

• 进入node目录:

```
cd node
```

• 启动 Zora 主网文件夹的下载:

```
./download-config.py zora-mainnet-0
```

• 为 CONDUIT_NETWORK 变量设置一个值，告诉节点在 Zora主网启动：

```
export CONDUIT_NETWORK=zora-mainnet-0
```

• 在环境文件中输入 API 密钥，以便节点使用它运行。首先，创建一个.env文件：

```
cp .env.example .env
```

• 编辑文件:

```
nano .env
```

• 在 .env 文件中，用 Alchemy 账户的 API 密钥替换 <HTTP://...>。
  你可以在你的 Alchemy http://alchemy.com 账户上找到你的 API 密钥。
• 按CTRL+X, 再按Y ，再回车关闭文件

• 运行节点

```
screen -S zora
docker compose up --build
```

节点成功启动以后可以按CTRL+A+D退出Screen

如果想停止节点，先恢复screen，再按CTRL+C即可

```
screen -r zora
```
