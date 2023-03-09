![image](https://user-images.githubusercontent.com/126272940/221437702-8f3d6be1-79b5-47b3-b96f-acd3bc8349d4.png)

POST Request json example:

```JSON
{
  "signature": "9ce8d820f543c5a68f214da51cdad84b",
  "username": "testuser",
  "role": "release"
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

# Admin Requests

#### List All Roles
```bash
curl --location 'http://localhost:40000/admin/listRoles' \
--header 'admin_key: 123456'
```

#### Create OR Edit roles
```bash
curl --location 'http://localhost:40000/admin/editRole' \
--header 'admin_key: 123456' \
--header 'Content-Type: application/json' \
--data '{
    "name": "role_name",
    "role":"1234567890"
}'
```

#### Delete Role
```bash
curl --location 'http://localhost:40000/admin/deleteRole' \
--header 'admin_key: 123456' \
--header 'Content-Type: application/json' \
--data '{
    "name": "role_name"
}'
```

# Environment variables

- #### SECRET
  - The secret key with which the signature will be generated can be any string

- #### DISCORD_TOKEN
  - Discord bot token

- #### DISCORD_GUILD
  - Discord server id

- #### ADMIN_PASSWORD
  - Used as password to admin requests

# Installation steps

1. Install [Docker](https://docs.docker.com/engine/install/)

2. Run docker run. Do not forget to change tokens and passwords.
```bash
docker run -p 40000:80 --name=Verifier --env=SECRET=random_secret_password --env=ADMIN_PASSWORD=123456 --env=DISCORD_GUILD=server_id --env=DISCORD_TOKEN=discord_token --mount source=Verifier,target=/app/data --restart=always -d elleqt/verifier:latest
```

REST is now started on port `40000` (if you not changed it) with `/verify` endpoint
```BASH
curl --location 'http://localhost:40000/verify' \
--header 'Content-Type: application/json' \
--data '{
    "signature": "9ce8d820f543c5a68f214da51cdad84b",
    "username": "testuser",
    "role":"release"
}'
```

# Get Role

Just use interaction `/verify` in any discord channel on ur server

![image](https://user-images.githubusercontent.com/126272940/221445981-f522d105-218b-4fd4-a40e-d5b54656386c.png)
