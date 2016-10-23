# d4m-nfs

With the Docker for Mac's (D4M) current implementation of osxfs, depending on how read and write heavy containers are on mounted volumes, performance can be abismal.

d4m-nfs blantently steals from the way that DockerRoot/xhyve used NFS mounts to get around i/o performance issues. With this implementation D4M appears to even outperform DockerRoot/xhyve under a full Drupal stack (mariadb/redis/php-fpm/nginx/varnish/haproxy), including persistent MySQL databases.

The advantage of this over a file sync strategy is simpler, less overhead and not having to duplicate files.

Please note:
* Only /Users/$USER directory is mounted, this might change if there is a request to be all user directories, or other locations.
* The /Users mount under D4M still exists and will continute to be slow, the d4m-nfs mount is under /mnt.
* When mounting Docker volumes, you need to change paths like /Users/$USER mounts with /mnt.
* To connect to the D4M moby linux VM use: screen -r d4m
* To disconnect from the D4M moby linux VM tty screen session use Ctrl-a d