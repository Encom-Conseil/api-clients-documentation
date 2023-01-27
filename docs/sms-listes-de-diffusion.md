## Gestion des listes de diffusion

---

### Obtenir les listes de diffusion disponibles

**GET /api/v1/sms/recipientLists**

#### Paramètres :

- customerAccount * : compte client Encom.

#### Exemples de requête

##### Curl :

```
curl --request GET \
  --url 'https://telecom0585-clients.bluerocktel.net/api/v1/sms/recipientLists?customerAccount=CL3578' \
  --header 'authorization: Bearer {token} '
```

##### PHP :

```
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://telecom0585-clients.bluerocktel.net/api/v1/sms/recipientLists?customerAccount=CL3578",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "GET",
  CURLOPT_POSTFIELDS => "",
  CURLOPT_HTTPHEADER => array(
    "authorization: Bearer {token} "
  ),
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
} else {
  echo $response;
}
```

##### Python :

```
import http.client

conn = http.client.HTTPSConnection("telecom0585-clients.bluerocktel.net")

payload = ""

headers = { 'authorization': "Bearer {token} " }

conn.request("GET", "/api/v1/sms/recipientLists?customerAccount=CL3578", payload, headers)

res = conn.getresponse()
data = res.read()

print(data.decode("utf-8"))
```
#### Exemple de réponse :

```
[
  {
    "id": 1,
    "customerAccount": "CL3578",
    "name": "Clients Liste 1",
    "created_at": "2020-06-12 17:27:00",
    "updated_at": "2020-07-08 06:48:38"
  },
  {
    "id": 2,
    "customerAccount": "CL3578",
    "name": "Clients Liste 2",
    "created_at": "2020-07-08 06:49:05",
    "updated_at": "2020-07-08 06:49:05"
  },
  {
    "id": 3,
    "customerAccount": "CL3578",
    "name": "Prospects Liste 1",
    "created_at": "2020-07-08 06:49:26",
    "updated_at": "2020-07-08 06:49:40"
  }
]
```

---

### Créer une nouvelle liste de diffusion

**POST /api/v1/sms/recipientLists**

#### Paramètres :

- customerAccount * : compte client Encom
- name * : nom de la liste de diffusion

#### Exemples de requête

##### Curl :

```
curl --request POST \
  --url 'https://telecom0585-clients.bluerocktel.net/api/v1/sms/recipientLists?customerAccount=CL3578&name=Test%20%2B%2B%2B&id=7' \
  --header 'authorization: Bearer {token} '
```

##### PHP :

```
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://telecom0585-clients.bluerocktel.net/api/v1/sms/recipientLists?customerAccount=CL3578&name=Test%20%2B%2B%2B&id=7",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "POST",
  CURLOPT_POSTFIELDS => "",
  CURLOPT_HTTPHEADER => array(
    "authorization: Bearer {token} "
  ),
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
} else {
  echo $response;
}
```

##### Python :

```
import http.client

conn = http.client.HTTPSConnection("telecom0585-clients.bluerocktel.net")

payload = ""

headers = { 'authorization': "Bearer {token} " }

conn.request("POST", "/api/v1/sms/recipientLists?customerAccount=CL3578&name=Test%20%2B%2B%2B&id=7", payload, headers)

res = conn.getresponse()
data = res.read()

print(data.decode("utf-8"))
```

#### Exemple de réponse

Lorsque la liste est créée avec succès, l'API retourne un code "201 Created" ainsi qu'un tableau contenant l'id et le nom de la nouvelle liste :

```
{
  "id": 9,
  "name": "Test Cyrille"
}
```

---

### Renommer une liste de diffusion

**PUT /api/v1/sms/recipientLists**

#### Paramètres :

- customerAccount * : compte client Encom
- id * : id de la liste de diffusion
- name * : nouveau nom de la liste de diffusion

#### Exemples de requête

##### Curl :

```
curl --request PUT \
  --url 'https://telecom0585-clients.bluerocktel.net/api/v1/sms/recipientLists?customerAccount=CL3578&name=Test%20%2B%2B%2B&id=7' \
  --header 'authorization: Bearer {token} '
```
##### PHP :

```
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://telecom0585-clients.bluerocktel.net/api/v1/sms/recipientLists?customerAccount=CL3578&name=Test%20%2B%2B%2B&id=7",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "PUT",
  CURLOPT_POSTFIELDS => "",
  CURLOPT_HTTPHEADER => array(
    "authorization: Bearer {token} "
  ),
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
} else {
  echo $response;
}
```

##### Python :

```
import http.client

conn = http.client.HTTPSConnection("telecom0585-clients.bluerocktel.net")

payload = ""

headers = { 'authorization': "Bearer {token} " }

conn.request("PUT", "/api/v1/sms/recipientLists?customerAccount=CL3578&name=Test%20%2B%2B%2B&id=7", payload, headers)

res = conn.getresponse()
data = res.read()

print(data.decode("utf-8"))
```

#### Exemple de réponse

Lorsque la liste est créée avec succès, l'API retourne un code "200 ok" ainsi qu'un tableau contenant l'id et le nouveau nom de la liste :

```
{
  "id": 9,
  "name": "Nouveau nom de la liste"
}
```

---

### Supprimer une liste de diffusion

**DELETE /api/v1/sms/recipientLists**

#### Paramètres :

- customerAccount * : compte client Encom
- id * : id de la liste de diffusion

#### Exemples de requête

##### Curl :

```
curl --request DELETE \
  --url 'https://telecom0585-clients.bluerocktel.net/api/v1/sms/recipientLists?customerAccount=CL3578&id=7' \
  --header 'authorization: Bearer {token} '
```

##### PHP :

```
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://telecom0585-clients.bluerocktel.net/api/v1/sms/recipientLists?customerAccount=CL3578&id=7",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "DELETE",
  CURLOPT_POSTFIELDS => "",
  CURLOPT_HTTPHEADER => array(
    "authorization: Bearer {token} "
  ),
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
} else {
  echo $response;
}
```

##### Python :

```
import http.client

conn = http.client.HTTPSConnection("telecom0585-clients.bluerocktel.net")

payload = ""

headers = { 'authorization': "Bearer {token} " }

conn.request("DELETE", "/api/v1/sms/recipientLists?customerAccount=CL3578&id=7", payload, headers)

res = conn.getresponse()
data = res.read()

print(data.decode("utf-8"))
```

#### Exemple de réponse

Lorsque la liste est supprimée, l'API retourne un code "200 OK" ainsi que le message "deleted" :

```
{
  "response": "deleted"
}
```
Lorsque la liste n'existe pas, l'API retourne un code "404 Not found"  ainsi que le message "not found" :

```
{
  "response": "not found"
}
```