# sysbench

Nifty command-line tool to measure server performance.

    apt-get install sysbench

## CPU

    sysbench --test=cpu --cpu-max-prime=20000 run --num-threads=4

## Disk I/O

    sysbench --test=fileio --file-total-size=6G prepare
    sysbench --test=fileio --file-total-size=6G --file-test-mode=rndrw --max-time=300 --max-requests=0 --file-extra-flags=direct run
    sysbench --test=fileio --file-total-size=6G cleanup

## MySQL

    mysql -u root -p
    create database benchmark;
    sysbench --test=oltp --oltp-table-size=1000000 --mysql-db=benchmark --mysql-user=root --mysql-password=123456 prepare

    sysbench --test=oltp --oltp-table-size=1000000 --mysql-db=benchmark --mysql-user=root --mysql-password=123456 --max-time=60 --oltp-read-only=on --max-requests=0 --num-threads=8 run

## References

1. https://github.com/akopytov/sysbench
