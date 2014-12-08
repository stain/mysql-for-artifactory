# mySQL Docker image tuned for Artifactory

Based on the [official mySQL image](https://registry.hub.docker.com/_/mysql/),
applying the recommended [mySQL tuning for Artifactory](https://www.jfrog.com/confluence/display/RTF/MySQL).

## Usage with Artifactory

This image would typically be [linked to](https://docs.docker.com/userguide/dockerlinks/) 
from [artifactory-with-mysql](https://registry.hub.docker.com/u/soilandreyes/artifactory-with-mysql/):

    sudo docker run --name mysql-for-artifactory mysql-for-artifactory
    sudo docker run --name artifactory --link mysql-for-artifactory:mysql soilandreyes/artifactory-with-mysql


## Details

This mage sets up the database `artdb` with username `artifactory`
and password `password`, to match the defaults of
[$ARTIFACTORY_HOME/misc/db/mysql.properties](http://subversion.jfrog.org/artifactory/public/trunk/distribution/standalone/src/main/install/misc/db/mysql.properties).

The mySQL root password has also been set to `password`. 

`/var/lib/mysql` is exposed as a Docker volume.

It should not normally be needed to back up mySQL for Artifactory, as
you can instead use [Artifactory's
backup](https://www.jfrog.com/confluence/display/RTF/Managing+Backups).

