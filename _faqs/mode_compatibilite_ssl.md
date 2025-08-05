---
layout: page
title: "Pourquoi sur certains anciens appareils la vue à propos indique: Mode de compatibité SSL activé ?"
---

Pour afficher les images de doris.ffessm.fr sur ces appareils plus anciens (Android Nougat ou antérieur), un mode de compatibilité est utilisé pour télécharger les images en raison d'une limitation de leur système d'exploitation.


<!--more-->

**Q :** Pourquoi un message concernant la sécurité SSL ou un mode de compatibilité apparaît-il sur mon appareil Android plus ancien ? / Pourquoi les images ne s'affichent-elles plus correctement ? (cf. [#226](https://github.com/doris-ffessm/doris-android/issues/226))

**R :** Sur certains appareils Android plus anciens (généralement ceux fonctionnant sous Android 7.0 Nougat, API 24, ou versions antérieures), vous pourriez rencontrer des difficultés pour afficher les images provenant du serveur https://doris.ffessm.fr ou voir une notification indiquant un mode de compatibilité.

**L'explication technique :**

Ceci est dû à l'évolution des standards de sécurité sur internet et à la manière dont les certificats SSL/TLS, qui sécurisent la connexion entre votre appareil et les serveurs, sont validés. Plus précisément, certains certificats racines nécessaires pour valider la chaîne de confiance des certificats modernes (comme ceux émis par l'autorité de certification Let's Encrypt, largement utilisée) ne sont plus présents ou ne sont plus mis à jour sur ces systèmes d'exploitation vieillissants.

Fin septembre 2021, un certificat racine important de Let's Encrypt (DST Root CA X3) a expiré. Bien que Let's Encrypt ait mis en place des solutions pour la majorité des systèmes, les appareils Android très anciens qui n'ont pas reçu de mises à jour de leur liste de certificats de confiance peuvent ne plus reconnaître la validité des nouveaux certificats émis pour des sites comme https://doris.ffessm.fr. Pour en savoir plus sur ce problème spécifique avec Let's Encrypt et les anciens appareils, vous pouvez consulter (en anglais) : [L'annonce de Let's Encrypt](https://letsencrypt.org/docs/dst-root-ca-x3-expiration-september-2021/)



**Notre solution pour assurer la continuité du service :** (cf. [https://github.com/doris-ffessm/doris-android/issues/226](https://github.com/doris-ffessm/doris-android/issues/226))

Afin de permettre à ces appareils plus anciens de continuer à afficher les images essentielles à l'application DORIS, nous avons mis en place un mécanisme de compatibilité. 

Sur les appareils concernés (ceux avec une version d'Android API 24 ou inférieure), la vérification stricte du certificat SSL pour le domaine https://doris.ffessm.fr est temporairement assouplie.

Un message informatif est présent dans la section "À Propos" de l'application sur les appareils où ce mode de compatibilité est actif.

**Quels sont les risques ?**

Nous estimons que le risque associé à cette mesure palliative reste très limité pour les raisons suivantes :

1.Nombre d'appareils concernés très faible : D'après les statistiques de la console Google Play, le nombre d'utilisateurs actifs sur des versions d'Android aussi anciennes est inférieur à une dizaine.

2.Source unique et identifiée : L'application télécharge des images exclusivement depuis une source unique et bien définie : https://doris.ffessm.fr. L'assouplissement ne concerne que cette source et ces données (les images). Il n'y a pas de manipulation de données sensibles (identifiants, mots de passe, etc.) via ce canal avec la sécurité ainsi ajustée.

Nous nous efforçons de maintenir la meilleure compatibilité possible tout en étant conscients des impératifs de sécurité. Cette solution vise à ne pas pénaliser les quelques utilisateurs encore sur ces plateformes anciennes pour l'accès aux images de DORIS. Idéalement, l'utilisation d'un appareil avec un système d'exploitation plus récent et régulièrement mis à jour est toujours recommandée pour une sécurité optimale.
