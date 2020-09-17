execute speedtest every minute `crontab -e`
```
* * * * * speedtest --format=csv | awk -F "\"*,\"*" '{print "speedtest_ping v="$3"\nspeedtest_upload v="$6*8"\nspeedtest_download v="$7*8}' | curl -XPOST "smarthub:8086/api/v2/write?bucket=telegraf/autogen&precision=s" --data-binary @-
```
