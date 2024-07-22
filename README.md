# Chasm-Network

> I'm flying tomorrow so I couldn't share the repo, sorry I'm throwing it at night so you don't fall behind in points.

#

> I installed my Chasm Network Scout Node and started collecting points, details:

> Any server with minimal hardware is enough.

> We run a single node.

#

#### Installation

```console
sudo apt update && sudo apt upgrade -y

for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done

sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

echo \
  “deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo “$VERSION_CODENAME”) stable” | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update


sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

sudo docker run hello-world
```

#

> We should have a fee Mantle token in our Testnet wallet, I think 0.10$ is enough.

> Then let's create a Chasm Season account [here](https://scout.chasm.net/private-mint), mint it and setup it.

> We need to create some accounts, in order:

> [Groq](https://console.groq.com/keys) - [OpenRouter](https://openrouter.ai/settings/keys) - [OpenAI](https://platform.openai.com/api-keys).

#

```console
nano .env
# we went into .env with nano.
# paste the following code block into it.
```

> I am writing the places you need to edit below the code block.

```console
PORT=3001
LOGGER_LEVEL=debug

# Chasm
ORCHESTRATOR_URL=https://orchestrator.chasm.net
SCOUT_NAME=
SCOUT_UID=
WEBHOOK_API_KEY=
# Scout Webhook Url, update based on your server's IP and Port
# e.g. http://123.123.123.123:3001/
WEBHOOK_URL=

# Chosen Provider (groq, openai)
PROVIDERS=groq
MODEL=gemma2-9b-it
GROQ_API_KEY=

# Optional
OPENROUTER_API_KEY=
OPENAI_API_KEY=
```
> Set Scout Name.

> Your Scout ID [Chasm Season](https://scout.chasm.net/new-scout) will show up in your account when you bring your mouse to the blurred parts.

> Webhook API is the same way.

> Webhook URL: http://IP_ADRESİNİZ:3001/ - edit your IP address and do it.

> Groq API in your Groq account.

> Openrouter and OpenAI keys you created above, get them from there.

#

> Then save with CTRL + X + Y ENTER and exit.

#

```console
# let's start our node.
docker pull johnsonchasm/chasm-scout
docker run -d --restart=always --env-file ./.env -p 3001:3001 --name scout johnsonchasm/chasm-scout

source ./.env
curl -X POST \
     -H “Content-Type: application/json” \
     -H “Authorization: Bearer $WEBHOOK_API_KEY” \
     -d '{“body”:“{\”model\“:\”gemma-7b-it\“,\”messages\“:[{\”role\“:\”system\“,\”content\“:\”You are a helpful assistant.\“}]}”}' \
     $WEBHOOK_URL
Those who receive a # port error can eliminate the error with these commands
sudo ufw allow 3001
sudo ufw allow 3001/tcp

# If we got OK output with this command, we are done.
curl localhost:3001

If the # command doesn't work, click on the link in the output of this command and look at the top left.
docker logs scout
```

> If the installation was successful, you will see your name at the end of the list [here](https://scout.chasm.net/leaderboard).

<img width=“1318” alt=“Screenshot 2024-07-20 00 44 02” src=“https://github.com/user-attachments/assets/45a468af-d186-4e2c-9f9b-614d5de92091”>
