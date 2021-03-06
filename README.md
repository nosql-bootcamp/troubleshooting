# troubleshooting

## Manque de mémoire disque elastic

En cas d'erreur du type : 

```
[2022-02-15T09:21:59,449][WARN ][o.e.c.r.a.DiskThresholdMonitor] flood stage disk watermark [95%] exceeded on [zv1yO02SSTaewFX3UaSZdg][C:\progs\elasticsearch-8.0.0\data] free: 842.3mb[0.6%], all indices on this node will be marked read-only
```

Il faut désactiver la contrainte d'espace disque avec la requête suivant sur le cluster :

```
PUT /_cluster/settings
{
    "persistent": {
        "cluster.routing.allocation.disk.threshold_enabled": false
    }
}
```

## Problème avec twirl au lancement de l'application marvel-heroes

Pour résoudre ce souci, il faut empêcher intellij de surcharger la version sbt déclarée dans le projet ("disable version override") dans la popup qui apparâit au lancement de l'application.

## Autre souci au lancement de l'application via `~run`

Soyez sûr d'utiliser la version 11 de java (File -> Project Structure -> Langage version)


## failed to submit a listener notification task. event loop shut down (dans les logs de marvel heroes)

Un client redis a sans doute été mal fermé, après avoir fait un `redisClient.connect()` et exécuté la requête, il faut faire un `redisClient.close()` dans les méthodes redis.
