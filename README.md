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
