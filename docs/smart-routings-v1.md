## Routages intelligents (V1) 

---

Il est possible d'interroger l'Api Clients Encom, soit par rapport au numéro de l'appelant, soit par rapport à un code que celui-ci est invité à saisir.

En principe, votre call flow tentera d'abord de reconnaître l'appelant par son numéro, et ne l'invitera à saisir son code d'identification que s'il n'est pas déjà reconnu.

Une fois l'appelant identifié par l'une ou l'autre des méthodes, l'Api Clients Encom vous indiquera vers quelle file d'appels le diriger, mais aussi s'il est VIP et/ou sous contrat d'astreinte.

Note importante : le paramètre "customerAccount", qui correspond au compte client Encom, doit être passé dans toutes les requêtes vers l'API Clients Encom. En effet, le jeton d'identification est personnel et son détenteur peut dans certains cas avoir accès à plusieurs comptes clients.

### Déterminer la (ou les) file(s) d'appels de destinations en fonction du numéro de l'appelant

***GET /api/v1/smartRoutings**

#### Paramètres 

- customerAccount : mandatory
- number : mandatory
- format : json ou raw (json si non précisé)

#### Exemples de requête

##### Curl

```
#### Exemples de requête

##### Curl

```
curl --request GET \
  --url 'https://clients.encom-conseil.fr/api/v1/smartRoutings?customerAccount=CL0000&number=00331XXXXXXXX' \
  --header 'authorization: Bearer {token} '
```

##### PHP

```
<?php

$curl = curl_init();

curl_setopt_array($curl, [
  CURLOPT_URL => "https://clients.encom-conseil.fr/api/v1/smartRoutings?customerAccount=CL0000&number=00331XXXXXXXX",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "GET",
  CURLOPT_POSTFIELDS => "",
  CURLOPT_HTTPHEADER => [
    "Authorization: Bearer {token}"
  ],
]);

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
} else {
  echo $response;
}
```

##### Python

```
import http.client

conn = http.client.HTTPSConnection("clients.encom-conseil.fr")

payload = ""

headers = {
    'Authorization': "Bearer {token}"
    }

conn.request("GET", "/api/v1/smartRoutings?customerAccount=CL0000&number=0033XXXXXXXXX", payload, headers)

res = conn.getresponse()
data = res.read()

print(data.decode("utf-8"))
```

#### Réponse

L'Api retourne une réponse '400 bad request' si la requête est mal-formulée.

L'Api retourne une réponse '403 not authorized' si l'utilisateur n'a pas les droits suffisants sur le compte client.

Si une des quatre destinations possibles est explicitement précisée dans la requête, seule celle-ci est retournée : 

```
{
  "destination1": "207"
}
```
Si aucune destination n'est précisée, les 4 valeurs sont retournées :

```
{
  "destination1": "207",
  "destination2": "209",
  "destination3": "214",
  "destination4": "216"
}
```

Il est possible de recevoir les valeurs dans un format brut, séparées par des virgules, en ajoutant le couple paramètre/valeur "format/raw" dans la requête :

```
207,209,214,216
```
