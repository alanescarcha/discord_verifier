![image](https://user-images.githubusercontent.com/126272940/221437702-8f3d6be1-79b5-47b3-b96f-acd3bc8349d4.png)

POST Request json example:
```JSON
{
    "signature": "9ce8d820f543c5a68f214da51cdad84b",
    "username": "testuser",
    "role":"release"
}
```

Signature being generated by hashing in md5:
```LUA
function GenerateSignature(username, role, secretKey)
    return md5(string.format("role%susername%s%s",
        role,
        username,
        secretKey
    ))    
end
```

Answer will be send also in JSON
```JSON
{
    "success": true,
    "code": "40918d702d719255338e2c84b4cdde5f"
}
```

# Environment variables
![image](https://user-images.githubusercontent.com/126272940/221438077-5fae0784-c212-41df-baaa-275681f6eef5.png)

#### SECRET
The secret key with which the signature will be generated can be any string

#### DB_URL
URL for database. Currently only mariadb supported
Example: `root:123456@tcp(localhost:40002)/verifier`

#### DISCORD_TOKEN
Discord bot token

#### DISCORD_GUILD
Discord server id

# Installation steps

#### 1. Install [Docker](https://docs.docker.com/engine/install/)

#### 2. Download & Open project directory in terminal and write `docker build . -t verifier:latest`

#### 3. Edit passwords and etc in docker-compose.yml

#### 4. `docker compose up -d`
