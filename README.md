# aces-news-migration

## connect to docker external database
- Find the NAME_default of the docker service

      docker network ls
     > The NAME_default listed is what you will use for the database connection in settings.php but without _default

      'host' => 'database.NAME.internal',
- Test the connection

      lando ssh -s database -c "mysql -ulamp -plamp -h database.NAME.internal"

Example connection:

    $databases['migrate']['default'] = array (
      'database' => 'lamp',
      'username' => 'lamp',
      'password' => 'lamp',
      'prefix' => '',
      'host' => 'database.acescopy.internal',
      'port' => '',
      'namespace' => 'Drupal\\Core\\Database\\Driver\\mysql',
      'driver' => 'mysql',
    );

SQL Query Example:

    SELECT ln.nid, ln.type, fd.title, nb.body_value, nb.body_summary, nb.body_format FROM node ln LEFT JOIN node_field_data fd ON ln.nid = fd.nid INNER JOIN node__body nb ON ln.nid = nb.entity_id WHERE ln.type='news' ORDER BY ln.nid ASC

Migration information:

    lando drush mim aces_news --limit=20
    lando drush mr aces_news
    lando drush pmu aces_news_migration -y && lando drush pm:enable aces_news_migration -y
    lando drush mst aces_news -y && lando drush mrs aces_news -y

User creation:
https://www.drupal.org/node/1349632

## Installation with composer
<ol>
<li>Add the custom module</li><br/>
```
cd ~/illinois_framework/

composer config repositories.aces-news-migration '{"type": "vcs", "url": "https://github.com/aces-wms/aces-news-migration.git"}'
    
composer require aces-wms/aces-news-migration:^1.0

```

