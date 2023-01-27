## Messages vers une liste de diffusion

---

### Envoyer un message vers une liste de diffusion

**POST /api/v1/sms/groupedMessage**

#### Paramètres

- customerAccount * : compte client Encom
- smsRecipientListId * : identifiant de la liste de diffusion
- message * : texte du message
- type * : type du message, 't' pour 'transactionnel' ou 'm' pour marketing
- idSend: campagne d'envoi (facultatif)
- listener: url recevant la notification de résultat du message (facultatif)

Note : le paramètre 'customerAccount', qui correspond au compte client Encom, doit être passé dans toutes les requêtes vers l'API Clients Encom. En effet, le jeton d'identification est personnel et son détenteur peut dans certains cas avoir accès à plusieurs comptes clients.

##### Mention obligatoire "STOP AU 36111"

Attention : pour tout envoi de message à caractère marketing (type 'm'), la mention "STOP AU 36111" est obligatoire afin de fournir à vos destinataires un moyen de désinscription et de respecter les obligations de la CNIL. Lorsque vous postez un message de type marketing sur l'API en omettant cette mention, elle est automatiquement ajoutée à la fin de votre message.

##### Personnalisation des messages

Lorsque la liste de diffusion contient le noms des destinataires, il est possible de personnaliser les messages en indiquant "%%name%%" dans le message.

#### Exemples de requête

##### Curl

```
curl --request POST \
  --url 'https://telecom0585-clients.bluerocktel.net/api/v1/sms/groupedMessage?customerAccount=CL3578&message=Hello%20World!&type=t&smsRecipientListId=1' \
  --header 'authorization: Bearer {token} '
```

##### PHP

```
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => "https://telecom0585-clients.bluerocktel.net/api/v1/sms/groupedMessage?customerAccount=CL3578&message=Hello%20World!&type=t&smsRecipientListId=1",
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

##### Python

```
import http.client

conn = http.client.HTTPSConnection("telecom0585-clients.bluerocktel.net")

payload = ""

headers = { 'authorization': "Bearer {token} " }

conn.request("POST", "/api/v1/sms/groupedMessage?customerAccount=CL3578&message=Hello%20World!&type=t&smsRecipientListId=1", payload, headers)

res = conn.getresponse()
data = res.read()

print(data.decode("utf-8"))
```

#### Exemple de réponse

Lorsque les messages sont planifiés avec succès, l'API retourne un code "201 Created" ainsi que les ids des messages :

```
{
  "store": "22,23"
}
```

Vous pouvez ensuite obtenir le statut de chaque message envoyé en utilisant le  [endpoint GET /api/v1/sms/singleMessage](sms-messages-unitaires.md)