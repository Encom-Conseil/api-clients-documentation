## Routages intelligents 

---

Il est possible d'interroger l'Api Clients Encom, soit par rapport au numéro de l'appelant, soit par rapport à un code que celui-ci est invité à saisir.

En principe, votre call flow tentera d'abord de reconnaître l'appelant par son numéro, et ne l'invitera à saisir son code d'identification que s'il n'est pas déjà reconnu.

Une fois l'appelant identifié par l'une ou l'autre des méthodes, l'Api Clients Encom vous indiquera vers quelle file d'appels le diriger, mais aussi s'il est VIP et/ou sous contrat d'astreinte.

Note importante : le paramètre "customerAccount", qui correspond au compte client Encom, doit être passé dans toutes les requêtes vers l'API Clients Encom. En effet, le jeton d'identification est personnel et son détenteur peut dans certains cas avoir accès à plusieurs comptes clients.

### Déterminer la file d'appels de destination en fonction du numéro de l'appelant

*****GET /api/{customerAccount}/customer/number/{number}**

#### Exemples de requête

##### Curl

```
curl --request GET \
  --url https://clients.encom-conseil.fr/api/{customerAccount}/customer/number/{number} \
  --header 'Authorization: Bearer {token}'
```

#### Réponse

Si le numéro de l'appelant est trouvé, la file d'appels correspondante est retournée sous forme de chaîne, par exemple : 900

S'il n'est pas trouvé, un message "not found" est envoyé au format JSON avec un code 404.

### Déterminer si l'appelant est VIP en fonction de son numéro

**GET /api/{customerAccount}/customer/isVipFromNumber/{number}**

#### Réponse

Si le numéro de l'appelant est trouvé, un message true (s'il est VIP) ou false (s'il ne l'est pas) est renvoyé au format JSON avec un code 200.

S'il n'est pas trouvé, un message "not found" est renvoyé au format JSON avec un code 404.

### Déterminer si l'appelant est sous contrat d'astreinte en fonction de son numéro

**GET /api/{customerAccount}/customer/hasOnCallDutyContractFromNumber/{number}**

#### Réponse

Si le numéro de l'appelant est trouvé, un message true (s'il est sous contrat d'astreinte) ou false (s'il ne l'est pas) est renvoyé au format JSON avec un code 200.

S'il n'est pas trouvé, un message "not found" est renvoyé au format JSON avec un code 404.

### Déterminer la file d'appels de destination en fonction du code saisi par l'appelant

**GET /api/{customerAccount}/customer/code/{code}**

#### Réponse

Si le code saisi par l'appelant est reconnu, la file d'appels correspondante est retournée sous forme de chaîne, par exemple : 900

S'il n'est pas reconnu, un message "not found" est envoyé au format JSON avec un code 404.

### Déterminer si l'appelant est VIP en fonction du code saisi

**GET /api/{cutomerAccount}/customer/isVipFromCode/{code}**

#### Réponse

Si le code saisi par l'appelant est reconnu, un message true (s'il est VIP) ou false (s'il ne l'est pas) est renvoyé au format JSON avec un code 200.

S'il n'est pas reconnu, un message "not found" est renvoyé au format JSON avec un code 404.

### Déterminer si l'appelant est sous contrat d'astreinte en fonction du code saisi

**GET /api/{customerAccount}/customer/hasOnCallDutyContractFromCode/{code}**

#### Réponse

Si le code saisi par l'appelant est reconnu, un message true (s'il est sous contrat d'astreinte) ou false (s'il ne l'est pas) est renvoyé au format JSON avec un code 200.

S'il n'est pas reconnu, un message "not found" est renvoyé au format JSON avec un code 404.

