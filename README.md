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
