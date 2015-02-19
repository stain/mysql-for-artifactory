# mySQL Docker image tuned for Artifactory

Based on the [official mySQL image](https://registry.hub.docker.com/_/mysql/),
applying the recommended [mySQL tuning for Artifactory](https://www.jfrog.com/confluence/display/RTF/MySQL).

**Docker image:** [stain/mysql-for-artifactory](https://registry.hub.docker.com/u/stain/mysql-for-artifactory/)

## Usage with Artifactory

This image would typically be [linked to](https://docs.docker.com/userguide/dockerlinks/) 
from [artifactory-with-mysql](https://registry.hub.docker.com/u/stain/artifactory-with-mysql/):

    docker run --name mysql-for-artifactory-data -v /var/lib/mysql busybox
    docker run -d --volumes-from mysql-for-artifactory-data --name mysql-for-artifactory stain/mysql-for-artifactory
    docker run --name artifactory --link mysql-for-artifactory:mysql -p 8080:8080 stain/artifactory-with-mysql


## Details

This image sets up the database `artdb` with username `artifactory`
and password `password`, to match the defaults of
[$ARTIFACTORY_HOME/misc/db/mysql.properties](http://subversion.jfrog.org/artifactory/public/trunk/distribution/standalone/src/main/install/misc/db/mysql.properties).

The mySQL root password has also been set to `password`. 

`/var/lib/mysql` is exposed as a Docker volume - you will probably want to create a 
[Data volume container](https://docs.docker.com/userguide/dockervolumes/) as in the
example above.

It should not normally be needed to back up mySQL for Artifactory, as
you can instead use [Artifactory's
backup](https://www.jfrog.com/confluence/display/RTF/Managing+Backups).

