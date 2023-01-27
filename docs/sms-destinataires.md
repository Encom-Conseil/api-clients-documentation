## Destinataires

---

### Obtenir les destinataires d'un liste de diffusion

**GET /api/v1/sms/recipients**

#### Paramètres :

- customerAccount * : compte client Encom
- smsRecipientListId * : id de la liste de diffusion

#### Exemples de requête :

##### Curl :

```
curl --request GET \
  --url 'https://telecom0585-clients.bluerocktel.net/api/v1/sms/recipients?customerAccount=CL3578&smsRecipientListId=1' \
  --header 'authorization: Bearer {token} '
```

##### PHP :

```
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://telecom0585-clients.bluerocktel.net/api/v1/sms/recipients?customerAccount=CL3578&smsRecipientListId=1",
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

conn.request("GET", "/api/v1/sms/recipients?customerAccount=CL3578&smsRecipientListId=1", payload, headers)

res = conn.getresponse()
data = res.read()

print(data.decode("utf-8"))
```

#### Exemple de réponse

L'API retourne un tableau contenant la liste des numéros, avec le nom correspondant s'il est disponible, ou *null* s'il ne l'est pas :

```
{
  "00336********": null,
  "00336********": "Jack"
}
```

---

### Ajouter un destinataire à une liste de diffusion

**POST /api/v1/sms/recipients**

#### Paramètres :

- customerAccount * : compte client Encom
- smsRecipientListId * : id de la liste de diffusion
- number * : numéro de téléphone mobile du destinataire
- name : nom du destinataire (facultatif)

#### Exemples de requête

##### Curl :

```
curl --request POST \
  --url 'https://telecom0585-clients.bluerocktel.net/api/v1/sms/recipients?customerAccount=CL3578&smsRecipientListId=1&number=0603790932' \
  --header 'authorization: Bearer {token} '
```
##### PHP : 

```
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://telecom0585-clients.bluerocktel.net/api/v1/sms/recipients?customerAccount=CL3578&smsRecipientListId=1&number=0603790932",
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

conn.request("POST", "/api/v1/sms/recipients?customerAccount=CL3578&smsRecipientListId=1&number=06********", payload, headers)

res = conn.getresponse()
data = res.read()

print(data.decode("utf-8"))
```

#### Exemple de réponse

Si le destinataire, identifié par son numéro de téléphone mobile, n'existe pas dans votre compte, il est créé puis attaché à la liste passée en paramètre.

Si le destinataire, identifié par son numéro de téléphone mobile, existe déjà dans votre compte, il n'est pas dupliqué mais attaché à liste passée en paramètre. Un même destinataire peut ainsi exister dans plusieurs listes de diffusion.

Dans les 2 cas, l'API retourne un code "201 Created'.